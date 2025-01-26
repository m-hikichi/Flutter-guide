# カルーセルとは

カルーセルは、ユーザーが画像や情報を水平方向にスクロールできるようにするUIパターンです。これは、ユーザーが複数のアイテムを見ることができ、それぞれのアイテムがフルスクリーンで表示されることを可能にします。例えば、オンラインショッピングサイトでは、商品の画像をスライドショー形式で表示するためにカルーセルがよく使用されます。

## PageViewを用いたカルーセルの実装

Flutterでは、`PageView`ウィジェットを使用してカルーセルを簡単に作成できます。

|オプション|説明|
|:--|:--|
|`ViewportFraction`|表示されるページの幅を制御します。値が1.0の場合、各ページはビューポートの全幅を占めます。値が0.8の場合、各ページはビューポートの80％の幅を占め、両側に隣のページが表示されます。|

## サンプルコード

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

final animals = ["犬", "猫", "狐", "兎"];

Widget modelToWidget(String animal) {
  return Container(
    padding: const EdgeInsets.all(4.0),
    margin: const EdgeInsets.all(4.0),
    alignment: Alignment.center,
    decoration: BoxDecoration(
      color: Colors.white,
      borderRadius: BorderRadius.circular(20.0),
    ),
    child: Text(animal),
  );
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    final carousel = Container(
      height: MediaQuery.sizeOf(context).height,
      color: Colors.blue,
      child: PageView.builder(
        controller: PageController(viewportFraction: 0.9),
        itemCount: animals.length,
        itemBuilder: (c, i) => modelToWidget(animals[i]),
      ),
    );

    return MaterialApp(
      home: Scaffold(
        body: carousel,
      ),
    );
  }
}
```