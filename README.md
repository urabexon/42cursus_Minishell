# 42cursus_Minishell🐚

この課題は、42Tokyo本科Common Core(基礎課程)の中盤に位置するペア課題です。<br>
課題PDFの要件とbashの動作を参考に、簡素化したbashのようなshellをC言語で作成します。<br>
また、この課題の制作過程は別のリポジトリにあります。<br>

- [https://github.com/Yosshii-42/minishell_test](https://github.com/Yosshii-42/minishell_test)

## Usage💻
### 必要条件(readlineのインストール)
`readline` (シェルがコマンドを受け付けるときに使用されます。)
```shell
brew install readline
```

### インストール
このリポジトリをクローンします。
```shell
git clone git@github.com:urabexon/42cursus_Minishell.git
```
このリポジトリにディレクトリを変更します。
```shell
cd minishell
```
コンパイルして実行ファイルを作成します: `minishell`.
```shell
make
```
実行します。
```shell
./minishell
```

## Implementation Function🎓
Bashの基本的な機能を作成しました。
- 適切な実行ファイルを検索して起動する（例：./a.out、/bin/ls ...）
- 組み込み関数： echo, cd, pwd, export, unset, env, exit
- リダイレクトによるファイルI/O管理： >, >>, <, <<
- パイプによるプロセス間通信： |
- シグナル： Ctrl-C、Ctrl-D、Ctrl-C
- シングルクォート/ダブルクォートの有無による環境変数の展開 (例: $PWD, '$PATH', 「$HOME」 ...)
- 終了ステータスの展開: $?

## Working Point💡
42Tokyoの課題では、「Norminette」と呼ばれるコーディング規約があります。<br>
それに準拠する形で記載しなければなりません。

- [https://github.com/42School/norminette/blob/master/pdf/ja.norm.pdf](https://github.com/42School/norminette/blob/master/pdf/ja.norm.pdf)

それに加えて、各課題ごとに使用できる関数が決められており、指定されている関数以外は使用することができません。<br>
その上で、for文の使用が禁止されていたり1つの関数につき25行までの記述制限がされていたりとかなり厳しいものになっており、それらに対応するためにコードをどのようにリファクタリングするかを常に考えました。<br>
非常に頭を悩ませましたが、結果として的確に、短く無駄のないコードを記述する実装力が身についたと感じております。

## Points Learned📋
- そもそもbash、shellとは何か
- 全体構成設計とデータ構造の定義
- シェルの構造
- 字句解析(lexer)
- 構文解析(parser)
- pipeとプロセスのデータのやり取り
- 書き込みや読み取りなどの各権限について
- 環境変数の展開
- シグナル処理
- shellのリダイレクト処理
- fd(ファイルディスクリプタ)の管理やメモリ管理
- リークチェックや統合テストなどの各種テスト
- 複雑かつ曖昧な、巨大なプログラムでのエラーハンドリング
- GitのブランチやGithubのissueといったチーム開発で必要な機能の活用方法
- 進捗とタスク管理
- 話し合いの重要性とチーム開発の楽しさ

## Overall Composition💫
今回の課題では、以下の点に注意しました。
- 課題の上で必須要件、追加要件、実装しない要件(未定義要件)を明確にする。

bashの機能を簡易的に再現するのが課題の目的、趣旨です。<br>
そのためbashそのものを完璧に再現することではありません。<br>
その前提のもと、どのように要件を達成するべきかを考えました。

- shellは基本的にReadline(入力処理) → Lexer(字句解析) → Parser(構文解析) → Expansion(環境変数展開、本来のbashの場合さらに7つの工程に分けられる) → CommandExecution(命令実行) といった工程に分けることができる。
- 課題として*(ワイルドカード)などの対応を行う場合、最初の設計、構造を抽象構文木(ツリー構造、AST)などを使用するため根本から変える必要があるが、未定義要件のためなるべく工程を削減し、動作を再現する方針で進行した。
- 提出したMinishellでは、Readline(入力処理) → Lexer(字句解析) → Expansion(環境変数展開) → CommandExecution(命令実行)といった流れで実行している。

結果として、課題の要件項目は無事達成となりました。<br>
要件としては非常にコンパクトで想定よりも順調なペースで進行することができて良い経験となりました。

## PDF of Design Documents📝
- [simplified_design_documents](simplified_design_documents.pdf)

## Development Members🧑‍💻
- hurabe (データ構造設計、lexer(tokenizer)設計、シグナル設計、各Builtinコマンド作成)
- yotsurud (大枠の全体設計、pipe/プロセス設計、heredoc設計、各Builtinコマンド作成)

## Production Period📅
- 2024/10/11~2024/12/12 (2ヶ月)

## Reference🔖
- [https://aosabook.org/en/v1/bash.html](https://aosabook.org/en/v1/bash.html)
- [https://tiswww.case.edu/php/chet/readline/rltop.html](https://tiswww.case.edu/php/chet/readline/rltop.html)
- [https://www.geeksforgeeks.org/signals-c-language/](https://www.geeksforgeeks.org/signals-c-language/)