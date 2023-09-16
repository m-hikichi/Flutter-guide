# FlutterのContainerの基本

```dart
final containerWidget = Container(
  // 設定を記載
);
```

## color
`color` プロパティは、コンテナの背景色を指定するのに使用します。このプロパティには `Color` クラスのインスタンスを指定します。

```dart
final containerWidget = Container(
  color: Colors.blue, // 例: 青色の背景
);
```

## width・height
`width` および `height` プロパティを使用して、コンテナの幅と高さを指定できます。

```dart
final containerWidget = Container(
  width: 200,   // 幅を200ピクセルに設定
  height: 100,  // 高さを100ピクセルに設定
);
```

## child
`child` プロパティは、コンテナ内に配置するウィジェットを指定します。これは通常、他のウィジェット（テキスト、イメージ、Column・Row、他のコンテナなど）を含むために使用されます。

```dart
final containerWidget = Container(
  child: Text('Hello, World!'), // テキストウィジェットを追加
);
```

## alignment
`alignment` プロパティは、`child` ウィジェットの配置を制御します。このプロパティには `Alignment` クラスのインスタンスを指定します。

```dart
final containerWidget = Container(
  alignment: Alignment.center, // 子ウィジェットを中央に配置
  child: Text('Centered Text'),
);
```

## padding・margin
`padding` および `margin` プロパティは、コンテナの内側および外側の余白を制御します。

### padding
`padding` プロパティは、コンテナ内のコンテンツとコンテナの境界との間に余白を追加します。

```dart
final containerWidget = Container(
  padding: EdgeInsets.all(16.0), // 内側に16ピクセルの余白を追加
  child: Text('Text with padding'),
);
```

### margin
`margin` プロパティは、コンテナ自体と周囲の要素との間に余白を追加します。

```dart
final containerWidget = Container(
  margin: EdgeInsets.all(16.0), // 外側に16ピクセルの余白を追加
  child: Text('Text with margin'),
);
```

## サンプルコード
以下は、すべてのプロパティを組み合わせたサンプルコードです。

```dart
import 'package:flutter/material.dart';

void main() {
  final containerWidget = Container(
    color: Colors.blue,                // 背景色を青に設定
    width: 200,                        // 幅を200ピクセルに設定
    height: 100,                       // 高さを100ピクセルに設定
    child: Text('Sample Container'),   // テキストウィジェットを追加
    alignment: Alignment.centerLeft,   // 子ウィジェットを中央に配置
    padding: EdgeInsets.all(16),       // 内側に16ピクセルの余白を追加
    margin: EdgeInsets.all(16),        // 外側に16ピクセルの余白を追加
  );

  // アプリケーションの基本構造を定義
  final app = MaterialApp(
    home: Scaffold(
      body: Center(
        child: containerWidget,
      ),
    ),
  );

  // アプリケーションを起動
  runApp(app);
}
```
