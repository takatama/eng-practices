# 小さな CL



## なぜ小さな CLを書くのか？ {#why}

小さく、シンプルな CL とは、次のような CL のことです。

-   **より早くレビューされる。**レビュアが1つの大きな CL をレビューするためにスケジュールに30分のブロックを確保するよりも、5分間でできる小さな CL をレビューを5、6回行う時間を見つける方が簡単です。
-   **より完全にレビューされる。**大きな変更があると、何度も前後に移動しながら分量の多い詳細なコメンタリを行う必要があってストレスがかかる傾向があり、重要な点が見逃されたり抜け落ちてしまう可能性が増します。
-   **バグが入りにくくなる。**より少ない変更しか加えていないため、あなたもレビュアも CL の影響を効果的に考えやすくなり、バグが入り込んでいないか確認しやすくなります。
-   **リジェクトされた場合でも、作業の無駄が少なくて済む。**もし巨大な CL を書いて、その後レビュアがそもそも全体的な方向性が違っていると指摘した場合、あなたはたくさんの作業を無駄にしてしまいます。
-   **よりマージがしやすい。**巨大な CL は作業に長い時間がかかります。そのため、マージするときにたくさんのコンフリクトが生じてしまい、頻繁にマージしなければならなくなります。
-   **より簡単によい設計が行える。**小さいコードの設計やコードの健全性を洗練させるのは、大きな変更を隅々まで洗練させるよりもずっと簡単です。
-   **レビュアのブロッキングを短くできる。**変更全体のうち、自己完結した一部分を送信するようにすれば、現在の CL がレビューされるのを待っている間に、続きのコーディングができるようになります。
-   **ロールバックがよりシンプルになる。**大きな CL は最初の CL 提出時から CL をロールバックするまでの間に更新された複数のファイルを触る可能性が高くなり、ロールバックが複雑になってしまいます (おそらく中間の CL も同時にロールバックしなければならなくなります)。

**レビュアには、ただ CL が大きすぎるというだけの理由で無条件にリジェクトする決定権がある**ということを覚えておいてください。普通は、レビュアはあなたのコントリビューションに感謝し、どうにかして小さな一連の変更に分けられないかとお願いすることになるでしょう。あなたがすでに変更を書き終えた後に分割を行うのにはたくさんの仕事が必要になるかもしれませんし、大きな変更を受け入れるべき理由について議論するのに長い時間が掛かってしまうかもしれません。初めの段階で単に小さい CL を書いた方が簡単です。

## 小さいとはどのくらいか？ {#what_is_small}

一般に、1つの CL の適切なサイズとは、**1つの自己完結した変更**のことです。つまり、次のような変更のことを指します。

-   その CL は、**ただ1つのこと**だけを扱う最小の変更を行っていること。これは通常、ある機能の全体を一度に変更するのではなく、ある機能の1つの部分だけ変更するということです。一般に、小さすぎる CL を書く間違いと、大きすぎる CL を書く間違いの両方を経験した方がいいです。あなたのレビュアと協力して、受け入れられるサイズを見つけましょう。
-   レビュアがその CL について理解する必要がある全ての情報 (将来の開発については除く) は、CL、CL の説明、既存のコードベース、すでにレビュー済みの CL の中に含めること。
-   その CL をチェックインした後でも、ユーザーにとっても開発者にとってもシステムが適切に動作し続けること。
-   その CL が行おうとしていることを理解するのが難しくなるほど小さすぎないこと。もし新しい API を1つ追加する場合、レビュアが API の使われ方をよりよく理解できるように、同じ CL の中に API の使用方法も含めるべきです。これにより、使われない API をチェックインするのを防ぐことにもなります。

どのくらいの大きさが「大きすぎるか」についての厳格なルールはありません。通常、1つの CL に対して 100 行のコードというのは妥当で、1000 行というのは大きすぎますが、最終的にはあなたのレビュアの判断に委ねられます。1 ファイルに対する 200 行の変更は問題ないかもしれませんが、200 行が 50 ファイルに渡って分散している場合は、通常は大きすぎます。

あなたはコードを書き始めた瞬間からそのコードに親しく関わっていても、レビュアにはそのコンテキストが分からないことがよくある、ということを心に留めておきましょう。あなたには受け入れ可能なサイズの CL だと思われても、レビュアには混乱を与えてしまうかもしれません。迷った場合には、自分が書く必要があると思うよりも小さい CL を書くようにしましょう。レビュアが CL が小さすぎると文句を言うことはまれです。

## 大きな CL はどのようなときに認められるのか？ {#large_okay}

次のように、大きな変更が悪くないとされる場合も少しだけあります。

-   1つのファイル全体を削除した場合は、通常1行だけを変更したとして数えます。レビュアがレビューするのに長い時間が掛からないからです。
-   完全に信頼できる自動リファクタリングツールが大きな CL を生成し、レビュアの仕事が単に動作確認を行い、その変更を本当に望んでいる場合。こうした CL は大きくなることがありますが、この場合でも、上に書いたような注意の一部 (マージやテストに関する注意など) は当てはまります。

### ファイルを分割する {#splitting-files}

CL を分割するもう一つの方法は、自己完結した一連の変更を、別々のレビュアを必要とするファイルごとにグループ化することです。

一例としては、1つの CL でプロトコル・バッファの修正を行い、別の CL でその proto を使用するコードの変更を行うようにします。proto の変更の CL は、それを使用するコードの CL よりも先に送信しなければなりませんが、2つの CL を両方同時にレビューすることができるようになります。このように分割した場合、両方のレビュアたちにあなたが書いた他の CL の存在について知らせることで、レビュアたちがあなたの変更のコンテキストを知ることができるようにするといいでしょう。 

別の例としては、1つの CL でコードの変更を行い、別の CL でそのコードを使用する設定や検証を行うようにします。こうすることで、必要があったときにより簡単にロールバックできるようになります。設定や検証のためのファイルは、コードの変更よりも素早く本番環境に投入できるからです。

## リファクタリングを分離する {#refactoring}

It's usually best to do refactorings in a separate CL from feature changes or
bug fixes. For example, moving and renaming a class should be in a different CL
from fixing a bug in that class. It is much easier for reviewers to understand
the changes introduced by each CL when they are separate.

Small cleanups such as fixing a local variable name can be included inside of a
feature change or bug fix CL, though. It's up to the judgment of developers and
reviewers to decide when a refactoring is so large that it will make the review
more difficult if included in your current CL.

## 関連するテストコードを同じ CL の中に含める {#test_code}

Avoid splitting test code into a separate CL. Tests validating your code
modifications should go into the same CL, even if it increases the code line
count.

However, <i>independent</i> test modifications can go into separate CLs first,
similar to the [refactorings guidelines](#refactoring). That includes:

*   validating pre-existing, submitted code with new tests.
*   refactoring the test code (e.g. introduce helper functions).
*   introducing larger test framework code (e.g. an integration test).

## ビルドを壊さない {#break}

If you have several CLs that depend on each other, you need to find a way to
make sure the whole system keeps working after each CL is submitted. Otherwise
you might break the build for all your fellow developers for a few minutes
between your CL submissions (or even longer if something goes wrong unexpectedly
with your later CL submissions).

## 十分小さくできない {#cant}

Sometimes you will encounter situations where it seems like your CL *has* to be
large. This is very rarely true. Authors who practice writing small CLs can
almost always find a way to decompose functionality into a series of small
changes.

Before writing a large CL, consider whether preceding it with a refactoring-only
CL could pave the way for a cleaner implementation. Talk to your teammates and
see if anybody has thoughts on how to implement the functionality in small CLs
instead.

If all of these options fail (which should be extremely rare) then get consent
from your reviewers in advance to review a large CL, so they are warned about
what is coming. In this situation, expect to be going through the review process
for a long time, be vigilant about not introducing bugs, and be extra diligent
about writing tests.

Next: [レビュアのコメントの扱い方](handling-comments.md)
