# Drawer

Drawerは、Flutterアプリケーションでよく使用されるウィジェットの一つで、ナビゲーションメニューを提供します。主にスクリーンの左側からスライドして表示され、アプリケーション内の主要なナビゲーションリンクを含むことが多いです。<br>
Drawerウィジェットは、Scaffoldウィジェットのdrawerプロパティとして設定されます。以下に、Drawer内に表示するサイドメニューの定義方法を示します。

## サイドメニューの定義

サイドメニューは、主に以下の2つの部分で構成されています。

### DrawerHeader

DrawerHeaderは、ドロワーの上部に表示される部分です。ここには、アプリケーションのロゴやユーザーの情報などを表示することができます。

### ListTile

ListTileは、ドロワー内の各メニューアイテムを表します。これらは通常、DrawerHeaderの下にリスト形式で配置されます。各ListTileはタップ可能で、タップすると特定の画面に遷移したり、特定のアクションを実行したりします。

### サンプルコード

`lib/side_menu.dart`
```dart
import 'package:flutter/material.dart';

class SideMenu extends StatelessWidget {
  const SideMenu({super.key});

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: [
        DrawerHeader(
          padding: const EdgeInsets.all(0),
          margin: const EdgeInsets.all(0),
          child: Container(
            color: Colors.blue,
            alignment: Alignment.center,
            child: const Text('DrawerHeader'),
          ),
        ),
        ListTile(
          title: const Text('ListTile A'),
          onTap: () {
            debugPrint('リストタイル A をタップしました');
          },
        ),
        ListTile(
          title: const Text('ListTile B'),
          onTap: () {
            debugPrint('リストタイル B をタップしました');
          },
        ),
        ListTile(
          title: const Text('ListTile C'),
          onTap: () {
            debugPrint('リストタイル C をタップしました');
          },
        ),
      ],
    );
  }
}
```

`lib/main.dart`
```dart
import 'package:flutter/material.dart';
import 'side_menu.dart';

main() {
  // アップバー
  final appBar = AppBar(
    title: const Text('appBar'),
    backgroundColor: Colors.blue,
  );


  // ドロワー
  const drawer = Drawer(
    child: SideMenu(),
  );

  // ボディ
  const body = Center(
    child: Text('body'),
  );

  // 画面
  final scaffold = Scaffold(
    appBar: appBar,
    drawer: drawer,
    body: body,
  );

  // アプリ
  final app = MaterialApp(
    debugShowCheckedModeBanner: false,
    home: scaffold,
  );

  runApp(app);
}
```