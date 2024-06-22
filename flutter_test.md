# Flutterでのテスト

## Unit Test

非常に単純なカウンタクラスのテストを行います。
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

### テストファイルの作成

`test`ディレクトリの中に入り、ユニットテストを行うdartファイルを作成します。このとき、ファイル名は`*_test.dart`にする必要があります。これにより、アプリケーションをテストするためのテストファイルであることがFlutterに伝えられます。

### テストコードの作成

まず、`flutter_test.dart`のインポートを行います。
```dart
import 'package:flutter_test/flutter_test.dart'
```

`void main()`を定義し、テストコードを記述します。`test`関数の引数には、テストの名前とテストしたい動作を記載します。`expect`を使用して、想定通りに動作したかどうかをテストします。
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

必要に応じて、`group`関数を用いてテストをグループ化できます。

### テストの実行

`flutter test`コマンドを用いて、テストを実行します。

### サンプルコード

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