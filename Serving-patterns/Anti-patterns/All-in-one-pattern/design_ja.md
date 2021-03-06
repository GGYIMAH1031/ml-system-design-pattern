# All-in-one pattern

## Case
- 複数の推論モデルを稼働させるシステムで、全てのモデルが同一のサーバで稼働している状態。

## Situation
1つの目的のために複数の推論モデルを稼働させたいユースケースは存在しますが、全推論モデルを同一サーバで稼働させることは避けたほうが良いでしょう。全推論器を同一環境でモノリシックに稼働させる場合、サーバコストは多少安価に済むかもしれませんが、モデル開発や障害切り分け、更新が難しくなり、人件費が増大するでしょう。<br>
モデル開発のデメリットは環境選択の自由度が制限されることです。機械学習のライブラリやアルゴリズムは日進月歩で更新されています。他のモデルと足並みを揃えて環境構築することは、使えるロジックの制限となり、最適な選択ができなくなる可能性があります。<br>
モノリシックな環境で障害が発生した場合、障害箇所を全てのログから検索し特定する必要があります。システム的な障害切り分けは困難になりますが、同様に機械学習モデルとしての障害（正常な推論が成されていない状況）も、同一環境で全てのロジックをトレースすることになり、複雑性と障害対応時間が増すでしょう。<br>
システムやモデルの更新も同様に複雑かつ時間を要するものになります。モデルの展開方法（[モデル・イン・イメージ・パターン](./../../../Operation-patterns/Model-in-image-pattern/design_ja.md)か[モデル・ロード・パターン](./../../../Operation-patterns/Model-load-pattern/design_ja.md)か）にも依りますが、システム更新と同時にモデル更新が発生し、整合性を検証する必要があります。システムの更新頻度とモデルの更新頻度は一致しないことが多いですが、モノリシックな構成だと両方を同時に更新するため、作業コストが増大します。<br>
複数のモデルを稼働させる場合、特別の理由がない限りは1モデル1推論器のマイクロサービスにして運用することを推奨します。

## Diagram
![diagram](diagram.png)


## Pros
- サーバコストは多少安価。

## Cons
- 開発、運用コストが増大。

## Work around
- 単一責任の原則に則り、マイクロサービスとして開発し、運用する。

## Related design pattern
- [Prep-pred pattern](./../../Prep-pred-pattern/design_ja.md)
- [Microservice vertical pattern](./../../Microservice-vertical-pattern/design_ja.md)
- [Microservice horizontal pattern](./../../Microservice-horizontal-pattern/design_ja.md)