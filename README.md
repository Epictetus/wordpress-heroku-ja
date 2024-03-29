# WordPress Heroku

[WordPress](http://wordpress.org/) を [Heroku](http://www.heroku.com/)にデプロイするプロジェクト。
このプロジェクトには [PostgreSQL for WordPress](http://wordpress.org/extend/plugins/postgresql-for-wordpress/) と [WP Read-Only](http://wordpress.org/extend/plugins/wpro/)が同梱されています。

Installation
============

Githubからプロジェクトをclone

    $ git clone git://github.com/sson/wordpress-heroku-ja.git
    
[Heroku Toolbelt](https://toolbelt.heroku.com/)をインストールし、Herokuにアプリ(your-app-nameを好きな名前に置き換え)を作成。

    $ cd wordpress-heroku-ja
    $ heroku create your-app-name
    > Creating your-app-name... done, stack is cedar
    > http://your-app-name.herokuapp.com/ | git@heroku.com:your-app-name.git
    > Git remote heroku added

アプリ用DB(PostgreSQL)をアドオンで追加

    $ heroku addons:add heroku-postgresql:dev
    > Adding heroku-postgresql:dev to your-app-name... done, v2 (free)
	> Attached as HEROKU_POSTGRESQL_COLOR
	> Database has been created and is available
	> Use `heroku addons:docs heroku-postgresql:dev` to view documentation

DB情報の環境変数キーを表示(`YOURCOLOR`を置き換え)

    $ heroku pg
    > === HEROKU_POSTGRESQL_[YOURCOLOR]_URL
    > Plan:        Dev
    > Status:      available
    > Connections: 0
    > PG Version:  9.1.6
    > Created:     2013-01-20 08:07 UTC
    > Data Size:   5.9 MB
    > Tables:      0
    > Rows:        0/10000 (In compliance)
    > Fork/Follow: Unsupported

    

作成したDBをprimaryに設定

	$ heroku pg:promote HEROKU_POSTGRESQL_[YOURCOLOR]_URL
	> Promoting HEROKU_POSTGRESQL_YOURCOLOR_URL to DATABASE_URL... done

`wp-config.php`を`wp-config-sample.php`をコピーして作成

    $ cp wp-config-sample.php wp-config.php

`wp-config.php`をコミット

    $ git add .
    $ git commit -m "Initial WordPress commit"
    
Herokuにデプロイ

    $ git push heroku master
    > -----> Heroku receiving push
    > -----> PHP app detected
    > -----> Bundling Apache v2.2.22
    > -----> Bundling PHP v5.3.10
    > -----> Discovering process types
    >        Procfile declares types -> (none)
    >        Default types for PHP   -> web
    > -----> Compiled slug size is 13.8MB
    > -----> Launcing... done, v5
    >        http://your-app-name.herokuapp.com deployed to Heroku
    >
    > To git@heroku:your-app-name.git
    > * [new branch]    production -> master 

