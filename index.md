---
layout: default
---

# WP_UnitTestCase ドキュメント (非公式)

## このドキュメントについて

WordPressのコア開発では、WP_UnitTestCaseというユニットテスト用のフレームワークが導入されており、これはプラグインやテーマの開発でも使用することができます。

しかし、残念ながらWP_UnitTestCaseに関する公式なドキュメントは存在しません。

そこで、WP_UnitTestCaseのドキュメントをGitHub上で公開することにしました。

[https://github.com/miya0001/wp_unittestcase-docs](https://github.com/miya0001/wp_unittestcase-docs)

ぜひ、ドキュメントの作成にご協力ください。

## WP_UnitTestCaseとは？

WP_UnitTestCaseは、WordPressのコア、プラグイン、テーマなどを開発するためのユニットテスト用フレームワークです。

このフレームワークは、PHPUnitのサブクラスとしてメンテナンスされており、これを使用することでWordPress開発における継続的インテグレーションを可能にします。

[https://phpunit.de/](https://phpunit.de/)

## インストール方法

WP_UnitTestCaseを導入するには何通りかの方法があります。

### WP-CLIを使って導入する

もしあなたがプラグイン開発のためにWP_UnitTestCaseを導入したいのなら、WP-CLIを使えば簡単に導入できます。

すでに開発中のプラグインに対してユニットテストを導入するには以下のコマンドを実行してください。

```
$ wp scaffold plugin-tests my-plugin
```

これから新しくプラグインを作る際には以下のコマンドを実行しましょう。

```
$ wp scaffold plugin my-plugin
```

コマンドの実行に成功すると以下のようなファイルが生成されているはずです。

```
$ cd $(wp plugin path --dir my-plugin)
$ tree
.
├── .travis.yml
├── bin
│   └── install-wp-tests.sh
├── my-plugin.php
├── phpunit.xml
├── readme.txt
└── tests
    ├── bootstrap.php
    └── test-sample.php

2 directories, 7 files
```

つぎにユニットテスト用のWordPress環境をインストールします。

この環境は、あくまでもテスト用の環境なのでマシンの再起動後などに何度もセットアップする必要がありますが、WP-CLIには専用のシェルスクリプトがあらかじめ用意されておりそれを実行すれば簡単にセットアップが完了します。

```
$ cd $(wp plugin path --dir my-plugin)
$ bash bin/install-wp-tests.sh wordpress_test root '' localhost latest
```

WP-CLIでは、[Travis CI](https://travis-ci.org/)を使用した継続的インテグレーションに必要なファイル(`.travis.yml`)も自動的に生成してくれます。

[https://github.com/wp-cli/wp-cli/wiki/Plugin-Unit-Tests](https://github.com/wp-cli/wp-cli/wiki/Plugin-Unit-Tests)

### VVVを使って導入する

もし、あなたがWordPressコア開発やテーマ開発のためにユニットテストを行いたいのなら、[Varying Vagrant Vagrants(VVV)](https://github.com/Varying-Vagrant-Vagrants/VVV)を使うのが簡単です。

詳しいインストール方法はVVVのドキュメントを御覧ください。

[https://github.com/Varying-Vagrant-Vagrants/VVV](https://github.com/Varying-Vagrant-Vagrants/VVV)


## テストを実行してみる

では、さっそくユニットテストを実行してみましょう。

### WordPressプラグインでユニットテストを実行する。

WP-CLIを使って、ユニットテスト用の環境を用意したのなら、すぐにテストを行うことができます。

プラグインのディレクトリに移動してから以下のコマンドを実行してください。

```
$ phpunit
```

コマンドを実行したら以下のように出力されるはずです。

```
Installing...
Running as single site... To run multisite, use -c tests/phpunit/multisite.xml
Not running ajax tests. To execute these, use --group ajax.
Not running ms-files tests. To execute these, use --group ms-files.
Not running external-http tests. To execute these, use --group external-http.
PHPUnit 4.3.4 by Sebastian Bergmann.

Configuration read from /Users/miyauchi/www/dev.local/www/wordpress/wp-content/plugins/my-plugin-2/phpunit.xml

.

Time: 1.28 seconds, Memory: 19.75Mb

OK (1 test, 1 assertion)
```

もし、エラーが出たら、インストールの手順をやり直してみてください。

### テスト用ファイルの構成

上述しましたが、WP-CLIでは以下のコマンドを実行すればユニットテストのひな形が自動的に作成されます。

```
$ wp scaffold plugin-tests my-plugin
```

ここではサンプルを見てみましょう。

```
├── .travis.yml
├── bin
│   └── install-wp-tests.sh
├── my-plugin.php
├── phpunit.xml
├── readme.txt
└── tests
    ├── bootstrap.php
    └── test-sample.php
```

プラグインのユニットテストに関連するファイルは以下のファイルです。

* .travis.yml
* bin/install-wp-tests.sh
* phpunit.xml
* tests/bootstrap.php
* test-sample.php

WP-CLIが自動的に生成するテストのひな形は、`tests/`ディレクトリ以下にある`test-`で始まるファイル名の`.php`ファイルを順番に読み込み、その中に書かれたテストを実行していきます。

以下のソースは、サンプルとして設置された`tests/test-sample.php`のソースです。

```
<?php

class SampleTest extends WP_UnitTestCase {

    function testSample() {
        // replace this with some actual testing code
        $this->assertTrue( true );
    }
}
```

このファイルの中で重要なポイントは3つです。

* クラスは、WP_UnitTestCaseを継承したクラスであること。
* 名前がtestで始まるメソッドが、phpunit実行時に自動的に実行される。
* $this->assertTrue()という記述をアサーションと言い、このアサーションを利用してプラグイン内のコードが期待通りに動いているかを順番に評価していく。

アサーションには、他にもたくさんあります。

* `assertTrue()` - 引数の値が`true`なら成功
* `assertEquals()` - 2つの引数が一致すれば成功
* `assertRegExp()` - 第一引数で正規表現を指定し、

PHPUnitには他にもたくさんのアサーションが用意されています。

[https://phpunit.de/manual/current/ja/appendixes.assertions.html](https://phpunit.de/manual/current/ja/appendixes.assertions.html)

また、WP_UnitTestCaseによって追加されたWordPressに特化したアサーションもいくつかあります。
