
# Mackerelの導入

## 用語について

- オーガニゼーション

Mackerelにアカウントを所有するユーザーはサービス全体で一つのアカウントを使用します。

Mackerelでは監視を行う対象の単位として「オーガニゼーション」という
ものがあり、Mackerelのユーザーはこのオーガニゼーションに所属することになります。

またユーザーは、複数のオーガニゼーションに所属することが可能です。

Mackerelでは通常は組織単位ではなく、ITサービスやシステムの単位でオーガニゼーションを構成します。これは、業務委託先に所属するユーザーや、エンドユーザーなど、
運営主体と異なる組織のユーザーをオーガニゼーションに参加可能にするためです。

- ホスト

Mackerelでは監視対象となるホストにエージェントをインストールし、そのエージェントがmackerelのサービスを提供するサーバーと通信を行う事でメトリクスの収集を行います。

Mackerelでは、一ヶ月でのアクティブ ^[通常、mackerel-agentの起動数] なホスト数の移動平均でホスト数を算出し、 ^[[https://mackerel.io/ja/docs/entry/faq/contracts/calculate-host-number](https://mackerel.io/ja/docs/entry/faq/contracts/calculate-host-number)]、算出したホスト数が課金の単位となります。

また、プランごとの各種項目数がプラン上限を超えている場合、ホスト数として換算して課金を行います。^[[https://mackerel.io/ja/docs/entry/faq/contracts/limit-exceeded-conversion](https://mackerel.io/ja/docs/entry/faq/contracts/limit-exceeded-conversion)]

なお課金プランの詳細については、サービス運営元にお問い合わせください。

- メトリック

mackerel-agentが収集するホストの様々なホストの状況をメトリックと呼びます。メトリクス
とも呼ばれますが、Mackerelのサービスにおいてはメトリックと呼ばれるため、本稿でもメトリックという呼び方で統一します。^[[https://mackerel.io/ja/docs/entry/glossary](https://mackerel.io/ja/docs/entry/glossary)]

## Mackerelのセットアップ

※フリープランについて

https://mackerel.io/signup

→ [Mackerel] Please verify your email


```
curl -fsSL https://mackerel.io/file/script/setup-all-yum-v2.sh | MACKEREL_APIKEY='xxx' sh
```

サーバーのプロビジョニングのスクリプトに組み込む等の理由で、
手順を踏んでセットアップを行う場合は、
手動でセットアップする場合

