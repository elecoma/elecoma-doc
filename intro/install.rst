インストール
============

エレコマをインストールしよう

動作環境・推奨環境
-------------------

エレコマの動作環境を確認しよう

.. list-table:: エレコマの動作環境

   * - OS
     - CentOS 5.4
   * - DB
     - postgersql 8.3系
   * - Ruby
     - 1.8.7
   * - Rails
     - 2.3.2



用意するもの
------------

エレコマをダウンロードしよう

エレコマには必要なpluginが含まれていません、各自ダウンロードしましょう





インストール
------------

.. highlight:: bash

1. rubyのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     $ sudo yum install gcc
     $ sudo yum install zlib-devel
     $ sudo yum install openssl-devel
     $ sudo yum install ncurses-devel
     $ sudo yum install readline-devel
     $ wget ftp://ftp.ruby-lang.org/pub/ruby/1.8/ruby-1.8.7-p174.tar.gz
     $ tar zxf ruby-1.8.7-p174.tar.gz 
     $ cd ruby-1.8.7-p174
     $ ./configure
     $ make
     $ sudo make install

2. gemのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     $ wget http://rubyforge.org/frs/download.php/60718/rubygems-1.3.5.tgz
     $ tar zxf rubygems-1.3.5.tgz
     $ cd rubygems-1.3.5
     $ sudo ruby setup.rb
     
3. ImageMagickのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     $ sudo yum install libjpeg-devel libpng-devel gd-devel freetype-devel
     $ wget \
       ftp://ftp.kddlabs.co.jp/graphics/ImageMagick/ImageMagick-6.5.8-4.tar.gz
     $ tar zxf ImageMagick-6.5.8-4.tar.gz
     $ cd ImageMagick-6.5.8-4
     $ ./configure
     $ make
     $ sudo make install

4. Rmagickのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     $ alias sudo="sudo PATH=$PATH"
     $ sudo gem install rmagick -v 2.12.2
     $ unalias sudo
    
5. 依存するgemのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     $ sudo gem install rails -v 2.3.5
     $ sudo gem install gettext -v 2.1.0
     $ sudo gem install gruff -v 0.3.6
     $ wget http://www.artonx.org/data/lhalib/lhalib-0.8.1.gem
     $ sudo gem install lhalib-0.8.1.gem
     $ sudo gem install webmock -v 1.3.4
     $ sudo gem install thoughtbot-factory_girl -v 1.2.2 \
      --source http://gems.github.com

6. PostgreSQLのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     $ sudo yum install postgresql-devel
     $ sudo yum install postgresql-server
     $ sudo gem install postgres

7. ecユーザの作成
^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     # adduser ec
     # passwd ec
     (パスワード変更)

8. アプリケーションの展開
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     # cd /usr/local
     # tar zxf (DOWNLOAD_PATH)/elecoma-<version>.tar.gz
     # mv elecoma-<version> ec
     # chown -R ec:ec /usr/local/ec


9. postgresqlのセットアップ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     # vim /var/lib/pgsql/data/pg_hba.conf
     (password cryptを設定します)
     # /etc/init.d/postgresql start
     # su - postgres
     $ psql template1
     # alter user postgres with password 'xxxx';
     # q\
     $ createuser ec
     Shall the new role be a superuser? (y/n) y
     $ psql template1
     # alter user ec with password 'elephant';
     # \q
     $ createdb --owner=ec ec_dev
     CREATE DATABASE
     $ createdb --owner=ec ec_test
     CREATE DATABASE
     $ createdb --owner=ec ec
     CREATE DATABASE
     $ psql -l
             List of databases
        Name    |  Owner   | Encoding 
     -----------+----------+----------
      ec        | ec       | UTF8
      ec_dev    | ec       | UTF8
      ec_test   | ec       | UTF8
      postgres  | postgres | UTF8
      template0 | postgres | UTF8
      template1 | postgres | UTF8
     (6 rows)

10. 開発向けセットアップ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     # su - ec
     $ cd /usr/local/ec/
     $ cd config
     $ cp database.example.yml database.yml
     $ vim database.yml
     $ diff database.example.yml database.yml 
     3,4c3,4
     <   username: postgres
     <   password: 
     ---
     >   username: ec
     >   password: elephant
     $ cd environments
     $ vim development.rb
     (メールサーバの設定を変更)
     $ vim production.rb
     (メールサーバの設定を変更)
     $ vim test.rb
     (メールサーバの設定を変更)

11. gitのインストール
^^^^^^^^^^^^^^^^^^^^^^^

::

     $ wget http://kernel.org/pub/software/scm/git/git-1.6.5.5.tar.gz
     $ tar zxf git-1.6.5.5.tar.gz 
     $ cd git-1.6.5.5
     $ ./configure
     $ make
     $ sudo make install

12. プラグインのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     $ ruby script/plugin install git://github.com/realityforge/rails-active-form.git
     $ ruby script/plugin install git://github.com/rails/acts_as_list.git
     $ ruby script/plugin install git://github.com/technoweenie/acts_as_paranoid.git
     $ ruby script/plugin install git://github.com/rails/acts_as_tree.git
     $ ruby script/plugin install http://topfunky.net/svn/plugins/ar_fixtures/
     $ ruby script/plugin install git://github.com/jpmobile/jpmobile.git -r 'tag 0.0.8'
     $ ruby script/plugin install http://taslam-plugins.googlecode.com/svn/trunk/jpmobile_emoticon_filter/
     $ cd vendor/plugins
     $ git clone git://github.com/tmtysk/mbmail.git mbmail
     $ cd mbmail
     $ git checkout 654ce3ec2dfa10ac3b05cd9354eb84456d206a6d
     $ rm -fr lib/jpmobile
     $ rm -fr .git
     $ cd ../../..
     $ ruby script/plugin install git://github.com/jamesgolick/resource_controller.git
     $ ruby script/plugin install git://github.com/mislav/will_paginate.git
     $ ruby script/plugin install git://github.com/kakutani/yaml_waml.git
     $ ruby script/plugin install git://github.com/rails/ssl_requirement.git
     $ ruby script/plugin install git://github.com/DianthuDia/double_submit_protection.git
     $ ruby script/plugin install git://github.com/champierre/image_submit_tag_ext.git
     $ ruby script/plugin install git://github.com/dchelimsky/rspec-rails.git -r 'tag 1.2.9'
     $ ruby script/plugin install git://github.com/dchelimsky/rspec.git -r 'tag 1.2.9'


13. passengerのインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    $ sudo yum install gcc-c++
    $ sudo yum install httpd-devel
    $ sudo gem install passenger
    $ sudo passenger-install-apache2-module 

14. apacheの設定
^^^^^^^^^^^^^^^^^^^^^^^

::

    $ sudo vim /etc/httpd/conf.d/ec.conf
    LoadModule passenger_module /usr/local/lib/ruby/gems/1.8/gems/passenger-2.2.7/ext/apache2/mod_passenger.so
    PassengerRoot /usr/local/lib/ruby/gems/1.8/gems/passenger-2.2.7
    PassengerRuby /usr/local/bin/ruby

    <VirtualHost *:80>
      ServerName ec.example.com
      DocumentRoot /usr/local/ec/public
      RailsEnv production
      <Directory /usr/local/ec/public>
        AllowOverride all
        Options -MultiViews
      </Directory>
    </VirtualHost>

15. production DBの作成
^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    # su - ec
    $ rake db:migrate RAILS_ENV=production

16. apache の再起動
^^^^^^^^^^^^^^^^^^^^^

::

    $ sudo /etc/init.d/apache restart

17. script/mailを起動
^^^^^^^^^^^^^^^^^^^^^^^^

::

    $ ./script/mail_restart.sh -e production
    (メールマガジン送信用のプロセスを立ち上げます)

.. note::

    ※webrickでの起動も可能です。

    ::

        $ ruby ./script/server -e production
    

うまくインストールできない場合は
----------------------------------

