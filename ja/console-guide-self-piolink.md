## Security > WEB Firewall > コンソール使用ガイド > Self > PIOLINK(WEBFRONT-KS)

WEB Firewall Selfサービスでは、Webサーバーを保護できるようにWebファイアウォールインスタンスを作成し、運営できるガイドを提供します。
ここではWEB Firewall Selfサービスの使い方を紹介します。

WEB Firewallサービスを利用するには、**NHN Cloud Console**にログインし、サービスリストで**Security > WEB Firewall**をクリックします。

## サービス申請および解除

![webfirewall_console_guide_self_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_220613.png)

### Webファイアウォールの作成

1. **WEB Firewall**コンソールの**Self利用申請**で**移動**をクリックしてインスタンス作成ページへ移動します。
2. **+ インスタンス作成**をクリックし、イメージリストからPLOS WAFを選択し、インスタンス情報を入力します。詳しい方法は、**Webファイアウォールインスタンス作成の詳細手順**を参照してください。

※インスタンスが作成され次第、利用料金が発生します。

### Webファイアウォールの解除

Webファイアウォールインスタンスを選択して削除します。

※ Webファイアウォール構成時、トラフィックがWebファイアウォール経由で利用中にインスタンスを削除した場合、サービス障害が発生することがあります。<BR>
※使用中のWebサービスを確認した後、インスタンスを削除してください。

## Webファイアウォールインスタンス作成の詳細手順

![webfirewall_console_guide_self_1_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_piolink_230904.png)

※以下の例のように、信頼するIPおよび使用ポートに対してセキュリティグループ(security group)を設定します。

| Direction | IPプロトコル | ポート範囲 | 遠隔 | 説明 |
| :-------: | :-----: | :---: | :---: | :--- |
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | Webサービスポート |
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | Webサービスポート |
| Ingress | TCP | 8443 | x.x.x.x/32 (CIDR) | Webファイアウォール管理用ポート(管理者IPのみ許可) |
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | Webファイアウォールターミナルポート(管理者IPのみ許可) |
| Ingress | ICMP | - | 192.168.0.0/24 (CIDR) | WebファイアウォールとWebサーバー間のヘルスチェック(health check)通信 |

※ Webファイアウォールの基本ヘルスチェック(health check)方式は、ICMPに設定されており、Webサーバーとヘルスチェック(health check)が失敗した場合、Webサービスは動作しません。

## Webファイアウォールの初期設定

* Webファイアウォールの初期設定ガイドを参考にして初期設定を実施してください。主な内容は次のとおりです。

  * アプリケーションを設定します。
  * 負荷分散メニューで実際に保護されるサーバーを設定します。
  * プロキシで動作させるには、Source NAT機能を有効にします。
  * WebファイアウォールIPへのアクセスをテストして、Webサービスが正常かどうかを確認します。
  * 設定した内容を保存してバックアップします。

[WEBFRONT-KS初期設定ガイド](https://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_初期%20設定%20ガイド.pdf)
* 初期設定完了後、保護対象ドメイントラフィックがWebファイアウォールを経由するように設定するには、WebファイアウォールFloating IPでDNSを変更する必要があります。
* 製造社が提供するリリースノートを参考にして、WebファイアウォールPLOSを最新バージョンにアップデートする必要があります。
  * リリースノートのダウンロード方法: Webファイアウォール接続 > SYSTEM > 一般設定 > PLOS管理 > ダウンロードPLOS > ダウンロード

## Webファイアウォール運営

Webファイアウォール構成の説明書を参考にして機器を運営してください。主な内容は次のとおりです。

* 使用するセキュリティポリシーを有効にします。
* 学習機能を活用して例外処理などのポリシー最適化を実施します。
* セキュリティログをモニタリングします。

[WEBFRONT-KSアプリケーション構成説明書](https://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_アプリケーション%20構成%20説明書.pdf) <BR>
[WEBFRONT-KSシステム構成説明書](https://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_システム%20構成%20説明書.pdf) <BR>
※ Selfサービスでは使用ガイドのみ提供され、Managedサービスを利用する場合は、運営代行および24時間セキュリティ監視サービスを提供します。
