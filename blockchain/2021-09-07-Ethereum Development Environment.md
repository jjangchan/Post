# 1. 이더리움 개발 환경 설치(Ethereum Development Environment)



## 1.1 Intall node.js and npm

RPC 방식으로 이더리움 노드와 통신을 제공하는 공식 클라이언트 라이브러리는 `web.js`다 따라서 `node.js`와 `npm`을 설치해야 한다.



### macOS

```
# if not installed brew
# /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew install node
```



### Ubuntu 20.04.3 LTS

```
sudo apt install nodejs npm

# macOS 패키지 명의 일관성을 유지한다.
sudo ln -s /usr/bin/nodejs /usr/bin/node
```



## 1.2 Install solidity

```
sudo npm install -g solc
```



## 1.3 이더리움 클라이언트(ethereum clinet)

이더리움 클라이언트는 이더리움 프로토콜 구현체로서, 이더리움 네트워크 및 블록체인과 통신하는 프로그램이다. 이더리움 클라이언트의 역할은 다음과 같다.

- 새로운 체인 동기화
- 새 블록 다운로드 및 확인
- 피어와 연결
- 트랜잭션 확인 및 실행
- 로컬 트랜잭션을 네트워크로 브로드캐스트
- 기본적인 채굴 기능 제공
- 종류는 Geth, 가나슈(Ganache), Eth, 패리티(Parity) 등이 있다.



## 1.4 Install Geth(go-ethereum)

### macOS

```
brew tap ethereum/ethereum
brew install ethereum
```



### Ubuntu 20.04.3 LTS

```
sudo apt install -y golang
sudo apt install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt update
sudo apt install ethereum
```



## 1.5 트러플이란?

트러플은 솔리디티 및 EVM의 개발 프레임워크다. 대체로 컨트랙트의 컴파일, 배포, 테스트 절차를 간소화해준다.



### install truffle

```
sudo npm install -g truffle
```



### ex) 트러플로 간단한 댑 배포하기

```
cd ~
mkdir truffle-test
cd truffle-test

# 일련의 폴더와 예제 파일을 생성
truffle init

# 가나슈를 실행하는 트러플 개발 콘솔 열기
truffle develop

migrate

.exit
```



## 1.6 Geth 명령어



| 설명                                   | 명령                                         |
| -------------------------------------- | :------------------------------------------- |
| 기본 동작을 위한 geth모드              | geth                                         |
| 통신용 콘설(로그가 없는 사일런트 모드) | geth console --verbosity 0                   |
| 명령 도움말                            | geth help                                    |
| 링키비 테스트넷                        | geth -rinkeby                                |
| 계정 관리                              | geth account                                 |
| 계정 생성                              | geth account new                             |
| 메인넷 동기화                          | geth --syncmode "fast" --cache=1024          |
| 링키비 동기화                          | geth --rinkeby --fast --cache=1024           |
| RPC 모드                               | geth -rpc                                    |
| 로컬 지갑 접근을 위한 RPC 모드         | geth --rpc -rpcapi, web3, eth, net, personal |
| 커스텀 네트워크 포트 수신              | geth --post <port>                           |
| 커스텀 RPC 포트 수신                   | geth --rpc --rpcport <port>                  |



더 자세한 내용은 [ref Geth](https://geth.ethereum.org/docs/dapp/native-bindings) 에서 찾을 수 있다.



# 2. 블록 체인 연결하기

- 컨트랙트를 배포하거나 네트워크 트랜잭션을 실행하려면 사용할 각 네트워크에 전체 노드를 동기화해야 한다.

- 테스트넷은 이더움 프로토콜을 실행하지만 토큰이 없는 네트워크라고 할 수 있다. 가스 비용을 지불하지 않고도 코드, 배포, 트랜잭션을 테스트 할 수 있다.

- 모든 퍼블릭 이더리움 네트워크에는 고유한 네트워크 ID가 있다. 이더리움 메인넷 네트워크 ID는 1 이며, 링키비 테스트넷 네트워크 ID는 4이다.
- 프라이빗 페인은 다른 네트워크와의 동기화를 피하기 위해 네트워크 ID로 큰 크기의 고유 난수를 사용하는 것이 좋다.



## 네트워크 동기화

Geth에서는 세 가지 모드로 네트워크 동기화를 진행할 수 있다.

1. 라이트 노드는 블록 헤더를 동기화 하지만 트랜잭션을 처리하거나 상대 트리를 유지 관리하지 않는다.
2. 풀 노드는 블록체인 상대 트리의 로컬 스냅숏을 유지하고 전체 블록을 다운로드하고 블록체인의 로컬 복사본에서 블록 트랜잭션을 실행하고 합의 프로세스에 참여한다.
3. 아카이브 노드는 풀 아카이브 노드라고 불리는데, 상대 트리의 현재 스냅숏뿐 아니라 제네시스 블록 이후 블록체인에서 발생한 모든 상태 전환의 복사본을 유지한다.



## 메인넷 동기화

```
# Blockchain sync mode ("fast", "full", "snap" or "light") (default: snap)
geth --syncmode "fast" --cache=1024
```



## 테스트넷 동기화

```
# 포트 충돌이 나므로 port를 커스텀해서 변경
geth --rinkeby --port 31303
```



## 포우셋

포우셋은 테스트를 위한 암호화폐를 무료로 지급하는 웹사이트이다.