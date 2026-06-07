# テーブル定義書

## users

| カラム名       | 型            | NULL | PK | UNIQUE | 説明      |
| ---------- | ------------ | ---- | -- | ------ | ------- |
| id         | BIGINT       | NO   | ○  | -      | ユーザーID  |
| name       | VARCHAR(255) | NO   | -  | -      | ユーザー名   |
| email      | VARCHAR(255) | NO   | -  | ○      | メールアドレス |
| password   | VARCHAR(255) | NO   | -  | -      | パスワード   |
| created_at | TIMESTAMP    | NO   | -  | -      | 作成日時    |
| updated_at | TIMESTAMP    | NO   | -  | -      | 更新日時    |

---

## categories

| カラム名       | 型            | NULL | PK | UNIQUE | 説明      |
| ---------- | ------------ | ---- | -- | ------ | ------- |
| id         | BIGINT       | NO   | ○  | -      | カテゴリID  |
| name       | VARCHAR(255) | NO   | -  | -      | カテゴリ名   |
| slug       | VARCHAR(255) | NO   | -  | ○      | URL用識別子 |
| created_at | TIMESTAMP    | NO   | -  | -      | 作成日時    |
| updated_at | TIMESTAMP    | NO   | -  | -      | 更新日時    |

---

## products

| カラム名        | 型            | NULL | PK | FK            | 説明     |
| ----------- | ------------ | ---- | -- | ------------- | ------ |
| id          | BIGINT       | NO   | ○  | -             | 商品ID   |
| category_id | BIGINT       | NO   | -  | categories.id | カテゴリID |
| name        | VARCHAR(255) | NO   | -  | -             | 商品名    |
| description | TEXT         | YES  | -  | -             | 商品説明   |
| price       | INT          | NO   | -  | -             | 商品価格   |
| status      | BOOLEAN      | NO   | -  | -             | 公開状態   |
| created_at  | TIMESTAMP    | NO   | -  | -             | 作成日時   |
| updated_at  | TIMESTAMP    | NO   | -  | -             | 更新日時   |

### status

| 値 | 説明  |
| - | --- |
| 0 | 非公開 |
| 1 | 公開  |

---

## product_images

| カラム名       | 型            | NULL | PK | FK          | 説明     |
| ---------- | ------------ | ---- | -- | ----------- | ------ |
| id         | BIGINT       | NO   | ○  | -           | 商品画像ID |
| product_id | BIGINT       | NO   | -  | products.id | 商品ID   |
| image_path | VARCHAR(255) | NO   | -  | -           | 画像パス   |
| sort_order | INT          | NO   | -  | -           | 表示順    |
| created_at | TIMESTAMP    | NO   | -  | -           | 作成日時   |
| updated_at | TIMESTAMP    | NO   | -  | -           | 更新日時   |

---

## sizes

| カラム名 | 型           | NULL | PK | 説明    |
| ---- | ----------- | ---- | -- | ----- |
| id   | BIGINT      | NO   | ○  | サイズID |
| name | VARCHAR(50) | NO   | -  | サイズ名  |

### 初期データ

| サイズ |
| --- |
| S   |
| M   |
| L   |
| XL  |

---

## colors

| カラム名 | 型           | NULL | PK | 説明     |
| ---- | ----------- | ---- | -- | ------ |
| id   | BIGINT      | NO   | ○  | カラーID  |
| name | VARCHAR(50) | NO   | -  | カラー名   |
| code | VARCHAR(20) | NO   | -  | カラーコード |

### 初期データ

| カラー   | コード     |
| ----- | ------- |
| Black | #000000 |
| White | #FFFFFF |
| Navy  | #000080 |
| Gray  | #808080 |

---

## product_variants

| カラム名       | 型            | NULL | PK | FK          | 説明          |
| ---------- | ------------ | ---- | -- | ----------- | ----------- |
| id         | BIGINT       | NO   | ○  | -           | 商品バリエーションID |
| product_id | BIGINT       | NO   | -  | products.id | 商品ID        |
| size_id    | BIGINT       | NO   | -  | sizes.id    | サイズID       |
| color_id   | BIGINT       | NO   | -  | colors.id   | カラーID       |
| sku        | VARCHAR(100) | NO   | -  | -           | SKU         |
| stock      | INT          | NO   | -  | -           | 在庫数         |
| created_at | TIMESTAMP    | NO   | -  | -           | 作成日時        |
| updated_at | TIMESTAMP    | NO   | -  | -           | 更新日時        |

### 制約

```text
UNIQUE(product_id, size_id, color_id)
UNIQUE(sku)
```

---

## addresses

| カラム名         | 型            | NULL | PK | FK       | 説明     |
| ------------ | ------------ | ---- | -- | -------- | ------ |
| id           | BIGINT       | NO   | ○  | -        | 住所ID   |
| user_id      | BIGINT       | NO   | -  | users.id | ユーザーID |
| postal_code  | VARCHAR(20)  | NO   | -  | -        | 郵便番号   |
| prefecture   | VARCHAR(100) | NO   | -  | -        | 都道府県   |
| city         | VARCHAR(255) | NO   | -  | -        | 市区町村   |
| address1     | VARCHAR(255) | NO   | -  | -        | 番地     |
| address2     | VARCHAR(255) | YES  | -  | -        | 建物名    |
| phone_number | VARCHAR(20)  | NO   | -  | -        | 電話番号   |

---

## favorites

| カラム名       | 型      | NULL | PK | FK          | 説明      |
| ---------- | ------ | ---- | -- | ----------- | ------- |
| id         | BIGINT | NO   | ○  | -           | お気に入りID |
| user_id    | BIGINT | NO   | -  | users.id    | ユーザーID  |
| product_id | BIGINT | NO   | -  | products.id | 商品ID    |

### 制約

```text
UNIQUE(user_id, product_id)
```

---

## carts

| カラム名    | 型      | NULL | PK | FK       | 説明     |
| ------- | ------ | ---- | -- | -------- | ------ |
| id      | BIGINT | NO   | ○  | -        | カートID  |
| user_id | BIGINT | NO   | -  | users.id | ユーザーID |

---

## cart_items

| カラム名               | 型      | NULL | PK | FK                  | 説明          |
| ------------------ | ------ | ---- | -- | ------------------- | ----------- |
| id                 | BIGINT | NO   | ○  | -                   | カート商品ID     |
| cart_id            | BIGINT | NO   | -  | carts.id            | カートID       |
| product_variant_id | BIGINT | NO   | -  | product_variants.id | 商品バリエーションID |
| quantity           | INT    | NO   | -  | -                   | 数量          |

---

## orders

| カラム名        | 型           | NULL | PK | FK           | 説明     |
| ----------- | ----------- | ---- | -- | ------------ | ------ |
| id          | BIGINT      | NO   | ○  | -            | 注文ID   |
| user_id     | BIGINT      | NO   | -  | users.id     | ユーザーID |
| address_id  | BIGINT      | NO   | -  | addresses.id | 配送先住所  |
| total_price | INT         | NO   | -  | -            | 合計金額   |
| status      | VARCHAR(50) | NO   | -  | -            | 注文状態   |

### status

| 値         | 説明    |
| --------- | ----- |
| pending   | 未決済   |
| paid      | 決済完了  |
| shipping  | 配送中   |
| completed | 配送完了  |
| cancelled | キャンセル |

---

## order_items

| カラム名               | 型      | NULL | PK | FK                  | 説明          |
| ------------------ | ------ | ---- | -- | ------------------- | ----------- |
| id                 | BIGINT | NO   | ○  | -                   | 注文明細ID      |
| order_id           | BIGINT | NO   | -  | orders.id           | 注文ID        |
| product_variant_id | BIGINT | NO   | -  | product_variants.id | 商品バリエーションID |
| price              | INT    | NO   | -  | -                   | 購入時価格       |
| quantity           | INT    | NO   | -  | -                   | 数量          |

---

## payments

| カラム名                     | 型            | NULL | PK | FK        | 説明         |
| ------------------------ | ------------ | ---- | -- | --------- | ---------- |
| id                       | BIGINT       | NO   | ○  | -         | 決済ID       |
| order_id                 | BIGINT       | NO   | -  | orders.id | 注文ID       |
| stripe_payment_intent_id | VARCHAR(255) | NO   | -  | -         | Stripe決済ID |
| amount                   | INT          | NO   | -  | -         | 決済金額       |
| status                   | VARCHAR(50)  | NO   | -  | -         | 決済状態       |
| paid_at                  | TIMESTAMP    | YES  | -  | -         | 決済日時       |
| created_at               | TIMESTAMP    | NO   | -  | -         | 作成日時       |
| updated_at               | TIMESTAMP    | NO   | -  | -         | 更新日時       |
