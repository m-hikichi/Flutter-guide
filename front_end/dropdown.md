# Dropdown

## switch

`switch`は、値をチェックし、それに対応する処理を行うための構文です。通常、複数の`if`文や`else if`文を使用する代わりに、`switch`文を活用することでコードがより読みやすく、管理しやすくなります。

### switch文

```dart
switch (変数) {
    case 値1:
        // 値1に対する処理
        break;
    case 値2:
        // 値1に対する処理
        break;
    default:
        // どのcaseにも該当しない場合の処理
}
```

### switch式

```dart
const x = 1;

final tmp = switch (x) {
    1 => "one",
    2 => "two",
    3 => "three",
    int() => "over"
};
```

## enum

`enum`は、一連の固定された値を管理するために使用されます。

```dart
enum Day {
    sun,  // 日
    mon,  // 月
    tue,  // 火
    wed,  // 水
    thu,  // 木
    fri,  // 金
    sat,  // 土
}

Day today = Day.sun;
print(today);
```

## dropdown

ドロップダウンメニューは、ユーザーがリストから1つの項目を選択するためのウィジェットです。例えば、フォームの国選択や設定ページのWiFiネットワーク選択など、ユーザーがリストから選択する必要がある場面でよく使用されます。

### DropdownButton

Flutterでドロップダウンメニューを表示するには、`DropdownButton`を使用します。`DropdownButton`のプロパティで，`items`・`value`・`onChanged`は必須です。

|プロパティ|説明|
|:--|:--|
|`items`|ドロップダウンで選択できる値|
|`value`|選択中の値|
|`onChanged`|値が選択されたときの処理|
|`dropdownColor`|ドロップダウンの背景色|
|`elevation`|リストを開いた時の影の濃さ|
|`icon`|ドロップダウンボタンのアイコン|
|`iconSize`|ドロップダウンボタンのアイコンの大きさ|
|`itemHeight`|リストの高さ|
|`style`|テキストスタイル|
|`underline`|ドロップダウンボタンの下線|

### DropdownMenuItem

`DropdownMenuItem`の選択肢は、`DropdownMenuItem`で作成します。この時、`child`と`value`プロパティを設定する必要があります。

```dart
DropdownMenuItem(
    value: 1,
    child: Text("1"),
)
```

## サンプルコード

### enum
```dart
import 'package:riverpod_annotation/riverpod_annotation.dart';
part 'season.g.dart';

/// 季節
enum Season {
  spring, // 春
  summer, // 夏
  autumn, // 秋
  winter, // 冬
}

/// 季節を状態管理
@riverpod
class SeasonNotifier extends _$SeasonNotifier {
  @override
  Season build() {
    // 初期値
    return Season.spring;
  }

  /// 季節を変更する
  void updateSeason(Season season) {
    state = season;
  }
}
```

### dropdown
```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'season.dart';

class SeasonDropdown extends ConsumerWidget {
  const SeasonDropdown({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // 選択されている季節
    final season = ref.watch(seasonNotifierProvider);

    final items = [
      const DropdownMenuItem(
        value: Season.spring,
        child: Text("春"),
      ),
      const DropdownMenuItem(
        value: Season.summer,
        child: Text("夏"),
      ),
      const DropdownMenuItem(
        value: Season.autumn,
        child: Text("秋"),
      ),
      const DropdownMenuItem(
        value: Season.winter,
        child: Text("冬"),
      ),
    ];

    // ドロップダウン本体
    return DropdownButton(
        value: season,
        items: items,
        onChanged: (newSeason) {
          // 状態管理 -> 季節を変更
          final notifier = ref.read(seasonNotifierProvider.notifier);
          notifier.updateSeason(newSeason!);
        });
  }
}
```

### switch
```dart
import 'package:flutter/material.dart';
import 'season.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

/// 季節ごとの時間帯
class SeasonTime extends ConsumerWidget {
  const SeasonTime({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // 選択中の季節
    final season = ref.watch(seasonNotifierProvider);

    // テキスト
    return Text(
      switch (season) {
        Season.spring => 'あけぼの',
        Season.summer => 'よる',
        Season.autumn => 'ゆうぐれ',
        Season.winter => 'つとめて',
      },
    );
  }
}
```
