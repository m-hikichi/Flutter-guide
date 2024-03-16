# ダイアログ
アプリ画面の最前面に表示され、大事な確認・お知らせ・注意を知らせてくれるUIです。

## AlertDialog
`AlertDialog`はタイトル、メッセージ、ボタンがある一般的なダイアログです。
- `title`：ダイアログの上部に表示されるテキストです。
- `content`：ダイアログの主要なメッセージを表示します。
- `actions`：ダイアログの下部に表示されるボタンのリストです。
```dart
AlertDialog(
    title: タイトル
    content: コンテント
    actions: [
        アクションA
        アクションB
    ]
)
```

## ダイアログの表示
`showDialog`関数を使用してダイアログを表示します。
```dart
showDialog(
    context: context,
    builder: (_) => 表示したいダイアログ,
)
```

## サンプルコード
```dart
import 'package:flutter/material.dart';

class LemonDialog extends StatelessWidget {
  const LemonDialog({super.key});

  @override
  Widget build(BuildContext context) {
    return AlertDialog(
        title: const Text("レモン"),
        content: const Text("唐揚げにかけてもいいですか？"),
        actions: [
          TextButton(
              onPressed: () {
                // ダイアログを閉じる
                Navigator.pop(context, "Cancel");
              },
              child: const Text("キャンセル")),
          TextButton(
              onPressed: () {
                // ダイアログを閉じる
                Navigator.pop(context, "OK");
              },
              child: const Text("OK")),
        ]);
  }
}

/// ホーム画面
class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: ElevatedButton(
          onPressed: () async {
            // レモンダイアログを表示: showDialog
            // ダイアログが閉じるのを待つ: await
            // ダイアログの回答を受け取る: answer
            final answer = await showDialog(
              context: context,
              builder: (_) => const LemonDialog(),
            );

            // 回答を確認
            debugPrint(answer);
          },
          child: const Text('開く'),
        ),
      ),
    );
  }
}

/// アプリ本体
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(home: HomePage());
  }
}

void main() {
  const app = MyApp();
  runApp(app);
}
```
