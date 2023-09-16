# FlutterのColumnとRowの基本

Flutterでは、ColumnとRowを使用してウィジェットを垂直または水平に配置できます。ここでは、ColumnとRowの基本的な使用方法と主な配置オプションについて説明します。

## Column（垂直方向の配置）

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    // ここにウィジェットを追加
  ],
);
```

### `mainAxisAlignment`（垂直方向の配置）

- `start`：上端に配置
- `center`：中央に配置
- `end`：下端に配置
- `spaceEvenly`：等間隔に配置
- `spaceBetween`：両端に寄せて配置

### `crossAxisAlignment`（水平方向の配置）

- `start`：左端に配置
- `center`：中央に配置
- `end`：右端に配置
- `stretch`：伸ばして全体を埋める

### `mainAxisSize`（垂直方向のサイズ）

- `min`：Columnはその中の子供のウィジェットが占める最小のサイズに収縮します。つまり、子供のウィジェットが必要なだけのスペースを占めます。
- `max`：Columnは可能な限りのスペースを占めようとし、垂直方向に拡張します。通常、親ウィジェットが利用可能なスペース全体を占めるようになります。

### サンプルコード

```dart
import 'package:flutter/material.dart';

void main() {
  final columnWidget = Column(
    mainAxisAlignment: MainAxisAlignment.center,
    crossAxisAlignment: CrossAxisAlignment.center,
    children: [
      Text("レモン"),
      Text("リンゴ"),
      Text("ブドウ"),
    ],
  );

  final app = MaterialApp(
    home: Scaffold(
      body: Center(
        child: columnWidget,
      ),
    ),
  );

  runApp(app);
}
```

## Row（水平方向の配置）

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    // ここにウィジェットを追加
  ],
);
```

### `mainAxisAlignment`（水平方向の配置）

- `start`：左端に配置
- `center`：中央に配置
- `end`：右端に配置
- `spaceEvenly`：等間隔に配置
- `spaceBetween`：両端に寄せて配置

### `crossAxisAlignment`（垂直方向の配置）

- `start`：上端に配置
- `center`：中央に配置
- `end`：下端に配置
- `stretch`：伸ばして全体を埋める

### `mainAxisSize`（垂直方向のサイズ）

- `min`：Rowはその中の子供のウィジェットが占める最小のサイズに収縮します。つまり、子供のウィジェットが必要なだけのスペースを占めます。
- `max`：Rowは可能な限りのスペースを占めようとし、垂直方向に拡張します。通常、親ウィジェットが利用可能なスペース全体を占めるようになります。

### サンプルコード

```dart
import 'package:flutter/material.dart';

void main() {
  final rowWidget = Row(
    mainAxisAlignment: MainAxisAlignment.center,
    crossAxisAlignment: CrossAxisAlignment.center,
    children: [
      Text("レモン"),
      Text("リンゴ"),
      Text("ブドウ"),
    ],
  );

  final app = MaterialApp(
    home: Scaffold(
      body: Center(
        child: rowWidget,
      ),
    ),
  );

  runApp(app);
}
```

## ColumnとRowを組み合わせたサンプルコード

以下のサンプルコードは、ColumnとRowを組み合わせて使用する例です。

```dart
import 'package:flutter/material.dart';

void main() {
  final columnWidget = Column(
    mainAxisAlignment: MainAxisAlignment.center,
    crossAxisAlignment: CrossAxisAlignment.center,
    children: [
      Text("レモン"),
      Text("リンゴ"),
      Text("ブドウ"),
    ],
  );

  final rowWidget = Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    crossAxisAlignment: CrossAxisAlignment.center,
    children: [
      columnWidget, columnWidget, columnWidget,
    ],
  );

  final appWidget = MaterialApp(
    home: Scaffold(
      body: Center(
        child: rowWidget,
      ),
    ),
  );

  runApp(appWidget);
}
```
