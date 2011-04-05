.. _setup_admin_users:

Step.1 管理者ユーザーの設定
====================================

エレコマの管理者ユーザーの設定
-----------------------------------

エレコマを起動した直後は管理ユーザーが存在しません。

RAILS_ROOT/test/fixtures/admin_users.yml の 5, 6, 8行目を任意のものに変更します

.. highlight:: yaml
   :linenothreshold: 5

::

  # Read about fixtures at http://ar.rubyonrails.org/classes/Fixtures.html

  load_by_admin_user:
    id: 1
    name: admin #任意のユーザー名に修正してください
    login_id: admin #任意のログインIDに修正してください(半角英数字15文字以内)
    position: 1
    password: <%= AdminUser.encode_password 'pass' %> #passの部分を任意のパス
  ワードに修正してください（半角英数字15文字以内）
    authority_id: 1
    activity: true
  

コンソール画面から次のコードを入力してadmin_users.ymlの内容を登録します

.. highlight:: bash

::

   $ rake db:fixtures:load FIXTURES=admin_users RAILS_ENV=production

エレコマ管理画面にログイン
---------------------------

エレコマのインストールが完了したら

サイトドメイン/admin/ へアクセス

管理ユーザーのIDとPassを入力してログインします

.. image:: /images/intro/admin_users_1.gif
   :alt: エレコマのログイン画面

admin_users.ymlに入力した login_id と passward を使用してログインします

.. note::

   admin_users.ymlの内容を変更していない場合は次の設定になってます

      ID : admin

      パスワード : pass


管理者のIDとPassを管理画面から編集する
-----------------------------------------

.. warning::

   admin_users.ymlを変更しなかった場合は大変危険ですので直ぐに設定し直しましょう

エレコマの管理者ユーザーは管理画面の :ref:`admin_shops_system_admin_users` 画面からいつでも編集できます

:ref:`admin_shops` > :ref:`admin_shops_system` > :ref:`admin_shops_system_admin_users`

:ref:`admin_shops_system_admin_users` 画面ついての詳しい説明は :ref:`admin_shops_system_admin_users` を参照してください


