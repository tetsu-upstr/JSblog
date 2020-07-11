---
title: Chart.jsでグラフを描く
date: "2020-01-04T17:50:03.284Z"
template: "post"
draft: false
slug: "javascrpit-chartjs"
category: "programming"
tags:
  - "javascript"
description: "この記事では、JavaScriptのグラフ描画ライブラリ「Chart.js」について紹介しています。"
socialImage: "/media/42-line-bible.jpg"
---

JavaScriptのライブラリ「Chart.js」でグラフを表現する方法について確認します。

### Chart.jsとは

「Chart.js」とは、簡単に様々なグラフやチャートが表現できるオープンソースのJavaScriptライブラリです。
棒グラフや折れ線グラフ、レーダー、バブルチャートなど様々なグラフタイプを使用することができます。

### 利用方法
「Chart.js」は、GitHubからダウンロードするか、CDNを使うことができます。

```HTML:title=index.html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.1.4/Chart.min.js"&gt;&lt;/script>
```

このように、シンプルで見やすいグラフを描画できます。

![サンプルグラフ]("../sample_chart.png")

htmlは、canvasタグを埋め込むだけでOKです。

### HTML

CDNでscriptを読み込み、canvasタグを埋め込むだけなので簡単です。

```HTML:title=index.html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>graph</title>
  <link rel="stylesheet" href="style.css">
  <!-- Chart.js CDN -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.1.4/Chart.min.js"></script>
</head>
<body>
  <div class="box">
    <canvas id="graph"></canvas>
  </div>
  <script src="main.js" defer></script>
</body>
</html>
```

### JavaScript
「label」でグラフのラベル、「datasets」でデータの数値をそれぞれ設定できます。

グラフカラーは、「backgroundColor」で変更します。

```javascript:title=main.js
"use strict";

//「月別データ」
var mydata = {
labels: ["1月", "2月", "3月", "4月", "5月", "6月", "7月", "8月", "9月", "10月", "11月", "12月"],
datasets: [
  {
    label: '今年',
    backgroundColor: "rgba(0,0,255,0.5)",
    data: [65, 59, 80, 81, 56, 55, 48, 30, 12, 42, 38, 56],
  },
  {
    label: '昨年',
    backgroundColor: "rgba(0,0,255,0.1)",
    data: [42, 49, 50, 74, 76, 45, 34, 67, 32, 22, 54, 26],
  }
]
};

//「オプション設定」
var options = {
  title: {    
  display: true,
  text: 'サンプルチャート'
  }
};

var canvas = document.getElementById('graph');
var chart = new Chart(canvas, {

type: 'bar',  //グラフの種類
data: mydata,  //表示するデータ
options: options  //オプション設定

});
```

「type：」を変更することで、折れ線グラフなど他のグラフに変更することも可能です。

### オプションの設定

optionsを定義することで、グラフの設定を細かく変更することができます。

```javascript:title=main.js
let options = {
    scales: {
    //  縦軸の設定
      yAxes: [{
        ticks: {
        suggestedMin: 0, // 最小値と最大値の設定
        suggestedMax: 400, // suggestedMax数値が超えても調整してくれる
        stepSize: 100, // 100刻みにしてくれる
        callback: function(value, index, values) {
           return 'JPY ' + value; // 単位を付けられる
        }
        },
        id: 'sales_axes',
        type: 'linear',
        position: 'left'
      }]
    },
    // グラフタイトルの設定
    title: { 
      display: true,
      text: 'Annual Salse',
      fontSize: 18,
      position: 'left' // 横に配置も可能（デフォルトは上）
    },
    legend: {
    position: 'right' // 凡例を右に
    display: false // falseで凡例を消す
    }
  };
```

optionで最小値を設定しないと、最小値がグラフメーターから表示されなくなるので注意が必要です。

suggestedMaxで最大値を指定すると、指定した値を超えてもグラフは表示されます。

### SQLの値からグラフを描画する


`label`と`data`の配列の値を取得して、SQLの値からグラフを動的に描画することも可能です。

phpの記述

```php:title=test.php
<?php
if(isset($_POST['search'])) {
  
  echo
  '<caption class="table-title">販売実績</caption>
    <table class="item-table" id="results">
    <thead>
      <tr>
        <th class="sort" data-sort="name"><span>品名</span></th>
        <th class="sort" data-sort="month"><span>販売月</span></th>
        <th class="sort" data-sort="amount"><span>数量</span></th>
        <th><span>単価</span></th>
        <th class="sort proceeds" data-sort="proceeds"><span>売上金額</span></th>
        <th><span>店舗</span></th>
      </tr>
    </thead>
    <tbody class="list">';

  foreach($result as $row) {
    echo '<tr>';
    echo '<td class="name">' . $row['item_name'] .'</td>';
    echo '<td class="js-sales_month month"><span>' . $row['sale_month'] .'</span></td>';
    echo '<td class="amount">' . $row['amount'] .'</td>';
    echo '<td>' . $row['unit_price'] .'</td>';
    echo '<td class="js-proceeds proceeds"><span>' . $row['proceeds'] .'</span></td>';
    echo '<td>' . $row['store'] .'</td>';
    echo '</tr>';
  }
}
?>
```

Javascriptの記述

```javascript:title=main.js
var label_month = [];
var sales_data = [];

// labelsの値を取得
$('.js-sales_month').each(function(){
  var amount01 = $(this).find('span').text();
  label_month.push(amount01);
})

// dataの値を取得
$('.js-proceeds').each(function(){
  var amount02 = $(this).find('span').text();
  sales_data.push(amount02);
})

var ctx = document.getElementById('myChart').getContext('2d');
var chart = new Chart(ctx, {

  // 作成したいチャートタイプ
  type: 'bar',

  // グラフのデータ
  data: {
      // labels: ['1月', '2月', '3月'],
      labels: label_month,

      datasets: [{
          label: "販売実績の推移",
          backgroundColor: 'rgb(255, 99, 132)',
          borderColor: 'rgb(255, 99, 132)',
          data: sales_data
      }]
  },
```

上記の例では、`find`で`span`内のテキストを見つけて、配列へプッシュしています。