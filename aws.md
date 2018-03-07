# AWS at Wantedly

## AWS

- Amazon.com が提供しているクラウドコンピューティングサービス
- もともと自社システムとして使っていた技術を一般に公開したもの
- アクセスのピークやビジネススケールに合わせて、柔軟にリソースを制御可能
  - 従来（オンプレ）の場合は調達に数日 ~ 数週間かかり、スケールアップ & ダウンも容易ではなかった
- 基本的に使った分だけ支払えば良い
- Management Console のほか、API 経由ですべての操作を実行可能
  - プログラムのみでインフラを制御できる
  - 各言語対応の SDK が配布されている
- 世の中たいていの Web サービスは AWS 上で稼働している
- Amazon.com 全体の売上の1割を占める
  - [アマゾン、2016年の年間売上15兆円：北米のPrimeとAWSが貢献で安定してきた黒字経営(佐藤仁) - 個人 - Yahoo!ニュース](https://news.yahoo.co.jp/byline/satohitoshi/20170204-00067359/)
- 勝手な所感
  - リソースそのものにもちろんお金かかるけど、転送量も馬鹿にならない
  - AWS のマネージドサービスは、素の状態で使うのが難しい
    - 特に Lambda とか ECS とか
    - 各社独自ソリューションが発達してしまう

## リージョンとアベイラビリィーゾーン

http://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/using-regions-availability-zones.html

- 全世界の**リージョン**にデータセンターを持つ
  - 14 regions
  - 東京にもある (ap-northeast-1)
- 各リージョンに最低3つの**アベイラビリティーゾーン (AZ)** が存在する
  - 物理的・電源的に分離されたデータセンタ
  - 東京は3つ (1a, 1b, 1c)、ユーザが使えるのはこの内2つ
- 同一リージョン内で別々の AZ にあるインスタンスへアプリケーションをデプロイする **Multi-AZ** が推奨されている
  - 片方の AZ で障害があった場合でも、システムをダウンさせることなく稼働可能
  - ELB でアクセスを各 AZ に振り分ける
  - Wantedly では Kubernetes クラスタと RDS において Multi-AZ 構成を組んでいる

## EC2

- Elastic Computing Cloud
- 仮想コンピューティング環境
- 単位は**インスタンス**
- **AMI** から起動する
  - Amazon Linux, Ubuntu, CoreOS...
  - Wordpress などアプリケーションのインストールされたもの
  - 稼働中のインスタンスから作成したユーザ独自の AMI
- Launch -> (Start <-> Stop) -> Terminate
  - Terminate したらデータが全部消える
- 性能別に様々な**インスタンスタイプ**が存在する
  - t: 最も安価で性能が低い。CPU がバーストする
  - m: CPU とメモリのバランスがとれている
  - c: CPU 最適化
  - r: メモリ最適化
  - i: I/O 最適化
  - g: GPU 搭載
- ストレージは**インスタンスストア** と **EBS (Elastic Block Store)** が存在する
  - EBS は 外付け HDD / SSD みたいなもの
- 1時間単位で課金
- Wantedly では約200台のインスタンスが稼働している
  - 本番環境は c4
  - ステージング環境は m4
  - Elasticsearch は r3
  - 機械学習用に g2
  - Kubernetes クラスタに24台 (5 + 12 + 7)
- **Elastic IP** を利用して固定 Public IP 割当

## ELB

- Elastic Load Balancer
- EC2 の前段に置き、アクセスを各インスタンスに振り分ける L7 / L4 ロードバランサ
- SSL ターミネーション
  - ELB に SSL/TLS 証明書を持たせて、SSL セッションを ELB <-> クライアント間で完結させる

### CLB

- Classic Load Balancer
- 1年前までは ELB といえばこれだった
- プロトコル関係なしにバランシング
- Kubernetes 上のサービス前段にいるのはこれ

### ALB

- Application Load Balancer
- 2016年8月にリリース
  - 今後はこっちに力入れるんでしょうなあ
- L7 通信に特化したロードバランサ
- (ALB <-> クライアント) HTTP/2 対応
  - バックエンドと HTTP/2 したいなら CLB
- Path-based / Host-based rule
- 非 Kubernetes サービスの前段にいる

## ECS

- Elastic Container Service
- 複数 EC2 インスタンスをまとめて1クラスタとみなし、その上で Docker コンテナをよしなに実行する
  - 各 EC2 インスタンスにエージェント (ecs-agent) コンテナを配置する
  - master - slave の概念がない
- マイクロサービスと ELB に紐づく `Service`、実際のコンテナ定義を書く `TaskDefinition`
- Wantedly では使ってない
  - Kubernetes 使ってるので

## ECR

- Elastic Container Registry
- フルマネージド Docker image registry
- IAM によるアクセス制御が可能
- ローカルへ pull するのは面倒
  - 12時間ごとに `docker login $(aws ecr get-login --no-include-email)` を実行する必要がある
- Wantedly では大活躍
  - 自前で Docker Registry 運用してたときは死にまくってた

## AutoScaling Group

- EC2 インスタンスを自動でスケーリング
- 通常起動すべき台数 (`DesiredCount`) を下回ったら、不足分が自動で追加される
- メトリクスがしきい値を超えたらスケールアップしたり、業務時間に合わせてスケールアップ / ダウンできる

## VPC

- Virtual Private Cloud
- AWS 内での仮想ネットワーク環境
- VPC はリージョン単位
- VPC 内部で公開 / 非公開**サブネット**を切り、その中でインスタンスを起動する
  - サブネットは AZ 単位
- VPC -> サブネットで CIDR が割り振られる
- **セキュリティグループ**がインスタンスのファイアウォールとなる
- VPC Peering で VPC を繋げられる
  - 双方の CIDR が被ってると不可能

## RDS

- Relational Database Service
- インスタンスや RDB ソフトウェアの管理は AWS にお任せなデータベースサービス
  - セキュリティパッチ適用とかに気をもまなくて済む
  - SSH やカーネルレベルのチューニングとかはできない
- EC2 同様インスタンスタイプが存在する
- パラメータグループで DB のパラメータを設定
- 自動バックアップや Multi-AZ レプリケーションを設定可能
  - 5分前のバックアップから即時リカバリ
- Wantedly では PostgreSQL を利用
  - Heroku の標準 DB が PostgreSQL だった時の名残
- Aurora
  - ミドルウェアレベルまでフルマネージドかつ高可用性かつハイパフォーマンスな AWS 独自の DB エンジン
  - MySQL or PostgreSQL 互換

## ElastiCache

- フルマネージドの memcached / Redis サービス

## S3

- Simple Storage Service
- 99.999999999％ の耐久性を誇る、容量上限の存在しないストレージ
- 大量アクセスも難なく捌ききるスケーラブルなストレージ
  - オンプレ使っててもストレージだけは S3 使うところがあるくらい
- 一般的なディレクトリ構造と似た構成
- アクセス制限やバージョニング、自動アーカイブ機能
  - Standard: 普通はこれ
  - Reduced redundancy: 99.99% の耐久性、ちょっと安い
  - Glacier: 最も安い ($0.005/GB/mo, Standard の 1/5)、取り出すのに4-5時間かかる、バックアップ用途
- Wantedly では JavaScript や画像などのアセット、設定ファイルを保管

## CloudFront

- CDN (Content Delivery Network)
- 全世界にエッジを持ち、静的コンテンツをキャッシュして配信する
  - 日本だと東京・大阪にある
- Wantedly の画像はすべて CloudFront 経由で配信されている
  - 一部 JavaScript, CSS アセットも
- 古い画像が配信されたままにならないよう注意
 - Invalidate
 - パスにハッシュ値をつけてキャッシュさせる
- 最近だと動的コンテンツの前段にも CDN を置く事例がある
  - [Secured API Acceleration with Engineers from Amazon CloudFront and Sl…](https://www.slideshare.net/AmazonWebServices/secured-api-acceleration-with-engineers-from-amazon-cloudfront-and-slack)
  - Origin - Edge 間で AWS の太いバックボーンを使う
  - DDoS 対策
  - c.f. [CDN切り替え作業における、Web版メルカリの個人情報流出の原因につきまして - Mercari Engineering Blog](http://tech.mercari.com/entry/2017/06/22/204500)

## IAM

- Identity and Access Management
- AWS 上のアカウント管理の仕組み
- User, Group, Role
- 各リソースへのアクセスを IAM リソース単位で制御
- アクセスキーを IAM User 単位で発行
- Management Console 2段階認証やパスワードのローテーションも設定できる
- OpenID & SAML 連携も可能

## Lambda

- Function as a Service
- JavaScript (Node.js), Python, Java, C# で書かれたスクリプトを実行可能
- インスタンスや言語環境を整えることなく、コードだけ用意すればすぐ実行できる
- 月間100万リクエストまでは無料
- Wantedly では EC2 メンテナンスイベントの Slack 通知や定期的な中間イメージ生成、スローログ解析に利用
  - 運用自動化用途のみ、ユーザ向けプロダクションでは使ってない
- 例によって、デプロイソリューションが山のようにある
  - [Serverless Framework](https://serverless.com/) か [Apex](http://apex.run/) がおすすめ

## Route 53

- AWS の DNS サービス
- Wantedly ではほとんど使ってない
  - `*.wantedly.com` は Heroku 時代の名残で DNSimple を使っている
  - 新しいドメインは Route 53 で買ってレコードセットアップしていたりする
- ドメイン単位の **Hosted Zone** の下にレコードが存在する
- ルーティングポリシー何種類かある
  - DNS ラウンドロビン
  - リクエスト元に最も地理的に近い IP
  - 重み付け
  - レイテンシ
- ドメインも買える
