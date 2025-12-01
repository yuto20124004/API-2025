##  API実習　2025　課題レポート（第1回）修正版

####  ドラフト修正箇所
*  SheetDB無償APIの範囲内で、PATCH操作（部分更新）に修正、動作確認
*  REST4原則のチェックリストを教材テキストと整合


###  出題範囲：　API実習2025　第1回～第3回まで

###  提出期限：　2025/12/2(火) 17:00

###  提出方法：

- Githubアカウントの作成
- Githubアカウントの通知：FORMSで回答する：　**https://forms.office.com/r/CL1s98xPes**
- プライベートリポジトリの作成
- プライベートリポジトリへ、``keythrive`` を招待し承諾を得る
- **11/30までにここまで実施**する
- 課題に取り組む： Python環境**Colaboratory, Jupyter，VSCode**などで**コード記述**し，**必ず実行動作確認**する
- 課題の回答，レポートは，本マークダウンファイル（WebClassからダウンロード）を書き換えて，**自分の言葉で記述すること**
- ファイル名はそのままでよい。提出者はアカウントで特定可能
- **生成AIの回答，他学生のレポート内容をコピー＆ペーストしてはいけません**（明らかに不正行為で，自分の成長を妨げる弊害です）
- わからない問題は，進んでいる友達，学習支援センター，教員に質問して，必ず自分の理解とスキルにつなぐこと
- **考え方や不明な点を生成AIに質問して、回答そのものをもらうのではなく、考え方のヒントを聞いて、しっかり自分の中に消化吸収することは許容範囲内**
- 
- 各自のGithubのプライベートリポジトリ: https://github.com/アカウント/API-2025/report-01/ に、作成した課題レポートファイル一式をアップロード(push)、**必ずコミット**する
- 提出期限まで、ファイルの差し替え・アップデートは自由に可能
- 提出期限を過ぎたら、教員が自動取得する（**〆切を過ぎたら、差し替えできません**）

#####  指導教員：　情報学部　堀川

-------

レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
|B|20124004 | 井越悠斗 |


------

## 目次

## **SheetDB CRUD演習用課題レポート（11項目）**

GoogleスプレッドシートをAPI化し、SheetDBでCRUD操作を学ぶための演習課題

***

### **課題テーマ：Googleスプレッドシートをデータベースとして扱うAPI演習**

#### **前提条件**

*   Googleスプレッドシートを作成（1行目にカラム名：`id`, `name`, `email`, `score`）
*   **適当にダミーの成績データを登録する（実際の個人情報は使わない）**
*   SheetDBでAPIを作成し、エンドポイントを取得（例：`https://sheetdb.io/api/v1/XXXXXX`）
*   PostmanまたはcURLでAPIを操作して動作確認、期待した動きかどうか説明
*   更新系は、SheetDBスプレッドシート本体にデータが追加されたことを確認
*   動作確認の証跡としてスクリーンキャプチャを貼付


####  ドラフト修正箇所

*  PUT（完全更新）と PATCH（部分更新）は有償プランが必要なため、この課題から除外
  

***

### **課題一覧（10項目）**

1.  **APIエンドポイント確認**
    *   SheetDBで作成したAPIのURLを確認し、ブラウザでアクセスしてJSONレスポンスを表示

2.  **READ操作（GET）**
    *   全データを取得するGETリクエストをPostmanで送信。
    *   クエリパラメータ `limit` と `offset` を使ってページネーションの動作確認を実施
<img width="1408" height="869" alt="スクリーンショット 2025-12-01 131023" src="https://github.com/user-attachments/assets/11f67ada-8735-40ec-a6f7-849c67308859" />

3.  **条件検索（GET with Query）**
    *   `name` が「田中」のレコードだけ取得するGETリクエストを実行
<img width="1414" height="729" alt="スクリーンショット 2025-12-01 131345" src="https://github.com/user-attachments/assets/ea6fe1cb-c4be-4229-a7ff-d180cfdceb96" />

4.  **CREATE操作（POST）**
    *   新しいレコード（例：`id=101, name=田中, email=test@example.com, score=85`）を追加
<img width="1430" height="591" alt="スクリーンショット 2025-12-01 131455" src="https://github.com/user-attachments/assets/e66f97ed-0846-49b1-8aff-e18077ed3a34" />

5.  **複数レコード追加（POST）**
    *   `data` 配列で複数レコードを一度に追加する。
<img width="1413" height="666" alt="スクリーンショット 2025-12-01 131530" src="https://github.com/user-attachments/assets/e1319b0c-3e73-4daf-a932-9e975c397933" />

6.  **DELETE操作**
    *   `id=101` のレコードを削除するDELETEリクエストを送信
<img width="1411" height="592" alt="スクリーンショット 2025-12-01 131612" src="https://github.com/user-attachments/assets/8eb91b58-5c6b-42fd-b69b-c12be7581cc6" />

7.  **認証設定**
    *   SheetDBの管理画面でBasic認証を設定し、Postmanで認証付きリクエストを送信
<img width="1416" height="307" alt="スクリーンショット 2025-12-01 131703" src="https://github.com/user-attachments/assets/fad7bce7-7f3a-415b-849d-fd068eaed69e" />
<img width="1414" height="373" alt="スクリーンショット 2025-12-01 131741" src="https://github.com/user-attachments/assets/af423144-60a6-4e4c-89f1-2b79474ee663" />

8. **エラーハンドリング**
    *   存在しない `id` を指定してDELETEを実行し、レスポンスのエラー内容を確認
<img width="1405" height="600" alt="スクリーンショット 2025-12-01 131833" src="https://github.com/user-attachments/assets/61cbae6a-e227-4516-a43d-f168b7442f7a" />

9. **PATCH操作（部分更新）** **修正課題**
    SheetDB無償API利用範囲で、適切なPATCH操作を行い、特定のデータを部分更新し、レスポンスを確認する：
    * エンドポイント：　https://sheetdb.io/api/v1/XXXXXX/id/23`
    * ヘッダ：　Content-Type: application/json
    * ボディ(raw json) ：
     { 
        "email": "foo@bar.baz",
    }
    * レスポンス：　HTTPステイタスコード：　200 OK
　　* curlコマンドでの動作確認も可能
<img width="1411" height="477" alt="スクリーンショット 2025-12-01 131919" src="https://github.com/user-attachments/assets/eddede9f-15d8-4535-97f9-6d0c9fa82111" />
<img width="1416" height="507" alt="スクリーンショット 2025-12-01 131935" src="https://github.com/user-attachments/assets/4117f7d8-9589-419d-8862-5b67dade37cf" />

10. **RESTの4原則対応表**
    * 上記9の設問について、下記の4原則のどれを満たしているかを表にまとめよ：

**対応表**
|番号|アドレス可能性|統一インターフェース|ステートレス|接続性|
|-|-|-|-|-|
|1|〇||||
|2||〇|〇||
|3||〇|〇||
|4||〇|〇||
|5||〇|〇||
|6||〇|〇||
|7|||〇||
|8||〇|〇||
|9||〇|〇||



###### RESTの4原則

1.	アドレス可能性： 情報リソースはURIで一意に特定、規則的に参照
2.	統一インターフェース → HTTPメソッド（Post/Get/Put/Delete）でリソースを操作 
3.	ステートレス → 各リクエストは独立し、サーバは状態をもたない、状態管理しない
4.	接続性：情報と情報を紐付ける情報（XML, HTML, JSON）

***

### **追加チャレンジ**  加点要素とします

*   Postmanの「Tests」タブでレスポンス検証スクリプトを記述
*   JavaScript（axios）でSheetDB APIを呼び出す簡単なWebページを作成

***


