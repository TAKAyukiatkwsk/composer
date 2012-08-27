# はじめに

Composer は PHP で依存管理を行うためのツールです。 プロジェクトで必要な依存ライブラリの
定義と、インストールを行うことができます。

## 依存管理

Composer はパッケージマネージャではありません。もちろん、 "パッケージ" や ライブラリを
扱っていますが、 プロジェクトベースでパッケージを管理し、
プロジェクトのディレクトリの中にインストールします。 (例: `vendor` ディレクトリ)
標準ではグローバルにインストールされることはありません。
これが、依存管理です。

そのアイデアは新しいものではなく、 Composer は node の [npm](http://npmjs.org) や
ruby の [bundler](http://gembundler.com/). に強く影響を受けています。
しかし、このようなツールは PHP には存在しませんでした。

The problem that Composer solves is this:
次のように、Composer は問題を解決します:

a) You have a project that depends on a number of libraries.
a) プロジェクトに多くの依存ライブラリがあります。

b) Some of those libraries depend on other libraries .
b) 幾つかのライブラリは、他のライブラリに依存しています。

c) You declare the things you depend on
c) 依存する項目を宣言します。

d) Composer は、インストールされる必要のあるパッケージのバージョンを探し出し、
   インストールします。 (あなたのプロジェクトにダウンロードするという意味です。)

## 依存の宣言

プロジェクトを始めようというときに、あなたはロギングのためのライブラリが必要になりました。
そこで、あなたは [monolog](https://github.com/Seldaek/monolog) を使うことにしました。
プロジェクトにそれを追加するために、 プロジェクトの依存を宣言した、
`composer.json` というファイルを作る必要があります。

    {
        "require": {
            "monolog/monolog": "1.0.*"
        }
    }

`monolog/monolog` パッケージの `1.0` で始まる、いずれかのバージョン
が必要なプロジェクトを簡単にはじめることができます。

## インストール

### Composer のダウンロードと実行

#### ローカル

To actually get Composer, we need to do two things. The first one is installing
Composer (again, this mean downloading it into your project):

Composer を入手するには、2つの手順が必要です。はじめに、Composer を入手します。
(あなたのプロジェクトにダウンロードするという意味です。):

    $ curl -s https://getcomposer.org/installer | php

This will just check a few PHP settings and then download `composer.phar` to
your working directory. This file is the Composer binary. It is a PHAR (PHP
archive), which is an archive format for PHP which can be run on the command
line, amongst other things.

これは、幾つかのPHPの設定を確認し、 `composer.phar` を作業ディレクトリに
ダウンロードします。このファイルは Composer バイナリです。 これは、 PHAR
(PHPアーカイブ) で、特に、コマンドラインの実行に適したフォーマットです。

You can install Composer to a specific directory by using the `--install-dir`
option and providing a target directory (it can be an absolute or relative path):

`--install-dir` オプションにパスを指定をすることで、
特定のパスに Composer をインストールすることができます。
(絶対パスか、相対パスで指定することができます。):

    $ curl -s https://getcomposer.org/installer | php -- --install-dir=bin

#### グローバル

You can place this file anywhere you wish. If you put it in your `PATH`,
you can access it globally. On unixy systems you can even make it
executable and invoke it without `php`.

`PATH` に設定している場所に、Composer を設置することで、
グローバルにアクセスすることができます。Unix系システムでは、
`php` コマンドなしで実行可能な Composer を用意することができます。

You can run these commands to easily access `composer` from anywhere on your system:
以下のコマンドを実行することで、 `composer` に、システムのどこからでもアクセスできます:

    $ curl -s https://getcomposer.org/installer | php
    $ sudo mv composer.phar /usr/local/bin/composer

これにより、`composer` のみで Composer を実行することができます。

### Composer の利用

次に、依存を解決するために `install` コマンドを実行します:

    $ php composer.phar install

これにより、 `vendor/monolog/monolog` ディレクトリに monolog がダウンロードされます。

## オートロード

ダウンロードされたライブラリのほかに、 Composer は ダウンロードしたライブラリの
クラスをオートロードするための autoload ファイルを生成します。
これを使うには、あなたのコードの初期化プロセスに以下の行を追加してください:

    require 'vendor/autoload.php';

なんと、これだけで monolog を使うことができます! さらに、Composer について
知りたい場合は、続けて "基本的な使い方" の章をお読みください。

[Basic Usage](01-basic-usage.md) &rarr;
