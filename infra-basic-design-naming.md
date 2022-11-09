# 命名規則
## 本書の目的
命名規則を定める目的は以下の通り。  

* リソースの役割を示す
* 対象リソースの取り間違えを防ぐ
* 管理上の識別性

命名規則によって以下の識別を明確にする。  

* 対象システム
* 環境 (本番、ステージング、開発、性能試験)
* AWS リソース (Lambda、Security Group、RDS、ELB など)

## 関連資料
本書の前提となる資料、情報元となる資料は以下の通り。  

* [非機能要件一覧](https://docs.google.com/spreadsheets/d/1B5z5-YWOrzDnu0gY5AM-_wRCRX9LD9EZ/edit?usp=share_link&ouid=106375452255861814726&rtpof=true&sd=true)
* [構築ガイドライン](https://drive.google.com/file/d/1KaAbHae4c2WQy37im2Ujmpvk_nD-QD8-/view?usp=share_link)
* [クラウドセキュリティガイドライン](https://docs.google.com/document/d/1uHi7mWWJaxotaLL3iJ90vqa7ZCzF9PId/edit?usp=share_link&ouid=106375452255861814726&rtpof=true&sd=true)
* [POHR論理システム構成図](https://app.diagrams.net/#G122z8inmGkVqX_vwh6zkzKVSDbcr20eBX)

# 対象非機能要件
本書に関連する対象非機能要件は以下の通り。

|大項目|項番|定義項目|決定メトリクス|備考|
|---|---|---|---|---|
|セキュリティ|E.1.1.1|情報セキュリティに関するコンプライアンス|順守すべき社内規程、ルール、法令、ガイドライン等有|LION様策定のクラウドセキュリティガイドライン、構築ガイドラインを従った設計|
|システム環境・エコロジー|F.1.1.1/F.1.2.1|構築/運用時の制約条件|制約有り(重要な制約のみ適用)|LION様提供のAWSクラウドセキュリティガイドライン、AWS構築ガイドライン|

## 基本ルール
命名規則の基本ルールは以下の通り。  

* 単語間はハイフン (-) で結ぶ
* 英小文字と数字のみを使用

マルチバイト文字、英大文字、記号、アンダースコア (_) は使用しないようにする。  

# 命名規則表
* 対象システムの名前(sysname)
    * システムで一意となる識別子(例：pzone,dzone,lzone,oral,notifidel)
* 環境(env)
    * 本番、ステージング、開発など(PRD/STG/DEV/PERF)
* ネットワークレイヤー(nlayer)
    * パブリック、プライベートなど(public/private)
* 種別（type）
    * APサーバー、DBサーバーなど(app/db)
* 目的（use）
    * ログ保管用、静的コンテンツ配信用など(log/contents)

## AWSリソース

|AWSリソース|命名規則|備考|
|---|---|---|
|VPC|{sysname}-{env}-vpc| |
|Subnet|{sysname}-{env}-{nlayer}-{type}-subnetXX|XXは連番、AZ毎に分ける|
|RouteTable|{sysname}-{env}-{nlayer}-rtb||
|InternetGateway|{sysname}-{env}-igw||
|ELB|{sysname}-{env}-alb||
|TargetGroup|{sysname}-{env}-tg||
|EC2|{sysname}-{env}-{type}XX||
|ECS Cluster|{sysname}-{env}-{type}-cluster||
|ECS task|{sysname}-{env}-{type}-{use}-task||
|ECS Container|{sysname}-{env}-{type}-{use}-container||
|Lambda|{sysname}-{env}-{use}-lambda| |
|API Gateway|{sysname}-{env}-api| |
|IAMRole|{sysname}-{env}-{type}-role||
|SecurityGroup|{sysname}-{env}-{type}-sg||
|RDS|{sysname}-{env}-rds||
|S3|{sysname}-{env}-{type}{use}-{AccountID}|下記「S3命名規則補足」を参照|

## S3命名規則補足
S3 バケット名称を決定する際は以下に留意する。  

* 全世界で一意になるようにする
* 3～63 文字以内にする
* 英文字で始まり、英数字で終わる
* 英数字とハイフン以外は使用しない、大文字またはアンダースコアを含めない
* 末尾にハイフンと数字を付けない
* 仮想ホスティング形式のバケットを使用するときは、バケット名にピリオド (「.」) を使用しない


# タグ
上記で定めた命名規則は Name タグに付与する。  

環境ごと、システムごとにリソースを検索することは、管理面やコスト把握に有用である。  
そのため Name タグの他に環境タグとシステムタグも付与する。  

## Technical Tags

|タグキー|タグ値|
|---|---|
|Name|命名規則で定めたリソース名称を入力|
|Environment|環境名 (PRD/STG/DEV/PERF など) |
|SystemName|システムを識別可能な文字列|
|ApplicationID|稼働しているアプリケーションを識別する文字列|
|ApplicationRole|アプリケーション機能 (Web/DB/batch など)|




