## 에이치투오시스템테크놀리지

- Human to office
- 국내 유일 MOM(Message Oriented Middleware) 기술 보유 업체입니다.
- 분산처리시스템을 담당하고 있는 시스템 소프트웨어 회사
- 실시간 글로벌 트레이딩 시스템에 클라우드를 적용해서 런칭
- front office, 증권사 통합 보고서 관리 시스템, 모바일 트레이딩 시스템, OPenMCM



분산 처리 시스템을 담당하고 있는 시스템 소프트웨어 회사이며, 다양한 미들웨어 제품을 출시하고 금융 분야에서는 국내 유일 Message Oriented Middleware 기술을 보유하고 있습니다. 금융 서비스로는 front office, 증권사 통합 보고서 관리 시스템, 모바일 트레이딩 시스템, OpenMCM 서비스를 하고 있습니다.



### 미들웨어

분산 컴퓨팅 환경에서 서로 다른 기종의 하드웨어, 프로토콜, 통신환경 들을 연결하여, 응용프로그램과 그 프로그램이 운영되는 환경간에 원만한 통신이 이루어질수 있게 하는 중간자 역할을 하는 소프트웨어 



### TLS 암호화 방식

- 비대칭키 + 대칭키 알고리즘을 사용
- 대칭키는 보안에 취약하고, 비 대칭키는 계산이 오래 걸리고 cpu 리소스를 크게 소모하는 단점이 있음

따라서, 서버에 공개키로 대칭키을 암호화 하고, 서버에서는 암호화된 대칭키를 개인키로 복호화해서 대칭키을 알아내서 대칭키로 평문을 암호화해서 둘이 주고 받는 방식이다.



### CA 기관 인증서 발급 방법

CA(**Certificate Authority**) 기관에 서버가 인증 받는 방법은, 우선적으로 서버의 정보 도메인과 공캐키를 전달한다

- CA에서 서버의 공개키를 해시해서 지문(**Finger Print**) 등록
- 지문을 CA의 비밀키로 암호화해서 디지털 서명(**Digital Signing**) 등록
- 지문과 디지털 서명이 담은 인증서 발급 
- 클라이언트에서 서버랑 통신하려면 인증서 확인, apple 일 경우에는 keychain 에서 ca기관 공개키 검색
- 서명을 공개키로 복호화 후, 해시된 서버의 공개키 값(지문)과 일치한지 판별





