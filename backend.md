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

内部で使っているもので事前にある程度学んでおくと良いものは以下です。

- ORマッパー [SQLBoiler](https://github.com/volatiletech/sqlboiler)
- Redis クライアント [redigo](https://github.com/gomodule/redigo)
- [Google の API Design Guilde](https://cloud.google.com/apis/design/)
- エラーハンドリングのやりかた :point_right: [\`Wrap(err)\` in production - Speaker Deck](https://speakerdeck.com/izumin5210/wrap-err-in-production)


[WIP]

## Python

Wantedlyでは自然言語処理や機械学習のためのサーバにPythonを使うことがあります。

基本的にPythonはRestfulなサーバーよりも特定の機能を持ったシンプルなサーバーを作ることが多いので、サーバーのフレームワークとしてはTornadoを採用しています。
シンプルさと、ある程度肥大化した場合の機能も備えている絶妙なバランスと言う判断です。

### Tornado

Pythonの殆どのアプリケーションロジックはTornadoを使ってAPI化されています。

- http://www.tornadoweb.org/en/stable/
