# 画像の表示方法

## 画像の用意

1. 画像ファイルを `assets/images` フォルダに保存します。
2. アプリケーションの `pubspec.yaml` ファイルに、以下のコードを追加します。これにより、アプリが画像ファイルを認識できるようになります。
    ```yaml
    flutter:
      assets:
        - assets/images/
    ```

## 画像の表示

### `Image.asset()` - アプリ内の画像を表示
アプリ内にある画像を表示するには、`Image.asset()` ウィジェットを使用します。

#### サンプルコード

```dart
import 'package:flutter/material.dart';

void main() {
  final appWidget = MaterialApp(
    home: Scaffold(
      body: Center(
        child: Image.asset('images/sample_photo.png'),
      )
    )
  );

  runApp(appWidget);
}
```

### `Image.network()` - インターネット上の画像を表示
ウェブ上にある画像を表示するには、`Image.network()` ウィジェットを使用します。

#### サンプルコード

```dart
import 'package:flutter/material.dart';

void main() {
  final appWidget = MaterialApp(
    home: Scaffold(
      body: Center(
        child: Image.network('https://...'), // ここに画像のURLを入力
      )
    )
  );

  runApp(appWidget);
}
```

### `Image.memory()`

### `Image.file()`
