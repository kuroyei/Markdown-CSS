# Markdown CSS

VSCode 拡張機能 [Markdown+Math](https://marketplace.visualstudio.com/items?itemName=goessner.mdmath) で生成した HTML に適用するための CSS である．

## 使用方法

次のコードを Markdown ファイルに貼りつける．

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/kuroyei/Markdown-CSS/mdmath/style.css">
```

## デモ

Markdown でレポートを書く方法を記述している．

- [Markdown](https://github.com/kuroyei/Markdown-CSS/tree/main/mdmath/example.md)
- [HTML](https://kuroyei.com/demo/Markdown-CSS/mdmath/example.html)
- [PDF](https://kuroyei.com/demo/Markdown-CSS/mdmath/example.pdf)

## 印刷時の注意

オプション「背景のグラフィック」を有効にすること．

## 独自のタグ

- **タイトル**

    ```html
    <div id="title">

    タイトル

    </div>
    ```

- **著者と日付**

    ```html
    <div id="author-date">

    3年17席 &emsp; 黒江 遺産

    2024年 5月 16日

    </div>
    ```

- **2カラム**

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

## その他

- 途中の改ページを防ぐ

    ```html
    <div style="break-inside: avoid">

    印刷時に改ページさせたくないコンテンツ

    </div>
    ```

- その場で改ページする

    ```html
    <div style="page-break-after: always;"></div>
    ```

- 目次の作成
  
    VSCode 拡張機能 [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) を用いる．

- Mermaid を埋め込む

    ```html
    <script src="https://unpkg.com/mermaid/dist/mermaid.min.js"></script>
    ```

    ```html
    <pre class="mermaid">
    graph LR;
        A-->B;
        A-->C;
        B-->D;
        C-->D;
    </pre>
    ```

    ただし生成された HTML では Syntax error が発生する場合がある．

    `mermaid.min.js` を読み込む代わりに VSCode 拡張機能 [Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid) をインストールすると得られる `index.bundle.js` (e.g., `"C:\Users\user\.vscode\extensions\bierner.markdown-mermaid-1.23.0\dist-preview\index.bundle.js"`) を次のように読み込むと表示できる．

    ```html
    <script defer src="index.bundle.js"></script>
    ```

    [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) ではこの JavaScript を用いて Mermaid を表示しているようだ．

