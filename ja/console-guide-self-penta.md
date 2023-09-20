## Security > WEB Firewall > コンソール使用ガイド > Self > ペンタセキュリティ(WAPPLES SA)

WEB Firewall Selfサービスでは、Webサーバーを保護できるようにWebファイアウォールインスタンスを作成し、運営できるガイドを提供します。
ここではWEB Firewall Selfサービスの使い方を紹介します。

WEB Firewallサービスを利用するには**NHN Cloud Console**にログインし、サービスリストから**Security > WEB Firewall**をクリックします。

## サービス申請および解除

![webfirewall_console_guide_self_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_220613.png)

### Webファイアウォール作成

1. **WEB Firewall**コンソールの**Self利用申請**で**移動**をクリックし、インスタンス作成ページへ移動します。
2. **+インスタンス作成**をクリックしてイメージリストからPENTA WAFを選択し、インスタンス情報を入力します。詳しい方法は、下にある**Webファイアウォールインスタンス作成の詳細手順**を参照してください。

※インスタンスが作成され次第、利用料金が発生します。

### Webファイアウォール解除

Webファイアウォールインスタンスを選択して削除します。

※ Webファイアウォール構成時、トラフィックがWebファイアウォール経由で利用中にインスタンスを削除した場合、サービス障害が発生することがあります。<BR>
※使用中のWebサービスを確認してインスタンスを削除してください。

## Webファイアウォールインスタンス作成の詳細手順

![webfirewall_console_guide_self_1_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_penta_230904.png)

※以下の例のように、信頼するIPおよび使用ポートに対してセキュリティグループ(security group)を設定します。

| Direction | IPプロトコル | ポート範囲 | 遠隔 | 説明 |
| :-------: | :-----: | :---: | :---: | :--- |
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | WAF Webサービスポート |
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | WAF Webサービスポート |
| Ingress | TCP | 5001 | x.x.x.x/32 (CIDR) | WAF管理ツール(UI)ポート(管理者IPのみ許可) |
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | WAF SSHターミナルポート(管理者IPのみ許可) |
| Ingress | TCP/HTTP | 5000 | WAFの上部LBのIP<BR>x.x.x.x/32 (CIDR) | WAF(冗長化)と上部LB間のヘルスチェック(health check)ポート |
| Egress | TCP | 443 (HTTPS) | 218.145.29.166/32 (CIDR) | WAFライセンスアップデートサーバー 
| Egress | TCP | 443 (HTTPS) | 218.145.29.101/32 (CIDR) | WAFライセンスアップデートサーバー |
| Egress | TCP | 5001 | 218.145.29.168/32 (CIDR) | WAFセキュリティルール(custom rule)アップデートサーバー |

※参考: WAF冗長化(設定同期機能使用時)またはAuto Scaling使用時、WAF間5984、6984ポートの許容が必要

## Webファイアウォールの初期設定

* WAFの初回起動後の初期設定


1. ブラウザ(Chrome推奨)でWebファイアウォールWeb管理ツール(UI)に接続
    * https://WAF IP:5001
    * ログイン接続情報: ct@pentasecurity.comへお問い合わせ

2. 環境設定 > システム > 時間同期設定
    * 時間サーバーをそれぞれPenta Server 1&Penta Server 2に設定する

3. ネットワーク設定 > プロキシIP設定
    * NHN Cloud consoleで確認したネットワーク情報を入力(WAF IP、gateway、netmask)します。

4. WAF保護対象設定
    * ネットワーク設定 > 保護対象サーバー設定
    * サーバーモード: Proxyを選択し、portうぃ入力
    * WebサーバーIP(ドメイン)とportを入力(インフラ構成によって「単一」または「複数」を選択可能)
    * ヘルスチェックを使用しない(Webサーバードメインの入力時にのみ使用)
    * WAFがHTTPSサービスを提供する場合、SSL証明書を指定(SSLプロファイルメニューで事前の設定が必要)

5. 保護ポリシー設定
    * セキュリティ設定 > ポリシー設定 > 新規ポリシー追加(ベースポリシー: 「検出のみ実行してブロックはしない」を選択)
    * セキュリティ設定 > ポリシー設定 > 新規Webサイト追加(新規ポリシーに適用)

7. X-Forwarded-For IP設定
    * セキュリティ設定 > ポリシー付加設定 > X-Forwarded-For設定(Block & Detectいずれも設定)

* WAF適用時の参考事項
    * NHN Cloud管理型サービスプロバイダー(managed service provider、MSP)を通じて、顧客インフラ環境にWAFサービスが適用されるようにネットワークroutingを変更構成します。
    * 顧客のインフラ構成によって、WAF Floating IPでDNS変更が必要な場合や、WAF冗長構成時に上部ロードバランサーIPでDNSの変更が必要な場合があります。

## Webファイアウォールの運営

* Webファイアウォールの全体的なユーザーマニュアルおよび利用方法は、Webファイアウォールの管理ツール(UI)で提供します。
* 下画面のユーザーマニュアル位置を参考にして、Webファイアウォール運営全般の利用方法を参照してください。
![wapples_manual.png](https://static.toastoven.net/prod_web_firewall/wapples_manual.png)

※ Selfサービスでは使用ガイドのみ提供され、Managedサービスを利用する場合は、運営代行および24時間セキュリティ監視サービスを提供します。
