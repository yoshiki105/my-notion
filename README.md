# my-notion
[Notion](https://www.notion.so/)のクローンアプリです。

## 最低限の機能
- ユーザー登録
- テンプレート別ドキュメント管理
  - ドキュメント管理
    - リッチテキストコンテンツと編集機能
    - サブページ
  - データベース
    - ボード管理
      - ボードにリストがあり、そこにカードが紐づく
      - ドラッグ・アンド・ドロップでカードの位置を入れ替える
      - カード内にタスクリストを作成できる

## 使用技術
- Rails
- Nuxt.js
- WebSocket

## ER図

![my-notion_erd](https://user-images.githubusercontent.com/66538632/185011172-ea9789ed-5604-4a38-9826-6d9bc27665b0.jpg)

## 各テーブル・カラムについて

- usersテーブル
  - サービスを使用するユーザー情報。
  - usersテーブルのカラム
    - name
      - サービス内で使用するユーザー名。
    - email
      - メールアドレス。登録時使用。
    - crypted_password
      - 登録時・ログイン時に使用するパスワード。
    - salt
      - パスワードをより強固にするための文字列。

- blocksテーブル
  - Notionを構成する全ての要素。
  - blocksテーブルのカラム
    - block_id
      - 親blockのid。
    - user_id
      - 従属しているuserのid。
    - type
      - `page`, `to_do`, `workspace`などblockの表示を決める文字列が入る。
      - 子blockは親のtypeによって表示が変わることがある。
    - uid
      - 16進数で表現した32桁のユニークな文字列。
    - order_number
      - 子blockのときの表示順を決定する。

- propertiesテーブル
  - blockそれぞれが持っている固有の情報。
  - propertiesテーブルのカラム
    - block_id
      - 従属しているblockのid。
    - title
      - ほとんどの場合、blockが表示するテキスト。
    - checked
      - block_typeが`to_do`の時に使用。
    - text
      - block_typeが`database`の時に使用。
    - number
      - block_typeが`database`の時に使用。
