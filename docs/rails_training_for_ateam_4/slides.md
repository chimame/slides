## Rails勉強会 #4

rito

2017/07/12

---

### この会の目的
- - -
- Railsの知識を少しでも深めて業務に役立てよう
- チームおよび職種の枠を超えた相談を気軽に行おう

次回以降はリクエストがあればリクエスト内容をやります :smile:

---

### 今回の内容
コントローラ
- - -
みんな大好きなコントローラです！

---
### コントローラって何？
質問です。
- - -
- MVCデザインパターンというのをご存知ですか？
- それぞれの役割は知っていますか？

---
### コントローラの役割
コントローラの役割は以下です。
- - -
1. ユーザからの入力値を受け取る
2. モデルに対して加工命令を出す ← **超重要**
3. ユーザにデータ（View）とステータス（http status）を返す
4. ユーザ特有のデータ（Session,Cookie）を管理する

これだけです。
これ以上のことはコントローラではしないで下さい。
（切実なお願い）

---
### コントローラのテスト
テストする場合も役割だけをテストします。
- - -
1. 入力値はテスト時に渡す
2. expect{ post :create, id: @book.id }.to change(Book, :count).by(1)
  ただし、データ取得処理はモック
3. expect(response.status).to eq(200)
  expect(response).to render_template template
  expect(response).to redirect_to author_path
4. expect(session[:hoge]).to eq :fuga

---
### books_controllerのテスト作成
generatorで作成されたテストは正常終了していません
- - -
ですので、以下のコマンドが正常に終了するように直してみましょう
```shell
$ bundle exec rspec spec/controllers/books_controller.rb
```

---
### ハンズオン
以下の仕様となるようにbooks_controllerやviewに処理を追加して下さい。
- - -
1. showアクションが呼ばれる度に表示されたbookのidを記憶
2. 記憶しているidが表示するbookと異なればpriceの差を表示
3. 記憶しているidがない場合や同一の場合は表示しない

もちろんテストも作成して下さい

---
### 本日はこれで終了です
 :clap: お疲れ様でした :clap:
