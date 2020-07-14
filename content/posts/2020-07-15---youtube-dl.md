---
title: "youtubeをダウンロードしてipad(wifiモデル)で観るには"
date: "2020-07-15T22:40:32.169Z"
template: "post"
draft: false
slug: "youtube-dl"
category: "programming"
tags:
  - "youtube"
description: "wifiモデルのipadをスキマ時間のプログラミング学習に使いたいと思い調査しました。"
socialImage: "/media/image-0.jpg"
---

「休憩時間や移動時間などのスキマ時間を利用してプログラミング学習をしたい」

社会人は限られた時間の中で勉強する必要があり、解決策のひとつとしてipadを購入しました。

用途としては、下記のような活用方法を実践していました。

- kindleで技術書を読む
- Qiitaや技術ブログなどのwebクリップ記事をオフラインで読む
- 無料wifiスポットなどを活用して動画学習
- udemyなどの教材をダウンロードして視聴
- podcastをダウンロードしてテクノロジー関係の情報を聴く

## youtubeにある豊富なコンテンツを活用したい

最近ではyoutubeに動画教材をアップロードする方が増えてきました。

特に英語圏の動画は豊富で、「How to build」や「How to create」で検索すると様々なTipsを得るここができます。

私のipadはwifiモデルなので利用できる場所が限られますが、気に入った動画をいつでも繰り返して視聴したいと思うようになりました。

## youtube-dlでyoutube動画をダウンロード視聴

実際にmacOSで試した動画のダウンロード方法をメモとして残します。

### 1.インストール

homebrewでインストールします。

```
brew install youtube-dl
```

[公式ドキュメント](https://ytdl-org.github.io/youtube-dl/download.html)からもダウンロードが可能です。

### 2.使い方

まず、ダウンロードしたいフォルダに移動します。

```
cd Downloads
```

使い方は、ターミナルで下記のように記述するだけでOKです。

```
youtube-dl 動画URL
```



![Nulla faucibus vestibulum eros in tempus. Vestibulum tempor imperdiet velit nec dapibus](/media/image-0.jpg)

```html
<figure>
	<blockquote>
		<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus magna. Cras in mi at felis aliquet congue. Ut a est eget ligula molestie gravida. Curabitur massa. Donec eleifend, libero at sagittis mollis, tellus est malesuada tellus, at luctus turpis elit sit amet quam. Vivamus pretium ornare est.</p>
		<footer>
			<cite>— Aliquam tincidunt mauris eu risus.</cite>
		</footer>
	</blockquote>
</figure>
```
