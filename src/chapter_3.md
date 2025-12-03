# 3장. 이더리움 노드란?

이더리움 노드는 이더리움 스펙을 구현한 소프트웨어로, 다른 이더리움 노드들과 P2P 네트워크로 소통하는 프로그램이에요.

원래는 노드를 하나만 실행하면 이더리움 생태계에 참여하는 데 필요한 모든 기능을 쓸 수 있었죠. 그런데 2022년 9월 15일에 ‘머지(The Merge)’ 하드포크가 일어나면서 합의 방식이 기존의 작업증명(PoW)에서 새 지분증명(PoS) 방식인 Gasper로 바뀌었어요. 그러면서 합의(Consensus)와 실행(Execution) 역할이 분리됐고, 새로운 종류의 이더리움 클라이언트인 '합의 클라이언트'도 생겼습니다.

그래서 지금은 최신 이더리움 노드를 제대로 돌리려면 그림 3-1처럼 소프트웨어 두 개를 동시에 실행해야 해요. 각각의 역할은 아래와 같아요.

**합의(Consensus) 클라이언트**

이 소프트웨어는 블록체인의 단일 히스토리에 대해 모든 노드가 합의하도록 만드는 역할을 맡아요.

**실행(Execution) 클라이언트**

이건 네트워크에서 발생하는 모든 블록과 트랜잭션을 받고, EVM에서 실행하며, 결과가 맞는지 검증하는 역할입니다.

![그림 3-1. 이더리움 노드의 구조](./images/ch3/maet_0301.png)

여러 종류의 이더리움 클라이언트(실행, 합의 모두)는 공식 스펙과 표준화된 통신 프로토콜을 잘 지키면 서로 잘 호환됩니다. 클라이언트마다 개발팀도 다르고, 사용하는 프로그래밍 언어도 다양하지만, 모두 같은 프로토콜을 ‘말’하고 똑같은 규칙을 따라요. 그래서 네트워크상에서 같이 잘 동작할 수 있죠.

이더리움은 오픈 소스 프로젝트라 주요 클라이언트의 소스코드는 누구나 다운로드해서 원하는 대로 쓸 수 있습니다(LGPL v3.0 같은 오픈 소스 라이선스). 오픈 소스라는 건 단순히 ‘공짜’라는 의미 그 이상이에요. 누구나 개발에 참여할 수 있고, 코드를 들여다보며 개선도 할 수 있죠. 많은 사람이 코드에 참여하면 더 신뢰할 수 있는 소프트웨어가 됩니다.

이더리움의 공식 스펙은 원래 '옐로우 페이퍼'라는 문서에 정의되어 있어요. 이 문서는 이 책 공동 저자인 개빈 우드가 썼고, 지금도 이더리움에 주요 변화가 있을 때마다 계속 업데이트됩니다. 이 공식 문서를 토대로 각각 실행 클라이언트와 합의 클라이언트를 위한 두 가지 레퍼런스(참고용) 구현이 존재해요. 이 참고 구현들은 파이썬으로 작성되어, 읽기 쉽고 이해하기 쉽게 만들어져 있습니다.

> **참고**  
>
> 이 참고 스펙은 실제로 완전한 노드 소프트웨어를 만들기 위한 게 아니라, 구현할 때 참고할 수 있는 실행 가능한 '의사코드(pseudocode)'예요.

비트코인과 비교하면, 비트코인은 이런 공식 스펙 문서가 없고, 사실상 '비트코인 코어(Bitcoin Core)'라는 구현 자체가 스펙처럼 취급돼요. 반면 이더리움은 공식 문서(영어+수학적 명세), EIP(이더리움 개선 제안), 파이썬으로 작성된 합의 스펙 등을 조합해서 이더리움 노드의 표준 동작이 정의되어 있습니다.

이렇게 명확한 공식 명세 덕분에 이더리움에는 서로 독립적으로 개발된 다양한 소프트웨어 클라이언트가 존재해요. 실제로 이더리움 네트워크엔 블록체인 중에서 가장 다양한 구현이 돌아가고 있죠. 이 다양성은 네트워크를 공격으로부터 지키는 데도 도움이 됩니다. 특정 클라이언트에 문제가 생겨도 나머지 클라이언트가 네트워크를 계속 지탱해주니까요.

## 이더리움 네트워크 종류

이더리움에는 원래 ‘옐로우 페이퍼’의 공식 명세를 대체로 따르지만, 서로 완전히 호환되지는 않을 수도 있는 다양한 네트워크가 있어요.

예를 들어, 이더리움 클래식(Ethereum Classic), BNB 체인, 폴리곤(Polygon) 같은 EVM 호환 체인들도 실행 스펙의 상당 부분을 공유하지만, 합의 방식이나 일부 파라미터는 서로 다릅니다. 그래서 거의 같은 프로토콜을 쓰지만, 약간의 추가 작업이 필요해서 모든 이더리움 클라이언트가 모든 이더리움 기반 체인을 바로 지원하는 건 아니에요.

2025년 6월 기준으로, 이더리움 실행 클라이언트는 4개 언어로 5종류, 합의 클라이언트는 5개 언어로 5종류가 있습니다:

실행 클라이언트:

- Geth (Go 언어)
- Nethermind (C#)
- Besu (Java)
- Erigon (Go)
- Reth (Rust)

합의 클라이언트:

- Lighthouse (Rust)
- Lodestar (TypeScript)
- Nimbus (Nim)
- Prysm (Go)
- Teku (Java)

이번 장에서는 아래 두 가지 실행 클라이언트를 다룹니다:

**Geth**

이더리움 재단이 유지하는, 가장 오래되고 많이 쓰이는 실행 클라이언트

**Reth**

Parity/OpenEthereum 프로젝트 종료 후 Paradigm에서 새로 만든 러스트 기반 실행 클라이언트

그리고 아래 두 가지 합의 클라이언트도 살펴봐요:

**Prysm**

최초의 합의 클라이언트, 현재는 Offchain Labs가 관리

**Lighthouse**

가장 많이 쓰이는 합의 클라이언트, Sigma Prime에서 관리

각 클라이언트로 노드를 어떻게 세팅하는지, 특히 Geth-Prysm 조합과 Reth-Lighthouse 조합으로 설치하고, 주요 명령줄 옵션과 API도 살펴볼 거예요.

> **참고**  
>
> 여기서 소개하는 클라이언트 조합은 예시일 뿐이고, 마음에 드는 실행 클라이언트와 합의 클라이언트를 자유롭게 골라서 조합할 수 있습니다.

## 내가 풀노드를 직접 운영해야 할까?

블록체인의 건강, 안정성, 검열 저항성은 여러 곳에서 독립적으로 운영되는 풀노드(전체 블록 데이터를 저장하는 노드)가 얼마나 많으냐에 달려 있어요. 풀노드는 새로운 노드가 네트워크에 참여할 때 데이터를 제공할 수도 있고, 모든 트랜잭션과 스마트컨트랙트를 직접 검증할 수도 있습니다.

> **참고**
>
> 좀 더 정확히 구분하면,  
>
> **아카이브(Archive) 노드**  
> 블록체인 데이터를 모두 영구적으로 저장하는 노드  
>
> **풀(Full) 노드**  
> 과거 상태와 영수증 데이터는 일정 시점 이후 버리는 노드(노드 설치 시 기본 옵션)

다만, 풀노드를 돌리려면 하드웨어와 네트워크 트래픽이 꽤 필요해요. 2025년 6월 기준으로, 최소 2TB 이상의 데이터를 다운받아서 하드디스크에 저장해야 하고, 이 데이터 용량은 계속 빠르게 늘어나고 있습니다. 이 내용은 뒷부분 ‘풀노드 하드웨어 요구사항’에서 더 자세히 다룹니다.

실제로 이더리움 개발을 할 때는 꼭 메인넷 풀노드를 운영하지 않아도 돼요. 테스트넷 노드(테스트용 공개 체인)나, Anvil 같은 로컬 블록체인, Infura나 Alchemy 같은 서비스 제공자의 노드 API를 써도 거의 대부분의 개발 작업이 가능합니다.

로컬에 블록체인 데이터를 저장하거나 블록, 트랜잭션을 직접 검증하지 않고, 원격에서 동작하는 클라이언트(리모트 클라이언트)를 사용할 수도 있어요. 이런 클라이언트는 지갑 기능을 제공하며, 트랜잭션 생성과 전송도 할 수 있죠. 리모트 클라이언트는 내 풀노드, 공개 블록체인, 공개/허가형(Proof-of-Authority) 테스트넷, 개인용 블록체인 등 다양한 네트워크에 연결하는 데 쓸 수 있어요. 실제로는 MetaMask, Rabby Wallet, Coinbase Wallet 같은 리모트 클라이언트를 많이 쓰게 될 거예요. 여러 노드 옵션을 편하게 오갈 수 있으니까요.

보통 리모트 클라이언트와 지갑이라는 용어는 거의 같은 의미로 쓰이지만, 약간의 차이가 있긴 해요. 리모트 클라이언트는 지갑의 트랜잭션 기능에 더해, web3.js 같은 API도 제공하는 경우가 많거든요.

여기서 말하는 이더리움의 리모트 클라이언트는 ‘라이트 클라이언트’랑은 다른 개념이에요(비트코인의 SPV 클라이언트와 비슷한 게 라이트 클라이언트임). 라이트 클라이언트는 블록 헤더만 검증하고 머클 증명을 통해 트랜잭션의 포함 여부와 영향을 확인해서, 어느 정도 풀노드와 비슷한 보안을 누릴 수 있어요. 반면 이더리움의 리모트 클라이언트는 블록 헤더나 트랜잭션 검증을 아예 하지 않고, 풀노드를 완전히 신뢰해서 블록체인에 접근합니다. 그래서 보안이나 익명성이 좀 떨어질 수 있죠. 이런 문제는 내가 직접 운영하는 풀노드를 사용하면 어느 정도 해결할 수 있어요.

### 풀노드의 장단점

풀노드를 직접 돌리면 내가 연결하는 네트워크의 운영에도 도움을 주지만, 어느 정도 비용도 발생해요. 장단점을 정리해보면 아래와 같아요.

**장점:**

- 이더리움 네트워크의 건강과 검열 저항성 강화에 기여할 수 있음
- 모든 트랜잭션을 직접 검증함
- 중개자 없이 퍼블릭 블록체인에 있는 어떤 컨트랙트와도 직접 상호작용 가능
- 중개자 없이 직접 컨트랙트를 퍼블릭 블록체인에 배포할 수 있음
- 블록체인 상태(계정, 컨트랙트 등)를 오프라인으로 조회할 수 있음
- 내가 어떤 정보를 조회하는지 제3자에게 노출하지 않고 블록체인을 쿼리할 수 있음

**단점:**

- 꽤 많은 하드웨어, 저장공간, 인터넷 트래픽이 필요함(점점 더 늘어남)
- 처음 동기화할 때 며칠이 걸릴 수 있음
- 동기화를 유지하려면 꾸준히 관리·업데이트하고, 계속 켜두어야 함

### 공개 테스트넷의 장단점

풀노드를 직접 돌리든 아니든, 공개 테스트넷 노드를 한 번쯤 써볼 필요는 있어요. 테스트넷 노드의 장단점도 한번 볼게요.

**장점:**

- 테스트넷은 저장해야 할 데이터가 훨씬 적어요(2025년 6월 기준, 네트워크별로 100~300GB 정도)
- 동기화도 몇 시간 만에 끝남
- 컨트랙트 배포나 트랜잭션에는 실제 가치가 없는 테스트 이더(test ether)를 써요. 여러 곳에서 공짜로 받을 수 있음
- 테스트넷도 공개 블록체인이라 다른 사용자, 컨트랙트와 “라이브” 환경에서 테스트 가능

**단점:**

- 실제 돈을 쓸 수는 없어요(가치 없는 테스트 이더만 가능). 그래서 진짜 공격자 상황에서의 보안 테스트는 힘듦
- 테스트넷에서는 가스비가 의미가 없어서(무료임), 실제 메인넷 환경처럼 트랜잭션 수수료를 테스트하기 어려움. 또 메인넷에서 발생하는 네트워크 혼잡도 경험하기 힘듦
- 어떤 테스트넷은 특수 목적용으로 설계돼서 메인넷과 살짝 다를 수도 있음

### 로컬 블록체인 시뮬레이션의 장단점

여러 가지 테스트 목적이라면, 나만의 프라이빗 블록체인(단일 인스턴스)을 띄우는 게 제일 편할 때도 많아요. Anvil이 대표적인 로컬 블록체인 시뮬레이터고, 혼자서 마음껏 실험해볼 수 있습니다.

**장점:**

- 동기화가 필요 없고, 데이터도 거의 없음(블록 1번부터 내가 직접 만들어요)
- 테스트 이더가 필요 없음; 직접 블록 보상으로 원하는 만큼 받을 수 있음
- 사용자도, 컨트랙트도 나 혼자뿐
- 내가 배포한 컨트랙트만 있어서 환경이 깔끔함

**단점:**

- 사용자가 나 하나뿐이라 실제 퍼블릭 블록체인처럼 경쟁 상황이 없음(트랜잭션 공간 경쟁, 트랜잭션 순서 경쟁이 없음)
- 블록 생성도 내가 하기 때문에 예측이 쉬움. 그래서 퍼블릭 블록체인에서만 벌어지는 다양한 상황은 테스트가 어려움. 참고로 Anvil이나 Hardhat 같은 도구는 메인넷 환경에 가깝게 블록 생성 모드를 설정할 수 있지만, 진짜 메인넷과 똑같진 않아요
- 다른 컨트랙트가 없으니, 테스트하려는 것뿐 아니라 의존성이나 라이브러리도 다 내가 배포해야 함. 다행히 Anvil 같은 도구는 메인넷 특정 블록을 ‘포크’해서 실험할 수도 있어서, 실제 환경과 최대한 비슷하게 만들 수 있어요.

## 이더리움 노드 실행하기

시간과 여유가 있다면, 한 번쯤은 풀노드를 직접 돌려보는 걸 추천해요. 배우는 것도 많고, 프로세스를 직접 경험할 수 있거든요. 이 섹션에서는 Geth-Prysm과 Reth-Lighthouse 클라이언트를 다운로드·컴파일·실행하는 방법을 다룰 거예요. 명령줄(CLI) 사용이 조금은 익숙해야 하니, 미리 연습해두면 좋아요. 풀노드, 테스트넷, 개인용 블록체인 클라이언트로 쓸 때 모두 설치 방법은 비슷해요.

### 풀노드 하드웨어 요구사항

시작하기 전에, 내 컴퓨터가 이더리움 풀노드를 돌릴 수 있을지 먼저 확인해야 해요.  
풀노드를 제대로 돌리려면 최소 2TB의 저장공간이 필요합니다. 테스트넷 풀노드까지 같이 돌릴 거라면 추가로 100~400GB가 더 필요해요. 2TB 데이터를 받으려면 인터넷도 빠른 게 좋아요.

이더리움 동기화는 저장장치(I/O) 부담이 커서, SSD를 꼭 추천드려요. 하드디스크(HDD)밖에 없다면 최소 8GB 메모리를 캐시로 써야 좀 쾌적하게 돌아갑니다. 안 그러면 속도가 너무 느릴 수 있어요.

정리하면, 이더리움 풀노드 동기화에 필요한 최소 사양은 다음과 같아요:

- 2코어 이상 CPU
- 2TB 이상 여유 저장공간
- SSD 기준 8GB RAM 이상(혹은 HDD면 8GB 이상, SSD가 훨씬 유리함)
- 7Mbps 이상의 다운로드 인터넷

개발 도구, 클라이언트, 여러 블록체인까지 모두 저장하고 쾌적하게 쓰려면 이 정도는 권장해요:

- 4코어 이상, 클럭 속도가 빠른 CPU(코어 수보단 속도가 중요)
- 16GB 이상 메모리
- NVMe SSD 2TB 이상
- 24Mbps 이상의 인터넷

블록체인 크기가 얼마나 빠르게 커질지는 예측이 어렵기 때문에, 동기화 전에 블록체인 최신 용량을 꼭 확인하는 게 좋아요.

> **참고**
>
> 여기 적힌 저장공간 기준은 블록체인 과거 데이터를 일정 부분 삭제하는 ‘프루닝(pruning)’ 설정을 쓴 경우예요. 만약 모든 상태 데이터를 저장하는 ‘아카이브 노드’로 돌리면, 2TB로는 부족하고 12~15TB까지도 필요할 수 있습니다(클라이언트마다 다름). 항상 최신 하드웨어 요구사항은 클라이언트 공식 웹사이트에서 확인해 주세요.

### 클라이언트 빌드 및 실행을 위한 소프트웨어 요구사항

여기서는 Geth-Prysm과 Reth-Lighthouse 클라이언트를 다루지만, 대부분 유닉스 계열 환경(리눅스/맥)에서 명령줄로 실행하는 걸 전제로 하고 있어요. 예시 명령어와 결과는 macOS의 Bash 쉘 기준인데, 대부분의 리눅스에서도 똑같이 동작해요. 윈도우 사용자라면 WSL2(Windows Subsystem for Linux 2)를 쓰는 게 편해요.

> **팁**
>
> 이 장의 예제 대부분은 터미널에서 운영체제의 명령줄(CLI, shell)을 사용하는 방식입니다. 쉘 프롬프트에 명령어를 입력하면 결과가 나오고, 다시 프롬프트가 나타나죠. 예제에서 $ 기호 뒤에 나오는 굵은 글씨가 실제 입력해야 할 명령어고, $는 입력하지 않아도 됩니다. 명령어 밑에 나오는 줄은 명령 실행 후 터미널에 출력되는 결과예요. 다시 $가 나오면, 다음 명령어를 입력하라는 뜻입니다.

시작하기 전에, 필요한 소프트웨어를 설치해야 할 수도 있어요. 지금 쓰는 컴퓨터에서 소프트웨어 개발을 한 번도 해본 적이 없다면, git(소스코드 관리), golang(Go 언어), rust(시스템 프로그래밍 언어) 같은 도구들을 설치해야 합니다.

아래는 예제에서 사용할 네 가지 클라이언트의 공식 문서 링크예요:

- [Geth 공식 문서](https://oreil.ly/zYviP)
- [Prysm 공식 문서](https://oreil.ly/9-2FC)
- [Reth 공식 문서](https://oreil.ly/KDmMt)
- [Lighthouse 공식 문서](https://oreil.ly/RRpAs)

각 클라이언트의 구조나 설치 시 자주 발생하는 문제 등 더 자세한 정보가 궁금하다면 위 웹사이트들을 참고하면 좋아요!

### 준비 단계

홈 디렉터리에서 시작해서, *ethereum-node1*라는 폴더를 만들고 그 안에 *execution*과 *consensus*라는 하위 폴더 두 개를 만들어주세요:

```bash
$ mkdir ethereum-node1
$ cd ethereum-node1
$ mkdir execution
$ mkdir consensus
````

폴더 구조는 이렇게 생겼을 거예요:

```bash
ethereum-node1
├── consensus
└── execution
```

이번엔 위에서 했던 걸 *ethereum-node2*라는 폴더로 한 번 더 반복해볼게요:

```bash
$ cd .. # 홈 디렉터리로 다시 이동하는 명령어
$ mkdir ethereum-node2
$ cd ethereum-node2
$ mkdir execution
$ mkdir consensus
```

최종적으로 *ethereum-node1*과 *ethereum-node2*라는 두 개의 루트 폴더가 생기고, 각각의 폴더 안에 *execution*과 *consensus* 하위 폴더가 들어가 있어야 합니다.

그리고 [Go 언어](https://golang.org/)와 [Rust](https://www.rust-lang.org/)도 설치해야 해요. 설치 방법은 공식 사이트에서 친절하게 설명해주니 참고하면 어렵지 않아요.

### Geth-Prysm

먼저 만든 *ethereum-node1* 폴더로 이동합니다:

```bash
$ cd ethereum-node1
```

#### Geth

먼저 Geth를 소스 코드에서 빌드해서 설치해볼 거예요.
Geth는 Go 언어로 작성된 공식 이더리움 실행 클라이언트입니다(이더리움 재단에서 개발 중).
대부분의 이더리움 계열 블록체인은 저마다 전용 Geth를 가지고 있어요. 내 네트워크에 맞는 버전을 아래 저장소 링크 중에서 골라 사용해야 해요.

* [Ethereum](https://oreil.ly/qzK-O)
* [BNB Chain](https://oreil.ly/tGtL3)
* [Polygon PoS](https://oreil.ly/ZWhh3)

> **참고**
>
> 꼭 이렇게 직접 소스 코드로 빌드하지 않아도, 운영체제별로 미리 컴파일된 실행파일(바이너리)을 받아서 간단히 설치할 수도 있습니다. 각 저장소의 ‘releases’ 섹션에서 다운로드할 수 있어요.
> 하지만 직접 빌드해보면 내부 동작 원리를 더 잘 이해할 수 있습니다!

**저장소 클론하기**
첫 번째로, Git 저장소를 복제해서 소스 코드를 가져올 거예요. *execution* 폴더 안에서 아래 명령어를 입력하세요:

```bash
$ cd execution
$ git clone https://github.com/ethereum/go-ethereum.git
```

아래처럼 복제 진행 상황이 출력됩니다:

```bash
Cloning into 'go-ethereum'...
remote: Enumerating objects: 130745, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 130745 (delta 1), reused 6 (delta 0), pack-reused 130734
Receiving objects: 100% (130745/130745), 204.15 MiB | 6.13 MiB/s, done.
Resolving deltas: 100% (80729/80729), done.
```

이제 로컬에 Geth 소스 코드가 준비됐으니, 실행 파일로 빌드할 차례예요.

**Geth 빌드하기**
다운로드한 디렉터리로 들어가서 최신 릴리스를 선택한 뒤 make 명령을 입력하면 됩니다.
현재(예시 기준)는 v1.14.3이지만, 항상 최신 릴리스를 확인해 주세요.

```bash
$ cd go-ethereum
$ git checkout v1.14.3
$ make geth
```

컴파일이 잘 진행되면 이런 메시지가 뜰 거예요:

```bash
go run build/ci.go install ./cmd/geth
go: downloading golang.org/x/crypto v0.22.0
go: downloading golang.org/x/net v0.24.0
[...]
github.com/ethereum/go-ethereum/cmd/utils
github.com/ethereum/go-ethereum/beacon/blsync
github.com/ethereum/go-ethereum/cmd/geth
Done building.
Run "./build/bin/geth" to launch geth.
```

실제로 Geth가 잘 설치됐는지 확인해봅시다:

```bash
$ ./build/bin/geth version

GethVersion: 1.14.3-stable
Git Commit: ab48ba42f4f34873d65fd1737fabac5c680baff6
Architecture: arm64
Go Version: go1.22.2
Operating System: darwin
[...]
```

`geth version` 명령 결과는 컴퓨터마다 다를 수 있지만, 위와 비슷하게 나오면 성공입니다.

아직 Geth는 실행하지 마세요! 이더리움 노드 동기화를 위해서는 합의 클라이언트도 같이 설치해야 하거든요.

#### Prysm

이번엔 합의 클라이언트인 Prysm을 설치할 차례예요.
Prysm은 Offchain Labs에서 Go 언어로 개발 중인 합의 클라이언트입니다.
머지 이후 한동안 가장 널리 쓰였던 합의 클라이언트이고, 최근엔 다양성이 늘어나 점유율이 37% 정도로 줄었어요.

**바이너리 설치하기**
Geth처럼 소스 빌드도 가능하지만, Prysm은 바이너리로 설치하는 게 더 간편합니다.
먼저 *consensus* 폴더로 이동하세요:

```bash
$ cd ../.. # ethereum-node1 폴더로 이동
$ cd consensus
```

아래 명령어를 입력하면 Prysm 실행 스크립트를 다운로드하고 실행 권한을 줍니다:

```bash
$ curl https://raw.githubusercontent.com/prysmaticlabs/prysm/master/prysm.sh --output prysm.sh && chmod +x prysm.sh
```

**JWT 시크릿 생성하기**
실행 클라이언트와 합의 클라이언트가 서로 통신하려면 비밀번호 같은 역할을 하는 시크릿 파일이 필요합니다.
아래 명령어로 생성해 주세요:

```bash
$ ./prysm.sh beacon-chain generate-auth-secret
```

*jwt.hex* 파일이 생겼을 거예요. 이 파일을 상위 폴더로 옮겨주세요:

```bash
$ mv jwt.hex ../jwt.hex
```

#### 노드 실행하기

이제 실행 클라이언트, 합의 클라이언트 모두 준비됐고, JWT 시크릿 파일도 제대로 만들었으니 이더리움 풀노드를 직접 돌릴 수 있습니다!

**실행 클라이언트(Geth) 실행하기**
먼저 *execution* 폴더로 이동해서 Geth를 실행해 봅시다:

```bash
$ cd .. # ethereum-node1 폴더로 이동
$ cd execution
$ ./go-ethereum/build/bin/geth --mainnet \
	--http \
	--http.api eth,net,engine,admin \
	--authrpc.jwtsecret=../jwt.hex
```

아래처럼 로그가 나오면 정상입니다:

```bash
INFO [06-08|17:56:38.738] Starting Geth on Ethereum mainnet...
INFO [06-08|17:56:38.738] Bumping default cache on mainnet         provided=1024 updated=4096
INFO [06-08|17:56:38.740] Maximum peer count                       ETH=50 total=50
INFO [06-08|17:56:38.745] Set global gas cap                       cap=50,000,000
INFO [06-08|17:56:38.752] Initializing the KZG library             backend=gokzg
INFO [06-08|17:56:38.771] Allocated trie memory caches             clean=614.00MiB dirty=1024.00MiB
INFO [06-08|17:56:38.772] Using pebble as the backing database…
```

**합의 클라이언트(Prysm) 실행하기**
이제 터미널 새 창 또는 새 탭을 열고, *consensus* 폴더로 가서 Prysm을 실행하세요:

```bash
$ cd ethereum-node1
$ cd consensus
$ ./prysm.sh beacon-chain \
	--execution-endpoint=http://localhost:8551 \
	--mainnet \
	--jwt-secret=../jwt.hex \
	--checkpoint-sync-url=https://beaconstate.info \
	--genesis-beacon-api-url=https://beaconstate.info
```

처음 실행할 때 Prysm의 이용 약관 동의 화면이 뜰 수도 있어요.
그럴 때는 **accept**라고 입력하면 됩니다:

```bash
Prysm Terms of Use
By downloading, accessing or using the Prysm implementation (“Prysm”), you (referenced
herein as “you” or the “user”) certify that you have read and agreed to the terms and
conditions below.
TERMS AND CONDITIONS: https://github.com/prysmaticlabs/prysm/blob/develop/TERMS_OF_SERVICE.md
Type “accept” to accept this terms and conditions [accept/decline]: (default: decline):
```

````
이제 끝났어요! 터미널에서 실행 클라이언트와 합의 클라이언트가 쉴 새 없이 로그를 쏟아내는 걸 볼 수 있을 거예요.

실행 클라이언트:

```bash
INFO [06-08|18:08:49.039] Forkchoice requested sync to new head    number=20,048,206 hash=8df21a..4afb49 finalized=unknown
INFO [06-08|18:08:52.507] Syncing beacon headers                   downloaded=322,560 left=19,725,577 eta=42m4.183s
INFO [06-08|18:08:57.515] Looking for peers                        peercount=1 tried=42 static=0
INFO [06-08|18:09:00.508] Syncing beacon headers                   downloaded=370,688 left=19,677,449 eta=43m35.827s
INFO [06-08|18:09:01.637] Forkchoice requested sync to new head    number=20,048,207 hash=d99dab..0293c9 finalized=unknown
````

합의 클라이언트:

```bash
[2024-06-08 18:09:24]  INFO blockchain: Called new payload with optimistic block payloadBlockHash=0xd44520a09a7a slot=9253245
[2024-06-08 18:09:24]  INFO blockchain: Called fork choice updated with optimistic block finalizedPayloadBlockHash=0x38916be8a559 headPayloadBlockHash=0xd44520a09a7a headSlot=9253245
[2024-06-08 18:09:24]  INFO blockchain: Synced new block block=0xec930e7c... epoch=289163finalizedEpoch=289161 finalizedRoot=0xb8065a78... slot=9253245
[2024-06-08 18:09:24]  INFO blockchain: Finished applying state transition attestations=123 payloadHash=0xd44520a09a7a slot=9253245 syncBitsCount=510 txCount=212
[2024-06-08 18:09:24]  INFO p2p: Peer summary activePeers=64 inbound=0 outbound=63
[2024-06-08 18:09:28]  INFO sync: Subscribed to topic=/eth2/6a95a1a9/beacon_attestation_35/ssz_snappy[2024-06-08 18:09:36]  INFO blockchain: Called new payload with optimistic block payloadBlockHash=0xff879102f29e slot=9253246
```

이제 이더리움 풀노드가 체인 맨 끝까지 동기화를 시작한 거예요. 동기화에는 하드웨어 성능과 인터넷 속도에 따라 몇 시간에서 며칠이 걸릴 수도 있습니다.

> **참고**
>
> 위 예제에서 사용한 명령어와 옵션이 궁금하다면, [Geth 공식 문서](https://oreil.ly/zYviP)와 [Prysm 공식 문서](https://oreil.ly/4sn6-)를 참고해 보세요.

### Reth-Lighthouse

이번에는 실행 클라이언트로 Reth, 합의 클라이언트로 Lighthouse를 써서 같은 과정을 반복해 볼게요.

#### Reth

먼저 Reth를 설치해야 합니다. *ethereum-node2* 폴더로 이동해서 *execution* 폴더로 들어가 주세요.

**저장소 클론하기**
먼저 Git 저장소를 복제해 소스 코드를 내려받아야 해요. 홈 디렉터리에서 아래 명령어를 입력하세요:

```bash
$ cd ethereum-node2
$ cd execution
$ git clone https://github.com/paradigmxyz/reth
```

좋아요! 이제 로컬에 Reth 소스가 준비됐으니, 실행파일로 빌드할 수 있습니다.

**Reth 빌드하기**
Reth를 빌드하려면 아래 명령어를 실행하세요:

```bash
$ cd reth
$ cargo install --locked --path bin/reth --bin reth
```

설치가 끝나려면 10분 이상 걸릴 수도 있어요.
완료 후에 아래처럼 실행해서 Reth가 잘 설치됐는지 확인해 보세요:

```bash
$ reth --version
```

아래와 비슷하게 나오면 성공입니다(버전은 달라질 수 있음):

```bash
reth Version: 0.2.0-beta.6-dev
Commit SHA: ac29b4b73
Build Timestamp: 2024-04-22T17:29:01.000000000Z
Build Features: jemallocBuild Profile: maxperf+
```

#### Lighthouse

이제 합의 클라이언트인 Lighthouse를 설치해볼게요. *ethereum-node2* 폴더로 돌아가서 *consensus* 폴더로 이동합니다:

```bash
$ cd .. # ethereum-node2 폴더로 돌아가기
$ cd consensus
```

먼저 의존성 패키지부터 설치해야 해요. macOS라면:

```bash
$ brew install cmake
```

다른 운영체제라면 [Lighthouse 공식 문서](https://oreil.ly/vEghS)에서 안내를 참고하세요.

**저장소 클론하기**
다음으로 Git 저장소를 복제합니다:

```bash
$ git clone https://github.com/sigp/lighthouse.git
```

이제 로컬에 Lighthouse가 준비됐으니, 빌드해볼게요.

**Lighthouse 빌드하기**
아래 명령어를 실행하면 빌드가 시작돼요(10분 이상 걸릴 수 있음):

```bash
$ cd lighthouse
$ git checkout stable
$ make
```

#### 노드 실행하기

이번에도 실행 클라이언트(Reth)를 먼저 실행해야 해요.

**실행 클라이언트 실행하기**
*execution* 폴더로 이동해서 Reth를 실행하세요:

```bash
$ cd ../.. # ethereum-node2 폴더로 이동
$ cp ../ethereum-node1/jwt.hex ./jwt.hex # 앞서 만든 jwt.hex 파일을 복사해서 사용합니다
$ cd execution
$ reth node --full --http --http.api all --authrpc.jwtsecret=../jwt.hex
```

아래처럼 나오면 정상이에요:

```bash
2024-06-08T16:58:43.498297Z  INFO Starting reth version="0.2.0-beta.6-dev (ac29b4b73)"
2024-06-08T16:58:43.498434Z  INFO Opening database path="/Users/alessandromazza/Library/Application Support/reth/mainnet/db"
2024-06-08T16:58:43.514141Z  INFO Configuration loaded path="/Users/alessandromazza/Library/Application Support/reth/mainnet/reth.toml"
2024-06-08T16:58:43.514778Z  INFO Database opened
2024-06-08T16:58:43.514917Z  INFO Pre-merge hard forks (block based):…
```

**합의 클라이언트 실행하기**
새 터미널 창/탭을 열고, *consensus* 폴더로 들어가서 Lighthouse를 실행하세요:

```bash
$ cd ethereum-node2
$ cd consensus
$ lighthouse bn \
	--checkpoint-sync-url https://mainnet.checkpoint.sigp.io \
	--execution-endpoint http://localhost:8551 \
	--execution-jwt ../jwt.hex \
	--genesis-beacon-api-url=https://beaconstate.info
```

그리고 완료! 실행 클라이언트와 합의 클라이언트가 터미널에 로그를 계속 쏟아내는 걸 볼 수 있을 거예요.

실행 클라이언트:

```bash
2024-06-08T17:03:03.355648Z  INFO Received headers total=10000 from_block=18458372 to_block=18448373
2024-06-08T17:03:04.792262Z  INFO Received headers total=10000 from_block=18448372 to_block=18438373
2024-06-08T17:03:04.800043Z  INFO Received headers total=10000 from_block=18438372 to_block=18428373
2024-06-08T17:03:04.913377Z  INFO Received headers total=10000 from_block=18428372 to_block=18418373
```

합의 클라이언트:

```bash
Jun 08 17:03:24.929 INFO New block received                      root: 0xa49c057026cea3190df38548d49963e271ebdc4d6f93d2301adc4034d6563113, slot: 9253515
Jun 08 17:03:29.001 WARN Head is optimistic                      execution_block_hash: 0x5a14bfcb9e74c5b3a5121f99ef461ae066262200c269b5d11475274eb78aa7a5, info: chain not fully verified, block and attestation production disabled untilexecution engine syncs, service: slot_notifier
Jun 08 17:03:29.001 INFO Synced                                  slot: 9253515, block: 0xa49c…3113, epoch: 289172, finalized_epoch: 289170, finalized_root: 0xca35…2b06, exec_hash: 0x5a14…a7a5 (unverified), peers: 31, service: slot_notifier
```

이제 이더리움 풀노드가 체인 끝까지 동기화되고 있어요! 동기화에는 시간(하드웨어/인터넷 속도에 따라 몇 시간~며칠)이 걸릴 수 있습니다.

> **참고**
>
> 여기 예제에서 사용된 명령어/옵션에 대해 더 알고 싶다면 [Reth 공식 문서](https://reth.rs)와 [Lighthouse 공식 문서](https://oreil.ly/vEghS)를 참고하세요.

다음 섹션에서는 이더리움 블록체인을 처음 동기화할 때 어떤 점이 어려운지 설명합니다.

> **꿀팁**
>
> 위 과정이 너무 복잡하게 느껴진다면? 그래도 내 이더리움 풀노드를 직접 돌리고, 제3자를 신뢰하지 않는 환경을 원한다면?
>
> 정말 쉬운 솔루션이 있어요! 바로 BuidlGuidl Client라는 프로젝트인데, 한 줄 명령어로 이더리움 노드를 돌릴 수 있습니다. 믿기 힘들다면 [직접 확인해보세요!](https://oreil.ly/9FKZd)
>
> 또 다른 방법으론 [Dappnode](https://dappnode.com)를 사용하는 것! 두 가지 선택지가 있습니다:
>
> * 이더리움 풀노드가 내장된 플러그앤플레이(plug-n-play) 디바이스 구매
> * 직접 설치해서 누구나 쉽게 풀노드를 돌릴 수 있게 해주는 Dappnode Core 소프트웨어 설치

## 이더리움 기반 블록체인 최초 동기화

이더리움 블록체인을 처음 동기화할 땐, 클라이언트가 제네시스 블록부터 지금까지 모든 블록과 트랜잭션을 다 다운받아 검증해야 해요.
이 방식도 가능하지만, 시간도 오래 걸리고 메모리와 저장장치 등 리소스 요구사항이 매우 높습니다.

2016년 말, 많은 이더리움 계열 블록체인들이 DoS 공격을 당했었어요.
이 영향으로 전체 동기화(풀 싱크)를 시도하면 특정 구간에서 속도가 급격히 느려지게 됩니다.
예를 들어 이더리움 메인넷에서는 블록 2,283,397(2016년 9월 18일)부터 DoS 공격이 시작되어, 블록 2,700,031(2016년 11월 26일)까지 트랜잭션 검증 속도가 엄청 느려졌죠. 그 시기에는 한 블록 검증에 1분 이상 걸렸습니다.
이후 여러 번의 하드포크를 통해 공격을 막고, 스팸 트랜잭션으로 생긴 2천만 개의 빈 계정도 정리했습니다.

풀 검증 모드로 동기화하면, 이 구간을 검증하는 데 며칠 이상 걸릴 수도 있어요.
다행히 대부분의 이더리움 클라이언트는 '빠른 동기화(fast sync)' 옵션이 있습니다.
빠른 동기화는 체인 맨 끝까지는 블록 검증을 생략하고, 최신 블록부터는 다시 모든 트랜잭션을 검증합니다.
실행 클라이언트에선 snap sync, 합의 클라이언트에선 checkpoint sync가 이 역할을 해요.
이번 튜토리얼에서는 기본적으로 이 옵션을 모두 사용했지만, Reth는 아직 snap sync를 지원하지 않아요(2025년 6월 기준).

## JSON-RPC 인터페이스

이더리움 클라이언트는 API, 즉 RPC 명령어 세트를 제공합니다.
이 명령들은 JSON으로 인코딩되어, 흔히 "JSON-RPC API"라고 불려요.
이 API를 통해 이더리움 클라이언트를 프로그램적으로 제어하거나, 블록체인 데이터를 가져올 수 있습니다.

일반적으로 이 RPC 인터페이스는 8545번 포트에서 HTTP 서비스로 제공돼요.
보안을 위해 기본적으로는 로컬호스트(127.0.0.1)에서만 접속 가능하게 설정되어 있습니다.

JSON-RPC API에 접근하는 방법은 여러 가지가 있어요.
직접 HTTP 요청을 만들어도 되고, 원하는 언어에 맞는 라이브러리를 써서 각 명령어에 맞는 함수처럼 쓸 수도 있죠.
또는 curl 같은 커맨드라인 HTTP 클라이언트로도 바로 호출할 수 있습니다.

예를 들어, 아래처럼 하면 실행 클라이언트가 잘 켜져 있다면 버전을 확인할 수 있어요:

```bash
$ curl -X POST -H "Content-Type: application/json" --data \
	'{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}' \
	http://localhost:8545

{"jsonrpc":"2.0","id":1,"result":"Geth/1.14.3-stable/darwin-arm64/go1.22.2"}
```

여기서 curl로 *[http://localhost:8545*에](http://localhost:8545*에) POST 방식으로, JSON 형식의 요청을 보낸 거예요.
재미있는 부분은 실제로 보내는 JSON-RPC 명령어 부분입니다:

```bash
{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}
```

이 요청은 [JSON-RPC 2.0 명세](https://oreil.ly/m0HLL)에 따라 네 가지 필드를 포함해요:

**jsonrpc**
프로토콜 버전(항상 "2.0")

**method**
실행할 메서드 이름

**params**
호출에 쓸 파라미터(없으면 생략 가능)

**id**
요청을 구분하는 식별자(숫자, 문자열, null 등), 응답에서도 같은 값으로 돌아옵니다

> **꿀팁**
>
> id 파라미터는 여러 요청을 한 번에 처리하는 ‘배치 요청(batch)’에서 주로 쓰여요. 배치는 매번 HTTP 연결을 새로 맺지 않고, 여러 요청을 한 번에 보내서 효율을 높이는 방법입니다. 예를 들어 수천 개 트랜잭션을 한 번에 조회하고 싶을 때 쓰죠. 각각의 요청마다 id를 다르게 해주면, 응답에서도 각각의 id로 결과를 확인할 수 있습니다. 보통 카운터를 하나 만들어서 요청마다 값을 올려주면 간단하게 구현할 수 있어요.

응답은 아래처럼 옵니다:

```bash
{"jsonrpc":"2.0","id":1,"result":"Geth/1.14.3-stable/darwin-arm64/go1.22.2"}
```

즉, 현재 Geth 1.14.3-stable 버전이 JSON-RPC API를 제공 중임을 알 수 있죠.

좀 더 재미있는 예로, 현재 가스 가격을 가져오는 명령어도 이렇게 쓸 수 있어요:

```bash
$ curl -X POST -H "Content-Type: application/json" --data \
	'{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":4213}' \
	http://localhost:8545
	
{"jsonrpc":"2.0","id":4213,"result":"0x1B1717FC7"}
```

0x1B1717FC7라는 응답값이 현재 가스 가격(7.27 gwei, 1 gwei = 10억 wei)이라는 뜻이에요.
16진수가 익숙하지 않다면, 커맨드라인에서 아래처럼 바꿔볼 수 있습니다:

```bash
$ echo $((0x1B1717FC7))
7271972807
```

전체 JSON-RPC API 목록은 [이더리움 위키](https://oreil.ly/lO2Z0)에서 확인할 수 있어요.

> **꿀팁**
>
> 여기서는 curl로 직접 요청을 보냈지만, 실제 개발에선 라이브러리를 쓰는 게 훨씬 편해요. 아래 유명 라이브러리들을 써볼 수 있습니다:
>
> * [ethers.js](https://oreil.ly/JKvSJ)
> * [web3.py](https://oreil.ly/dHSF4)
> * [alloy](https://alloy.rs)

## 원격 이더리움 클라이언트

원격(리모트) 클라이언트는 전체 클라이언트(풀 노드)가 제공하는 모든 기능을 다 하진 않아요. 대신 이더리움 블록체인을 전부 저장하지 않아서 설치도 빠르고 저장공간도 훨씬 적게 들어요.

보통 이런 클라이언트로 할 수 있는 일들은 아래와 같아요:

* 지갑에서 개인키랑 이더리움 주소 관리하기
* 트랜잭션 만들고, 서명해서 네트워크에 보내기
* 스마트 컨트랙트와 상호작용하기 (데이터 페이로드 사용)
* DApp(디앱)을 둘러보고 사용하기
* 블록 탐색기 같은 외부 서비스로 연결해주기
* 이더 단위 변환이나 환율 정보를 외부에서 받아오기
* 웹 브라우저에 Web3 인스턴스(자바스크립트 객체) 주입하기
* 다른 클라이언트가 제공하거나 주입한 Web3 인스턴스 사용하기
* 로컬이나 원격 이더리움 노드에 RPC 서비스로 접속하기

원격 클라이언트는 흔히 전체 노드와 연결해서, 블록체인을 내 컴퓨터에 동기화하지 않아도 주요 기능을 사용할 수 있어요. 연결 대상은 내 PC에서 직접 실행하는 전체 노드일 수도 있고, 웹 서버나 타사의 서버에 있는 전체 노드일 수도 있죠.

이제 인기 있는 원격 클라이언트와 각각의 주요 기능을 살펴볼게요.

### 모바일(스마트폰) 지갑

실제로 서비스 중인 모바일 지갑의 대부분은 원격 클라이언트로 동작해요. 스마트폰은 리소스가 부족해서 전체 이더리움 클라이언트를 돌리기엔 힘들거든요. 라이트 클라이언트도 개발은 되고 있지만, 이더리움에서 널리 쓰이진 않아요. 그나마 가장 유명한 게 [Helios](https://oreil.ly/4joTo)인데, 아직 실험 단계의 소프트웨어입니다.

인기 있는 모바일 지갑으로는 아래와 같은 것들이 있어요 (예시일 뿐, 공식 추천이나 보안·기능에 대한 보장은 아니에요):

**Coinbase Wallet**

이더리움(그리고 L2 포함), EVM 호환 L1, 비트코인, 솔라나, 라이트코인, 도지코인 등 여러 체인을 지원하는 모바일 지갑이에요. 코인베이스 계정과도 연동 가능해요.

**Phantom**

이것도 멀티체인 지갑이에요. 이더리움, 솔라나, 비트코인, 폴리곤을 지원해요.

**Trust Wallet**

100개가 넘는 블록체인을 지원하는 멀티체인 모바일 지갑이에요. iOS랑 안드로이드 모두에서 사용할 수 있어요.

**Uniswap Wallet**

유니스왑 팀에서 만든 모바일 지갑이에요. 이더리움이랑 EVM 호환 L1, L2만 지원해요. iOS, 안드로이드 모두에서 쓸 수 있고, 출시된 지는 꽤 최근이에요.

### 브라우저 지갑

브라우저(크롬, 파이어폭스 등) 확장 프로그램이나 플러그인으로 설치해서 쓸 수 있는 지갑이나 디앱 브라우저도 다양하게 있어요. 이런 것들도 브라우저 안에서 돌아가는 원격 클라이언트죠. 대표적으로 아래와 같은 것들이 있어요:

**MetaMask**

[MetaMask](https://metamask.io)는 [2장](https://masteringethereum.xyz/chapter_2.html#getting-started-with-metamask)에서 다뤘듯이, 다양한 기능을 가진 브라우저 지갑이에요. RPC 클라이언트이기도 하고, 기본적인 스마트 컨트랙트 탐색도 할 수 있어요. 크롬, 파이어폭스, 오페라, 브레이브 브라우저 등에서 쓸 수 있습니다.

**Phantom**

Phantom도 웹 브라우저 지갑이 있는데, 인터페이스가 아주 깔끔하고 사용하기 쉬워요.

**Rabby Wallet**

Rabby는 새로 나온 멀티체인 웹 브라우저 지갑이에요. 100개가 넘는 EVM 호환 체인을 지원합니다.

**Coinbase Wallet**

코인베이스 월렛도 웹 브라우저 버전이 있어요. 모바일 버전과 기능은 비슷해요.

### 하드웨어 지갑

대부분의 모바일·브라우저 지갑은 하드웨어 지갑이랑 연동해서 쓸 수 있어요. 하드웨어 지갑은 인터넷에 절대 직접 연결되지 않는, 오프라인 장치라 보안이 훨씬 더 좋아요. 물리적인 공격이나 변조에도 강하게 만들어졌죠. 대표적인 제품은 Ledger와 Trezor가 있어요.

## 마무리

이번 장에서는 이더리움 클라이언트에 대해 살펴봤어요. 클라이언트를 다운받고 설치해서 동기화하면, 여러분도 이더리움 네트워크의 일원이 되어 블록체인을 복제하면서 전체 시스템의 안정성과 건강에 기여하게 되는 거죠.

앞으로도 다양한 이더리움 클라이언트가 계속 나올 거예요. 워낙 연구와 개발이 활발하게 이루어지고 있으니까요. 앞으로 주목할 만한 주제는 이런 게 있어요:

**히스토리 프루닝(History pruning)**
풀 노드의 저장 공간 부담을 줄이기 위해 옛날 데이터를 잘라내는 기능

**버클 트리와 스테이트리스(Verkle trees and statelessness)**
이더리움 전체 상태를 가지지 않아도 블록을 검증할 수 있는 기술

**zk-EVM**
블록 안의 트랜잭션 전체를 재실행하지 않아도, 영지식증명(zk)을 통해 블록의 정당성을 검증하는 방법

이런 내용들은 다음 장들에서 차근차근 다뤄볼 거예요. 그 전에, 이 모든 걸 가능하게 하는 진짜 마법—암호학—에 대해 먼저 알아봅시다!
