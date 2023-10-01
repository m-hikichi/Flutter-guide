# BottomNavigationBar

BottomNavigationBarは、アプリケーションの下部に表示されるナビゲーションバーです。これは、ユーザーがアプリケーション内で簡単に移動できるようにするためのものです。

## BottomNavigationBarItem

BottomNavigationBarItemは、BottomNavigationBar内の各項目を表すウィジェットです。これは、アイコンとラベルを持つことができます。

### サンプルコード

BottomNavigationBarItemを作成するには、アイテムとラベルを指定します。ここでは、`Icon(Icons.home)`をアイコンとして、`Home`をラベルとして使用しています。

```dart
BottomNavigationBarItem(
  icon: Icon(Icons.home),
  label: 'Home',
)
```

## BottomNavigationBar

### サンプルコード

```dart
BottomNavigationBar(
  items: // BottomNavigationBarItemのリスト,
  backgroundColor: // バーの色,
  selectedItemColor: // 選択されたアイテムの色,
  unselectedItemColor: // 選択されていないアイテムの色,
  currentIndex: // インデックス,
  onTap: // インデックスを変更するための処理,
)
```

## Scaffoldの設定

`body`には、`pages`の中からindexに合わせてページが選ばれるように、`bottomNavigationBar`には、BottomNavigationBarを設定する。

```dart
const pages = [
  PageA(),
  PageB(),
  PageC(),
];

Scaffold(
  body: pages[index],
  bottomNavigationBar: bar,
);
```

## 全体のサンプルコード

`page_a.dart`
```dart
import 'package:flutter/material.dart';


class PageA extends StatelessWidget {
  const PageA({super.key});

  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      backgroundColor: Colors.white,
      body: Center(
        child: Text(
          '画面 A',
          style: TextStyle(
            // 文字の大きさ
            fontSize: 20,
            // 文字の太さ
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

`main.dart`
```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'page_a.dart';
import 'page_b.dart';
import 'page_c.dart';


// プロバイダー
final indexProvider = StateProvider(
  (ref) {
    // 初期値を設定（変化するデータ 0, 1, 2...）
    return 0;
  }
);

// 画面全体
class Root extends ConsumerWidget {
  const Root({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // インデックスを監視しておく
    final index = ref.watch(indexProvider);

    // ボトムナビゲーションバーのアイテム
    const items = [
      BottomNavigationBarItem(
        icon: Icon(Icons.person),
        label: 'アイテムA',
      ),
      BottomNavigationBarItem(
        icon: Icon(Icons.home),
        label: 'アイテムB',
      ),
      BottomNavigationBarItem(
        icon: Icon(Icons.settings),
        label: 'アイテムC',
      ),
    ];

    // ボトムナビゲーションバーの設定
    final bar = BottomNavigationBar(
      items: items,
      backgroundColor: Colors.blue,
      selectedItemColor: Colors.white,
      unselectedItemColor: Colors.black,
      currentIndex: index,
      onTap: (index) {
        // タップされたとき インデックスを変更する
        ref.read(indexProvider.notifier).state = index;
      },
    );

    const pages = [
      PageA(),
      PageB(),
      PageC(),
    ];

    return Scaffold(
      body: pages[index],
      bottomNavigationBar: bar,
    );
  }
}


main() {
  // アプリ
  const app = MaterialApp(home: Root());

  // プロバイダースコープでアプリを囲む
  const scope = ProviderScope(child: app);
  runApp(scope);
}
```
