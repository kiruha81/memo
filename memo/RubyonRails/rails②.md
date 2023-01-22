# deviseのサインアップ、サインイン時のカラム受け取りはデフォルトでemailとpasswordのみ
#### nameカラムを使うときは追記が必要(①で書いてる)
#### その後コントローラー(application_controller.rb)で許可しないといけない
before_action :configure_permitted_parameters, if: :devise_controller?

  protected

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:name])
  end

# form_with
#### 基本形
<%= form_with model: , url: , method: :デフォルトはget, do |f| %>
  <%= f.text_field :カラム名, placeholder: "空白時になにか書ける" %>
  <%= f.text_area :カラム名 %>
  <%= f.submit '○○' %>
<% end %>
#### 記述例
<%= form_with model: @post_image do |f| %>
  <h4>画像</h4>
    <%= f.file_field :image, accept: "image/*" %>
  <h4>ショップ名</h4>
    <%= f.text_field :shop_name %>
  <h4>説明</h4>
    <%= f.text_area :caption %>
  <%= f.submit '投稿' %>
<% end %>
#### file_fieldはデフォルトだと何でもアップロードできるのでaccept(受け入れる)でファイルの種類を絞る

# モデル名.new
#### 格納するための箱のようなもの。箱がないとカラムたちも入れない。

# インスタンス変数
#### @をつけることによってviewとやり取りできる
#### コントローラーの変数は定義された変数でしかやり取りできない
##### 例：コントローラーのshowで定義した変数はviewのshowでしか使えない

# ストロングパラメーター
#### 記述例
private
  def list(モデル名)_params
    params.require(:list(モデル名)).permit(:title, :body(カラム名))
  end

##### params：パラメータ
##### require：必須
##### permit：許可

#### 実装することによって脆弱性をなくしている。
### privateに対してprotectedがある。
#### 記述例(deviseのサインアップ、サインイン時のカラム受け取りの許可)
protected

def configure_permitted_parameters
  devise_parameter_sanitizer.permit(:sign_up, keys: [:name])
end

#### protectedは他のコントローラーからも呼び出せるという効果がある

# eachメソッドを使用した一覧表示
#### 記述例
<%= @lists.each do |変数| %>

  <%= 変数.id %>
  <%= 変数.title %>
  <%= 変数.body %>

<% end %>

#### eachは順番に取得するメソッド

# findメソッド
#### 記述例
@list = List.find(params[:id])

#### findは引数を受け取るメソッド
#### params：パラメータ
#### [:id]はidのカラム
### Listモデルからidパラメータを取得して(探して、見つけて)いる。

# link_toメソッド
#### 基本形
<%= link_to 表示させるテキスト , リンク先URL [,オプション] %>
#### 記述例
<%= link_to list.title, list_path(list.id) %>
#### methodも指定できる。デフォルトはGET

# 保存、更新、削除
#### GET　　　データの取得(ページ自体もデータ)
#### POST　　 新しいデータの作成
#### PUT　　　既存のデータの更新
#### PATCH　　既存のデータの一部更新
#### DELETE	　既存のデータを削除

#### POST   = create
#### PUT    = update
#### PATCH  = update
#### DELETE = destroy

# after_sign_in_path_forとafter_sign_out_path_for
#### 記述例
def after_sign_in_path_for(resource)
  about_path
end

#### deviseをinstallすると使えるメソッド
#### サインイン(サインアウト)した後にどこに移動するか設定する
#### controllers/application_controller.rbで記述する
#### デフォルト設定はroot_path

# before_actionについて
#### 定義されたアクション等の前に実行することができる？

# current_user.id
#### currentは現在という意味

