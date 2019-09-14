# コードレビューのスピード



## なぜコードレビューは早くなければならないのか？ {#why}

**Google では、開発者のチームが1つの製品を協力して開発する速度を最適化しています。**これは、個人の開発者がコードを書くことができる速度を最適化するのとは逆です。個人の開発者の速度が重要なのは確かですが、チーム全体の速度と**同じくらい**重要というわけではありません。

もしもコードレビューが遅かった場合、以下のような問題が起こってしまいます。

*   **チーム全体の速度が低下してしまう。**たしかに、ある個人がレビューに速やかに返事をしなかったとしても、他の仕事を進めることはできます。しかし、各 CL のレビューや再レビューの遅れが積み重なれば、チームの残りのメンバーが行う新しい機能やバグの修正に、数日、数週間、数ヶ月の遅れが生じてしまいます。
*   **開発者がコードレビューのプロセスに抵抗するようになってしまう。**もしもレビュアが数日に1回しか返事をせず、CL を送るたびに大きな変更を要求するようなことをすれば、開発者には大きなストレスがかかり、変更を加えるのが大変になってしまいます。多くの場合、このような状況は、レビュアの仕事が「厳しすぎる」という不満として現れます。レビュアが**同一の**大きな変更を要求したしても、開発者が変更をするたびに**すみやかに**返事が返ってくれば、不満は無くなる傾向があります。**コードレビューのプロセスに関する不満の大部分は、実際にはレビューのプロセスをすみやかに行うことによって解消されます。**
*   **コードの健康状態に大きな影響を与えてしまう。**レビューが遅いと、開発者に完璧ではない CL を提出しないようにさせる圧力が掛かります。さらに、レビューが遅いと、コードのクリーンアップ、リファクタリング、既存の CL に対する追加の改善をしようとする気持ちも弱めてしまいます。

## コードレビューはどのくらい早くあるべきか？ {#fast}

集中状態にあるタスクがない場合には、**レビュー対象のコードが来たすぐ後にコードレビューを行なわなければなりません。**

コードレビューリクエストに対して、**返事をするまでに掛けることが許される最大の時間は、1営業日です。** (つまり、最低でも翌日最初にするべきです。)

以下のガイドラインに従うならば、通常の CL では、1日の間に (必要があれば) 複数回のラウンドでレビューを行わなければならない、ということになります。

## 速さ vs. 解釈 {#interruption}

There is one time where the consideration of personal velocity trumps team
velocity. **If you are in the middle of a focused task, such as writing code,
don't interrupt yourself to do a code review.** Research has shown that it can
take a long time for a developer to get back into a smooth flow of development
after being interrupted. So interrupting yourself while coding is actually
_more_ expensive to the team than making another developer wait a bit for a code
review.

Instead, wait for a break point in your work before you respond to a request for
review. This could be when your current coding task is completed, after lunch,
returning from a meeting, coming back from the microkitchen, etc.

## 素早い応答 {#responses}

When we talk about the speed of code reviews, it is the _response_ time that we
are concerned with, as opposed to how long it takes a CL to get through the
whole review and be submitted. The whole process should also be fast, ideally,
but **it's even more important for the _individual responses_ to come quickly
than it is for the whole process to happen rapidly.**

Even if it sometimes takes a long time to get through the entire review
_process_, having quick responses from the reviewer throughout the process
significantly eases the frustration developers can feel with "slow" code
reviews.

If you are too busy to do a full review on a CL when it comes in, you can still
send a quick response that lets the developer know when you will get to it,
suggest other reviewers who might be able to respond more quickly, or
[provide some initial broad comments](navigate.md). (Note: none of this means
you should interrupt coding even to send a response like this&mdash;send the
response at a reasonable break point in your work.)

**It is important that reviewers spend enough time on review that they are
certain their "LGTM" means "this code meets [our standards](standard.md)."**
However, individual responses should still ideally be [fast](#fast).

## タイムゾーンを越えるレビュー {#tz}

When dealing with time zone differences, try to get back to the author when they
are still in the office. If they have already gone home, then try to make sure
your review is done before they get back to the office the next day.

## コメント付き LGTM {#lgtm-with-comments}

In order to speed up code reviews, there are certain situations in which a
reviewer should give LGTM/Approval even though they are also leaving unresolved
comments on the CL. This is done when either:

*   The reviewer is confident that the developer will appropriately address all
    the reviewer's remaining comments.
*   The remaining changes are minor and don't _have_ to be done by the
    developer.

The reviewer should specify which of these options they intend, if it is not
otherwise clear.

LGTM With Comments is especially worth considering when the developer and
reviewer are in different time zones and otherwise the developer would be
waiting for a whole day just to get "LGTM, Approval."

## 大きな CL {#large}

If somebody sends you a code review that is so large you're not sure when you
will be able to have time to review it, your typical response should be to ask
the developer to
[split the CL into several smaller CLs](../developer/small-cls.md) that build on
each other, instead of one huge CL that has to be reviewed all at once. This is
usually possible and very helpful to reviewers, even if it takes additional work
from the developer.

If a CL *can't* be broken up into smaller CLs, and you don't have time to review
the entire thing quickly, then at least write some comments on the overall
design of the CL and send it back to the developer for improvement. One of your
goals as a reviewer should be to always unblock the developer or enable them to
take some sort of further action quickly, without sacrificing code health to do
so.

## 時間の経過によるコードレビューの改善 {#time}

If you follow these guidelines and you are strict with your code reviews, you
should find that the entire code review process tends to go faster and faster
over time. Developers learn what is required for healthy code, and send you CLs
that are great from the start, requiring less and less review time. Reviewers
learn to respond quickly and not add unnecessary latency into the review
process.
But **don't compromise on
the [code review standards](standard.md) or quality for an imagined improvement
in velocity**&mdash;it's not actually going to make anything happen more
quickly, in the long run.

## 緊急事態

There are also [緊急事態](../emergencies.md) where CLs must pass through the
_whole_ review process very quickly, and where the quality guidelines would be
relaxed. However, please see [緊急事態とはどのような時か？](../emergencies.md#what) for
a description of which situations actually qualify as emergencies and which
don't.

Next: [コードレビューのコメントの書き方](comments.md)
