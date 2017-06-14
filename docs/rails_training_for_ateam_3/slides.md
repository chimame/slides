## Rails勉強会 #3

rito

2017/06/14

---

### この会の目的
- - -
- Railsの知識を少しでも深めて業務に役立てよう
- チームおよび職種の枠を超えた相談を気軽に行おう

次回以降はリクエストがあればリクエスト内容をやります :smile:

---

### 今回の内容
ルーティング
- - -
要望があったので今回はルーティングについて行います。

---
### Railsルーター（ルーティング）の役割
 :exclamation: URLからコントローラおよびアクションを割り当てる :exclamation:
- - -
GET /parents/13 #=> ParentsController#show id: 13

---
### ルーティングの基本
Railsルーターの基本はRESTfulです
- - -
以下の記述をconfig/routes.rbに追記して確認(`bundle exec rails routes`)して確認しましょう
```ruby
#config/routes.rb
Rails.application.routes.draw do
  resources :books
end
```

---
### routes.rbのテスト
もちろん、今作成したroutes.rbのテストコードも作成することができます
（が、自分は殆ど作ることはありません :pensive: ）

- - -
実際に動くものの方がイメージがつきやすので、以下のコマンドを実行
```shell
bin/rails g scaffold_controller book title:string sub_title:string author:string release_date:date price:integer
```

作成された `spec/routing/books_routing_spec.rb` を見てみましょう

---
### routes.rbの色々な書き方
では以下のようなroutes.rbが書かれている場合のテストはどうなりますか？ :thinking:

- - -
```ruby
# config/routes.rb
Rails.application.routes.draw do
  resources :books do
    resources :rental_histories do
      collection do
        get 'months/(:current_month)', action: :months, as: :months
      end
    end

    member do
      post :new_confirm
    end
  end

  namespace :api do
    resources :books
  end

  scope '/admin' do
    resources :rental_histries
  end
end
```
実際にテストを作ってみて下さい
（Controllerはカラでいいので作成して下さい）

---
### ネストが長いURL
ここからは上記が終わった方向け
先程の例で`rental_histories`は常に`books`が付くので長い :cry:

- - -
なので `shallow: true` を付けると、、、？

---
### テストの修正
`shallow: true` を付ければテストが失敗するので、修正しましょう

---
### 本日はこれで終了です
 :clap: お疲れ様でした :clap:
