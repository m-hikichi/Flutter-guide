# ListView

## ListViewとは何か？

ListViewは、Flutterウィジェットの一つで、一連のアイテムをスクロール可能なリストとして表示するためのものです。このリストは、画面内に収まりきらないアイテムに対してもスクロール機能を提供し、リストを効率的に表示できるようにします。このガイドでは、ListViewを使ってツイートやYouTubeのコメントなどを効果的に表示する方法を説明します。

## 仮想スクロールとは？

画面外にあるアイテムを描画せずに、画面内に収まるアイテムだけを描画する仕組みです。この機能により、無駄な描画処理を最小限に抑えることができます。

## 無限スクロールを実現する

無限スクロールを実現するためには、サーバからモデルを読み込み、描画を行う必要があります。ListView.builderウィジェットを使用して、アイテムがスクロールされるたびに新しいモデルを読み込み、リストに追加することができます。

## 準備

### クラスの定義

以下は、ツイートを表すTweetクラスの定義です。

```dart
class Tweet {
  // ユーザの名前
  final String userName;
  // アイコン画像
  final String iconUrl;
  // ツイートメッセージ
  final String text;
  // 送信日時
  final String createDateTime;

  // コンストラクタ
  Tweet(this.userName, this.iconUrl, this.text, this.createDateTime);
}
```

### モデルの準備

通常はサーバから取得します。

```dart
final models = [
  Tweet('ルフィ', 'images/banana.png', '海賊王におれはなる！', '2022/1/1'),
  Tweet('ゾロ', 'images/banana.png', 'おれはもう！二度と敗けねェから！', '2022/1/2'),
  Tweet('ナミ', 'images/banana.png', 'もう背中向けられないじゃないっ！', '2022/1/3'),
];
```

### モデルをウィジェットに変換する

ツイートモデルをウィジェットに変換する関数を作成します。

```dart
Widget modelToWidget(Tweet model) {
  // model を使って好きな Widget を作る
}
```

### ListViewを使用

最後に、ListView.builderを使用してリストビューを構築します。これにより、モデルの数だけアイテムが表示され、スクロール時に新しいアイテムを追加できます。

```dart
final list = ListView.builder(
  itemCount: // モデルの数,
  itemBuilder: (c, i) => modelToWidget(models[i]),
);
```

## サンプルコード

```dart
import 'package:flutter/material.dart';

// ツイート
class Tweet {
  // ユーザの名前
  final String userName;
  // アイコン画像
  final String iconUrl;
  // ツイートメッセージ
  final String text;
  // 送信日時
  final String createDateTime;

  // コンストラクタ
  Tweet(this.userName, this.iconUrl, this.text, this.createDateTime);
}

final tweets = [
  Tweet('ルフィ', 'images/banana.png', '海賊王におれはなる！', '2022/1/1'),
  Tweet('ゾロ', 'images/banana.png', 'おれはもう！二度と敗けねェから！', '2022/1/2'),
  Tweet('ナミ', 'images/banana.png', 'もう背中向けられないじゃないっ！', '2022/1/3'),
  Tweet('ウソップ', 'images/banana.png', 'お前らの”伝説のヒーロー”になってやる！', '2022/1/4'),
  Tweet('サンジ', 'images/banana.png', 'たとえ死んでもおれは女は蹴らん・・・！', '2022/1/5'),
  Tweet('チョッパー', 'images/banana.png', '人間ならもっと自由だ！', '2022/1/6'),
  Tweet('ビビ', 'images/banana.png', 'もう一度仲間と呼んでくれますか!?', '2022/1/7'),
  Tweet('ロビン', 'images/banana.png', '生ぎたいっ！', '2022/1/8'),
  Tweet('フランキー', 'images/banana.png', '存在することは罪にはならねェ！', '2022/1/9'),
  Tweet('ブルック', 'images/banana.png', '男が一度・・・必ず帰ると言ったのだから！', '2022/1/10'),
  Tweet('ジンベイ', 'images/banana.png', '失ったものばかり数えるな！', '2022/1/11'),
  Tweet('シャンクス', 'images/banana.png', 'この帽子をお前に預ける', '2022/2/1'),
  Tweet('ヒルルク', 'images/banana.png', '違う!…人に忘れられた時さ…!', '2022/2/2'),
  Tweet('ドクタークレハ', 'images/banana.png', '優しいだけじゃ人は救えないんだ!', '2022/2/3'),
  Tweet('ティーチ', 'images/banana.png', '人の夢は!終わらねェ!', '2022/2/4'),
  Tweet('ガンフォール', 'images/banana.png', '人の生きるこの世界に“神”などおらぬ!', '2022/2/5'),
  Tweet('ボンクレー', 'images/banana.png', '理由なんざ他にゃいらねェ!', '2022/2/6'),
  Tweet('イワンコフ', 'images/banana.png', '“奇跡”ナメるんじゃないよォ!', '2022/2/7'),
  Tweet('ニューゲート', 'images/banana.png', 'バカな息子をそれでも愛そう・・・', '2022/1/8'),
  Tweet('エース', 'images/banana.png', '愛してくれて・・・ありがとう', '2022/2/9'),
  Tweet('ロー', 'images/banana.png', '取るべきイスは…必ず奪う!', '2022/2/10'),
  Tweet('サボ', 'images/banana.png', '以後ルフィのバックにはおれがついてる!', '2022/2/11'),
  Tweet('バルトロメオ', 'images/banana.png', 'この子分盃!勝手に頂戴いたしますだべ!', '2022/3/1'),
];

// ツイートモデルをウィジェットに変換する関数
Widget tweetToWidget(Tweet tweet) {
  final iconWidget = Container(
    margin: const EdgeInsets.all(15),
    width: 60,
    height: 60,
    child: ClipRRect(
      borderRadius: BorderRadius.circular(30.0),
      child: Image.asset(tweet.iconUrl),
    ),
  );

  final metaTextWidget = Container(
    padding: const EdgeInsets.all(6),
    height: 40,
    alignment: Alignment.centerLeft,
    child: Text(
      '${tweet.userName}    ${tweet.createDateTime}',
      style: const TextStyle(color: Colors.grey),
    ),
  );

  final textWidget = Container(
    padding: const EdgeInsets.all(8),
    alignment: Alignment.centerLeft,
    child: Text(
      tweet.text,
      style: const TextStyle(fontWeight: FontWeight.bold),
    ),
  );

  return Container(
    padding: const EdgeInsets.all(1),
    decoration: BoxDecoration(
      border: Border.all(color: Colors.blue),
      color: Colors.white,
    ),
    width: double.infinity,
    height: 120,
    child: Row(
      children: [
        iconWidget,
        Expanded(
          child: Column(
            children: [
              metaTextWidget,
              textWidget,
            ],
          ),
        ),
      ],
    ),
  );
}

void main() {
  final tweetListWidget = ListView.builder(
    itemCount: tweets.length,
    itemBuilder: (context, index) => tweetToWidget(tweets[index]),
  );

  final appWidget = MaterialApp(
    home: Scaffold(
      body: Center(
        child: tweetListWidget,
      ),
    ),
  );

  runApp(appWidget);
}
```