# Flutter 布局与 Constraints


## Flutter 布局
[基础布局](https://docs.flutter.dev/development/ui/layout)


👇🏻下面的组件[https://api.flutter.dev/](https://api.flutter.dev/)搜索

了解 Row , Column 类似于 Flex 盒子布局  
了解 Stack , Stack 下面嵌套 Position 类似于 Position  
了解 ListView  , 为组件添加 滚动条  
了解 [GridView](https://api.flutter.dev/flutter/widgets/GridView-class.html)  , [Grid 布局](https://youtu.be/bLOtZDTm4H8)  




## flutter Constraints


![核心 constraints 图片](https://docs.flutter.dev/assets/images/docs/ui/layout/article-hero-image.png)


| | | |
| ----------- | ----------- |   ----------- |
| constraints  | 向下约束    |    (constraints go down) | 
| size        | 上报         | (sizes go up) |
| position   |   父级决定    |    (parents sets position)|

[官方介绍 Constraints （了解松约束，紧约束） ](https://docs.flutter.dev/development/ui/layout/box-constraints)  
[官方推荐的文档 深入理解 Constraints](https://docs.flutter.dev/development/ui/layout/constraints)


> tips:  使用 LayoutBuilder 可以查看父级传递过来的 constraints ()

```dart
LayoutBuilder(
    builder: (BuildContext context, BoxConstraints constraints) {
        if (constraints.maxWidth > 600) {
        return _buildWideContainers();
        } else {
        return _buildNormalContainer();
        }
    },
```


---- 
### 从了解约束开始 , 👇🏻是定义的地方
```dart 
// constraints
class BoxConstraints extends Constraints {
  /// Creates box constraints with the given constraints.
  const BoxConstraints({
    this.minWidth = 0.0,
    this.maxWidth = double.infinity,
    this.minHeight = 0.0,
    this.maxHeight = double.infinity,
  }) : assert(minWidth != null),
       assert(maxWidth != null),
       assert(minHeight != null),
       assert(maxHeight != null);


  /// The minimum width that satisfies the constraints.
  final double minWidth;

  /// The maximum width that satisfies the constraints.
  ///
  /// Might be [double.infinity].
  final double maxWidth;

  /// The minimum height that satisfies the constraints.
  final double minHeight;

  /// The maximum height that satisfies the constraints.
  ///
  /// Might be [double.infinity].
  final double maxHeight;

```

### 了解松约束和紧约束

```dart
 
/// Creates box constraints that is respected only by the given size.
  BoxConstraints.tight(Size size)
    : minWidth = size.width,
      maxWidth = size.width,
      minHeight = size.height,
      maxHeight = size.height;
```
紧约束 -- 强制子 Widget 的大小必须满足约束值 , 子widget 期望的 size 必须满足 约束
size 最后呈现的大小，根据一系列的规则


```dart

    //this.minWidth = 0.0,
   // this.maxWidth = double.infinity,
    //this.minHeight = 0.0,
   // this.maxHeight = double.infinity,


 BoxConstraints loosen() {
    
    return BoxConstraints(
      maxWidth: maxWidth,
      maxHeight: maxHeight,
    );
  }
```
松约束 -- 传递给子组件的是  0 - maxWidth  ， 0 - maxHeight


-----


    
```dart
runApp(
    Container(width:100,height:100,color:Colors.red)
)
```
此处出现，全屏红色的原因是 根组件传递个给Container 的约束是紧约束，

```dart
runApp(
    Align(
        aliment: Aligment.center,
        child:Container(width:100,height:100,color:Colors.red)
    )
)
```
Align 承受了紧约束，传递给 Container 是松约束 
> tips 这时候 Align 的 是个大的盒子，想要 正确的渲染出 Contaienr 这个小盒子，按照GUI编程的思路, 还需要考虑到 Container 在 Align 的位置。这里需要引入 Offset 的概念


![官方图片](https://docs.flutter.dev/assets/images/docs/ui/layout/children.png)


> Widget: “嘿！我的父级。我的约束是多少？”  
> Parent: “你的宽度必须在 80 到 300 像素之间，高度必须在 30 到 85 之间。”  
> Widget: “嗯…我想要 5 个像素的内边距，这样我的子级能最多拥有 290 个像素宽度和 75 个像素高度。”  
> Widget: “嘿，我的第一个子级，你的宽度必须要在 0 到 290，长度在 0 到 75 之间。”  
> First child: “OK，那我想要 290 像素的宽度，20 个像素的长度。”  
> Widget: “嗯…由于我想要将我的第二个子级放在第一个子级下面，所以我们仅剩 55 个像素的高度给第二个子级了。”  
> Widget: “嘿，我的第二个子级，你的宽度必须要在 0 到 290，长度在 0 到 55 之间。”  
> Second child: “OK，那我想要 140 像素的宽度，30 个像素的长度。”  
> Widget: “很好。我的第一个子级将被放在 x: 5 & y: 5 的位置，而我的第二个子级将在 x: 80 & y: 25 的位置。”  
> Widget: “嘿，我的父级，我决定我的大小为 300 像素宽度，60 像素高度。”  





## 总结
约束的理解是了解整个Flutter构建UI的基石，构建UI的规则就是 Constraints


