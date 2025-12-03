# Chapter 12. 분산형 애플리케이션

이 장에서는 DApp(분산형 애플리케이션)의 비밀을 풀어보며, 그들이 무엇인지, 어떻게 동작하는지, 핵심 아키텍처가 어떻게 구성되는지를 설명합니다. 기초 개념을 다룬 뒤, 실제로 손으로 직접 첫 번째 DApp을 만들어 보는 실습 예제를 진행해 보겠습니다. 스마트 컨트랙트를 배포하고 프론트엔드를 연결하며, 거의 프로덕션 환경에 가까운 스택을 준비하는 과정을 단계별로 안내합니다. 끝까지 읽으면, 동작하는 DApp과 이 혁신적인 애플리케이션의 핵심 개념을 확실히 이해할 수 있을 거예요.

## DApp이란?

**DApp**은 *decentralized application*의 줄임말이며, 기존 애플리케이션과는 완전히 다른 패러다임입니다. 전통적인 앱 구조(그림 12‑1)는 다음과 같습니다:

- **앱 로직**: 소스코드가 비공개
- **데이터 저장소**: 중앙 집중형 데이터베이스
- **프론트엔드**: 유일한 사용자 인터페이스

![General architecture of a legacy application](images/ch12/maet_1201.png)

그림 12‑1. 기존 애플리케이션의 일반적인 구조

인스타그램, 틱톡, 은행 앱 등 대부분이 이와 비슷한 아키텍처를 사용합니다. 공식 사이트가 다운되면 다른 웹사이트로 로그인할 수 없죠.

DApp은 두 가지 목표를 갖습니다:  
1) 단일 장애 지점을 없애기 위해  
2) 팀이 사라져도 계속 사용할 수 있도록

그 구조는 그림 12‑2처럼 간단히 요약됩니다:

- **스마트 컨트랙트**(Ethereum 기반)가 로직을 담당합니다. 대부분 Solidity나 Vyper 코드가 공개되어 있어요.
- 스마트 컨트랙트 자체에 데이터(데이터베이스 역할)를 저장할 수 있습니다.
- 공식 프론트엔드 외에도 커뮤니티에서 만든 대체 프론트엔드를 사용해도 됩니다.

![General architecture of a DApp](images/ch12/maet_1202.png)

그림 12‑2. DApp의 일반적인 구조

> **주의**  
> DApp은 일부 중앙화된 오프체인 컴포넌트를 가질 수 있지만, 핵심 로직에는 보통 필요하지 않습니다. 이 경우에도 최악의 상황에서는 온체인 데이터만으로 완전히 동작하도록 설계하는 것이 좋습니다. 실제로는 중앙화된 요소에 의존하는 DApp도 존재하며, 이는 진정한 분산형 애플리케이션이라기보다는 하이브리드 형태라고 할 수 있습니다.

다음 섹션에서는 DApp 스택의 각 구성요소를 더 깊게 살펴보고, 이들이 어떻게 상호작용하고 Ethereum 프로토콜과 연결되는지 이해해 보겠습니다.

## 백엔드 (스마트 컨트랙트)

DApp에서 핵심 비즈니스 로직과 데이터 저장은 스마트 컨트랙트에 인코딩되어 Ethereum 블록체인에서 실행됩니다. 블록체인은 분산형 백엔드 역할을 하며, 트랜잭션 실행, 상태 변화, 기록 보관이 네트워크에 의해 신뢰성 있게 강제됩니다.

사용자는 중앙 팀을 믿지 않아도 됩니다. 언제든지 Ethereum 네트워크가 정상적으로 동작하고 스마트 컨트랙트의 상태를 올바르게 업데이트하기 때문입니다.

또한 이 구조는 **검열 저항성**이라는 강력한 특성을 부여합니다. 전통적인 앱은 정부 정책에 따라 특정 국가에서 접근을 금지할 수 있지만, Ethereum 기반 DApp에서는 주소가 스마트 컨트랙트와 상호작용하는 것을 막기 어렵습니다. 공식 사이트를 차단해도 누구나 대체 프론트엔드를 만들고 사용하면 됩니다.

### Tornado Cash 스토리

Tornado Cash는 분산형 믹싱 서비스로, 트레이서블(또는 “오염된”) 암호화폐를 다른 자금과 혼합해 출발지와 수신자를 숨깁니다. 2022년 8월 8일 미국 재무부가 Tornado Cash를 블록리스트에 올려 미국 시민·기업이 사용을 금지했습니다. 이후 개발자 Alexey Pertsev는 암호화폐 믹싱 플랫폼 자체를 만든 혐의로 체포되었습니다.

하지만 서비스는 여전히 IPFS 게이트웨이를 통해 접근 가능하며, 공식 웹사이트가 차단돼도 전 세계 어디서든 Tornado Cash를 사용할 수 있습니다.

## 데이터 저장

스마트 컨트랙트에 데이터를 저장하고 읽어오는 것은 가능하지만 비용이 많이 들고 확장성이 떨어집니다. 모든 정보를 온체인에 저장할 필요는 없습니다.

- **핵심 상태**(예: 잔액, 소유권 기록)는 스마트 컨트랙트에 직접 저장합니다.
- 나머지 정보는 전통적인 데이터베이스나 인덱서 같은 오프체인 솔루션에 저장해도 됩니다. 프론트엔드가 블록체인과 상호작용할 필요 없이 빠르게 데이터를 조회할 수 있죠.

> **주의**  
> *블록체인 인덱서는* 트랜잭션 데이터를 가공해 머신·인간이 읽을 수 있는 형태로 변환하고, 데이터베이스에 로드해 빠른 쿼리를 가능하게 합니다. 블록체인 자체에서는 직접 검색할 수 없으므로, 예를 들어 특정 계정의 USDC 잔액을 알고 싶다면 모든 트랜잭션을 필터링해야 하지만 인덱서를 사용하면 바로 조회가 가능합니다.

핵심은 **필수 데이터와 로직만 온체인에 두고** 나머지는 오프체인에 두는 것입니다.

### IPFS

IPFS(InterPlanetary File System)는 분산형, 컨텐츠 주소 기반 저장 시스템입니다. 파일을 해시로 식별하고, 해당 해시를 요청하면 어느 IPFS 노드에서든 파일을 가져올 수 있습니다.

IPFS는 HTTP 대신 웹 애플리케이션 전달 프로토콜로 자리 잡으려 합니다. 한 서버에 파일을 두지 않고, IPFS에 저장해 언제든지 접근할 수 있죠.

### Merkle 트리

데이터를 오프체인에 저장하고 온체인에는 **Merkle 루트**만 보관하는 방법이 자주 쓰입니다. 이렇게 하면 가스 비용을 크게 절감하면서도 체인에서 검증이 가능합니다.

> **주의**  
> 이 예시는 “whitelist”라는 용어가 기술적 맥락에서 사용되었음을 알려드립니다. 산업계 전반에 걸쳐 널리 쓰이는 용어지만, 포함·배제와 관련된 부정적 의미를 가질 수 있습니다. 이해를 돕기 위해 그대로 유지했습니다.

가장 흔한 활용 사례는 NFT 컬렉션을 만들 때 특정 주소만 저렴하게 민팅할 수 있도록 whitelist를 설정하는 것입니다. 두 가지 옵션이 있는데, 첫 번째는 스마트 컨트랙트에 매핑(`address => bool`)으로 저장하고, 두 번째는 오프체인에서 Merkle 트리를 만들어 루트를 온체인에 저장한 뒤 각 주소에게 Merkle 증명을 제공하는 방식입니다.

> **주의**  
> Merkle 방식을 사용하면 가스 비용이 크게 절감되지만, 트리와 증명이 신뢰할 수 없을 경우 위험이 존재합니다. 가능하다면 원본 리스트를 공개해 누구나 Merkle 루트의 유효성을 검증하도록 하는 것이 좋습니다.

## 프론트엔드 (웹 사용자 인터페이스)

DApp의 프론트엔드는 React, Angular, Vue 등 유명한 Web2 프레임워크로 만들 수 있습니다. Ethereum 체인과 상호작용할 때는 `viem`이나 `ethers.js` 같은 라이브러리를 사용해 추상화합니다.

**단순히 체인에서 직접 데이터를 읽어 모든 컴포넌트를 업데이트하는 방식**은 페이지가 느려지고 사용자 경험이 나빠집니다. 그래서 대부분의 개발자는 중앙화된 데이터 저장소를 활용해 체인과의 상호작용을 최소화하고, 필요할 때만 블록체인을 조회합니다.

그림 12‑3은 완전(단순화)한 DApp 아키텍처를 보여줍니다.

![Complete DApp architecture](images/ch12/maet_1203.png)

그림 12‑3. 완전한 DApp 아키텍처

## 간단한 DApp 예제

지금까지 DApp의 기본 개념을 살펴봤습니다. 이제 손으로 직접 DApp을 만들어 보겠습니다.

다음과 같은 튜토리얼이 많지만, **Speedrun Ethereum**(https://oreil.ly/Onygc)을 강력히 추천합니다. 빠르게 학습하고 바로 멋진 프로젝트를 만들 수 있어요. 모든 챌린지를 완료하고 BuidlGuidl 커뮤니티에 참여해 보세요.

이번 예제는 “Hello World” DApp입니다. 컴퓨터와 인터넷 연결만 있으면 됩니다.

### 설치 요구사항

이 튜토리얼을 따라하려면 **node.js**와 **yarn**를 설치하세요. Scaffold‑ETH 2(https://scaffoldeth.io)는 개발 환경을 빠르게 구성해 주는 멋진 도구입니다.

### DApp 만들기

터미널에서 다음 명령어를 실행합니다:

```bash
$ npx create-eth@latest
```

프로젝트 이름을 묻습니다. 예시로 `mastering-ethereum`을 입력했습니다:

```
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+ 
 | Create Scaffold-ETH 2 app | 
 +-+-+-+-+-+-+-+-+-+-+-+-+-+-+

? Your project name: mastering-ethereum
```

그 다음 Solidity 프레임워크를 선택합니다. 여기서는 Hardhat을 사용합니다:

```
? What solidity framework do you want to use?
❯ hardhat
   foundry
  none
```

잠시 후 “Congratulations” 메시지와 함께 다음 단계 안내가 표시됩니다:

```
  Congratulations! Your project has been scaffolded! 🎉

  Next steps:

  cd mastering-ethereum
  
        Start the local development node
  
        yarn chain
  
        In a new terminal window, deploy your contracts
  
        yarn deploy
  
    In a new terminal window, start the frontend
  
    yarn start
  
 Thanks for using Scaffold-ETH 2 🙏 , Happy Building!
```

### 체인 시작

프로젝트 폴더로 이동합니다:

```bash
$ cd mastering-ethereum
```

`packages/hardhat/contracts`에 `YourContract.sol` 예제 스마트 컨트랙트가 있습니다. 이 폴더에 필요한 모든 컨트랙트를 넣어야 합니다.

`packages/nextjs`에는 프론트엔드 구조가 이미 준비되어 있습니다.

이 튜토리얼은 기본 설정만 사용하므로, 새 계약을 작성하거나 프론트엔드를 수정하지 않습니다.

먼저 로컬 체인을 시작합니다:

```bash
$ yarn chain
```

### 컨트랙트 배포

다음으로, 앞서 만든 로컬 체인에 컨트랙트를 배포합니다. 새로운 터미널에서 실행하세요:

```bash
$ yarn deploy
```

배포 로그가 나타납니다:

```
Generating typings for: 2 artifacts in dir: typechain-types for target: ethers-v6
Successfully generated 6 typings!
Compiled 2 Solidity files successfully (evm target: paris).
deploying "YourContract" (tx: 0x8ec9ba16869588c2826118a0043f63bc679a4e947f739e8032e911475e77dcb4)...: deployed at 0x5FbDB2315678afecb367f032d93F642f64180aa3 with 532743 gas
👋  Initial greeting: Building Unstoppable Apps!!!
📝  Updated TypeScript contract definition file on ../nextjs/contracts/deployedContracts.ts
```

이 명령은 `YourContract` 예제 컨트랙트를 로컬 체인에 배포합니다. 실제 프로젝트에서는 `packages/hardhat/deploy/00_deploy_your_contract.ts`를 수정해 필요한 모든 컨트랙트를 배포하도록 합니다.

체인을 실행 중인 터미널에서 로그가 새로 나타납니다:

```
eth_sendTransaction
  Contract deployment: <UnrecognizedContract>
  Contract address:    0x5fbdb2315678afecb367f032d93f642f64180aa3
  Transaction:         0x8ec9ba16869588c2826118a0043f63bc679a4e947f739e8032e911475e77dcb4
  From:                0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
  Value:               0 ETH
  Gas used:            532743 of 532743
  Block #1:            0xa7b8e3b6f82eccb3542279573dbf8efa2b876ff00807a8619feef191007e06d9
```

`Contract deployment`과 `Contract address`가 보이면 배포가 성공한 것입니다.

### 프론트엔드 시작

Scaffold‑ETH 예제에는 기본 프론트엔드가 포함되어 있어 바로 상호작용을 테스트할 수 있습니다. 새로운 터미널에서 실행하세요:

```bash
$ yarn start
```

다음과 같은 메시지가 뜹니다:

```
yarn start
  ▲ Next.js 14.2.21
  - Local:        http://localhost:3000
 
 ✓ Starting...
 ✓ Ready in 1767ms
```

브라우저에서 `http://localhost:3000`을 열면 프론트엔드가 표시됩니다 (그림 12‑4).

![Scaffold-ETH frontend](images/ch12/maet_1204.png)

그림 12‑4. Scaffold‑ETH 프론트엔드

### 컨트랙트와 상호작용하기

축하합니다! 이제 DApp을 실험하고 상호작용할 수 있습니다. 개발 워크플로우에 필수적인 두 가지 기능이 있는데요:

- **버너 지갑**  
- **디버그 계약(Debug Contracts) 섹션**

프론트엔드 오른쪽 상단에 이미 랜덤한 버너 지갑이 연결돼 있습니다. 이는 브라우저에 일시적으로 저장된 개인키를 가진 주소입니다. 페이지를 새로 고쳐도 같은 주소가 유지됩니다.

버너 지갑은 개발 중 매우 편리합니다. 필요할 때만 실제 Web3 지갑을 연결하면 됩니다. 아래 그림 12‑5, 12‑6, 12‑7에서 과정을 확인하세요.

![Disconnect burner wallet](images/ch12/maet_1205.png)

그림 12‑5. 버너 지갑 끊기

![Connect Wallet button](images/ch12/maet_1206.png)

그림 12‑6. Connect Wallet 버튼

![Choose wallet](images/ch12/maet_1207.png)

그림 12‑7. 지갑 선택

두 번째 기능은 **디버그 계약** 섹션입니다. 페이지 중앙에 있는 “Debug Contracts” 링크를 클릭하면 됩니다. 기본 예제에서는 그림 12‑8과 같은 화면이 나타납니다.

![Debug Contracts section](images/ch12/maet_1208.png)

그림 12‑8. 디버그 계약 섹션

여기서 프론트엔드를 만들지 않아도 모든 컨트랙트를 직접 호출해 볼 수 있습니다. 개발 중에 컨트랙트가 예상대로 동작하는지 확인할 때 유용합니다.

간단한 시연을 해볼게요. 먼저 버너 지갑에 자금을 충전해야 합니다. 오른쪽 가장자리에 있는 “Grab funds” 버튼(그림 12‑9)을 클릭하면 바로 ETH를 받을 수 있습니다.

![Grab funds button](images/ch12/maet_1209.png)

그림 12‑9. Grab funds 버튼

이제 `setGreeting` 섹션에서 `_newGreeting`에 **hello world**를 입력하고, “payable value”에 **0.1**을 넣습니다. 그 뒤 *payable value* 오른쪽 별표를 클릭하면 ETH가 wei로 변환됩니다. 마지막으로 Send 버튼을 눌러 트랜잭션을 전송합니다.

그림 12‑10은 Send 버튼을 누르기 전 컨트랙트 상태입니다:  
- ETH 잔액: 0  
- greeting: “Building Unstoppable Apps!!!”  
- premium: false  
- totalCounter: 0

![Contract state before transaction](images/ch12/maet_1210.png)

그림 12‑10. 트랜잭션 전 컨트랙트 상태

Send 버튼을 누른 뒤 그림 12‑11에서 보이듯, ETH 잔액은 0.1이 되고 greeting은 “hello world”로 바뀌며 premium이 true가 됩니다.

![Contract state after transaction](images/ch12/maet_1211.png)

그림 12‑11. 트랜잭션 후 컨트랙트 상태

입력값과 동작에 따라 컨트랙트가 어떻게 반응하는지 직접 실험해 보세요.

### Vercel에 배포하기

DApp이 만족스러워졌다면, Vercel 같은 프로덕션 환경에 배포할 수 있습니다. Vercel은 프론트엔드‑as‑a‑service 도구로, 간단히 한 번의 명령으로 애플리케이션을 인터넷에 올릴 수 있습니다.

Scaffold‑ETH는 `yarn vercel:yolo`라는 하나의 명령으로 바로 배포해 줍니다. 터미널에서 실행하세요:

```bash
$ yarn vercel:yolo
```

Vercel 계정 연결(또는 새로 만들기) 후 프로젝트 이름을 지정하면 끝! 몇 분 안에 전 세계 누구나 접속할 수 있는 URL이 생성됩니다.

Vercel 프로필에서 새 프로젝트를 확인해 보세요. 그림 12‑12처럼 도메인 필드가 표시됩니다.

![Vercel project page](images/ch12/maet_1212.png)

그림 12‑12. Vercel 프로젝트 페이지

## DApp을 더욱 분산화하기

앞서 Vercel에 배포했지만, Vercel은 중앙집중형 서비스입니다. 모든 파일이 자체 서버에 저장되므로 정책에 따라 검열될 수 있고 IP 주소를 추적할 수도 있습니다.

더욱 분산화하려면 프론트엔드를 **IPFS** 같은 P2P 네트워크에 호스팅하고, ENS와 `eth.limo` 같은 서비스를 활용해 전 세계 어디서든 접근 가능하도록 할 수 있습니다.

### 분산형 웹사이트

[Eth.limo](https://eth.limo/)는 DWebsites(분산형 웹사이트)를 만들 때 유용한 서비스입니다. ENS 기술을 기반으로 `.eth` 도메인 이름과 IPFS 콘텐츠 해시를 연결해 줍니다. Vitalik Buterin은 `vitalik.eth`로 자신의 지갑 주소와 블로그를 연결했습니다.

ENS는 단순히 도메인을 이더리움 주소에 매핑하는 것뿐 아니라, IPFS 웹사이트(예: `bafybeif3dy…ga4zu`)를 가리킬 수도 있습니다. 대부분의 브라우저가 IPFS URL을 제대로 해석하지 못하므로, `eth.limo`는 ENS 이름과 IPFS 콘텐츠를 자동으로 연결해 HTTPS로 제공하는 역방향 프록시 역할을 합니다.

### 한계

- IPFS는 정적 파일만 지원합니다(서버 사이드 로직 불가).
- `eth.limo`를 사용하려면 ENS 도메인을 구매하고, 프론트엔드의 IPFS 콘텐츠 해시와 연결해야 합니다.
- 반드시 `*.eth.limo` 형식으로 접근해야 하며 `.limo` 부분을 빼면 브라우저에서 해결되지 않습니다.

> **팁**  
> 대부분의 브라우저가 아직 ENS/IPFS를 완전히 지원하지 않지만, Brave 같은 일부 브라우저는 점차 지원을 추가하고 있습니다. (예: https://oreil.ly/LlJT7)

`eth.limo` 자체도 중앙화된 제3자 서비스이므로 갑작스런 중단 가능성을 염두에 두어야 합니다. 만약 중단되면 IPFS를 통해 여전히 접근할 수 있지만, `.eth.limo` URL은 동작하지 않을 것입니다.

더 깊게 배우고 싶다면 공식 웹사이트(https://eth.limo)에서 자세한 정보를 확인해 보세요.

### IPFS에 배포

Scaffold‑ETH 2는 `yarn ipfs` 명령으로 프론트엔드를 IPFS에 빠르게 업로드할 수 있습니다. 새로운 터미널을 열고 실행하세요:

```bash
$ yarn ipfs
```

명령이 끝나면 다음과 같은 메시지가 표시됩니다:

```
   Creating an optimized production build ...
 
 ✓ Compiled successfully
 ✓ Linting and checking validity of types
    
 ✓ Collecting page data
    
 ✓ Generating static pages (8/8)
 ✓ Collecting build traces
    
 ✓ Finalizing page optimization

…

🚀  Upload complete! Your site is now available at: https://community.bgipfs.com/ipfs/bafybei…
```

표시된 URL(예: `https://community.bgipfs.com/ipfs/bafybei…`)이 IPFS 콘텐츠 해시를 가리키는 주소입니다. 여전히 ENS와 `eth.limo`를 설정해 개인 도메인으로 연결하면 됩니다.

명령의 내부 동작은 다음과 같습니다:

1. 프론트엔드를 빌드해 정적 파일을 준비합니다.
2. BuidlGuidl(Scaffold‑ETH 2 유지자)의 IPFS 커뮤니티 노드에 업로드합니다.
3. `community.bgipfs.com/<ipfs-content-hash>` 형태의 URL이 반환됩니다.

IPFS 노드를 직접 운영하고 싶다면 [BuidlGuidl IPFS](https://www.bgipfs.com)를 참고하세요.

## App → DApp

이번 장에서는 Scaffold‑ETH를 활용해 로컬 체인에서 컨트랙트를 배포하고, 프론트엔드와 상호작용하며, Vercel에 배포한 뒤 IPFS로 분산화까지 진행했습니다. 그림 12‑13은 완전한 DApp을 만들기 위한 엔지니어링 스택의 간단한 개요를 보여줍니다.

![DApp engineering stack](images/ch12/maet_1213.png)

그림 12‑13. DApp 전체 엔지니어링 스택 요약

## 결론

이번 장에서는 최신 도구를 활용해 기본적인 DApp을 만드는 과정을 단계별로 안내했습니다. 다음 장에서는 Ethereum에서 가장 중요한 DApp과 그 카테고리들을 살펴보고, DeFi라는 큰 그림을 함께 탐험할 예정이니 기대해 주세요!
