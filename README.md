# awstidy
 A CLI tool designed to efficiently understand, organize, and manage AWS resources.
## 要件

### 機能要件

1. **AWSリソースの取得**
    - 全リソースのリスト化（フィルタリング対応）。
    - 出力形式：CSV、JSON、テキスト。
2. **ARN情報の取得**
    - 指定したリソースのARNを一覧表示。
3. **リソース削除**
    - 削除候補リソースの提案。
    - 確認後、指定リソースを削除。
4. **インフラ設定**
    - 必要なIAMロール・ポリシーのIaCによる自動デプロイ。
5. **認証**
    - AWS STSによる一時認証。

### 非機能要件

- 高いセキュリティとプライバシー保護。
- インストールと利用が簡単。
- モジュール化された設計で将来の拡張に対応。

---

## 仕様

### CLI操作例

1. **リソース一覧の取得**
    
    ```bash
    
    awstidy list-resources --format csv --output resources.csv
    
    ```
    
2. **ARNリストの出力**
    
    ```bash
    
    awstidy list-arns --resource-type ec2
    
    ```
    
3. **削除候補の確認**
    
    ```bash
    awstidy suggest-deletion --output candidates.json
    
    ```
    
4. **リソース削除**
    
    ```bash
    awstidy delete-resource --arn <resource-arn>
    
    ```
    
5. **IAMロールの自動作成**
    
    ```bash
    awstidy setup-iam
    
    ```
    

---

## 設計

### 全体構造

1. **コアモジュール**
    - AWSリソース情報の取得・整形。
    - 出力フォーマット変換。
2. **認証モジュール**
    - AWS STSを用いた一時認証。
3. **削除モジュール**
    - AWSリソース削除の操作。
4. **インフラ設定モジュール**
    - 必要なIAMロールとポリシーを生成・デプロイ（AWS CDK使用）。
5. **CLIインターフェース**
    - ユーザー入力と各モジュールの連携。

---

### 使用技術

- 言語: Go
- AWS SDK: `aws-sdk-go-v2`
- IaC: AWS CDK
- テスト: 単体テスト