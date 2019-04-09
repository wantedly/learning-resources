サーバサイド
===========

## Ruby on Rails

Wantedlyの本体アプリケーションはRuby on Railsで書かれています。
Railsのコンセプトを理解して、最低限のアプリを書けるようになりましょう。

- [Rails Tutorial](https://www.railstutorial.org/book) 定番Railsチュートリアル。しっかり読み込むよりも、最初は一通り流すことを重視したほうがよい。[日本語訳](http://railstutorial.jp/)
- [Ruby on Rails Guides](http://guides.rubyonrails.org/) Rails公式のドキュメント。ベストプラクティスが一通り学べる。Rails Tutorialを一通りやったあとぐらいに読むとRailsの理解が深まる。
- [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) & [Rails Style Guide](https://github.com/bbatsov/rails-style-guide) Wantedlyは大枠でこのstyle guidesに従っています。

ブックマークしておくと良いリファレンス

- [Ruby Core API & Standard Library API](http://ruby-doc.org/) Rubyと標準ライブラリのドキュメント
- [Ruby on Rails Documentation](http://api.rubyonrails.org/) RailsのAPIドキュメント
- [RSpec](https://www.relishapp.com/rspec) テストフレームワークであるRSpecのドキュメント
- [Better Specs](http://betterspecs.org) より良いRSpecを書くためのガイドライン
- [Everyday Rails - RSpecによるRailsテスト入門](https://leanpub.com/everydayrailsrspec-jp/read) RailsのためのRSpecとしてステップ・バイ・ステップで説明されているので入門に適した一冊


### 参考リンク

- [rails開発に加わる前に学んで欲しいこと](http://qiita.com/reikubonaga/items/60b4f6ee0a86ed06e83b)
- [Rubyはじめての人がRails開発に参加するときに最初に知っておくべきこと](http://qiita.com/awakia/items/42525adb473c7cc6b811)
- [Ruby/Railsチェックポイント](http://qiita.com/awakia/items/ea81e2da242e8e28dec6)


## Golang

WantedlyではAPIサーバにGo言語を使うことがあります。

### grapi

Golangのほとんどのアプリケーションは grapi を利用し gRPC + grpc-gateway で実装されています。
- https://github.com/izumin5210/grapi
- Go Conference での発表資料
  - [grapi: Bulding JSON API server with grpc-gateway for microservices - Speaker Deck](https://speakerdeck.com/izumin5210/grapi-bulding-json-api-server-with-grpc-gateway-for-microservices)


### よく使うパッケージ・ツール・フレームワーク

- フレームワーク
    - Web framework : [grapi](https://github.com/izumin5210/grapi)
    - Pubsub worker : [subee](https://github.com/wantedly/subee)
- ミドルウェアのクライアント
    - RDB の ORM : [SQLBoiler](https://github.com/volatiletech/sqlboiler)
    - Redis クライアント : [redigo](https://github.com/gomodule/redigo)
- テスト
    - オブジェクト比較 : [github.com/google/go-cmp](https://github.com/google/go-cmp)
    - モック  : [gomock & mockgen](https://github.com/golang/mock)
    - See also
        - [Advanced Testing with Go - Speaker Deck](https://speakerdeck.com/mitchellh/advanced-testing-with-go)
        - [Tips for develoepr-friendly testing #golangtokyo - Speaker Deck](https://speakerdeck.com/izumin5210/tips-for-develoepr-friendly-testing-number-golangtokyo)
- ツール
    - `.env` : [direnv](https://github.com/direnv/direnv)
        - See also [基本セット - Create a new application with Golang](./new-app.md#%E5%9F%BA%E6%9C%AC%E3%82%BB%E3%83%83%E3%83%88)
    - ツール管理 : [gex](https://github.com/izumin5210/gex)
    - Lint
        - See also [Lint & eviewdog - Create a new application with Golang](https://github.com/wantedly/dev-docs/blob/master/go/new-app.md#lint--reviewdog)
        - [Reviewdog](https://github.com/reviewdog/reviewdog)
        - [golangci-lint](https://github.com/golangci/golangci-lint)
        - [wraperr](https://github.com/srvc/wraperr)
- その他
    - エラーハンドリング : [github.com/srvc/fail](https://github.com/srvc/fail)
        - See also [\`Wrap(err)\` in production - Speaker Deck](https://speakerdeck.com/izumin5210/wrap-err-in-production)
    - DI : [github.com/google/wire](https://github.com/google/wire)
        - See also [google/wireを使ったDIとDI関数のシグネチャについて #go - My External Storage](https://budougumi0617.github.io/2018/12/14/how-to-use-google-wire/)



[WIP]

## Python

Wantedlyでは自然言語処理や機械学習のためのサーバにPythonを使うことがあります。

基本的にPythonはRestfulなサーバーよりも特定の機能を持ったシンプルなサーバーを作ることが多いので、サーバーのフレームワークとしてはTornadoを採用しています。
シンプルさと、ある程度肥大化した場合の機能も備えている絶妙なバランスと言う判断です。

### Tornado

Pythonの殆どのアプリケーションロジックはTornadoを使ってAPI化されています。

- http://www.tornadoweb.org/en/stable/
