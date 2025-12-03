# 10장. 토큰

**토큰(token)**이라는 말은 옛 영어 *tācen*에서 유래했어요. 그 뜻은 ‘표시’나 ‘상징’이죠. 보통은 교통권, 세탁권, 아케이드 게임용 토큰 같은 작은 가치를 가진 물리적 아이템을 일컫는 데 쓰여요. 하지만 블록체인에선 “블록체인 기반의 추상화 개념으로 소유할 수 있고 자산·통화·접근 권한 등을 나타내는 것”이라는 의미로 재정의되고 있어요.

물리적 토큰이 ‘작은 가치’라는 인식이 있었던 이유는 사용처가 한정돼 있었기 때문이에요. 특정 비즈니스, 조직, 장소에서만 쓰이고 교환하기 어려웠죠. 블록체인 토큰은 이런 제약을 없애거나 완전히 재정의할 수 있어요. 이제는 전 세계 어디서든 여러 목적에 동시에 사용되고 다른 토큰이나 화폐와 자유롭게 거래될 수 있답니다.

이 장에서는 토큰이 어떻게 만들어지고 어떤 용도로 쓰이는지, 그리고 그 속성(대체 가능성·내재성 등)을 살펴볼 거예요. 마지막으로 토큰을 만들고 실험해 보는 방법도 보여줄게요.

## 토큰은 어떻게 쓰여?

가장 눈에 띄는 용도는 디지털 개인 화폐이지만, 그 외에도 많은 기능이 겹쳐서 사용돼요. 예를 들어 한 토큰이 투표권·접근 권한·자산 소유권을 동시에 가질 수 있죠.

| **용도** | **설명** |
|---|---|
| **통화 (Currency)** | 개인 거래에서 가치가 결정되는 화폐 역할을 해요. |
| **리소스 (Resource)** | 공유 경제나 자원 공유 환경에서 사용되는 토큰(예: 저장공간, CPU). |
| **자산 (Asset)** | 금, 부동산, 자동차 등 실물·디지털 자산의 소유권을 나타내요. |
| **접근 (Access)** | 포럼, 독점 웹사이트, 호텔 방, 렌트카 같은 디지털·실제 재산에 대한 접근 권한을 줘요. |
| **주식 (Equity)** | DAO나 법인에서 주주 지분을 나타내는 토큰이죠. |
| **투표 (Voting)** | 디지털·법적 시스템에서 투표권을 부여해요. |
| **수집품 (Collectible)** | CryptoPunks 같은 디지털 수집품이나 그림 같은 물리적 수집품을 대표해요. |
| **신원 (Identity)** | 아바타 같은 디지털 신원, 혹은 국가 ID 같은 법적 신원을 나타내요. |
| **인증 (Attestation)** | 결혼 기록·출생 증명서·대학 학위 같은 공인 문서를 인증해요. |
| **유틸리티 (Utility)** | 서비스 접근이나 비용 지불에 쓰이는 토큰이죠. |

물리적 세계에서는 운전면허가 ‘인증’과 ‘신원’을 동시에 갖는 것처럼, 디지털 세계에서도 여러 기능을 한 토큰에 담아낼 수 있어요.

## 토큰과 대체 가능성 (Fungibility)

[위키피디아](https://oreil.ly/ge7zP)에서는 “대체 가능성은 개별 단위가 본질적으로 교환 가능한 물품·상품의 속성”이라고 정의해요. 토큰이 **대체 가능**하면, 어떤 단위를 다른 단위로 바꾸어도 가치나 기능에 차이가 없어요.

반대로 **비대체 가능 토큰(NFT)** 은 각각 고유한 실물·디지털 항목을 대표하기 때문에 서로 교환할 수 없죠. 예를 들어 특정 반고흐 그림의 소유권을 나타내는 토큰은 다른 피카소 토큰과 같은 가치가 아니에요. NFT마다 고유 식별자(시리얼 넘버)가 있어요.

다음 장에서 대체 가능·비대체 가능한 토큰 예를 살펴볼게요.

> **참고**  
> “대체 가능”이라는 용어는 보통 ‘현금으로 바로 교환될 수 있다’는 의미로 쓰이지만, 여기서는 단위가 서로 바뀌어도 가치에 차이가 없다는 뜻이에요.

## 대당사자 위험 (Counterparty Risk)

**대당사자 위험**은 거래 상대방이 의무를 이행하지 않을 가능성입니다. 예를 들어 귀금속 예치증서를 보유하고 판매하는 경우, 세 명 이상(판매자·구매자·보관자)이 관여해요. 물리적 자산을 보유한 사람이 거래를 완수해야 하므로 추가 위험이 발생합니다.

토큰으로 간접적으로 자산을 거래하면 보통 **보관자**가 필요해요. 그 보관자가 실제 자산을 가지고 있는지, 토큰 전송에 따라 소유권이 이전되는지를 확인해야 해요. 디지털 토큰과 물리적 자산을 연결할 때는 이 점을 꼭 명심하세요.

## 토큰과 내재성 (Intrinsicality)

**내재성(intrinsic)**은 ‘속 안에서’라는 뜻이에요. 블록체인에 직접 존재하는 디지털 아이템(예: CryptoKitty)은 **내재 자산**이라 부르죠. 이 경우, 토큰을 보유하면 별도의 중개자가 없으므로 대당사자 위험이 없습니다.

반면 실물 자산(부동산·주식·금 등)을 대표하는 토큰은 **외래 자산**입니다. 법률·관습·정책에 따라 관리되며, 블록체인 외부에서 보유됩니다. 따라서 보관자와 기록 시스템이 필요해 대당사자 위험이 존재합니다.

블록체인 기반 토큰의 가장 큰 장점은 외래 자산을 내재 자산으로 전환해 대당사자 위험을 제거할 수 있다는 점이에요. 예를 들어 기업 주식(외래)을 DAO 지분 토큰(내재)으로 바꾸는 것이죠. 스테이블코인도 마찬가지로 화폐에 연결된 외래 자산(국채·현금 등)을 기반으로 한 내재 토큰이랍니다.

## 유틸리티, 주식, 아니면 현금 사냥?

거대 이더리움 프로젝트가 대부분 토큰을 발행하지만, 정말 필요할까요? “모든 것을 토큰화하라”는 슬로건은 매력적이지만 현실은 훨씬 복잡해요. 토큰은 커뮤니티를 조직하고 인센티브를 주는 강력한 도구가 될 수 있지만, 투기·흥분과도 동반돼요.

### 이론상 두 가지 주요 목적

1. **유틸리티 토큰** – 특정 생태계에서 서비스나 자원에 접근할 수 있게 해주는 토큰.  
2. **주식 토큰** – 회사 주식처럼 소유권·통제권을 나타내는 토큰.

실제로는 이 구분이 모호해요. 많은 유틸리티 토큰은 투기적이며, 주식형 토큰은 실제 거버넌스 권한을 제공하지만 의미 있는 참여를 보장하지 못할 때가 많습니다.

> **참고**  
> 2025년 1월에 트럼프 전 대통령이 만든 밈 코인이 하루 만에 시가총액 150억 달러를 기록했어요. 이는 토큰이 실제 가치보다 흥분을 이끌어내는 사례예요.

### 좋은 토큰인가?

토큰은 선악이 아니라 설계·구현 방식에 따라 가치를 결정해요. 실제로 유용한 토큰과 단순히 자금 조달 도구인 토큰을 구별하려면 다음 질문을 던져보세요.
- 이 토큰이 프로토콜에서 꼭 필요한가?  
- 없으면 프로젝트가 잘 돌아갈까?

정직하게 답하면 진짜 혁신인지 마케팅에 불과한지 판단할 수 있어요.

## “오리” 같은 토큰

스타트업은 오랫동안 토큰을 자금 조달 도구로 활용해왔어요. 하지만 공개 증권 발행은 대부분 규제 대상이죠. 토큰을 ‘유틸리티 토큰’이라 부르며 증권이 아니라는 주장을 해왔지만, 실제로는 “오리처럼 보이고 물음표처럼 울리는 것”이라면 여전히 증권으로 분류될 수 있어요.

SEC(미국 증권거래위원회)는 최근 몇 년간 토큰 오퍼링에 대해 점점 강경한 입장을 취해왔어요. 예를 들어 2020년 Ripple Labs의 XRP가 등록되지 않은 증권이라고 주장했죠. 이더리움 자체도 2018년에 ‘분산화’라며 증권이 아니라고 했지만, 2024년 PoS 전환 시 스테이킹 보상이 배당과 유사해 다시 검토 대상이 되었어요.

법적 프레임워크는 블록체인 이전에 만들어졌기 때문에 토큰을 평가하기 어려워요. 투자자 보호와 혁신 촉진 사이에서 균형을 잡아야 해요.

## 이더리움 토큰

블록체인 토큰은 이더리움이 등장하기 전에도 존재했어요. 비트코인이 첫 번째 토큰이라 할 수 있죠. 하지만 이더리움의 **첫 토큰 표준**(ERC-20)이 도입되면서 토큰 붐이 일어났어요.

### ERC‑20 토큰 표준

2015년 11월, Fabian Vogelsteller가 제안한 ERC‑20은 대체 가능한 토큰을 위한 인터페이스를 정의해요. 주요 함수와 이벤트는 다음과 같아요:

| 함수/이벤트 | 설명 |
|---|---|
| `totalSupply()` | 현재 존재하는 총 공급량 반환 |
| `balanceOf(address)` | 주소의 잔액 조회 |
| `transfer(to, value)` | 토큰 전송 |
| `transferFrom(from, to, value)` | 승인된 토큰 전송 |
| `approve(spender, value)` | 특정 주소에 허용량 부여 |
| `allowance(owner, spender)` | 남은 허용량 조회 |
| `Transfer` 이벤트 | 전송 시 발생 |
| `Approval` 이벤트 | 승인 시 발생 |

옵션으로는 이름(`name()`), 심볼(`symbol()`), 소수점(`decimals()`)이 있어요.

#### Solidity 예시

```solidity
contract ERC20 {
    function totalSupply() public view returns (uint256 theTotalSupply);
    function balanceOf(address _owner) public view returns (uint256 balance);
    function transfer(address _to, uint256 _value) public returns (bool success);
    function transferFrom(address _from, address _to, uint256 _value) public returns (bool success);
    function approve(address _spender, uint256 _value) public returns (bool success);
    function allowance(address _owner, address _spender) public view returns (uint256 remaining);
    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
}
```

#### 데이터 구조

```solidity
mapping(address account => uint256) _balances;
mapping(address account => mapping(address spender => uint256)) public _allowances;
```

### ERC‑20 워크플로우

1. **단일 트랜잭션** – `transfer`  
   가장 흔한 방식으로, 한 번의 호출만으로 토큰을 보낼 수 있어요.

2. **두 단계(approve + transferFrom)**  
   계약이 토큰을 전송하도록 허용하고, 이후 실제 전송을 수행해요. 주로 ICO나 거래소에서 사용돼요.

#### 예시 이미지

![ERC‑20 두 단계](images/ch10/maet_1001.png)

> **참고**  
> ICO(Initial Coin Offering)는 기업이 토큰을 판매해 자금을 모으는 방식이에요. IPO와 비슷하지만 규제가 덜한 편이죠.

### ERC‑2612: Gasless Transfers

ERC‑2612는 `permit` 메커니즘으로 가스 없이 토큰 전송을 승인할 수 있게 해줘요. 사용자는 서명만 하면 되고, 실제 트랜잭션은 다른 사람이 제출해요. 이는 특히 스마트 월렛(EIP‑4337 등)과 결합하면 유용합니다.

### ERC‑20 구현

OpenZeppelin의 `ERC20` 구현이 가장 많이 쓰이고 있어요. 보안에 중점을 두고 지속적으로 업데이트됩니다.

## 우리만의 ERC‑20 토큰 만들기 (Foundry 사용)

1. **프로젝트 생성**

```bash
$ mkdir METoken
$ cd METoken
$ forge init
```

2. **OpenZeppelin 설치**

```bash
$ forge install OpenZeppelin/openzeppelin-contracts
```

3. **토큰 계약 작성** (`METoken.sol`)

```solidity
pragma solidity 0.8.28;
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract METoken is ERC20 {
    constructor(uint256 initialSupply) ERC20("METoken", "MET") {
        _mint(msg.sender, initialSupply);
    }
}
```

4. **컴파일**

```bash
$ forge build
```

5. **배포 스크립트** (`METokenDeploy.s.sol`)

```solidity
pragma solidity 0.8.28;
import {Script, console} from "forge-std/Script.sol";
import {METoken} from "../src/METoken.sol";

contract METokenDeployer is Script {
    METoken public _METoken;

    function run() public {
        vm.startBroadcast();
        _METoken = new METoken(50_000_000e18);
        vm.stopBroadcast();
    }
}
```

6. **배포 실행** (Anvil 로컬 체인 사용)

```bash
$ forge script script/METokenDeploy.s.sol --broadcast --rpc-url "http://127.0.0.1:8545" --private-key <DEPLOYER_PRIVATE_KEY>
```

7. **상호작용 예시** (`METokenInteraction.s.sol`)

```solidity
pragma solidity 0.8.28;
import {Script, console} from "forge-std/Script.sol";
import {METoken} from "../src/METoken.sol";

contract METokenInteraction is Script {
    METoken public _METoken = METoken(0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512);
    address alice = 0x70997970C51812dc3A010C7d01b50e0d17dc79C8;

    function run() public {
        vm.startBroadcast();
        uint256 ourBalance = _METoken.balanceOf(msg.sender);
        console.log("Deployer initial balance:", ourBalance);

        uint256 aliceBalance = _METoken.balanceOf(alice);
        console.log("Alice initial balance:", aliceBalance);

        bool success = _METoken.transfer(alice, 50e18);
        if (success) {
            console.log("Transfer successful");
        } else {
            console.log("Transfer failed");
            revert();
        }

        ourBalance = _METoken.balanceOf(msg.sender);
        console.log("Deployer final balance:", ourBalance);

        aliceBalance = _METoken.balanceOf(alice);
        console.log("Alice final balance:", aliceBalance);
        vm.stopBroadcast();
    }
}
```

8. **실행**

```bash
$ forge script script/METokenInteraction.s.sol --private-key <DEPLOYER_PRIVATE_KEY> --rpc-url "http://127.0.0.1:8545" -vv
```

## ERC‑20 토큰의 문제점

- **컨트랙트 주소로 토큰 전송 시 잃어버림**  
  `transfer`는 컨트랙트가 토큰을 받을 준비가 되어 있는지 확인하지 않아요. 그래서 잘못된 주소에 보낼 경우 토큰이 영원히 사라집니다.

- **토큰과 이더의 차이**  
  토큰 전송은 가스 비용이 필요하지만, 토큰 자체로는 지불할 수 없어요. 이는 사용자에게 혼란을 줍니다.

- **`approve`‑`transferFrom` 두 단계**  
  초보자에게는 번거롭고, 무제한 허용으로 인한 보안 위험이 존재합니다.

### 해결책

- **ERC‑2612 (`permit`)** – 서명 기반 승인으로 가스 없이 토큰을 전송할 수 있어요.  
- **EIP‑4337 등 스마트 월렛** – 타인이 가스를 지불해 주는 구조를 제공해요.

## ERC‑223, ERC‑777, ERC‑1155

| 표준 | 특징 |
|---|---|
| **ERC‑223** | 컨트랙트가 토큰을 받을 수 있는지 확인하고 실패 시 전송 중단. |
| **ERC‑777** | 훅(hook) 기능으로 `tokensToSend`·`tokensReceived`를 제공해, 한 번에 안전하게 토큰 전송 가능. |
| **ERC‑1155** | 하나의 컨트랙트에서 여러 종류(토큰 ID)를 관리할 수 있어요. 배치 전송도 지원합니다. |

각 표준은 장단점이 있으니 프로젝트 요구사항에 맞게 선택하세요.

## ERC‑721: NFT

NFT는 고유성을 강조한 토큰이에요. `uint256` 식별자를 통해 각 토큰을 구분하고, 메타데이터 URI를 연결해 이미지·설명 등을 저장할 수 있어요. 실물 자산(부동산·자동차)이나 디지털 예술품 등 다양한 용도로 활용됩니다.

## ERC‑1155: 멀티토큰

게임 개발자에게 유용한 표준이에요. 하나의 컨트랙트에서 가상 화폐, 고유 아이템, 소비성 토큰 등을 모두 관리할 수 있어요. 배치 전송으로 가스 비용을 절감하고, 안전 메커니즘(컨트랙트가 `IERC1155Receiver`를 구현해야 함)도 제공해요.

## 토큰 표준 사용 시 고려사항

1. **표준 준수** – 최소 기능만 구현하면 모든 지갑·거래소와 호환됩니다.  
2. **기능 확장** – 보안에 주의하며 필요에 따라 `burn`, `mint`, `pause` 등 추가 기능을 넣을 수 있어요.  
3. **EIP‑165** – 컨트랙트가 지원하는 인터페이스를 선언해 다른 시스템이 확인할 수 있게 해줍니다.

## 결론

토큰은 단순한 디지털 화폐를 넘어, 거버넌스·접근권·신원·자산 소유권 등 다양한 역할을 수행합니다. ERC‑20, ERC‑721, ERC‑1155 같은 표준 덕분에 토큰은 지갑·거래소·DApp 간의 상호 운용성을 확보하고, 블록체인 생태계를 더욱 효율적이고 연결된 구조로 만들어 주죠.

이번 장에서는 토큰의 종류와 표준을 살펴보고, 직접 토큰을 만들고 활용해 보는 방법까지 배웠어요. 이제 여러분도 토큰을 통해 새로운 아이디어를 구현해 보세요!
