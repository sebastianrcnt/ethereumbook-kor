# 7장. 스마트 계약과 솔리디티

## 이더리움에서의 계정 종류
2장에서 언급했듯이, 이더리움에는 **EOA(Externally Owned Account)** 와 **컨트랙트 계정** 두 가지가 있어요.  
- **EOA** 는 사용자가 소유하고, 지갑 같은 외부 프로그램으로 제어돼요.  
- **컨트랙트 계정** 은 스마트 계약이라 불리는 프로그램 코드에 의해 제어돼요.

간단히 말하면, EOA는 코드나 데이터 저장소가 없고, 컨트랙트 계정은 둘 다 가지고 있어요. EOA는 외부에서 비밀키로 서명한 트랜잭션으로 조작되고, 컨트랙트 계정은 사전에 정의된 스마트 계약 코드를 따라 움직여요. 두 종류 모두 이더리움 주소로 식별돼요.

## 스마트 계약이란?
스마트 계약이라는 용어는 1990년대 Nick Szabo가 “디지털 형태의 약속 집합”이라고 정의했어요. 이후 비트코인과 같은 분산형 블록체인이 등장하면서 개념이 발전했죠.  
이 책에서는 **스마트 계약**을 EVM(이더리움 가상 머신) 안에서 실행되는 불변 컴퓨터 프로그램으로 정의해요.

### 핵심 정의
| 특성 | 의미 |
|------|------|
| **컴퓨터 프로그램** | 스마트 계약은 단순히 코드일 뿐이에요. “계약”이라는 말은 법적 의미가 없어요. |
| **불변(Immutable)** | 한 번 배포하면 코드는 바뀌지 않아요. 수정하려면 새 인스턴스를 배포해야 해요. |
| **결정론적(Deterministic)** | 같은 트랜잭션과 블록 상태에서 실행 결과는 항상 동일해요. |
| **EVM 컨텍스트** | 자신의 상태, 호출 트랜잭션의 컨텍스트, 최근 블록 정보만 접근 가능해요. |
| **분산형 월드 컴퓨터** | 모든 노드가 같은 초기 상태를 가지고 동일한 최종 상태를 만들어 하나의 “세계 컴퓨터”처럼 동작해요. |

## 스마트 계약 수명 주기
스마트 계약은 Solidity 같은 고급 언어로 작성돼요.  
1. **컴파일** → EVM 바이트코드로 변환  
2. **배포** → 컨트랙트 생성 트랜잭션(`to` 필드가 비어 있음)으로 배포  
3. **실행** → 외부에서 호출된 트랜잭션에 의해 실행돼요.

컨트랙트 계정은 사전 키가 없으니, “자기 자신을 제어”합니다.  
**중요:** 컨트랙트는 오직 트랜잭션이 호출할 때만 실행돼요. EOA에서 시작된 트랜잭션이 체인에 전달되면, 그 트랜잭션이 컨트랙트를 호출하고, 필요하면 다른 컨트랙트도 차례대로 호출해요.

## 이더리움 고급 언어 소개
EVM은 바이트코드만 실행할 수 있어요. 그래서 대부분의 개발자는 **고급 언어**(Solidity, Vyper 등)를 사용해 코드를 작성하고 컴파일러가 바이트코드로 변환하도록 해요.

### 주요 언어 목록 (인기순)
| 언어 | 특징 |
|------|------|
| **Solidity** | JavaScript/C++/Java와 비슷한 절차적(명령형) 문법. 가장 많이 쓰여요. |
| **Yul** | 중간 단계 언어로, 고급 최적화에 사용돼요. 초보자는 Solidity부터 시작하세요. |
| **Vyper** | Python 유사 문법으로 안전성을 강조해요. |
| **Huff** | 매우 낮은 수준의 코드로 효율성을 극대화해요. 초보자에게는 어려워요. |
| **Fe** | Rust/파이썬에서 영감을 받은 정적 타입 언어. 아직 초기 단계예요. |

## Solidity로 스마트 계약 만들기
Solidity는 Gavin Wood가 만든 언어로, 이더리움뿐 아니라 다른 EVM 기반 체인에서도 사용돼요.  
주요 도구는 **solc(솔리디티 컴파일러)**이며, ABI(응용 프로그램 바이너리 인터페이스)도 함께 관리해요.

### 버전 선택
Solidity는 **semantic versioning**(MAJOR.MINOR.PATCH)을 따르며, 현재 0.8.x 시리즈가 주류예요.  
```solidity
pragma solidity ^0.8.26;
```
위처럼 `^`를 붙이면 0.8.26 이하 버전은 허용되지 않아요.

### 설치 예시 (Ubuntu)
```bash
$ sudo add-apt-repository ppa:ethereum/ethereum
$ sudo apt update
$ sudo apt install solc
$ solc --version
```

## 간단한 Faucet 계약 예시
먼저 가장 기본적인 `Faucet` 계약을 살펴볼게요.

### 7‑1. Faucet.sol (기본)
```solidity
// SPDX-License-Identifier: GPL-3.0
contract Faucet {
    // 누구든지 요청하면 이더를 보내줘요
    function withdraw(uint _withdrawAmount, address payable _to) public {
        require(_withdrawAmount <= 100000000000000000); // 제한 금액
        _to.transfer(_withdrawAmount);
    }
    // 임의로 입금받을 수 있어요
    receive() external payable {}
}
```

### 컴파일
```bash
$ solc --optimize --bin Faucet.sol
```
결과는 이더리움 블록체인에 제출 가능한 16진수 바이트코드가 돼요.

## ABI(응용 프로그램 바이너리 인터페이스)
ABI는 스마트 계약의 함수와 이벤트를 외부에서 호출할 때 필요한 데이터 구조를 정의해줘요.  
```bash
$ solc --abi Faucet.sol
```
결과 예시:
```json
[
  {"inputs":[{"internalType":"uint256","name":"withdrawAmount","type":"uint256"}],
   "name":"withdraw",
   "outputs":[],"stateMutability":"nonpayable","type":"function"},
  {"stateMutability":"payable","type":"receive"}
]
```

## Solidity 버전 지정
```solidity
pragma solidity 0.8.26;
```
이렇게 하면 컴파일러가 해당 버전과 호환되는지 확인해요.

## Solidity 프로그래밍 기초

### 데이터 타입
| 타입 | 설명 |
|------|------|
| `bool` | true/false |
| `int`, `uint` | 부호 있는/없는 정수 (8~256 비트) |
| `address` | 20바이트 이더리움 주소 (`balance`, `transfer` 등 메서드 포함) |
| `bytes1 ~ bytes32` | 고정 길이 바이트 배열 |
| `bytes`, `string` | 가변 길이 바이트/문자열 |
| `enum` | 사용자 정의 열거형 (uint8 기반) |
| `array` | 정적·동적 배열 |
| `struct` | 여러 변수를 묶은 구조체 |
| `mapping` | 키→값 해시 테이블 |

#### 단위
- **시간**: `seconds`, `minutes`, `hours`, `days`
- **이더**: `wei`, `ether` (예: `0.1 ether`)

### 변수 정의와 범위
| 종류 | 설명 |
|------|------|
| **State 변수** | 계약에 영구 저장되는 데이터 (`public`, `private` 등 접근 제어 가능) |
| **Local 변수** | 함수 내부에서만 존재하는 임시 데이터 |
| **Global 변수** | EVM이 자동으로 제공하는 값(`block`, `msg`, `tx` 등) |

#### 예시
```solidity
uint public count; // State, 외부에서도 읽을 수 있음
```

### 전역 객체와 함수

- `msg.sender`, `msg.value`, `msg.data`
- `tx.gasprice`, `tx.origin`
- `block.number`, `block.timestamp`, `block.basefee` 등
- 주소 메서드: `transfer`, `send`, `call`, `delegatecall`, `staticcall`

### 함수 정의
```solidity
function foo(uint x) public view returns (uint) {
    return x + 1;
}
```
접근 제어(`public`, `private`, `internal`, `external`)와 상태 변경 여부(`pure`, `view`, `payable`)를 지정할 수 있어요.

#### 특별 함수
- **`receive()`**: 빈 calldata로 이더를 받을 때 호출돼요.
- **`fallback()`**: 존재하지 않는 함수를 호출했을 때 실행돼요. `payable` 옵션이 가능해요.

### 생성자(컨스트럭터)
```solidity
constructor() {
    owner = msg.sender;
}
```
배포 시 한 번만 실행돼요.

### 함수 수식어(Modifier)
```solidity
modifier onlyOwner {
    require(msg.sender == owner);
    _;
}
function changeOwner(address newOwner) public onlyOwner { ... }
```
`_`는 실제 함수 코드가 삽입되는 위치를 나타내요.

### 상속(Inheritance)
```solidity
contract Owned {
    address owner;
    constructor() { owner = msg.sender; }
    modifier onlyOwner { require(msg.sender == owner); _; }
}
contract Pausable is Owned {
    bool paused;
    modifier whenNotPaused { require(!paused); _; }
    function pause() public onlyOwner { paused = true; }
    function unpause() public onlyOwner { paused = false; }
}
contract Faucet is Pausable {
    function withdraw(uint amount) public whenNotPaused { ... }
}
```
상속을 통해 재사용성과 모듈화를 높일 수 있어요.

### 오류 처리
- `assert` : 내부 불변성 검사, 실패 시 모든 가스 소모  
- `require` : 입력값 검증, 실패 시 남은 가스 반환  
- `revert()` : 상태 롤백

```solidity
require(msg.sender == owner, "Only owner");
```

### 이벤트(Event)
이벤트는 트랜잭션 로그에 기록돼요. 외부 애플리케이션이 이를 구독해 실시간으로 알림을 받을 수 있어요.

```solidity
event Withdrawal(address indexed to, uint amount);
emit Withdrawal(msg.sender, withdrawAmount);
```

#### 예시: Faucet 계약에 이벤트 추가
```solidity
contract Faucet is Pausable {
    event Withdrawal(address indexed to, uint amount);
    event Deposit(address indexed from, uint amount);

    function withdraw(uint amount) public whenNotPaused {
        require(amount <= 0.1 ether);
        payable(msg.sender).transfer(amount);
        emit Withdrawal(msg.sender, amount);
    }

    receive() external payable {
        emit Deposit(msg.sender, msg.value);
    }
}
```

### 다른 계약 호출
- **새 인스턴스 생성**: `new ContractName()`  
- **기존 주소 캐스팅**: `ContractName(addr)` (위험)  
- **Low‑level call**: `call`, `delegatecall`, `staticcall`  

#### 예시: `call`
```solidity
(bool success, bytes memory data) = target.call(
    abi.encodeWithSignature("withdraw(uint256)", 0.1 ether)
);
require(success, "Call failed");
```

### 가스(Gas) 고려사항
- **동적 배열** 사용 시 과도한 가스 소모 위험  
- **다른 계약 호출** 시 예측 불가능한 가스 비용  
- **스토리지 접근**은 메모리보다 비싸므로 필요 시 캐시 활용  

#### 가스 추정
1. 현재 **베이스 프라이스** 확인 (`ethers.js`의 `getBlock("latest")`)  
2. 원하는 **팁(티핑)** 설정  
3. 예상 **가스 사용량**을 `estimateGas()` 로 계산  
4. 총 비용 = (베이스 + 팁) × 가스 사용량

## 마무리
이 장에서는 스마트 계약과 Solidity 언어를 깊게 다뤘어요. 간단한 Faucet 예제를 통해 변수, 함수, 이벤트, 상속, 오류 처리 등 핵심 개념을 차근차근 확장해 나갔죠. 다음 장에서는 Vyper라는 다른 계약 지향 언어를 살펴볼 거예요. 즐거운 코딩 되세요!
