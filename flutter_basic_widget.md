# Image 与 Text  与其他基础的 Widget


1）从asset中加载图片

在工程根目录下创建一个images目录，并将图片 avatar.png 拷贝到该目录。

在pubspec.yaml中的flutter部分添加如下内容：


```dart
  assets:
    - images/avatar.png
```

```dart
Image(
  image: AssetImage("images/avatar.png"),
  width: 100.0
);

或者

Image.asset("images/avatar.png",
  width: 100.0,
)
```

2）从网络加载图片

```dart
Image(
  image: NetworkImage(
      "https://avatars2.githubusercontent.com/u/20411648?s=460&v=4"),
  width: 100.0,
)

或者

Image.network(
  "https://avatars2.githubusercontent.com/u/20411648?s=460&v=4",
  width: 100.0,
)
```




-----

```dart

// 基础 Text 组件

Text("Hello world",
  textAlign: TextAlign.left,
);

Text("Hello world! I'm Jack. "*4,
  maxLines: 1,
  overflow: TextOverflow.ellipsis,
);

Text("Hello world",
  textScaleFactor: 1.5,
);
```

```dart
// 实现稍微复杂的 Text , 实现2端 TextSpan

Text.rich(TextSpan(
  children: [
     TextSpan(
       text: "Home: "
     ),
     TextSpan(
       text: "https://flutterchina.club",
       style: TextStyle(
         color: Colors.blue
       ),  
       recognizer: _tapRecognizer
     ),
  ]
))
```


[👆🏻参考](https://book.flutterchina.club/chapter3/text.html#_3-1-3-textspan)

[button 参考](https://docs.flutter.dev/release/breaking-changes/buttons)