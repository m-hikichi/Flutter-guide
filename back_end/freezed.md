# freezedとは

Flutterでは、`setState`や`riverpod`を使用して状態管理を行いますが、時々値の変更が検出されず、画面が更新されないことがあります。これは、Flutterが「インスタンスが変わったかどうか」を基に値の変更を検出するためです。インスタンス内で値が変わっても、そのインスタンス自体は変わらないため、状態管理の観点からは「値は変わっていない」と判断され、結果として画面が更新されません。新しいインスタンスを作成し、それをStatefulWidgetのメンバー変数に設定することで、変更が検出され、画面が更新されます。<br>
`freezed`は、不変（immutable）なデータクラスを簡単に作成するためのDartパッケージです。`freezed`を使用すると、イミュータブルなデータクラスを生成する際に必要なコードを自動的に生成してくれます。<br>
手動でクラスとメソッドを実装することも可能ですが、クラスが増えるとミスが発生しやすくなるというデメリットがあります。`freezed`を使用することで、これらのメソッドを自動生成することが可能になり、コードの管理がより簡単になります。

## immutableとは

Immutable（イミュータブル）とは「不変」という意味で、オブジェクトの状態が変わらないことを指します。Immutableなクラスとして定義すると、値を書き換えられないため予期せぬトラブルを防げます。**値を書き換えたい場合は、コピー/クローンをした上で値を変更し、別のインスタンスとして扱います。**

## インストール方法

1. `pubspec.yaml`を開き、`dependencies`の下に`freezed_annotation`を追加する。
    ```yaml
    dependencies:
      freezed_annotation:
    ```
2. `pubspec.yaml`を開き、`dev_dependencies`の下に`freezed`と`build_runner`を追加する。
    ```yaml
    dev_dependencies:
      freezed:
      build_runner:
    ```

## immutableなクラスの作成方法

1. クラスファイルを作成し、以下のようにクラスの定義を行う。(今回は魚を扱うFishkラスを`fish.dart`ファイルに作成)

```dart
import 'package:freezed_annotation/freezed_annotation.dart';
part 'fish.freezed.dart'; // ファイル名が dog.dart なら dog.freezed.dart にする

@freezed
class Fish with _$Fish {
  const factory Fish({
    // 名前
    required String name,
    // 大きさ
    required int size,
    // 値段
    required int price,
  }) = _Fish;
}
```
2. ターミナルにて`flutter pub run build_runner build --delete-conflicting-outputs`を実行する。実行後、`fish.freezed.dart`ファイルが生成される。

## サンプルコード

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
// 自分が作った fish.dart ファイルを読み込む
import 'fish.dart';

// メイン関数
void main() {
  const app = MaterialApp(home: Home());
  const scope = ProviderScope(child: app);
  runApp(scope);
}

// 魚データの状態管理
final fishProvider = StateProvider((ref) {
  return const Fish(
    name: 'マグロ',
    size: 200,
    price: 300,
  );
});

// ホーム画面
class Home extends ConsumerWidget {
  const Home({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // 魚データ
    final fish = ref.watch(fishProvider);

    final nameText = Text(
      '名前: ${fish.name}',
    );
    final sizeText = Text(
      '大きさ: ${fish.size} cm',
    );
    final priceText = Text(
      '値段: ${fish.price} 万円',
    );

    final button = ElevatedButton(
      onPressed: () => onPressed(ref),
      child: const Text('変更する'),
    );

    final column = Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        nameText,
        sizeText,
        priceText,
        button,
      ],
    );

    // 画面の真ん中にカラムを置く
    return Scaffold(
      body: Center(
        child: column,
      ),
    );
  }

  // ボタンを押したときの関数
  void onPressed(WidgetRef ref) {
    // 今画面に出ている魚
    final fish = ref.read(fishProvider);

    // 入れ物ごと変えた 新しい魚
    final newFish = fish.copyWith(
      // 値段を 500 にする
      price: 500,
    );

    // 画面を変更する
    ref.read(fishProvider.notifier).state = newFish;
  }
}
```
