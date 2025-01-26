# 自作ウィジェット（StatelessWidget）

このガイドでは、Flutterアプリ内で独自のウィジェットを作成し、それを使用する方法を紹介します。この独自のウィジェットは、「バナナのカウンター」を表示します。

```dart
class MyWidget extends StatelessWidget {
  const MyWidget({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return const Placeholder();
  }
}
```

## はじめに

まず、`main.dart`と同じディレクトリに新しいDartファイルを作成してください。このファイルは、自作ウィジェットのコードを格納します。

```
lib
├── main.dart
└── banana_counter.dart
```

## 自作ウィジェットの作成

以下のコードは、バナナのカウンターを表示する独自のウィジェットを定義するサンプルです。このウィジェットは、バナナの画像とカウントを横に並べたものを返します。

### サンプルコード

このサンプルコードでは、バナナの画像とカウントを含むウィジェットを作成し、それをContainer内に配置して背景色やサイズを設定しています。

```dart
import 'package:flutter/material.dart';

class BananaCounter extends StatelessWidget {
  const BananaCounter({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // バナナの画像
    final bananaImageWidget = Image.asset("images/banana.png");

    // 数字の表示
    const countTextWidget = Text(
      "999",
      style: TextStyle(
        color: Colors.yellow,
        fontSize: 50,
      ),
    );

    // バナナと数字を横に並べる
    final rowWidget = Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      crossAxisAlignment: CrossAxisAlignment.center,
      children: [bananaImageWidget, countTextWidget],
    );

    // 背景色や大きさを指定
    final containerWidget = Container(
      color: Colors.black87,
      width: 300,
      height: 100,
      child: rowWidget,
      alignment: Alignment.centerLeft,
      padding: EdgeInsets.all(10),
      margin: EdgeInsets.all(10),
    );

    return containerWidget;
  }
}
```

## 自作ウィジェットの使用

### サンプルコード
```dart
import 'package:flutter/material.dart';
import 'package:sample/banana_counter.dart';

void main() {
  // BananaCounterウィジェットのインスタンスを作成
  final bananaCounterWidget = BananaCounter();

  // アプリケーションの基本構造を定義
  final app = MaterialApp(
    home: Scaffold(
      body: Center(
        child: bananaCounterWidget,
      ),
    ),
  );

  // アプリケーションを起動
  runApp(app);
}
```

## 引数を渡す

```dart
import 'package:flutter/material.dart';

class BananaCounter extends StatelessWidget {
  // バナナの数
  final int number;

  // コンストラクタ (バナナの数を指定してBananaCounterウィジェットを作成する)
  const BananaCounter({Key? key, required this.number}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // バナナの画像
    final bananaImage = Image.asset("images/banana.png");

    // 数字の表示
    final textWidget = Text(
      '$number',
      style: const TextStyle(
        color: Colors.yellow,
        fontSize: 50,
      ),
    );

    // バナナと数字を横に並べる
    final row = Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      crossAxisAlignment: CrossAxisAlignment.center,
      children: [bananaImage, textWidget],
    );

    // 背景色や大きさを指定
    final container = Container(
      color: Colors.black87,
      width: 300,
      height: 100,
      child: row,
      alignment: Alignment.centerLeft,
      padding: EdgeInsets.all(10),
      margin: EdgeInsets.all(10),
    );

    return container;
  }
}
```

このコードでは、`BananaCounter`ウィジェットに`number`という引数を追加し、その数値を表示するように調整しています。引数を渡すには、ウィジェットを作成する際に引数を指定し、使用する際にその引数の値を指定します。
呼び出し時に引数を渡す例を以下に示します。

```dart
import 'package:flutter/material.dart';
import 'package:sample/banana_counter.dart';

void main() {
  // BananaCounterウィジェットのインスタンスを作成し、numberプロパティに値を設定
  const bananaCounterWidget = BananaCounter(number: 888);

  // アプリケーションの基本構造を定義
  const app = MaterialApp(
    home: Scaffold(
      body: Center(
        child: bananaCounterWidget,
      ),
    ),
  );

  // アプリケーションを起動
  runApp(app);
}
```
