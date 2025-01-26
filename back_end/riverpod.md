# Riverpodとは何か？

RiverpodはFlutterアプリケーションの状態管理と依存性注入のための強力なライブラリです。Riverpodを使用すると、アプリケーション内で状態を共有し、簡単にアクセスできるプロバイダー（Provider）を定義できます。これにより、アプリケーションのさまざまな部分でデータを簡単に管理でき、UIの更新をトリガーすることができます。

以下に、Riverpodを使ったFlutterアプリの基本的なセットアップと使用方法を説明します。

## パッケージのインストール

### 1. pubspec.yamlにパッケージを追記する

1. `pubspec.yaml`ファイルに、`dependencies`の下に`flutter_riverpod`パッケージを追加します。

    ```yaml
    dependencies:
      flutter_riverpod:
    ```

2. `pubspec.yaml`を開き、`dev_dependencies`の下に`build_runner`を追加する。

    ```yaml
    dev_dependencies:
      build_runner:
      riverpod_generator:
    ```

3. 以下のコマンドを実行し、パッケージのインストールを行う。

    ```bash
    flutter pub get
    ```

## 状態の作成

### State

Stateは、アプリケーションの「状態」を表します。これは、アプリケーションの動作や表示に影響を与えるデータで、ユーザーの操作や外部のイベントによって変化します。この変化する「状態」をうまく管理することを「状態管理」と呼びます。

### Notifier

Notifierは、状態を「書き換える」役割を持つエンティティです。具体的には、Notifierは状態の変更をトリガーし、その変更をリッスンしているウィジェットに通知します。これにより、状態の変更が発生したときにUIを適切に更新することができます。Riverpodでは、StateNotifierやChangeNotifierなど、状態の変更を管理するためのクラスが提供されています。

### Provider

Providerは、状態を守る「壁」のようなものです。Providerを使用すると、状態を安全にカプセル化し、そのアクセスを制御することができます。具体的には、ConsumerWidgetのrefを用いることで、Providerが提供する状態を参照することができます。しかし、それ以外のウィジェットからは、Providerが保護する状態に直接アクセスすることはできません。これにより、状態の不適切な変更やアクセスを防ぐことができ、アプリケーションの安全性と信頼性を向上させることができます。

### Stateのデータに対応するNotifierとProvider

|State||Notifier|Provider|
|:--:|:--|:--:|:--:|
|Simple系|`int`, `String`|Notifier|NotifierProvider|
|Complex系|`List`, `class`|Notifier|NotifierProvider|
|Future系|`Future<String>`|AsyncNotifier|AsyncNotifierProvider|
|Stream系|`Stream<String>`|AsyncNotifier|AsyncNotifierProvider|

`riverpod_generator`パッケージを用いた場合、以下のNotifierを定義することで、上記の表を意識せずにNotifier・Providerを作成できる
```dart
import 'package:riverpod_annotation/riverpod_annotation.dart';
part 'xxx.g.dart'; // ファイル名(xxx.dart)と同じにする

@riverpod
class XxxNotifier extends _$XxxNotifier {
  @override
  XXX build() {
    return x; // 初期値
  }

  // 状態を更新するコード
  void updateState() {
    // 処理を記載
    state = ...;
  }
}
```

以上のコードを作成後、以下のコマンドを実行することでStateのデータ型に対応したNotifierやProviderを自動で作成してくれる。

```bash
flutter pub run build_runner build --delete-conflicting-outputs
```

## 作成した状態の使用

### Providerの作成

`riverpod_generator`パッケージを用いて、NotifierとProviderを作成した場合、Providerの名前はNotifierの一番最初の文字を小文字にした名前で自動生成される。  
例）`XxxNotifier`で作成した場合：`xxxNotifierProvider`

### ConsumerWidgetの作成

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'xxx.dart';

class XxxWidget extends ConsumerWidget {
  const XxxWidget({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    
    // 状態の監視
    final xxx = ref.watch(xxxNotifierProvider);

    // 状態を更新するためのウィジェットの作成
    final button = ElevatedButton(
      onPressed: () {
        // 状態を編集するための notifier の取得
        final notifier = ref.read(xxxNotifierProvider.notifier);
        // notifier を用いて、状態の更新
        notifier.updateState();
      },
      child: const Text("+1"),
    );

    // 状態の表示
    final text = Text("状態値：$xxx");

    return Column(children: [text, button],);
  }
}
```

- `ref.watch`：状態を見**続ける**ので、関数スコープから抜けた後も有効のまま。これにより`build`関数を抜けた後に状態を変更しても、変更を検知し画面に反映できる。
- `ref.listen`：耳を澄まし**続ける**ので、状態が変わったときに「ダイアログを表示」や「スナックバーを表示」するなど、命令を実行した場合に使う。
  ```dart
  ref.listen(
    xxxNotifierProvider,
    (oldState, newState) { /* 命令コード */ },
  );
  ```
- `ref.read`：状態を読み取る

### AsyncValue

Stateが`Future`・`Stream`のなどの非同期データを扱う際に有用です。  
AsyncValueは、非同期操作の３つの状態を表現します：

- loading：この状態は、非同期操作が完了していないことを示します。つまり、データはまだ「準備中」です。この状態では、通常、ローディングスピナーなどのインジケータを表示します。
- error：この状態は、非同期操作がエラーで終了したことを示します。エラー情報は、この状態の中に含まれています。この情報を使用して、ユーザにエラーメッセージを表示したり、エラーの回復策を提供したりできます。
- data：この状態は、非同期操作が成功し、データが「準備OK」であることを示します。この状態では、取得したデータを使用してUIを更新します。

AsyncValueを使用すると、非同期操作の結果を簡単に管理し、それに基づいてUIを更新することができます。

```dart
class XxxWidget extends ConsumerWidget {
  const XxxWidget({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    
    // 状態の監視
    final xxx = ref.watch(xxxNotifierProvider);

    // 状態の表示
    final widget = xxx.when(
      loading: () => const Text("準備中"),
      error: (e, s) => Text("エラー：$e"), // e: どんなエラー s: どこでエラー の情報が入っている
      data: (d) => Text("$d"), // d: データ本体
    )

    // 状態を更新するウィジェットなどを作成するなど
    ...

    return widget;
  }
}
```

### main.dartからの呼び出し

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'xxx_widget.dart';

void main() {
  // アプリ
  const app = MaterialApp(
    home: Scaffold(
      body: Center(
        child: XxxWidget(),
      ),
    ),
  );

  // プロバイダースコープで囲む
  const scope = ProviderScope(child: app);

  // アプリを動かす
  runApp(scope);
}
```