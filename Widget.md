# Flutter Widgetの基本

このサンプルコードは、Flutterを使用して単純なテキスト表示アプリを作成するものです。以下は、各ウィジェットについての説明です。

## コード

```dart
import 'package:flutter/material.dart';

void main() {
  const sampleText = "サンプル";

  const textWidget = Text(sampleText);

  const centerWidget = Center(child: textWidget);

  const scaffoldWidget = Scaffold(body: centerWidget);

  const appWidget = MaterialApp(home: scaffoldWidget);

  runApp(appWidget);
}
```

### ウィジェットの説明

#### `Text`

```dart
const sampleText = "サンプル";
const textWidget = Text(sampleText);
```

`Text` ウィジェットは、テキストを表示するためのウィジェットです。このサンプルでは、`sampleText` 変数に格納されたテキストを表示するために使用されています。

#### `Center`

```dart
const centerWidget = Center(child: textWidget);
```

`Center` ウィジェットは、子ウィジェットを中央に配置するためのウィジェットです。`textWidget` を中央に配置するために使用されます。

#### `Scaffold`

```dart
const scaffoldWidget = Scaffold(body: centerWidget);
```

`Scaffold` ウィジェットは、アプリケーションの基本的な画面構造を提供するウィジェットです。このウィジェットは、アプリケーションのフレームワークとして機能し、アプリケーションの基本的な構造を定義します。具体的には、アプリケーションの上部アプリバー、ドロワー（サイドメニュー）、および本文エリアなどを含みます。このサンプルでは、`centerWidget` を本文エリアとして持ち、テキストを中央に表示する基本的な画面構造を提供します。

#### `MaterialApp`

```dart
const appWidget = MaterialApp(home: scaffoldWidget);
```

`MaterialApp` ウィジェットは、Flutterアプリケーションを初期化するためのウィジェットです。このサンプルでは、`scaffoldWidget` をホーム画面（ルート）として設定し、アプリケーションのエントリーポイントとして使用します。アプリケーションのテーマやルート(route)などを設定するために使用されます。

これらのウィジェットを組み合わせることで、Flutterアプリケーションが構築され、テキストを中央に表示する基本的な構造が定義されます。

### まとめたコード

```dart
import 'package:flutter/material.dart';

void main() {
  // アプリケーションの基本構造を定義
  const appWidget = MaterialApp(
    home: Scaffold(
      body: Center(
        child: Text("サンプル")
      )
    )
  );

  // アプリケーションを起動
  runApp(appWidget);
}
```