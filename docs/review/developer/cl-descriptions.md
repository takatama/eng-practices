# よい CL の説明を書く

CL の説明 (description) とは、**何を (what)** 変更したのか、それが **なぜ (why)** 変更されたのかについてのパブリックな記録です。Google のバージョン管理の歴史の永続的な一部となるものであり、何年にも渡って、あなたのレビュア以外にも数百人の人たちに読まれる可能性があるものです。

将来の開発者は、あなたの説明に基づいて CL を検索することになります。たとえば、将来誰かが、手元に詳細な情報がない状態で、かすかな記憶を頼りにあなたの CL を探すことになるかもしれません。もし重要な情報のすべてがコードの中にしか存在せず、説明の中に書かれていなければ、あなたの CL を発見するのは極めて困難なものとなってしまいます。

## 1行目 {#firstline}

*   行われたことについての短い要約。
*   命令形で書かれた完全な文。
*   空行を続ける。

CL の説明の**1行目**は、「その CL によって具体的に**何が**なされたのか」についての短い要約でなければなりません。その後ろには1行の空行を続けます。将来のコードの検索者のほとんどは、コードのバージョン管理のヒストリーを閲覧しているときにこれを目にすることになります。そのため、この1行目は、CL や説明の全文を読まなくても、あなたの CL が実際に何を「行った」のかを理解できるほど十分な情報を含んでおり、参考になるものでなければなりません。

伝統的に、CL の説明の1行目は、命令形で書かれた完全な文として書きます。たとえば、\"**Deleting** the FizzBuzz RPC and **replacing** it with the new system." ではなく、\"**Delete** the FizzBuzz RPC and **replace** it with the new system." と言います。(「FizBuzz RPC を削除し、新しいシステムで置換する。」) しかし、説明の残りの部分は命令形で書く必要はありません。

## 本文は informative である {#informative}

説明の残りの部分は、十分な情報を含んでおり参考になる (informative) ものでなければなりません。解決した問題の簡単な説明や、なぜそれが最適なアプローチであるかの説明になるかもしれません。もしそのアプローチに欠点があれば、その欠点に言及しなければなりません。関連することであれば、バグ番号やベンチマークの結果、設計ドキュメントへのリンクなどのバックグラウンドの情報も含めます。

たとえ小さな CL であっても、詳細について注意を向けることには価値があります。CL をコンテキストの中に置いてください。

## 悪い CL の説明 {#bad}

"Fix bug" というのは、不適切な CL の説明です。どんなバクなのでしょうか？ そのバグを修正するためにどんなことをしたのでしょうか？ その他の悪い説明としては、次のようなものがあります。

-   "Fix build." (ビルドを修正する。)
-   "Add patch." (パッチを追加する。)
-   "Moving code from A to B." (コードを A から B に移動する。)
-   "Phase 1." (フェーズ1。)
-   "Add convenience functions." (便利な関数を追加する。)
-   "kill weird URLs." (おかしな URL を削除する。)

これらの一部は実際にあった CL の説明です。CL の作者は役に立つ情報を提供していると信じていたのかもしれませんが、CL の説明の目的を果たせていません。

## よい CL の説明 {#good}

以下によい説明の一例を挙げます。

### 機能の変更

> rpc: remove size limit on RPC server message freelist.
>
> Servers like FizzBuzz have very large messages and would benefit from reuse.
> Make the freelist larger, and add a goroutine that frees the freelist entries
> slowly over time, so that idle servers eventually release all freelist
> entries.

最初の文は、この CL が実際に何を行ったのかを説明しています。説明の残りの部分では、解決した問題、なぜこれが良い解決方法であるのか、そして、特定の実装に関してさらに詳しい情報が書かれています。

### リファクタリング

> Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
>
> Add a Now method to Task, so the borglet() getter method can be removed (which
> was only used by OOMCandidate to call borglet's Now method). This replaces the
> methods on Borglet that delegate to a TimeKeeper.
>
> Allowing Tasks to supply Now is a step toward eliminating the dependency on
> Borglet. Eventually, collaborators that depend on getting Now from the Task
> should be changed to use a TimeKeeper directly, but this has been an
> accommodation to refactoring in small steps.
>
> Continuing the long-range goal of refactoring the Borglet Hierarchy.

最初の文は、CL が何を行い、過去のコードからどのように変更されたかを説明しています。説明の残りの部分では、この CL のコンテキストで、特定の実装について解決策が理想的ではないこと、そして将来の可能な方向性について書かれています。また、この変更が**なぜ**なされたのかも説明しています。

The first line describes what the CL does and how this is a change from the
past. The rest of the description talks about the specific implementation, the
context of the CL, that the solution isn't ideal, and possible future direction.
It also explains *why* this change is being made.

### コンテキストが必要な小さな CL

> Create a Python3 build rule for status.py.
>
> This allows consumers who are already using this as in Python3 to depend on a
> rule that is next to the original status build rule instead of somewhere in
> their own tree. It encourages new consumers to use Python3 if they can,
> instead of Python2, and significantly simplifies some automated build file
> refactoring tools being worked on currently.

最初の文は、実際に行われたことを説明しています。説明の残りの部分では、**なぜ**その変更が行われたかを説明し、レビュアに多くのコンテキストを提供しています。

## CL を送信する前に説明を見直す

CL は、レビュー中に大幅に変更される可能性があります。CL を送信する前には、現在でも説明が実際に CL が行っていることを正しく反映しているか、CL の説明を見直す価値があります。

Next: [小さな CL](small-cls.md)
