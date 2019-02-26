## Security > WEB Firewall > コンソール使用ガイド > Self

WEB Firewall Selfサービスでは、Webサーバーを保護できるようにWebファイアウォールインスタンスを作成して運営できるガイドを提供します。
ここではWEB Firewall Selfサービスの使用方法を紹介します。

WEB Firewallサービスを利用するには、**TOAST Console**にログインし、サービスリストから**Security > WEB Firewall**をクリックします。

## サービス申請および解除

![webfirewall_01_201812.png](https://static.toastoven.net/prod_web_firewall/webfirewall_01_201812.png)

### Webファイアウォール作成

1. **WEB Firewall**コンソールの**利用料金**の下にある**Self**行で**リンク**をクリックして、インスタンス作成ページに移動します。
2. **+ インスタンス作成**をクリックし、画像リストからPLOS WAFを選択してインスタンス情報を入力します。詳細は下記**Webファイアウォールインスタンス作成方法**を参照してください。

※インスタンスが作成されると、すぐに利用料金がかかります。

### Webファイアウォール解除

Webファイアウォールインスタンスを選択して削除します。

※ Webファイアウォール構成時、トラフィックがWebファイアウォールを経由している途中でインスタンスを削除すると、サービス障害が発生することがあります。
※使用中のWebサービスを確認してから、インスタンスを削除してください。

## Webファイアウォールインスタンス作成方法

![webfirewall_02_201812.png](https://static.toastoven.net/prod_web_firewall/webfirewall_02_201812.png)

※下記の例のように、信頼するIPおよび使用ポートに対してセキュリティーグループ(security group)を設定します。

| Direction | IPプロトコル | ポート範囲 | 遠隔 | 説明 |
| :-------: | :-----: | :---: | :---: | :--- |
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | Webサービスポート |
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | Webサービスポート |
| Ingress | TCP | 8443 | x.x.x.x/32 (CIDR) | Webファイアウォール管理用ポート(管理者IPのみ許可) |
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | Webファイアウォールターミナルポート(管理者IPのみ許可) |
| Ingress | ICMP | - | 192.168.0.0/24 (CIDR) | WebファイアウォールとWebサーバー間の状態確認(health check)通信 |

※ Webファイアウォールの基本状態確認(health check)方式はICMPに設定されており、Webサーバーと状態確認(health check)が失敗した時はWebサービスが動作しません。

## Webファイアウォールの初期設定

Webファイアウォールの初期設定ガイドを参照して初期設定を行います。主な内容は次のとおりです。

*アプリケーションを設定します。
*負荷分散メニューで、実際に保護するサーバーを設定します。
*プロキシで動作するようにするには、Source NAT機能を有効にします。
* WebファイアウォールIPへのアクセスをテストして、Webサービスが正常かどうかを確認します。
*設定した内容を保存してバックアップします。

[WEBFRONT-KS初期設定ガイド](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_初期%20設定%20ガイド.pptx)
※初期設定完了後、保護対象ドメイントラフィックがWebファイアウォールを経由するように、DNSをWebファイアウォールFloating IPに変更する必要があります。

## Webファイアウォールの運用

Webファイアウォール構成説明書を参照して機器を運用します。主な内容は次のとおりです。

*使用するセキュリティーポリシーを有効にします。
*学習機能を活用して、例外処理などのポリシー最適化を行います。
*セキュリティーログをモニタリングします。

[WEBFRONT-KSアプリケーション構成説明書](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_アプリケーション%20構成%20説明書.pdf)
[WEBFRONT-KSシステム構成説明書](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_システム%20構成%20説明書.pdf)
※ Selfサービスでは使用ガイドのみ提供され、Managedサービス利用時、運営代行および24時間セキュリティー監視サービスを提供します。
