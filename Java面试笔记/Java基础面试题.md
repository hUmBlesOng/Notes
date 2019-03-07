## Java面试题

### 1、面向对象的特征有哪些?
面向对象的特征主要有以下几个方面：
- **抽象**：抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么。
- **继承**：继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的重要手段
- **封装**：通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口（可以想想普通洗衣机和全自动洗衣机的差别，明显全自动洗衣机封装更好因此操作起来更简单；我们现在使用的智能手机也是封装得足够好的，因为几个按键就搞定了所有的事情）。
- **多态性**：多态性是指允许不同子类型的对象对同一消息作出不同的响应。简单的说就是用同样的对象引用调用同样的方法但是做了不同的事情。多态性分为编译时的多态性和运行时的多态性。如果将对象的方法视为对象向外界提供的服务，那么运行时的多态性可以解释为：当A系统访问B系统提供的服务时，B系统有多种提供服务的方式，但一切对A系统来说都是透明的（就像电动剃须刀是A系统，它的供电系统是B系统，B系统可以使用电池供电或者用交流电，甚至还有可能是太阳能，A系统只会通过B类对象调用供电的方法，但并不知道供电系统的底层实现是什么，究竟通过何种方式获得了动力）。方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1). 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2). 对象造型（用父类型引用引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。

### 2、访问修饰符public,private,protected,以及不写（默认）时的区别?
| 修饰符    | 当前类 | 同包 | 子类 | 其他类 |
| --------- | ------ | ---- | ---- | ------ |
| public    | √     | √   | √   | √     |
| protected | √     | √   | √   | ×      |
| default   | √     | √   | ×    | ×      |
| private   | √     | ×    | ×    | ×      |

### 3、String 是最基本的数据类型吗?
不是。Java中的基本数据类型只有8个：byte、short、int、long、float、double、char、boolean；除了基本类型（primitive type），剩下的都是引用类型（reference type），Java 5以后引入的枚举类型也算是一种比较特殊的引用类型

### 4、float f=3.4;是否正确?
不正确。3.4是双精度数，将双精度型（double）赋值给浮点型（float）属于**向下转型**（down-casting，也称为窄化）会造成精度损失，因此需要强制类型转换`float f =(float)3.4;` 或者写成`float f =3.4F;`
+ 既然有**向下转型**, 那么也有**向上转型**, 向上转型如下: 
  - 把子类对象直接赋给父类引用叫upcasting向上转型，向上转型不用强制转型。如`Father father = new Son();`
  - upcasting 会丢失子类特有的方法,但是子类overriding 父类的方法，子类方法有效，向上转型只能引用父类对象的属性，要引用子类对象属性，则要写getter函数。
  - 向上转型的作用，减少重复代码，父类为参数，调有时用子类作为参数，就是利用了向上转型。这样使代码变得简洁。体现了JAVA的抽象编程思想。

### 5、short s1 = 1; s1 = s1 + 1;有错吗?short s1 = 1; s1 += 1;有错吗?
对于short s1 = 1; s1 = s1 + 1;由于1是int类型，因此s1+1运算结果也是int 型，需要强制转换类型才能赋值给short型。而short s1 = 1; s1 += 1;可以正确编译，因为s1+= 1;相当于s1 = (short)(s1 + 1);其中有隐含的强制类型转换

### 6、Java有没有goto?
goto 是Java中的保留字，在目前版本的Java中没有使用。（根据James Gosling（Java之父）编写的《The Java Programming Language》一书的附录中给出了一个Java关键字列表，其中有goto和const，但是这两个是目前无法使用的关键字，因此有些地方将其称之为保留字，其实保留字这个词应该有更广泛的意义，因为熟悉C语言的程序员都知道，在系统类库中使用过的有特殊意义的单词或单词的组合都被视为保留字）

### 7、int和Integer有什么区别?
Java是一个近乎纯洁的面向对象编程语言，但是为了编程的方便还是引入了基本数据类型，但是为了能够将这些基本数据类型当成对象操作，Java为每一个基本数据类型都引入了对应的包装类型（wrapper class），int的包装类就是Integer，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以相互转换。
Java 为每个原始类型提供了包装类型： 
- 原始类型: boolean，char，byte，short，int，long，float，double 
- 包装类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double

``` java
class AutoUnboxingTest {

    public static void main(String[] args) {
        Integer a = new Integer(3);
        Integer b = 3;                  // 将3自动装箱成Integer类型
        int c = 3;
        System.out.println(a == b);     // false 两个引用没有引用同一对象
        System.out.println(a == c);     // true a自动拆箱成int类型再和c比较
    }
}
```
最近还遇到一个面试题，也是和自动装箱和拆箱有点关系的，代码如下所示：

``` java
public class Test03 {
    public static void main(String[] args) {
        Integer f1 = 100, f2 = 100, f3 = 150, f4 = 150;

        System.out.println(f1 == f2);
        System.out.println(f3 == f4);
    }
}
```
如果不明就里很容易认为两个输出要么都是true要么都是false。首先需要注意的是f1、f2、f3、f4四个变量都是Integer对象引用，所以下面的==运算比较的不是值而是引用。装箱的本质是什么呢？当我们给一个Integer对象赋一个int值的时候，会调用Integer类的静态方法valueOf，如果看看valueOf的源代码就知道发生了什么。

``` java
public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
```
IntegerCache是Integer的内部类，其代码如下所示：

``` java
/**
     * Cache to support the object identity semantics of autoboxing for values between
     * -128 and 127 (inclusive) as required by JLS.
     *
     * The cache is initialized on first usage.  The size of the cache
     * may be controlled by the {@code -XX:AutoBoxCacheMax=<size>} option.
     * During VM initialization, java.lang.Integer.IntegerCache.high property
     * may be set and saved in the private system properties in the
     * sun.misc.VM class.
     */

    private static class IntegerCache {
        static final int low = -128;
        static final int high;
        static final Integer cache[];

        static {
            // high value may be configured by property
            int h = 127;
            String integerCacheHighPropValue =
                sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
            if (integerCacheHighPropValue != null) {
                try {
                    int i = parseInt(integerCacheHighPropValue);
                    i = Math.max(i, 127);
                    // Maximum array size is Integer.MAX_VALUE
                    h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
                } catch( NumberFormatException nfe) {
                    // If the property cannot be parsed into an int, ignore it.
                }
            }
            high = h;

            cache = new Integer[(high - low) + 1];
            int j = low;
            for(int k = 0; k < cache.length; k++)
                cache[k] = new Integer(j++);

            // range [-128, 127] must be interned (JLS7 5.1.7)
            assert IntegerCache.high >= 127;
        }

        private IntegerCache() {}
    }
```
简单的说，如果整型字面量的值在-128到127之间，那么不会new新的Integer对象，而是直接引用常量池中的Integer对象，所以上面的面试题中`f1==f2`的结果是true，而f3==f4的结果是false。

### 8、&和&&的区别?
&运算符有两种用法：(1)按位与；(2)逻辑与。&&运算符是短路与运算。逻辑与跟短路与的差别是非常巨大的，虽然二者都要求运算符左右两端的布尔值都是true整个表达式的值才是true。&&之所以称为短路运算是因为，如果&&左边的表达式的值是false，右边的表达式会被直接短路掉，不会进行运算。很多时候我们可能都需要用&&而不是&，例如在验证用户登录时判定用户名不是null而且不是空字符串，应当写为：`username != null &&!username.equals("")`，二者的顺序不能交换，更不能用&运算符，因为第一个条件如果不成立，根本不能进行字符串的equals比较，否则会产生NullPointerException异常。注意：逻辑或运算符（|）和短路或运算符（||）的差别也是如此。

### 9、解释内存中的栈(stack)、堆(heap)和方法区(method area)的用法?
1. **栈（stack）**：Java栈的区域很小，只有1M，特点是存取速度很快，所以在stack中存放的都是快速执行的任务，基本数据类型的数据，和对象的引用（reference）。JVM只会直接对JavaStack（Java栈）执行两种操作：①以帧为单位的压栈或出栈；②通过-Xss来设置， 若不够会抛出StackOverflowError异常。
   - 每个线程包含一个栈区，栈中只保存基本数据类型的数据和自定义对象的引用(不是对象)，对象都存放在堆区中
   - 每个栈中的数据(原始类型和对象引用)都是私有的，其他栈不能访问。
   - 栈分为3个部分：基本数据类型的变量区、执行环境上下文、操作指令区(存放操作指令)。
2. **堆（heap）**：类的对象放在heap（堆）中，所有的类对象都是通过new方法创建，创建后，在stack（栈）会创建类对象的引用（内存地址）。堆是垃圾收集器管理的主要区域，由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，再具体一点可以分为Eden、Survivor（又可分为From Survivor和To Survivor）、Tenured。
3. **方法区（method）**：method（方法区）又叫静态区，存放所有的①类（class），②静态变量（static变量），③静态方法，④常量和⑤成员方法。
   - 1.又叫静态区，跟堆一样，被所有的线程共享。
   - 方法区中存放的都是在整个程序中永远唯一的元素。这也是方法区被所有的线程共享的原因。
>补充：静态变量和常量的区别： 静态变量本质是变量，是整个类所有对象共享的一个变量，其值一旦改变对这个类的所有对象都有影响；常量一旦赋值后不能修改其引用，其中基本数据类型的常量不能修改其值。

### 10、Math.round(11.5) 等于多少？Math.round(-11.5)等于多少？ 
Math.round(11.5)的返回值是12，Math.round(-11.5)的返回值是-11。四舍五入的原理是在参数上加0.5然后进行下取整。

### 11、switch 是否能作用在byte 上，是否能作用在long 上，是否能作用在String上？ 
switch只支持int，String，enum类型，由于java的自动转型，所以byte，char，short这三种也支持，由于java中包装类的自动拆箱，Integer，Byte，Char，Short也支持。
>注意：在java1.6中表达式类型只能为int和enum，1.7之后加入了对String的支持。

### 12、用最有效率的方法计算2乘以8？
`2 << 3`（左移3位相当于乘以2的3次方，右移3位相当于除以2的3次方）。

### 13、数组有没有length()方法？String有没有length()方法？
数组没有length()方法，有length的属性。String 有length()方法。JavaScript中，获得字符串的长度是通过length属性得到的，这一点容易和Java混淆。

### 14、在Java中，如何跳出当前的多重嵌套循环？
在最外层循环前加一个标记如A，然后用break A;可以跳出多重循环。
>补充：Java中支持带标签的break和continue语句，作用有点类似于C和C++中的goto语句，但是就像要避免使用goto一样，应该避免使用带标签的break和continue，循环语句（for，while）里面出现return是没问题的，然而如果你使用了continue或者break，就会让循环的逻辑和终止条件变得复杂，难以确保正确。

### 15、构造器（constructor）是否可被重写（override）？
构造器不能被继承，因此不能被重写，但可以被重载。

### 16、两个对象值相同(x.equals(y) == true)，但却可有不同的hash code，这句话对不对？
不对，如果两个对象x和y满足x.equals(y) == true，它们的哈希码（hash code）应当相同。Java对于eqauls方法和hashCode方法是这样规定的：(1)如果两个对象相同（equals方法返回true），那么它们的hashCode值一定要相同；(2)如果两个对象的hashCode相同，它们并不一定相同。
>关于equals方法，它必须满足**自反性**（x.equals(x)必须返回true）、**对称性**（x.equals(y)返回true时，y.equals(x)也必须返回true）、**传递性**（x.equals(y)和y.equals(z)都返回true时，x.equals(z)也必须返回true）和**一致性**（当x和y引用的对象信息没有被修改时，多次调用x.equals(y)应该得到同样的返回值），而且对于任何非null值的引用x，x.equals(null)必须返回false。实现高质量的equals方法的诀窍包括：1. 使用==操作符检查"参数是否为这个对象的引用"；2. 使用instanceof操作符检查"参数是否为正确的类型"；3. 对于类中的关键属性，检查参数传入对象的属性是否与之相匹配；4. 编写完equals方法后，问自己它是否满足对称性、传递性、一致性；5. 重写equals时总是要重写hashCode；6. 不要将equals方法参数中的Object对象替换为其他的类型，在重写时不要忘掉@Override注解。

### 17、是否可以继承String类？
String 类是final类，不可以被继承。

### 18、当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递？
是值传递。Java语言的方法调用只支持参数的值传递。当一个对象实例作为一个参数被传递到方法中时，参数的值就是对该对象的引用。对象的属性可以在被调用过程中被改变，但对对象引用的改变是不会影响到调用者的。

### 19、String和StringBuilder、StringBuffer的区别？
- String是只读字符串，也就意味着String引用的字符串内容是不能被改变的。
- StringBuilder类的对象可以直接进行修改。StringBuilder没有被synchronized修饰，因此它的效率比StringBuffer要高。
- StringBuffer和StringBuilder的方法完全相同。StringBuffer的所有方法都被synchronized修饰，所以它是线程安全的。

### 20、重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？
方法的重载和重写都是实现多态的方式，区别在于前者实现的是编译时的多态性，而后者实现的是运行时的多态性。
1. 重载发生在一个类中，同名的方法如果有不同的参数列表（参数类型不同、参数个数不同或者二者都不同）则视为重载；重写发生在子类与父类之间。
2. 重写要求子类被重写方法与父类被重写方法有相同的返回类型，比父类被重写方法更好访问，不能比父类被重写方法声明更多的异常（里氏代换原则）。重载对返回类型没有特殊的要求。

### 21、描述一下JVM加载class文件的原理机制？