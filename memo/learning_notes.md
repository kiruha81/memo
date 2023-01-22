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






# config/environments 誰でも見れるようにするやつ
config.hosts.clear

# active_storage installコマンド マイグレーション忘れずに
rails active_storage:install

# 画像が表示されるモデルにつけるやつ
has_one_attached :image

# gemをinstallするときはGemfileにinstallしたいgemを書いてから
bundle install

# rails側で画像サイズの管理をするときに使うgem image_processingをinstallしたときのエラー回避のための記述をconfig/environmentsで
config.active_job.queue_adapter = :inline

# 使用する画像ファイルはapp/assets/imageの中へ