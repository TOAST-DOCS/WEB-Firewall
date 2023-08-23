## Security > WEB Firewall > 콘솔 사용 가이드 > Self > 파이오링크(WEBFRONT-KS)

WEB Firewall Self 서비스에서는 웹 서버를 보호할 수 있도록 웹 방화벽 인스턴스를 생성하고 운영할 수 있는 가이드를 제공합니다.
여기에서는 WEB Firewall Self 서비스 사용 방법을 소개합니다.

WEB Firewall 서비스를 이용하려면 **NHN Cloud Console**에 로그인하고, 서비스 목록에서 **Security > WEB Firewall**을 클릭합니다.

## 서비스 신청 및 해제

![webfirewall_console_guide_self_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_220613.png)

### 웹 방화벽 생성

1. **WEB Firewall** 콘솔의 **Self 이용 신청**에서 **바로가기** 버튼을 클릭해 인스턴스 생성 페이지로 이동합니다.
2. **+ 인스턴스 생성**을 클릭하고 이미지 목록에서 PLOS WAF를 선택한 후 인스턴스 정보를 입력합니다. 자세한 방법은 아래 **웹 방화벽 인스턴스 생성 세부 절차**를 참고하시기 바랍니다.

※ 인스턴스가 생성되는 즉시 이용 요금이 부과됩니다.

### 웹 방화벽 해제

웹 방화벽 인스턴스를 선택하고 삭제합니다.

※ 웹 방화벽 구성 시 트래픽이 웹 방화벽으로 경유되어 이용하는 도중에 인스턴스를 삭제할 경우 서비스 장애가 발생할 수 있습니다.<BR>
※ 사용 중인 웹 서비스를 확인한 후 인스턴스를 삭제하시기 바랍니다.

## 웹 방화벽 인스턴스 생성 세부 절차

![webfirewall_console_guide_self_1_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_1_220523.png)

※ 아래 예시와 같이 신뢰하는 IP 및 사용 포트에 대해서 보안 그룹(security group)을 설정합니다.

| Direction | IP 프로토콜 | 포트 범위 | 원격 | 설명 |
| :-------: | :-----: | :---: | :---: | :--- |
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | 웹 서비스 포트 |
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | 웹 서비스 포트 |
| Ingress | TCP | 8443 | x.x.x.x/32 (CIDR) | 웹 방화벽 관리용 포트(관리자 IP만 허용) |
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | 웹 방화벽 터미널 포트(관리자 IP만 허용) |
| Ingress | ICMP | - | 192.168.0.0/24 (CIDR) | 웹 방화벽과 웹 서버 간 상태 확인(health check) 통신 |

※ 웹 방화벽의 기본 상태 확인(health check) 방식은 ICMP로 설정되어 있으며, 웹 서버와 상태 확인(health check) 실패 시 웹 서비스가 동작하지 않습니다.

## 웹 방화벽 초기 설정

* 웹 방화벽 초기 설정 가이드를 참고하여 초기 설정을 진행하며, 주요 내용은 다음과 같습니다.

  * 애플리케이션을 설정합니다.
  * 부하 분산 메뉴에서 실제 보호받을 서버를 설정합니다.
  * 프락시로 동작하게 하려면 Source NAT 기능을 활성화합니다.
  * 웹 방화벽 IP로 접근하는 것을 테스트하여 웹 서비스 정상 여부를 확인합니다.
  * 설정한 내용을 저장하고 백업합니다.

[WEBFRONT-KS 초기 설정 가이드](https://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_초기%20설정%20가이드.pdf)
* 초기 설정 완료 후, 보호 대상 도메인 트래픽이 웹 방화벽으로 경유하도록 웹 방화벽 플로팅 IP로 DNS를 변경해야 합니다.
* 제조사에서 제공하는 릴리스 노트를 참고하여 웹 방화벽 PLOS 버전을 최신으로 업데이트해야 합니다.
  * 릴리스 노트 다운로드 방법: 웹 방화벽 접속 > SYSTEM > 일반 설정 > PLOS 관리 > 다운로드 PLOS > 다운로드

## 웹 방화벽 운영

웹 방화벽 구성 설명서를 참고하여 장비를 운영하며, 주요 내용은 다음과 같습니다.

* 사용할 보안 정책을 활성화합니다.
* 학습 기능을 활용하여 예외 처리 등 정책 최적화를 진행합니다.
* 보안 로그를 모니터링합니다.

[WEBFRONT-KS 애플리케이션 구성 설명서](https://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_애플리케이션%20구성%20설명서.pdf)
[WEBFRONT-KS 시스템 구성 설명서](https://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_시스템%20구성%20설명서.pdf)
※ Self 서비스에서는 사용 가이드만 제공되며, Managed 서비스 이용 시 운영 대행 및 24시간 보안관제 서비스를 제공합니다.
