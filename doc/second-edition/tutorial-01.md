<!-- # Tutorial 1 - The Basics -->

# Tutorial 1 - 基本的なこと

<!-- In this first tutorial we are going to create and configure a minimum ClojureScript (CLJS) project by using the boot build tool. -->

まずは [boot][2] というビルドツールを使って、最小限の ClojureScript ([CLJS][1]) のプロジェクトを作ってみよう。

<!-- ## Requirements -->

## 必要な環境

<!-- This tutorial requires java and boot to be installed on your computer. -->

このチュートリアルでは `java` と `boot` が必要だ。

<!-- To install java follow the instructions for your operating system. To install boot follow the very easy instructions in the corresponding section of its README. -->

OS に `java` をインストールするには [instructions][3] を参考にして欲しい。
`boot` のついてはこちらの [README][4] にとても簡単な使い方が書いてあるので参考にして欲しい。

<!-- Test the installation by issuing the boot -h command at the terminal. Then submit the boot -u command to get the latest boot updates. -->

ターミナルで `boot -h` コマンドを試してみよう。
また、最新の `boot` を使うには `boot -u` を実行すればいい。

<!-- NOTE 1: I strongly suggest to use Java 8. If you're using Java 7, it might be worth mentioning https://github.com/boot-clj/boot/wiki/JVM-Options#permgen-errors -->

> NOTE 1: Java 8 を使うことを強く勧める。もし Java 7 を使っているなら、以下のページを参考にしたほうがよい。
> https://github.com/boot-clj/boot/wiki/JVM-Options#permgen-errors

<!-- ## Create the project structure -->

## プロジェクトを作ろう

<!-- A minimum CLJS web project is composed of 3 files: -->

最小限の CLJS プロジェクトは 3 ファイルから構成されている。

<!-- * an html page;
* a CLJS source code;
* a boot build file to compile CLJS source code. -->

* HTML ページ
* CLJS のソースコード
* CLJS のソースコードをコンパイルするための `boot` のビルドファイル

<!-- Even if CLJS does not dictate specific directory structure, it's a
good practice to organize your project in such a way that it will be
easy for anyone, even yourself in a few months, to be able to
understand the project components and its structure. Moreover, each
building tool has its own idiosyncrasies, which they call
defaults. The more you adhere to the defaults of the tool at
hand, the less pain you will experience while managing the project.-->

もし CLJS があるディレクトリ構造に影響していないとしても、
数ヶ月のうちにはプロジェクトの構造と構成を理解することは簡単にできるので
プロジェクトの構造を実際に作ってみるのはよい練習になるだろう。
更に、どのビルドツールもそれぞれ初期設定というクセを持っている。
このツールの初期設定を手近にモノにすればするほど、プロジェクトを管理するのに払う経験が少なくてすむ。

<!-- While taking these premises into account, let's create a directory
structure for our new project, named `modern-cljs`, by adhering as
much as possible to the `boot` defaults. -->

アカウントが既にあるという前提で、`boot` の設定に沿って
`modern-cljs` という新しいプロジェクトのディレクトリを作ってみよう。

<!-- The suggested files layout of the project is the following: -->

プロジェクトのファイルのレイアウトは以下のようにするといい。

```bash
modern-cljs/
├── build.boot
├── html
│   └── index.html
└── src
    └── cljs
        └── modern_cljs
            └── core.cljs
```

<!-- * `modern-cljs` is the home directory of the project;
* `src/cljs/` hosts CLJS source files;
* `html` hosts html resources; -->

* `modern-cljs` はこのプロジェクトのホームディレクトリ。
* `src/cljs/` は CLJS ソースファイルのホストディレクトリ。
* `html` は HTML ファイルのホストディレクトリ。

<!-- > NOTE 2: Single segment namespace are
> [discouraged in CLJ/CLJS][5]. That's why we created the
> `modern_cljs` directory name. Due to [Java difficulties][6] in
> managing hyphen "-" (or other special characters) in package names,
> we substituted an underscore (`_`) for any hyphen (`-`) in
> corresponding directory names. -->

> NOTE 2: シングルセグメントの namespace は [CLJ/CLJS ではお勧めしない][5]。
> それで `modern_cljs` というディレクトリ名にした。
> [Java の問題][6] のせいで、パッケージ名にハイフン "-" (や他の特殊な文字列) をつけると、
> ディレクトリ名のどのハイフン(`-`) も、アンダースコア (`_`) に置換されてしまう。

<!-- > NOTE 3: Please note that the filename extension for ClojureScript
> source is **cljs**, not **clj**. -->

> NOTE 3: ClojureScript のファイル拡張子は **clj** でなく **cljs** であることに注意。

<!-- Issue the following command at the terminal: -->

では、下のコマンドをターミナルで実行してみよう。

```bash
mkdir -p modern-cljs/{src/cljs/modern_cljs,html}
```

<!-- Let's now create the three needed files by issuing the folowing
command: -->

それから、必要なファイルを作ろう。

```bash
cd modern-cljs
touch html/index.html src/cljs/modern_cljs/core.cljs build.boot
```

<!-- ## Hello World in CLJS -->

## CLJS で Hello World しよう

<!-- We're now going to write our very first CLJS code. Open the
`src/cljs/modern_cljs/core.cljs` file with your preferred editor and
type into it the following CLJS code: -->

それでは最初の CLJS コードを書いてみよう。
君の好きなエディタで `src/cljs/modern_cljs/core.cljs` ファイルを開いて、次のコードを書いてみよう。

```clj
;; create the main project namespace
(ns modern-cljs.core)

;; enable cljs to print to the JS console of the browser
(enable-console-print!)

;; print to the console
(println "Hello, World!")
```

<!-- Every CLJ/CLJS file must start with a namespace declaration matching a
path on your disk: -->

CLJ/CLJS ファイルを書くときは、まず始めにディスク上のパスに合った namespace を
宣言することになっている。

`modern-cljs.core` <--> `modern_cljs/core.cljs`

<!-- The `(enable-console-print!)` expression redirects any printing output
to the console of the browser in such a way that the `(println "Hello,
world!")` prints `Hello, World!` to the console. -->

`(enable-console-print!)` 式は、コンソールに `Hello, World!` を出力するために
`(println "Hello, world!")` を書くように、ブラウザのコンソールに出力できるようにする。

<!-- ### Minimal build.boot -->

### 最小限の build.boot

<!-- We now need a way to compile down `core.cljs` to JS and link it to the
`index.html` page. -->

それでは `core.cljs` を JS にコンパイルして `index.html` ページにリンクさせてみよう。

<!-- First, open the file `html/index.html` and edit it as follow: -->

まずはじめに、 `html/index.html` を開いて以下のように書いてみよう。

```html
<!doctype html>
<html>
  <head>
    <title>Hello, World!</title>
  </head>
  <body>
    <script src="main.js"></script>
  </body>
</html>
```
<!-- Note that there are no references to CLJS files. We only added a
`<script>` tag to link the `index.html` page to the `main.js`
file. This JS file will be generated by the `boot` building tool while
compiling the above `core.cljs` source code. -->

これはまだ CLJS を参照していない。
`index.html` ページに `<script>` タグで `main.js` ファイルを指定しただけだ。
この JS ファイルは、`core.cljs` のソースコードがコンパイルされると同時に `boot` ツールで生成される。

<!-- To compile the `core.cljs` file, we need to configure the `boot` command by
editing the `build.boot` file, which is just a regular CLJ file with a
different extension: -->

`core.cljs` ファイルをコンパイルするには、CLJ ファイルとは違った拡張子のこの
 `build.boot` ファイルを編集することで `boot` の設定をすればよい。

```clj
(set-env!
 :source-paths #{"src/cljs"}
 :resource-paths #{"html"}

 :dependencies '[[adzerk/boot-cljs "1.7.170-3"]])

(require '[adzerk.boot-cljs :refer [cljs]])
```

<!--Pretty minimal! The `set-env!` function sets `:source-paths` and
`:resource-paths` options to the corresponding values of the project
structure as we have created above. Then it injects the `boot-cljs`
compilation task as the only explicit dependency of the project by
adding it to the `:dependencies` keyword.-->

ミニマルで良いね! `set-env!` 関数はこれから書くコードのソースパスに相当する
`:source-paths` と `:resource-paths` を設定する。
それから、 `:dependencies` にこのプロジェクトに依存する唯一の
`boot-cljs` コンパイルタスクを追加しよう。

<!--Note that even if we did not include any `clojure` and `clojurescript`
dependencies, `boot` will be able to automagically download the
corresponding releases it knows to work well with it.-->

ここに `clojure` や `clojurescript` を追記しないくても、 `boot` は自動でこれらを
ダウンロードしてちゃんと動くように、よしなにやってくれるので覚えておこう。

<!--Finally, the `require` form makes the `cljs` task visible to the
`boot` command.-->

最期に `boot` コマンドで `cljs` タスクを実行できるように `require` 関数を追記しよう。

<!--If you now run the `boot -h` command from the terminal, you'll see
that the `cljs` task is now available to `boot`.-->

ターミナルで `boot -h` コマンドを実行すると、 `boot` で `cljs` タスクが使えるのが分かるだろう。

```bash
boot -h

...

Tasks:   ...
         target                      Writes output files to the given dir...
         ...
         zip                         Build a zip file for the project.

         cljs                        Compile ClojureScript applications.

...

Do `boot <task> -h` to see usage info and TASK_OPTS for <task>.
Implicit target dir is deprecated, please use the target task instead.
Set BOOT_EMIT_TARGET=no to disable implicit target dir.
```

<!--Note that `boot` notifies a warning saying that using an implicit
target directory is deprecated. Instead you should use the `target`
task and set `BOOT_EMIT_TARGET=no` to disable implicit target
directory generation.-->

`boot` はコンパイル対象のディレクトリを黙示に指定すると警告が出ることを忘れないように。
その場合は `target` タスクを使い、コンパイル対象のディレクトリ生成を明示できるよう
`BOOT_EMIT_TARGET=no` と設定しよう。

<!--When you don't know anything about `boot` build tool, that message has
no meaning at all even if you ask for more information with the
following command:-->

`boot` ツールについてわからなくなったら、次のコマンドでさらに詳しい情報を知ることができる。 

```bash
boot target -h
Writes output files to the given directory on the filesystem.

Options:
  -h, --help      Print this help info.
  -d, --dir PATH  Conj PATH onto the set of directories to write to (target).
  -L, --no-link   Don't create hard links.
  -C, --no-clean  Don't clean target before writing project files.
Implicit target dir is deprecated, please use the target task instead.
Set BOOT_EMIT_TARGET=no to disable implicit target dir.
```

<!--At the moment we don't care about the above deprecation. We only want
to have more information about the `cljs` task by issuing the
following command:-->

今のところは、これ以上は説明しないのだが、次のコマンドにあるように
`cljs` タスクについてはこの程度しか情報がない。

```bash
boot cljs -h
Compile ClojureScript applications.
...
Available --optimization levels (default 'none'):
...
```

<!--As you see, the default optimization directive for the CLJS compiler
is `none`. A next tutorial will explain the different CLJS compilation
optimizations (i.e. `none`, `whitespace`, `simple` and `advanced`). At
the moment stay with `none`, which is commonly used during development
cycles. Let's see `boot cljs` at work:-->

このように、CLJS コンパイラのデフォルト説明は `none` となっている。
次のチュートリアルでは、他の CLJS コンパイルを最適化する方法を説明する。
(例えば、 `none`、`whitespace`、`simple`、そして `advanced` だ。)
現状の開発サイクルの間は `none` で進める。それでは `boot cljs` ではじめよう。

```bash
boot cljs
Writing main.cljs.edn...
Compiling ClojureScript...
• main.js
```

<!--You now know why we called the JS file included in the
`<script>` tag of the `index.html` page `main.js`: just to adhere to an easy
default.-->

これで `index.html` の `<script>` タグに埋め込まれた `main.js` ファイルが呼ばれる。

<!--Let's see what has been generated by the `cljs` compilation task:-->

では、 `cljs` タスクで何が生成されたか見てみよう。

```bash
.
├── build.boot
├── html
│   └── index.html
├── src
│   └── cljs
│       └── modern_cljs
│           └── core.cljs
└── target
    ├── index.html
    ├── main.js
    └── main.out
        ├── boot
        │   └── cljs
        │       ├── main494.cljs
        │       ├── main494.cljs.cache.edn
        │       ├── main494.js
        │       └── main494.js.map
        ├── cljs
        │   ├── core.cljs
        │   ├── core.js
        │   └── core.js.map
        ├── cljs_deps.js
        ├── goog
        │   ├── array
        │   │   └── array.js
        │   ├── asserts
        │   │   └── asserts.js
        │   ├── base.js
        │   ├── debug
        │   │   └── error.js
        │   ├── deps.js
        │   ├── dom
        │   │   └── nodetype.js
        │   ├── object
        │   │   └── object.js
        │   └── string
        │       ├── string.js
        │       └── stringbuffer.js
        └── modern_cljs
            ├── core.cljs
            ├── core.cljs.cache.edn
            ├── core.js
            └── core.js.map

17 directories, 26 files
```

<!--A lot of stuff. We're not digging into it right now. At the
moment we're only interested in noting a few things:-->

たくさんのファイルが作られたようだ。
今すぐは深く掘り下げて見なくてもよい。
今のところはこの 2 つだけわかっていればいい。

<!--* the original directory structure living in `html` and `src` is
  untouched
* everything, even the `index.html` resource, has been generated into
  the new `target` directory. This is the implicit target directory we
  continuously received warning about at any submitted `boot` command.-->
  
* `html` と `src` にあるソースは何も変わっていない。
* `index.html` を含め全てのソースは `target` ディレクトリに作られる。
  このディレクトリは、`boot` コマンドで警告が出ても変わらずコンパイル対象となる。

<!--## Get rid of warnings-->

## 警告が出ないようにしよう

<!--Let's get rid of these warnings. First, delete the `target` directory:-->

警告が出ないように、まずは `target` ディレクトリを削除しよう。

```bash
rm -rf target
```

<!--Then, create a new `boot.properties` file as follows:-->

次に、 `boot.properties` を新しく作ろう。

```bash
boot -V > boot.properties
```

<!-- Finally open the `boot.properties` file to disable the implicit target
directory generation:-->

最後に `boot.properties` にコンパイル対象のディレクトリを明示できるように、次のように追記しよう。

```bash
#http://boot-clj.com
#Sun Jan 03 10:26:34 CET 2016
BOOT_CLOJURE_NAME=org.clojure/clojure
BOOT_CLOJURE_VERSION=1.7.0
BOOT_VERSION=2.5.5
BOOT_EMIT_TARGET=no
```

<!--This way you're pinning the project to the `2.5.5` release of `boot`
which is the latest available at the time of writing. Take into
account that `boot` maintainers are working hard to continuously add
new features and correcting bugs. This means that in a very short time
a new release could be available. `boot` maintainers follow the rules
of [semantic versioning](http://semver.org/). So, to be sure that the
project we're building runs without any problem, the best thing you
can do it's to explicitly pin the project to the above `2.5.5.`
release as follows:-->

こうすることで、今最新の `boot` のリリースバージョン `2.2.5` をプロジェクトで
使うよう指定できる。 `boot` の開発者は続けて機能を追加したりバグをつぶしたりしてくれる。
つまり、頻繁にリリースされ使うことができるのだ。
`boot` の開発者は [セマンティックバージョニング](http://semver.org/) に則って開発を進める。
なので、問題が無い限りは、先ほど指定した `2.2.5` バージョンで進めるのが良い。
 
```bash
BOOT_VERSION=2.5.5 boot -V > boot.properties
```

<!--Obviously you have to re-add the `BOOT_EMIT_TARGET=no` directive as above.-->

こうした後は  `BOOT_EMIT_TARGET=no` の上に追記されるだろう。

```bash
#http://boot-clj.com
#Sun Jan 03 10:26:34 CET 2016
BOOT_CLOJURE_NAME=org.clojure/clojure
BOOT_CLOJURE_VERSION=1.7.0
BOOT_VERSION=2.5.5
BOOT_EMIT_TARGET=no
```

<!--You can now safely relaunch the CLJS compilation by composing the
`cljs` and the `target` tasks within the `boot` command as follows:-->

これで `cljs` と `target` タスクを `boot` コマンドに加えることで、
CLJS を安定してコンパイルするようにできた。

```bash
boot cljs target -d target
Writing main.cljs.edn...
Compiling ClojureScript...
• main.js
Writing target dir(s)...
```

<!--The start has been a little bit over complicated, but we freed ourself
from the above annoying notification about the implicit target
directory been deprecated.

If you take a look at the `modern-cljs` home directory you'll see
again that everything has been generated under the now explicit
`target` directory.-->

これでもううっとうしい警告はもう出ることもなくなった。

`modern-cljs` のホームディレクトリをちらっと見ると、
`target` ディレクトリに全てコンパイルされたのが分かるだろう。

<!--## Visit index.html

`boot` uses a pretty neat approach in taking apart the input of the
project from the corresponding output generated by its tasks. You'll
never see an input file from the `:source-paths` and the
`:resource-path` original directories be modified by any `boot`
task. Aside from internally generated temporary directories,
everything happens into the explicit `target` directory.

Open a browser and visit the local `target/index.html` file. Now open
the console in your Development Tool (e.g. Chrome Development Tool).
If everything went ok, you should see "Hello, World!" printed at the
console.-->

## index.html を開いてみる

`boot` は作ったタスクを使って、指定通りにファイルを生成させてプロジェクトを
すっきりと整理するのに使える。
`boot` タスクを使って `:source-paths` や `:resource-path` を好きなように指定しておけば、
ファイルをいちいち確認しなくてすむ。
一時的に作られるファイルは別として、全てのファイルは `target` ディレクトリにコンパイルされ、
出力される。

ブラウザを開いて `target/index.html` ファイルを開いてみよう。
そしてコンソールのディベロッパーコンソールを開いてみよう(Chrome の開発ツールなど)。
問題なく動いていたら、コンソールに  "Hello, World!" の文字が見えるだろう。

<!--## Next Step - [Tutorial 2: Immediate Feedback Principle][7]-->

## 次回 - [Tutorial 2: すぐ評価しよう][7]

<!--In the next [tutorial][7] we're going to adhere as closely as possible to
the [Bret Victor Immediate Feedback Principle][8] to build a very
interactive development environment.-->

次の[チュートリアル][7] では、[Bret Victor Immediate Feedback Principle][8] のような
とってもインタラクティブな開発環境を作ってみよう。

# License

Copyright © Mimmo Cosenza, 2012-2015. Released under the Eclipse Public
License, the same as Clojure.

[1]: https://github.com/clojure/clojurescript.git
[2]: http://boot-clj.com/
[3]: https://java.com/en/download/help/index_installing.xml?os=All+Platforms&j=8&n=20
[4]: https://github.com/boot-clj/boot#install
[5]: http://stackoverflow.com/questions/13567078/whats-wrong-with-single-segment-namespaces
[6]: http://docs.oracle.com/javase/specs/jls/se8/html/jls-6.html
[7]: https://github.com/naoiwata/modern-cljs/blob/translate-japanese-se/doc/second-edition/tutorial-02.md
[8]: https://vimeo.com/36579366
