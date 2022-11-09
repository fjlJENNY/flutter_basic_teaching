
# 状态管理

[**状态管理官方文档**](https://docs.flutter.dev/development/data-and-backend/state-mgmt/declarative)



## 开始以声明书方式思考 , 已数据驱动页面

![Statement](https://docs.flutter.dev/assets/images/docs/development/data-and-backend/state-mgmt/ui-equals-function-of-state.png)


假设一个页面如下

![页面这样](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c14907a559d74eb1b57aa1ca5efe916e~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

一个页面的数据大致分为三种类型  
[1]. 在程序运行期间恒定不可改变的数据。   
[2]. 根据用户交互而产生变化的本地数据。  
[3]. 不由用户直接控制的网络数据。  


## 声明式 VS 命令式

```dart
// 命令式
b.setColor(red)
b.clearChildren()
ViewC c3 = new ViewC(...)
b.add(c3)
```

```dart
// 声明式
 ViewB(
  color: red,
  child: const ViewC(),
);
```

声明式描述此处页面处于什么状态，也是此时数据如何表现。当更改状态，会触发用户界面的重绘  


[状态分为局部状态和全局状态](https://docs.flutter.dev/development/data-and-backend/state-mgmt/ephemeral-vs-app)

局部状态一般使用临时变量保存，使用setState修改状态   
这边介绍的是跨组件（屏幕）的状态   

前端也有状态提升的概念， A是B和C 的父组件，B和C的通信，比较常见的做法是将 状态提升到A上  [参考Rect](https://zh-hans.reactjs.org/docs/lifting-state-up.html)


还有种情况是跨祖先状态交互 ， 前端 React 使用到 Redux,[flutter实现的redux](https://pub.dev/packages/redux) ， vue 使用 vuex .            

这边最基础的方式是Flutter 的 InheritedWidget 组件 ,(InheritedWidget 是存储数据的节点，一般提供个 of 方法，方便子节点查找) [InheritedWidget 2分钟视频](https://youtu.be/Zbm3hjPjQMk)

```dart
class FrogColor extends InheritedWidget {
  const FrogColor({
    super.key,
    required this.color,
    required super.child,
  });

  final Color color;

  static FrogColor of(BuildContext context) {
    final FrogColor? result = context.dependOnInheritedWidgetOfExactType<FrogColor>();
    assert(result != null, 'No FrogColor found in context');
    return result!;
  }

  @override
  bool updateShouldNotify(FrogColor old) => color != old.color;
}
```




官方推荐的状态管理包[provider](https://pub.dev/packages/provider)
> tips: 查看 prodiver_counter 用最基础的 provider 状态管理包的基础案例

[基于 provider 的优化版本 - 官方 riverpod 推荐 ](https://pub.dev/packages/riverpod)

> 其他的参考资料  
> [官方文档 state manage options](https://docs.flutter.dev/development/data-and-backend/state-mgmt/options)
