# レビュアのコメントの扱い方



レビューのために CL を提出すると、レビュアはあなたの CL にいくつかのコメントを返してくれることがあります。このページでは、レビュアのコメントを扱うときに知っておくと役に立つことを紹介します。

## 個人的なものとして捉えない {#personal}

レビューの目的は、Google のコードベースとプロダクトの品質を維持することです。レビュアがあなたが書いたコードに批判的なコメントを加えるのは、あなた自身やあなたの能力に対して個人的な攻撃をしているからではなく、あなたとコードベースと Google を助けようとしているからだと考えてください。

時には、レビュアが苛立ちを感じてそのいらだちをコメントに表すこともあるかもしれません。それはレビュアにとってよいプラクティスではありませんが、開発者として、あなたはそのようなことがあるという心構えを持たなければなりません。そのようなときには、「レビュアは私に、どんな建設的なことを伝えようとしているのだろう？」と、自分自身に問いかけてみてください。そして、レビュアがその建設的な意見を実際に自分に言ったものとして振る舞ってください。

**コードレビューのコメントに怒りを込めて返事をすることは、絶対にあってはなりません。**万が一そのようなことをしたとすれば、それは、コードレビューツール上に永遠に記録され続ける、プロフェッショナルとしての重大なエチケット違反です。もしあなたが怒ったりイライラして親切に返事をすることができないのなら、丁寧に返事ができるくらい冷静になるまで、しばらくあなたのコンピュータから離れて散歩をしたり、何か他の仕事をしましょう。

一般に、もしレビュアが建設的で丁寧なやり方でフィードバックを提供しないのであれば、直接相手に会ってそのことを説明してください。もし直接またはビデオ会話で相手と話せない場合には、その時は個人的なメールを送ってください。あなたが嫌なことは何なのか、そして、どんな違ったことをレビュアにしてほしいのかを、優しく丁寧に説明してください。もし相手がこの個人的なディスカッションでも非建設的な返事をしたり、意図した結果が得られないならば、そのときは、あなたのマネージャに適切に解決を依頼します。

## コードを修正する {#code}

レビュアにあなたのコードで理解できないところがあると言われた場合、あなたの最初の返事は、コード自体をより明確にするものでなければなりません。もしコードが明確にできない場合、コードがそこにある理由を説明するコードコメントを追加してください。もしコメント無意味なものに思われるなら、その場合にのみコードレビューツール上の返事で説明を行うべきです。

レビュアがあなたのコードの一部を理解できなかった場合、将来コードを読んだ他の人も理解できない可能性があります。コードレビューツール上で返事を書いても将来コードを読む人の助けにはなりませんが、あなたが書いたコードを明確にしたり、コードコメントを追加すれば、彼らを助けることができます。

## よく考える {#think}

Writing a CL can take a lot of work. It's often really satisfying to finally
send one out for review, feel like it's done, and be pretty sure that no further
work is needed. So when a reviewer comes back with comments on things that could
be improved, it's easy to reflexively think the comments are wrong, the reviewer
is blocking you unnecessarily, or they should just let you submit the CL.
However, **no matter how certain you are** at this point, take a moment to step
back and consider if the reviewer is providing valuable feedback that will help
the codebase and Google. Your first question to yourself should always be, "Is
the reviewer correct?"

If you can't answer that question, it's likely the reviewer needs to clarify
their comments.

If you *have* considered it and you still think you're right, feel free to
respond with an explanation of why your method of doing things is better for the
codebase, users, and/or Google. Often, reviewers are actually providing
*suggestions* and they want you to think for yourself about what's best. You
might actually know something about the users, codebase, or CL that the reviewer
doesn't know. So fill them in; give them more context. Usually you can come to
some consensus between yourself and the reviewer based on technical facts.

## コンフリクトを解決する {#conflicts}

Your first step in resolving conflicts should always be to try to come to
consensus with your reviewer. If you can't achieve consensus, see
[The Standard of Code Review](../reviewer/standard.md), which gives principles
to follow in such a situation.
