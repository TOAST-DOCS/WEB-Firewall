## Security > WEB Firewall > 콘솔 사용 가이드 > Self > 파이오링크(WEBFRONT-KS)

WEB Firewall Self 서비스에서는 웹 서버를 보호할 수 있도록 웹 방화벽 인스턴스를 생성하고 운영할 수 있는 가이드를 제공합니다.
여기에서는 WEB Firewall Self 서비스 사용 방법을 소개합니다.

WEB Firewall 서비스를 이용하려면 **NHN Cloud Console**에 로그인하고, 서비스 목록에서 **Security > WEB Firewall**을 클릭하여 서비스를 활성화합니다.

![webfirewall_gov_kr_console-guide-self-piolink-gov_01_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_01_241122.png)<br><br>

## 서비스 신청 및 해지
<br>

### 웹 방화벽 생성

![webfirewall_gov_kr_console-guide-self-piolink-gov_02_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_02_241122.png)
![webfirewall_gov_kr_console-guide-self-piolink-gov_03_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_03_241122.png)

1. **WEB Firewall** 콘솔의 **Self 이용 신청**에서 **바로 가기**를 클릭해 "Compute > Instance" 페이지로 이동합니다.
2. **+ 인스턴스 생성**을 클릭하고 이미지 목록에서 PLOS WAF를 선택한 후 인스턴스 정보를 입력합니다. 자세한 방법은 아래 **웹 방화벽 인스턴스 생성 세부 절차**를 참고하십시오.

> [참고]
> * 인스턴스가 생성되는 즉시 이용 요금이 부과됩니다.

<br>

### 웹 방화벽 해지

![webfirewall_gov_kr_console-guide-self-piolink-gov_04_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_04_241122.png)

1. 인스턴스 목록에서 웹 방화벽 인스턴스를 선택합니다.
2.  '…' 버튼을 클릭하고 **인스턴스 삭제**를 선택하여 인스턴스를 삭제합니다.

> [주의]
> * 웹 서비스가 웹 방화벽을 경유하여 서비스 되고 있을 때 인스턴스를 삭제할 경우 서비스 장애가 발생할 수 있습니다.
> * 웹 방화벽 인스턴스 삭제 시 관련 서비스를 유의하여 삭제하시기 바랍니다.

<br>

## 웹 방화벽 인스턴스 생성 세부 절차
웹 방화벽 인스턴스 생성 시 참고할 수 있는 세부 절차를 가이드합니다.
<br>

### 1. 이미지
![webfirewall_gov_kr_console-guide-self-piolink-gov_05_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_05_241122.png)

1. 공용 이미지 목록에서 "PLOS WAF" 이미지를 선택합니다.

<br>

### 2. 인스턴스 정보
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_06_241122.png" width="1200" />

1. 가용성 영역(Availablility Zone): 웹 방화벽 인스턴스가 위치할 가용성 영역을 설정합니다. 가용성 영역에 대한 자세한 설명은 [인스턴스 개요의 가용성 영역](https://docs.nhncloud.com/ko/Compute/Instance/ko/overview/#availability-zone)을 참고합니다.
2. 인스턴스 이름: 웹 방화벽 인스턴스의 이름을 설정합니다.
3. 인스턴스 타입: 가상 하드웨어의 성능을 설정합니다. 아래 웹 방화벽의 권장사양 표를 참고하여 인스턴스 타입을 설정합니다.
4. 인스턴스 수: 생성할 인스턴스의 수를 설정합니다.
5. 키 페어: 인스턴스의 SSH 접속 수단으로 사용되는 키 쌍입니다. 기존 키페어를 사용하거나, 새로운 키페어를 생성하여 사용합니다.

| Throughput (Mbps) | 인스턴스 타입 | vCPU | Memory(GB) |
| :-------: | :-----: | :---: | :---: |
| 100 | m2.c2m4 | 2 | 4 | 
| 300 | r2.c2m8 | 2 | 8 | 
| 500 | m2.c4m8 | 4 | 8 |
| 1,000 | m2.c8m16 | 8 | 16 |

<p align="center">[표1. 웹 방화벽(WEBFRONT-KS) 권장 인스턴스 타입]</p>

### 3. 루트 블록 스토리지
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_07_241122.png" width="1100" />

1. 블록 스토리지 타입: HDD, SSD, Encrypted HDD, Encrypted SSD를 선택할 수 있습니다. Encrypted HDD/SSD에 대한 정보는 [암호화 블록 스토리지](https://docs.nhncloud.com/ko/Storage/Block%20Storage/ko/console-guide/#_2)를 참고합니다.
2. 블록 스토리지 크기(GB): 루트 블록 스토리지의 용량을 설정합니다.

### 4. 네트워크 설정
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/gov/kr/webfirewall_gov_kr_console-guide-self-piolink-gov_08_241122.png" width="1200" />

1. 네트워크 인터페이스 설정
    - 네트워크 인터페이스 생성: 네트워크 서브넷을 선택하면 자동으로 인터페이스가 생성되는 방식입니다.
    - 기존 네트워크 인터페이스 지정: 기존에 생성되어 있는 인터페이스를 설정하는 방식입니다. 아래의 "2. 네트워크"와 "3. 플로팅 IP" 설정은 기존 인터페이스의 설정을 따르기에 생략됩니다.
2. 네트워크: VPC에 정의된 서브넷 중에서 인스턴스에 연결할 서브넷을 선택합니다.
3. 플로팅 IP: 인스턴스 생성 후 플로팅 IP 사용 여부를 지정합니다. 이때 웹 방화벽 인스턴스가 속한 VPC가 인터넷 게이트웨이와 연결되어 있어야 합니다. 지금 설정하지 않더라도 "Instance > 플로팅 IP 관리", "Network Interface > 플로팅 IP 관리" 등에서 설정할 수 있습니다.
4. 보안그룹: 웹 방화벽 인스턴스에 적용할 보안그룹을 선택합니다. 보안 그룹은 아래 설정 예시를 참고합니다.

<br>

| 방향 | IP 프로토콜 | 포트 | 원격(CIDR) | 설명 |
| :-------: | :-----: | :---: | :---: | :--- |
| 수신 | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | WAF 웹 서비스 포트 |
| 수신 | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | WAF 웹 서비스 포트 |
| 수신 | TCP | 8443 | 관리자 IP | 웹 방화벽 관리용 포트(관리자 IP만 허용) |
| 수신 | TCP | 22 (SSH) | 관리자 IP | 웹 방화벽 터미널 포트(관리자 IP만 허용) |
| 송신 | ICMP | - | 0.0.0.0/0 | 보호 대상 웹 서버 헬스체크 |
| *송신 | 임의 | - | 0.0.0.0/0 | WAF의 외부 라이선스, 시그니처 업데이트 등 통신 용도 |

<p align="center">[표2. 보안 그룹 설정 예시]</p>

> [참고]
> * 웹 방화벽의 기본 상태 확인(health check) 방식은 ICMP로 설정되어 있으며, 웹 서버와 상태 확인(health check) 실패 시 웹 서비스가 동작하지 않습니다.
> * 위 [표2. 보안그룹 설정 예시]의 WAF의 *송신 규칙은 예시와 같이 모든 외부 통신을 허용하는 것을 권장합니다.

## 웹 방화벽 초기 설정

* 웹 방화벽 초기 설정 가이드를 참고하여 초기 설정을 진행하며, 주요 내용은 다음과 같습니다.
	* 애플리케이션을 설정합니다.
	* 부하 분산 메뉴에서 실제 보호 받을 서버를 설정합니다.
	* 프락시로 동작하게 하려면 Source NAT 기능을 활성화합니다.
	* 웹 방화벽 IP로 접근하는 것을 테스트하여 웹 서비스 정상 여부를 확인합니다.
	* 설정한 내용을 저장하고 백업합니다.

[WEBFRONT-KS 초기 설정 가이드](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS_%EC%B4%88%EA%B8%B0%20%EC%84%A4%EC%A0%95%20%EA%B0%80%EC%9D%B4%EB%93%9C.pdf)

* 초기 설정 완료 후, 보호 대상 도메인 트래픽이 웹 방화벽으로 경유하도록 웹 방화벽 플로팅 IP로 DNS를 변경해야 합니다.
* 제조사에서 제공하는 릴리스 노트를 참고하여 웹 방화벽 PLOS 버전을 최신으로 업데이트해야 합니다.
	* 릴리스 노트 다운로드 방법: 웹 방화벽 접속 > SYSTEM > 일반 설정 > PLOS 관리 > 다운로드 PLOS > 다운로드

## 웹 방화벽 운영

웹 방화벽 구성 설명서를 참고하여 장비를 운영하며, 주요 내용은 다음과 같습니다.

* 사용할 보안 정책을 활성화합니다.
* 학습 기능을 활용하여 예외 처리 등 정책 최적화를 진행합니다.
* 보안 로그를 모니터링합니다.

[WEBFRONT-KS 애플리케이션 구성 설명서](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS-%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98%20%EA%B5%AC%EC%84%B1%20%EC%84%A4%EB%AA%85%EC%84%9C.pdf) <br>
[WEBFRONT-KS 시스템 구성 설명서](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS-%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B5%AC%EC%84%B1%20%EC%84%A4%EB%AA%85%EC%84%9C.pdf) <BR>
※ Self 서비스에서는 사용 가이드만 제공되며, Managed 서비스 이용 시 운영 대행 및 24시간 보안관제 서비스를 제공합니다.
