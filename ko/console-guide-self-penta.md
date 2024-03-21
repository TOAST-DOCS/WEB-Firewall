## Security > WEB Firewall > 콘솔 사용 가이드 > Self > 펜타시큐리티(WAPPLES SA)

WEB Firewall Self 서비스에서는 웹 서버를 보호할 수 있도록 웹 방화벽 인스턴스를 생성하고 운영할 수 있는 가이드를 제공합니다.
여기에서는 WEB Firewall Self 서비스 사용 방법을 소개합니다.

WEB Firewall 서비스를 이용하려면 **NHN Cloud Console**에 로그인하고, 서비스 목록에서 **Security > WEB Firewall**을 클릭합니다.

## 서비스 신청 및 해제

![webfirewall_console_guide_self_1_240321.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_web_firewall/Penta/webfirewall_console_guide_self_1_240321.png)

### 웹 방화벽 생성

1. **WEB Firewall** 콘솔의 **Self 이용 신청**에서 **바로가기** 버튼을 클릭해 인스턴스 생성 페이지로 이동합니다.
2. **+ 인스턴스 생성**을 클릭하고 이미지 목록에서 PENTA WAF를 선택한 후 인스턴스 정보를 입력합니다. 자세한 방법은 아래 **웹 방화벽 인스턴스 생성 세부 절차**를 참고하시기 바랍니다.

※ 인스턴스가 생성되는 즉시 이용 요금이 부과됩니다.

### 웹 방화벽 해제

웹 방화벽 인스턴스를 선택하고 삭제합니다.

※ 웹 방화벽 구성 시 트래픽이 웹 방화벽으로 경유되어 이용하는 도중에 인스턴스를 삭제할 경우 서비스 장애가 발생할 수 있습니다.<BR>
※ 사용 중인 웹 서비스를 확인한 후 인스턴스를 삭제하시기 바랍니다.

## 웹 방화벽 인스턴스 생성 세부 절차

![webfirewall_console_guide_self_1_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_penta_230904.png)

※ 아래 예시와 같이 신뢰하는 IP 및 사용 포트에 대해서 보안 그룹(security group)을 설정합니다.

| Direction | IP 프로토콜 | 포트 범위 | 원격 | 설명 |
| :-------: | :-----: | :---: | :---: | :--- |
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | WAF 웹 서비스 포트 |
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | WAF 웹 서비스 포트 |
| Ingress | TCP | 5001 | x.x.x.x/32 (CIDR) | WAF 관리도구(UI) 포트(관리자 IP만 허용) |
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | WAF SSH 터미널 포트(관리자 IP만 허용) |
| Ingress | TCP/HTTP | 5000 | WAF의 상단 LB의 IP<BR>x.x.x.x/32 (CIDR) | WAF(이중화)와 상단 LB간 헬스체크(health check) 포트 |
| Egress | TCP | 443 (HTTPS) | 218.145.29.166/32 (CIDR) | WAF 라이선스 업데이트 서버 
| Egress | TCP | 443 (HTTPS) | 218.145.29.101/32 (CIDR) | WAF 라이선스 업데이트 서버 |
| Egress | TCP | 5001 | 218.145.29.168/32 (CIDR) | WAF 보안룰(custom rule) 업데이트 서버 |

※ 참고 : WAF 이중화(설정 동기화 기능 사용 시) 또는 Auto Scaling 사용 시 WAF 간 5984, 6984 포트 허용 필요

## 웹 방화벽 초기 설정

* WAF 최초 구동 후 초기 설정 하기

1. 브라우저(크롬 권장)에서 웹방화벽 웹 관리도구(UI) 접속
    * https://WAF IP:5001
    * 로그인 접속 정보 : ct@pentasecurity.com 로 문의

2. 환경설정 > 시스템 > 시간동기화 설정하기
    * 시간 서버 각각 Penta Server 1 &  Penta Server 2 설정하기

3. 네트워크 설정 > 프록시IP 설정하기
    * NHN console 에서 확인한 네트워크 정보 입력(WAF IP, gateway, netmask)

4. WAF 보호대상 설정 하기
    * 네트워크 설정 > 보호대상 서버 설정하기
    * 서버 모드 : Proxy 선택 및 port 입력
    * 웹서버 IP(도메인)과 port 입력 (인프라 구성에 따라 '단일' 또는 '다중' 선택 가능)
    * 헬스체크 사용 안함 (웹서버 도메인 입력 시만 사용)
    * WAF가 HTTPS 서비스 할 경우 SSL 인증서 지정 (SSL 프로파일 메뉴에서 사전 설정 필요)

5. 보호 정책 설정 하기
    * 보안설정 > 정책 설정 > 신규 정책 추가 (기반 정책: '탐지만 하고 차단 안함' 선택)
    * 보안설정 > 정책 설정 > 신규 웹사이트 추가 (신규 정책에 적용)

6. X-Forwarded-For IP 설정하기
    * 보안설정 > 정책 부가 설정 > X-Forwarded-For 설정 (Block & Detect 모두 설정)

* WAF 적용 시 참고사항
    * NHN cloud Managed Service 사업자(MSP)를 통해 고객 인프라 환경에 WAF 서비스가 적용 되도록 네트워크 routing을 변경 구성합니다.
    * 고객 인프라 구성에 따라 WAF 플로팅 IP로 DNS 변경이 필요하거나, WAF 이중화 구성 시 상단 로드밸런서 IP로 DNS 변경이 필요할 수 있습니다.

## 웹 방화벽 운영

* 웹 방화벽의 전반적인 사용자 메뉴얼 및 이용 방법은 웹방화벽의 관리도구(UI)에서 제공합니다.
* 아래 화면의 메뉴얼 위치를 참고하여, 웹방화벽 운영 전반의 이용 가이드를 참고하시기 바랍니다.
![wapples_manual.png](https://static.toastoven.net/prod_web_firewall/wapples_manual.png)

※ Self 서비스에서는 사용 가이드만 제공되며, Managed 서비스 이용 시 운영 대행 및 24시간 보안관제 서비스를 제공합니다.
