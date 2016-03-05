# Objc2Lua

##限制：

- 它不保证生成完全可执行的lua文件，仍需要程序要人工后期处理（例如需要自行添加WaxClass的头描述，对宏的处理，和一些转换错误的语法进行人工修正转换等等）

- 它不完全支持C/C + +的语法（可能会出现相关语法无法识别或者转换错误，到时候请手动转换，而且LUA并不支持直接调用C方法，仍需要在OC封装一层）

- 它不合并Categories（请手动将Catergory合并到同一个lua中）

- 它不支持协议的转换（程序不会对协议进行转换输出）

- 它对宏不进行太多处理，所以宏仍需要程序员自行处理，但会提取出可以的宏作为注释放到LUA开头

- 它不完全支持Block（Block转换后会提示不支持）

- 不完全的For循环转换（主要在循环体部分，需要人工改写，例如使用i=1,100,1或paris循环等）

- 可能会出End不匹配的现象（可能出现在Switch，For，If等语句的转换上，如果｛｝都写的话的话应该会匹配，主要出现在没有只有一行时省略｛｝的情况）

##支持：

- 自动将消息调用转成WAX的形式

- 自动将方法声明转换成WAX的形式

- 自动将对属性的操作转换成对应的get/set方法调用格式

- 自动将switch转换成if-elseif嵌套的方式，但不完美需要可能需要人工校对

- 自动将do-while转换成repeat-until形式

- 自动将if，For等语句进行转换，但由于Lua与OC的语法不同，所以仍然需要人工校正

- 支持@[],@{}的语法糖，并自动转换为LUA中的Table表述形式

- 自动判断可能的宏定义和宏函数，添加到文件中(在文件最后以注释的形式添加)，便于手工查找并修改

- 自动将CGSizeMake->CGSize（还有一些其他wax支持的结构体如CGRect等）

- 还有其他一些细节就不一一列举了

##其他说明：

- 对OC中_XXX的变量不做转换（可以自行替换为self.xxx的形式或其他变量声明形式，但依旧不提倡使用self.xxx，该方法存取变量的性能开销较大，能使用local请尽量使用local）

- 宏的识别暂时为以下三种

    1.k+大写字母+任意字符

    2.AAA_BBB_CCC类似的形式

    3._+纯大写

##需要预处理：

1.Block（如果能替换成非Block方法或注释掉最好，不替换也行，但会提示不支持）

2.多线程，现WAX还不支持多线程，所以如果有用到GCD或其他多线程的地方也需要进行处理

3.纯C\C++方法

特别注意：如果语句最后不是分号,一定要加上分号，否则会影响识别的！！！

##转换完之后仍然需要人工校对，以下方面需要特别关注：

1.For

2.Switch

3.IF

4.所有使用到宏的地方

5.转换时提示报错的地方

6.依然建议逐行校对，防止转换失误

7.建议将一些结构使用LUA中的table之类的代替，以减少使用WAX带来的性能损失，并能用local变量的请尽量用local变量

##使用方法：

1.安装JRE或者JDK

2.双击运行jar包

3.选择要转换的目录，程序会自动转换该目录下的所有.m文件

4.生成的文件在同目录下扩展名为.lua

5.相关报错会在开始按钮下方的控制台输出

##特别感谢以下开源程序：

https://github.com/yahoojapan/objc2swift

https://github.com/bang590/JSPatchConvertor

https://github.com/irclark2000/ObjcToJava

##jar文件
Java/classes/artifacts/Objc2Lua_jar目录下
