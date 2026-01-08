# Next15 + prisma + supabase でSNSサービスを作って公開した

**投稿日:** 2024年11月26日

**更新日:** 2024年11月26日

**著者:** [@daichi2007](https://qiita.com/daichi2007)

**タグ:** `Next.js`, `prisma`, `Supabase`, `個人開発`

---

## はじめに

今回は初めてNext.jsを使ったWebサービスを公開しました。Next.jsのモダンな機能をたくさん使った実装になっていますので、それらの実装や開発した経験について紹介します。

## 自己紹介

2007年生まれの17歳です。高校一年生の途中で高校を中退してから１年半ほどアルバイトでシステム開発をしながら個人開発をしています。

## サービスの内容

XやInstagramの機能、デザインを参考に、投稿やいいね、コメントなど基本的な機能のみを実装しました。

**デモ用ログイン情報:**

* **email:** `demo@example.com`
* **password:** `password`

## なぜSNSを題材にしたのか

* いいねやフォローなど様々な細かいDB操作を含む機能が多く、クライアントからサーバーまでフルスタックに実装する経験を得られる。
* 日常的によく利用するXやInstagramなどから設計のヒントやアイデアの着想を得やすい。
* 実際に自分で使ったり友人に使ってもらいやすく、それらによって様々な改善すべき点を得られる。

## 使用技術とそれらを採用した理由

* **Next.js 15 / React 19**
* **Prisma (ORM)**
* **TailwindCSS**
* UIコンポーネントライブラリの使用も検討したが、自作でスタイルや動作を実装する経験を積みたいと思い採用。


* **Supabase (DB, Auth, Storage)**
* Firebaseを検討していたが、わかりやすいドキュメントとシンプルな認証システムに魅力を感じ採用。


* **Vercel**: ホスティング
* **tailwind-variants**
* **sharp**: 画像処理
* **zod**: フォームバリデーション
* **qrcode**: 「プロフィールをシェア」機能でのQRコード生成
* **linkify**: 投稿テキスト内のURLをリンクに変換
* **eslint / prettier**

[👉 GitHubリポジトリ](https://github.com/okmr2217/imageable)（※リンク先は記事内の情報を参照）

## Next15 AppRouter での設計

### データの取得（投稿データの取得やプロフィール情報の取得）

すべて **Server Component** で行い、Client Component に Props として渡す設計にしました。

### データの操作（投稿やいいね、フォローなどの操作）

いいねやフォローなどUIの変化を含むインタラクティブなものは、Client Component から **Server Actions** を呼び出す形で実装しました。なるべく React 19 の `useActionState` を利用しています。

### モーダルをサーバーコンポーネントで実装する

Next.js の **Parallel Routes** と **Intercepting Routes** を利用しました。これによりモーダルを開くとURLが変化し、Server Component でデータの取得を行うことが可能になりました。

## 開発を通して感じたこと

* Server Component や Server Actions の登場により、Laravel や Rails などで MPA を作る場合と似たような開発の流れになってきていると感じました。
* Prisma や Supabase など Node.js 界隈のコミュニティは非常に活発で、盛り上がりを実感しました。
* Next.js では DB 操作から Client Component まで全てに型情報がつき、`prisma.schema` でのテーブル定義を末端まで渡せるのは非常に開発体験が良く、開発スピードを速める要因になると感じました。

## おわりに

SNSサービスという特性上、通知や画像の参照などOS依存の操作が多くなるため、やはりスマホアプリとしての開発もしてみたいと思いました。
