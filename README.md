# 大まかな手順

### 参考サイト
- https://dev.classmethod.jp/articles/githubactions-ecs-fargate-cicd-beginner/

### IAMユーザー作成
- IAMユーザーを作成
- ロールを割り当て（ECR, ECS用）
- アクセスキーを発行
- アクセスキーを~/.aws/configに設定（aws configure）

### GitHubActionsの設定
- 空のリポジトリを作成
- GitHub Secrectsでアクセスキー・シークレットアクセスキーを設定
  - AWS_ACCESS_KEY_ID
  - AWS_SECRET_ACCESS_KEY
- Actionsで「Deploy to Amazon ECS」のテンプレートを作成し、コミットする

### ソースコードの準備-1
- リポジトリをクローン（.awsディレクトリのみある状態）
- 別ブランチに切り替える（mainブランチにpushするとCICDが実行されてしまう）
- Dockerfile または dockercompose.yml を作成
- 実行したいアプリケーションを開発
- ECSタスク定義のjsonを作成…☆

### ECRにコンテナをアップロード
- ECRコンソールで、画面の指示に従って行う

### ECSにデプロイ
- 大前提として、GitHubActionsを使用するためには、最初にコンソールで１回目のデプロイを済ませている必要がある
- コンソールでデプロイ作業を実行する
- タスク定義ファイルは「☆」の部分で作成したjsonを使用する。

### ソースコードの準備-2
- ECR, ECSでの作業時に設定した環境変数をaws.ymlに設定しpush
- mainブランチへのマージリクエスト作成＆マージ実行
- CICDが問題なく動作することを確認する