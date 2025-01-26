# ProgressIndicator

アプリケーションの状態や進行状況をユーザーに伝えるためのウィジェットです。例えば、アプリをロードしたり、フォームを送信したり、更新を保存したりするときに、ユーザーに処理が完了するまで待たせることがあります。そのときに、`ProgressIndicator`を使うことで、ユーザーに処理の進捗や残り時間を示すことができます。

## Flutter標準のProgressIndicator

Flutterでは、`ProgressIndicator`は基本的なクラスであり、`CircularProgressIndicator`と`LinearProgressIndicator`という2種類のサブクラスがあります。

- `CircularProgressIndicator`<br>
    円型のインジケータで、`valueColor`というプロパティに色を設定することで進行状況を表現します。
- `LinearProgressIndicator`<br>
    直線型のインジケータで、`value`というプロパティに0から1までの値を設定することで進行状況を表現します。

## `percent_indicator`のProgressIndicator

### `CircularPercentIndicator`

```dart
CircularPercentIndicator(
    percent: // パーセントの値を保持する変数,
    backgroundColor: // 背景色,
    progressColor: // 進行状況を表すバーの色,
    radius: // 半径
    lineWidth: // 円の太さ,
);
```

### `LinearPercentIndicator`

```dart
LinearPercentIndicator(
    percent: // パーセントの値を保持する変数,
    backgroundColor: // 背景色,
    progressColor: // 進行状況を表すバーの色,
    alignment: MainAxisAlignment.center,
    lineHeight: // 線の太さ,
    width: // 全体の横幅,
);
```

### サンプルコード

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'package:percent_indicator/percent_indicator.dart';

// メイン関数
void main() {
  const app = MaterialApp(home: Home());
  const scope = ProviderScope(child: app);
  runApp(scope);
}

// どのぐらい進んだかを表すパーセントの状態管理
final percentProvider = StateProvider((ref) {
  // 最初は 0% からスタート
  return 0.00;
});

// ホーム画面
class Home extends ConsumerWidget {
  const Home({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // パーセント
    final percent = ref.watch(percentProvider);

    // 丸型のインジケーター
    final circular = CircularPercentIndicator(
      percent: percent,
      backgroundColor: Colors.grey,
      progressColor: Colors.blue,
      animation: true,
      animationDuration: 200,
      animateFromLastPercent: true,
      radius: 60.0,
      lineWidth: 20.0,
      center: Text('${percent * 100}%'),
    );

    // 棒型のインジケーター
    final linear = LinearPercentIndicator(
      percent: percent,
      backgroundColor: Colors.grey,
      progressColor: Colors.blue,
      animation: true,
      animationDuration: 200,
      animateFromLastPercent: true,
      alignment: MainAxisAlignment.center,
      lineHeight: 20,
      width: 300,
      center: Text('${percent * 100}%'),
    );

    // ボタン
    final button = ElevatedButton(
      onPressed: () => onPressed(ref),
      child: const Text('スタート'),
    );

    // 縦に並べるカラム
    final column = Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        circular,
        linear,
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
  void onPressed(WidgetRef ref) async {
    // 1秒まつ
    await Future.delayed(const Duration(seconds: 1));
    // 20%
    ref.read(percentProvider.notifier).state = 0.20;
    // 1秒まつ
    await Future.delayed(const Duration(seconds: 1));
    // 40%
    ref.read(percentProvider.notifier).state = 0.40;
    // 1秒まつ
    await Future.delayed(const Duration(seconds: 1));
    // 60%
    ref.read(percentProvider.notifier).state = 0.60;
    // 1秒まつ
    await Future.delayed(const Duration(seconds: 1));
    // 80%
    ref.read(percentProvider.notifier).state = 0.80;
    // 1秒まつ
    await Future.delayed(const Duration(seconds: 1));
    // 100%
    ref.read(percentProvider.notifier).state = 1.00;
  }
}
```

## Shimmer Effect

アプリケーションのロード中に、画像やテキストなどのコンテンツを表す形を描いて、光沢や動きを加えることで、ユーザーに処理が完了するまで待たせる効果です。Shimmer Effectは、アプリケーションの見た目やユーザー体体験を向上させるために有効な手法です。
