# ページを作成する

## インストール後

インストール後、GROWI の URL へアクセスすると、管理者 ID を設定する画面が表示されます。

管理者 ID を入力し、GROWI へログインすると以下の画面が表示されます。

<img :src="$withBase('/assets/images/install.png')" alt="start">

ここからチュートリアルを開始します。

管理者設定については[管理者ガイド](/ja/admin-guide/management-cookbook/app-settings.html)をご参照ください。

## 新規ページ作成

GROWI は、wiki ページを作成するシステムです。

まずは新規ページを作成しましょう。


<img :src="$withBase('/assets/images/create.png')" alt="create">

画面右上の「作成」ボタンをクリックすると、ページ作成が表示されます。

<img :src="$withBase('/assets/images/create_page1.png')" alt="create">

「ページを以下に作成」の入力欄に「チュートリアル」と入力し、作成ボタンをクリックします。

<img :src="$withBase('/assets/images/create_page2.png')" alt="create">

ページの編集画面が表示されます。

以下の Markdown 記述の内容をコピーして、GROWI の編集画面へ貼りつけてみましょう。

```

# はじめてのページ
## 見出し1

* 箇条書き1
* 箇条書き2

## 見出し2

1. 番号リスト  
2. 番号リスト

```

<img :src="$withBase('/assets/images/tutorial_page1.png')" alt="page">

貼り付けると、下記のように内容がリアルタイムに反映されたプレビューが画面右側に表示されます。

実際に編集画面で文字を入力し、右側のプレビュー画面への反映を確認しましょう。

編集したら、「作成」ボタンをクリックします。

<img :src="$withBase('/assets/images/tutorial_page2.png')" alt="page">

クリックすると、記事が作成され、画像のようにページが参照できるようになります。

「編集」タブと「View」タブを切り替えて、編集モードと View モードにできます。

早速作成したページを編集しましょう。

## 見出しと階層化

ページには半角シャープを使って見出しを付ける事ができます。

半角シャープは 2つ、3つと増やすごとに、階層化されます。

<img :src="$withBase('/assets/images/tutorial_page2.png')" alt="page">

見出しを作成すると、ページ右側に索引が自動的に作成されるので、積極的に活用しましょう。

## 文書と階層化

ページにはテキスト文書を記載できます。また、その文書は階層化ができます。

半角ハイフン、半角アスタリスクのいずれかを利用して、段落を利用してみましょう。

```

# GROWI の使い方を学ぶ

このページでは、GROWI Docs のチュートリアルに沿って GROWI の使い方を学びます。

## ページの作成と編集

ページを作成して編集します。

## 見出しと本文の使い方
見出しと本文の使い方を学びます。

### 見出し
見出しを作成すると、ページ右側に索引が作成されます。

### 本文
本文として、文章をページへ記載します。文章は段落にできます。

以下のいずれかの記号と半角スペースで、段落を作成できます。

- 半角ハイフン`-`
- 半角アスタリスク`*`
    - さらに階層化
        - そのまた更に階層化
    - 階層をひとつ戻す

```

一つ目の段落の次の行を開始する時に、半角スペースを2つまたは Tab キーを入力してインデントして文章を書いてください。


<img :src="$withBase('/assets/images/edit_text.png')" alt="text">

階層化された文書がプレビュー画面で確認できます。

本文の階層化で、文書の内容を整理しましょう。

<img :src="$withBase('/assets/images/view_text.png')" alt="text">

文章が長くなったら、積極的に階層化するのも読みやすい wiki 作成のポイントです。

## Web ページへのリンクを作成

- Wiki ページへのリンクを作成
  
  編集画面上部のボタンで、リンク用の入力欄が挿入されます。 `[]` 括弧と `()` 括弧をつなげるとリンクが作成できます。

  `[]` の中にタイトルを、`()` の中にページ URL を作成します。

  ```

  入力欄
  []()

  [GROWI Docs](https://docs.growi.org/)
  ```

<img :src="$withBase('/assets/images/add_link.png')" alt="link">


- 手書きで文字とリンクを作成

  手書きで `[]` と `()` 記号を組み合わせてリンクを作成できます。

```

  [タイトル](http://growi.org)

```

## 画像を挿入する

- 画像参照ボタンで画像挿入欄が挿入されます。エクスクラメーションと `[]` 括弧と `()` 括弧をつなげると画像挿入ができます。

```

### 画像の挿入

  ![]()

  ![growi](https://growi.org/assets/images/logo.png)

```

<img :src="$withBase('/assets/images/add_image.png')" alt="image">

- 編集画面下部の Attach 機能を利用する


<img :src="$withBase('/assets/images/attach.png')" alt="attach">

  Attach 機能では、ファイルをアップロードし、AWS や GCS へ保存できます。
  Attache 機能でファイルをアップロードするには管理画面で設定が必要です。

  設定方法については[こちら](/ja/admin-guide/admin-cookbook/attachment.html)をご覧ください。

::: tip
ページを新規作成する画面で画像を添付すると、自動的にページが保存され、公開範囲が **自分のみ** に変更されます。
公開範囲については[こちら](/ja/guide/features/authority.html#%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AB%E5%AF%BE%E3%81%99%E3%82%8B%E9%96%B2%E8%A6%A7%E3%83%BB%E7%B7%A8%E9%9B%86%E6%A8%A9%E9%99%90%E3%81%AE%E8%A8%AD%E5%AE%9A%E6%96%B9%E6%B3%95)をご覧ください。
:::

## 絵文字(emoji) を使う

GROWI では、絵文字を利用できます。

- 使い方

```

## 絵文字を使う　:beginner:

```

<img :src="$withBase('/assets/images/use_emoji.png')" alt="emoji">

上記のように、特定の絵文字を `:` で囲い利用できます。

対象の絵文字一覧は[こちら](/ja/guide/features/emoji.html)を参照してください。

## 便利な本文の使い方

GROWI では、本文の編集時に多数のテクニックで文章を読みやすくできます。

- 強調
- 強調太字
- 強調赤字背景反転
- 水平線
- 取り消し線
- 段落強調

それぞれ、以下の Markdown 記述をそのまま記事へ貼り付けて、実際にプレビューを確認してみましょう。


```
### 便利な本文の使い方
いろいろな文章や段落の便利な書き方を紹介します。

- 強調

  **強調** したい箇所を半角アスタリスク2つで囲います。
  
    ```
    **強調**
    ```
  
  
- 強調赤字背景反転

  `強調` したい箇所をバッククォートで囲います。
  
    ```
    `強調`
    ```

  
- 水平線
  
  半角ハイフンを3つ連続して書くと、水平線となります。
  
  ---
  
- 取り消し線
  
  文章の中で~~消したい~~取り消し線を付けたい箇所を半角チルダ2つで囲います。
  
- 段落強調

  段落として背景反転して協調できます。
  バッククオート3つで囲います。
```

## テーブルを作成する

以下の2種類の方法で、テーブルを作成できます。

- 半角パイプライン`|` を2つ続けて入力し、Enter キーを押す
- 編集画面のバーにあるテーブルボタンをクリック

<img :src="$withBase('/assets/images/edit_table1.png')" alt="table1">

<img :src="$withBase('/assets/images/edit_table2.png')" alt="table2">

## テーブルを編集する

作成したテーブルを、View モードの画面から編集できます。

View モードでテーブルにカーソルを当てると、下記のようにアイコンが表示されます。

<img :src="$withBase('/assets/images/edit_table3.png')" alt="table3">

クリックすると、下記のようにテーブルを編集できます。

<img :src="$withBase('/assets/images/edit_table4.png')" alt="table4">

## ページ一覧を出力する

GROWI では、作成したページを一覧出力する便利な機能があります。

詳細は[こちら](/ja/guide/tips/hierarchical.html)に記載されています。

簡単な使い方だけ覚えましょう。

トップページへ移動し、下記のように lsx を記載しましょう。

```

$lsx()

```

<img :src="$withBase('/assets/images/lsx_sample.png')" alt="lsx">

すると、編集中の記事の配下のページ一覧が出力されます。

一覧出力してみると、ページを移動して階層をもっとカスタマイズしたくなります。

階層の修正やページの移動については[こちら](/ja/guide/features/page_operation.html)を参照してください。

さまざまな階層を整理して、GROWI での情報共有がもっと手軽になるように、自由に編集できます。

ここまでチュートリアルに沿って進めたら、どんどんページを作成して Wiki を育てていきましょう。
