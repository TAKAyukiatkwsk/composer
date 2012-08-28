# 基本的な使い方

## インストール

To install Composer, you just need to download the `composer.phar` executable.
Composer をインストールするためには、まずは実行可能な `composer.phar` をダウンロードする必要があります。

    $ curl -s http://getcomposer.org/installer | php

For the details, see the [Introduction](00-intro.md) chapter.
詳細は、[はじめに](00-intro.md) の章を御覧ください。

To check if Composer is working, just run the PHAR through `php`:
もし、Composer が動作するかを確認する場合は、 `php` コマンドで PHAR を実行してください:

    $ php composer.phar

This should give you a list of available commands.
これにより、利用可能なコマンドリストが表示されるでしょう。

> **Note:** You can also perform the checks only without downloading Composer
> by using the `--check` option. For more information, just use `--help`.
>
> **Note:** もし、Composer をダウンロードせずに、環境のチェックだけ行いたい場合は
> `--check` オプションを追加して、実行してください。 さらに情報が欲しい場合は、
> `--help` オプションを追加してください。
>
>     $ curl -s http://getcomposer.org/installer | php -- --help


## `composer.json`: プロジェクト設定

To start using Composer in your project, all you need is a `composer.json`
file. This file describes the dependencies of your project and may contain
other metadata as well.

Composer をプロジェクトで使い始めるために、まずは `composer.json` ファイルが
必要です。このファイルは、あなたのプロジェクトの依存を宣言して、プロジェクトに
関わるメタデーターを含みます。

The [JSON format](http://json.org/) is quite easy to write. It allows you to
define nested structures.

`composer.json` は、とても作成しやすい [JSON形式](http://json.org/) で、
定義されたネスト構造を許容します。

### `require` キー

The first (and often only) thing you specify in `composer.json` is the
`require` key. You're simply telling Composer which packages your project
depends on.

`require` key は、`composer.json` で最初に (これだけ) 明記するものです。
このキーでプロジェクトの依存パッケージを Composer に簡単に支持することができます。


    {
        "require": {
            "monolog/monolog": "1.0.*"
        }
    }

As you can see, `require` takes an object that maps **package names** (e.g. `monolog/monolog`)
to **package versions** (e.g. `1.0.*`).

見ての通り、 `require` は、 キーが **パッケージ名** (例: `monolog/monolog`)、
値が **パッケージバージョン** (例: `1.0.*`)  であるオブジェクトです。

### パッケージ名

The package name consists of a vendor name and the project's name. Often these
will be identical - the vendor name just exists to prevent naming clashes. It allows
two different people to create a library named `json`, which would then just be
named `igorw/json` and `seldaek/json`.

パッケージ名には、ベンダー名とプロジェクト名を含みます。パッケージ名は一意で、
ベンダーネームは名前の衝突を防ぐために存在します。このことは、2人が `json` という名前の
ライブラリを `igorw/json` 、 `seldaek/json` のように名付けることを許容します。


Here we are requiring `monolog/monolog`, so the vendor name is the same as the
project's name. For projects with a unique name this is recommended. It also
allows adding more related projects under the same namespace later on. If you
are maintaining a library, this would make it really easy to split it up into
smaller decoupled parts.

ここで、必要としている `monolog/monolog` は、 ベンダー名がプロジェクト名と
同一です。ユニークな名前を持ったプロジェクトについてはこれが推奨されます。
これにより、後に関係するプロジェクトを、同じ名前空間に追加することができます。
ライブラリをメンテナンスするときに、より細かい単位に分割することをより簡単にします。

### パッケージバージョン

We are requiring version `1.0.*` of monolog. This means any version in the `1.0`
development branch. It would match `1.0.0`, `1.0.2` or `1.0.20`.

例では、monolog では、 `1.0.*` というバージョンを必要としています。これは、開発
ブランチの `1.0` のいずれかを意味します。`1.0.0` や `1.0.2` 、 `1.0.20` といった
バージョンにマッチします。

Version constraints can be specified in a few different ways.

バージョン指定は、幾つかの指定方法が存在します。

* **Exact version:** You can specify the exact version of a package, for
  example `1.0.2`. This is not used very often, but can be useful.

* **厳密なバージョン指定:** `1.0.2` のように パッケージのバージョンを厳密に
  指定します。あまり頻繁には使われませんが、有用になりえるでしょう。

* **Range:** By using comparison operators you can specify ranges of valid
  versions. Valid operators are `>`, `>=`, `<`, `<=`, `!=`. An example range
  would be `>=1.0`. You can define multiple ranges, separated by a comma:
  `>=1.0,<2.0`.

* **範囲指定:** 比較演算子を利用することで、それに該当するバージョンを指定する
  ことができます。有効な演算子は `>`, `>=`, `<`, `<=`, `!=` です。例えば、
  `>=1.0` のような範囲指定ができます。また、 `>=1.0,<2.0` のようにコンマで区切る
  ことで複数の範囲を指定することができます。

* **Wildcard:** You can specify a pattern with a `*` wildcard. `1.0.*` is the
  equivalent of `>=1.0,<1.1-dev`.

* **ワイルドカード:** `*` ワイルドカードを指定することで、パターンを指定することができます。
  `1.0.*` は、 `>=1.0,<1.1-dev` と同一です。

## 依存のインストール

To fetch the defined dependencies into your local project, just run the
`install` command of `composer.phar`.

定義された依存をローカルのプロジェクトに取得するためには、 `composer.phar`
の `install` コマンドを実行するだけです。

    $ php composer.phar install

This will find the latest version of `monolog/monolog` that matches the
supplied version constraint and download it into the `vendor` directory.
It's a convention to put third party code into a directory named `vendor`.
In case of monolog it will put it into `vendor/monolog/monolog`.

コマンドの実行により、指定したバージョンにマッチする `monolog/monolog` の
最新バージョンを探し出し、 `vendor` ディレクトリにダウンロードします。
これは、サードパーティのコードは `vendor` ディレクトリに配置するという
風習によるものです。今回の場合、monolog は `vendor/monolog/monolog` に
配置されます。

> **Tip:** If you are using git for your project, you probably want to add
> `vendor` into your `.gitignore`. You really don't want to add all of that
> code to your repository.

> **Tip:** もしも、プロジェクトで git を利用している場合は、 `vendor` を
> `.gitignore` に追加する必要があるでしょう。リポジトリにすべてのコードを
> 追加する必要はありません。

Another thing that the `install` command does is it adds a `composer.lock`
file into your project root.

また、 `install` コマンドにより、プロジェクトのルートに `composer.lock`
が追加されます。

## `composer.lock` - ロックファイル

After installing the dependencies, Composer writes the list of the exact
versions it installed into a `composer.lock` file. This locks the project
to those specific versions.

依存をインストールした後に、Composer は インストールされた厳密なバージョンが
書かれた `composer.lock` ファイルを作成します。これは、プロジェクトの特定の
バージョンに、プロジェクトをロックするためのものです。

**Commit your application's `composer.lock` (along with `composer.json`) into version control.**

**アプリケーションの `composer.lock` は (`composer.json` と共に) バージョンコントロールにコミットするようにしてください。**

This is important because the `install` command checks if a lock file is present,
and if it is, it downloads the versions specified there (regardless of what `composer.json`
says). This means that anyone who sets up the project will download the exact
same version of the dependencies.

これは `install` コマンドは、事前にロックファイルを確認し、(`composer.json` の内容にかかわらず )
特定のバージョンをダウンロードするため重要なことです。 このことは、誰かがセットアップした
プロジェクトと厳密に同じ依存バージョンをダウンロードするということです。

If no `composer.lock` file exists, Composer will read the dependencies and
versions from `composer.json` and  create the lock file.

もし、 `composer.lock` が存在しないときは、 Composer は、 `composer.json` から
依存とバージョンを読み込み、ロックファイルの作成を行います。

This means that if any of the dependencies get a new version, you won't get the updates
automatically. To update to the new version, use `update` command. This will fetch
the latest matching versions (according to your `composer.json` file) and also update
the lock file with the new version.

このことは、ある依存で新しいバージョンになろうとも、自動的にはアップデートされないことを意味します。
新しいバージョンにアップデートしたい場合は、 `update` コマンドを利用してください。
このコマンドは、最新のマッチするバージョンを取得し (`composer.json` ファイルの内容に従います。)
ロックファイルを新しいバージョンのものに更新します。

    $ php composer.phar update

> **Note:** For libraries it is not necessarily recommended to commit the lock file,
> see also: [Libraries - Lock file](02-libraries.md#lock-file).

> **Note:** ライブラリの場合、必ずしもロックファイルをコミットすることは推奨されません。
> [ライブラリ - ロックファイル](02-libraries.md#local-file) も確認してください。

## Packagist

[Packagist](http://packagist.org/) is the main Composer repository. A Composer
repository is basically a package source: a place where you can get packages
from. Packagist aims to be the central repository that everybody uses. This
means that you can automatically `require` any package that is available
there.

[Packagist](http://packagist.org/) は、メインの Composer レポジトリです。 Composer
レポジトリは、基本的にパッケージが取得できる場所を示している、パッケージソースです。
Packagist の目標は、誰でも利用することができる中央レポジトリになることです。
つまり、 自動的に `require` により取得できるパッケージがあるということです。

If you go to the [packagist website](http://packagist.org/) (packagist.org),
you can browse and search for packages.

[packagist website](http://packages.org/) (packages.org) では、
パッケージの表示と検索を行うことができます。

Any open source project using Composer should publish their packages on
packagist. A library doesn't need to be on packagist to be used by Composer,
but it makes life quite a bit simpler.

Composer を利用しているオープンソースプロジェクトは、パッケージを packagist に
公開するべきでしょう。ライブラリは、Composer が利用する packagist 上にある必要は
ありませんが、このことは生活をよりシンプルにするでしょう。

## オートローディング

For libraries that specify autoload information, Composer generates a
`vendor/autoload.php` file. You can simply include this file and you
will get autoloading for free.

オートロード情報を指定するライブラリのために、 Composer は `vendor/autoload.php`
ファイルを生成します。このファイルは簡単に include することができ、
これによりオートローディングを気軽に行うことができます。

    require 'vendor/autoload.php';

This makes it really easy to use third party code. For example: If your
project depends on monolog, you can just start using classes from it, and they
will be autoloaded.

これだけで、簡単にサードパーティのコードを利用することができます。例えば、
monolog に依存しているプロジェクトでは、以下のようにクラスを使うことができ、
クラスはオートロードされます。

    $log = new Monolog\Logger('name');
    $log->pushHandler(new Monolog\Handler\StreamHandler('app.log', Monolog\Logger::WARNING));

    $log->addWarning('Foo');

You can even add your own code to the autoloader by adding an `autoload` field
to `composer.json`.

`autoload` フィールドを `composer.json` に追加することで、
あなたが作成したコードも、オートローダーに追加することもできます。

    {
        "autoload": {
            "psr-0": {"Acme": "src/"}
        }
    }

Composer will register a
[PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md)
autoloader for the `Acme` namespace.

Composer は、[PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md)
オートローダーに、 `Acme` という名前空間を登録します。

You define a mapping from namespaces to directories. The `src` directory would
be in your project root, on the same level as `vendor` directory is. An example
filename would be `src/Acme/Foo.php` containing an `Acme\Foo` class.

あなたは、名前空間とディレクトリをマッピングを定義します。 `src` ディレクトリは
プロジェクトのルートディレクトリに有り、 `vendor` ディレクトリと同じ階層です。
例えば、 `src/Acme/Foo.php` には、 `Acme/Foo` クラスを含んでいます。

After adding the `autoload` field, you have to re-run `install` to re-generate
the `vendor/autoload.php` file.

`autoload` フィールドを追加した後で、`vendor/autoload.php` を再生成するために、
再度 `install` コマンドを実行する必要があります。

Including that file will also return the autoloader instance, so you can store
the return value of the include call in a variable and add more namespaces.
This can be useful for autoloading classes in a test suite, for example.

`vendor/autoload.php` をロードするときに オートローダーのインスタンスも返します。
そのインスタンスに、さらに名前空間を追加することができます。
これは、テストスイートなどでオートローディングを行うときに便利です。

    $loader = require 'vendor/autoload.php';
    $loader->add('Acme\Test', __DIR__);

In addition to PSR-0 autoloading, classmap is also supported. This allows
classes to be autoloaded even if they do not conform to PSR-0. See the
[autoload reference](04-schema.md#autoload) for more details.

PSR-0 オートローディングの他に、クラスマップによる方法もサポートしています。
これにより、PSR-0 に準拠しない形式のクラスでもオートロードを行うことができます。
[autoloader reference](04-schema.md#autoload) で詳細を確認できます。

> **Note:** Composer provides its own autoloader. If you don't want to use
that one, you can just include `vendor/composer/autoload_namespaces.php`,
which returns an associative array mapping namespaces to directories.

> **Note:** Composer は独自のオートローダーを提供しています。もしも、それが必要ないときは
> 名前空間とディレクトリの組み合わせ配列を、 `vendor/composer/autoload_namespaces.php` を
> include するだけで取得することができます。

&larr; [はじめに](00-intro.md)  |  [ライブラリ](02-libraries.md) &rarr;
