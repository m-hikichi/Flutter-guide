# ボタンウィジェット

Flutterではさまざまな種類のボタンウィジェットが利用できます。以下ではそれぞれのボタンについて説明します。

## ElevatedButton（浮き上がるボタン）

背景が浮き上がったボタンで、高い視認性を持っています。一般的なアクションに使用されます。

```dart
final buttonWidget = ElevatedButton(
  style: ElevatedButton.styleFrom(
    // ボタンの背景色を指定
    backgroundColor: Colors.blue,
  ),
  // ボタンが押された際に実行される関数を指定
  onPressed: xxxx,
  // ボタンに表示するテキスト
  child: const Text("ボタンに表示するテキスト"),
);
```

`onPressed: null,`を設定することで、ボタンを押せない状態にすることができます。

## TextButton（テキストボタン）

シンプルなテキストのボタンで、通常はリンクや軽微なアクションに使用されます。

## OutlinedButton（枠線ボタン）

テキストを囲む枠線があるボタンで、セカンダリなアクションに使用されます。

## IconButton（アイコンボタン）

テキストではなくアイコンを含むボタンで、アイコンをクリックしてアクションを実行します。

## FloatingActionButton（浮動アクションボタン）

画面の底部に配置され、円形のボタンで、通常は特定の画面アクションをトリガーするために使用されます。

## DropdownButton（ドロップダウンボタン）

ドロップダウンリストから選択肢を選ぶためのボタンで、通常は選択肢が多い場合に使用されます。

## PopupMenuButton（ポップアップメニューボタン）

ボタンをタップするとポップアップメニューが表示され、選択肢を選ぶことができるボタンです。一般的にはコンテキストメニューを表示するために使用されます。

## サンプルコード

このサンプルコードでは、ElevatedButtonを作成し、ボタンが押された際に通信のステータスを表示するアプリケーションが作成されています。

```dart
import 'package:flutter/material.dart';

void main() {
  // ボタンが押された際に実行される関数
  void handleCommunication() {
    debugPrint("通信開始");
    debugPrint("通信中...");
    debugPrint("通信終了");
  }

  // ElevatedButtonの作成
  final buttonWidget = ElevatedButton(
    style: ElevatedButton.styleFrom(
      backgroundColor: Colors.blue,
    ),
    onPressed: handleCommunication,
    child: const Text(
      "押してみて",
      style: TextStyle(
        color: Colors.white,
      ),
    ),
  );

  // アプリケーションの基本構造を定義
  final appWidget = MaterialApp(
    home: Scaffold(
      body: Center(
        child: buttonWidget,
      ),
    ),
  );

  // アプリケーションを起動
  runApp(appWidget);
}
```
