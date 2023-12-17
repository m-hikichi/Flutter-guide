# Radio・Checkbox

## Radio

たくさんの候補の中から、どれか一つを選んでもらうためのUIです。

### RadioListTile

```dart
RadioListTile(
    groupValue: radioId,
    onChanged: // ラジオボタンが押されたときに実行する関数,
    value: // ラジオボタンに付けたいID,
    title: // 表示する文字,
),
```

### サンプルコード

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

void main() {
  const app = MaterialApp(home: Home());
  const scope = ProviderScope(child: app);
  runApp(scope);
}

// 選ばれたラジオボタンID
final radioIdProvider = StateProvider<String?>((ref) {
  // 最初はどれも選ばれていないので null
  return null;
});

class Home extends ConsumerWidget {
  const Home({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // ラジオボタンID に合わせて画面を変化
    final radioId = ref.watch(radioIdProvider);

    // ラジオボタンが押されたときの関数
    void onChangedRadio(String? id) {
      ref.read(radioIdProvider.notifier).state = id!;
    }

    // 縦に並べる
    final col = Column(
      children: [
        // ラジオボタンたち

        RadioListTile(
          groupValue: radioId,
          onChanged: onChangedRadio,
          value: 'A',
          title: const Text('ラジオボタンA'),
        ),

        RadioListTile(
          groupValue: radioId,
          onChanged: onChangedRadio,
          value: 'B',
          title: const Text('ラジオボタンB'),
        ),

        RadioListTile(
          groupValue: radioId,
          onChanged: onChangedRadio,
          value: 'C',
          title: const Text('ラジオボタンC'),
        ),

        // OK ボタン
        ElevatedButton(
          onPressed: () {
            // 選ばれたラジオボタンIDを確認する
            debugPrint(radioId);
          },
          child: const Text('OK'),
        ),
      ],
    );

    return Scaffold(
      body: col,
    );
  }
}
```

## Checkbox

同時に何個でも選んでもらうためのUIです。

### Switchウィジェットとの使い分け

- `Checkbox`：後でまとめて設定したい場合。Checkboxリストの下に「OK」ボタンなどを配置し、OKボタンが押された際にまとめてCheckboxの値を反映させます。
- `Switch`：1つずつすぐに設定したい場合。Switchの値が切り替えられた瞬間に反映されます。
### CheckboxListTile

```dart
CheckboxListTile(
    onChanged: // チェックが付けられたときに実行する関数,
    value: // チェックされたかどうか（trueまたはfalse）,
    title: // 表示する文字,
),
```

### サンプルコード

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

void main() {
  const app = MaterialApp(home: Home());
  const scope = ProviderScope(child: app);
  runApp(scope);
}

// 選ばれたチェックボックスIDたち
final checkedIdsProvider = StateProvider<Set<String>>((ref) {
  // 最初は空っぽ {}
  return {};
});

class Home extends ConsumerWidget {
  const Home({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // チェックボックスIDたち に合わせて画面を変化
    final checkedIds = ref.watch(checkedIdsProvider);

    // チェックボックスが押された時の関数
    void onChangedCheckbox(String id) {
      final newSet = Set.of(checkedIds);
      if (checkedIds.contains(id)) {
        newSet.remove(id);
      } else {
        newSet.add(id);
      }
      ref.read(checkedIdsProvider.notifier).state = newSet;
    }

    // 縦に並べる
    final col = Column(
      children: [
        CheckboxListTile(
          onChanged: (check) => onChangedCheckbox('A'),
          value: checkedIds.contains('A'),
          title: const Text('チェックボックスA'),
        ),

        CheckboxListTile(
          onChanged: (check) => onChangedCheckbox('B'),
          value: checkedIds.contains('B'),
          title: const Text('チェックボックスB'),
        ),

        CheckboxListTile(
          onChanged: (check) => onChangedCheckbox('C'),
          value: checkedIds.contains('C'),
          title: const Text('チェックボックスC'),
        ),

        // OK ボタン
        ElevatedButton(
          onPressed: () {
            // 選ばれたチェックボックスIDを確認する
            debugPrint(checkedIds.toString());
          },
          child: const Text('OK'),
        ),
      ],
    );

    return Scaffold(
      body: col,
    );
  }
}
```
