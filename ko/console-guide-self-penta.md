## Security > WEB Firewall > 콘솔 사용 가이드 > Self > 펜타시큐리티(WAPPLES SA)

WEB Firewall Self 서비스에서는 웹 서버를 보호할 수 있도록 웹 방화벽 인스턴스를 생성하고 운영할 수 있는 가이드를 제공합니다.
여기에서는 WEB Firewall Self 서비스 사용 방법을 소개합니다.

WEB Firewall 서비스를 이용하려면 **NHN Cloud Console**에 로그인하고, 서비스 목록에서 **Security > WEB Firewall**을 클릭하여 서비스를 활성화합니다.

![
webfirewall_public_kr_console-guide-self-penta_01_241113.png](https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_01_241113.png)
<br><br>

## 서비스 이용 및 해지
### 웹 방화벽 생성

![
webfirewall_public_kr_console-guide-self-penta_02_241113.png](https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_02_241113.png)
![
webfirewall_public_kr_console-guide-self-penta_03_241113.png](https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_03_241113.png)

1. **WEB Firewall** 콘솔의 **Self 이용 신청**에서 **바로 가기**를 클릭해 "Compute > Instance" 페이지로 이동합니다.
2. **+ 인스턴스 생성**을 클릭하고 이미지 목록에서 PENTA WAF를 선택한 후 인스턴스 정보를 입력합니다. 자세한 방법은 아래 **웹 방화벽 인스턴스 생성 세부 절차**를 참고하십시오.

> [참고]
> * 인스턴스가 생성되는 즉시 이용 요금이 부과됩니다.
> * WAPPLE SA(PENTA WAF)의 최소 권장 인스턴스 사양은 2vCore / Memory 4GB으로 권장 미만 사양의 인스턴스 사용 시 정상적으로 동작하지 않을 수 있습니다. **따라서 반드시 권장 사양 이상의 인스턴스 타입을 사용**해야 합니다.

<br>

### 웹 방화벽 해지

![
webfirewall_public_kr_console-guide-self-penta_04_241113.png](https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_04_241113.png)

1. 인스턴스 목록에서 웹 방화벽 인스턴스를 선택합니다.
2.  '…' 버튼을 클릭하여 **인스턴스 삭제**를 클릭하여 인스턴스를 삭제합니다.

> [주의]
> * 웹 서비스가 웹 방화벽을 경유하여 서비스 되고 있을 때 인스턴스를 삭제할 경우 서비스 장애가 발생할 수 있습니다.
> * 웹 방화벽 인스턴스 삭제 시 관련 서비스를 유의하여 삭제하시기 바랍니다.
<br>

## 웹 방화벽 인스턴스 생성 세부 절차
웹 방화벽 인스턴스 생성 시 참고할 수 있는 세부 절차를 가이드합니다.
<br>

### 1. 이미지
 ![
webfirewall_public_kr_console-guide-self-penta_05_241113.png](https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_05_241113.png)

1. 공용 이미지 목록에서 "PENTA WAF" 이미지를 선택합니다.

<br>

### 2. 인스턴스 정보
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_06_241113.png" width="1200" />


1. 가용성 영역(Availablility Zone): 웹 방화벽 인스턴스가 위치할 가용성 영역을 설정합니다. 가용성 영역에 대한 자세한 설명은 [인스턴스 개요의 가용성 영역](https://docs.nhncloud.com/ko/Compute/Instance/ko/overview/#availability-zone)을 참고합니다.
2. 인스턴스 이름: 웹 방화벽 인스턴스의 이름을 설정합니다.
3. 인스턴스 타입: 가상 하드웨어의 성능을 설정합니다. 아래 웹 방화벽의 권장사양 표를 참고하여 인스턴스 타입을 설정합니다.
4. 인스턴스 수: 생성할 인스턴스의 수를 설정합니다.
5. 키 페어: 인스턴스의 SSH 접속 수단으로 사용되는 키 쌍입니다. 기존 키페어를 사용하거나, 새로운 키페어를 생성하여 사용합니다.

> [참고]
> ※ WAPPLE SA(PENTA WAF)의 최소 권장 인스턴스 사양은 2vCore / Memory 4GB으로 **권장 사양 미만의 인스턴스 사용 시 정상적으로 동작하지 않을 수 있습니다.**
> **따라서 반드시 권장 사양 이상의 인스턴스 타입을 사용해야 합니다.**

| Throughput (Mbps) | 인스턴스 타입 | vCPU | Memory(GB) |
| :-------: | :-----: | :---: | :---: |
| 100 | m2.c2m4 | 2 | 4 | 
| 300 | m2.c4m8 | 4 | 8 | 
| 700 | m2.c8m16 | 8 | 16 |
| 1,500 | m2.c16m32 | 16 | 32 |

<p align="center">[표1. 웹 방화벽(WAPPLES SA) 권장 인스턴스 타입]</p>

### 3. 루트 블록 스토리지
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_07_241113.png" width="1100" />

1. 블록 스토리지 타입: HDD, SSD, Encrypted HDD, Encrypted SSD를 선택할 수 있습니다. Encrypted HDD/SSD에 대한 정보는 [암호화 블록 스토리지](https://docs.nhncloud.com/ko/Storage/Block%20Storage/ko/console-guide/#_2)를 참고합니다.
2. 블록 스토리지 크기(GB): 루트 블록 스토리지의 용량을 설정합니다. PENTA WAF의 최소 용량은 200GB입니다.

### 4. 네트워크 설정
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_08_241113.png" width="1200" />

1. 네트워크 인터페이스 설정
    - 네트워크 인터페이스 생성: 네트워크 서브넷을 선택하면 자동으로 인터페이스가 생성되는 방식입니다.
    - 기존 네트워크 인터페이스 지정: 기존에 생성되어 있는 인터페이스를 설정하는 방식입니다. 아래의 "2. 네트워크"와 "3. 플로팅 IP" 설정은 기존 인터페이스의 설정을 따르기에 생략됩니다.
2. 네트워크: VPC에 정의된 서브넷 중에서 인스턴스에 연결할 서브넷을 선택합니다. **PENTA WAF는 추가 인터페이스 설정을 지원하지 않습니다.**
3. 플로팅 IP: 인스턴스 생성 후 플로팅 IP 사용 여부를 지정합니다. 이때 웹 방화벽 인스턴스가 속한 VPC가 인터넷 게이트웨이와 연결되어 있어야 합니다. 지금 설정하지 않더라도 "Instance > 플로팅 IP 관리", "Network Interface > 플로팅 IP 관리" 등에서 설정할 수 있습니다.
4. 보안그룹: 웹 방화벽 인스턴스에 적용할 보안그룹을 선택합니다. 보안 그룹은 아래 설정 예시를 참고합니다.

<br>

| 방향 | IP 프로토콜 | 포트 | 원격(CIDR) | 설명 |
| :-------: | :-----: | :---: | :---: | :--- |
| 수신 | TCP | 80 (HTTP) | 0.0.0.0/0 | WAF 웹 서비스 포트 |
| 수신 | TCP | 443 (HTTPS) | 0.0.0.0/0 | WAF 웹 서비스 포트<br><span style="color:#e11d21;">*아래 주의사항 참고</span> |
| 수신 | TCP | 5001 | 관리자 IP | WAF 관리 도구(UI) 포트(관리자 IP만 허용) |
| 수신 | TCP | 22 (SSH) | 관리자 IP | WAF SSH 터미널 포트(관리자 IP만 허용) |
| 수신 | TCP | 5000 | WAF의 상단 LB의 IP | 상단 LB의 헬스체크(health check) 포트 |
| 수신 | TCP | 5984 | WAF의 보안그룹 혹은 WAF IP 대역대 | WAF 간 정책 동기화<br><span style="color:#e11d21;">*이중화 시 필요</span> | 
| *송신 | 임의 | - | 0.0.0.0/0 | WAF의 외부 라이선스, 시그니처 업데이트 등 통신 용도<br>(개별 설정 필요할 경우 [표3. WAF 송신 목록] 참고) |

<p align="center"> [표2. 보안 그룹 설정 예시] </p>


<br />

> [참고]
> * 이중화(설정 동기화 기능 사용 시) 또는 Auto Scaling 사용 시 웹 방화벽 간 5984 포트 허용이 추가로 필요합니다.

<br>

위 [표2. 보안그룹 설정 예시]의 WAF의 *송신 규칙은 예시와 같이 모든 외부 통신을 허용하는 것을 권장합니다. 송신 규칙을 개별로 허용이 필요한 경우 아래 [표3. WAF 송신 목록]을 참고합니다.

<br>

| 방향 | IP 프로토콜 | 포트 | 원격(CIDR) | 설명 |
| :-------: | :-----: | :---: | :---: | :--- |
| 송신 | TCP | 443 (HTTPS) | 218.145.29.166/32 | WAF 라이선스 업데이트 서버 |
| 송신 | TCP | 443 (HTTPS) | 218.145.29.101/32 | WAF 라이선스 업데이트 서버 |
| 송신 | TCP | 5001 | 218.145.29.168/32 | WAF 보안룰(custom rule) 업데이트 서버 |
| 송신 | UDP | 123 | 218.145.29.166/32 | Penta 시간 서버 |
| 송신 | UDP | 123 | 218.145.29.163/32 | Penta 시간 서버 |
| *송신 | TCP | 5984 | WAF의 보안그룹 혹은 WAF IP 대역대 | WAF 간 정책 동기화<br><span style="color:#e11d21;">*이중화 시 필요</span> |

<p align="center">[표3. WAF 송신 목록]</p>

<br>

> [주의]
> * 웹 방화벽에서 보호대상 서버 TCP 443(HTTPS) 정책을 설정 하지 않았을 경우, 웹 방화벽으로 TCP 443(HTTPS) 접속 시 관리 도구(UI)에 접근 가능합니다. 따라서 위 보안그룹 ACL 중 "수신 TCP 443" 규칙은 **웹 방화벽의 보호대상 서버 TCP 443 설정 후 보안그룹에서 허용**합니다.

## 웹 방화벽 초기 설정

### WAF 최초 구동 후 초기 설정 하기
1. 브라우저(크롬 권장)에서 웹방화벽 웹 관리 도구(UI) 접속
	* https://WAF IP:5001
	* 처음 로그인 접속 정보 : ct@pentasecurity.com 로 문의
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_01_241113.png" width="1000" />
2. 환경설정 > 시스템 > 시간동기화 설정하기
   	* 시간 서버 각각 설정하기
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_02_241113.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_03_241113.png" width="1000" />
3. 네트워크 설정 > 프록시IP 설정하기
	* NHN console 에서 확인한 네트워크 정보 입력(WAF IP, gateway, netmask)
 		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_04_241113.png" width="1000" />
   		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_05_241113.png" width="1000" />
   		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_06_241113.png" width="1000" />
4. WAF 보호 대상 설정하기
	* 네트워크 설정 > 보호 대상 서버 > 웹 서버 추가
 					<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_07_241113.png" width="1000" /> 
	* 보호 대상 서버 등록하기
 		* 단일: 웹 호스트명에 따라 분기할 필요 없이 설정한 보호대상 웹 서버(혹은 하단 LB 등)의 IP 혹은 포트로 연결할 경우 사용합니다. ( 1:1 매칭)
   		* 다중: 웹 호스트명에 따라 보호대상 웹 서버(혹은 하단 LB 등)의 IP 혹은 포트로 분기하여 연결할 경우 사용합니다. (1:N 매칭)

		* 단일 설정
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_08_241113.png" width="1000" />
		* 다중 설정
  			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_09_241113.png" width="1000" />
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_10_241113.png" width="1000" />
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_11_241113.png" width="1000" />
> [참고]
> * WAF가 HTTPS 서비스를 제공해야 할 경우 [네트워크 설정 > SSL 프로파일 > 인증서 추가]를 진행한 후 각 보호대상 웹 서버 추가 시 SSL 설정을 진행할 수 있습니다.
> * 자세한 사항은 아래 "웹 방화벽 운영" 항목에 기재된 위치의 사용자 매뉴얼을 참고합니다.

5. 보호 정책 설정하기
	* 보안 설정 > 정책 설정 > 신규 정책 추가(기반 정책: '탐지만 하고 차단 안 함' 선택)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_12_241113.png" width="1000" />
  		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_13_241113.png" width="800" />
	* 보안 설정 > 정책 설정 > 신규 웹사이트 추가(신규 정책에 적용)
  		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_14_241113.png" width="800" />
    		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_15_241113.png" width="1000" />
6. X-Forwarded-For IP 설정하기
	* 보안 설정 > 정책 부가 설정 > X-Forwarded-For 설정(Block & Detect 모두 설정)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_16_241113.png" width="1000" />
<br>

> [WAF 적용 시 참고 사항]
> * NHN Cloud 관리형 서비스 공급자(managed service provider, MSP)를 통해 고객 인프라 환경에 WAF 서비스가 적용되도록 네트워크 routing을 변경 구성합니다.
> * 고객 인프라 구성에 따라 WAF 플로팅 IP로 DNS 변경이 필요하거나, WAF 이중화 구성 시 상단 로드 밸런서 IP로 DNS 변경이 필요할 수 있습니다.

<br>

## 웹 방화벽 운영

* 웹 방화벽의 전반적인 사용자 매뉴얼 및 이용 방법은 웹 방화벽의 관리 도구(UI)에서 제공합니다.
* 아래 화면의 사용자 매뉴얼 위치를 참고하여 웹 방화벽 운영 전반의 이용 방법을 참고하십시오.
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/kr/webfirewall_public_kr_console-guide-self-penta_WAF_17_241113.png" width="1000" />

> [참고]
> * Self 서비스에서는 사용 가이드만 제공되며, Managed 서비스 이용 시 운영 대행 및 24시간 보안관제 서비스를 제공합니다.
