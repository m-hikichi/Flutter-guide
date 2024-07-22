# Flutterでのテスト

## テスト環境の準備

`flutter_test`パッケージを使用します。通常、Flutterプロジェクトを作成すると自動的に含まれます。

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
```

## テストファイルの作成

プロジェクトの`test`ディレクトリにテストファイルを作成します。このとき、`unit_test.dart`や`widget_test.dart`のように、ファイル名は`*_test.dart`にする必要があります。これにより、アプリケーションをテストするためのテストファイルであることがFlutterに伝えられます。

## テストの実行

ターミナルで以下のコマンドを実行して、すべてのテストを実行します。

```bash
flutter test
```

特定のテストファイルのみを実行する場合は、ファイルパスを指定します。

```bash
flutter test test/widget_test.dart
```

## テストコード

### Unit Test

ユニットテスト（Unit Test）は、プログラムの比較的小さな単位（ユニット）で、個々の機能が正しく動作しているかを検証するためのテストです。主にビジネスロジックやデータ処理のテストに使用されます。

#### テストコードの作成

まず、`flutter_test.dart`のインポートを行います。
```dart
import 'package:flutter_test/flutter_test.dart'
```

`void main()`を定義し、テストコードを記述します。
- `test`関数：ユニットテストを定義するために使用します。関数の引数には、テストの名前とテストしたい動作を記載します。
- `expect`関数：テストの期待値を確認し、想定通りに動作したかどうかをテストします。
```dart
test(
  "Testing the increment counter",
  () {
    // setup
    Counter counter = Counter(value: 5);

    // do
    counter.incrementCounter();

    // test
    expect(counter.value, 6);
  },
);
```

<details>
<summary>カウンタクラスのソースコード</summary>

```dart
class Counter {
  int value;
  Counter({this.value = 0});

  void incrementCounter() {
    value++;
  }

  void decrementCounter() {
    value--;
  }
}
```
</details>

必要に応じて、`group`関数を用いてテストをグループ化できます。

<details>
<summary>サンプルコード</summary>

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:flutter_sample_test/counter.dart';

void main() {
  group("Testing the counter", () {
    test(
      "Testing the initialize",
      () {
        // setup
        Counter counter = Counter();
        
        // test
        expect(counter.value, 0);
      }
    );

    test(
      "Testing the increment counter",
      () {
        // setup
        Counter counter = Counter(value: 5);

        // do
        counter.incrementCounter();

        // test
        expect(counter.value, 6);
      },
    );

    test(
      "Testing the decrement counter",
      () {
        // setup
        Counter counter = Counter(value: 10);

        // do
        counter.decrementCounter();

        // test
        expect(counter.value, 9);
      },
    );
  });
}
```

</details>

### Widget Test

ウィジェットテスト（Widget Test）は、FlutterアプリのUIコンポーネント（ウィジェット）が期待通りに動作するかを確認するためのテストです。これにより、UIの見た目や動作が正しいかどうかを検証できます。

#### テストコードの作成

まず、`flutter_test.dart`のインポートを行います。
```dart
import 'package:flutter_test/flutter_test.dart'
```

`void main()`を定義し、テストコードを記述します。
- `WidgetTester`クラス：ウィジェットのビルドや操作を行うためのヘルパークラスです。
- `testWidgets`関数：ウィジェットテストを定義するために使用します。
- `pumpWidget`メソッド：ウィジェットをビルドしてフレームをトリガーします。
- `expect`関数：テストの期待値を確認するために使用します。

<details>
<summary>サンプルコード</summary>

```dart
import 'package:flutter/material.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:your_app/main.dart';

void main() {
  testWidgets('Counter increments smoke test', (WidgetTester tester) async {
    // Widget Treeを構築
    await tester.pumpWidget(MyApp());
    // MyAppがMaterialAppでラップされていない場合はラップする必要あり
    // await tester.pumpWidget(MaterialApp(home: MyApp()))

    // find.textで、Widget Treeから特定のWidgetを探す。今回は、カウンターが0から始まることを確認
    expect(find.text('0'), findsOneWidget);  // 1つ見つかることを期待する。
    expect(find.text('1'), findsNothing);  // 1つも見つからないことを期待する。

    // アプリ内の'+'アイコンをタップする操作をシミュレート
    await tester.tap(find.byIcon(Icons.add));
    // Widget Treeを再ビルド
    await tester.pump();

    // カウンターが1に増加したことを確認します。
    expect(find.text('0'), findsNothing);
    expect(find.text('1'), findsOneWidget);
  });
}
```

</details>
