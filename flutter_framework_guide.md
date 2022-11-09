![frame_image](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/499653d5c6df4ab7bcc3d802379d3c8f~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)


Flutter 框架分为2条主线

# **1. Build (build)**

### **BuildOwner**   贯穿了整个 Build
    
    Widget 构建 -> Element 树 ->  RenderObject 树 

    Element 树主要是管理多颗树的层级关系，主要包括树的遍历，查找，插入，删除等等

    RenderObject 树 主要提供 ”canvas" 绘制的信息。比如 Constraints, Size, Offset 等


# **2. Render(layout , render)**  
 
### **PiplineOwner**  贯穿整个 Render, RenderObject 挂载的owner 就是此处owner    

      

![render pipline](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/3/5/16949bfa3d932c82~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)


![render piple](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/3/5/1694a19f7dd0da57~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)


> ## [**👆🏻参考**](https://juejin.cn/post/6844903791427321863)