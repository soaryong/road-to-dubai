# Cosmos Basic

Hello World!

모두 안녕하세요, 코스모스 베이직 과정에 오신 걸 환영합니다!

이번 로드 투 두바이라는 과정을 통해서, 제가 이렇게 코스모스 베이직 과정을 담당하게 된 이유는

개인적인 생각에 한국에서는 아쉽게도 코스모스 생태계에 대해서 아직 좋은 자료와 개발자들의 참여가 활발하지 못한 것 같아서

그 장벽을 허물고 코스모스 생태계라고 불리는 코스모스 SDK 기반의 앱체인 생태계에도 많은 한국 개발자들이 이해하고 참여하고 나아가 좋은 기회를 발견하실 수 있도록 도움을 주고 싶어서 이렇게 시작하게 되었습니다.

## 1. 코스모스 오버뷰

0. 블록체인 기초 & golang 기초

- 블록체인 기초

  - PoW & PoS
  - How to describe BLOCKCHAIN in one line
  - PBFT(tendermint)
  - 비트,이더 vs 텐더민트 큰 차이점(포크 유무)

- golang 기초
  - 퍼블릭 자료로 대체?
  - 우리가 티칭?

1. 앱 체인에 대한 필요성 공감(이해) aka 코스모스 출현배경

- [코스모스 출현 배경](https://ida.interchain.io/academy/1-what-is-cosmos/1-blockchain-and-cosmos.html)
  - 기존 블록체인(비트코인, 이더리움) 한계점
  - 인터체인 등장 배경 Tendermint
    - DPoS, PBFT
  - 비트,이더 vs 텐더민트 큰 차이점(포크 유무)
- [코스모스 인터체인 생태계](https://ida.interchain.io/academy/1-what-is-cosmos/2-cosmos-ecosystem.html)
  - 허브
  - IBC
    - ICQ (ICS-031)
  - ICA
  - CometBFT(fork tendermint)
  - cosmos-sdk (~v0.50)
    - x/(auth, authz, bank, stake, gov, liquidstaking, … 등) 모듈 설명
  - smart contract
    - 인터체인을 중심으로한 기존 cosmos 생태계에 스마트 컨트랙트를 어떻게 활용할 수 있는지에 대해 설명한다.
    - cosmwasm
    - ethermint(evmos, kava, polaris - bera, canto)
      - evm : precompile된 contract을 넣어서 cosmos-sdk
  - Ignite CLI
    - scaffold module, message, query, model
- ~~코스모스 아키텍처 및 구동 원리 (https://ida.interchain.io/academy/2-cosmos-concepts/1-architecture.html#)~~
  - ~~App~~
    - ~~Application Layer, Cosmos Layer~~
  - ~~ABCI~~
  - ~~Tendermint~~
    - ~~Consensus Layer, Networking Layer~~
    - ~~Tendermint Core~~
  - ~~상태머신~~
- [코스모스 생태계 현황](https://ida.interchain.io/academy/1-what-is-cosmos/3-interchain-use-cases.html)
  - 주요 체인들(Cosmoshub, Osmosis, Juno, DyDx, Sei, Stargaze, Evmos, Medibloc, …)
  - DEX: osmosis, astroport
  - Game
  - …

## 3. cosmos-sdk 설치

- cosmos-sdk를 위한 기본 환경(Dockr, Node.js, rust 등) 설치 (https://ida.interchain.io/tutorials/2-setup/)
- 아마 요 중간에 protobuf 와 buf package manager가 있어야 커스텀 모듈 만들 때 도움이 될듯

# 미션 작성 방향

- golang 기본 실습

- cosmos-sdk로 앱 체인 만들기 실습

| 미션                  | 설명                                                                                    |
| --------------------- | --------------------------------------------------------------------------------------- |
| Cosmos 앱 체인 만들기 | Cosmos SDK를 활용하여 앱 체인을 만들어 간단한 기능(account 생성 및 query)을 활용해본다. |

- Cosmos sdk로 직접 빌드해보기 (https://ida.interchain.io/tutorials/3-run-node/)
- Account 생성하기
- bank 모듈을 사용하여 토큰 stake 하기 |
  | bank 모듈 사용하기 | Cosmos SDK의 bank 모듈을 활용하여 토큰 전송(send) 기능을 활용해본다. |
  | staking 모듈 사용하기 | Cosmos SDK의 staking 모듈을 활용하여 토큰 스테이킹 기능을 활용해본다. |
  | governance 모듈 사용하기 | Cosmos SDK의 gov 모듈을 활용하여 proposal과 vote를 통해 탈중앙화 거버넌스 기능을 활용해본다. |
  | authz 모듈 사용하기 | Cosmos SDK의 authz 모듈을 활용하여 Account Abstraction 기능을 활용해본다. |
  | Relayer를 활용하여 앱 체인 간 상호작용 해보기 | Cosmos SDK의 Relayer를 활용하여 ICS-20 토큰 발행 및 전송을 해보며 앱 체인 간의 상호작용(Interchain Communication)을 다뤄본다. |
  | Name Service 커스텀 모듈 생성하기 | 자신이 생성한 Cosmos 앱 체인에 Name service 모듈을 추가하여 직접 커스텀해본다. |

# 추가 제안 및/혹은 요청 사안

1. 지금 생각해보니까 각자 나 처럼 굉장히 퓨어한 깡통 앱체인을 만들어 본다.

- https://github.com/Jeongseup/jeongseupchain/blob/main/app/app.go

2. 그런 개인 앱체인에 모듈을 하나 추가해본다.

3. 좀 더 실증적인 프로젝트를 참고해서 모듈을 추가하고 반영해본다.

4. 시간이 남으면 와즘 붙여보기

5. object capability model? -> 이거 설명하면 CS 자료구조 알고리즘 대강이라도 알고있다고 쳐야함

The Cosmos SDK is built on the [**object-capability model (opens new window)**](https://docs.cosmos.network/v0.45/core/ocap.html). It not only favors modularity but also encapsulates code implementation. An object-capability model ensures that:

https://docs.cosmos.network/v0.45/core/ocap.html

6. 마지막으로는 민트스테이션 사용해보기?
