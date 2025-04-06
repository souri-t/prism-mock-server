# Prism Mock API サーバー

このプロジェクトは、[Prism](https://stoplight.io/open-source/prism)を使用したモックAPIサーバーを提供します。OpenAPI仕様に基づいてユーザー管理のRESTful APIをシミュレートします。

## 概要

このモックサーバーは、以下のエンドポイントを提供します：

- ユーザー一覧の取得 (GET `/users`)
- ユーザーの新規作成 (POST `/users`)
- 特定のユーザーの取得 (GET `/users/{userId}`)
- ユーザー情報の更新 (PUT `/users/{userId}`)
- ユーザーの削除 (DELETE `/users/{userId}`)

## 前提条件

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## 使用方法

### サーバーの起動

```bash
docker-compose up
```

サーバーは `http://localhost:3080` でアクセス可能になります。

### サーバーの停止

```bash
docker-compose down
```

## APIエンドポイントの詳細

### ユーザー一覧の取得

```
GET http://localhost:3080/users
```

#### レスポンス例

```json
[
  {
    "id": 1,
    "name": "山田太郎",
    "email": "yamada@example.com",
    "age": 30,
    "createdAt": "2025-01-15T09:30:00.000Z"
  },
  {
    "id": 2,
    "name": "佐藤花子",
    "email": "sato@example.com",
    "age": 25,
    "createdAt": "2025-01-20T14:15:00.000Z"
  },
  {
    "id": 3,
    "name": "鈴木一郎",
    "email": "suzuki@example.com",
    "age": 35,
    "createdAt": "2025-01-25T11:45:00.000Z"
  }
]
```

### ユーザーの新規作成

```
POST http://localhost:4010/users
Content-Type: application/json

{
  "name": "田中健太",
  "email": "tanaka@example.com",
  "age": 28
}
```

**注意**: このエンドポイントはどのようなパラメータでも受け付けます。必須フィールドの制約はなく、常に成功レスポンスを返します。

#### レスポンス例

```json
{
  "id": 4,
  "name": "田中健太",
  "email": "tanaka@example.com",
  "age": 28,
  "createdAt": "2025-04-06T10:15:30.000Z"
}
```

### 特定のユーザーの取得

```
GET http://localhost:4010/users/1
```

#### レスポンス例

```json
{
  "id": 1,
  "name": "山田太郎",
  "email": "yamada@example.com",
  "age": 30,
  "createdAt": "2025-01-15T09:30:00.000Z"
}
```

### ユーザー情報の更新

```
PUT http://localhost:4010/users/1
Content-Type: application/json

{
  "name": "山田太郎（更新済）",
  "email": "yamada_updated@example.com",
  "age": 31
}
```

**注意**: このエンドポイントはどのようなパラメータでも受け付けます。必須フィールドの制約はなく、常に成功レスポンスを返します。

#### レスポンス例

```json
{
  "id": 1,
  "name": "山田太郎（更新済）",
  "email": "yamada_updated@example.com",
  "age": 31,
  "createdAt": "2025-01-15T09:30:00.000Z"
}
```

### ユーザーの削除

```
DELETE http://localhost:4010/users/1
```

#### レスポンス

204 No Content

## プロジェクト構成

```
.
├── docker-compose.yml     # Dockerコンテナ設定
├── openapi.yml           # OpenAPI仕様のAPI定義
└── examples/             # レスポンス例のJSONファイル
    ├── user-created.json    # ユーザー作成成功時のレスポンス例
    ├── user-detail.json     # ユーザー詳細のレスポンス例
    ├── user-not-found.json  # ユーザーが見つからない場合のエラー例
    ├── user-updated.json    # ユーザー更新成功時のレスポンス例
    └── users-list.json      # ユーザー一覧のレスポンス例
```

## 参考リンク

- [Prism ドキュメント](https://docs.stoplight.io/docs/prism)
- [OpenAPI 仕様](https://swagger.io/specification/)