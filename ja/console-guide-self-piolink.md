## Security > WEB Firewall > コンソール使用ガイド > Self > パイオリンク(WEBFRONT-KS)

WEB Firewall Selfサービスでは、Webサーバーを保護できるようにWebファイアウォールインスタンスを作成し、運営できるガイドを提供します。
ここではWEB Firewall Selfサービスの使い方を紹介します。

WEB Firewallサービスを利用するには、**NHN Cloud Console**にログインし、サービス一覧から**Security > WEB Firewall**をクリックしてサービスを有効化します。

![webfirewall_public_ja_console-guide-self-piolink_01_241125.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_01_241125.png)
<br><br>

## サービス利用および解約

![webfirewall_public_ja_console-guide-self-piolink_02_241125.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_02_241125.png)
![webfirewall_public_ja_console-guide-self-piolink_03_241125.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_03_241125.png)

1. **WEB Firewall**コンソールの**Self利用申請**から**ショートカット**をクリックし、**「Compute > Instance」** ページに移動します。
2. **「+ インスタンス作成」** をクリックし、イメージリストからPLOS WAFを選択した後、インスタンス情報を入力します。詳細な手順は**WAFインスタンス作成の詳細手順**を参照してください。

> [参考]
> * インスタンスが作成されると、すぐに利用料金が発生します。

<br>

### Webファイアウォール作成

![webfirewall_public_ja_console-guide-self-piolink_04_241125.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_04_241125.png)

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
![webfirewall_public_ja_console-guide-self-piolink_05_241125.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_05_241125.png)

1. パブリックイメージリストから「PLOS WAF」イメージを選択します。

<br>

### 2. インスタンス情報
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_06_241125.png" width="1200" />

1. アベイラビリティゾーン: WAFインスタンスを配置する可用性領域を設定します。可用性領域の詳細については[「インスタンス概要のインスタンスタイプ」](https://docs.nhncloud.com/ja/Compute/Instance/ja/overview/#availability-zone)を参照してください。
2. インスタンス名: WAFインスタンスの名前を設定します。
3. インスタンスタイプ: 仮想ハードウェアの性能を設定します。以下の **[表1. WAF(WEBFRONT-KS)推奨インスタンスタイプ]** を参考にインスタンスタイプを設定します。
4. インスタンス数: 作成するインスタンスの数を設定します。
5. キーペア: インスタンスへのSSH接続手段として使用されるキーペアです。既存のキーペアを使用するか、新しいキーペアを作成して使用します。

| Throughput (Mbps) | インスタンスタイプ | vCPU | Memory(GB) |
| :-------: | :-----: | :---: | :---: |
| 100 | m2.c2m4 | 2 | 4 | 
| 300 | r2.c2m8 | 2 | 8 | 
| 500 | m2.c4m8 | 4 | 8 |
| 1,000 | m2.c8m16 | 8 | 16 |

<p align="center">[表1. WAF(WEBFRONT-KS)推奨インスタンスタイプ]</p>

### 3. ルートブロックストレージ
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_07_241125.png" width="1200" />

1. ブロックストレージタイプ: HDD、SSD、Encrypted HDD、Encrypted SSDから選択できます。Encrypted HDD/SSDについては[「暗号化ブロックストレージ」](https://docs.nhncloud.com/ja/Storage/Block%20Storage/ja/console-guide/#_2)を参照してください。
2. ブロックストレージサイズ(GB): ルートブロックストレージの容量を設定します

### 4. ネットワーク設定
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/public/ja/webfirewall_public_ja_console-guide-self-piolink_08_241125.png" width="1200" />

1. ネットワークインターフェース設定
   * ネットワークインターフェース作成: 選択したサブネットに自動的にインターフェースが作成される方式です。
   * 既存のネットワークインターフェース指定: 既に作成されているインターフェースを設定する方式です。 以下の「2. ネットワーク」と「3. Floating IP」設定は、既存のインターフェースの設定に従うため、省略されます。
2. ネットワーク: VPCに定義されたサブネットの中からインスタンスに接続するサブネットを選択します。PENTA WAFは追加インターフェース設定をサポートしません。
3. Floating IP: インスタンス作成後に「Floating IP」使用の有無を指定します。この際、WAFインスタンスが所属するVPCがインターネットゲートウェイと接続されている必要があります。現在設定しなくても「Instance > Floating IP管理」、「Network Interface > Floating IP管理」などで設定できます。
4. セキュリティグループ: WAFインスタンスに適用するセキュリティグループを選択します。セキュリティグループは以下の **[表2. セキュリティグループ設定例]** を参照してください。

<br>

| 方向 | IPプロトコル | ポート | リモート(CIDR) | 説明 |
| :-------: | :-----: | :---: | :---: | :--- |
| 수신 | TCP | 80 (HTTP) | 0.0.0.0/0 | WAFウェブサービス |
| 수신 | TCP | 443 (HTTPS) | 0.0.0.0/0 | WAFウェブサービス |
| 수신 | TCP | 8443 | 管理者IP | WAF 管理コンソール(UI)ポート(管理者IPのみ許可) |
| 수신 | TCP | 22 (SSH) | 管理者IP | WAF SSH ターミナルポート(管理者IPのみ許可) |
| 송신 | ICMP | - | 0.0.0.0/0 | WebファイアウォールとWebサーバー間のヘルスチェック(health check)通信 |
| *송신 | 임의 | - | 0.0.0.0/0 | WAFの外部ライセンス、シグネチャ更新などの通信用途 |

<p align="center"> [表2. セキュリティグループ設定例] </p>

> [参考]
> * WAFのデフォルトステータス確認(health check)方式はICMPに設定されており、Webサーバとステータス確認(health check)が失敗した場合、Webサービスが動作しません。
> * 上記[表2. セキュリティグループ設定例]のWAFの*送信ルールは、例のようにすべての外部通信を許可することを推奨します。

## WAFの初期設定

* WAFの初期設定ガイドを参考にして初期設定を実施してください。主な内容は次のとおりです。
  * アプリケーションを設定します。
  * 負荷分散メニューで実際に保護されるサーバーを設定します。
  * プロキシで動作させるには、Source NAT機能を有効にします。
  * wAF IPへのアクセスをテストして、Webサービスが正常かどうかを確認します。
  * 設定した内容を保存してバックアップします。

[WEBFRONT-KS_初期設定ガイド](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS_KR_Initial-Setup-Guide.pdf)
* 初期設定完了後、保護対象ドメイントラフィックがWebファイアウォールを経由するように設定するには、WebファイアウォールFloating IPでDNSを変更する必要があります。
* 製造社が提供するリリースノートを参考にして、WebファイアウォールPLOSを最新バージョンにアップデートする必要があります。
  * リリースノートのダウンロード方法: Webファイアウォール接続 > SYSTEM > 一般設定 > PLOS管理 > ダウンロードPLOS > ダウンロード

## WAF運営

WAF構成の説明書を参考にして機器を運営してください。主な内容は次のとおりです。

* 使用するセキュリティポリシーを有効にします。
* 学習機能を活用して例外処理などのポリシー最適化を実施します。
* セキュリティログをモニタリングします。

[WEBFRONT-KS_アプリケーション設定ガイド](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS_KR_Application-Configuration-Guide.pdf) <BR>
[WEBFRONT-KS_システム設定ガイド](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS_KR_System-Configuration-Guide.pdf) <BR>

> [参考]
> * Selfサービスでは使用ガイドのみ提供され、Managedサービスを利用する場合は、運営代行および24時間セキュリティ監視サービスを提供します。
