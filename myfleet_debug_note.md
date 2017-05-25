# 笔记 #

- GridView各item不居中---------gridView的item的布局文件，必须加gravity:center。否则还是不居中。
- 自写多个字符串拼接的sql语句时，记得加括号和逗号，否则报syntax error错误。sql语法错误
- unable to start componentinfo nullpointer exception:无法运行oncreate方法，不一定是activity的错误，可能是其他语句。eclipse报错不准
- table xxx already exists----------sql语句改为：create table if not exists xxx(...)
- resoucesnotfoundException-------可能是eclipse抽风了，可以project-clear 或者重启。这次我是循环写错了，低级错误 .康伟解决了。是Toast.makeText方法，第二个参数如果是int，会自动把参数当成int resId去找资源文件，自然就错了。所以把参数后加""就解决了。
- 布局里用addView添加子view不显示-----1，先保证layoutparams是具体的五大布局类型。2，setContentView里不能写布局文件xml，而是写添加子view的那个布局类对象，因为布局文件xml本身没变，自然也就不显示了。
- edittext输入软键盘的回车后保存信息：用setonkeylistener。并取消焦点。但是如何不让edittext不用final变量？------用final类型没什么问题，又不是static静态变量，不会造成内存负担。
- 想在离开本act后保存UI-------重写onPause，在里面把数据保存到数据库即可
- 想让Activity在第一次显示时加载一种UI的数据，在以后进入这个页面后加载另一种UI数据，怎么做？:用sp保存是否是第一次进入
- 为什么onCreate的setContent无效了？是因为重写了onResume了？-----------是
- 为什么saveText写在viewchild遍历循环外就成功了？按道理应该和显示布局没关系吧？-------因为saveText的入参是一个viewgroup，saveText方法内部对该viewgroup进行了迭代，但是外部你在循环设置viewgroup内部的textview时：迭代到第一个textview时，你就调用了saveText，并且把只设置了第一个textview的viewgroup传了进去（这是viewgroup中只是第一个textview被设了新值），然后saveText方法内部又对传入的viewgroup进行了迭代；接着迭代到第二个textview时，又进行了类似的一遍（只不过这次viewgroup中有前两个textview设置了新值）说白了就是你迭代了遍viewgroup（相当于嵌套for循环）
- 为什么我的Eclipse里写上Log.i语句或者SYstem.out.print()，不打印Log？
- 为什么对象比较要用TextUtils.equals方法？-------因为对象用“==”，默认比较地址值，肯定不正确。用安卓默认sdk即可，不需要导入第三方包 
- 为什么使用activity后，退出再重新进去，textview还有文本？----因为安卓内部把这个textview控件弄成全局变量了，退出时自动保存
- 在子类里写这些生命周期方法太麻烦，能不能写在基类里？可是还要保存到不同的table中，怎么搞？-----可以抽象的。把基类设置成抽象的基类，添加String item _name字段和setItemName方法，逼子类传递特有的table名字。在Base基类里在onCreate方法里获取这个item_name。然后在onResume里去使用它即可。
- 在公司写不优雅的代码，会不会被项目经理砍死？-------
- 你看，你的onCreate方法里，第一次加载页面，setContentView用的是布局文件。可是我想把textview的文本放在本地里，不是xml里
- 你觉得放在自定义的常量类里好，还是R.strings里好——放在R.strings里好。如果是自定义常量类里还需要许多遍历方法，很麻烦--------直接放R.strings里就好
- getIdentifier()参数报错：-------int stringId = mContext.getResources().getIdentifier("hello","string", mContext.getPackageName());  第二个参数写类别，第三个参数是包名，不能用null代替。
- android.database.sqlite.SQLiteException: near index: syntax error (code 1):------index是sql关键词，改成order_index通过
- getResources().getIdentifier(key, "string", getPackageName())找不到资源--------循环里，布局的textview写多了，造成getIdentifier(key, "string", getPackageName())时，key，第四个和第五个string资源找不到，报错。
- public LinearLayout addTextView(Context nowContext,int layoutId,int count)不显示正确的三个textview------考虑是onResume方法把onCreate方法的setContentView弄失效了，复制SecretaryAct的生命周期方法，结果R.string数量不匹配，更改后finished！

2017/5/25 16:45:15 















