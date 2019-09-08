# コードレビューの基準



コードレビューの主な目的は、Google のコードベースのコード全体の健全性が、時間の経過とともに改善されることを保証することです。コードレビューのツールとプロセスのすべては、この目的のために設計されています。

この目的を達成するには、一連のトレードオフの間でバランスを取る必要があります。

まずはじめに、開発者は自分たちのタスクを**前に進める**ことができなければなりません。もしあなたがコードベースに対する改善を全く提出しなければ、コードベースが改善することは決してありません。また、レビュアが**あらゆる変更**を加えるのを非常に難しくしてしまえば、開発者が将来改善を加えようとするインセンティブが失われてしまいます。

一方で、各 CL が、時間が経過してもコードベースのコード全体の健全性が低下しないような高い品質を備えていることを保証することも、レビュアの義務です。しかし、それはやっかいなことに思われるかもしれません。通常コードベースでは、特にチームが厳しい時間の成約にさらされていて、目標を達成するためにショートカットを使わなければならないと感じているような場合、時間の経過とともに小さな健全性の低下が重なり、コード全体の健全性も少しずつ低下してゆくものだからです。

さらに、レビュアは、自分がレビューしたコード全体に対する所有権と責任を持ちます。レビュアは、コードベースが一貫性を持ち続け、メンテナンス性が維持され、[「コードレビューで何を期待するべきか」](looking-for.md)で言及されている他のすべての事柄についても保証しようとします。

したがって、私たちがコードレビュー中に期待する基準として、次のルールを定めます。

**一般に、ある CL が作業対象のシステムのコード全体の健全性を具体的に向上させる状態に一度でも達したならば、たとえその CL が完璧なものでなくても、レビュアは承認を賛成しなければならない。**

これは、すべてのコードレビューガイドラインの中で**最も**重要な原則です。

この基準にはもちろん制限があります。たとえば、レビュアがシステムに望まない機能を追加する CL であれば、たとえコードがよく設計されていたとしても、レビュアは承認を拒否することができます。

A key point here is that there is no such thing as "perfect" code&mdash;there is
only _better_ code. Reviewers should not require the author to polish every tiny
piece of a CL before granting approval. Rather, the reviewer should balance out
the need to make forward progress compared to the importance of the changes they
are suggesting. Instead of seeking perfection, what a reviewer should seek is
_continuous improvement_. A CL that, as a whole, improves the maintainability,
readability, and understandability of the system shouldn't be delayed for days
or weeks because it isn't "perfect."

Reviewers should _always_ feel free to leave comments expressing that something
could be better, but if it's not very important, prefix it with something like
"Nit: " to let the author know that it's just a point of polish that they could
choose to ignore.

Note: Nothing in this document justifies checking in CLs that definitely
_worsen_ the overall code health of the system. The only time you would do that
would be in an [emergency](../emergencies.md).

## メンタリング

Code review can have an important function of teaching developers something new
about a language, a framework, or general software design principles. It's
always fine to leave comments that help a developer learn something new. Sharing
knowledge is part of improving the code health of a system over time. Just keep
in mind that if your comment is purely educational, but not critical to meeting
the standards described in this document, prefix it with "Nit: " or otherwise
indicate that it's not mandatory for the author to resolve it in this CL.

## 原則 {#principles}

*   Technical facts and data overrule opinions and personal preferences.

*   On matters of style, the [style guide](http://google.github.io/styleguide/)
    is the absolute authority. Any purely style point (whitespace, etc.) that is
    not in the style guide is a matter of personal preference. The style should
    be consistent with what is there. If there is no previous style, accept the
    author's.

*   **Aspects of software design are almost never a pure style issue or just a
    personal preference.** They are based on underlying principles and should be
    weighed on those principles, not simply by personal opinion. Sometimes there
    are a few valid options. If the author can demonstrate (either through data
    or based on solid engineering principles) that several approaches are
    equally valid, then the reviewer should accept the preference of the author.
    Otherwise the choice is dictated by standard principles of software design.

*   If no other rule applies, then the reviewer may ask the author to be
    consistent with what is in the current codebase, as long as that doesn't
    worsen the overall code health of the system.

## 対立の解消 {#conflicts}

In any conflict on a code review, the first step should always be for the
developer and reviewer to try to come to consensus, based on the contents of
this document and the other documents in [The CL Author's Guide](../developer/)
and this [Reviewer Guide](index.md).

When coming to consensus becomes especially difficult, it can help to have a
face-to-face meeting or a VC between the reviewer and the author, instead of
just trying to resolve the conflict through code review comments. (If you do
this, though, make sure to record the results of the discussion in a comment on
the CL, for future readers.)

If that doesn't resolve the situation, the most common way to resolve it would
be to escalate. Often the
escalation path is to a broader team discussion, having a TL weigh in, asking
for a decision from a maintainer of the code, or asking an Eng Manager to help
out. **Don't let a CL sit around because the author and the reviewer can't come
to an agreement.**

Next: [コードレビューで何を期待するべきか](looking-for.md)
