# コードレビューでの反対の扱い方



開発者はあなたのコードレビューに反対することがあります。一般には、あなたの提案に同意しなかったり、あなたのレビューが厳しすぎると不満を言う場合などがあります。

## 誰が正しいのか？ {#who_is_right}

開発者があなたの提案に同意しなかったときには、初めに少し立ち止まって、開発者の意見が正しいのではないかとよく考えてください。多くの場合、レビュアのあなたよりも開発者の方がコードに親しんでいるため、コードの特定の側面についてより良い考えを本当に持っているのかもしれません。開発者の意見は意味のあるものとなっているでしょうか？ それは、コードの健康状態という観点からも意味がありますか？ もしそうならば、あなたの意見は正しかったので問題はなくなった、と開発者に伝えましょう。

しかし、開発者が常に正しいとは限りません。その場合、レビュアは、なぜ提案が正しいと信じているのかという理由を、さらに詳しく説明しなければなりません。よい説明というのは、開発者の返信に対する理解を示す言葉と、その変更が必要な理由についての追加情報の両方を含んだものです。

特に、レビュアがその提案によってコードの健康状態を改善できると信じている場合、もしコードの質の改善のために追加の作業を必要とすることを正当化できると信じるならば、レビュアはその変更を主張し続けなければなりません。**コードの健康状態の改善は、小さな一歩から起こるものです。**

本当に開発者の腑に落ちるまでには、数往復をかけて提案を説明しなければならないこともあります。常に[丁寧に](comments.md#courtesy)話し続けることを忘れないでください。そして、単に相手に**同意する**のではなく、あなたがちゃんと開発者が言っていることに耳を傾けて**理解しようとしている**ことが伝わるように心がけてください。

## 怒った開発者 {#upsetting_developers}

Reviewers sometimes believe that the developer will be upset if the reviewer
insists on an improvement. Sometimes developers do become upset, but it is
usually brief and they become very thankful later that you helped them improve
the quality of their code. Usually, if you are [礼儀正しく](comments.md#courtesy) in
your comments, developers actually don't become upset at all, and the worry is
just in the reviewer's mind. Upsets are usually more about
[コメントの書かれ方](comments.md#courtesy) than about the reviewer's
insistence on code quality.

## 後できれいにする {#later}

A common source of push back is that developers (understandably) want to get
things done. They don't want to go through another round of review just to get
this CL in. So they say they will clean something up in a later CL, and thus you
should LGTM *this* CL now. Some developers are very good about this, and will
immediately write a follow-up CL that fixes the issue. However, experience shows
that as more time passes after a developer writes the original CL, the less
likely this clean up is to happen. In fact, usually unless the developer does
the clean up *immediately* after the present CL, it never happens. This isn't
because developers are irresponsible, but because they have a lot of work to do
and the cleanup gets lost or forgotten in the press of other work. Thus, it is
usually best to insist that the developer clean up their CL *now*, before the
code is in the codebase and "done." Letting people "clean things up later" is a
common way for codebases to degenerate.

If a CL introduces new complexity, it must be cleaned up before submission
unless it is an [緊急事態](../emergencies.md). If the CL exposes surrounding
problems and they can't be addressed right now, the developer should file a bug
for the cleanup and assign it to themselves so that it doesn't get lost. They
can optionally also write a TODO comment in the code that references the filed
bug.

## 厳密さに関する一般的な不満 {#strictness}

If you previously had fairly lax code reviews and you switch to having strict
reviews, some developers will complain very loudly. Improving the
[スピード](speed.md) of your code reviews usually causes these complaints to fade
away.

Sometimes it can take months for these complaints to fade away, but eventually
developers tend to see the value of strict code reviews as they see what great
code they help generate. Sometimes the loudest protesters even become your
strongest supporters once something happens that causes them to really see the
value you're adding by being strict.

## 対立を解消する {#conflicts}

以上のすべてに従ってもなお、あなたと開発者との間にある対立が解消できないときは、[コードレビューの基準](standard.md)を読んで、対立を解消するのを助けるガイダンスと原則を確認してください。
