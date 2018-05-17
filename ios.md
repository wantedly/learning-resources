iOS
===========

プログラミング経験があり、これからiOSアプリ開発にチャレンジするエンジニアが、効率良く情報を得るために参考になりそうなリンク集。

## 情報収集

基本的に毎週更新されるサイトを見ておけば良い。これらのサイトを起点にして、気になる開発者が発信している情報を見に行ったり、ブログをRSSリーダーに突っ込んだりして観測範囲を広げていくのがおすすめ。

- [iOS Goodies](http://ios-goodies.com/) これが一番シンプルで見やすい。
- [this week in Swift](https://swiftnews.curated.co/) 知名度の高いエンジニアが発信している。2017年11月を最後に更新停止中。
- [Swift Weekly Brief](https://swiftweekly.github.io/) Swift の開発状況に詳しい。


## 学習コンテンツ

- [Design+Code](https://designcode.io/) iOSアプリ開発におけるデザインと実装の両面を学べる。デザインも含めてまるっと自分でアプリをつくれるようになるまで到達したい人におすすめ。
- [raywenderlich.com](https://www.raywenderlich.com/) 様々なトピックを扱っている。動画コンテンツの配信や書籍の出版も行なっている。初心者向けのコンテンツも多い。
- [NSScreencast](https://nsscreencast.com/episodes) 動画で学べる。エピソードごとにソースコードも付いている。良質なコンテンツが多い。
- [Realm Academy](https://academy.realm.io/section/apple/) ([日本語動画](https://academy.realm.io/jp/section/apple/)) Realm が発信している。カンファレンスの発表などを記事にしたコンテンツが多い。中級者向けのトピックが多い。
- [objc](https://www.objc.io/issues/) 中級~上級者向けの話題を扱う。Objective-C が主流だった時代に実装のベストプラクティスや応用技術について考察して発信していたサイト。最近は書籍の出版やインタビュー動画の配信を行なっている。

## 書籍

https://itunes.apple.com/book/id881256329
Apple 公式。Swift の文法を手早く把握したい人向け。iBooks で読むと読みやすいのでおすすめ。


https://www.objc.io/books/
https://store.raywenderlich.com/products
洋書であれば、この辺りで探すのがおすすめ。

https://store.raywenderlich.com/products/rxswift
特に RxSwift について学ぶ必要がある人はこれ。体系的にまとまってる書籍はこれくらい。

http://gihyo.jp/book/2017/978-4-7741-8730-3
和書は詳しくないけど、これとか良いかも。ジェネリクスとか中級者向けの内容も含んでいる。

http://amzn.asia/ifcRkeT
Auto Layout を手早くキャッチアップしたいなら、これとか良いはず。


## 便利ツール

https://wwdc.io/
WWDCのセッションの動画を試聴するにはこのアプリを使うのが良い。技術レベルの高いエンジニアほど、WWDCのセッションの内容をしっかり確認している印象がある。自分の関心のある分野から重点的に観ていくと良い。

https://github.com/jfahrenkrug/WWDC-Downloader
WWDCのセッションのサンプルコードを一括ダウンロードできる。

https://github.com/KrauseFx/xcode-install
AppStore から Xcode をインストールすると意図しないタイミングでアップデートしてしまうことがある。特定のバージョンの Xcode をインストールするのに利用すると良い。

https://github.com/facebook/chisel
Xcode のコンソールを利用して様々なデバッグ操作ができる。view のデバッグに用いることが多いが、最近は Xcode にviewのデバッグ機能が登場して利用機会が少し減ったかも。多機能で様々な用途があるので入れておいた方が良い。

http://nshipster.com/network-link-conditioner/
通信速度が遅い状況などを再現できる。通信エラー時の問題などのデバッグに用いることがある。※リンク先はツールの紹介記事

https://kapeli.com/dash
Apple のドキュメントを参照するのに便利。CocoaPodsに対応したライブラリのドキュメントも一括管理できたりもする。

## ライブラリ集

https://swift.libhunt.com/
おおよその人気度合いがわかったり、類似のライブラリの発見や比較ができる。カテゴリー別に有名どころがわかったりする。情報が多いので導入するかどうかの判断材料を集めやすい。

https://github.com/vsouza/awesome-ios
https://github.com/matteocrippa/awesome-swift
こういった情報でざっくり探すのも良いかも。

## カンファレンス

最近は、国内でもカンファレンスが盛ん。

https://www.tryswift.co/
https://iosdc.jp
いくつかは定期的に開催されている。

https://academy.realm.io/jp/section/apple/
https://www.youtube.com/channel/UCF-W8FRL7d_9konHA9eNObA
try! Swift の登壇内容は Realm のブログを見に行くと内容を見ることができる。iOSDC の登壇内容は動画が公開されている。他にも個人で内容をまとめたブログが数多く公開されているので探してみると良い。

## その他

### アプリ実装

https://github.com/dkhamsing/open-source-ios-apps
実装が公開されているアプリは、設計の参考になることが多い。いろいろなアプリの実装に目を通して引き出しを増やしておくと良い。

https://github.com/artsy/eigen
https://github.com/artsy/eidolon
https://github.com/devxoul/Drrrible
https://github.com/kickstarter/ios-oss

### 企業

https://github.com/artsy
http://artsy.github.io
個人的にモダンな開発スタイルを取り入れる目的でよく参考にしている。CocoaPods などのコミッターも在籍している。先進的な開発をしていて、オープンな場で開発している。参考になるリポジトリが多い。技術ブログで情報発信もしている。

https://github.com/Ramotion
凝った UI の実装を数多く公開している。インタラクティブなアニメーションの実装ができるようになりたいときは参考にしてみても良いかも。

