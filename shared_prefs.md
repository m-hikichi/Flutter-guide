# shared_preferencesとは
`shared_preferences`は、Flutterで使用できるキーと値のペアを保存するための永続的なストレージを提供するパッケージです。

## shared_preferencesの導入方法
1. `pubspec.yaml`ファイルに`shared_preferences`パッケージを追加します。
    ```yaml
    dependencies:
      shared_preferences:
    ```
2. パッケージをインストールします。プロジェクトのルートディレクトリで以下のコマンドを実行します。
    ```
    flutter pub get
    ```
3. 使用したいDartファイルでパッケージをインポートします。
    ```dart
    import 'package:shared_preferences/shared_preferences.dart';
    ```

## shared_preferencesを使ったデータの保存と読み込み
まず、SharedPreferencesインスタンスを取得します。
```dart
SharedPreferences prefs = await SharedPreferences.getInstance();
```

次に、保存したいデータ型に応じて適切なメソッドを選択します。
- 整数値を保存
    ```dart
    await prefs.setInt('my_int_key', 10);
    ```
- 浮動小数点数を保存
    ```dart
    await prefs.setDouble('my_double_key', 10.0);
    ```
- 文字列を保存
    ```dart
    await prefs.setString('my_string_key', 'Hello, World!');
    ```
- ブール値を保存
    ```dart
    await prefs.setBool('my_bool_key', true);
    ```
- 文字列のリストを保存
    ```dart
    await prefs.setStringList('my_string_list_key', ['a', 'b', 'c']);
    ```

データを読み込むには、以下のようにします。
- 整数値を保存
    ```dart
    final int myIntValue = prefs.getInt('my_int_key') ?? 0;
    ```
- 浮動小数点数を保存
    ```dart
    final double myDoubleValue = prefs.getDouble('my_double_key') ?? 0.0;
    ```
- 文字列を保存
    ```dart
    final String myStringValue = prefs.getString('my_string_key') ?? '';
    ```
- ブール値を保存
    ```dart
    final bool myBoolValue = prefs.getBool('my_bool_key') ?? false;
    ```
- 文字列のリストを保存
    ```dart
    final List<String> myStringListValue = prefs.getStringList('my_string_list_key') ?? [];
    ```
