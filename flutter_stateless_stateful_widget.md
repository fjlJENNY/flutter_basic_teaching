# 从 StatelessWidget 和 StatefulWidget 开始认识 widget

> **Widget是配置项，所有的入参字段都是 final** 

> **[官方文档 Introduction to widgets](https://docs.flutter.dev/development/ui/widgets-intro)**

```dart
// Hello World
import 'package:flutter/material.dart';

void main() {
  runApp(
    const Center(
      child: Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```



## StatelessWidget

Stateless 是一个空白节点，Stateless 存在的意义就是 **“不可变组合（件）”**  ***(只可接受参数)***

![手指](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8b1f968d55264972867ab39c47e62176~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)

```dart
// 下面形成了 "组件"  Finger (Widget)
class Finger extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return Column(
        children:[
            FingerA()，
            FingerB(),
            FingerC(),
        ],
    ),
  }
}
```


## StatefulWidget

StatefulWidget 同样是一个空白节点，StatefulWidget  **“是”** 个 **“可变组合（件）”** 


```dart
class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
  
    return Row(
      children: <Widget>[
        RaisedButton(
          onPressed: _increment,
          child: Text('Increment'),
        ),
        Text('Count: $_counter'),
      ],
    );
  }
}

```

~~StatefulWiget 存储内部状态~~  State 存储内部状态  
需要更新的地方 setState



## State 组件的生命周期

![https://book.flutterchina.club/chapter2/flutter_widget_intro.html#_2-2-6-state](https://book.flutterchina.club/assets/img/2-5.a59bef97.jpg)



```dart
class CounterWidget extends StatefulWidget {
  const CounterWidget({Key? key, this.initValue = 0});

  final int initValue;

  @override
  _CounterWidgetState createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;

  @override
  void initState() {
    super.initState();
    //初始化状态
    _counter = widget.initValue;
    print("initState");
  }

  @override
  Widget build(BuildContext context) {
    print("build");
    return Scaffold(
      body: Center(
        child: TextButton(
          child: Text('$_counter'),
          //点击后计数器自增
          onPressed: () => setState(
            () => ++_counter,
          ),
        ),
      ),
    );
  }

  @override
  void didUpdateWidget(CounterWidget oldWidget) {
    super.didUpdateWidget(oldWidget);
    print("didUpdateWidget ");
  }

  @override
  void deactivate() {
    super.deactivate();
    print("deactivate");
  }

  @override
  void dispose() {
    super.dispose();
    print("dispose");
  }

  @override
  void reassemble() {
    super.reassemble();
    print("reassemble");
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    print("didChangeDependencies");
  }
}
```


- initState：当 widget 第一次插入到 widget 树时会被调用，对于每一个State对象，Flutter 框架只会调用一次该回调，所以，通常在该回调中做一些一次性的操作，如状态初始化、订阅子树的事件通知等。不能在该回调中调用BuildContext.dependOnInheritedWidgetOfExactType（该方法用于在 widget 树上获取离当前 widget 最近的一个父级InheritedWidget，关于InheritedWidget我们将在后面章节介绍），原因是在初始化完成后， widget 树中的InheritFrom widget也可能会发生变化，所以正确的做法应该在在build（）方法或didChangeDependencies()中调用它。

- didChangeDependencies()：当State对象的依赖发生变化时会被调用；例如：在之前build() 中包含了一个InheritedWidget （第七章介绍），然后在之后的build() 中Inherited widget发生了变化，那么此时InheritedWidget的子 widget 的didChangeDependencies()回调都会被调用。典型的场景是当系统语言 Locale 或应用主题改变时，Flutter 框架会通知 widget 调用此回调。需要注意，组件第一次被创建后挂载的时候（包括重创建）对应的didChangeDependencies也会被调用。

- build()：此回调读者现在应该已经相当熟悉了，它主要是用于构建 widget 子树的，会在如下场景被调用：
    1. 在调用initState()之后。
    2. 在调用didUpdateWidget()之后。
    3. 在调用setState()之后。
    4. 在调用didChangeDependencies()之后。
    5. 在State对象从树中一个位置移除后（会调用deactivate）又重新插入到树的其他位置之后。
    
- reassemble()：此回调是专门为了开发调试而提供的，在热重载(hot reload)时会被调用，此回调在Release模式下永远不会被调用。

- didUpdateWidget ()：在 widget 重新构建时，Flutter 框架会调用widget.canUpdate来检测 widget 树中同一位置的新旧节点，然后决定是否需要更新，如果widget.canUpdate返回true则会调用此回调。正如之前所述，widget.canUpdate会在新旧 widget 的 key 和 runtimeType 同时相等时会返回true，也就是说在在新旧 widget 的key和runtimeType同时相等时didUpdateWidget()就会被调用。

- deactivate()：当 State 对象从树中被移除时，会调用此回调。在一些场景下，Flutter 框架会将 State 对象重新插到树中，如包含此 State 对象的子树在树的一个位置移动到另一个位置时（可以通过GlobalKey 来实现）。如果移除后没有重新插入到树中则紧接着会调用dispose()方法。

- dispose()：当 State 对象从树中被永久移除时调用；通常在此回调中释放资源。


> [上面生命周期的 来源](https://book.flutterchina.club/chapter2/flutter_widget_intro.html#_2-2-6-state)


## StatelessWidget Vs StatefulWidget

结论 StatefulWidget 比  StatelessWidget 多了创建 State  

State “Element tree 状态的映射” , 可以 "添加局部的变量", 通过 setState 修改局部变量，导致组件的重新创建。修改页面 UI
 



