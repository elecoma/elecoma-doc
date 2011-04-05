
ディレクティブ実験場
======================

.. _note:

ノート .. note::
--------------------

.. note::
   ノート

   .. note::
      入れ子が可能


.. _warning:

警告 .. warning::
-------------------

.. warning::
   警告！！！！

   .. note::
      これも入れ子ＯＫみたい

.. _sidebar:

サイドバー ..sidebar::
-------------------------

.. sidebar:: タイトル
   :subtitle: サブタイトル

   サイドバー


.. _line_block:

ラインブロック .. line-block::
-----------------------------------

.. line-block::

   ラインブロック

.. _Parsed:

Parsed Literal Block .. parsed-literal::
--------------------------------------------------

.. parsed-literal::

   ( (note_, warning_?)?,
     sidebar_?,
     (line_block_, Parsed_?)?,
     Topic_ )


.. _Topic:

トピック .. Topic::
-----------------------------------

.. Topic:: トピックタイトル

   てすと

コンテンツ .. Contents::
---------------------------------

.. contents:: 
   コンテンツの内容



.. header:: htmlでは無効？
   ヘッダー

.. footer:: htmlでは無効？
   フッター

.. meta::
   :keywords: sphinx, directives test park

生データ .. raw::
-----------------------

.. raw:: html

   <h1>htmlタグが使える!!</h1>
   テスト<br />
   <b>太字</b>
   <script type="text/javascript" />
   window.onload = function() {
      var flash=true;
      var delay = 1000;
      setInterval(function() {
          var now = new Date();
          var theHour = now.getHours();
          var theMin = now.getMinutes();
          var clockDisp = " " + ((theHour < 10) ? " " : "") + theHour;
          clockDisp += ((flash == true) ? ":" : " ");
          clockDisp += ((theMin <10) ? "0" : "") + theMin;
          document.getElementById("clock").innerHTML = clockDisp;
          flash - !flash;
      }, delay);
   };
   </script>

   <p>javascriptテスト 現在の時刻:<span id="clock"><span></p>

   

画像関連 .. image:: & .. figure::
-----------------------------------

imageディレクティブ

.. image:: /images/intro/admin_users_1.gif


figureディレクティブ

.. figure:: /images/intro/admin_users_1.gif 
   :figwidth: 200


imageディレクティブでslimebox2を利用

.. image:: /images/admin/shopmaster.png
   :scale: 20%
   :alt: てすと
   :class: lightbox

ソースコードの表示
-----------------------

ソースコードのテスト::

  test

ああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああ


.. highlight:: c
   :linenothreshold: 5

ハイライトのテスト::

     #include <stdio.h>
     
     void main(){
       int i = 0;
       printf("i = %d", i);
     }

てすと::

     #include <stdio.h>
     
     void main(){
     }

行番号テスト::

     #include <stdio.h>

     void main(){
     int hogehogehogehoge = 0,hogehogehoge = 0,hogehoge = 0,hoge = 0;
     printf("テストテストテストテストテストテスト\n hogehogehogehoge = %d\n hogehogehoge = %d\n hogehoge = %d\n hoge = %d\n",hogehogehogehoge, hogehogehoge, hogehoge, hoge);
     }
