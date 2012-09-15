# Command-line interface
# コマンドラインインターフェイス

You've already learned how to use the command-line interface to do some
things. This chapter documents all the available commands.

既に、コマンドラインインターフェースを利用して、何かをやる方法について
学んできましたが、この章では全ての利用できるコマンドを紹介します。

## init

In the [Libraries](02-libraries.md) chapter we looked at how to create a
`composer.json` by hand. There is also an `init` command available that makes
it a bit easier to do this.

[ライブラリ](02-Libraries.md) チャプターでは、 `composer.json` の手動での作成方法を
確認しました。 `init` コマンドも、 `composer.json` を作ることができ、手動で行うより
は、やや簡単な方法です。

When you run the command it will interactively ask you to fill in the fields,
while using some smart defaults.

コマンドを実行すると、対話的に入力するフィールドについて尋ねられ、
すぐに使えるデフォルトを使うことができます。

    $ php composer.phar init

### Options
### オプション

* **--no-interaction:** (**-n**) Run the command in non-interactive mode.
  The rest of these options only make sense when you are in this mode.
* **--name:** Name of the package.
* **--description:** Description of the package.
* **--author:** Author name of the package.
* **--homepage:** Homepage of the package.
* **--require:** Package to require with a version constraint. Should be
  in format `foo/bar:1.0.0`.
* **--require-dev:** Development requirements, see **--require**.

* **--no-interaction:** (**-n**) 非対話モードで実行します。
  以下のオプションは、このモードでのみ有効です。
* **--name:** パッケージ名
* **--description:** パッケージ説明
* **--author:** パッケージ作成者
* **--homepage:** パッケージのホームページ
  in format `foo/bar:1.0.0`.
* **--require:** パッケージが必要なバージョン制約。フォーマットは `foo/bar:1.0.0` のようにしてください。
* **--require-dev:** 開発版で必要なバージョン制約。 **--require** を確認してください。

## install

The `install` command reads the `composer.json` file from the current
directory, resolves the dependencies, and installs them into `vendor`.

`install` コマンドは `composer.json` をカレントディレクトリから読み込み、
依存を解決し、 `vendor` へインストールするものです。

    $ php composer.phar install

If there is a `composer.lock` file in the current directory, it will use the
exact versions from there instead of resolving them. This ensures that
everyone using the library will get the same versions of the dependencies.

もし、カレントディレクトリに、 `composer.lock` が存在している場合は、
そのファイルに明記しているバージョンから依存を解決します。これは、
誰でも同じバージョンの依存を取得することを保証します。

If there is no `composer.lock` file, composer will create one after dependency
resolution.

`composer.lock` が存在しない場合は、composer は依存解決後にそれを作成します。

### Options
### オプション

* **--prefer-source:** There are two ways of downloading a package: `source`
  and `dist`. For stable versions composer will use the `dist` by default.
  The `source` is a version control repository. If `--prefer-source` is
  enabled, composer will install from `source` if there is one. This is
  useful if you want to make a bugfix to a project and get a local git
  clone of the dependency directly.
* **--dry-run:** If you want to run through an installation without actually
  installing a package, you can use `--dry-run`. This will simulate the
  installation and show you what would happen.
* **--dev:** By default composer will only install required packages. By
  passing this option you can also make it install packages referenced by
  `require-dev`.
* **--no-scripts:** Skips execution of scripts defined in `composer.json`.

* **--prefer-source:** パッケージのダウンロードには `source` と `dist` という
  2つの方法があります。安定版については、 composer は `dist` をデフォルトで利用します。
  `source` とは、バージョンコントロールレポジトリのことです。 `--prefer-source`
  が有効の場合、composer は、 `source` からインストールすることを優先します。
  これは、プロジェクトのためにバグフィックスをして、依存ディレクトリの
  ローカル git クローンから入手する際に便利です。
* **--dry-run:** もし、パッケージを実際にはインストールしたくない場合は、
  `--dry-run` を利用することができます。 これは、インストールをシミュレーションし、
  何が起こるかを見ることができます。
* **-dev:** composer はデフォルトで、 `require` に指定されたパッケージのみを
  インストールします。このオプションを指定すると、 `require-dev` に指定された
  パッケージもインストールします。
* **--no-scripts:** `composer.json` で定義された、スクリプトの実行をスキップします。

## update

In order to get the latest versions of the dependencies and to update the
`composer.lock` file, you should use the `update` command.

最新バージョンの依存を入手し、 `composer.lock` の更新を行いたいときに、
`update` コマンドを利用します。

    $ php composer.phar update

This will resolve all dependencies of the project and write the exact versions
into `composer.lock`.

このコマンドは、プロジェクトの全ての依存を解決し、解決したバージョンを `composer.lock`
に書き出します。

If you just want to update a few packages and not all, you can list them as such:

もし、全てではなく、幾つかのパッケージのみをアップデートしたい場合は、以下のように
アップデートすることができます。

    $ php composer.phar update vendor/package vendor/package2

### Options
### オプション

* **--prefer-source:** Install packages from `source` when available.
* **--dry-run:** Simulate the command without actually doing anything.
* **--dev:** Install packages listed in `require-dev`.
* **--no-scripts:** Skips execution of scripts defined in `composer.json`.

* **--prefer-source:** 可能であれば、パッケージを `source` からインストールします。
* **--dry-run:** コマンドを実際には実行せずにシミュレーションします。
* **--dev:** `require-dev` に指定されたパッケージをインストールします。
* **--no-scripts:** `composer.json` で定義されたスクリプトの実行をスキップします。

## require

The `require` command adds new packages to the `composer.json` file from
the current directory.

`require` コマンドは、新しいパッケージを カレントディレクトリの `composer.json`
に追加します。

    $ php composer.phar require

After adding/changing the requirements, the modified requirements will be
installed or updated.

必要なパッケージを 追加/変更 した後に、変更された必要パッケージはインストールか
アップデート されます。

If you do not want to choose requirements interactively, you can just pass them
to the command.

もし、必要パッケージの選択を対話的に行いくない場合は、以下のようにコマンドを
実行してください:

    $ php composer.phar require vendor/package:2.* vendor/package2:dev-master

### Options
### オプション

* **--prefer-source:** Install packages from `source` when available.
* **--dev:** Add packages to `require-dev`.

* **--prefer-source:** 可能であれば、`パッケージを `source` からインストールします。
* **--dev:** `require-dev` にパッケージを追加します。

## search

The search command allows you to search through the current project's package
repositories. Usually this will be just packagist. You simply pass it the
terms you want to search for.

search コマンドは、現在のプロジェクトのパッケージレポジトリから、パッケージバージョンを
検索することができます。 通常は、 packagist から検索されます。単純に、検索したい言葉を
コマンドに渡してください。

    $ php composer.phar search monolog

You can also search for more than one term by passing multiple arguments.

さらに、複数の値を渡すことにより、2つ以上の言葉から検索することができます。

## show

To list all of the available packages, you can use the `show` command.

利用できるパッケージを全て表示する場合は、`show` コマンドを利用することができます。

    $ php composer.phar show

If you want to see the details of a certain package, you can pass the package
name.

もし、特定のパッケージの詳細を見たいばいは、パッケージ名を渡してください。

    $ php composer.phar show monolog/monolog

    name     : monolog/monolog
    versions : master-dev, 1.0.2, 1.0.1, 1.0.0, 1.0.0-RC1
    type     : library
    names    : monolog/monolog
    source   : [git] http://github.com/Seldaek/monolog.git 3d4e60d0cbc4b888fe5ad223d77964428b1978da
    dist     : [zip] http://github.com/Seldaek/monolog/zipball/3d4e60d0cbc4b888fe5ad223d77964428b1978da 3d4e60d0cbc4b888fe5ad223d77964428b1978da
    license  : MIT

    autoload
    psr-0
    Monolog : src/

    requires
    php >=5.3.0

You can even pass the package version, which will tell you the details of that
specific version.

さらに、バージョンを渡すことで、特定のバージョンに関する詳細情報を問い合わせることができます。

    $ php composer.phar show monolog/monolog 1.0.2

### Options

* **--installed:** Will list the packages that are installed.
* **--platform:** Will list only platform packages (php & extensions).

* **--installed:** インストールされたパッケージを表示します。
* **--platform:** (php や extensions) のような プラットフォームパッケージのみを表示します。

## depends

The `depends` command tells you which other packages depend on a certain
package. You can specify which link types (`require`, `require-dev`)
should be included in the listing. By default both are used.

`depends` コマンドは、指定したパッケージに依存するパッケージを問い合わせるものです。
リンクタイプ (`require` や `require-dev`) を問い合わせ時に指定することができます。
デフォルトでは、両方が利用された状態です。

    $ php composer.phar depends --link-type=require monolog/monolog

    nrk/monolog-fluent
    poc/poc
    propel/propel
    symfony/monolog-bridge
    symfony/symfony

### Options
### オプション

* **--link-type:** The link types to match on, can be specified multiple times.

* **--line-type:** マッチさせるリンクタイプ。複数回指定することができます。

## validate

You should always run the `validate` command before you commit your
`composer.json` file, and before you tag a release. It will check if your
`composer.json` is valid.

`composer.json` をコミットする前や、タグをリリースする前に、`validate` コマンドを
毎回実行するべきでしょう。このコマンドは、 `composer.json` が正しいかどうかを
確認することができます。

    $ php composer.phar validate

## self-update

To update composer itself to the latest version, just run the `self-update`
command. It will replace your `composer.phar` with the latest version.

composer 自体を最新のバージョンにアップデートしたい場合は、 `self-update` コマンドを
実行するだけです。これで、 `composer.phar` を最新バージョンに置き換えられます。

    $ php composer.phar self-update

If you have installed composer for your entire system (see [global installation](00-intro.md#globally)),
you have to run the command with `root` privileges

もし、composer をグローバルにインストールした場合 ([グローバルインストール](00-intro.md#グローバル))、
`root` 権限でこのコマンドを実行する必要があります。

    $ sudo composer self-update

## create-project

You can use Composer to create new projects from an existing package.
There are several applications for this:

Composer は、既に存在するプロジェクトから新しいプロジェクトを作成することができます。
以下のような、要件で利用できます:

1. You can deploy application packages.
2. You can check out any package and start developing on patches for example.
3. Projects with multiple developers can use this feature to bootstrap the
   initial application for development.

1. アプリケーションパッケージをデプロイすることができます。
2. どのパッケージもチェックアウトすることができ、試験的なパッチで開発をはじめることができます。
3. 複数の開発者のプロジェクトは、開発のために、最初の初期設定において
   この機能を利用することができます。

To create a new project using composer you can use the "create-project" command.
Pass it a package name, and the directory to create the project in. You can also
provide a version as third argument, otherwise the latest version is used.

Composer をついかい、新しいプロジェクトを作成するときは、 "create-project" を
使うことができます。 パッケージ名を渡すことで、そのパッケージプロジェクトを
ディレクトリに作成します。3つ目の値ではバージョンを指定することができ、
省略した場合、最新版が利用されます。

The directory is not allowed to exist, it will be created during installation.

インストール時に、ディレクトリを作成するため、対象のディレクトリが存在しないように
してください。

    php composer.phar create-project doctrine/orm path 2.2.0

By default the command checks for the packages on packagist.org.

デフォルトでは、packagist.org からパッケージを探します。

### Options
### オプション

* **--repository-url:** Provide a custom repository to search for the package,
  which will be used instead of packagist. Can be either an HTTP URL pointing
  to a `composer` repository, or a path to a local `packages.json` file.
* **--prefer-source:** Get a development version of the code checked out
  from version control.
* **--dev:** Install packages listed in `require-dev`.

* **--repository-url:** packagist より優先的に検索する、カスタムレポジトリを指定
  します。`composer` レポジトリの HTTP URL か、ローカルの `packagis.json` ファイルを
  指定することができます。
* **--prefer-source:** 開発版のコードをバージョンバージョンコントロールから
  チェックアウトします。
* **--dev:** `require-dev` で指定されたパッケージをインストールします。

## dump-autoload

If you need to update the autoloader because of new classes in a classmap
package for example, you can use "dump-autoload" to do that without having to
go through an install or update.

もし、クラスマップを利用するようなパッケージで、新しいクラスを追加するために
オートローダーをアップデートしたい場合、 install や update を用いずに
"dump-autoload" を使うことができます。

Additionally, it can dump an optimized autoloader that converts PSR-0 packages
into classmap ones for performance reasons. In large applications with many
classes, the autoloader can take up a substantial portion of every request's
time. Using classmaps for everything is less convenient in development, but
using this option you can still use PSR-0 for convenience and classmaps for
performance.

さらに、パフォーマンスのために、PSR-0 パッケージをクラスマップのパッケージに
最適化することができます。大きなアプリケーションは大量のクラスがあり、
オートローダーは、リクエスト時間を多く消費する主要なものです。クラスマップを
使うことにより開発は不便になりますが、PSR-0 を使うよりは、パフォーマンスに
有利になります。

### Options
### オプション

* **--optimize:** Convert PSR-0 autoloading to classmap to get a faster
  autoloader. This is recommended especially for production, but can take
  a bit of time to run so it is currently not done by default.

* **--optimize:**  高速なオートロードのために、PSR-0
  オートローディングをクラスマップに変換します。
  これは、特に本番環境での利用が推奨されますが、最適化実行が完了していない
  場合、実行に少し時間がかかります。

## help

To get more information about a certain command, just use `help`.

利用することのできるコマンドを表示する場合は、 `help` を利用してください。

    $ php composer.phar help install

## Environment variables

## 環境変数

You can set a number of environment variables that override certain settings.
Whenever possible it is recommended to specify these settings in the `config`
section of `composer.json` instead. It is worth noting that that the env vars
will always take precedence over the values specified in `composer.json`.

いくつかの環境変数を上書きすることにより、Composer の設定を変更することができます。
可能であれば、 `composer.json` の `config` に設定することが推奨されます。
これは、`composer.json` に設定された環境変数を常時使う場合に、とても便利です。


### COMPOSER

By setting the `COMPOSER` env variable it is possible to set the filename of
`composer.json` to something else.

`COMPOSER` 環境変数を設定することにより、 `composer.json` のファイル名を
別のものに変更することができます。

For example:
例:

    $ COMPOSER=composer-other.json php composer.phar install

### COMPOSER_ROOT_VERSION

By setting this var you can specify the version of the root package, if it can
not be guessed from VCS info and is not present in `composer.json`.

この値を設定することにより、ルートパッケージのバージョンを定義することができます。
もし、VCSの情報や、 `composer.json` に設定されていない場合は、この値を使います。

### COMPOSER_VENDOR_DIR

By setting this var you can make composer install the dependencies into a
directory other than `vendor`.

この値を設定することにより、composer の依存をインストール先を
`vendor` から変更することができます。

### COMPOSER_BIN_DIR

By setting this option you can change the `bin` ([Vendor Bins](articles/vendor-bins.md))
directory to something other than `vendor/bin`.

この値を変更することにより、 `bin` ([Vendor Bins](articles/vendor-bins.md))
ディレクトリの値を、 `vendor/bin` から変更することができます。

### http_proxy or HTTP_PROXY

If you are using composer from behind an HTTP proxy, you can use the standard
`http_proxy` or `HTTP_PROXY` env vars. Simply set it to the URL of your proxy.
Many operating systems already set this variable for you.

もし、composer を HTTP proxy 下で利用したい場合は、環境標準の `http_proxy` か
`HTTP_PROXY` を利用することができます。単純に、proxy の URL をセットしてください。
多くのオペレーションシステムは、既にこの値がセットされています。

Using `http_proxy` (lowercased) or even defining both might be preferable since
some tools like git or curl will only use the lower-cased `http_proxy` version.
Alternatively you can also define the git proxy using
`git config --global http.proxy <proxy url>`.

git や curl といったツールは 小文字の `http_proxy` しかサポートしていないため、
`http_proxy` を設定するか、両方の値を設定することが望ましいでしょう。
ほかに、 `git config --global http.proxy <proxy url>` という
git の設定をすることで git のプロキシの設定を行うことができます。

### COMPOSER_HOME

The `COMPOSER_HOME` var allows you to change the composer home directory. This
is a hidden, global (per-user on the machine) directory that is shared between
all projects.

`COMPOSER_HOME` は、composer のホームディレクトリを変更することができます
これは、隠しグローバルディレクトリ (ユーザごと) によって、全プロジェクトに
横断します。

By default it points to `/home/<user>/.composer` on *nix,
`/Users/<user>/.composer` on OSX and
`C:\Users\<user>\AppData\Roaming\Composer` on Windows.

デフォルトでは、 *nix では、 `/home/<user>/.composer`
OSX では、 `/Users/<user>/.composer`
Windows では、 `C:\Users\<user>\AppData\Roaming\Composer\ です。

#### COMPOSER_HOME/config.json

You may put a `config.json` file into the location which `COMPOSER_HOME` points
to. Composer will merge this configuration with your project's `composer.json`
when you run the `install` and `update` commands.

`config.json` ファイルを `COMPOSER_HOME` で指定したディレクトリに配置することにより
Composer は、 `install` や `update` コマンドを実行した時に、
このファイルの設定を、プロジェクトの `composer.json` とマージします。

This file allows you to set [configuration](04-schema.md#config) and
[repositories](05-repositories.md) for the user's projects.

このファイルには [設定](04-schema.md#config) と [レポジトリ](05-repository.md)
の値をユーザディレクトリで設定することができます。

In case global configuration matches _local_ configuration, the _local_
configuration in the project's `composer.json` always wins.

グローバルの設定と _ローカル_ の設定が競合する場合、 プロジェクトの `composer.json`
にある、 _ローカル_ の設定が常に優先されます。

### COMPOSER_PROCESS_TIMEOUT

This env var controls the time composer waits for commands (such as git
commands) to finish executing. The default value is 300 seconds (5 minutes).

この設定は、 composer がコマンド (gitコマンドなど) の実行に対して
待つ時間を設定します。デフォルトは 300 秒 (5分) です。

&larr; [ライブラリ](02-libraries.md)  |  [スキーマ](04-schema.md) &rarr;
