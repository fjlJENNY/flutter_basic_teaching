
[官方下载地址](https://docs.flutter.dev/get-started/install)     
[中文版本下载地址](https://flutter.cn/docs/get-started/install)

### **1. 使用镜像**

Flutter官方为中国开发者搭建了临时镜像，大家可以将如下环境变量加入到用户环境变量中：

```
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```

**注意：** 此镜像为临时镜像，并不能保证一直可用，读者可以参考https://flutter.dev/community/china 以获得有关镜像服务器的最新动态。

### **2. Windows 安装**

建议将安装包zip解压到你想安装Flutter SDK的路径（如：`C:\src\flutter` )

更新环境变量

如果你想在Windows系统自带命令行运行flutter命令，需要添加以下环境变量到用户PATH：

- 转到 “控制面板>用户帐户>用户帐户>更改我的环境变量”
- 在“用户变量”下检查是否有名为“Path”的条目:
    - 如果该条目存在， 追加`flutter\bin`的全路径，使用 ; 作为分隔符.
    - 如果该条目不存在，创建一个新用户变量 Path ，然后将 `flutter\bin` 的全路径作为它的值.

重启Windows以应用此更改.

 

### **3. MacOS 安装**

添加`flutter`相关工具到 path中：

`export PATH=`pwd`/flutter/bin:$PATH`

### **4. Flutter 安装后检查**

`flutter doctor --verbose`
按照提示步骤完成

### **5. 编辑器选择**

![Untitled](doc/Untitled.png)

 编辑器装上 Flutter  和 dart  插件

### **6.编写第一个程序**

 IDE  找到  ”New Flutter Project”  ,  创建第一个程序

`flutter pub get`    下载依赖

`flutter run`   运行程序

 编辑器装上 Flutter  和 dart  插件

