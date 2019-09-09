# コードレビューで何を期待するべきか



注意: 以下の各ポイントについて考えるときは、必ず[コードレビューの基準](standard.md)を考慮するようにしてください。

## 設計

レビュー中に取り上げるべき最も重要なことは、CL の全体的な設計をどのようにするかということです。CL 中のさまざまなコードのインタラクションは意味のあるものですか？ その変更はコードベースかライブラリ、どちらに帰属するべきものでしょうか？ システムの残りの部分とよく統合されていますか？ その機能を追加するのは本当に今が適切なタイミングですか？

## 機能性

その CL は開発者が意図した通りのことを行っているでしょうか？ 開発者は、そのコードのユーザーにとって、どんなよいことがあると考えていますか？ ここで言う「ユーザー」とは、通常エンドユーザー (もし変更がエンドユーザーに影響する場合) と開発者 (将来このコードを「使う」必要があるユーザーのこと) の双方のことを指します。

ほとんどの場合、私たちレビュアは、開発者がコードレビューを受ける前に CL が正しく動作していることを十分よくテストしていると期待します。しかし、あなたはレビュアとしてさらに、エッジケースについて考え、平行性の問題を探し、自分がユーザーとなったときのことを想像し、コードを読むだけでわかるようなバグが存在しないことを確認しなければなりません。

必要に応じてレビュア自身で CL の動作を検証**してもよい**ですが、レビュアによる CL の動作チェックが最も重要なのは、**UI の変更**のような、ユーザーに直接影響を与えるような変更が含まれている場合です。コードを読むだけでは、一部の変更がユーザーにどのくらい大きな影響を与えるのかを理解するのは困難です。そのような変更に対しては、もし CL にパッチを当てて自分で試してみるのが大変な場合は、開発者に機能性を確認するためのデモを提供するように依頼することが許されます。

他にも、コードレビュー中に機能性について考えるのが特に重要となることがあります。CL の中で行われているある種の **並列プログラミング** が、理論的にデッドロックやレースコンディションを引き起こす可能性があるような場合です。 ある種の問題は、単にコードを実行しただけでは発見するのが非常に困難です。通常、誰か (開発者とレビュアの双方) がそのような平行性の問題が入り込んでいないことを、コード全体を通して注意深く考え抜く必要があります。(これはまた、レースコンディションやデッドロックが起こりうる並行性モデルを使用しない方が良い理由でもあります。そのような並行性モデルを使用すると、コードレビューやコードの理解が非常に複雑になってしまいます。)

## 複雑さ

CL は必要以上に複雑ではないでしょうか？ これは CL のあらゆるレベルで確認してください。1行1行、どの行も複雑ではないですか？ 「複雑すぎる」とは、通常**「コードの読み手が素早く理解できない」**という意味です。また、**「開発者がこのコードを呼び出したり修正しようとしたときにバグが入り込みやすい」**と言うこともできます。

典型的な種類の複雑さは、開発者が必要以上にコードを一般化してしまったり、現在はシステムに必要ではない機能を追加してしまうといった、**オーバーエンジニアリング**です。レビュアは特に、オーバーエンジニアリングに警戒しなければなりません。将来解決する必要がある**かもしれない**と予想される問題ではなく、**今現在**解決する必要があると知っている問題を解決するよう、開発者を促してください。将来の問題は、問題が現れたときに解決されるべきです。問題の具体的な形や要件を確認することができるのは、予想している頭の中ではなく、物理的な宇宙の中においてなのです。

## テスト

Ask for unit, integration, or end-to-end
tests as appropriate for the change. In general, tests should be added in the
same CL as the production code unless the CL is handling an
[emergency](../emergencies.md).

Make sure that the tests in the CL are correct, sensible, and useful. Tests do
not test themselves, and we rarely write tests for our tests—a human must ensure
that tests are valid.

Will the tests actually fail when the code is broken? If the code changes
beneath them, will they start producing false positives? Does each test make
simple and useful assertions? Are the tests separated appropriately between
different test methods?

Remember that tests are also code that has to be maintained. Don't accept
complexity in tests just because they aren't part of the main binary.

## 命名

Did the developer pick good names for everything? A good name is long enough to
fully communicate what the item is or does, without being so long that it
becomes hard to read.

## コメント

Did the developer write clear comments in understandable English? Are all of the
comments actually necessary? Usually comments are useful when they **explain
why** some code exists, and should not be explaining *what* some code is doing.
If the code isn't clear enough to explain itself, then the code should be made
simpler. There are some exceptions (regular expressions and complex algorithms
often benefit greatly from comments that explain what they're doing, for
example) but mostly comments are for information that the code itself can't
possibly contain, like the reasoning behind a decision.

It can also be helpful to look at comments that were there before this CL. Maybe
there is a TODO that can be removed now, a comment advising against this change
being made, etc.

Note that comments are different from *documentation* of classes, modules, or
functions, which should instead express the purpose of a piece of code, how it
should be used, and how it behaves when used.

## スタイル

We have [スタイルガイド](http://google.github.io/styleguide/) at Google for all
of our major languages, and even for most of the minor languages. Make sure the
CL follows the appropriate style guides.

If you want to improve some style point that isn't in the style guide, prefix
your comment with "Nit:" to let the developer know that it's a nitpick that you
think would improve the code but isn't mandatory. Don't block CLs from being
submitted based only on personal style preferences.

The author of the CL should not include major style changes combined with other
changes. It makes it hard to see what is being changed in the CL, makes merges
and rollbacks more complex, and causes other problems. For example, if the
author wants to reformat the whole file, have them send you just the
reformatting to as one CL, and then send another CL with their functional
changes after that.

## ドキュメント

If a CL changes how users build, test, interact with, or release code, check to
see that it also updates associated documentation, including
READMEs, g3doc pages, and any generated
reference docs. If the CL deletes or deprecates code, consider whether the
documentation should also be deleted.
If documentation is
missing, ask for it.

## すべての行 {#every_line}

Look at *every* line of code that you have been assigned to review. Some things
like data files, generated code, or large data structures you can scan over
sometimes, but don't scan over a human-written class, function, or block of code
and assume that what's inside of it is okay. Obviously some code deserves more
careful scrutiny than other code&mdash;that's a judgment call that you have to
make&mdash;but you should at least be sure that you *understand* what all the
code is doing.

If it's too hard for you to read the code and this is slowing down the review,
then you should let the developer know that
and wait for them to clarify it before you try to review it. At Google, we hire
great software engineers, and you are one of them. If you can't understand the
code, it's very likely that other developers won't either. So you're also
helping future developers understand this code, when you ask the developer to
clarify it.

If you understand the code but you don't feel qualified to do some part of the
review, make sure there is a reviewer on the CL who is qualified, particularly
for complex issues such as security, concurrency, accessibility,
internationalization, etc.

## コンテキスト

It is often helpful to look at the CL in a broad context. Usually the code
review tool will only show you a few lines of code around the parts that are
being changed. Sometimes you have to look at the whole file to be sure that the
change actually makes sense. For example, you might see only four new lines
being added, but when you look at the whole file, you see those four lines are
in a 50-line method that now really needs to be broken up into smaller methods.

It's also useful to think about the CL in the context of the system as a whole.
Is this CL improving the code health of the system or is it making the whole
system more complex, less tested, etc.? **Don't accept CLs that degrade the code
health of the system.** Most systems become complex through many small changes
that add up, so it's important to prevent even small complexities in new
changes.

## よいこと {#good_things}

If you see something nice in the CL, tell the developer, especially when they
addressed one of your comments in a great way. Code reviews often just focus on
mistakes, but they should offer encouragement and appreciation for good
practices, as well. It’s sometimes even more valuable, in terms of mentoring, to
tell a developer what they did right than to tell them what they did wrong.

## まとめ

コードレビュー中には、以下のことを保証しなければなりません。

-   コードがよく設計されている。
-   機能がコードの利用者にとってもよいものとなっている。
-   すべての UI の変更は、意味があってよいものに見える。
-   並列プログラミングでは、すべての処理を安全に完了させている。
-   コードが必要以上に複雑ではない。
-   開発者が、現時点で必要かどうかは分からないが、将来必要になる**かもしれない**ものを実装していない。
-   コードに適切なユニットテストが存在する。
-   テストがよく設計されている。
-   開発者がすべてのものに明確な名前を使用している。
-   コメントが明確で役に立つものであり、大部分は**コードの動作 (what)** ではなく**そのコードである理由 (why)** を説明するものとなっている。
-   コードに適切なドキュメントが書かれている (一般には g3doc で)。
-   コードが Google のスタイルガイドに従っている。

レビュアは、レビューを依頼されたコードの**すべての行**をレビューし、**コンテキスト**をしっかり捉えて、**コードの健全性が改善されている**ことを確認し、そして、開発者が行った**よいこと**を褒めてください。

Next: [レビューで CL をナビゲートする](navigate.md)
