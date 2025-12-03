# 9장. 스마트 컨트랙트 보안

스마트 컨트랙트를 작성할 때 **보안**은 가장 중요한 고려사항 중 하나예요.  
실수는 금전적 손해를 초래하고, 공격자는 쉽게 이를 이용하죠. 이 장에서는 보안 베스트 프랙티스와 디자인 패턴을 살펴보고,  
컨트랙트에 취약점을 끌어올 수 있는 **보안 안티패턴**까지 함께 다뤄볼게요.

> 스마트 컨트랙트는 작성한 대로 정확히 실행돼요.  
> 그래서 프로그래머가 의도한 것과 다를 수 있고,  
> 모든 컨트랙트는 공개되어 있어 누구든지 트랜잭션을 보내서 상호작용할 수 있죠.  
> 취약점이 발견되면 손실은 거의 복구 불가능해요.  
> 따라서 베스트 프랙티스를 따르고 검증된 디자인 패턴을 활용하는 것이 필수적이에요.

## 보안 베스트 프랙티스

### 1️⃣ 민첩성 / 단순화
- 코드를 짜기 전, 모든 컴포넌트가 정말 필요한지 한 번 더 고민해보세요.  
- 구조를 정리한 뒤에도 코드 리뷰를 통해 줄 수 있는 줄이기, 예외 처리 최소화 등을 찾아보는 것이 좋아요.  
- 단순한 컨트랙트일수록 이해·테스트·감사하기가 훨씬 편하답니다.

### 2️⃣ 코드 재사용
- **“Wheel을 새로 만들지 말자”**라는 원칙이죠.  
- 이미 검증된 라이브러리(예: OpenZeppelin)를 활용하면,  
  “내가 쓴 코드보다 훨씬 안전하다”는 점을 기억하세요.  
- `DRY` 원칙을 지키며 중복 코드를 함수나 라이브러리로 바꾸면,
  보안 리스크를 줄일 수 있어요.

### 3️⃣ 코드 품질
- 스마트 컨트랙트는 **금전적 손실**이 바로 이어지는 환경이에요.  
- 일반 프로그래밍과 달리, 한 번 배포하면 수정이 거의 불가능합니다.  
- 따라서 **항상 철저한 테스트와 코드 리뷰**를 거쳐야 해요.

### 4️⃣ 가독성 / 감사 용이성
- 코드를 읽기 쉽고 문서화가 잘 되어 있으면,
  외부 감사를 받을 때 큰 도움이 돼요.  
- 커뮤니티의 지혜를 활용하려면, **공개 개발**과 오픈소스 방식을 권장합니다.

### 5️⃣ 테스트 범위
- 입력값이 항상 정당한지 가정하지 말고,
  모든 경계 조건을 테스트하세요.  
- 외부 호출(ether 전송 등)을 할 때는 반드시 반환 값을 확인해야 해요.

## 보안 위험과 안티패턴

### 🔒 재진입 공격 (Reentrancy)

#### 취약점
- 컨트랙트가 외부 주소에 ether를 보내면,
  상대방이 **fallback** 혹은 `receive`에서 다시 원래 함수로 호출할 수 있어요.  
- 이때, 아직 상태가 업데이트되지 않은 채로 재진입하면,
  공격자는 의도치 않게 자금을 빼낼 수 있죠.

#### 예시
```solidity
contract EtherStore {
    uint256 public withdrawalLimit = 1 ether;
    mapping(address => uint256) public lastWithdrawTime;
    mapping(address => uint256) balances;

    function depositFunds() public payable{
        balances[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(block.timestamp >= lastWithdrawTime[msg.sender] + 1 weeks);
        uint256 _amt = balances[msg.sender];
        if(_amt > withdrawalLimit){
            _amt = withdrawalLimit;
        }
        (bool res, ) = address(msg.sender).call{value: _amt}("");
        require(res, "Transfer failed");
        balances[msg.sender] = 0;
        lastWithdrawTime[msg.sender] = block.timestamp;
    }
}
```
- `address(msg.sender).call`이 **외부 호출**이라 재진입 공격의 포인트가 돼요.

#### 방어법
1. **check‑effect‑interaction 패턴**  
   상태를 먼저 갱신한 뒤 외부 호출을 수행합니다.
2. **ReentrancyGuard** 같은 라이브러리 사용  
   `nonReentrant` modifier로 재진입을 차단할 수 있어요.
3. 가능하면 `transfer`/`send` 대신 `call`을 쓰되, 반환값을 꼭 확인하세요.

> ⚠️ EIP‑1153(Transient Storage) 도입으로 **ReentrancyGuardTransient**가 등장했어요.  
> 이 기능은 트랜잭션 단위에서만 필요한 데이터를 저장해 가스 비용을 절감합니다.  
> 다만, EIP‑1153이 지원되는 체인에서만 사용 가능하니 주의하세요.

### 🔄 DELEGATECALL 안티패턴

#### 취약점
- `delegatecall`은 호출한 컨트랙트가 **자신의 저장소**를 그대로 사용해요.  
- 이로 인해, 라이브러리와 메인 컨트랙트 간에 슬롯이 충돌하면,
  예기치 않은 상태 변형이 발생할 수 있어요.

#### 예시
```solidity
contract FibonacciLib {
    uint256 public start;
    uint256 public calculatedFibNumber;

    function setStart(uint256 _start) public { start = _start; }
    ...
}
```
- `FibonacciBalance`가 이 라이브러리를 delegatecall 하면,
  **slot[0]**(라이브러리 주소)가 실제로는 `start` 변수와 겹쳐서
  예기치 않은 값이 저장될 수 있어요.

#### 방어법
- **stateless library**를 사용하세요.  
  라이브러리는 상태 변수를 갖지 않도록 설계하면,
  delegatecall 시 충돌 위험이 사라집니다.
- `delegatecall`을 꼭 필요할 때만 쓰고,  
  호출 전후에 저장소 구조가 어떻게 바뀔지를 명확히 파악하세요.

### 🔁 읽기 전용 재진입 (Read‑only Reentrancy)

- 외부 컨트랙트의 **view** 함수를 호출해 데이터를 읽을 때,
  그 컨트랙트가 내부적으로 state를 변경할 수 있는 콜백을 실행하면
  **불안정한 상태**를 반환받게 됩니다.  
- 이로 인해, 다른 컨트랙트가 잘못된 정보를 바탕으로 결정을 내릴 수 있어요.

### 🔧 검증되지 않은 CALL 반환값

- `call`, `send` 등은 실패 시 `false`를 반환하지만,
  **revert**하지 않으므로 개발자가 직접 확인해야 해요.  
- 예시: `Lotto` 컨트랙트에서 `winner`에게 ether를 보낼 때
  `send`의 반환값을 체크하지 않아, 성공 여부와 무관하게 상태가 변경됩니다.

### ⚡️ 전략적 가격 조작 (Price Manipulation)

- **오라클**이 제공하는 가격 정보를 부정확하게 만들면,
  대출 한도 초과, 담보 가치 왜곡 등 심각한 손실을 초래할 수 있어요.  
- 해결책: Chainlink, Pyth 같은 **분산형 오라클** 사용하고,
  TWAP(시간 가중 평균 가격)으로 단기 조작 방지.

### 🛡️ 잘못된 입력 검증 (Improper Input Validation)

- 주소가 `address(0)`인지, 배열 길이가 적절한지 등을
  반드시 확인해야 해요.  
- 예시: `Aggregator` 컨트랙트에서 사용자 입력으로 받은
  staking contract 주소를 검증하지 않아,
  악의적 계약을 호출해 거액 토큰을 탈취할 수 있었어요.

### 🔁 서명 재사용 공격 (Signature Replay Attack)

- 서명을 한 번만 사용하도록 **nonce**를 도입하고,
  `ecrecover` 대신 OpenZeppelin의 ECDSA 라이브러리를 활용하세요.  
- 또한, `abi.encodePacked` 대신 `abi.encode`를 쓰면
  입력값이 바뀌어도 같은 해시가 생성되는 문제를 방지할 수 있어요.

### ⚙️ 배포 및 업그레이드 시 잘못된 설정 (Misconfiguration)

- **업그레이드** 중 필수 변수 초기화를 빼먹으면,
  공격자가 컨트랙트를 제어할 수 있는 기회를 얻어요.  
- 예시: Ronin Bridge가 `_totalOperatorWeight`를 초기화하지 않아
  한 시간 만에 해킹이 발생한 사례.

## 결론

스마트 컨트랙트 보안은 **코드 작성** 단계에서부터 시작됩니다.  
검증된 라이브러리를 활용하고, 철저한 테스트와 리뷰를 거치며,
배포·업그레이드 과정에서도 설정을 꼼꼼히 확인해야 해요.

> “자신만의 암호화 코드를 만들지 말라”는 원칙이 있듯이,
> 스마트 컨트랙트에서도 **검증된 코드**를 최대한 재사용하는 것이
> 가장 안전하고 효율적인 방법입니다.  

---

### 📚 추가 자료

- Cyfrin Updraft Smart Contract Security and Auditing  
- Secureum Bootcamp  
- Ethernaut (OpenZeppelin Wargame)  
- Damn Vulnerable DeFi (CTF)  
- Capture the Ether, QuillCTF, Paradigm CTF 등  

이 외에도 다양한 온라인 리소스와 커뮤니티가 있으니,
계속해서 학습하고 실전 경험을 쌓아보세요!
