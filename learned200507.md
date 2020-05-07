# 課題ECサイト
スマホ向け、テイクアウトメニュー注文サイト  
<img src="https://i.gyazo.com/dc63dc0738e1ea6526d970bd433642f1.png" alt="Image from Gyazo" width="250"/>

## 使用技術
- Rails6
- Ruby2.7
- JavaScript
- Haml
- SCSS

## 主な機能一覧
- SHOP開設/編集
- ログイン/ログアウト機能
- メニュー登録/編集/削除
- カート機能（カートに追加/削除）
- カード決済（ログインなしで決済可能）
- 受注アラート機能

### SHOP開設/編集
<img src="https://i.gyazo.com/ad9034459d01e9497a0f532e3718ef16.png" alt="Image from Gyazo" width="250"/><img src="https://i.gyazo.com/85ac8bdd600b6eee24ab029545b3c9a6.png" alt="Image from Gyazo" width="400"/>
<img src="https://i.gyazo.com/26c362aa365e48810af806730a9c3332.png" alt="Image from Gyazo" width="250"/>

- 店名、パスワード、お店の紹介文を入力することで、SHOPを開設することができます。
- お店の位置情報は、JavaScriptで取得、input type="hidden"でformに自動追加されます。
- 店舗詳細ページの「お店の情報を編集」から、編集可能です。

### ログイン/ログアウト機能
<img src="https://i.gyazo.com/f4ee03d739c6cd64592111aae7397f8b.png" alt="Image from Gyazo" width="400"/>

- 店名とパスワードの入力でログイン認証可能です。
- gem bcrypt を使用

### メニュー登録/編集/削除
#### ログイン時  
<img src="https://i.gyazo.com/1198e5fba6c70f2b821a8a6500d49fa8.png" alt="Image from Gyazo" width="250"/> <img src="https://i.gyazo.com/1ceda95c2541c3fc146d0018cc3ba83e.png" alt="Image from Gyazo" width="400"/>

- メニュー名、価格を入力することで、メニューを登録することができます。
- 一覧の各メニュー名の横にある「編集」「削除」リンクを押すことで、編集/削除を行うことができます。

#### 未ログイン or ログインユーザー以外の店舗詳細ページ  
<img src="https://i.gyazo.com/19536b1bb513e8b9b3e0d30fead8a7c4.png" alt="Image from Gyazo" width="400"/>

- 「カートに追加」ボタンが表示されるようになります。

### カート機能（カートに追加/削除）
<img src="https://i.gyazo.com/2f4593877fc5232900e5842abd14e9b3.png" alt="Image from Gyazo" width="400"/>
<img src="https://i.gyazo.com/ceb00fa3624c1640def3f54d1cfcdf3f.png" alt="Image from Gyazo" width="400"/>

- 「カートに追加」ボタンを押すことで、カートにメニューを追加できます。
- 「カートに追加」ボタンを押すと同時に、現在位置をJavaScriptで取得し、お店の所在地との距離を算出し、受け取り時間の予測を行います。
- 「削除」を押すことで、カート内のメニューを削除できます。
- 「購入確認へ」ボタンを押すことで、購入確認画面に遷移します。

### カード決済（ログインなしで決済可能）
<img src="https://i.gyazo.com/5ba1e5895b083bb7ed0e44ef8590aad1.png" alt="Image from Gyazo" width="300"/><img src="https://i.gyazo.com/63ea7ff28b2609fa814a54eac5513cc0.png" alt="Image from Gyazo" width="300"/>

- 購入確認画面にて、カード情報を入力することで、購入することができます（ログイン不要）。
- gem Payjp を使用。
- テスト用カード： 4242424242424242

### 受注アラート機能
<img src="https://i.gyazo.com/691cddd70f486286421608451cf5272c.png" alt="Image from Gyazo" width="400"/>
<img src="https://i.gyazo.com/45c31c91c163aad483a4fa8d5078bfd3.png" alt="Image from Gyazo" width="300"/>

- 商品が購入されると、ヘッダーのベルアイコンが赤色になり、受注を把握することができます。
- ベルアイコンを押すと、受注一覧ページに遷移することができます。

## 改善点
- 地域登録の改善
  - 座標を取得することはできたが、座標から地域や住所を取得することができなかった。勉強してできるようにする。
- カート商品の個数管理
  - 商品を1つずつしかカートへ入れることができないので、カートで数量の管理もできるようにする。
- アラート機能改善
  - 通知を削除することができないので、チェックした通知は消えるように改善したい。

## 開発を終えて
「Rails6を利用した開発」「最初からdockerを使用した開発」「現在地の取得」「カート機能」「ログインなしカード決済」など、初めて挑戦するタスクが多く、非常に勉強になりました。  
まだまだ自分のスキルが未熟であることを実感し、もっと勉強を頑張ろうという刺激を得ることができました。  
この度は貴重な機会を与えてくださり、本当にありがとうございました。
