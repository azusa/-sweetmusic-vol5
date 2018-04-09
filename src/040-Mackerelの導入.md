\lhead[]{}
\rhead[]{}
\chead[Mackerelの導入]{Mackerelの導入}

# Mackerelの導入

Mackerelの導入方法については「Mackerel サーバ監視［実践］入門」[@Inoue2017] にも記述がありますが、本著においても記述を理解するために必要な範囲についてこの章で説明を行います。

## Mackerelに登録する

新規の登録は、 [https://mackerel.io/signup](https://mackerel.io/signup) より行います。([@fig:img_040_a_image])

![サインアップ画面](img/signup-1.png){#fig:img_040_a_image}

メールアドレスを入力すると、作成するオーガニゼーションの
入力を求められるので、それに従います。([@fig:img_040_b_image])

![オーガニゼーションの入力](img/signup-2.png){#fig:img_040_b_image}

続いてプランの選択に移ります。オーガニゼーションの登録から2週間は
Trialプランとして、全ての機能を制限なく使用することができますので、
Trialプランを選択します。([@fig:img_040_c_image])

![プランの選択](img/signup-3.png){#fig:img_040_c_image}

プランの選択が完了すると、登録したメールアドレスに

>  [Mackerel] Please verify your email


というSubjectのメールが届くので、メール文中の案内にしたがって
アカウントのパスワードの設定を行うと、初期登録は完了です。[@fig:img_040_d_image]

![パスワードの設定](img/signup-4.png){#fig:img_040_d_image}

## mackerel-agentのセットアップ

mackerelにログインすると、ダッシュボードの左下に、

- 「スタートガイド」
- 「新規ホストの登録」

というリンクがあります。セットアップは、このリンクから辿るガイダンスに従って行います。[@fig:img_040_e_image]

![ダッシュボード](img/signup-5.png){#fig:img_040_e_image}

「新規ホストの登録」を選択すると、対象のOSごとにmackerel-agentを
セットアップするためのワンライナーが表示されます。表示されているスクリプトをコピーして、セットアップするホストのプロンプト上で実行します。([@fig:img_040_f_image])

![新規ホストの登録](img/signup-6.png){#fig:img_040_f_image}

なお、ワンライナー中にはmackerelにアクセスするためのAPIキーが含まれているので、公開Gitレポジトリーにコミットして公の場に露出することなどがないよう、扱いには注意してください。

CentOS7のセットアップするワンライナーのスクリプトは、[@lst:code_040_code01]のようになります。

```{#lst:code_040_code01 caption="セットアップするワンライナー"}
curl -fsSL https://mackerel.io/file/script/setup-all-yum-v2.sh | MACKEREL_APIKEY='xxx' sh
```

サーバーをセットアップする(プロビジョニング)のスクリプトに
組み込む等の理由で手順を踏んでセットアップを行う場合があります。
この場合は、「または段階的に新規ホストを登録する」以下の記述に従って、
ホストのセットアップを行います。

以下にCentOS7の場合のセットアップ手順を示します。

Mackerelのyumレポジトリーのセットアップを行います。([@lst:code_040_code02])

```{#lst:code_040_code02 caption="yumレポジトリーのセットアップ"}
 curl -fsSL https://mackerel.io/file/script/setup-yum-v2.sh | sh
```

mackerel-agentのインストールを行います。([@lst:code_040_code03])

```{#lst:code_040_code03 caption="mackerel-agentのインストール"}
sudo yum install -y mackerel-agent
```

続いて、mackerel-agentの初期化を行います。([@lst:code_040_code04])

```{#lst:code_040_code04 caption="mackerel-agentの初期化"}
sudo mackerel-agent init -apikey="(APIキー)"
```

mackerel-agentを起動します。[@lst:code_040_code05]


```{#lst:code_040_code05 caption="mackerel-agentの起動"}
sudo systemctl start mackerel-agent
```

なお、mackerel-agentのログの閲覧は、 `sudo journalctl -u mackerel-agent.service` で行います。


## Windowsへのmackerel-agentの導入

mackerel-agentはMicrosoft Windows(以下Windows)上で動作するホスト上での動作も公式にサポートしています。

Windowsのホストにmackerel-agentを導入するには、「新規ホストの登録」のページ中で「Microsoft Windows」を選択して、「mackerel-agent-latest.msi」をダウンロードし、ガイダンスの指示に従ってインストールを行います。

## ユーザーの招待について

すでに作成されたオーガニゼーションには、オーガニゼーションの管理者が
招待を行うことによってユーザーが加わることができます。

ユーザーの招待は、メニュー左上のオーガニゼーション名をクリックして表示する設定画面で、「メンバー」タブ内の「招待する」ボタンを選択して行います。
