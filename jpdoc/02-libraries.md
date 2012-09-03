# Libraries
# ライブラリ

This chapter will tell you how to make your library installable through composer.
この章では、composer を通してインストールすることができるライブラリの作り方を説明します。

## Every project is a package
## 全てのプロジェクトはパッケージである

As soon as you have a `composer.json` in a directory, that directory is a
package. When you add a `require` to a project, you are making a package that
depends on other packages. The only difference between your project and
libraries is that your project is a package without a name.

`composer.json` がディレクトリに有ると、そのディレクトリはパッケージとなります。
もし、プロジェクトに `require` を追加すると、他のパッケージに依存した、パッケージ
を作成することができます。プロジェクトとライブラリの違いは、プロジェクトには
名前がないということだけです。

In order to make that package installable you need to give it a name. You do
this by adding a `name` to `composer.json`:

インストール可能なパッケージを作成するには、名前をつけてください。これを行うには、
`composer.json` に、  `name` を追加してください:

    {
        "name": "acme/hello-world",
        "require": {
            "monolog/monolog": "1.0.*"
        }
    }

In this case the project name is `acme/hello-world`, where `acme` is the
vendor name. Supplying a vendor name is mandatory.

この場合、プロジェクト名は `acme/hello-world` で、 `acme` は ベンダー名です。
ベンダー名を指定することは必須です。

> **Note:** If you don't know what to use as a vendor name, your GitHub
username is usually a good bet. While package names are case insensitive, the
convention is all lowercase and dashes for word separation.

> **Note:** もし、ベンダー名を何にして良いのかわからないときは、あなたの
Github ユーザ名を使うのが良いでしょう。パッケージ名は大文字小文字を区別しないため、
風習では、全て小文字で、文字の区切りとしてダッシュ (-) を使います。

## Specifying the version
## バージョン定義

You need to specify the package's version some way. When you publish your
package on Packagist, it is able to infer the version from the VCS (git, svn,
hg) information, so in that case you do not have to specify it, and it is
recommended not to. See [tags](#tags) and [branches](#branches) to see how
version numbers are extracted from these.

パッケージのバージョンを定義する場合は幾つかの方法があります。Packagist でパッケージを登録
するとき、VCS (git, svn, hg) のバージョン情報から推測します。したがって、パッケージでバージョン番号を
指定する必要はなく、指定しないことが推奨されています。バージョン番号の抽出方法は
[タグ](#タグ) と [ブランチ](#ブランチ) を御覧ください。

If you are creating packages by hand and really have to specify it explicitly,
you can just add a `version` field:

もし、パッケージを手動で作り、明確にバージョンを定義する場合は、 `version` フィールドを
利用してください:

    {
        "version": "1.0.0"
    }

### Tags
### タグ

For every tag that looks like a version, a package version of that tag will be
created. It should match 'X.Y.Z' or 'vX.Y.Z', with an optional suffix for RC,
beta, alpha or patch.

すべてのバージョンのようなタグは、タグに対応するパッケージバージョンが作成されます。
タグ名は、 'X.Y.Z' か 'v.Y.Z' にマッチするようにして、任意のサフィックスとして
RC、beta、alpha または patch を付加してください。

Here are a few examples of valid tag names:

以下は有効なタグ名の例です:

    1.0.0
    v1.0.0
    1.10.5-RC1
    v4.4.4beta2
    v2.0.0-alpha
    v2.0.4-p1

> **Note:** If you specify an explicit version in `composer.json`, the tag name must match the specified version.
> **Note:** もし `composer.json` にバージョン名を定義する場合は、タグ名は明記したバージョンと同じものにする必要があります。

### Branches
### ブランチ

For every branch, a package development version will be created. If the branch
name looks like a version, the version will be `{branchname}-dev`. For example
a branch `2.0` will get a version `2.0.x-dev` (the `.x` is added for technical
reasons, to make sure it is recognized as a branch, a `2.0.x` branch would also
be valid and be turned into `2.0.x-dev` as well. If the branch does not look
like a version, it will be `dev-{branchname}`. `master` results in a
`dev-master` version.

全てのブランチは、パッケージの開発バージョンが作られます。ブランチ名を
バージョンのように取り扱っている場合、バージョンは `{ブランチ名}-dev` となります
例えば、ブランチが `2.0` である場合、 バージョン名は `2.0.x-dev` となります。
(`.x` は技術的な理由により付け加えられ、 `2.0.x` ブランチも `2.0.x-dev` という
バージョンに変換されます。) もしも、バージョン表記に該当しないブランチは、
`dev-{ブランチ名}` というバージョンになります。 `master` ブランチは、`dev-master` という
バージョンになります。

Here are some examples of version branch names:

以下は、バージョンブランチ名の例です:

    1.x
    1.0 (equals 1.0.x)
    1.1.x

> **Note:** When you install a dev version, it will install it from source.
> **Note:** dev バージョンをインストールする場合、ソースコードからインストールされます。

### Aliases
### エイリアス

It is possible alias branch names to versions. For example, you could alias
`dev-master` to `1.0.x-dev`, which would allow you to require `1.0.x-dev` in all
the packages.

Composer はバージョンにエイリアス名を付けることができます。例えば、 `1.0.x-dev` という
`dev-master` を参照するエイリアスを作成した場合、 パッケージで `1.0.x-dev` という
依存を作成することができます。

See [Aliases](articles/aliases.md) for more information.

詳しくは、 [エイリアス](articles/aliases.md) を御覧ください。

## Lock file
## ロックファイル

For your library you may commit the `composer.lock` file if you want to. This
can help your team to always test against the same dependency versions.
However, this lock file will not have any effect on other projects that depend
on it. It only has an effect on the main project.

ライブラリの場合、 `composer.lock` ファイルは必要なときにコミットする形で
問題ありません。 このファイルは、チーム内で同じ依存バージョンを毎回テストすることを
助けます。 しかし、このロックファイルはプロジェクトの依存に影響を与えません。
メインプロジェクトのみに影響を与えるものなのです。

If you do not want to commit the lock file and you are using git, add it to
the `.gitignore`.

もし、git を使っていてコミットされることを望まない場合は、 `.gitignore` に
`composer.local` を追加してください。

## Light-weight distribution packages
## 軽量配信パッケージ

Including the tests and other useless information like .travis.yml in
distributed packages is not a good idea.

テストや .travis.yml のようなファイルを配信パッケージに含めることは良いことではありません。

The `.gitattributes` file is a git specific file like `.gitignore` also living
at the root directory of your library. It overrides local and global
configuration (`.git/config` and `~/.gitconfig` respectively) when present and
tracked by git.

`.gitattributes` ファイルは、 `.gitignore` のような git 固有のファイルで
ライブラリのルートディレクトリに配置します。 このファイル git で管理され、トラッキングされるとき
は、 ローカルやグローバルの設定を上書きします。 (`.git/config と `~/.gitconfig` のことです)

Use `.gitattributes` to prevent unwanted files from bloating the zip
distribution packages.

`.gitattributes` は zip 配信パッケージを作成するときに、不必要なファイルを
指定するときに利用してください。`

    // .gitattributes
    Tests/ export-ignore
    phpunit.xml.dist export-ignore
    Resources/doc/ export-ignore
    .travis.yml export-ignore

Test it by inspecting the zip file generated manually:

手動で zip ファイルを作成して試してみましょう。

    git archive branchName --format zip -o file.zip

> **Note:** files would be still tracked by git just not included in the
> distribution. This will only work for GitHub packages installed from
> dist (i.e. tagged releases) for now.

> **Note:** git で既にトラッキングされているファイルは、配信に含まれない
> 配信に含まれないファイルであっても、トラッキングされます。 今のところ、
> Github の配信 (i.e. タグ付けされたリリース) をインストールしたときのみ
> 機能するでしょう。

## Publishing to a VCS
## VCSへの公開

Once you have a vcs repository (version control system, e.g. git) containing a
`composer.json` file, your library is already composer-installable. In this
example we will publish the `acme/hello-world` library on GitHub under
`github.com/composer/hello-world`.

一度、 `composer.json` を含んだ vcs レポジトリ (version control system, 例: git)
作成したのであれば、作成したライブラリは既に composer でインストールできるものです。
例えば、 `acme/hello-world` ライブラリは `github.com/composer/hello-world` 上で
配信するものとします。

Now, To test installing the `acme/hello-world` package, we create a new
project locally. We will call it `acme/blog`. This blog will depend on
`acme/hello-world`, which in turn depends on `monolog/monolog`. We can
accomplish this by creating a new `blog` directory somewhere, containing a
`composer.json`:

ここで、`acme/hello-world` パッケージをインストールするために、新しいプロジェクトを
ローカルに作成します。名前を `acme/blog` としましょう。この blog は、
`monolog/monolog` に依存した、 `acme/hello-world` に依存しています。
このようなプロジェクトを作るために、新しく `blog` ディレクトリを作り
以下の様な `composer.json` を作成しましょう。

    {
        "name": "acme/blog",
        "require": {
            "acme/hello-world": "dev-master"
        }
    }

The name is not needed in this case, since we don't want to publish the blog
as a library. It is added here to clarify which `composer.json` is being
described.

まだ blog をライブラリとして公開するつもりはないた、名前は必要ありません。
`composer.json` についてを明記するために追加しています。

Now we need to tell the blog app where to find the `hello-world` dependency.
We do this by adding a package repository specification to the blog's
`composer.json`:

ここで、 blog アプリに、`hello-world` をどこから探せば良いのかを提示する必要があります。
blog の `composer.json` に パッケージのレポジトリ情報を追加しましょう。

    {
        "name": "acme/blog",
        "repositories": [
            {
                "type": "vcs",
                "url": "https://github.com/composer/hello-world"
            }
        ],
        "require": {
            "acme/hello-world": "dev-master"
        }
    }

For more details on how package repositories work and what other types are
available, see [Repositories](05-repositories.md).

さらに、パッケージレポジトリの働きや、ほかの有効なタイプに付いて知りたい場合は、
[レポジトリ](05-repository.md) を御覧ください。

That's all. You can now install the dependencies by running composer's
`install` command!

これで、composer の `install` コマンドによって依存をインストールすることができます。

**Recap:** Any git/svn/hg repository containing a `composer.json` can be added
to your project by specifying the package repository and declaring the
dependency in the `require` field.

**要約:** `composer.json` を含んだ git/svn/hg レポジトリは、あなたのプロジェクトに
パッケージレポジトリを指定して、 `require` フィールドによる依存の宣言を
行うことがｄきます。

## Publishing to packagist
## Packagistへの公開

Alright, so now you can publish packages. But specifying the vcs repository
every time is cumbersome. You don't want to force all your users to do that.

もちろん、あなたは、これまで紹介した方法でパッケージを発行することができます。
しかし、毎回 vcs レポジトリを指定することは、非常にやっかいです。
全てのユーザに強制させたくはないと考えるでしょう。

The other thing that you may have noticed is that we did not specify a package
repository for `monolog/monolog`. How did that work? The answer is packagist.

また、 `monolog/monolog` をインストールするときには、パッケージレポジトリを
指定していないことにあなたは気づいているでしょう。どうなっているのでしょうか。
答えは packagist です。

[Packagist](http://packagist.org/) is the main package repository for
composer, and it is enabled by default. Anything that is published on
packagist is available automatically through composer. Since monolog
[is on packagist](http://packagist.org/packages/monolog/monolog), we can depend
on it without having to specify any additional repositories.

[Packagist](http://packagist.org/) は、composer の中央パッケージレポジトリで、
デフォルトで有効になっています。Pakcagist に公開されたパッケージは自動的に
composer で有効になるということです。 monolog のときは [packagistにあるものを参照し](http://packagist.org/packages/monolog/monolog)
追加のレポジトリの指定なしで、依存を管理することができました。

If we wanted to share `hello-world` with the world, we would publish it on
packagist as well. Doing so is really easy.

もし、`hello-world` をこの world で共有したいのであれば、packagist に登録したほうが
良いでしょう。これは、とても簡単です。

You simply hit the big "Submit Package" button and sign up. Then you submit
the URL to your VCS repository, at which point packagist will start crawling
it. Once it is done, your package will be available to anyone.

Packagist で、大きな "Submit Package" ボタンを押し、サインアップをします。
そして、 VCS レポジトリの URL を送信すると、 Packagist は、クローリングを始めます。
これだけで、誰でもあなたのパッケージを参照することができるのです。

&larr; [基本的な使い方](01-basic-usage.md) |  [CLI](03-cli.md) &rarr;
