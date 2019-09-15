# 緊急事態

すべてのコードレビューをできるだけ速く行わなければならない、緊急事態の CL というものが存在します。



## 緊急事態とはどのような時か？ {#what}

緊急事態の CL とは、本番環境上でユーザーに非常に大きな影響を与えるバグを修正したり、差し迫った法律上の問題を処理したり、主要なセキュリティホールを修正したりするなど、ロールバックではなく、連続して適用する必要がある変更**小さな**変更のことです。

緊急事態では、私たちは[レスポンスのスピード](reviewer/speed.md)だけではなく、コードレビュープロセス全体のスピードについて極めて慎重になります。レビュアは、レビューの速さと、他の何よりもコードの正しさ (この CL が実際に緊急事態を解決するものとなっているのか？) について注意深く確認しなければなりません。また、(おそらく自明ですが) 緊急事態のレビューは、他のすべてのコードレビューに優先して、CL が送られてきたタイミングで行わなければなりません。

しかし、緊急事態が解消された後には、緊急事態の CL 全体をもう一度見直し、[より完全なレビュー](reviewer/looking-for.md)を行わなければなりません。

## 緊急事態でないのはどのような時か？ {#not}

緊急事態について明確にするために、以下に緊急事態**ではない**ような場合を挙げます。

-   来週ではなく今週中に、新機能を立ち上げたいと望んでいる場合 (パートナー契約などの具体的な[ハード・デッドライン](#deadlines)が存在する場合を除く)。
-   開発者が1つの機能に非常に長い時間、取り掛かり続けており、CL を取り込んでほしいと心から願っている場合。
-   現在、レビュアの全員が深夜や勤務時間外である別のタイムゾーンにいる場合。
-   金曜日の1日の終りで、週末に開発者が離れる前にぜひとも取り込んでおきたい CL がある場合。
-   [ソフト・デッドライン (ハード・デッドラインではない)](#deadlines) が存在するため、マネージャが今日中にこのレビューを完了させて CL をチェックインする必要がある、と言っている場合。
-   テストの失敗やビルドの破壊を起こした CL をロールバックする場合。

などなど。

## ハード・デッドラインとは何か？ {#deadlines}

A hard deadline is one where **something disastrous would happen** if you miss
it. For example:

-   Submitting your CL by a certain date is necessary for a contractual
    obligation.
-   Your product will completely fail in the marketplace if not released by a
    certain date.
-   Some hardware manufacturers only ship new hardware once a year. If you miss
    the deadline to submit code to them, that could be disastrous, depending on
    what type of code you’re trying to ship.

Delaying a release for a week is not disastrous. Missing an important conference
might be disastrous, but often is not.

Most deadlines are soft deadlines, not hard deadlines. They represent a desire
for a feature to be done by a certain time. They are important, but you
shouldn’t be sacrificing code health to make them.

If you have a long release cycle (several weeks) it can be tempting to sacrifice
code review quality to get a feature in before the next cycle. However, this
pattern, if repeated, is a common way for projects to build up overwhelming
technical debt. If developers are routinely submitting CLs near the end of the
cycle that "must get in" with only superficial review, then the team should
modify its process so that large feature changes happen early in the cycle and
have enough time for good review.
