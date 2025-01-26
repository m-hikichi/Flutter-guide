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

## ウィジェットの説明

### `Text`

```dart
const sampleText = "サンプル";
const textWidget = Text(sampleText);
```

`Text` ウィジェットは、テキストを表示するためのウィジェットです。このサンプルでは、`sampleText` 変数に格納されたテキストを表示するために使用されています。

### `Center`

```dart
const centerWidget = Center(child: textWidget);
```

`Center` ウィジェットは、子ウィジェットを中央に配置するためのウィジェットです。`textWidget` を中央に配置するために使用されます。

### `Scaffold`

```dart
const scaffoldWidget = Scaffold(body: centerWidget);
```

`Scaffold` ウィジェットは、アプリケーションの基本的な画面構造を提供するウィジェットです。このウィジェットは、アプリケーションのフレームワークとして機能し、アプリケーションの基本的な構造を定義します。
|オプション|内容|
|:--|:--|
|`appBar`|画面の上部に表示されるバーで、アプリの名前やメニューボタンなどを表示する場所です。|
|`drawer`|画面の左側からスライドして出てくるメニューで、ユーザーがアプリ内の他のページに移動するためのリンクやボタンを配置することができます。|
|`endDrawer`|`drawer`と同じですが、画面の右側からスライドして出てきます。|
|`body`|アプリケーションの主要なコンテンツが表示される部分です。ここにはテキスト、画像、ビデオなど、あらゆる種類のウィジェットを配置することができます。|
|`floatingActionButton`|画面上に浮かぶ丸いボタンで、ユーザーがタップすると何か特定のアクション（例えば新しいページを開く、データを保存するなど）を起動します。|
|`bottomNavigationBar`|画面下部に表示されるバーで、ユーザーがアプリ内で簡単に移動できるようにするためのものです。|

### `MaterialApp`

```dart
const appWidget = MaterialApp(home: scaffoldWidget);
```

`MaterialApp` ウィジェットは、Flutterアプリケーションを初期化するためのウィジェットです。このサンプルでは、`scaffoldWidget` をホーム画面（ルート）として設定し、アプリケーションのエントリーポイントとして使用します。アプリケーションのテーマやルート(route)などを設定するために使用されます。

これらのウィジェットを組み合わせることで、Flutterアプリケーションが構築され、テキストを中央に表示する基本的な構造が定義されます。

## まとめたコード

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