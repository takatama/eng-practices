# 緊急事態

すべてのコードレビューをできるだけ速く行わなければならない、緊急事態の CL というものが存在します。



## 緊急事態とはどのような時か？ {#what}

緊急事態の CL とは、本番環境上でユーザーに非常に大きな影響を与えるバグを修正したり、差し迫った法律上の問題を処理したり、主要なセキュリティホールを修正したりするなど、ロールバックではなく、連続して適用する必要がある変更**小さな**変更のことです。

緊急事態では、私たちは[レスポンスのスピード](reviewer/speed.md)だけではなく、コードレビュープロセス全体のスピードについて極めて慎重になります。レビュアは、レビューの速さと、他の何よりもコードの正しさ (この CL が実際に緊急事態を解決するものとなっているのか？) について注意深く確認しなければなりません。また、(おそらく自明ですが) 緊急事態のレビューは、他のすべてのコードレビューに優先して、CL が送られてきたタイミングで行わなければなりません。

しかし、緊急事態が解消された後には、緊急事態の CL 全体をもう一度見直し、[より完全なレビュー](reviewer/looking-for.md)を行わなければなりません。

## 緊急事態でないのはどのような時か？ {#not}

To be clear, the following cases are *not* an emergency:

-   Wanting to launch this week rather than next week (unless there is some
    actual [hard deadline](#deadlines) for launch such as a partner agreement).
-   The developer has worked on a feature for a very long time and they really
    want to get the CL in.
-   The reviewers are all in another timezone where it is currently nighttime or
    they are away on an off-site.
-   It is the end of the day on a Friday and it would just be great to get this
    CL in before the developer leaves for the weekend.
-   A manager says that this review has to be complete and the CL checked in
    today because of a [soft (not hard) deadline](#deadlines).
-   Rolling back a CL that is causing test failures or build breakages.

And so on.

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
