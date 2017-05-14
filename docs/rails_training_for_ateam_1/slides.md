## Rails勉強会 #1

rito

2017/05/XX

---

### この会の目的
- - -
- Railsの知識を少しでも深めて業務に役立てよう
- チームおよび職種の枠を超えた相談を気軽に行おう

次回以降はリクエストがあればリクエスト内容をやります :smile:

---

### 今回の内容
- - -
テストってどうやって書くの？

---
### てことで実際にテストを書いていきましょう

---
### まずは以下のリポジトリをcloneして下さい

```shell
$ git clone https://github.com/chimame/rails_training.git
```

---
### Bookモデルを作成してあります。
軽くモデルの中身を説明します。

---
### テスト環境の構築

```shell
$ rails g rspec:install
```

---
### Bookモデルのfull_titleのテストを追加
- - -
`spec/models/book_spec.rb`を作成
```ruby
require 'rails_helper'

RSpec.describe Book, type: :model do
  describe '#full_title' do
    let(:book) { Book.new(title: title, sub_title: sub_title) }
    let(:title) { 'D・N・A2' }
    subject { book.full_title }

    context 'sub_titleがない場合' do
      let(:sub_title) { nil }
      it { is_expected.to eq 'D・N・A2 - ' }
    end
    
    context 'sub_titleがある場合' do
      let(:sub_title) { '何処かで失くしたあいつのアイツ' }
      example 'タイトルとサブタイトルが結合されること' do
        expect(book.full_title).to eq 'D・N・A2 - 何処かで失くしたあいつのアイツ'
      end
    end
  end
end
```

---
### テストを実行してみよう

```shell
bundle exec rspec
```

---
### 次は自分でテストを作成してみましょう
- - -
`calculate_loan_charge_from` メソッドの
テストを作成してみて下さい :pencil:

ちなみにわざとテストしにくいコードで書いています :stuck_out_tongue_winking_eye:

---
### 本日はこれで終了です
 :clap: お疲れ様でした :clap: