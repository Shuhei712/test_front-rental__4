# SYMUNITY レンタルカタログシステム

## バージョン管理
|Date|Version|内容|
|:--:|:--:|:---|
|2022/07/20|v1.0.0|レンタルカタログシステム リリース|
|2022/08/17|v1.1.0|・QRコード資料ダウンロードページの追加<br>・スクリーンカテゴリーの追加<br>・機材名と型番をコピー(右クリックできるように変更)|
|2022/08/22|v1.1.1|・掛け率表示の修正<br>・ブレイクポイント(小数点)を追加|
|2023/03/27|v1.1.2|・ファーストビューのデザイン変更|
|2023/06/20|v1.1.3|・ファーストビューのデザイン変更(PickUpの型番)|
|2023/12/22|v1.2.0|・ファーストビューのデザイン・機能変更<br>・機材が見つからない時の404ページ対応<br>・アンカーリンク不具合対応<br>・ローディング消去＆代替の対策|
|2024/03/28|v2.0.0|・会員機能追加
|2024/02/04|v2.0.1|・添付フィールドのUI<br>・検索結果：クエリ追加、ページネーション/パンくず不具合、絞り込みキーワードを×でリセットした際Nullが入る、ページ変更でトップにスクロールしない(FF)<br>・カート：連絡方法 補足・初期値　等
|2024/02/08|v2.0.2|・keyup.enterのブラウザによる挙動の違い対応<br>・支払方法はお客情報に合わせる、/infoに支払方法を表示<br>・注文状況「注文取消し」を赤文字<br>・注文回答欄を出す条件変更　等
|2024/04/30|v2.0.3|・カートの日付選択の再設定<br>・申し込みでレンタルが完了しない旨を強調<br>・過去お取引ありの場合、身分証提出不要　等
|2024/05/08|v2.0.4|・カートの重複警告<br>・お問い合わせ入力項目変更<br>・Twitter→X、営業時間の表記変更
|2024/05/08|v2.0.6|・お問い合わせリンク先を会員は会員フォームに<br>・お問い合わせページに電話追加<br>・営業時間コンポーネント変更<br>・SolidWaterロゴ、Copyright変更　等

### nodejs のバージョン `v16.13.0`

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out the [documentation](https://nuxtjs.org).

## git の運用方法

### 各ブランチについて

```bash
# master：
大元。一番上の親となるブランチ。
本番環境のリソースはこのブランチのリソースと一致する。

# develop：
開発用ブランチ。featureブランチはすべてここにマージされる。
このブランチは複数切らず、案件開始時に一回のみ切るブランチ。

# feature：
各機能ごとに作るブランチ。
よくfutureと間違えて「フューチャー」と読む方がいるが、正しい読み方は「フィーチャー」。
複数切るブランチになるのため「feature/機能名」のようにする。

#release：
リリース用ブランチ。段階リリースを行う場合に作成するブランチ。
複数切るブランチになるため「release/リリース日」のようにする。

#hotfix：
バグ修正用ブランチ。バグ修正が必要になった場合に一時的に作成するブランチ。
複数切るブランチになるため「hotfix/バグ名」のようにする。
```

### 運用手順

```
1. masterからdevelopを切る。
2. developからfeatureを切る。（機能ごとにブランチを切るので、複数のfeatureを切ることがほとんど）
3. feature内で作業し、変更内容をdevelopにマージ。
4. 全てのfeatureをdevelopにマージできたら、developからreleaseを切る。
5. releaseを本番環境にデプロイして、問題が無ければreleaseをmasterにマージ。
6. masterでバージョンのタグを付ける
7. 以降、2番の手順に戻って繰り返し。
```
バグが発生した場合
```
8. 本番運用中にバグが発生した場合は、masterからhotfixを切る。
9. hotfixでバグ修正を行い、hotfixをデプロイ。
10. 問題なければhotfixをmasterにマージ。
11. masterをdevelopにマージ。
12. 次のリリースに向けてmasterからreleaseを切る。

```
## サーバ の運用方法
### 運用手順
#### 本番 (masterで運用)
```
sudo git pull origin master
sudo npm run build
pm2 restart [id]
```
#### 緊急時に元のversionに戻すとき (releaseで運用)
```
sudo git fetch
sudo git checkout -b [branch名] [remote名/branch名]
// release/0000 origin/release/0000
sudo npm run build
pm2 restart [id]
```



## Special Directories

You can create the following extra directories, some of which have special behaviors. Only `pages` is required; you can delete them if you don't want to use their functionality.

### `assets`

The assets directory contains your uncompiled assets such as Stylus or Sass files, images, or fonts.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/assets).

### `components`

The components directory contains your Vue.js components. Components make up the different parts of your page and can be reused and imported into your pages, layouts and even other components.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/components).

### `layouts`

Layouts are a great help when you want to change the look and feel of your Nuxt app, whether you want to include a sidebar or have distinct layouts for mobile and desktop.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/layouts).

### `pages`

This directory contains your application views and routes. Nuxt will read all the `*.vue` files inside this directory and setup Vue Router automatically.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/get-started/routing).

### `plugins`

The plugins directory contains JavaScript plugins that you want to run before instantiating the root Vue.js Application. This is the place to add Vue plugins and to inject functions or constants. Every time you need to use `Vue.use()`, you should create a file in `plugins/` and add its path to plugins in `nuxt.config.js`.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/plugins).

### `static`

This directory contains your static files. Each file inside this directory is mapped to `/`.

Example: `/static/robots.txt` is mapped as `/robots.txt`.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/static).

### `store`

This directory contains your Vuex store files. Creating a file in this directory automatically activates Vuex.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/store).
