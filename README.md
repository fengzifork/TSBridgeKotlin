# TSBridgeKotlin

目的：Android 学习过程中开发一个简单的小应用

语言：使用 Kotlin 语言编写（原先为 Java ）

功能实现：
1、两个页面，分别用于公告发布与显示；

2、发布页面包含发布者名称、发布文本内容输入文本框，发布图片内容选择、清除按钮，发布按钮；
内容分文字和图片两部分，只要有其一即可发布，清除按钮目前只是用来清空已选图片；
注：发布信息存入 Bmob 云数据平台

3、显示页面以列表的形式将公告内容进行展示，包括发布者头像、名称、内容（文字或图片），其中图片内容可以点击放大、还原；

4、点击公告图片内容会以弹出的对话框放大显示，对话框内容是自定义布局（用 Anko 直接在 Kotlin 代码中编写，不再借助 xml）；

5、添加了需要联网操作的网络连接判断，如果没有连接则给出页面让用户点击按钮去设置网络（包括移动和无线两个入口）；

6、添加了 SDK 6.0 及以上版本设备的危险权限申请机制，目前有 Manifest.permission.WRITE_EXTERNAL_STORAGE；
当用户拒绝并选择了不再显示时，下次操作需要该权限时会显示页面让用户点击按钮去设置权限；
注：同上面的网络设置，从设置页面回到某页面时会自行判断所需条件是否满足，如果满足则进行下一步，否则给出提示

7、添加了公告信息列表的下拉刷新功能，如果有最新的数据则加载
注：最新的数据显示在列表上方，即开头部分

8、当activity的上下文context销毁以后，若 Glide 的 with 和其发生关联正在异步加载图片，那么就会出现异常，
解决方法是开始新建加载任务时就通过 context 去获取全局的上下文（ onetxt.getApplicationContext() ），
在 Kotlin 中是 context.applicationContext；

9、将原先利用异步类 + Glide 实现加载图片改为了 Glide，因为其本身就是异步的，而图片加载完成后会自动切换到主线程去显示图片；

10、添加了用户信息，包括注册、登录、注销，
只有登录用户才能才送消息，而接收则没有此要求；