# JSONとは

JSONは、データを転送するためのシンプルなテキスト形式のデータ表現です。多くのプログラミング言語で普遍的に使用されているため、JSONは言語間でデータをやり取りするのに適しています。

### jsonDecode

JSON形式の文字列を受け取り、それをJSONデータ構造（JsonMap）に変換します。

### fromJson

JSONデータ構造（JsonMap）からDartオブジェクトを作成するために使用されます。このメソッドは通常、ファクトリコンストラクタとして実装され、JSONデータを解析し、クラスのインスタンスを構築します。

### toJson

DartオブジェクトをJSONデータ構造（JsonMap）に変換するために使用されます。このメソッドは、DartオブジェクトのデータをJSONに適した形式で表現するMapを返します。

### jsonEncode

JSONデータ構造（JsonMap）を受け取り、それをJSON形式の文字列に変換します。

## FlutterにてJSONを扱う方法

1. `pubspec.yaml`を開き、`dependencies`の下に`freezed_annotation`を追加する。
    ```yaml
    dependencies:
        freezed_annotation:
    ```

2. `dev_dependencies`を開き、`dev_dependencies`に`freezed`・`build_runnter`・`json_serializable`を追加する。
    ```yaml
    dev_dependencies:
        freezed:
        build_runner:
        json_serializable:
    ```

## JSONの扱い（例１）
### JSON 例
```json
{
    "name": "トマト",
    "color": "赤",
    "season": "夏"
}
```

<details>
<summary>JSONを格納する野菜クラス</summary>

```dart
import 'package:freezed_annotation/freezed_annotation.dart';
part 'vegetable.freezed.dart';
part 'vegetable.g.dart';

@freezed
class Vegetable with _$Vegetable {
  const factory Vegetable({
    required String name,
    required String color,
    required String season,
  }) = _Vegetable;
  factory Vegetable.fromJson(Map<String, dynamic> json) => _$VegetableFromJson(json);
}
```
</details>

### jsonDecode・fromJson 例
```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'vegetable.dart';

void main() async {
  // Stubを使えるようにする
  WidgetsFlutterBinding.ensureInitialized();

  // JSON <-- Stub
  final json = await rootBundle.loadString("stub/level1.json");

  // JsonMap <-- JSON
  final map = jsonDecode(json);

  // 野菜データ <-- JsonMap
  final data = Vegetable.fromJson(map);

  // データの中身を確認
  debugPrint("データの中身： $data");
}
```

## toJson・jsonEncode 例

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'vegetable.dart';

void main() async {
  // 適当な野菜のデータ
  const data = Vegetable(
    name: "キャベツ",
    color: "緑",
    season: "冬"
  );

  // JsonMap <-- 野菜データ
  final map = data.toJson();

  // JSON <-- JsonMap
  final json = jsonEncode(map);

  // JSONの中身を確認する
  debugPrint("JSONの中身: $json");
}
```

## JSONの扱い（例２）
### JSON例
```json
{
    "size": "中",
    "price": 300,
    "content": {
        "name": "トマト",
        "color": "赤",
        "season": "夏"
    }
}
```

<details>
<summary>JSONを格納する野菜パッククラス</summary>

```dart
import 'package:freezed_annotation/freezed_annotation.dart';
import 'vegetable.dart';
part 'pack.freezed.dart';
part 'pack.g.dart';

@freezed
class Pack with _$Pack {
  const factory Pack({
    required String size,
    required int price,
    required Vegetable content,
  }) = _Pack;
  factory Pack.fromJson(Map<String, dynamic> json) => _$PackFromJson(json);
}
```
</details>

### jsonDecode・fromJson 例

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'pack.dart';

void main() async {
  // Stubを使えるようにする
  WidgetsFlutterBinding.ensureInitialized();

  // JSON <-- Stub
  final json = await rootBundle.loadString("stub/level2.json");

  // JsonMap <-- JSON
  final map = jsonDecode(json);

  // 野菜パックデータ <-- JsonMap
  final data = Pack.fromJson(map);

  // データの中身を確認
  debugPrint("データの中身： $data");
}
```

## toJson・jsonEncode 例

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'vegetable.dart';
import 'pack.dart';

void main() async {
  // 適当な野菜のデータ
  const content = Vegetable(
    name: "アボガド",
    color: "緑",
    season: "秋"
  );
  // 適当な野菜パックのデータ
  const data = Pack(
    size: "中",
    price: 800,
    content: content,
  );

  // JsonMap <-- 野菜データ
  final map = data.toJson();

  // JSON <-- JsonMap
  final json = jsonEncode(map);

  // JSONの中身を確認する
  debugPrint("JSONの中身: $json");
}
```

## JSONの扱い（例３）
### JSON例
```json
{
    "title": "ほくほくカレー",
    "calories": 600,
    "vegetables": [
        {
            "name": "タマネギ",
            "color": "白",
            "season": "すべての季節"
        },
        {
            "name": "ニンジン",
            "color": "オレンジ",
            "season": "春・夏・冬"
        },
        {
            "name": "ジャガイモ",
            "color": "茶",
            "season": "春・秋"
        }
    ]
}
```

<details>
<summary>JSONを格納するレシピクラス</summary>

```dart
import 'package:freezed_annotation/freezed_annotation.dart';
import 'vegetable.dart';
part 'recipe.freezed.dart';
part 'recipe.g.dart';

@freezed
class Recipe with _$Recipe {
  const factory Recipe({
    required String title,
    required int calories,
    required List<Vegetable> vegetables,
  }) = _Recipe;
  factory Recipe.fromJson(Map<String, dynamic> json) => _$RecipeFromJson(json);
}
```
</details>

### jsonDecode・fromJson 例

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'recipe.dart';

void main() async {
  // Stubを使えるようにする
  WidgetsFlutterBinding.ensureInitialized();

  // JSON <-- Stub
  final json = await rootBundle.loadString("stub/level3.json");

  // JsonMap <-- JSON
  final map = jsonDecode(json);

  // レシピデータ <-- JsonMap
  final data = Recipe.fromJson(map);

  // データの中身を確認
  debugPrint("データの中身： $data");
}
```

## toJson・jsonEncode 例

```dart
略
```
