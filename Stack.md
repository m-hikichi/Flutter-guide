# Stackウィジェットとは

Stackウィジェットは、複数のウィジェットを重ねて表示するためのウィジェットです。例えば、背景画像の上にテキストを表示したり、ボタンを画像の特定の位置に配置したりすることが可能です。

## Stackウィジェットの基本的な使い方

以下の例では、ウィジェットAが一番奥に、ウィジェットBがその上に、ウィジェットCが一番手前に表示されます。これは、`children`リストの順序によって決まります。リストの最初のウィジェットが最も奥に、最後のウィジェットが最も手前に表示されます。

```dart
Stack(
    children: [
        A, // 奥
        B,
        C, // 手前
    ],
)
```

## Positionedウィジェット

Positionedウィジェットは、Stackの中で自由に配置できるウィジェットです。これにより、ウィジェットの位置をピクセル単位で正確に制御することが可能になります。`left`、`right`、`top`、`bottom`の各パラメータを使用して、ウィジェットの位置を指定します。また、`width`と`height`を指定することでウィジェットのサイズを調整することもできます。

```dart
Stack(
    children: [
        Positioned(
            left:
            right:
            top:
            bottom:
            width:
            height:
            child:
            ...
        ),
    ],
)
```

## Align

Alignウィジェットは、Stack内のウィジェットを特定の位置に配置するためのウィジェットです。これは、Positionedウィジェットと同様に、ウィジェットの位置を制御するために使用されますが、Alignウィジェットは、ウィジェットを特定の「アライメント」に配置します。これにより、ウィジェットをStackの特定の位置に簡単に配置することができます。
```dart
Stack(
    children: [
        Align(
            alignment: Alignment.topLeft,
            child: Text("Hello World"),
        ),
    ],
)
```

また、`Alignment(x, y)`を使用して、-1から1の範囲でウィジェットの位置を指定することもできます。ここで、(-1, -1)は左下、(0, 0)は中央、(1, 1)は右上を表します。

```dart
Stack(
    children: [
        Align(
            alignment: Alignment(0.5, 0.5),
            child: Text("Hello World"),
        ),
    ],
)
```

## クリッピングの選択

Stackウィジェットは、子ウィジェットがStackの境界を超えて描画されるかどうかを制御する`clipBehavior`プロパティを持っています。`Clip.none`を設定すると、子ウィジェットはStackの境界を超えて描画されます。一方、`Clip.hardEdge`を設定すると、子ウィジェットはStackの境界で切り取られ、境界を超えて描画されません。
```dart
Stack(
    clipBehavior: Clip.none // 切り取りなし
    children:
)
```
```dart
Stack(
    clipBehavior: Clip.hardEdge // 切り取り
    children:
)
```