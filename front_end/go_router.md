# Flutterアプリの画面遷移を簡単に管理しよう：go_router

## 準備

### 各画面を作成する

Flutterアプリ内で使用する各画面のデザインを定義するDartファイルを作成します。以下は、3つの画面を持つアプリの例です。

```
lib
├── main.dart
├── page_a.dart
├── page_b.dart
└── page_c.dart
```

各Dartファイルには、その画面の要素を定義するクラスが含まれます。例えば、`PageA` クラスは以下のようになります。

```dart
import 'package:flutter/material.dart';

class PageA extends StatelessWidget {
  const PageA({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // 画面上部に表示するバー
    final appBar = AppBar(
        backgroundColor: Colors.red,
        title: const Text("画面 A")
    );
    
    return Scaffold(
        appBar: appBar,
    );
  }
}
```

### pubspec.yamlファイルを編集

`pubspec.yaml` ファイルに、`go_router` パッケージの依存関係を追加します。

```yml
dependencies:
  go_router:
```


### main.dartを編集

`main.dart` ファイルで、以下の手順を実行します。

1. `go_router` パッケージをインポートします。

    ```dart
    import 'package:go_router/go_router.dart'
    ```

2. 各画面のDartファイルをインポートします。

    ```dart
    import 'package:sample/page_a.dart';
    import 'package:sample/page_b.dart';
    import 'package:sample/page_c.dart';
    ```

3. アプリ全体を定義した `App` クラスを作成します。

    ```dart
    class App extends StatelessWidget {
    App({super.key});

    final router = GoRouter(
      // 初期画面のパス（アプリが起動した時に表示する画面）
      initialLocation: '/a',
      // パスと画面の組み合わせ
      routes: [
        GoRoute(
            path: '/a',
            builder: (context, state) => const PageA(),
        ),
        GoRoute(
            path: '/b',
            builder: (context, state) => const PageB(),
        ),
        GoRoute(
            path: '/c',
            builder: (context, state) => const PageC(),
        ),
      ],
    );

    @override
    Widget build(BuildContext context) {
      return MaterialApp.router(
        routeInformationProvider: router.routeInformationProvider,
        routeInformationParser: router.routeInformationParser,
        routerDelegate: router.routerDelegate,
      );
    }
    ```

## 画面移動

### 画面を進む

アプリ内で画面を進める場合、以下のコードを使用します。

```dart
context.push('/b')
```


### 前の画面に戻る

前の画面に戻るには、以下のコードを使用します。このコードは、スタックに保存されている前の画面に戻ります。

```dart
context.pop()
```


### 指定した画面に進む

特定の画面に進む場合、以下のコードを使用します。

```dart
context.go('/a')
```

### サンプルコード

以下は、ボタンを押すことで「画面 B」に移動できる `PageA` のサンプルです。

```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

class PageA extends StatelessWidget {
  const PageA({Key? key}) : super(key: key);

  push(BuildContext context) {
    // 画面 B へ進む
    context.push('/b');
  }

  @override
  Widget build(BuildContext context) {
    // 画面上部に表示するバー
    final appBar = AppBar(
        backgroundColor: Colors.red,
        title: const Text("画面 A")
    );

    final pushButton = ElevatedButton(
      style: ElevatedButton.styleFrom(
        backgroundColor: Colors.green
      ),
      onPressed: () => push(context),
      child: const Text('進む >'),
    );
    
    return Scaffold(
        appBar: appBar,
        body: pushButton,
    );
  }
}
```
