# 回答用紙 （学生用）

(本Markdownファイルを記入し、課題を完成、提出すること)

##  API実習　2025　課題レポート（第3回）

**API 実習課題**: FastAPI + Streamlit + OpenAPIドキュメントの「設計」「実装」「動作確認」

###  出題範囲：　API実習2025　第7回～第9回まで

###  提出期限：　2025/12/23(火) 17:00

-------

レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
|B| 20124004 |  井越　悠斗 |


# 　**ToDo メモ管理 API 実習レポート（FastAPI / Streamlit）**

## 1. 実習の目的

（※ APIとは何か？今回の授業で学ぶことを100～200字程度で記述）

> **記入欄：**
APIとは、プログラム同士が安全に会話するための共通ルール。  
今回の授業ではHTTPプロトコルを介してアプリケーション間でデータや機能をやり取りするためのインターフェースWebAPIの基本概念やリソース設計やバージョングのRESTfulAPIやスキーマ定義やDataLoaderのGraphQLAPI、型安全性やエンドツール統合のtRPCAPI設計、設計変更しやすいAPIやAPIをバージョンで管理するということを学ぶ。
> 
---

## 2. API 設計（エンドポイント仕様）

| メソッド   | パス          | 内容 | リクエスト例 | レスポンス例 |  
| ------ | ----------- | ------ | ------ |　------　|  
| GET    | /todos      |    リソースの取得    |    GET /todos    |　200 OK {"id":1,"title":"勉強"}　|  
| POST   | /todos      |    リソースの作成    |    POST /todos {"title":"バイト"}    |　201 Created {"id":2, "title":"バイト"}　|  
| PUT    | /todos/{id} |    リソースの完全置換    |    PUT /todos/1 {"title":"勉強"}|　200 OK {"id":1, "title":"勉強"}　|  
| DELETE | /todos/{id} |    リソースの削除    |    DELETE /todos/2    |　204 No Content　|  

> ※ 例を JSON 形式で記載
> **記入欄：**



## 3. 使用した技術構成（選択した項目に ✓）

| 使用技術            |  使用 | 備考（任意） |  
| --------------- | :-: | ------ |  
| FastAPI         | [✓] |        |  
| Streamlit       | [✓] |        |  
| SQLite（DB 永続化）  | [✓] |        |  
| SQLAlchemy（ORM） | [✓] |        |  
| そのほか            | [ ] |        |  

> ※ SQLite / SQLAlchemy を使用した場合は後半の加点欄も記入

---

## 4. FastAPI コード（主要部分のみ抜粋）

（※ スクリーンショット不可。**テキストで貼り付ける**）

```python
# FastAPI の主要コードをここに貼る

from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from typing import List

app = FastAPI()


class Todo(BaseModel):
    id: int
    title: str
    done: bool

class TodoCreate(BaseModel):
    title: str

class TodoUpdate(BaseModel):
    done: bool


todos: List[Todo] = [ {
                        "id":1,
                        "title":"勉強",
                        "done":False
                      },
                      {
                        "id":2,
                        "title":"バイト",
                        "done":False
                      },
                      {
                        "id":3,
                        "title":"課題",
                        "done":False
                      },
                    ]
next_id = 0

@app.get("/todos", response_model=List[Todo])
def Get_todos():
    return todos



@app.post("/todos", response_model=Todo)
def Create_todo(todo_create: TodoCreate):
    global next_id
    todo = Todo(
        id=next_id,
        title=todo_create.title,
        done=False
    )
    todos.append(todo)
    next_id += 1
    return todo



@app.put("/todos/{todo_id}", response_model=Todo)
def Update_todo(todo_id: int, todo_update: TodoUpdate):
    for todo in todos:
        if todo.id == todo_id:
            todo.done = todo_update.done
            return todo
    raise HTTPException(status_code=404, detail="Todo not found")



@app.delete("/todos/{todo_id}")
def Delete_todo(todo_id: int):
    for i, todo in enumerate(todos):
        if todo.id == todo_id:
            todos.pop(i)
            return {"message": "Todo deleted"}
    raise HTTPException(status_code=404, detail="Todo not found")

```

---

## 5. OpenAPI ドキュメント動作確認（スクリーンショット貼付）

| 操作         | 貼付欄 |
| ---------- | --- |
| POST（新規追加） |  <img width="1419" height="911" alt="image" src="https://github.com/user-attachments/assets/e9b8a3b6-9900-40ee-90ff-4594c8582c8b" />  
   <img width="1401" height="603" alt="image" src="https://github.com/user-attachments/assets/cae33ea5-5c31-4d4d-acd6-358338294544" />|
| GET（一覧取得）  |  <img width="1417" height="944" alt="image" src="https://github.com/user-attachments/assets/41a598b7-658f-4e4b-9eda-d9b52485b265" />
<img width="1414" height="300" alt="image" src="https://github.com/user-attachments/assets/1fac23f9-676a-4e41-865d-13fca49d1522" />|
| PUT（更新）    |  <img width="1092" height="833" alt="image" src="https://github.com/user-attachments/assets/1def3930-b2e3-4439-90d9-73c4d00a93b4" />
  <img width="1089" height="770" alt="image" src="https://github.com/user-attachments/assets/8ddbe91e-05f8-4c29-aba5-6237373c8f83" />|
| DELETE（削除） |  <img width="1082" height="633" alt="image" src="https://github.com/user-attachments/assets/80aa2300-6dec-4d0e-b61f-0b3fe8559d54" />
  <img width="1076" height="749" alt="image" src="https://github.com/user-attachments/assets/61e74be0-a304-4772-994f-08dd21647963" />|


---

## 6. Streamlit 画面 UI（スクリーンショット貼付）

| 画面キャプチャ       | 貼付欄 |
| ------------- | --- |
| 実行画面          | <img width="953" height="679" alt="image" src="https://github.com/user-attachments/assets/63ac1449-1c8b-4ad4-acb0-5aa991753469" />
  |
| 操作例（追加・更新・削除） | <img width="781" height="86" alt="image" src="https://github.com/user-attachments/assets/7998615b-9cf8-4699-b4ba-0c615d5b0494" />
   |

---

## 7. API 通信ログ（サーバログ or Web通信キャプチャなど）

サーバーコンソールやログ画面のキャプチャを 1 枚以上添付

| ログ例（貼付欄） |
| -------- |
|   <img width="994" height="149" alt="image" src="https://github.com/user-attachments/assets/9005fc17-bc19-4d47-a843-027cfabfbc06" />
    <img width="619" height="130" alt="image" src="https://github.com/user-attachments/assets/c639c507-b68d-48bf-8bbd-9847b0d1c752" />
|

---

## 8. 学習したこと・感想（100文字以上）

> **記入欄：**
今回の課題を通して、FastAPI と Streamlit を連携させた Web アプリ開発の基礎を学んだ。特に、API 側で状態を正しく保持する重要性や、Streamlit が再描画のたびにコードを再実行する仕組みを理解できたことは大きな学びである。また、OpenAPI やサーバログを用いて通信を確認することで、フロントエンドとバックエンドの責務分離とデバッグの考え方を実践的に身につけることができた。


## チャレンジ課題：  9. SQLite / SQLAlchemy 導入内容

（使用した人のみ記述）

### 9-1. ER図（例：テーブル）

```
# 具体例を書いたり、手書きを撮影して貼っても良い

```

### 9-2. DB を使うメリット

> **記入欄：**

### 9-3. SQLAlchemy を使用した理由

> **記入欄：**


## 10. 参考資料（使用した場合のみ記入）

| 種類     | URL / 書籍名 |
| ------ | --------- |
| Webサイト |           |
| 書籍     |           |
| その他    |           |

**提出前チェックリスト**

* [ ] API のコードを貼った
* [ ] OpenAPI のスクリーンショットを貼った
* [ ] Streamlit UI の画像を貼った
* [ ] 学習したことを 100 字以上書いた
* [ ] SQLite / SQLAlchemy の加点欄（使った場合のみ）











