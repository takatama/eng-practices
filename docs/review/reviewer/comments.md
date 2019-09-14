# コードレビューのコメントの書き方



## まとめ

-   やさしさを持ちましょう。
-   あなたの考えの論理を説明しましょう。
-   問題を指摘して明確な方向性を示すことと、開発者自身に決定させることのバランスを取りましょう。
-   レビュアのあなただけに複雑なコードの意味を説明させるのではなく、代わりに開発者に対して、コードをシンプルにしたりコードにコメントを追加してもらうようにしましょう。

## 礼儀

一般に、コードをレビューしている開発者に対しては、非常に明快な態度を取り、助けに満ちた気持ちを示すとともに、丁寧に、尊敬の気持ちを持って接することが大切です。このことを実践する方法の1つは、決して**開発者**についてコメントをしないで、必ず**コード**についてコメントをすることを忘れないことです。このプラクティスには必ず従わなければならないというわけではありませんが、このように話さなければ相手を怒らせてしまったり、争いのもとになってしまう可能性のあることを言う場合には、このプラクティスを絶対に使わなければなりません。以下に例を示します。

悪い例: "どうして**あなたは**ここでスレッドを使用したのですか？ この場所で並列性から得られる恩恵がないのは明らかですよね？"

よい例: "この場所の並列性モデルはシステムに複雑さを加えていますが、私には具体的な性能の恩恵は得られていないように見えます。性能向上が得られない場合には、このコードはマルチスレッドにする代わりにシングルスレッドにするのが最適です。"

## なぜかという理由を説明する {#why}

上の「よい」例で気がつくことの1つは、開発者が**「なぜか」という理由 (why)** を理解することをコメントが助けているという点です。あなたのレビューコメントに常にこの情報を加える必要はありませんが、あなたのコメントの意図、あなたが従っているベストプラクティス、あなたの提案でコードの健康状態がどのように改善するか、などの追加説明を加える方が適切なこともあります。

## ガイダンスを与える {#guidance}

**In general it is the developer's responsibility to fix a CL, not the
reviewer's.** You are not required to do detailed design of a solution or write
code for the developer.

This doesn't mean the reviewer should be unhelpful, though. In general you
should strike an appropriate balance between pointing out problems and providing
direct guidance. Pointing out problems and letting the developer make a decision
often helps the developer learn, and makes it easier to do code reviews. It also
can result in a better solution, because the developer is closer to the code
than the reviewer is.

However, sometimes direct instructions, suggestions, or even code are more
helpful. The primary goal of code review is to get the best CL possible. A
secondary goal is improving the skills of developers so that they require less
and less review over time.

## 説明を受け入れる {#explanations}

If you ask a developer to explain a piece of code that you don't understand,
that should usually result in them **rewriting the code more clearly**.
Occasionally, adding a comment in the code is also an appropriate response, as
long as it's not just explaining overly complex code.

**Explanations written only in the code review tool are not helpful to future
code readers.** They are acceptable only in a few circumstances, such as when
you are reviewing an area you are not very familiar with and the developer
explains something that normal readers of the code would have already known.

Next: [コードレビューでの差し戻しの扱い方](pushback.md)
