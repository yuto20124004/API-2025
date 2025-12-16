##  API実習　2025　課題レポート（第3回）

**API 実習課題**: FastAPI + Streamlit + OpenAPIドキュメントの「設計」「実装」「動作確認」

###  出題範囲：　API実習2025　第7回～第9回まで

###  提出期限：　2025/12/23(火) 17:00


## 課題のコンセプト

- かんたんなToDoメモ管理をWebで実施する課題
- FastAPIを使ったシンプルなAPIの設計と動作確認
- Streamlitと、FastAPIのOpenAPIドキュメント画面を使ったAPI実装確認
- チャレンジ加点要素：　Sqlite,SqlAlchemyを導入することでプラス

--- 
# FastAPIで作るToDoメモ管理とStreamlit連携**

## **目的**

* REST API の基本（GET / POST / PUT / DELETE）を設計・実装
* FastAPI による API 設計と実装ができる
* OpenAPI ドキュメントから動作確認ができる
* Streamlit から API を呼び出してデータ通信を行う

## **課題内容**

### 1．　FastAPI を用いた ToDo メモ管理 API の作成

以下の仕様を満たす **ToDo API** を `main.py` として作成

| 項目                   | 内容                                    |
| -------------------- | ------------------------------------- |
| データ項目                | `id: int`, `title: str`, `done: bool` |
| 保存方法                 | **メモリ上のリスト管理（辞書でも可）**                 |
| エンドポイント（要求）          |                                       |
| `GET /todos`         | 登録された全てのToDoを取得                       |
| `POST /todos`        | 新しいToDoを追加 (title を JSON で送信)         |
| `PUT /todos/{id}`    | `done` 状態を更新                          |
| `DELETE /todos/{id}` | 指定 ID の ToDo を削除                      |

> `id` は自動採番（0,1,2,...）で良い


### 2.OpenAPIドキュメントを使った動作確認

1. FastAPI サーバーを起動

   ```
   uvicorn main:app --reload
   ```
2. ブラウザで OpenAPI を表示

   ```
   http://127.0.0.1:8000/docs
   ```
3. 以下を全て **OpenAPI 画面で実行し、スクリーンショットを撮影**

   * 新規登録（POST）
   * 取得（GET）
   * 更新（PUT）
   * 削除（DELETE）

### 3. Streamlit を用いた Web UI の作成

* ファイル名： `app.py`
* FastAPI と通信し、以下の画面を作成

| UI 操作     | API                |
| --------- | ------------------ |
| タスク一覧を表示  | GET /todos         |
| 新しいタスク追加  | POST /todos        |
| 完了チェックを切替 | PUT /todos/{id}    |
| 削除ボタン     | DELETE /todos/{id} |

> `requests` ライブラリを使用して API と通信すること

#### 注意事項

* Streamlit だけで ToDo を管理 **することはNG**で、必ず **FastAPI にリクエストして操作する**こと

##  **動作確認の提出**

レポートに以下の内容をまとめて提出すること：

### 提出レポート内容

| 番号 | 記載内容                                         |
| -- | -------------------------------------------- |
| 1  | 目的（APIとは何か、今回の学習目的）                          |
| 2  | API設計（エンドポイント一覧表の提出）                         |
| 3  | FastAPI のコード（主要部分のみ）                         |
| 4  | OpenAPI での動作確認スクリーンショット（POST/GET/PUT/DELETE） |
| 5  | Streamlit 画面のスクリーンショット                       |
| 6  | Streamlit と FastAPI が通信していた証拠（サーバログでも可）      |
| 7  | 学習したこと・感想（最低100文字）                           |

##  **評価基準（80点満点）**

| 評価項目              | 点数 |
| ----------------- | -: |
| API 設計（エンドポイント仕様） | 15 |
| FastAPI の実装と動作    | 25 |
| Streamlit との通信・画面 | 25 |
| レポートの品質（スクショ＋説明）  | 15 |

## **ヒント（任意）**

* `pydantic` で入力データ（POST用）を定義
* Streamlit では `st.button`, `st.checkbox`, `st.text_input` 
* FastAPI の CORS を有効にすると安定

```python
  from fastapi.middleware.cors import CORSMiddleware
  app.add_middleware(
      CORSMiddleware,
      allow_origins=["*"],
      allow_methods=["*"],
      allow_headers=["*"],
  )
```

# チャレンジ加点要素： **加点ポイント（+20点）**

**SQLite + SQLAlchemy を導入すると加点**になる

以下のいずれか、または複数に取り組んだ場合に最大 20 点を加点する。

| 加点内容                                           | 点数 |
| ---------------------------------------------- | -: |
| SQLiteを導入し、データを永続化する                           | +8 |
| SQLAlchemy ORMを使用してモデル定義・クエリ実装する               | +8 |
| `id` を SQLite の AutoIncrement にし、API側で採番管理をしない | +4 |

> 仕様は「データが永続化される以外は同じ」、実装難易度に応じて部分加点あり


###  実行方法

**必要なパッケージのインストール**
(参考)　自ら詳しく調べること

requirements.txt

```
fastapi
uvicorn
pydantic
pandas
streamlit
requests
sqlalchemy
```
```bash
$ python3 -m venv venv
$ source venv/bin/activate
$ pip3 install update pip
$ pip3 install --upgrade pip
$ pip3 install -r requirements.txt

```

| 操作             | コマンド                         |
| -------------- | ---------------------------- |
| FastAPI サーバ起動 | `uvicorn main:app --reload`  |
| Streamlit 起動   | `streamlit run app.py`       |
| OpenAPIドキュメント  | `http://127.0.0.1:8000/docs` |

### 提出レポートに追記する項目（SQLite導入者）

| 内容         | 記述例                   |
| ---------- | --------------------- |
| DB採用理由     | なぜ永続化が必要か             |
| ER図（簡単でOK） | `Todo(id,title,done)` |
| ORMを使う利点   | 型安全、SQL不要、保守性向上       |


### 参考URL

FastAPI, Streamlit, SQLAlchemy関連の**公式サイト**と**初心者向けのわかりやすい技術解説サイト**

###  **公式サイト**

1.  **FastAPI**  
    <https://fastapi.tiangolo.com/ja/>  
    → Pythonで高速なWeb APIを構築するためのモダンなフレームワーク。型ヒント、非同期処理、Swagger UI対応などが特徴。 [\[fastapi.tiangolo.com\]](https://fastapi.tiangolo.com/ja/)

2.  **Streamlit**  
    <https://streamlit.io/>  
    → データアプリやダッシュボードをPythonだけで簡単に作れるフレームワーク。HTMLやJS不要で、数行コードでWebアプリ化可能。 [\[streamlit.io\]](https://streamlit.io/)

3.  **SQLAlchemy**  
    <https://www.sqlalchemy.org/>  
    → Python用の強力なORM（Object Relational Mapper）とSQLツールキット。データベース操作をPythonicに記述可能。 [\[sqlalchemy.org\]](https://www.sqlalchemy.org/)


#### *おすすめ学習順序**

1.  **APIの基礎** → 上記Zenn記事で「APIとは？」を理解
2.  **FastAPI** → PythonでAPI構築を体験
3.  **Streamlit** → データ可視化やダッシュボードを作成
4.  **SQLAlchemy** → データベース連携を学習
### **わかりやすい技術解説サイト**

*   **FastAPI入門記事（Qiita）**  
    [FastAPIの使い方（Python初心者向け）](https://qiita.com/Hashimoto-Noriaki/items/6dbefe8068dbfe2c236d)  
    → 型ヒント、ルーティング、Swagger UIの自動生成など、基本から丁寧に解説。 [\[qiita.com\]](https://qiita.com/Hashimoto-Noriaki/items/6dbefe8068dbfe2c236d)

*   **Streamlit入門記事（Zenn）**  
    [【Streamlit入門】爆速でWEBアプリを作ろう](https://zenn.dev/upgradetech/articles/8d81f8a8df88cc)  
    → インストールからUI要素、データ可視化まで、初心者でもすぐ試せる内容。 [\[zenn.dev\]](https://zenn.dev/upgradetech/articles/8d81f8a8df88cc)

*   **SQLAlchemy基本解説（Qiita）**  
    [SQLAlchemyの基本的な使い方](https://qiita.com/arkuchy/items/75799665acd09520bed2)  
    → ORMの概念、モデル定義、セッション管理などをわかりやすく説明。 [\[qiita.com\]](https://qiita.com/arkuchy/items/75799665acd09520bed2)

*   **APIの基礎解説（Zenn）**  
    [【初心者向け】APIとは？使い方と実装方法をわかりやすく解説](https://zenn.dev/homatsu_tech/articles/d664a65b776efe)  
    → APIの仕組み、REST APIの基本、JavaScriptやExpressでの実装例あり。 [\[zenn.dev\]](https://zenn.dev/homatsu_tech/articles/d664a65b776efe)




https://github.com/rhoboro/mywallets-api
