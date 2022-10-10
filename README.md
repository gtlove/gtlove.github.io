# gtlove.github.io

글로벌 서비스를 위한 시스템 구축 시 아키텍처 검토사항 및 시스템 설계 방안

AWS : https://aws.amazon.com/ko/blogs/korea/creating-a-multi-region-application-with-aws-services/

AWS를 이용한 Global 서비스 인프라 설계
https://www.joinc.co.kr/w/Site/cloud/AWS/GlobalService


Regulation (법규 및 규정 준수)
Data Replication
Operation
Time to market

글로벌 서비스?
- 대량의 트래픽
- 여러 국가에서 서비스하여 지연시간
- 각 국가별 법률 및 규정 준수 (Regulation) : 데이터 보존 및 개인 정보 보호 요구 사항 준수 등
- 다수의 서버, 배포 파이프라인 자동화
- i18n 지원
- 

(
Regulation
지연시간
서비스배포
)


Software layer
 proxy (api gateway 관련 항목들)
  routing
 protocol
  rest / thrift, protobuffer
  thrigt

 biz logic
  no shared data, stateless
   scalability, prevent trouble propagation

가용성, 확장성, 보안

DevOps, 자동화

Infrastructure layer
 - Location
   사업 대상 지역 (시간/비용/인력 비용 큼)
   기 구축되어진 데이터 센터나 ISP (서비스 품질 하락)
   글로벌 public cloud 사업자 (학습, 제공 서비스 확인 필요)
 - 컨텐트 속도 비용
   CDN 서비스 비용
   데이터 트래픽 비용
   DNS 서비스 --- 찾아보자
 - 데이터베이스 및 스토리지

 - 캐시, 검색, 로깅

 - 중앙 관리 (Chef server - 전체 인프라 관리)
   Git & CI
   Admin toolls (빌링, 모니터링, 유저, 보안정책, 자원 현황, 서비스 통계 등)	https://www.joinc.co.kr/w/Site/cloud/AWS/GlobalService
   작업 요청 시스템 (ex. jira)

 - 자원 접근 통제
 - 네트워크 격리
 - 서비스 트래픽, 관리 트래픽 분리 (OpenVPN, ...)
 - 모니터링
 - 보안 정책

 * 정적 데이터 저장 공간 분리
  HTML, CSS, JS, Image, File, ...
  ObjectStorage 사용하여 고유 URL
  CDN 서비스 사용 (AWS CloudFront, Akamai, ...)
  PoP (Points of Presence) 

 * DB 서버 안정성
  Read replication

 * CQRS 패턴
  Command와 쿼리 책임을 분리
  https://azderica.github.io/02-architecture-msa/
  https://webcache.googleusercontent.com/search?q=cache:M8lrK1olH1YJ:https://always-kimkim.tistory.com/entry/cqrs-pattern&cd=3&hl=ko&ct=clnk&gl=kr
 
 * DNS Lookup 
  짧은 서비스 downtime을 위한 짧ㅇ느 TTL 낮게 설정한 경우? 한국 네임 서버 부하
  static 서버 등 다수 도메인 서버 일 것이다. reverse proxy 인 경우 아니라면
  dns 조회에 따른 지연 시간 늘어진다.
  DNS anycast 와 같은 방법을 통해 근거리 네임서버 질의 사용

DR 은???

GSLB
 전통 DNS를 발전시킨 형태 서버 상태를 확인 후 IP 정보를 배포
  LB, DR, 클라우드를 백업 서비스로 이용 등 활용


다국어 
사용자 데이터를 해당 국가 내에서 저장

통화

결제 시스템
- 신용카드, paypal, 현금, 선구매 후결제 ...
-----------

https://kerberosj.tistory.com/186
웹 서비스의 해외 진출 시 고려 사항
