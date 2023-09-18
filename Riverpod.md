# Riverpodとは何か？

RiverpodはFlutterアプリケーションの状態管理と依存性注入のための強力なライブラリです。Riverpodを使用すると、アプリケーション内で状態を共有し、簡単にアクセスできるプロバイダー（Provider）を定義できます。これにより、アプリケーションのさまざまな部分でデータを簡単に管理でき、UIの更新をトリガーすることができます。

以下に、Riverpodを使ったFlutterアプリの基本的なセットアップと使用方法を説明します。

## 準備

### 1. プロジェクトにRiverpodを追加する

`pubspec.yaml`ファイルに、`flutter_riverpod`パッケージを追加します。これにより、Riverpodをプロジェクトに導入できます。

```yaml
dev_dependencies:
  flutter_riverpod:
```

### 2. 必要なライブラリをインポートする

`main.dart`ファイルで、Riverpodライブラリをインポートします。

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';
```

### 3. アプリケーションをプロバイダースコープでラップする

Riverpodのプロバイダーを使用するには、アプリケーション全体を`ProviderScope`内にラップする必要があります。以下は、`main.dart`内でこれを行う方法です。

```dart
void main() {
  // アプリ
  final app = MaterialApp(home: Sample());

  // プロバイダースコープで囲む
  final scope = ProviderScope(child: app);

  // アプリを動かす
  runApp(scope);
}
```

### 4. プロバイダーを設定する

Riverpodを使用する際には、データの状態を管理するためのプロバイダーを定義します。以下は、簡単なプロバイダーの例です。

```dart
final nicknameProvider = StateProvider<String>(
  (ref) {
    // 初期値を設定
    return "ボタンを押すことで変化します";
  }
);
```

### 5. ConsumerWidgetの設定

ConsumerWidgetはRiverpodライブラリ内のウィジェットで、データを監視し、UIを構築するために使用されます。

```dart
class Sample extends ConsumerWidget {
  const Sample({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // ここにウィジェットを構築するためのコードを書きます
  }
}
```

## サンプルコード

以下は、Riverpodを使用して簡単なFlutterアプリを構築するサンプルコードです。

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';


void main() {
  // アプリ
  const app = MaterialApp(home: Sample());

  // プロバイダースコープで囲む
  const scope = ProviderScope(child: app);

  // アプリを動かす
  runApp(scope);
}

// プロバイダー
final nicknameProvider = StateProvider<String>(
  (ref) {
    // 変化するデータ
    return "ボタンを押すことで変化します";
  }
);

// 画面
class Sample extends ConsumerWidget {
  const Sample({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // データを監視しておく
    final nickname = ref.watch(nicknameProvider);

    void pushRed(WidgetRef ref) {
      final notifier = ref.read(nicknameProvider.notifier);
      notifier.state = "ヒトカゲ";
    }

    void pushBlue(WidgetRef ref) {
      final notifier = ref.read(nicknameProvider.notifier);
      notifier.state = "ゼニガメ";
    }

    void pushGreen(WidgetRef ref) {
      final notifier = ref.read(nicknameProvider.notifier);
      notifier.state = "フシギダネ";
    }

    final columnWidget = Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      crossAxisAlignment: CrossAxisAlignment.center,
      children: [
        Text(nickname),
        ElevatedButton(
          style: ElevatedButton.styleFrom(backgroundColor: Colors.red),
          onPressed: () => pushRed(ref),
          child: const Text("ボタンに表示するテキスト"),
        ),
        ElevatedButton(
          style: ElevatedButton.styleFrom(backgroundColor: Colors.blue),
          onPressed: () => pushBlue(ref),
          child: const Text("ボタンに表示するテキスト"),
        ),
        ElevatedButton(
          style: ElevatedButton.styleFrom(backgroundColor: Colors.green),
          onPressed: () => pushGreen(ref),
          child: const Text("ボタンに表示するテキスト"),
        ),
      ],
    );

    final app = MaterialApp(
      home: Scaffold(
        body: Center(
          child: columnWidget,
        ),
      ),
    );

    return app;
  }
}
```