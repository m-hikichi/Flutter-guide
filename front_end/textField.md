# 文字入力ウィジェット

```dart
// 文字入力ウィジェットを作成する
final textField = TextField();
```

## decoration（装飾）

文字入力ウィジェットの外観をカスタマイズする方法について説明します。

```dart
// 装飾オプションを設定した文字入力ウィジェットを作成する
final textField = TextField(
  decoration: const InputDecoration(
    // 境界線を追加
    border: OutlineInputBorder(),
    // ラベルテキストを設定
    labelText: "あなたの名前",
    // ヒントテキストを設定
    hintText: "カタカナで入力してください",
    // エラーテキストを設定
    errorText: "名前が長すぎます",
  ),
);
```

### border（境界線）

文字入力フィールドの周りに境界線を追加します。これにより、フィールドの境界がはっきりと表示されます。

### labelText（ラベルテキスト）

文字入力フィールドの上に表示されるラベルテキストを設定します。例えば、「あなたの名前」というテキストがフィールドの上に表示されます。

### hintText（ヒントテキスト）

文字入力フィールド内に初めから表示されるヒントテキストを設定します。これは、ユーザーに対して入力する内容のヒントを提供するのに役立ちます。例えば、「カタカナで入力してください」というテキストが入力フィールドに薄く表示されます。

### errorText（エラーテキスト）

ユーザーの入力がエラーの場合に表示されるエラーメッセージを設定します。例えば、「名前が長すぎます」というメッセージがエラーが発生した際に表示されます。

## Controller（コントローラー）

文字入力フィールドの値を制御および監視するための「コントローラー」について説明します。

```dart
final controllerWidget = TextEditingController();

final textField = TextField(
  controller: controllerWidget,
);
```

## サンプルコード

```dart
import 'package:flutter/material.dart';

void main() {
  final nameController = TextEditingController();

  final nameTextField = TextField(
    decoration: const InputDecoration(
      // 境界線を追加
      border: OutlineInputBorder(),
      // ラベルテキストを設定
      labelText: "あなたの名前",
      // ヒントテキストを設定
      hintText: "カタカナで入力してください",
      // エラーテキストを設定
      errorText: "名前が長すぎます",
    ),
    controller: nameController,
  );

  void printName() {
    debugPrint(nameController.text);
  }

  final button = ElevatedButton(onPressed: printName, child: const Text("ボタン"));

  final appWidget = MaterialApp(
    home: Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [nameTextField, button],
        ),
      ),
    ),
  );

  runApp(appWidget);
}
```