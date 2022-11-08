## Container （类似于一个 box）介绍


###  Container的使用案例
```dart
 LayoutBuilder(
            builder: (BuildContext context, BoxConstraints constraints) {
            return Align(
                alignment: Alignment.center,
                child: Container(
                constraints: BoxConstraints(
                    maxHeight: constraints.maxHeight,
                    maxWidth: constraints.maxWidth,
                    minWidth: constraints.minWidth,
                    minHeight: constraints.minHeight,
                ),
                decoration: BoxDecoration(
                    color: Colors.red,
                    border: Border.all(width: 1.0),
                ),
                padding: EdgeInsets.zero,
                margin: const EdgeInsets.all(2.0),
                transform: Matrix4.skewY(0.3),
                clipBehavior: Clip.none,
                child: const Text('Apartment for rent!'),
                ),
            );
            },
        ),
```


### 嵌套式Container

```dart
LayoutBuilder(
              builder: (BuildContext context, BoxConstraints constraints) {
                print("constraints : $constraints");
                return Transform(
                  transform: Matrix4.skewY(0.3),
                  child: Padding(
                    padding: const EdgeInsets.all(2.0),
                    child: LimitedBox(
                      maxWidth: constraints.maxWidth,
                      maxHeight: constraints.maxHeight,
                      child: Align(
                        alignment: Alignment.center,
                        child: Padding(
                          padding: EdgeInsets.zero,
                          child: ColoredBox(
                            color: Colors.red,
                            child: ClipPath(
                              clipBehavior: Clip.none,
                              child: DecoratedBox(
                                decoration: BoxDecoration(
                                  border: Border.all(width: 1.0),
                                ),
                                child: Text('Apartment for rent!'),
                              ),
                            ),
                          ),
                        ),
                      ),
                    ),
                  ),
                );
              },
            ),
```


> [Flutter Container 介绍](https://book.flutterchina.club/chapter5/container.html#_5-4-3-padding%E5%92%8Cmargin)

> [Flutter Container (DecoratedBox) 介绍](https://book.flutterchina.club/chapter5/decoratedbox.html#_5-2-1-decoratedbox)

> [Flutter Container (Alignment) 介绍](https://book.flutterchina.club/chapter4/alignment.html)

> [Flutter Containe（Padding）介绍](https://book.flutterchina.club/chapter5/padding.html)


#### 优先级别低
> [Flutter Container (Trasform) 介绍 ](https://book.flutterchina.club/chapter5/transform.html)