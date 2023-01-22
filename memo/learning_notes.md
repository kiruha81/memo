form_with の　placeholder
１７章

19章
 def favorited_by?(user)
    favorites.exists?(user_id: user.id)
  end

  # post_image/index

  <% @post_images.each do |post_image| %>
  <div>
    <%= link_to post_image_path(post_image.id) do %>
      <%= image_tag post_image.get_image %>
    <% end %>
    <p>投稿ユーザー画像：<%= image_tag post_image.user.get_profile_image(100, 100) %></p>
    <P>ショップ名：<%= post_image.shop_name %></P>
    <p>説明：<%= post_image.caption %></p>
    <p>ユーザーネーム：<%= post_image.user.name %></p>
    <p><%= link_to "#{post_image.post_comments.count} コメント", post_image_path(post_image.id) %></p>
  </div>

<% end %>


# user/show

<% @post_images.each do |post_image| %>
<div>
  <%= link_to post_image_path(post_image.id) do %>
    <%= image_tag post_image.get_image %>
  <% end %>
  <p>投稿ユーザー画像：<%= image_tag post_image.user.get_profile_image(100, 100) %></p>
  <p>ショップ名：<%= post_image.shop_name %></p>
  <p>説明：<%= post_image.caption %></p>
  <p>ユーザーネーム：<%= post_image.user.name %></p>
  <p><%= link_to "#{post_image.post_comments.count} コメント", post_image_path(post_image.id) %></p>
</div>
<% end %>




# railsをcloud9にinstall
wget https://wals.s3.ap-northeast-1.amazonaws.com/curriculum/rails/environment.sh
↓
sh environment.sh
↓
rails -v

#rails アプリ install
rails new アプリ名

# ターミナルのフォルダとファイル削除
rm -rf フォルダ名

# config/environments 誰でも見れるようにするやつ
config.hosts.clear

# rails サーバー起動
rails s

# active_storage installコマンド マイグレーション(rails db:migrate)忘れずに
rails active_storage:install

# 使用する画像ファイルはapp/assets/imageの中へ

# 作る前に確認 アプリ2の2

# 画像が表示されるモデルにつけるやつ
has_one_attached :image

# rails側で画像サイズの管理をするときに使うgem image_processingをinstallしたときのエラー回避のための記述をconfig/environmentsで
config.active_job.queue_adapter = :inline
#### gem image_processingはGemfileにコメントアウトで記述あり

# gemをinstallするときはGemfileにinstallしたいgemを書いてから
bundle install

# ユーザー管理するときはdeviseのgemを使う
## Gemfileに
gem 'devise'
↓
bundle install
↓
rails g devise:install
↓
#### deviseを用いたときのモデル作成の記述は通常と異なる
rails g devise User
↓
#### nameカラムを使用したいときはテーブルに追加する
###### db/migrate/～.rb
t.string :name
rails db:migrate
#### devise用のルーティング：devise_for :users がconfig/routes.rbに入力されている
##### sign_up、sign_in、sign_outとか

# モデル作成　削除は g → d
rails g model モデル名(単数形の頭文字は大文字 例：User)
## テーブルは小文字の複数形になる(例：users)

# カラム追加はdb/migrateの中で
#### integer(整数)、string(短文)、text(長文)、time(時刻) など　詳しくはアプリ2-2
t.データ型 :カラム名
↓
## データベースに反映させる必要がある
rails db:migrate

## db/schema.rbで反映を確認できる

## 後から追加する場合は
rails g migration Addカラム名Toテーブル名 カラム名:型名
## 削除
rails g migration Removeカラム名Fromテーブル名 カラム名:型名
### もしくは
#### dbの稼働状況を確認
rails db:migrate:status
#### dbをdawnすることができるコマンド(戻す)
rails db:rollback
↓
db/migrate内のテーブルファイルでカラム追加
↓
rails db:migrate

# コントローラー
rails g controller コントローラー名(小文字の複数形)
#### コントローラー名の後にアクション名をつけるとviewとアクションが追加される(複数可)


