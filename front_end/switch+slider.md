# FlutterのSwitch・Sliderウィジェットについて

## Switch

Switchウィジェットは、ユーザーがオンとオフの状態を切り替えることができるウィジェットです。

### Switchウィジェットの作成

```dart
Switch(
  value: isSwitched,
  onChanged: (Switchedvalue) {
    ref.read(isSwitchedProvider.notifier).state = Switchedvalue;
  },
  activeColor: Colors.blue,
  activeTrackColor: Colors.green,
  inactiveThumbColor: Colors.black,
  inactiveTrackColor: Colors.grey,
);
```

ここで、`isSwitched`はbool型の変数で、Switchの現在の状態（オンまたはオフ）を保持します。

### Switchウィジェットのプロパティ

- `value` : Switchが現在オンかオフかを示すbool値です。trueならオン、falseならオフです。
- `onChanged` : Switchが切り替えられたときに呼び出されるコールバック関数です。この関数は新しい値を引数として受け取ります。

### Switchウィジェットのカスタマイズ
Switchウィジェットは、色やサイズなど、さまざまな方法でカスタマイズすることができます。

- `activeColor` : Switchがオンのときの色を設定します。
- `activeTrackColor` : Switchがオンのときのトラック（スイッチの背景）の色を設定します。
- `inactiveThumbColor` : Switchがオフのときの色を設定します。
- `inactiveTrackColor` : Switchがオフのときのトラック（スイッチの背景）の色を設定します。

### サンプルコード

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';


void main() {
  const app = MaterialApp(home: Sample());
  const scope = ProviderScope(child: app);
  runApp(scope);
}

final isSwitchedProvider = StateProvider((ref) {
  return true;
});

class Sample extends ConsumerWidget {
  const Sample({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final isSwitched = ref.watch(isSwitchedProvider);
    final toggleSwitch = Switch(
      value: isSwitched,
      onChanged: (Switchedvalue) {
        ref.read(isSwitchedProvider.notifier).state = Switchedvalue;
      },
      activeColor: Colors.blue,
      activeTrackColor: Colors.green,
      inactiveThumbColor: Colors.black,
      inactiveTrackColor: Colors.grey,
    );

    final text = Text(isSwitched ? "True" : "False");

    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            toggleSwitch,
            text,
          ],
        ),
      ),
    );
  }
}
```


## Slider

Sliderウィジェットは、ユーザーが値を選択するためのウィジェットです。

### Sliderウィジェットの作成

```dart
Slider(
  value: value,
  min: 0.0,
  max: 100.0,
  onChanged: (double value) {
    ref.read(valueProvider.notifier).state = value;
  },
  thumbColor: Colors.blue,
  activeColor: Colors.green,
  inactiveColor: Colors.red,
);
```

ここで、`currentValue`はdouble型の変数で、Sliderの現在の値を保持します。

### Sliderウィジェットのプロパティ

- `value` : Sliderの現在の値を示すdouble値です。
- `min` : Sliderの最小値を示すdouble値です。
- `max` : Sliderの最大値を示すdouble値です。
- `onChanged` : Sliderが移動したときに呼び出されるコールバック関数です。この関数は新しい値を引数として受け取ります。

### Sliderウィジェットのカスタマイズ
Sliderウィジェットは、色やサイズなど、さまざまな方法でカスタマイズすることができます。

- `thumbColor` : スライダーのつまみ（ユーザーがドラッグする部分）の色を設定します。
- `activeColor` : Sliderがアクティブ（つまり、現在の値）のときの色を設定します。
- `inactiveColor` : Sliderが非アクティブ（つまり、現在の値より大きいまたは小さい）のときの色を設定します。

### サンプルコード

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';


void main() {
  const app = MaterialApp(home: Sample());
  const scope = ProviderScope(child: app);
  runApp(scope);
}

final valueProvider = StateProvider((ref) {
  return 0.0;
});

class Sample extends ConsumerWidget {
  const Sample({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final value = ref.watch(valueProvider);
    final slider = Slider(
      value: value,
      min: 0.0,
      max: 100.0,
      onChanged: (double value) {
        ref.read(valueProvider.notifier).state = value;
      },
      thumbColor: Colors.blue,
      activeColor: Colors.green,
      inactiveColor: Colors.red,
    );

    final text = Text("$value");

    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            slider,
            text,
          ],
        ),
      ),
    );
  }
}
```


## RangeSlider

RangeSliderウィジェットは、ユーザーが範囲を選択するためのウィジェットです。

### RangeSliderウィジェットの作成

```dart
RangeSlider(
  values: range,
  min: 0.0,
  max: 100.0,
  onChanged: (RangeValues value) {
    ref.read(rangeProvider.notifier).state = value;
  },
  activeColor: Colors.green,
  inactiveColor: Colors.red,
);
```

ここで、`currentRangeValues`はRangeValues型の変数で、RangeSliderの現在の値を保持します。

### RangeSliderウィジェットのプロパティ

- `values` : RangeSliderの現在の値を示すRangeValues値です。これは選択された範囲の最小値と最大値を含みます。
- `min` : RangeSliderの最小値を示すdouble値です。
- `max` : RangeSliderの最大値を示すdouble値です。
- `onChanged` : Sliderが移動したときに呼び出されるコールバック関数です。この関数は新しい範囲を引数として受け取ります。

### RangeSliderウィジェットのカスタマイズ
RangeSliderウィジェットは、色やサイズなど、さまざまな方法でカスタマイズすることができます。

- `activeColor` : RangeSliderがアクティブ（つまり、現在の範囲）のときの色を設定します。
- `inactiveColor` : RangeSliderが非アクティブ（つまり、現在の範囲より大きいまたは小さい）のときの色を設定します。

### サンプルコード

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';


void main() {
  const app = MaterialApp(home: Sample());
  const scope = ProviderScope(child: app);
  runApp(scope);
}

final rangeProvider = StateProvider((ref) {
  return const RangeValues(10, 90);
});

class Sample extends ConsumerWidget {
  const Sample({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final range = ref.watch(rangeProvider);
    final rangeSlider = RangeSlider(
      values: range,
      min: 0.0,
      max: 100.0,
      onChanged: (RangeValues value) {
        ref.read(rangeProvider.notifier).state = value;
      },
      activeColor: Colors.green,
      inactiveColor: Colors.red,
    );

    final text = Text("$range");

    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            rangeSlider,
            text,
          ],
        ),
      ),
    );
  }
}
```
