### 符号引用
在java代码中，一个类可能使用另外类或者接口的字段或者调用另外一个类的方法。
在编译的时候，class文件中是通过叫做"符号引用"的方式来实现的。
```
public interface Intf {
    public static String str = "abcde";
    public static int ival = new Random().nextInt();
}

public class T {
    public static int tint = Intf.ival;
}
```
class T编译成class 文件之后，利用javap -verbose 查看class文件，可以看到
在初始化static int tint的时候，从常量池的第12项取值
```
static {};
  Code:
   Stack=1, Locals=0, Args_size=0
   0:    getstatic    #12; //Field Intf.ival:I
   3:    putstatic    #17; //Field tint:I
   6:    return
  LineNumberTable: 
   line 6: 0
   line 3: 6

```
常量池的第12项是一个符号引用，指向Intf的ival字段。ival的值只能在运行的时候才能确定。
```
const #12 = Field    #13.#15;    //  Intf.ival:I
const #13 = class    #14;    //  Intf
```
在运行的时候会将符号引用解析为指向Intf内存地址的直接引用。

如果将class T改为如下，引用的是Intf的一个在编译时候就可以确定的常量值。
通过查看编译后的class文件，发现在T的class文件中，是将str = "abcde";的值
"abcde"直接复制了一份放到了常量池中，没有符号引用。
```
public class T {
    public static String tstr = Intf.str;
}
```
在初始化static int tint的时候，从常量池的第12项取值
```
static {};
  Code:
   Stack=1, Locals=0, Args_size=0
   0:    ldc    #12; //String abcde
   2:    putstatic    #14; //Field tstr:Ljava/lang/String;
   5:    return
  LineNumberTable: 
   line 5: 0
   line 3: 5
```
常量池的第12项直接为"abcde"字符串。
```
const #12 = String    #13;    //  abcde
const #13 = Asciz    abcde;
```

### 直接引用
直接引用是直接指向目标的指针、相对偏移量或是一个能间接定位到目标的句柄。直接引用是和虚拟机实现的内存布局相关的，同一个符号引用在不同虚拟机实例上翻译出来的直接引用一般不会相同，如果有了直接引用，那引用的目标必定在内存中存在。