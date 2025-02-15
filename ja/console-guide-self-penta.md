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
2. **「+ インスタンス作成」** をクリックし、イメージリストからPENTA WAFを選択した後、インスタンス情報を入力します。詳細な手順は**WAFインスタンス作成の詳細手順**を参照してください。

> [参考]
> * インスタンスが作成されると、すぐに利用料金が発生します。
> * WAPPLE SA(PENTA WAF)の最小推奨インスタンス仕様は2vCore / Memory 4GBであり、推奨仕様未満のインスタンスを使用すると正常に動作しない可能性があります。**そのため、必ず推奨仕様以上のインスタンスタイプを使用する**必要があります。

<br>

### Webファイアウォール作成

![webfirewall_public_ja_console-guide-self-penta_04_241119.png](https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_04_241119.png)

1. インスタンスリストからWAFインスタンスを選択します。
2. 「…」ボタンをクリックし、**「インスタンスの削除」** を選択してインスタンスを削除します。

> [注意]
> * ウェブサービスがWAFを経由して提供されている場合、インスタンスを削除するとサービス障害が発生する可能性があります。
> * WAFインスタンスを削除する際は、関連するサービスに注意して削除してください。

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

> [参考]
> 
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
   * ネットワークインターフェース作成: 選択したサブネットに自動的にインターフェースが作成される方式です。
   * 既存のネットワークインターフェース指定: 既に作成されているインターフェースを設定する方式です。 以下の「2. ネットワーク」と「3. Floating IP」設定は、既存のインターフェースの設定に従うため、省略されます。
2. ネットワーク: VPCに定義されたサブネットの中からインスタンスに接続するサブネットを選択します。PENTA WAFは追加インターフェース設定をサポートしません。
3. Floating IP: インスタンス作成後に「Floating IP」使用の有無を指定します。この際、WAFインスタンスが所属するVPCがインターネットゲートウェイと接続されている必要があります。現在設定しなくても「Instance > Floating IP管理」、「Network Interface > Floating IP管理」などで設定できます。
4. セキュリティグループ: WAFインスタンスに適用するセキュリティグループを選択します。セキュリティグループは以下の **[表2. セキュリティグループ設定例]** を参照してください。

<br>

| 方向 | IPプロトコル | ポート | リモート(CIDR) | 説明 |
| :-------: | :-----: | :---: | :---: | :--- |
| 受信 | TCP | 80 (HTTP) | 0.0.0.0/0 | WAFウェブサービス |
| 受信 | TCP | 443 (HTTPS) | 0.0.0.0/0 | WAFウェブサービスポート<br><span style="color:#e11d21;">*下記[注意]参考</span> |
| 受信 | TCP | 5001 | 管理者IP | WAF 管理コンソール(UI)ポート(管理者IPのみ許可) |
| 受信 | TCP | 22 (SSH) | 管理者IP | WAF SSH ターミナルポート(管理者IPのみ許可) |
| 受信 | TCP | 5000 | WAF前端LBのIP | 前端LBのヘルスチェック(health check)ポート |
| 受信 | TCP | 5984 | WAFのセキュリティグループまたはWAFのIP範囲 | WAF間のポリシー同期<br><span style="color:#e11d21;">*HA構成時に必要</span> | 
| *送信 | 任意 | - | 0.0.0.0/0 | WAFの外部ライセンス、シグネチャ更新などの通信用途<br>(個別設定が必要な場合[表3. WAF送信リスト])参考 |

<p align="center"> [表2. セキュリティグループ設定例] </p>

<br />

> [参考]
> * HA構成で設定同期機能を使用する場合、WAF間で5984ポートの許可が必要です。

<br>

上記[表2. セキュリティグループ設定例]のWAFの*送信ルールは、例のようにすべての外部通信を許可することを推奨します。送信ルールを個別に許可する必要がある場合は、下記[表3. WAF送信リスト]を参照してください。

<br>

| 方向 | IPプロトコル | ポート | リモート(CIDR) | 説明 |
| :-------: | :-----: | :---: | :---: | :--- |
| 送信 | TCP | 443 (HTTPS) | 218.145.29.166/32 | WAFライセンス更新サーバー |
| 送信 | TCP | 443 (HTTPS) | 218.145.29.101/32 | WAFライセンス更新サーバー |
| 送信 | TCP | 5001 | 218.145.29.168/32 | WAFセキュリティルール(custom rule)更新サーバー |
| 送信 | UDP | 123 | 218.145.29.166/32 | ペンタセキュリティの時間サーバー (変更可能) |
| 送信 | UDP | 123 | 218.145.29.163/32 | ペンタセキュリティの時間サーバー (変更可能) |
| 送信 | UDP,TCP | 53 | 164.124.101.2/32 | DNSサーバー - LG U+ (変更可能) |
| 送信 | UDP,TCP | 53 | 8.8.8.8/32 | DNSサーバー - Google (変更可能) |
| *送信 | TCP | 5984 | WAFのセキュリティグループまたはWAFのIP範囲 | WAF間のポリシー同期<br><span style="color:#e11d21;">*HA構成時に必要</span> |

<p align="center">[表3. WAF送信リスト]</p>

<br>

> [注意]
> * WAFで保護対象サーバー「TCP 443(HTTPS)」ポリシーを設定しない場合、WAFに「TCP 443(HTTPS)」で接続し、管理コンソール(UI)にアクセスできます。したがって、上記のセキュリティグループACLの「受信TCP 443」ルールは、WAFの保護対象サーバーに設定後、セキュリティグループで許可する必要があります。

## WAFの初期設定

### WAF 最初の駆動後、初期設定をする
1. ブラウザ(Chrome推奨)を使用して、WAFの管理コンソール(UI)にアクセスします。
	* https://WAF IP:5001
	* 初回ログインの接続情報については、ct@pentasecurity.comまでお問い合わせください。
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_01_241119.png" width="1000" />
<br>

2. 環境設定 > システム > 時刻同期を設定する
	* 各時刻サーバーを個別に設定する
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_02_241119.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_03_241119.png" width="1000" />
<br>

3. ネットワーク設定 > プロキシIPを設定する
	* NHN Cloud Consoleで確認したネットワーク情報を入力する(WAF IP、ネットマスク、ゲートウェイ)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_04_241119.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_05_241119.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_06_241119.png" width="1000" />
<br>

4. WAFの保護対象を設定する
	* ネットワーク設定 > 保護対象サーバー > ウェブサーバー追加
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_07_241119.png" width="1000" /><br><br>
	* 保護対象サーバーを登録する
		* シングル: ウェブホスト名で分岐する必要なく、設定した保護対象ウェブサーバー(またはWEBのLBなど)のIPまたはポートに接続する場合に使用します。(1:1マッチング)
		* マルチ: ウェブホスト名に基づいて、保護対象ウェブサーバー(またはWEBのLBなど)のIPまたはポートに分岐して接続する場合に使用します。(1:Nマッチング) <br><br>
		* シングル設定
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_08_241119.png" width="1000" /><br><br>
		* マルチ設定
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_09_241119.png" width="1000" />
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_10_241119.png" width="1000" /><br><br>
	* 最終適用
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_11_241119.png" width="1000" /><br><br>

>[参考]
> * WAFがHTTPSサービスを提供する必要がある場合、[ネットワーク設定 > SSLプロファイル > 証明書追加]を実行した後、各保護対象ウェブサーバーを追加する際にSSL設定を行うことができます。
> * 詳細については、以下の「WAF運用」項目に記載されている場所のユーザーマニュアルを参照してください。

<br>

5. 保護ポリシーを設定する
	* セキュリティ設定 > ポリシー設定 > 新規ポリシー追加(基盤ポリシ: 「検知のみ行い遮断はしない」選択)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_12_241119.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_13_241119.png" width="800" /><br><br>
	* セキュリティ設定 > ポリシー設定 > 新規ウェブサイト追加(新規ポリシー適用)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_14_241119.png" width="800" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_15_241119.png" width="1000" />

<br>

6. X-Forwarded-For IP 設定する
	* セキュリティ設定 > ポリシー付加設定 > X-Forwarded-For設定 (Block、Detectすべて設定)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_16_241119.png" width="1000" /><br><br>

> [WAFに適用する際の参考]
> * 顧客のインフラ環境にWAFサービスが適用されるように、ネットワーク経路の変更が必要です。
> * 顧客インフラの構成に応じて、WAFのFloating IPへのDNS変更が必要な場合や、WAFのHA構成時に前段ロードバランサーIPへのDNS変更が必要な場合があります。

<br>

## WAF運用
* WAFの全般的なユーザーマニュアルおよび利用方法は、WAFの管理コンソール(UI)で提供されます。
* 下記の画面のユーザーマニュアルの位置を参考にして、WAF運用全般の利用方法をご確認ください。
	<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/ja/webfirewall_public_ja_console-guide-self-penta_WAF_17_241119.png" width="1000" /><br><br>

> [参考]
> * Selfサービスでは使用ガイドのみが提供され、Managedサービスを利用する際には運用代行および24時間セキュリティ監視サービスが提供されます。
