## Security > WEB Firewall > 콘솔 사용 가이드 > Self

웹 방화벽 Self형 서비스는 웹 서버를 보호할 수 있도록 웹 방화벽 Instance를 생성하고 운영할 수 있는 가이드를 제공합니다.
아래에서 Web Firewall Self 형 서비스 사용 방법을 소개합니다.

Self형 Web Firewall 서비스를 이용하기 위해 **TOAST Cloud Console**에 로그인하고, 서비스 목록 내 Security>Web Firewall 을 클릭하여 활성화합니다.

## 서비스 신청 및 해제

### 웹 방화벽 생성

1. TOAST Cloud Console 내 이용 신청 <span style="color:#1995dc">**\|바로 가기\|** </span> 버튼을 통해 Instance 생성 페이지로 이동
2. Image 리스트에서 PLOS 선택 후 Instance 정보를 입력 후 생성
※ Instance 생성이 완료되는 즉시 이용 요금이 부과됩니다.

### 웹 방화벽 해제

1. 웹 방화벽 Instance 선택 후 삭제
※ 웹 방화벽 보호 서비스 이용 중 Instance를 삭제할 경우 서비스 장애가 발생할 수 있으니 주의하시기 바랍니다.

## 웹 방화벽 Instance 생성 세부 절차

1. Instance 생성

* Image 탭에서 PLOS WAF 선택

![waf_02.png](/files/2134548686701164473)
[그림1] 웹 방화벽 Instance 생성

2\. Instance 정보 입력

* Availability Zone : Instance가 생성될 존
* 이름 : Instance 이름
* Flavor : 하드웨어 스펙
* 장치 크기 (GB) : 용량
* Instance 수 : Instance 생성 개수

![waf_03.png](/files/2134549570623236718)
[그림2] 웹 방화벽 Instance 정보 입력

※ 권장사양

* 아래 표를 참고하여 고객 서비스 환경에 따라 알맞은 Flavor 및 장치 크기를 설정하시기 바랍니다

![waf_04.png](/files/2134551003034178006)
[그림3] 웹 방화벽 권장사양

3\. Key Pairs & Security 설정

* SSH 터미널 접근에 사용할 Key Pairs를 생성하고 선택합니다.
* 적용할 Security Groups 을 선택하여 접근제어를 적용합니다.
※ 허용된 IP 및 포트에 대해서만 접근할 수 있도록 설정을 권고합니다.

4\. Network 설정

* 사용할 네트워크를 선택합니다.
※ 웹 방화벽과 웹서버는 동일 네트워크로 설정하여야 서비스할 수 있으므로 주의하시기 바랍니다

5. Floating IP 연결

* 웹 방화벽 공인 IP를 설정합니다.
* 설정할 Instance를 클릭하고 상단 추가 기능 탭에서 Floating IP 연결을 클릭합니다.

![waf_05.png](/files/2134563431558164773)
[그림4] 웹 방화벽 Floating IP 연결

## 웹 방화벽 초기 설정

웹 방화벽 설정 가이드 문서를 참고하여 초기 설정을 진행하며, 주요 내용은 다음과 같습니다.

* 애플리케이션을 설정하고 활성화합니다.
* 부하분산 메뉴에서 실제 보호받을 서버에 대해 설정합니다.
* Proxy로 동작시키기 위해 Source NAT 기능을 활성화합니다.
* 웹 방화벽 IP로 접근 테스트하여 웹서비스 정상 여부를 확인합니다.
* 설정한 내용을 저장하고 백업합니다.

[Piolink WEBFRONT 초기 설정 가이드](aaa)
※ 초기 설정 완료 후, 보호 대상 도메인 트래픽이 웹 방화벽으로 경유 되도록 웹 방화벽 Floating IP로 DNS 변경 작업이 필요합니다

## 웹 방화벽 운영

웹 방화벽 운영 가이드 문서를 참고하여 장비 운영을 진행하며, 주요 내용은 다음과 같습니다.

* 사용할 보안정책을 활성화합니다.
* 학습기능을 활용하여 예외처리 등 정책 최적화를 진행합니다.
* 보안 로그를 모니터링 합니다.

[Piolink WEBFRONT 운영 가이드(Application)](aaa)
[Piolink WEBFRONT 운영 가이드(System)](aaa)
