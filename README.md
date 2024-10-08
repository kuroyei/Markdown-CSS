# Markdown CSS

Visual Studio Code の拡張機能「Markdown All in One」により Markdown から生成した HTML に対して適用するための CSS である．レポートの作成に使用することを想定している．

## デモ

- [Markdown](https://github.com/kuroyei/Markdown-CSS/blob/main/demo/demo.md?plain=1)
- [HTML](https://kuroyei.com/demo/Markdown-CSS/demo.html)
- [PDF](https://kuroyei.com/demo/Markdown-CSS/demo.pdf)


## インストール

- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
- [Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid) (for Mermaid ダイアグラム)
- [Markdown Emoji](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-emoji) (for 絵文字)
- [Markdown Footnotes](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-footnotes) (for 脚注)

## 設定

<kbd>Ctrl</kbd> + <kbd>,</kbd> により VSCode の設定を開き、拡張機能 Markdown All in One について次のように設定する．

```json
{
  "markdown.extension.print.absoluteImgPath": false,
  "markdown.extension.print.includeVscodeStylesheets": false
}
```

## 使用方法

次のコードを Markdown の先頭に貼り付ける．

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/sindresorhus_github-markdown-css_github-markdown-light.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/style.css">

<style>
:root {
    /* 基本的なフォントファミリー */
    /* --font-base: ; */

    /* 等幅フォントファミリー */
    /* --font-code: ; */

    /* コードブロックのフォントサイズ */
    /* --font-size-codeblock: ; */
}
</style>
```

> [!NOTE]
> 自身でフォント等を変更したい場合は `<style>` を編集する．

## 独自の要素

- 文書名・著者名・日付

    ```html
    <h1 id="title">
    Markdown でレポートを書こう
    </h1>
    <address id="author">
    <span class="mono">4I14</span> &emsp; 黒江 遺産
    </address>
    <time id="date">
    2024年10月8日
    </time>
    ```

- 等幅フォントで表示

    `class="mono"` を指定する．

- 2カラム

    ```html
    <div class="column-wrapper">
    <div class="column-left">

    左側のコンテンツ

    </div>
    <div class="column-right">

    右側のコンテンツ

    </div>
    </div>
    ```

- 途中で改ページさせない

    ```html
    <div class="avoid-break">

    印刷時に改ページさせたくないコンテンツ

    </div>
    ```

- その場で改ページする

    ```html
    <div class="break-after"></div>
    ```

## 置換

> [!NOTE]
> [`.*`] は正規表現を用いることを意味する．

- 画像

    画像の幅を調整できるようにする．また、画像の下にキャプションが表示されるようにする．

    <table>
    <thead>
    <tr>
    <th>Find [<code>.*</code>]</th>
    <th>Replace</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td>

    ```regex
    !\[(.*)\]\((.*?)\)
    ```

    </td>
    <td>

    ```html
    <figure style="width: 70%">
    <img src="$2" alt="$1">
    <figcaption>

    $1

    </figcaption>
    </figure>
    ```

    </td>
    </tr>
    </tbody>
    </table>

## 記法

- [基本的な書き方とフォーマットの構文 - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [情報を表に編成する - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables)
- [コードブロックの作成と強調表示 - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks)
- [ダイアグラムの作成 - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams)

## ロードマップ

- [ ] KaTeX の mhchem extension に対応する
