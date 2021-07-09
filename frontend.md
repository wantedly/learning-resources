フロントエンド
=============

## 技術スタック

以下がメインで使われています。

- [React](https://ja.reactjs.org/docs/)
- [TypeScript](https://www.typescriptlang.org/)
- [GraphQL](https://graphql.org/)
  - [Nexus](https://github.com/graphql-nexus/nexus) (BFF Server)
  - [Apollo Client](https://www.apollographql.com/docs/react/)

また、一部の古いページには、Haml, JavaScript, Angular が用いられています。

## 参考リンク

開発の際の参考にすると良いリファレンス

### React

- [React ドキュメント](https://ja.reactjs.org/docs) 以下の章は特にお勧めの章です。
  - [フックの導入](https://ja.reactjs.org/docs/hooks-intro.html)
  - [Reactの流儀](https://ja.reactjs.org/docs/thinking-in-react.html)
- [Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0) 設計の考え方として参考にしています。
- [Storybook](https://storybook.js.org/) コンポーネント開発にはStorybookを用いています。
### BFF

- [フロントエンドに型の秩序を与えるGraphQLとTypeScript](https://www.wantedly.com/companies/wantedly/post_articles/183567) BFFによるスキーマファーストな開発を行なっています。
- [Web API に秩序を与える Protocol Buffers](https://speakerdeck.com/south37/protocol-buffers-for-web-api-number-builderscon) BFFより裏側の Web API のスキーマ管理には Protocol Buffers を使用しています。

### Design Syetem

- [React でデザインシステムを正しく実装する - コンポーネントカタログを超えて](https://www.wantedly.com/companies/wantedly/post_articles/302873)
- [Wantedly UI Components](https://www.figma.com/community/file/994992887565225147)

### その他

- [frolint](https://github.com/wantedly/frolint) Wantedly共通のLint設定が含まれています。
