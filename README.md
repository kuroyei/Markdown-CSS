# Markdown CSS

レポート作成を想定した、VSCode の拡張機能「Markdown All in One」により Markdown から生成した HTML に対して適用するための CSS である．

> [!IMPORTANT]
> 拡張機能によって生成される HTML が異なるため、他の拡張機能では機能しない．

## コンテンツ

- `style.css` : [**@kuroyei**](https://github.com/kuroyei) が作成したもの
- `sindresorhus_github-markdown-css_github-markdown-light.css` : [sindresorhus/github-markdown-css/`github-markdown-light.css`](https://github.com/sindresorhus/github-markdown-css/blob/main/github-markdown-light.css) から文字列 `.markdown-` を取り除いたもの

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
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/default.min.css">

<style>
:root {
    /* 基本フォントファミリー */
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

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> でコマンドパレットを開き、`html` 等と検索して [Markdown All in One: Print current document to HTML] を実行する．

生成された HTML を Web ブラウザで開き、PDF に印刷する．

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
    <div style="flex-basis: 47.5%;">

    左側のコンテンツ

    </div>
    <div style="flex-basis: 47.5%;">

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

- 中央揃えのキャプション付き表

    表を次のタグで囲む．

    ```html


    ```html
    <figure class="">
    
    ```

    ```html

    <figcaption>

    </figcaption>
    </figure>
    ```

    表中の padding を小さくしたい場合は、`figure` にクラス `compact` を指定する．つまり、開始タグを次のようにする．表が表示される大きさを小さくできる．

    ```html
    <figure class="compact">
    
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

## 数式中のフォント

数式中に本文と同じフォントの文字を表示するには、次の命令を使用する．

| フォント | 命令 |
| --- | --- |
| 基本フォントファミリー | `\textsf{}`, `\mathsf{}` |
| 等幅フォントファミリー | `\texttt{}`, `\mathtt{}` |

数式中に本文と同じ大きさの文字を表示するには、`\footnotesize` を使用する．

## KaTeX Macros

[**@kuroyei**](https://github.com/kuroyei) が使用しているマクロをご紹介する．これらはユーザー辞書に登録すると便利である．

| 目的 | マクロ | 例 |
| --- | --- | --- |
| 文字の大きさを本文と同じにする | `\newcommand\ntsize[1]{{\footnotesize #1}}` | `P \ntsize{\textsf{ は正則}}` |
| 単位 | `\def\unit#1{\,\mathrm{\scriptsize [{#1}]}}` | `9.8 \unit{kg \cdot m/s^2}` |
| ネイピア数 | `\def\e{\mathrm{e}}` | `\e^x` |
| 微分、微小量 | `\def\d{\mathrm{d}}` | `\d x` |
| フーリエ変換 | `\def\fourier{\mathcal{F}}` | `\fourier[f(t)]` |
| ラプラス変換 | `\def\laplace{\mathcal{L}}` | `\laplace[f(t)]` |
| 順列 | `\newcommand\perm[2]{{}_{#1}\mathrm{P}_{#2}}` | `\perm{n}{r}` |
| 組合せ | `\newcommand\comb[2]{{}_{#1}\mathrm{C}_{#2}}` | `\comb{n}{r}` |

## 注意

- 印刷時はオプション「背景のグラフィック」を有効にすること．

## CSS が更新されない場合

jsDelivr から取得される CSS が更新されない場合は [Purge CDN cache - jsDelivr](https://www.jsdelivr.com/tools/purge) にてリンクを貼り付け [Purge now] する．複数回試行しなければならない場合がある．

<table>
<thead>
<tr>
<th>CSS</th>
<th>リンク</th>
</tr>
</thead>
<tbody>
<tr>
<td>

[`style.css`](https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/style.css)

</td>
<td>

```plain text
https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/style.css
```

</td>
</tr>
<tr>
<td>

[`sindresorhus_github-markdown-css_github-markdown-light.css`](https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/sindresorhus_github-markdown-css_github-markdown-light.css)

</td>
<td>

```plain text
https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/sindresorhus_github-markdown-css_github-markdown-light.css
```

</td>
</tr>
</tbody>
</table>

<!--

## 配信状況

jsDelivr から取得される CSS が最新であるか

| CSS | 状態 |
| --- | --- |
| [`style.css`](https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/style.css) | |
| [`sindresorhus_github-markdown-css_github-markdown-light.css`](https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/sindresorhus_github-markdown-css_github-markdown-light.css) | |

-->

## 記法

- [基本的な書き方とフォーマットの構文 - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [情報を表に編成する - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables)
- [コードブロックの作成と強調表示 - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks)
- [ダイアグラムの作成 - GitHub Docs](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams)

## ロードマップ

- [ ] KaTeX の mhchem extension に対応する
- [ ] Noto Color Emoji を印刷できるようにする
  - 絵文字を svg に置換する？
- [x] Syntax Highlighting に対応する
