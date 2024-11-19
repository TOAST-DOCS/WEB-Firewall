## Security > WEB Firewall > コンソール使用ガイド > Self > ペンタセキュリティ(WAPPLES SA)

WEB Firewall Selfサービスでは、Webサーバーを保護できるようにWebファイアウォールインスタンスを作成し、運営できるガイドを提供します。
ここではWEB Firewall Selfサービスの使い方を紹介します。

WEB Firewallサービスを利用するには、**NHN Cloud Console**にログインし、サービス一覧から**Security > WEB Firewall**をクリックしてサービスを有効化します。

![webfirewall_public_ja_console-guide-self-penta_01_241119.png](https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_01_241119.png)
<br><br>

## サービス利用および解約

![webfirewall_public_ja_console-guide-self-penta_02_241119.png](https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_02_241119.png)
![webfirewall_public_ja_console-guide-self-penta_03_241119.png](https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_03_241119.png)

1. **WEB Firewall**コンソールの**Self利用申請**から**ショートカット**をクリックし、**「Compute > Instance」** ページに移動します。
2. **「+ インスタンス作成」** をクリックし、イメージリストからPENTA WAFを選択した後、インスタンス情報を入力します。詳細な手順は**ウェブファイアウォールインスタンス作成の詳細手順**を参照してください。

> [参考]
> - インスタンスが作成されると、すぐに利用料金が発生します。
> - WAPPLE SA(PENTA WAF)の最小推奨インスタンス仕様は2vCore / Memory 4GBであり、推奨仕様未満のインスタンスを使用すると正常に動作しない可能性があります。**そのため、必ず推奨仕様以上のインスタンスタイプを使用する**必要があります。

<br>

### Webファイアウォール作成

![webfirewall_public_ja_console-guide-self-penta_04_241119.png](https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_04_241119.png)

1. インスタンスリストからWAFインスタンスを選択します。
2. 「…」ボタンをクリックし、**「インスタンスの削除」** を選択してインスタンスを削除します。

> [注意]
> - ウェブサービスがWAFを経由して提供されている場合、インスタンスを削除するとサービス障害が発生する可能性があります。
> - WAFインスタンスを削除する際は、関連するサービスに注意して削除してください。

<br>

## WAFインスタンス作成の詳細手順
WAFインスタンスを作成する際の詳細な手順をガイドします。
<br>

### 1. イメージ
![webfirewall_public_ja_console-guide-self-penta_05_241119.png](https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_05_241119.png)

1. パブリックイメージリストから「PENTA WAF」イメージを選択します。

<br>

### 2. インスタンス情報
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_06_241119.png" width="1200" />


1. アベイラビリティゾーン: WAFインスタンスを配置する可用性領域を設定します。可用性領域の詳細については[「インスタンス概要のインスタンスタイプ」](https://docs.nhncloud.com/ja/Compute/Instance/ja/overview/#availability-zone)を参照してください。
2. インスタンス名: WAFインスタンスの名前を設定します。
3. インスタンスタイプ: 仮想ハードウェアの性能を設定します。以下の **[表1. WAF(WAPPLES SA)推奨インスタンスタイプ]** を参考にインスタンスタイプを設定します。
4. インスタンス数: 作成するインスタンスの数を設定します。
5. キーペア: インスタンスへのSSH接続手段として使用されるキーペアです。既存のキーペアを使用するか、新しいキーペアを作成して使用します。

> [参考]<br>
> ※ WAPPLE SA(PENTA WAF)の最小推奨インスタンス仕様は2vCore / Memory 4GBであり、推奨仕様未満のインスタンスを使用すると正常に動作しない可能性があります
> **そのため、必ず推奨仕様以上のインスタンスタイプを使用する必要があります。**

| Throughput (Mbps) | インスタンスタイプ | vCPU | Memory(GB) |
| :-------: | :-----: | :---: | :---: |
| 100 | m2.c2m4 | 2 | 4 | 
| 300 | m2.c4m8 | 4 | 8 | 
| 700 | m2.c8m16 | 8 | 16 |
| 1,500 | m2.c16m32 | 16 | 32 |

<p align="center">[表1. WAF(WAPPLES SA)推奨インスタンスタイプ]</p>

### 3. ルートブロックストレージ
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_07_241119.png" width="1200" />

1. ブロックストレージタイプ: HDD、SSD、Encrypted HDD、Encrypted SSDから選択できます。Encrypted HDD/SSDについては[「暗号化ブロックストレージ」](https://docs.nhncloud.com/ja/Storage/Block%20Storage/ja/console-guide/#_2)を参照してください。
2. ブロックストレージサイズ(GB): ルートブロックストレージの容量を設定します。PENTA WAFの最小容量は200GBです。

### 4. ネットワーク設定
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_08_241119.png" width="1200" />

1. ネットワークインターフェース設定
   - ネットワークインターフェース作成: 選択したサブネットに自動的にインターフェースが作成される方式です。
   - 既存のネットワークインターフェース指定: 既に作成されているインターフェースを設定する方式です。 以下の「2. ネットワーク」と「3. Floating IP」設定は、既存のインターフェースの設定に従うため、省略されます。
2. ネットワーク: VPCに定義されたサブネットの中からインスタンスに接続するサブネットを選択します。PENTA WAFは追加インターフェース設定をサポートしません。
3. Floating IP: インスタンス作成後に「Floating IP」使用の有無を指定します。この際、WAFインスタンスが所属するVPCがインターネットゲートウェイと接続されている必要があります。現在設定しなくても「Instance > Floating IP管理」、「Network Interface > Floating IP管理」などで設定できます。
4. セキュリティグループ: WAFインスタンスに適用するセキュリティグループを選択します。セキュリティグループは以下の **[表2. セキュリティグループ設定例]** を参照してください。

<br>

| 方向 | IPプロトコル | ポート | リモート(CIDR) | 説明 |
| :-------: | :-----: | :---: | :---: | :--- |
| 受信 | TCP | 80 (HTTP) | 0.0.0.0/0 | WAF 웹 서비스 포트 |
| 受信 | TCP | 443 (HTTPS) | 0.0.0.0/0 | WAF 웹 서비스 포트<br><span style="color:#e11d21;">*아래 주의사항 참고</span> |
| 受信 | TCP | 5001 | 관리자 IP | WAF 관리 도구(UI) 포트(관리자 IP만 허용) |
| 受信 | TCP | 22 (SSH) | 관리자 IP | WAF SSH 터미널 포트(관리자 IP만 허용) |
| 受信 | TCP | 5000 | WAF의 상단 LB의 IP | 상단 LB의 헬스체크(health check) 포트 |
| 受信 | TCP | 5984 | WAF의 보안그룹 혹은 WAF IP 대역대 | WAF 간 정책 동기화<br><span style="color:#e11d21;">*HA 구성 시 필요</span> | 
| *送信 | 任意 | - | 0.0.0.0/0 | WAF의 외부 라이선스, 시그니처 업데이트 등 통신 용도<br>(개별 설정 필요할 경우 [표3. WAF 송신 목록] 참고) |

<p align="center"> [表2. セキュリティグループ設定例] </p>
