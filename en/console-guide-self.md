## Security > Web Firewall > 콘솔 사용 가이드 > Self

Web Firewall Self 서비스는 웹 서버를 보호할 수 있도록 웹 방화벽 Instance를 생성하고 운영할 수 있는 가이드를 제공합니다.
아래에서 Web Firewall Self 서비스 사용 방법을 소개합니다.

Web Firewall 서비스를 이용하기 위해 **TOAST Cloud Console**에 로그인하고, 서비스 목록 내 Security > Web Firewall 을 클릭하여 활성화합니다.

## 서비스 신청 및 해제

![webfirewall_01_201812.png](https://static.toastoven.net/prod_web_firewall/webfirewall_01_201812.png)

### 웹 방화벽 생성

1. Console 내 이용 신청 <span style="color:#1995dc">**\|바로 가기\|** </span> 버튼을 통해 Instance 생성 페이지로 이동
2. Image 리스트에서 PLOS WAF 선택 후 Instance 정보를 입력 후 생성

※ Instance 생성이 완료되는 즉시 이용 요금이 부과됩니다.

### 웹 방화벽 해제

웹 방화벽 Instance 선택 후 삭제

※ 웹 방화벽 구성 시 트래픽이 웹 방화벽으로 경유되어 이용 중 Instance를 삭제할 경우 서비스 장애가 발생할 수 있습니다.
※ 사용중인 웹 서비스 확인 후에 Instance 삭제를 권고 드립니다.

## 웹 방화벽 Instance 생성 세부 절차

![webfirewall_02_201812.png](https://static.toastoven.net/prod_web_firewall/webfirewall_02_201812.png)

※ 아래 예시와 같이 신뢰된 IP 및 사용 포트에 대해서 Security Groups 설정을 진행합니다.

| Direction | IP 프로토콜 | 포트 범위 | 원격 | 설명 |
| :-------: | :-----: | :---: | :---: | :--- |
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | 웹 서비스 포트 |
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | 웹 서비스 포트 |
| Ingress | TCP | 8443 | x.x.x.x/32 (CIDR) | 웹 방화벽 관리용 포트 (관리자 IP만 허용) |
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | 웹 방화벽 터미널 포트 (관리자 IP만 허용) |
| Ingress | ICMP | - | 192.168.0.0/24 (CIDR) | 웹 방화벽과 웹 서버 간 Health Check 통신 |

※ 웹 방화벽의 기본 Health Check 방식은 ICMP로 설정되어 있으며, 웹 서버와 Health Check 실패 시 웹 서비스가 동작하지 않습니다.

## 웹 방화벽 초기 설정

웹 방화벽 초기 설정 가이드를 참고하여 초기 설정을 진행하며, 주요 내용은 다음과 같습니다.

* 애플리케이션을 설정합니다.
* 부하분산 메뉴에서 실제 보호받을 서버에 대해 설정합니다.
* Proxy로 동작시키기 위해 Source NAT 기능을 활성화합니다.
* 웹 방화벽 IP로 접근 테스트하여 웹 서비스 정상 여부를 확인합니다.
* 설정한 내용을 저장하고 백업합니다.

[WEBFRONT-KS 초기 설정 가이드](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_초기%20설정%20가이드.pptx)
※ 초기 설정 완료 후, 보호 대상 도메인 트래픽이 웹 방화벽으로 경유 되도록 웹 방화벽 Floating IP로 DNS 변경 작업이 필요합니다.

## 웹 방화벽 운영

웹 방화벽 구성 설명서를 참고하여 장비 운영을 진행하며, 주요 내용은 다음과 같습니다.

* 사용할 보안정책을 활성화합니다.
* 학습기능을 활용하여 예외처리 등 정책 최적화를 진행합니다.
* 보안 로그를 모니터링 합니다.

[WEBFRONT-KS 애플리케이션 구성 설명서](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_애플리케이션%20구성%20설명서.pdf)
[WEBFRONT-KS 시스템 구성 설명서](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_시스템%20구성%20설명서.pdf)
※ Self 서비스에서는 사용 가이드만 제공되며, Managed 서비스 이용 시 운영 대행 및 24시간 보안 관제 서비스를 제공합니다.