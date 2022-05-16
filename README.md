# bookers2 debug
dmm webcamp 研修カリキュラム 応用課題2
## debugした項目
### 1. routes.rbファイル end忘れ
routes.rb の最後に`end`を追記
<br><br>
### 2. ホストの許可
config/environments/development.rbにホストの許可を追記
<br><br>
### 3. users_controllerのend忘れ
users_controller.rbのindexアクションのend忘れ.`end`を追記
<br><br>
### 4. ルーティング、無限ループ
routes.rbの`devise_for :users`を`resources`の上に移動する。<br>
`resources :users, only: :show, :index, :edit, :update]`が先に読み込まれ、<br>
`GET '/users/:id' => 'users#show'`になる。<br>
deviseで`GET '/users/sign_in'`で、id = sign_inという判定になる。<br>
usersコントローラでログイン制限がかかっているので<br>
`/users/(idが)sign_in` => `users#show` => ログインしていないので `/users/sign_in`にリダイレクト => `users#show` => ...<br>
という無限ループになる。<br>
devise_forを上に記述することで<br>
`GET '/users/sign_in'`=> `devise/sessions#new`になる
<br><br>
### 5. `Webpacker::Manifest::MissingEntryError in Devise::Sessions#new`というエラー
`bundle exec rails webpacker:install`で解決
<br><br>
### 6. ヘッダー以外のレイアウトが表示されない(yield忘れ)
view/layouts/application.rb の `main`タグの中に `<%= yield %>`を追加する。<br>
`<%= yield %>` は、各ページの内容のhtmlファイルの内容を持ってくるメソッド
<br><br>