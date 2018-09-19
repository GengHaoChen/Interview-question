## JAVA基础
#### 1. JAVA 中的几种基本数据类型是什么,各自占用多少字节
| 数据类型 | 占用字节 | 占用内存位数 |
| :----: | :----: | :----: |
| short   | 2字节 | 16位 |
| int     | 4字节 | 32位 |
| long    | 8字节 | 64位 |
| byte    | 1字节 | 8位  |
| char    | 2字节 | 16位 |
| boolean | 1字节 | 8位  |
| float   | 4字节 | 32位 |
| double  | 8字节 | 64位 |

#### 2. String 类能被继承吗,为什么
1. 不能
2. String类声明 public final class
3. final修饰类表示不可被继承


#### 3. String,StringBuffer,StringBuilder的区别
* String 数据类型 使用char数组实现 拼接操作等会返回新的对象
* StringBuffer,StringBuilder 类String数据类型 使用char数组实现 拼接操作等不会返回新的对象
* StringBuffer中函数加有synchronized关键字 多线程安全
* StringBuilder中函数没有synchronized关键字 多线程不安全
* synchronized关键字表示程序中最多只有一个synchronized关键字程序运行,其他带有synchronized关键字程序需要等到前一个synchronized关键字程序运行完成才能运行

#### 4. ArrayList 和 LinkedList 有什么区别
1. ArrayList 
    * 线性结构
        * 顺序存储
2. LinkedList 
    * 线性结构
        * 链式存储

#### 5. 讲讲类的实例化顺序,比如父类静态数据,构造函数,字段,子类静态数据,构造函数,字段,当 new 的时候,他们的执行顺序.
1. 父类静态块
2. 父类静态属性
3. 子类静态块
4. 子类静态属性
5. 父类属性
5. 父类构造函数
6. 子类属性
7. 子类构造函数


#### 6. 用过哪些 Map 类,都有什么区别,HashMap是线程安全的吗,并发下使用的 Map 是什么,他们内部原理分别是什么,比如存储方式,hashcode,扩容,默认容量等.
* TreeMap
	* 红黑树
* HashMap
	* 散列表
		* 通过hash方法计算关键值保存到一个数组中
		* 相同hash冲突采用拉链法解决冲突
		* 当哈希表中的条目数超出了加载因子与当前容量的乘积时进行扩容操作
	    * 默认容量 16
		* 默认加载因子 0.75
* HashTable
	* 散列表
	* 除了同步运行和key&value不能为空之外与hashMap一致
* ConcurrentHashMap
	* 类似于hashTable,通过CAS(Compare and swap)控制线程安全
* LinkedHashMap 
	* HashMap子类
		* 保存前一个节点和后一个节点
		* 通过重写父类插入移除Entry(Entry&Node)后修改本地节点链表

#### 7.JAVA8 的 ConcurrentHashMap 为什么放弃了分段锁,有什么问题吗,如果你来设计,你如何设计
* 分段锁:一部分数据使用一把锁
* 1.8之后使用CAS(Compare and swap),基于CPU指令实现多线程锁


#### 8.有没有有顺序的 Map 实现类,如果有,他们是怎么保证有序的.
* LinkedHashMap
	* 继承于HashMap,通过重写HashMap的afterNodeAccess方法和afterNodeInsertion从而实现将数据加入链表

#### 9.象类和接口的区别,类可以继承多个类么,接口可以继承多个接口么,类可以实现多个接口么.
* 类:


        不可以继承多个类
        可以实现多个接口
        关键字 class
        属性和方法可以是所有访问修饰符


* 接口:


	    不可以继承多个接口
	    关键字 interface
	    方法修饰符只能是public
	    属性修饰符为只能为 public static final
	    不可以实现方法

#### 10.继承和聚合的区别在哪
* 继承:
    * 使用或实现重写父类或者超类提供的方法实现业务
* 聚合:
	* 组合多个类的方法实现业务

#### 11.讲讲你理解的 NIO
* java IO 模型之一
    * 面向缓冲区,同步非阻塞IO模型
    * Selector监听通道事件
    * 核心组件:通道,缓冲区,选择器
    * 数据从通道进入缓冲区
    
    
          NIO API 的集中抽象为缓冲区,它们是数据容器字符集及其相关解码器和编码器,它们在字节和 Unicode 字符之间进行转换
          各种类型的通道,它们表示到能够执行 IO 操作的实体的连接;
	      以及选择器和选择键它们与可选择信道 一起定义了多路的 无阻塞的 I/O 设施

		

#### 12.反射的原理,反射创建类实例的三种方式是什么.
* 反射原理
    * 每当编写并且编译了一个新类就会产生一个Class对象(被保存在一个同名.class文件中)
    * 在运行时打开和检查.class文件
    * 通过Class对象找到某一个类中的方法以及属性等

* 反射创建类实例


        Class.forName().newInstance();
        ClassLoader.loadClass().newInstance();
        类名.class.newInstance();
        Object.clone();
    
 #### 13.反射中,Class.forName 和 ClassLoader 区别
* 当使用.class来创建对Class对象的引用时,不会自动初始化该Class对象.为了使用类而做的准备工作包括三个步骤
    * Class.forName得到的class是已经初始化完成的
    * Classloader.loaderClass得到的class是还没有链接的
 
 
 
          1.加载:由类加载器执行,查找字节码并从这些字节码中创建一个class对象
    	  2.链接:验证类中的字节码,为静态域分配空间,解析这个类创建的对其他类的所有引用
    	  3.初始化:如果该类具有超类,则对其初始化,执行静态初始化器和静态初始化块.
	      初始化被元迟到了对静态方法(构造器隐式地是静态的)或者非常数静态域进行首次引用时才执行

#### 14.描述动态代理的几种实现方式,分别说出相应的优缺点

    以二进制形式修改已有类或者动态生成类,在类被加载入 Java 虚拟机之前动态改变类行为

* JDK
    * java原生动态代理
    * 运行速度慢
* Javassist
    * 没有类型检查
    * 没有泛型支持
    * 没有自动封包差包
    * 运行速度较快
* CGLIB
    * 会导致PermGen内存泄露
    * 运行速度块
    
#### 15.动态代理与CGLIB实现的区别
* JDK
  * 定义一个功能接口,然后让代理和来实现这个接口  
* CGLIB
  * 通过继承.代理继承自被代理类中的方法,这样代理则拥有了被代理类中的的功能,代理还可以通过重写被代理类中的方法,来实现多态.
  
#### 16.为什么CGlib方式可以对接口实现代理.

    通过继承.代理继承自被代理类中的方法,这样代理则拥有了被代理类中的的功能,代理还可以通过重写被代理类中的方法,来实现多态.

#### 17.final 的用途
* 修饰属性表示常量
* 修饰类表示不可被继承
* 修饰方法表示不可被重载

#### 18.写出三种单例模式实现
* 懒汉模式
    
    
    	public class Singleton {  
        	private static Singleton instance = null;  
        	private Singleton(){}  
        	public static Singleton getInstance() {  
            	if (instance == null) {  
                	synchronized (Singleton.class) {  
                    		if (instance == null) {
                        		instance = new Singleton();  
                    		}  
                	}  
            	}  
        	return instance;  
        	}  
    	}
        
* 饿汉模式


    	public class Singleton{  
        	private static Singleton instance = new Singleton();  
        	private Singleton(){}  
        	public static Singleton newInstance(){  
            		return instance;  
        	}  
    	}
    
* 枚举模式


    	public enum Singleton{  
        	instance;  
        	public void doSomething(){}      
    	}  

#### 19.如何在父类中为子类自动完成所有的 hashcode 和 equals 实现?这么做有何优劣
* 子类不实现hashcode和equals默认调用父类方法
* 父类设置公共参数,为公共参数实现hashcode和equals
    * 优点
        * 子类无需实现hashcode和equals
    * 缺点
        * 无法根据子类特定属性实现hashcode和equals
        

#### 20.请结合 OO 设计理念,谈谈访问修饰符 public private protected default 在应用设计中的作用
* public
    * 所有类可用
    * 有被所有对象知情的重要性
* private
    * 只有自身类可用
    * 只有自身对象依赖对其他对象没有使用用处或者其他对象不需要知情
* protected
    * 子类可用
    * 不想被其他类直接引用但是可被子类复写或者被子类使用,对其它对象用处不大
* default
    * 子类和同一个包下的类可用
    * 相同包下对象和子类需要使用或者需要感知到
    
#### 21.深拷贝和浅拷贝区别


        同为拷贝内容,但浅拷贝被拷贝对象的内容与拷贝对象内容同为一个引用,深拷贝拷贝对象会创建新的引用存放被拷贝对象内容
        
#### 22.数组和链表数据结构描述,各自的时间复杂度
* 数组
    * 线性结构
    * 顺序存储实现
    * 逻辑存储顺序与物理存储顺序一致
    * 长度固定
* 链表
    * 线性结构
    * 链式存储实现
    * 逻辑存储顺序与物理存储顺序不一致,需要记录元素前驱后继记录元素逻辑位置
    * 长度可变

#### 23.error和exception的区别,CheckedException,RuntimeException的区别
* error
    * 程序无法处理的错误,发生于虚拟机自身或虚拟机试图执行应用,可能会导致中断线程
* exception
    * 操作或操作可能会引发的错误,可以被程序处理
    * CheckedException
        * 检查型异常,强制要求必须做异常处理
    * RuntimeException
        * 运行时异常,因操作引发的异常,不要求强制做异常处理

#### 24.请列出5个运行时异常
* NullPointException 
    * 空指针异常
    * 调用对象为null的时候发生
* IndexOutOfBoundsException
    * 数组下标越界一场
    * 获取对象下标超出数组长度时
* ClassCastException
    * 类转换异常
    * 类型转换时类型不属于父子类或同一个类型时
* IllegalArgumentException
    * 非法参数异常
    * 函数需要参数与传递参数不符时 
* UnsupportedOperationException
    * 不支持操作异常
    * 调用函数不存在时

#### 25.在自己的代码中,如果创建一个java.lang.String对象,这个对象是否可以被类加载器加载?为什么
* 不可以
* jdk类加载器 启动类加载器(bootstrap)负责加载系统的核心类,比如rt.jar中的java类;所以自己创建的java.lang.String对象无法被加载

#### 26.说一说你对java.lang.Object对象中hashCode和equals方法的理解.在什么场景下需要重新实现这两个方法.
* equals
    * 进行非引用判断对象是否一致
    * 当使用属性或特殊方法判断对象是否一致时重新实现
* hashcode
    * 计算hashcode
    * 当需要在使用hash存储时为了让元素更分散或更密集时重新实现

#### 27.在jdk1.5中,引入了泛型,泛型的存在是用来解决什么问题
> 泛型实现了参数化类型的概念,使代码可以应用于多种类型.

> 最初的目的是希望类或方法能够具备最广泛的表达能力.

#### 28.这样的a.hashcode()有什么用,与a.equals(b)有什么关系
* a.hashcode()
    * 获取当前hashcode值
* a.equals(b)
    * 如果equals返回true按hashcode常规协定两个对象将会返回同一个hashcode值

* hashcode常规协定
    > 在 Java 应用程序执行期间,在对同一对象多次调用 hashCode 方法时,必须一致地返回相同的整数,前提是将对象进行 equals 比较时所用的信息没有被修改.从某一应用程序的一次执行到同一应用程序的另一次执行,该整数无需保持一致.

    > 如果根据 equals(Object) 方法,两个对象是相等的,那么对这两个对象中的每个对象调用 hashCode 方法都必须生成相同的整数结果.

    > 如果根据 equals(java.lang.Object) 方法,两个对象不相等,那么对这两个对象中的任一对象上调用 hashCode 方法不 要求一定生成不同的整数结果.但是,程序员应该意识到,为不相等的对象生成不同整数结果可以提高哈希表的性能.

#### 29.有没有可能 2 个不相等的对象有相同的 hashcode.
* 通过重写hashcode可以实现两个不想等对象拥有相同的hashcode
* string对象中字符串内容相反两个对象拥有想等的hashcode

#### 30.Java 中的 HashSet 内部是如何工作的


    hashset内部由hashmap具体实现
    通过向hashmap put(key,null) 实现hashset

#### 31.什么是序列化,怎么序列化,为什么序列化,反序列化会遇到什么问题,如何解决.
        

        一种用来处理对象流的机制.所谓对象流也就是将对象的内容进行流化
        对流化后的对象进行读写操作,也可将流化后的对象传输于网络之间在对对象流进行读写操作时会引发一些问题,而序列化机制正是用来解决这些问题的


## JVM 知识
#### 1.什么情况下会发生栈内存溢出
* 栈(JVM Stack)存放主要是栈帧(局部变量表,操作数栈,动态链接,方法出口信息)的地方
* 栈包含栈帧
* 栈溢出抛出java.lang.StackOverflowError错误出现此种情况是因为方法运行的时候请求新建栈帧时栈所剩空间小于战帧所需空间
    * 通过递归调用方法,不停的产生栈帧,一直把栈空间堆满,直到抛出异常

#### 2.JVM 的内存结构,Eden 和 Survivor 比例
* 内存结构
    * 堆内存
        * 年轻代
            * Eden
            * Survivor
                * to Survivor
                * from Survivor
        * 老年代
    * 方法区(永久代)
    * 元空间 1.8中出现 替代方法区
    * 栈  
* Eden 和 Survivor 默认分配比例为 8:2

* 堆内存
    * 存放对象实例 JVM全局共享
* 方法区(永久代)
    * 存放运行时常量池,字段和方法数据,构造函数和普通方法的字节码内容以及类,实例,接口初始化时需要使用到的特殊方法等数据 JVM全局共享
* 元空间(使用物理内存)
    * JDK 1.8中出现 
    * 大部分类元数据都在本地内存中分配
* 栈
    * 存放局部变量表,操作数栈,方法出口 JVM线程独占
* 在JDK1.8中
    * 字符串常量由永久代转移到堆中
    * 方法区(永久代)已不存在

#### 3.jvm 中一次完整的 GC 流程是怎样的,对象如何晋升到老年代,说说你知道的几种主要的jvm参数
1. 绝大多数刚创建的对象会被分配在Eden区
2. 当Eden区满的时候,执行Minor GC,将消亡的对象清理掉,并将剩余的对象复制到一个存活区Survivor()
3. 当一个Survivor也满的时候,将其中仍然活着的对象直接复制到另一个Survivor,以后Eden区执行Minor GC后,就将剩余的对象添加到另一个Survivor
4. 两个存活区切换了几次(HotSpot虚拟机默认15次)之后,仍然存活的对象将被复制到老年代
5. 当年老代内存不足时,将执行Major GC,也叫 Full GC

#### 4.你知道哪几种垃圾收集器,各自的优缺点,重点讲下 cms,包括原理,流程,优缺点
* 串行垃圾回收器
    * 新生代串行垃圾回收器
        * 利用复制算法进行垃圾回收
    * 老年代串行垃圾回收期
        * 利用标记压缩算法进行垃圾回收
* 并行垃圾回收器
    * 新生代ParNew垃圾回收器
        * 利用多线程复制算法进行垃圾回收
    * 新生代ParallelGC垃圾回收器
        * 利用多线程复制算法进行垃圾回收
        * 可以设置最大垃圾回收停顿时间
        * 可以设置吞吐量大小即系统用于垃圾回收的时间
        * 可以设置自动GC内存调节策略
    * 老年代ParallelOldGC回收器
        * 利用多线程标记压缩算法进行垃圾回收
            * 可以设置垃圾回收时的线程数量
* Current Mark Sweep CMS垃圾回收器
    * 老年代垃圾回收器
    * 利用多线程标记清除算法进行垃圾回收
    * 工作流程
        * 独占线程进行标记根对象
        * 并发标记所有对象
        * 清理钱准备以及控制停顿时间
        * 独占线程进行修正并标记数据
        * 并发清理垃圾
        * 并发充值内存
* G1垃圾回收器
    * 新生代GC
        * 利用多线程分区宣算法进行垃圾回收
        * 主要工作是回收eden区和survivor区.一旦eden区被占满,新生代GC就会启动,所有的eden区都应该被清空而survivor区会被手机一部分数据,但是应该至少仍然存在一个survivor区域
        * 老年代的区域会增多,因为部分survivor区或eden区的对象可能会晋升到到年代
    * 工作流程
        * 初始标记:多线程标记从根节点直接可达的对象
        * 根区域扫描:多线程扫描由survivor区直接可达的老年代区域,并标记这些可达的对象
        * 并发标记:扫描并查找整个堆的存活对象并标记
        * 重新标记:独占线程进行修正并标记数据
        * 独占清理:计算各个区域的存货对象和GC回收比例并进行排序,提供可混合回收的区域
        * 并发清理:识别并清理完全空闲的区域
     * 混合回收
        * 这个阶段会执行新生代GC又会选取一些被标记的老年代区域进行回收
        * 被清理对象中的存活对象会被移动到其他区域,这样可以减少空间碎片
        
#### 5.垃圾回收算法的实现原理


        引用计数算法
        对于一个对象,只要被任务一个对象引用,则该对象的引用计数器就累加1,当引用失效时,引用计数器就减1
        当该对象的引用计数器的值为0,则该对象不可能再被使用



        复制算法
        将原有内存区域分成两块,每次只使用一块区域,在垃圾回收时,将正在使用的内存中的存活对象复制到未使用的内存块中
        之后清除正在使用的内存块中的所有对象,交换两个内存的角色
        完成垃圾回收
        
        

        标记压缩算法
        首先需要从根节点开始,对所有可达对象做一次标记
        将所有存活对象压缩到内存一段
        之后清理边界外所有空间
        完成垃圾回收
        
        
        标记清除算法
        垃圾回收分为两个阶段
        在标记阶段首先通过根节点标记所有从根节点开始的可达对象,未被标记的对象就是未被引用的垃圾对象
        在清除阶段清除所有未被标记的对象
  
  
        分区算法
        将整个堆空间划分成连续的不同的小区间.每一个小区间都独立使用,独立回收.
        好处是可以控制一次回收多少个小空间
       
    
       分代算法
       将内存区间根据对象的特点分块根据每块内存区间的特点使用不同的回收算法以提高垃圾回收的效率
       
       
       
#### 6.当出现了内存溢出,你怎么排错

* 检查代码中是否有死循环或递归调用
* 检查是否有大循环重复产生新对象实体
* 检查对数据库查询中,是否有一次获得全部数据的查询.一般来说,如果一次取十万条记录到内存,就可能引起内存溢出
* 检查List,MAP等集合对象是否有使用完后,未清除的问题.List,MAP等集合对象会始终存有对对象的引用,使得这些对象不能被GC回收


#### 7.JVM 内存模型的相关知识了解多少,比如重排序,内存屏障,happen-before,主内存,工作内存等
* 内存模型
    * 主内存
        * 所有的线程所共享的
    * 工作内存
        * 线程单独使用不可共享
* 重排序
    * 编译器优化的重排序
    * 指令级别的并行重排序
    * 内存系统重排序
* happen-before:虚拟机和执行系统会对指令进行一定的重排但是指令重排是由原则的,这些原则是指令重排不可违背
    * 程序顺序原则:一个线程内保证语义的串行性
    * volatile规则:volatile变量的写先发生于读,这保证了volatile的可见性
    * 锁规则:解锁(unlock)必然发生在随后的加锁(lock)前
    * 传递性:A先于B,B先于C,那么A必然先于C
    * 线程的start()方法先于它的每一个动作
    * 线程的所有操作先于线程的终结(Thread.join)
    * 线程的中断(interrupt())先于被终端线程的代码
    * 对象的构造函数执行结束先于finalize()方法
* 内存屏障:硬件层提供了一系列的内存屏障 memory barrier / memory fence 来提供一致性的能力
    * 阻止屏障两边的指令重排序
    * 强制把写缓冲区/高速缓存中的脏数据等写回主内存让缓存中相应数据失效

#### 8.简单说说你了解的类加载器
* 类加载器:系统需使用一个类时在判断类是否已经被加载会先从地段类加载器进行判断,当系统需要加载一个类时会从顶层类加载器开始加载依次向下尝试直到从成功
    * bootstrap classloader 启动类加载器
        * 虚拟机组件
        * 加载核心类
        * 无法获得任何加载的类的classloader实现
    * extension classloader 扩展类加载器
        * 双亲为启动类加载器
    * app classloader 应用类加载器(系统类加载器)
        * 双亲为扩展类加载器
    * 自定义类加载器
        * 双亲为系统加载
* 双亲委托模式
    * 系统中的classloader在协同工作时,默认会使用双亲委托模式.即类加载的时候,系统会判断当前类是否已经被加载
    * 如果已经被加载就会直接返回可用的类,否则就会尝试加载
    * 在尝试加载时,会先请求双亲处理,如果双亲请求失败,则会自己加载
    
#### 9.讲讲 JAVA 的反射机制
* 反射
    * 在java语言层面进行方法调用模拟
    * 每当编写并且编译了一个新类就会产生一个Class对象(被保存在一个同名.class文件中)
    * 在运行时打开和检查.class文件
    * 通过Class对象找到某一个类中的方法以及属性等
    
#### 10.你们线上应用的 JVM 参数有哪些
* -server: 选择'server' vm
* -Xms: 设置初始java堆大小
* -Xmx: 设置最大java堆大小
* -Xss: 设置java线程堆栈大小
* -ea: 按指定的粒度启用断言
* -da: 禁用具有指定粒度的断言


#### 11.g1 和 cms 区别,吞吐量优先和响应优先的垃圾收集器选择
* cms
    * 标记压缩算法
    * 可以根据系统吞吐量进行垃圾回收
* g1
    * 分区算法
    * 垃圾回收响应时间短
    
#### 12.请解释如下 jvm 参数的含义:-server -Xms512m -Xmx512m -Xss1024K -XX:PermSize=256m -XX:MaxPermSize=512m -XX:MaxTenuringThreshold=20 XX:CMSInitiatingOccupancyFraction=80 -XX:+UseCMSInitiatingOccupancyOnly
* -server: 选择'server' vm
* -Xms512m: 设置初始java堆为512m
* -Xmx512m: 设置最大java堆为512m
* -Xss1024K: 设置java线程堆栈大小
* -XX:PermSize=256m: 设置非堆区初始内存为256m
* -XX:MaxPermSize=512m: 设置非堆区分配的内存的最大上限为512m
* -XX:MaxTenuringThreshold=20: 设置垃圾最大年龄为20,即对象在Survivor区存在的年龄为3(复制一次年龄+1)
* -XX:CMSInitiatingOccupancyFraction=80: 使用cms作为垃圾回收,使用80%后开始CMS收集
* -XX:+UseCMSInitiatingOccupancyOnly: 使用手动定义初始化定义开始CMS收集(禁止HotSpot自行触发CMS GC)


## 开源框架知识
#### 1.简单讲讲 tomcat 结构,以及其类加载器流程
* 组件
    * server
       * 代表整个tomcat容器
    * service
        * 拥有一个server和一个或者多个connector在一个engine内
    * engine
        * 一个engine表示为特定的请求处理流水线.由于服务可能有多个连接器,引擎会接收并处理来自这些连接器的所有请求并处理相应给适当传输客户端的连接器 
    * host
        * 一个主机是网络的名称,例如www.yourcompany.com的关联,到Tomcat服务器.引擎可能包含多个主机,Host元素也支持网络别名
    * connector
        * 连接器处理与客户端的通信.Tomcat有多个连接器可用.其中包括用于大多数HTTP流量的HTTP连接器,尤其是在将Tomcat作为独立服务器运行时,以及AJP连接器,该连接器实现了在将Tomcat连接到Web服务器时使用的AJP协议
    * context
        * 一个context代表一个Web应用程序.主机可能包含多个上下文,每个上下文都有唯一的路径
     
* 类加载器流程
    * bootstrap
        * 类加载器包含Java虚拟机提供的基本运行时类,以及来自System Extensions目录($JAVA_HOME/jre/lib/ext)中的JAR文件的所有类
    * system
        * 类加载器通常是从CLASSPATH环境变量的内容初始化的.所有这些类对于tomcat内部类和web应用程序都是可见的.但是,标准Tomcat启动脚本($CATALINA_HOME/bin/catalina.sh或%CATALINA_HOME%\bin\catalina.bat)完全忽略了CLASSPATH环境变量本身的内容,而是从以下存储库构建System类加载器
            * $CATALINA_HOME/bin/bootstrap.jar - 包含用于初始化Tomcat服务器的main()方法以及它依赖的类加载器实现类.
            * $CATALINA_BASE/bin/tomcat-juli.jar或$CATALINA_HOME/bin/tomcat-juli.jar - 记录实现类.其中包括java.util.loggingAPI的增强类(称为Tomcat JULI)和Tomcat内部使用的Apache Commons Logging库的软件包重命名副本.如果tomcat-juli.jar存在于$CATALINA_BASE/bin中,则使用它而不是$CATALINA_HOME/bin中的一个
            * $CATALINA_HOME/bin/commons-daemon.jar - Apache Commons Daemon项目中的类.这个JAR文件不存在于CLASSPATH由catalina.bat|构建的 .sh脚本,但是从bootstrap.jar的清单文件引用
    * common
        * 类加载器包含额外的类,这些类对于tomcat内部类和所有Web应用程序都是可见的,这个类加载器搜索的位置由common.loader$CATALINA_BASE/conf/catalina.properties中的属性定义.默认设置将按照它们列出的顺序搜索以下位置
            * 解压后的课程和资源 $CATALINA_BASE/lib
            * JAR文件 $CATALINA_BASE/lib
            * 解压后的课程和资源 $CATALINA_HOME/lib
            * JAR文件 $CATALINA_HOME/lib
        * 默认情况下,这包括以下内容:
            * annotations-api.jar - JavaEE注释类
            * catalina.jar - 实现Tomcat的Catalina servlet容器部分
            * catalina-ant.jar - Tomcat Catalina Ant任务
            * catalina-ha.jar - 高可用性软件包
            * catalina-storeconfig.jar - 从当前状态生成XML配置文件
            * catalina-tribes.jar - 分布式交流包
            * ecj - *.jar - Eclipse JDT Java编译器
            * el-api.jar - EL 3.0 API
            * jasper.jar - Tomcat Jasper JSP编译器运行时
            * jasper-el.jar - Tomcat Jasper EL实现
            * jsp-api.jar - JSP 2.3 API
            * servlet-api.jar - Servlet 3.1 API
            * tomcat-api.jar - 由Tomcat定义的几个接口
            * tomcat-coyote.jar - Tomcat连接器和实用程序类
            * tomcat-dbcp.jar - 基于Apache Commons Pool和Apache Commons DBCP的软件包重命名副本的数据库连接池实现.
            * tomcat-i18n - **.jar - 包含其他语言资源包的可选JAR.由于默认捆绑包也包含在每个单独的JAR中,因此如果不需要国际化消息,则可以安全地删除它们
            * tomcat-jdbc.jar - 另一个数据库连接池实现,称为Tomcat JDBC池
            * tomcat-util.jar - Apache Tomcat各种组件使用的公共类
            * tomcat-websocket.jar - WebSocket 1.1实现
            * websocket-api.jar - WebSocket 1.1 API

#### 2.tomcat如何调优,涉及哪些参数
* 配置 Connector 连接器的配置(bio,nio,apr)
* 配置文件优化
    * maxThreads:Tomcat 使用线程来处理接收的每个请求,这个值表示 Tomcat 可创建的最大的线程数,默认值是 200
    *  minSpareThreads:最小空闲线程数,Tomcat 启动时的初始化的线程数,表示即使没有人使用也开这么多空线程等待,默认值是 10
    * maxSpareThreads:最大备用线程数,一旦创建的线程超过这个值,Tomcat 就会关闭不再需要的 socket 线程
    * URIEncoding:指定 Tomcat 容器的 URL 编码格式,语言编码格式这块倒不如其它 WEB 服务器软件配置方便,需要分别指定
    * connectionTimeout:网络连接超时,单位:毫秒,设置为 0 表示永不超时,这样设置有隐患的.通常可设置为 30000 毫秒,可根据检测实际情况,适当修改
    * enableLookups:是否反查域名,以返回远程主机的主机名,取值为:true 或 false,如果设置为false,则直接返回IP地址,为了提高处理能力,应设置为 false.
    * disableUploadTimeout:上传时是否使用超时机制
    * connectionUploadTimeout:上传超时时间,毕竟文件上传可能需要消耗更多的时间,这个根据你自己的业务需要自己调,以使Servlet有较长的时间来完成它的执行,需要与上一个参数一起配合使用才会生效
    * acceptCount:指定当所有可以使用的处理请求的线程数都被使用时,可传入连接请求的最大队列长度,超过这个数的请求将不予处理,默认为100个
    * keepAliveTimeout:长连接最大保持时间(毫秒),表示在下次请求过来之前,Tomcat 保持该连接多久,默认是使用 connectionTimeout 时间,-1 为不限制超时
    * maxKeepAliveRequests:表示在服务器关闭之前,该连接最大支持的请求数.超过该请求数的连接也将被关闭,1表示禁用,-1表示不限制个数,默认100个,一般设置在100~200之间
    * compression:是否对响应的数据进行 GZIP 压缩,off:表示禁止压缩;on:表示允许压缩(文本将被压缩)force：表示所有情况下都进行压缩,默认值为off,压缩数据后可以有效的减少页面的大小,一般可以减小1/3左右,节省带宽
    * compressionMinSize:表示压缩响应的最小值,只有当响应报文大小大于这个值的时候才会对报文进行压缩,如果开启了压缩功能,默认值就是2048
    * compressableMimeType:压缩类型,指定对哪些类型的文件进行数据压缩
    * noCompressionUserAgents="gozilla,traviata":对于以下的浏览器,不启用压缩
    
#### 3.Spring 加载流程
1. ResourceLoader从存储介质中加载Spring配置信息并使用Resource表示这个配置文件的资源
2. BeanDefinitionReader读取Resource所指向的配置文件资源然后解析配置文件.配置文件中每一个<bean>解析成一个BeanDefinition对象,并保存到BeanDefinitionRegistry中
3. 容器扫描BeanDefinitionRegistry中的BeanDefinition,使用Java的反射机制自动识别出Bean工厂后处理后器(实现BeanFactoryPostProcessor接口)的Bean,然后调用这些Bean工厂后处理器对BeanDefinitionRegistry中的BeanDefinition进行加工处理
    1. 对使用到占位符的<bean>元素标签进行解析,得到最终的配置值,这意味对一些半成品式的BeanDefinition对象进行加工处理并得到成品的BeanDefinition对象
    2. 对BeanDefinitionRegistry中的BeanDefinition进行扫描,通过Java反射机制找出所有属性编辑器的Bean(实现java.beans.PropertyEditor接口的Bean),并自动将它们注册到Spring容器的属性编辑器注册表中(PropertyEditorRegistry)
4. Spring容器从BeanDefinitionRegistry中取出加工后的BeanDefinition,并调用InstantiationStrategy着手进行Bean实例化的工作
5. 在实例化Bean时,Spring容器使用BeanWrapper对Bean进行封装,BeanWrapper提供了很多以Java反射机制操作Bean的方法,它将结合该Bean的BeanDefinition以及容器中属性编辑器,完成Bean属性的设置工作
6. 利用容器中注册的Bean后处理器(实现BeanPostProcessor接口的Bean)对已经完成属性设置工作的Bean进行后续加工,直接装配出一个准备就绪的Bean
    1. 接口层描述了容器的重要组件及组件间的协作关系
    2. 继承体系逐步实现组件的各项功能
    
#### 4.Spring事务的传播属性
* PROPAGATION_REQUIRED:如果当前没有事务,就新建一个事务,如果已经存在一个事务中,加入到这个事务中
* PROPAGATION_SUPPORTS:支持当前事务,如果当前没有事务,就以非事务方式执行
* PROPAGATION_MANDATORY:使用当前的事务,如果当前没有事务,就抛出异常
* PROPAGATION_REQUIRES_NEW:新建事务,如果当前存在事务,把当前事务挂起
* PROPAGATION_NOT_SUPPORTED:以非事务方式执行操作,如果当前存在事务,就把当前事务挂起
* PROPAGATION_NEVER:以非事务方式执行,如果当前存在事务,则抛出异常
* PROPAGATION_NESTED:如果当前存在事务,则在嵌套事务内执行.如果当前没有事务,则执行与 PROPAGATION_REQUIRED 类似的操作

#### 5.Spring 如何管理事务的
* TransactionProxyFactoryBean:用于简化声明式事务处理的代理工厂bean
* PlatformTransactionManager:事务管理器,在目标资源上运行

#### 6.Spring 怎么配置事务(具体说出一些关键的 xml 元素)
* transactionManager:PlatformTransactionManager要使用的实现(例如,一个JtaTransactionManager实例)
* target:应为其创建事务代理的目标对象
* transactionAttributes:每个目标方法名称(或方法名称模式)的事务属性(例如传播行为和"只读"标志)

#### 7.说说你对 Spring 的理解,非单例注入的原理? 它的生命周期? 循环注入的原理 aop 的实现原理,说说 aop 中的几个术语,它们是怎么相互工作的
* 非单例注入
    * bean的部署的非单实例原型范围导致 每次创建一个新的bean实例时,都会创建一个对该特定bean的请求.也就是说,该bean被注入到另一个bean中,或者通过getBean()容器上的方法调用来请求它
    * Spring不管理原型bean的完整生命周期:容器实例化,配置并以其他方式组装原型对象,并将其交给客户端,而不再记录该原型实例.因此尽管在所有对象上调用初始化生命周期回调方法而不管范围,但在原型的情况下,不调用配置的销毁生命周期回调.客户端代码必须清理原型范围的对象并释放原型bean持有的昂贵资源
* 循环注入
    * 类A需要通过构造函数注入的类B的实例,而类B需要通过构造函数注入的类A的实例.如果将类A和B的Bean配置为相互注入,则Spring IoC容器会在运行时检测到此循环引用,并引发一个 BeanCurrentlyInCreationException
* IOC
    * IOC也被称为依赖注入
    * 对象通过构造函数参数,工厂方法的参数或在工厂方法构造或返回后在对象实例上设置的属性来定义它们的依赖关系,即它们使用的其他对象.容器在创建bean时会注入这些依赖关系.这个过程从根本上来说是相反的,因此名为控制反转(IOC)
* IOC容器
    * org.springframework.context.ApplicationContext 表示Spring IOC容器,并负责实例化,配置和组装上述bean.容器通过读取配置元数据获取有关要实例化,配置和组装的对象的指示信息.配置元数据用XML,Java注释或Java代码表示
* AOP实现原理
    * 通过JDK动态代理和CGLIB动态代理.JDK动态代理通过反射来接收被代理的类,并且要求被代理的类必须实现一个接口.JDK动态代理的核心是InvocationHandler接口和Proxy类
    * 如果目标类没有实现接口,那么Spring AOP会选择使用CGLIB来动态代理目标类



#### 8.Spring web mvc 中 DispatcherServlet 初始化过程
* HttpServlet
* HttpServletBean
    * 获取并设置servlet参数
* FrameworkServlet
    * 初始化IOC容器,容器初始化web.xml中配置的servlet,为其初始化自己的上下文信息servletContext并加载其设置的配置信息
* DispatcherServlet
    * 初始化WEB MVC 参数,HandlerMappings以及handler适配处理器HandlerAdapters以及视图生成器ViewResolver
    
    

## 操作系统
#### 1.Linux 系统下你关注过哪些内核参数
* vm.swappiness
    * linux 会使用硬盘的一部分做为SWAP分区,用来进行进程调度--进程是正在运行的程序--把当前不用的进程调成等待(standby),甚至睡眠(sleep),一旦要用,再调成活动(active)睡眠的进程就进入到SWAP分区把内存空出来让给活动的进程
    * 如果内存够大,应当设置 linux 不必太多的使用 SWAP 分区,可以通过修改 swappiness 的数值.swappiness=0的时候表示最大限度使用物理内存,然后才是 swap空间,swappiness＝100的时候表示积极的使用swap分区,并且把内存上的数据及时的搬运到swap空间里面
* net.ipv4.neigh.default.gc_stale_time
    * ARP参数,检查一次相邻层记录的有效性的周期.当相邻层记录失效时将在给它发送数据前,再解析一次.默认值是60秒
* net.ipv4.conf.all.rp_filter
    * 开启关闭全部反向路径过滤1为开启,0为关闭
    * 如果一台主机（或路由器）从接口A收到一个包,其源地址和目的地址分别是10.3.0.2和10.2.0.2,即<saddr=10.3.0.2, daddr=10.2.0.2, iif=A>, 如果启用反向路径过滤功能,它就会以<saddr=10.2.0.2, daddr=10.3.0.2>为关键字去查找路由表,如果得到的输出接口不为A,则认为反向路径过滤检查失败,它就会丢弃该包
* net.ipv4.conf.default.rp_filter
    * 开启关闭默认反向路径过滤1为开启,0为关闭
    * 如果一台主机（或路由器）从接口A收到一个包,其源地址和目的地址分别是10.3.0.2和10.2.0.2,即<saddr=10.3.0.2, daddr=10.2.0.2, iif=A>, 如果启用反向路径过滤功能,它就会以<saddr=10.2.0.2, daddr=10.3.0.2>为关键字去查找路由表,如果得到的输出接口不为A,则认为反向路径过滤检查失败,它就会丢弃该包
* net.ipv4.conf.default.arp_announce
    * 对网络接口上本地IP地址发出的ARP报文作出相应级别的限制
        * 0：本机所有IP地址都向任何一个接口通告ARP报文
        * 1：尽量仅向该网卡回应与该网段匹配的ARP报文
        * 2：只向该网卡回应与该网段匹配的ARP报文
* net.ipv4.conf.lo.arp_announce
    * 对网络接口上本地IP地址发出的ARP报文作出相应级别的限制
        * 0：本机所有IP地址都向任何一个接口通告ARP报文
        * 1：尽量仅向该网卡回应与该网段匹配的ARP报文
        * 2：只向该网卡回应与该网段匹配的ARP报文
* net.ipv4.conf.all.arp_announce
    * 对网络接口上本地IP地址发出的ARP报文作出相应级别的限制
        * 0：本机所有IP地址都向任何一个接口通告ARP报文
        * 1：尽量仅向该网卡回应与该网段匹配的ARP报文
        * 2：只向该网卡回应与该网段匹配的ARP报文
* net.ipv4.tcp_max_tw_buckets
    * 系统同时保持TIME_WAIT的最大数量,如果超过这个数字,TIME_WAIT将立刻被清除并打印警告信息
* net.ipv4.tcp_syncookies
    * 表示开启SYN Cookies.当出现SYN等待队列溢出时,启用cookies来处理,可防范少量SYN攻击,默认为0,表示关闭
* net.ipv4.tcp_max_syn_backlog
    * Tcp syn队列的最大长度,在进行系统调用connect时会发生Tcp的三次握手,server内核会为Tcp维护两个队列,Syn队列和Accept队列,Syn队列是指存放完成第一次握手的连接,Accept队列是存放完成整个Tcp三次握手的连接,修改net.ipv4.tcp_max_syn_backlog使之增大可以接受更多的网络连接 
* net.ipv4.tcp_synack_retries
    * tcp_synack_retries 显示或设定 Linux 核心在回应 SYN 要求时会尝试多少次重新发送初始 SYN,ACK 封包后才决定放弃.这是所谓的三段交握的第二个步骤.即是说系统会尝试多少次去建立由远端启始的 TCP 连线.tcp_synack_retries 的值必须为正整数,并不能超过 255.因为每一次重新发送封包都会耗费约 30 至 40 秒去等待才决定尝试下一次重新发送或决定放弃.tcp_synack_retries 的缺省值为 5,即每一个连线要在约180秒后才确定超时
* net.ipv6.conf.all.disable_ipv6
    * 设置启动关闭ipv6
* net.ipv6.conf.default.disable_ipv6
    * 设置启动关闭ipv6
* net.ipv6.conf.lo.disable_ipv6
    * 设置启动关闭ipv6
* fs.file-max
    * 设置系统所有进程一共可以打开的文件数量 
* net.core.somaxconn
    * 定义了系统中每一个端口最大的监听队列的长度
* vm.max_map_count
    * 设置限制一个进程可以拥有的VMA(虚拟内存区域)的数量
    
#### 2.Linux 下 IO 模型有几种,各自的含义是什么
* 阻塞IO(bloking IO)
    * 在这个IO模型中,用户空间的应用程序执行一个系统调用(recvform),这会导致应用程序阻塞,什么也不干,直到数据准备好,并且将数据从内核复制到用户进程,最后进程再处理数据,在等待数据到处理数据的两个阶段,整个进程都被阻塞.不能处理别的网络IO
* 非阻塞IO(non-blocking IO)
    * 非阻塞IO也会进行recvform系统调用,检查数据是否准备好,与阻塞IO不一样,非阻塞将大的整片时间的阻塞分成N多的小的阻塞,也就是说非阻塞的recvform系统调用调用之后,进程并没有被阻塞,内核马上返回给进程,如果数据还没准备好,此时会返回一个error.进程在返回之后,可以干点别的事情,然后再发起recvform系统调用.重复上面的过程,循环往复的进行recvform系统调用.这个过程通常被称之为轮询.轮询检查内核数据,直到数据准备好,再拷贝数据到进程,进行数据处理
* 多路复用IO(multiplexing IO)
    * 由于同步非阻塞方式需要不断主动轮询,轮询占据了很大一部分过程,轮询会消耗大量的CPU时间而后台可能有多个任务在同时进行,循环查询多个任务的完成状态,只要有任何一个任务完成,就去处理它
* 信号驱动式IO(signal-driven IO)
    * 允许Socket进行信号驱动IO,并安装一个信号处理函数,进程继续运行并不阻塞.当数据准备好时,进程会收到一个SIGIO信号,可以在信号处理函数中调用I/O操作函数处理数据
* 异步IO(asynchronous IO)
    * 用户进程进行aio_read系统调用之后,无论内核数据是否准备好,都会直接返回给用户进程,然后用户态进程可以去做别的事情.等到socket数据准备好了,内核直接复制数据给进程,然后从内核向进程发送通知.IO两个阶段,进程都是非阻塞的
    
#### 3.epoll 和 poll 有什么区别
* poll
    * 该函数准许进程指示内核等待多个事件中的任何一个发送,并只在有一个或多个事件发生或经历一段指定的时间后才唤醒没有最大文件描述符数量的限制
* epoll
    * epoll是在2.6内核中提出的,是之前的poll的增强版本.相对于select和poll来说,epoll更加灵活,没有描述符限制.epoll使用一个文件描述符管理多个描述符,将用户关系的文件描述符的事件存放到内核的一个事件表中,这样在用户空间和内核空间的copy只需一次
    
#### 4.平时用到哪些 Linux 命令
* uname -r 显示正在使用的内核版本 
* cat /proc/interrupts 显示中断 
* cat /proc/meminfo 校验内存使用 
* cat /proc/swaps 显示哪些swap被使用 
* cat /proc/version 显示内核的版本 
* cat /proc/net/dev 显示网络适配器及统计 
* cat /proc/mounts 显示已加载的文件系统 
* find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录
* groupadd group_name 创建一个新用户组 
* groupdel group_name 删除一个用户组  

#### 5.用一行命令查看文件的最后五行
* tail -n 5

### 6.用一行命令输出正在运行的 java 进程
* ps -ef | grep java

#### 7.介绍下你理解的操作系统中线程切换过程
* 线程的注册、销毁等工作是在 pthread库里面在内核中线程其实就是一个进程
* 一个线程调用了sleep,反映到核内就是sleep了一个轻量级进程,自然其他的线程(核内的轻量级进程)不受影响,照样可以run了.简言之,之所以sleep一个线程,其他线程仍然可以执行,这是因为在Linux下,线程和进程不是n对1的,而是1对1的

#### 8.进程和线程的区别
* 进程:具有一定独立功能的程序关于某个数据集合上的一次运行活动,进程是系统进行资源分配和调度的一个独立单位.
* 线程:进程的一个实体,是CPU调度和分派的基本单位,它是比进程更小的能独立运行的基本单位.线程自己基本上不拥有系统资源,只拥有一点在运行中必不可少的资源(如程序计数器,一组寄存器和栈),但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源

## 多线程
#### 1.多线程的几种实现方式,什么是线程安全
1. 继承Thread类创建线程
2. 实现Runnable接口创建线程
3. 实现Callable接口通过FutureTask包装器来创建Thread线程
4. 使用ExecutorService、Callable、Future实现有返回结果的线程

#### 2.volatile 的原理,作用,能代替锁么
* 原理
    * 通过CPU指令在修改操作时使工作内存中变量值失效,强制线程读取主内存数据
* 作用
    * 保证了不同线程对这个变量进行操作时的可见性,即一个线程修改了某个变量的值,这新值对其他线程来说是立即可见的
    * 禁止进行指令重排序
* 能代替锁么
    * 不能
    * volatile变量具有 synchronized 的可见性特性,但是不具备原子特性.这就是说线程能够自动发现 volatile变量的最新值
    * volatile作用于多个变量之间或者某个变量的当前值与修改后值之间没有约束
    * 单独使用 volatile 还不足以实现计数器、互斥锁

#### 3.画一个线程的生命周期状态图
1. new 
    * 新创建了一个线程对象
2. runnable
    * 实现Runnable接口和继承Thread可以得到一个线程类,new一个实例出来,线程就进入了初始状态
3. running
    * 可运行状态只是说你资格运行,调度程序没有挑选到你,你就永远是可运行状态
    * 调用线程的start()方法,此线程进入可运行状态
    * 当前线程sleep()方法结束,其他线程join()结束,等待用户输入完毕,某个线程拿到对象锁,这些线程也将进入可运行状态
    * 当前线程时间片用完了,调用当前线程的yield()方法,当前线程进入可运行状态
    * 锁池里的线程拿到对象锁后,进入可运行状态
4. dead
    * 当线程的run()方法完成时,或者主线程的main()方法完成时,我们就认为它死去.这个线程对象也许是活的,但是,它已经不是一个单独执行的线程.线程一旦死亡,就不能复生
    * 在一个死去的线程上调用start()方法,会抛出java.lang.IllegalThreadStateException异常
5. blocked
    * 当前线程T调用Thread.sleep()方法,当前线程进入阻塞状态
    * 运行在当前线程里的其它线程t2调用join()方法,当前线程进入阻塞状态
    * 等待用户输入的时候,当前线程进入阻塞状态
7. wait
    * 调用对象的wait(), notify()方法前,必须获得对象锁,也就是必须写在synchronized(obj) 代码段内
8, monitor
    * 当前线程想调用对象A的同步方法时,发现对象A的锁被别的线程占有,此时当前线程进入锁池状态.简言之,锁池里面放的都是想争夺对象锁的线程
    * 当一个线程1被另外一个线程2唤醒时,1线程进入锁池状态,去争夺对象锁
    * 锁池是在同步的环境下才有的概念,一个对象对应一个锁池
    
* 线程周期
    * new
        * runnable
            * running
                * sleep(),join() -> block -> sleep()结束 join结束 -> runnable
                * wait() -> wait -> notify(),notifyAll() -> monitor -> 持有锁 -> runnable
                * dead
         
#### 4.sleep 和 wait 的区别
* sleep
    * thread类提供
    * 线程没有释放锁
    * 让某个线程暂停运行一段时间,其控制范围是由当前线程决定
    * 需要捕捉异常
* wait
    * object类提供
    * 线程释放锁
    * 进入等待此对象的等待锁定池,只有针对此对象调用notify()方法后本线程才进入对象锁池准备
    * 不需要捕捉异常
    
#### 5.Lock 与 Synchronized 的区别
* lock
    * 通过代码实现的,要保证锁定一定会被释放,就必须将unLock()放到finally{}中
* synchronized
    * 在JVM层面上实现的,不但可以通过一些监控工具监控synchronized的锁定,而且在代码执行时出现异常,JVM会自动释放锁定

#### 6.synchronized 的原理是什么?解释以下名词:重排序,自旋锁,偏向锁,轻量级锁,可重入锁,公平锁,非公平锁,乐观锁,悲观锁
* synchronized 原理
    * 通过JVM指令 monitorenter(获取锁),monitorexit(释放锁) 实现
* 重排序
    * 编译器优化的重排序
    * 指令级别的并行重排序
    * 内存系统重排序
* 自旋锁
    * 在任何时刻最多只能有一个执行单元获得锁,如果自旋锁已经被别的执行单元保持,调用者就一直循环在那里看是否该自旋锁的保持者已经释放了锁
* 偏向锁
    * 大多数情况下锁不仅不存在多线程竞争,而且总是由同一线程多次获得.偏向锁的目的是在某个线程获得锁之后,消除这个线程锁重入的开销,看起来让这个线程得到了偏护
* 轻量级锁
    * b线程在锁竞争时,发现锁已经被a线程占用,则b线程不进入内核态,让b线程自旋,执行空循环,等待a线程释放锁
* 可重入锁
    * 线程可以进入任何一个它已经拥有的锁所同步的代码块
* 公平锁
    * 先等待的线程先获得锁
* 非公平锁
    * 先等待的线程可能无法先获得锁
* 乐观锁
    * 在提交操作的时候检查是否违反数据完整性
* 悲观锁
    * 数据被外界修改持保守态度,因此,在整个数据处理过程中,将数据处于锁定状态
    
    
#### 7.用过哪些原子类,他们的原理是什么
* atomicBoolean
* atomicInteger
* atomicLong
* 原理
    * 利用CPU的CAS指令
    * 它包含3个参数CAS(V,E,N).V表示要更新的变量,E表示预期值,N表示新值.仅当V值等于E值时,才会将V的值设为N,如果V值和E值不同,则说明已经有其他线程做了更新,则当前线程什么都不做.最后,CAS返回当前V的真实值
    
#### 8.用过线程池吗,newCache 和 newFixed 有什么区别,他们的原理简单概括下,构造函数的各个参数的含义是什么,比如 coreSize,maxsize 等
* newFixedThreadPool
    * 创建固定大小的线程池.每次提交一个任务就创建一个线程,直到线程达到线程池的最大大小.线程池的大小一旦达到最大值就会保持不变,如果某个线程因为执行异常而结束,那么线程池会补充一个新线程
* newCachedThreadPool
    * 创建一个可缓存的线程池.如果线程池的大小超过了处理任务所需要的线程,那么就会回收部分空闲的线程.当任务数增加时.此线程池又可以智能的添加新线程来处理任务.此线程池不会对线程池大小做限制,线程池大小完全依赖于操作系统能够创建的最大线程大小
* ThreadPoolExecutor构造函数
    * corePoolSize - 池中所保存的线程数,包括空闲线程.
    * maximumPoolSize - 池中允许的最大线程数.
    * keepAliveTime - 当线程数大于核心时,此为终止前多余的空闲线程等待新任务的最长时间.
    * unit - keepAliveTime 参数的时间单位.
    * workQueue - 执行前用于保持任务的队列.此队列仅保持由 execute 方法提交的 Runnable 任务.
    * threadFactory - 执行程序创建新线程时使用的工厂.
    * handler - 由于超出线程范围和队列容量而使执行被阻塞时所使用的处理程序.

#### 9.线程池的关闭方式有几种,各自的区别是什么
* shutdown
    1. 更新线程池状态为shutdown
    2. 中断所有空闲线程
    3. tryTerminated()尝试终止线程池
* shutdownNow
    1. 将线程池更新为stop状态
    2. 调用 interruptWorkers() 中断所有线程,包括正在运行的线程
    3. 将workQueue中待处理的任务移到一个List中,并在方法最后返回
* awaitTermination
    1. 所有任务完成执行
    2. 到达超时时间
    
#### 10.假如有一个第三方接口,有很多个线程去调用获取数据,现在规定每秒钟最多有 10 个线程同时调用它,如何做到
* Semaphore类,在许可可用前会阻塞每一个 acquire(),然后再获取该许可.每个 release() 添加一个许可,从而可能释放一个正在阻塞的获取者

#### 11.spring 的 controller 是单例还是多例,怎么保证并发的安全
* 单例还是多例
    * 单例
* 怎么保证并发的安全
    * 尽量减少使用可修改的成员变量
    * 使用threadLocal对象存储数据
    
#### 12.用三个线程按顺序循环打印 abc 三个字母,比如 abcabcabc
* ReentrantLock
    * 一个可重入的互斥锁 Lock,它具有与使用 synchronized 方法和语句所访问的隐式监视器锁相同的一些基本行为和语义,但功能更强大
    * ReentrantLock 将由最近成功获得锁,并且还没有释放该锁的线程所拥有.当锁没有被另一个线程所拥有时,调用 lock 的线程将成功获取该锁并返回.如果当前线程已经拥有该锁,此方法将立即返回

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
public class PrintABC {
    public static int cnt = 0;
    public static void main(String[] args) {
        
        final Lock lock = new ReentrantLock();
        Thread A = new Thread(new Runnable(){
            @Override
            public void run() {
                while(true){
                    lock.lock();
                    if(cnt%3==0){
                        System.out.println("A");
                        cnt++;
                    }
                    lock.unlock();
                }                
            }
            
        });
        Thread B = new Thread(new Runnable(){
            public void run(){
                while(true){
                    lock.lock();
                    if(cnt%3==1){
                        System.out.println("B");
                        cnt++;
                    }
                    lock.unlock();
                }
            }
        });
        
        Thread C = new Thread(new Runnable(){
            public void run(){
                while(true){
                    lock.lock();
                    if(cnt%3==2){
                        System.out.println("C");
                        cnt++;
                    }
                    lock.unlock();
                }
            }
        });
        A.start();
        B.start();
        C.start();
    }
}
```

#### 13.ThreadLocal 用过么,用途是什么,原理是什么,用的时候要注意什么
* 用途
    * 线程之间的变量隔离
* 原理
    * 获取当前线程对象
    * 用过ThreadLocalMap获取当前threadLocal如果没有则创建一个
    * 操作threadLocal

#### 14.如果让你实现一个并发安全的链表,你会怎么做
* 通过互斥锁ReentrantLock在进行节点的修改删除移动时加锁保证操作有效

#### 15.有哪些无锁数据结构,他们实现的原理是什么
* AtomicBoolean
* AtomicInteger
* AtomicLong
* 原理
    * 利用CPU的CAS指令
    * 它包含3个参数CAS(V,E,N).V表示要更新的变量,E表示预期值,N表示新值.仅当V值等于E值时,才会将V的值设为N,如果V值和E值不同,则说明已经有其他线程做了更新,则当前线程什么都不做.最后,CAS返回当前V的真实值
    
#### 16.讲讲 java 同步机制的 wait 和 notify
* wait
    * 在其他线程调用此对象的 notify() 方法或 notifyAll() 方法前,导致当前线程等待
    * 当前线程必须拥有此对象的锁.该线程发布对此锁的所有权并等待,直到其他线程通过调用 notify 方法,或 notifyAll 方法通知在此对象的监视器上等待的线程醒来.然后该线程将等到重新获得对监视器的所有权后才能继续执行
* notify
    * 唤醒在此对象的锁上等待的单个线程.如果所有线程都在此对象上等待,则会选择唤醒其中一个线程.选择是任意性的,并在对实现做出决定时发生.线程通过调用其中一个 wait 方法,在对象的锁上等待
    * 直到当前线程放弃此对象上的锁定,才能继续执行被唤醒的线程.被唤醒的线程将以常规方式与在该对象上主动同步的其他所有线程进行竞争;例如,唤醒的线程在作为锁定此对象的下一个线程方面没有可靠的特权或劣势
    * 此方法只应由作为此对象的锁的所有者的线程来调用.通过以下三种方法之一,线程可以成为此对象锁的所有者:
        * 通过执行此对象的同步实例方法
        * 通过执行在此对象上进行同步的 synchronized 语句的正文
        * 对于 Class 类型的对象.以通过执行该类的同步静态方法
        * 一次只能有一个线程拥有对象的监视器

#### 17.多线程如果线程挂住了怎么办
* 修改加锁顺序避免循环等待
* 加锁时限(线程尝试获取锁的时候加上一定的时限,超过时限则放弃对该锁的请求,并释放自己占有的锁)

#### 18.CountDownLatch 和 CyclicBarrier 的内部原理和用法,以及相互之间的差别
* CountDownLatch
    * 一个线程同步的辅助工具,通过它可以做到使一条线程一直阻塞等待,直到其他线程完成其所处理的任务.一个特性就是它不要求调用countDown方法的线程等到计数到达0时才继续,而在所有线程都能通过之前,它只是阻止任何线程继续通过一个await
    * 使用AQS(AbstractQueuedSynchronizer)状态来表示计数
    * 使当前线程等待,直到锁存器计数到零,如果当前计数为零,则此方法立即返回
* CyclicBarrier
    * 一个同步辅助类,它允许一组线程互相等待,直到到达某个公共的屏障点,所有线程一起继续执行或者返回.一个特性就是CyclicBarrier支持一个可选的Runnable命令,在一组线程中的最后一个线程到达之后,该命令只在每个屏障点运行一次.若在继续所有参与线程之前更新此共享状态,此屏障操作很有用
    * 递减锁存器的计数,如果线程计数达到零则释放所有正在等待的线程.如果当前计数大于零,那么它是递减的.如果新计数为零,则所有等待的线程都将重新启用线程调度目的,如果当前计数等于零,则不会发生任何事情
    
#### 19.使用 synchronized 修饰静态方法和非静态方法有什么区别
* Synchronized修饰非静态方法,实际上是对调用该方法的对象加锁
    * 情况1
        * 同一个对象在两个线程中分别访问该对象的两个同步方法
        * 结果:会产生互斥.
        * 解释:因为锁针对的是对象,当对象调用一个synchronized方法时,其他同步方法需要等待其执行结束并释放锁后才能执行

    * 情况2
        * 不同对象在两个线程中调用同一个同步方法
        * 结果:不会产生互斥
        * 解释:因为是两个对象,锁针对的是对象,并不是方法,所以可以并发执行,不会互斥.形象的来说就是因为我们每个线程在调用方法的时候都是new 一个对象,那么就会出现两个空间,两把钥匙

* Synchronized修饰静态方法,实际上是对该类对象加锁
    * 情况1
        * 用类直接在两个线程中调用两个不同的同步方法
        * 结果:会产生互斥.
        * 解释:因为对静态对象加锁实际上对类（.class）加锁,类对象只有一个,可以理解为任何时候都只有一个空间,里面有N个房间,一把锁,因此房间（同步方法）之间一定是互斥的.
    
    * 情况2
        * 用一个类的静态对象在两个线程中调用静态方法或非静态方法
        * 结果:会产生互斥.
        * 解释:因为是一个对象调用,同上.
    
    * 情况3
        * 一个对象在两个线程中分别调用一个静态同步方法和一个非静态同步方法
        * 结果:不会产生互斥
        * 解释:因为虽然是一个对象调用,但是两个方法的锁类型不同,调用的静态方法实际上是类对象在调用,即这两个方法产生的并不是同一个对象锁,因此不会互斥,会并发执行.
        
#### 20.简述 ConcurrentLinkedQueue 和 LinkedBlockingQueue 的用处和不同之处
* ConcurrentLinkedQueue
    * 基于链接节点的无界线程安全队列,它采用先进先出的规则对节点进行排序,当我们添加一个元素的时候,它会添加到队列的尾部,当我们获取一个元素时,它会返回队列头部的元素
    * 入队列
        * 获取当前尾节点
        * 循环获取尾节点下一个节点
            * 如果当前节点是尾节点
                * 通过CAS更新尾节点为当前节点
            * 如果节点不为空
                * 循环获取重新获取当前尾节点
            * 如果尾节点的下一个节点为尾节点
                * 更新当前节点为尾节点
    * 出队列
        * 获取当前队列头节点并循环获取节点元素
            * 如果当前节点不为空
                * 使用CAS跟新当前节点为null并返回
            * 如果当前节点为空
                * 获取当前节点的下一个节点
                    * 如果下一个节点不为空
                        * 设置节点为头节点
                    * 如果下一个节点为空
                        * 返回空
* LinkedBlockingQueue
    * 有边界的阻塞队列
        * 阻塞添加是指当阻塞队列元素已满时,队列会阻塞加入元素的线程,直队列元素不满时才重新唤醒线程执行元素加入操作
        * 阻塞删除是指在队列元素为空时,删除队列元素的线程将被阻塞,直到队列不为空再执行删除操作
    * 入队列
        * 加入重入锁(ReentrantLock)
        * 添加元素并获取当前未添加新元素时的队列长度
        * 如果容量未满唤醒下一个添加线程,执行添加操作
        * 释放重入锁
        * 如果当前队列只有一条数据
            * 唤醒获取删除元素线程
    * 出队列
        * 对插入和移除操作加锁
        * 循环查找删除数据
        * 找到删除节点
        * 删除
        
        
#### 21.导致线程死锁的原因？怎么解除线程死锁
* 指两个或两个以上的进程在执行过程中,由于竞争资源或者由于彼此通信而造成的一种阻塞的现象,若无外力作用,它们都将无法推进下去
    * 互斥条件:指进程对所分配到的资源进行排它性使用,即在一段时间内某资源只由一个进程占用.如果此时还有其它进程请求资源,则请求者只能等待,直至占有资源的进程用毕释放
    * 请求和保持条件:指进程已经保持至少一个资源,但又提出了新的资源请求,而该资源已被其它进程占有,此时请求进程阻塞,但又对自己已获得的其它资源保持不放
    * 不剥夺条件:指进程已获得的资源,在未使用完之前,不能被剥夺,只能在使用完时由自己释放
    * 环路等待条件:指在发生死锁时,必然存在一个进程——资源的环形链,即进程集合{P0,P1,P2,···,Pn}中的P0正在等待一个P1占用的资源;P1正在等待P2占用的资源,……,Pn正在等待已被P0占用的资源
* 当检测到系统中已发生死锁时,须将进程从死锁状态中解脱出来.常用的实施方法是撤销或挂起一些进程,以便回收一些资源,再将这些资源分配给已处于阻塞状态的进程,使之转为就绪状态,以继续运行



#### 22. 非常多个线程(可能是不同机器),相互之间需要等待协调,才能完成某种工作,问怎么设计这种协调方案
* 通过一致性中间件可实现多机器间线程协调
    * mysql 自增是原子操作可以通过自增协调多机器线程通信
    * zookeeper 强一致性中间件 节点操作协调多机器线程通信
    
    
## TCP 与 HTTP
#### 1.http1.0 和 http1.1 有什么区别
#### 2.TCP 三次握手和四次挥手的流程,为什么断开连接要 4 次,如果握手只有两次,会出现什么
#### 3.TIME_WAIT 和 CLOSE_WAIT 的区别
#### 4.说说你知道的几种 HTTP 响应码,比如 200, 302, 404
#### 5.当你用浏览器打开一个链接的时候,计算机做了哪些工作步骤
#### 6.TCP/IP 如何保证可靠性,说说 TCP 头的结构
#### 7.如何避免浏览器缓存
#### 8.简述 Http 请求 get 和 post 的区别以及数据包格式
#### 9.简述 HTTP 请求的报文格式
#### 10.HTTPS 的加密方式是什么,讲讲整个加密解密流程

## 架构设计与分布式
#### 1.常见的缓存策略有哪些,你们项目中用到了什么缓存系统,如何设计的
#### 2.用 java 自己实现一个 LRU
#### 3.分布式集群下如何做到唯一序列号
#### 4.设计一个秒杀系统,30 分钟没付款就自动关闭交易
* 
#### 5.如何做一个分布式锁
#### 6.如何使用 redis 和 zookeeper 实现分布式锁？有什么区别优缺点,分别适用什么场景
* zookeeper
    * 通过创建顺序节点来实现分布式锁
        * 客户端调用create()方法创建名为"lock"的节点,需要注意的是,这里节点的创建类型需要设置为EPHEMERAL_SEQUENTIAL
        * 客户端调用getChildren("locknode")方法来获取所有已经创建的子节点.
        * 客户端获取到所有子节点path之后,如果发现自己在步骤1中创建的节点是所有节点中序号最小的,那么就认为这个客户端获得了锁
        * 如果创建的节点不是所有节点中需要最小的,那么则监视比自己创建节点的序列号小的最大的节点,进入等待.直到下次监视的子节点变更的时候,再进行子节点的获取,判断是否获取锁
    * 释放锁的过程相对比较简单,就是删除自己创建的那个子节点即可 
#### 7.如果有人恶意创建非法连接,怎么解决
#### 8.分布式事务的原理,优缺点,如何使用分布式事务
#### 9.什么是一致性 hash
#### 10.什么是 restful,讲讲你理解的 restful
* 
#### 11.如何设计建立和保持 100w 的长连接
#### 12.如何防止缓存雪崩
#### 13.解释什么是 MESI 协议(缓存一致性)
#### 14.说说你知道的几种 HASH 算法,简单的也可以

#### 15.什么是 paxos 算法
* 首先将成员的角色分为proposers,acceptors和learners(允许身兼数职).
    * proposers提出提案,提案信息包括提案编号和提议的value
    * acceptor收到提案后可以接受(accept)提案,若提案获得多数acceptors的接受,则称该提案被批准(chosen)
    * learners只能"学习"被批准的提案.
* 角色约束
    1. 一个acceptor必须接受(accept)第一次收到的提案
    2. 一旦一个具有value v的提案被批准(chosen),那么之后批准(chosen)的提案必须具有value v
        1. 一旦一个具有value v的提案被批准(chosen),那么之后任何acceptor再次接受(accept)的提案必须具有value v
        2. 一旦一个具有value v的提案被批准(chosen),那么以后任何proposer提出的提案必须具有value v
        3. 如果一个编号为n的提案具有value v,那么存在一个多数派,要么他们中所有人都没有接受(accept)编号小于n 的任何提案,要么他们已经接受(accept)的所有编号小于n的提案中编号最大的那个提案具有value v
* 算法
    * 通过一个决议分为两个阶段:
        * prepare阶段
            * proposer选择一个提案编号n并将prepare请求发送给acceptors中的一个多数派
            * acceptor收到prepare消息后,如果提案的编号大于它已经回复的所有prepare消息,则acceptor将自己上次接受的提案回复给proposer,并承诺不再回复小于n的提案
        * 批准阶段
            * 当一个proposer收到了多数acceptors对prepare的回复后,就进入批准阶段.它要向回复prepare请求的acceptors发送accept请求,包括编号n和根据2.3决定的value(如果根据2.3没有已经接受的value,那么它可以自由决定value)
            * 在不违背自己向其他proposer的承诺的前提下,acceptor收到accept请求后即接受这个请求
    
    
#### 16.一个在线文档系统,文档可以被编辑,如何防止多人同时对同一份文档进行编辑更新
#### 17.线上系统突然变得异常缓慢,你如何查找问题
#### 18.说说你平时用到的设计模式
#### 19.Dubbo 的原理,数据怎么流转的
#### 20.一次 RPC 请求的流程是什么
#### 21.异步模式的用途和意义
#### 22.缓存数据过期后的更新如何设计
#### 23.编程中自己都怎么考虑一些设计原则的,比如开闭原则,以及在工作中的应用
#### 24.设计一个社交网站中的“私信”功能,要求高并发、可扩展等等. 画一下架构图
#### 25.MVC 模式,即常见的 MVC 框架
#### 26.聊了下曾经参与设计的服务器架构
#### 27.应用服务器怎么监控性能,各种方式的区别
#### 28.如何设计一套高并发支付方案,架构如何设计
#### 29.如何实现负载均衡,有哪些算法可以实现
#### 30.Zookeeper 的用途,选举的原理是什么
* zookeeper 强一致性中间件
    * Zxid
        * 64 位的数字
            * 低 32 位是一个简单的单调递增的计数器,针对客户端每一个事务请求,计数器加 1
            * 高 32 位则代表 Leader 周期 epoch 的编号,每个当选产生一个新的 Leader 服务器,就会从这个 Leader 服务器上取出其本地日志中最大事务的ZXID,并从中读取 epoch 值,然后加 1,以此作为新的 epoch,并将低 32 位从 0 开始计数
    * epoch
        * 当前集群所处的年代或者周期,每个 leader 都有自己的编号号,所以每次选举 leader 变更之后,都会在前一个编号的基础上加 1
    * logicalclock
        * Zookeeper服务器Leader选举的轮次,即选举轮次
    * 用途
        * 分布式环境中协调和管理服务
    * 节点角色
        * following:当前节点是跟随者,服从 leader 节点的命令
        * leading:当前节点是 leader,负责协调事务
        * election/looking:节点处于选举状态
    * 运行阶段
        * 阶段 1: Leader election (选举阶段)
            * 节点在一开始都处于选举阶段,只要有一个节点得到超半数节点的票数,它就可以当选准 leader.只有到达 阶段4 准 leader 才会成为真正的 leader.这一阶段的目的是就是为了选出一个准 leader,然后进入下一个阶段
        * 阶段 2: Discovery (发现阶段)
            * followers 跟准 leader 进行通信,同步 followers 最近接收的事务提议.这个一阶段的主要目的是发现当前大多数节点接收的最新提议,并且准 leader 生成新的 epoch,让 followers 接受,更新它们的 acceptedEpoch
        * 阶段 3: Synchronization (同步阶段)
            * 同步阶段主要是利用 leader 前一阶段获得的最新提议历史,同步集群中所有的副本.只有当 quorum 都同步完成,准 leader 才会成为真正的 leader.follower 只会接收 zxid 比自己的 last Zxid 大的提议
        * 阶段 4: Broadcast (广播阶段)
            * 到了这个阶段,Zookeeper 集群才能正式对外提供事务服务,并且 leader 可以进行消息广播.同时如果有新的节点加入,还需要对新节点进行同步
        * Recovery Phase (恢复阶段)
            * 这一阶段 follower 发送它们的 last Zixd 给 leader,leader 根据 last Zixd 决定如何同步数据.这里的实现跟前面 阶段3 有所不同,Follower 收到 TRUNC 指令会中止 L.lastCommitted Zxid 之后的提议,收到 DIFF 指令会接收新的提议
    * 选举原理
        1. 自增选举轮次:Zookeeper规定所有有效的投票都必须在同一轮次中,在开始新一轮投票时,会首先对logicalclock进行自增操作
        2. 初始化选票:在开始进行新一轮投票之前,每个服务器都会初始化自身的选票,并且在初始化阶段,每台服务器都会将自己推举为Leader
        3. 发送初始化选票:完成选票的初始化后,服务器就会发起第一次投票,Zookeeper会将刚刚初始化好的选票放入send queue中,由发送器WorkerSender负责发送出去
        4. 接收外部投票:每台服务器会不断地从receive queue队列中获取外部选票.如果服务器发现无法获取到任何外部投票,那么就会立即确认自己是否和集群中其他服务器保持着有效的连接,如果没有连接,则马上建立连接,如果已经建立了连接,则再次发送自己当前的内部投票
        5. 判断选举轮次:在发送完初始化选票之后,接着开始处理外部投票.在处理外部投票时,会根据选举轮次来进行不同的处理
            * 外部投票的选举轮次大于内部投票.若服务器自身的选举轮次落后于该外部投票对应服务器的选举轮次,那么就会立即更新自己的选举轮次(logicalclock),并且清空所有已经收到的投票,然后使用初始化的投票来进行PK以确定是否变更内部投票.最终再将内部投票发送出去
            * 外部投票的选举轮次小于内部投票.若服务器接收的外选票的选举轮次落后于自身的选举轮次,那么Zookeeper就会直接忽略该外部投票,不做任何处理,并返回步骤4
            * 外部投票的选举轮次等于内部投票.此时可以开始进行选票PK
        6. 选票PK:在进行选票PK时,符合任意一个条件就需要变更投票
            * 若外部投票中推举的Leader服务器的选举轮次大于内部投票,那么需要变更投票
            * 若选举轮次一致,那么就对比两者的ZXID,若外部投票的ZXID大,那么需要变更投票
            * 若两者的ZXID一致,那么就对比两者的SID,若外部投票的SID大,那么就需要变更投票
        7. 变更投票:经过PK后,若确定了外部投票优于内部投票,那么就变更投票,即使用外部投票的选票信息来覆盖内部投票,变更完成后,再次将这个变更后的内部投票发送出去
        8. 选票归档:无论是否变更了投票,都会将刚刚收到的那份外部投票放入选票集合receive set中进行归档.receive set用于记录当前服务器在本轮次的Leader选举中收到的所有外部投票(按照服务队的SID区别,如{(1, vote1), (2, vote2)...})
        9. 统计投票:完成选票归档后,就可以开始统计投票,统计投票是为了统计集群中是否已经有过半的服务器认可了当前的内部投票,如果确定已经有过半服务器认可了该投票,则终止投票.否则返回步骤4
        10. 更新服务器状态:若已经确定可以终止投票,那么就开始更新服务器状态,服务器首选判断当前被过半服务器认可的投票所对应的Leader服务器是否是自己,若是自己,则将自己的服务器状态更新为LEADING,若不是,则根据具体情况来确定自己是FOLLOWING或是OBSERVING
#### 31.Mybatis 的底层实现原理
#### 32.请思考一个方案,设计一个可以控制缓存总体大小的自动适应的本地缓存
#### 33.请思考一个方案,实现分布式环境下的 countDownLatch
#### 34.后台系统怎么防止请求重复提交
* 在服务器端生成一个唯一的随机标识号,专业术语称为Token(令牌),同时在当前用户的Session域中保存这个Token.然后将Token发送到客户端的Form表单中,在Form表单中使用隐藏域来存储这个Token,表单提交的时候连同这个Token一起提交到服务器端,然后在服务器端判断客户端提交上来的Token与服务器端生成的Token是否一致,如果不一致,那就是重复提交了,此时服务器端就可以不处理重复提交的表单.如果相同则处理表单提交,处理完后清除当前用户的Session域中存储的标识号
* 在下列情况下,服务器程序将拒绝处理用户提交的表单请求:
    * 存储Session域中的Token(令牌)与表单提交的Token(令牌)不同
    * 当前用户的Session中不存在Token(令牌)
    * 用户提交的表单数据中没有Token(令牌)
#### 35.如何看待缓存的使用(本地缓存,集中式缓存),简述本地缓存和集中式缓存和优缺点,本地缓存在并发使用时的注意事项
#### 36.描述一个服务从发布到被消费的详细过程
* 
#### 37.讲讲你理解的服务治理
* 
#### 38.如何做到接口的幂等性
* 

## 算法
#### 1.10 亿个数字里里面找最小的 10 个
#### 2.有 1 亿个数字,其中有 2 个是重复的,快速找到它,时间和空间要最优
#### 3.2 亿个随机生成的无序整数,找出中间大小的值
#### 4.给一个不知道长度的（可能很大）输入字符串,设计一种方案,将重复的字符排重
#### 5.遍历二叉树
#### 6.有 3n+1 个数字,其中 3n 个中是重复的,只有 1 个是不重复的,怎么找出来
#### 7.写一个字符串反转函数
#### 8.常用的排序算法,快排,归并、冒泡. 快排的最优时间复杂度,最差复杂度.冒泡排序的优化方案
#### 9.二分查找的时间复杂度,优势
#### 10.一个已经构建好的 TreeSet,怎么完成倒排序
#### 11.什么是 B+树,B-树,列出实际的使用场景
* 阶数
    * 树的阶数表示一个节点最多能有多少个子节点,比如二叉树的阶数就是2
* ┌┐
    * 向上取整
* B-树
    * 平衡多叉树
    * 每个非根节点所包含的关键字个数 j 满足:┌树阶数/2┐ - 1 <= 关键字个数(j) <= 树阶数 - 1
    * 除根结点以外的所有结点(不包括叶子结点)的度数正好是关键字总数加1,故内部子树个数 k 满足:┌树阶数/2┐ <= 内部子树个树 <= 树阶数 
    * 任意非叶子结点最多只有M(树的阶数)个儿子；且M>2
    * 根结点的儿子数为[2, M]
    * 除根结点以外的非叶子结点的儿子数为[M/2, M]
    * 每个结点存放至少┌M/2-1┐和至多M-1个关键字
    * 非叶子结点的关键字个数等于指向儿子的指针个数-1
    * 非叶子结点的关键字:K[1], K[2], ... , K[m-1],m<树阶数+1;且K[i]< K[i+1]
    * 非叶子结点的指针:P[1], P[2], ... , P[m];其中P[1]指向关键字小于K[1]的子树,P[m]指向关键字大于K[m-1]的子树,其它P[i]指向关键字属于(K[i-1], K[i])的子树
    * 所有的叶子结点都位于同一层
    
* B+树
    * B+树是应文件系统所需而出的一种B树的变型树.一棵m阶的B+树和m阶的B-树的差异在于
    * 有n棵子树的结点中含有n个关键字,每个关键字不保存数据,只用来索引,所有数据都保存在叶子节点
    * 所有的叶子结点中包含了全部关键字的信息,及指向含这些关键字记录的指针,且叶子结点本身依关键字的大小自小而大顺序链接
    * 所有的非终端结点可以看成是索引部分,结点中仅含其子树(根结点)中的最大(或最小)关键字
    
## 数据库知识
#### 1.数据库隔离级别有哪些,各自的含义是什么,MYSQL 默认的隔离级别是是什么
* 脏读
    * 一个事务读取到了另一个事务未提交的数据操作结果
* 不可重复读取
    * 一个事务对同一行数据重复读取两次,但是却得到了不同的结果
* 幻读
    * 事务在操作过程中进行两次查询,第二次查询的结果包含了第一次查询中未出现的数据或者缺少了第一次查询中出现的数据
* 读未提交(Read Uncommitted)
    * 允许脏读取,但不允许更新丢失.如果一个事务已经开始写数据,则另外一个事务则不允许同时进行写操作,但允许其他事务读此行数据
* 读提交(Read Committed) 
    * 允许不可重复读取,但不允许脏读取,读取数据的事务允许其他事务继续访问该行数据,但是未提交的写事务将会禁止其他事务访问该行
* 可重复读取(Repeatable Read)
    * 禁止不可重复读取和脏读取,但是有时可能出现幻读数据,读取数据的事务将会禁止写事务(但允许读事务),写事务则禁止任何其他事务
* 串行化(Serializable)
    * 事务只能一个接着一个地执行,不能并发执行

#### 2.MYSQL 有哪些存储引擎,各自优缺点
    
#### 3.高并发下,如何做到安全的修改同一行数据
* 乐观锁
    * 通过对数据加上类似version字段在每次修改时进行加一操作并判断当前version和数据库中version是否一直实现安全修改
#### 4.乐观锁和悲观锁是什么,INNODB 的行级锁有哪 2 种,解释其含义
* 乐观锁
    * 在提交操作的时候检查是否违反数据完整性
* 悲观锁
    * 数据被外界修改持保守态度,因此,在整个数据处理过程中,将数据处于锁定状态
* INNODB 行级锁
    * 共享锁(S):允许一个事务去读一行,阻止其他事务获得相同数据集的排他锁
        1. 事务A对数据添加共享锁,事务B可以对相同数据添加共享锁
        2. 事务A对数据进行修改,同时事务B对相同数据进行修改操作
        3. 事务A对数据进行修改完成之前,事务B对相同数据的修改操作会失败
    * 排他锁(X):允许获得排他锁的事务更新数据,阻止其他事务取得相同数据集的共享读锁和排他写锁
        1. 事务A对数据添加排他锁,事务B可以进行查询操作但对数据添加排他锁或者共享锁会进行等待
        2. 事务A对锁定数据进行修改操作后会释放锁,事务B可以获得锁,得到事务A的修改记录
#### 5.SQL 优化的一般步骤是什么,怎么看执行计划,如何理解其中各个字段的含义
* explain 命令
    * id
        * 数字相同执行顺序由上向下
        * 数字不同执行顺序id大优先执行
    * select_type
        * SIMPLE:查询中不包含子查询或者UNION
        * 查询中若包含任何复杂的子部分,最外层查询则被标记为:PRIMARY
        * 在SELECT或WHERE列表中包含了子查询,该子查询被标记为:SUBQUERY
        * 在FROM列表中包含的子查询被标记为:DERIVED(衍生)用来表示包含在from子句中的子查询的select,mysql会递归执行并将结果放到一个临时表中.服务器内部称为"派生表",因为该临时表是从子查询中派生出来的
        * 若第二个SELECT出现在UNION之后,则被标记为UNION;若UNION包含在FROM子句的子查询中,外层SELECT将被标记为:DERIVED
        * 从UNION表获取结果的SELECT被标记为:UNION RESULT
    * table
        * 表示查询的结果集
    * type
        * ALL,index,range,ref,eq_ref,const,system,NULL 从左到右,性能从最差到最好
            * ALL:Full Table Scan, MySQL将遍历全表以找到匹配的行
            * index:Full Index Scan, index与ALL区别为index类型只遍历索引树
            * range:索引范围扫描,对索引的扫描开始于某一点,返回匹配值域的行
            * ref: 使用非唯一索引扫描或者唯一索引的前缀扫描,返回匹配某个单独值的记录行
            * eq_ref: 类似ref,区别就在使用的索引是唯一索引,对于每个索引键值,表中只有一条记录匹配
            * const,system: 当MySQL对查询某部分进行优化,并转换为一个常量时,使用这些类型访问
            * NULL: MySQL在优化过程中分解语句,执行时甚至不用访问表或索引
    * possible_keys
        * 指出MySQL能使用哪个索引在表中找到记录,查询涉及到的字段上若存在索引,则该索引将被列出,但不一定被查询使用
    * key
        * 显示MySQL在查询中实际使用的索引,若没有使用索引,显示为NULL
    * key_len
        * 表示索引中使用的字节数,可通过该列计算查询中使用的索引的长度
    * ref
        * 表示上述表的连接匹配条件,即哪些列或常量被用于查找索引列上的值
    * rows
        * 表示MySQL根据表统计信息及索引选用情况,估算的找到所需的记录所需要读取的行数
    * extra
        * 包含不适合在其他列中显示但十分重要的额外信息
#### 6.数据库会死锁吗,举一个死锁的例子,mysql 怎么解决死锁
1. 事务之间对资源访问顺序的交替
    * 程序BUG导致,需要检查程序逻辑
2. 并发修改同一记录
    * 使用乐观锁
3. 索引不当导致全表扫描
    * SQL语句中不要使用太复杂的关联多表的查询
#### 7.MySql 的索引原理,索引的类型有哪些,如何创建合理的索引,索引如何优化
1.普通索引
    * 是最基本的索引,它没有任何限制
2.唯一索引
    * 与前面的普通索引类似,不同的就是:索引列的值必须唯一,但允许有空值.如果是组合索引,则列值的组合必须唯一
3.主键索引
    * 是一种特殊的唯一索引,一个表只能有一个主键,不允许有空值
4.组合索引
    * 指多个字段上创建的索引,只有在查询条件中使用了创建索引时的第一个字段,索引才会被使用.使用组合索引时遵循最左前缀集合
5.全文索引
    * 主要用来查找文本中的关键字,而不是直接与索引中的值相比较
#### 8.聚集索引和非聚集索引的区别
* 聚集索引:该索引中键值的逻辑顺序决定了表中相应行的物理顺序
* 非聚集索引:数据存储在一个地方,索引存储在另一个地方,索引带有指针指向数据的存储位置
#### 9.数据库中 BTREE 和 B+tree 区别
* B-树
    * 平衡多叉树
    * 每个非根节点所包含的关键字个数 j 满足:┌树阶数/2┐ - 1 <= 关键字个数(j) <= 树阶数 - 1
    * 除根结点以外的所有结点(不包括叶子结点)的度数正好是关键字总数加1,故内部子树个数 k 满足:┌树阶数/2┐ <= 内部子树个树 <= 树阶数 
    * 任意非叶子结点最多只有M(树的阶数)个儿子；且M>2
    * 根结点的儿子数为[2, M]
    * 除根结点以外的非叶子结点的儿子数为[M/2, M]
    * 每个结点存放至少┌M/2-1┐和至多M-1个关键字
    * 非叶子结点的关键字个数等于指向儿子的指针个数-1
    * 非叶子结点的关键字:K[1], K[2], ... , K[m-1],m<树阶数+1;且K[i]< K[i+1]
    * 非叶子结点的指针:P[1], P[2], ... , P[m];其中P[1]指向关键字小于K[1]的子树,P[m]指向关键字大于K[m-1]的子树,其它P[i]指向关键字属于(K[i-1], K[i])的子树
    * 所有的叶子结点都位于同一层
* B+树
    * B+树是应文件系统所需而出的一种B树的变型树.一棵m阶的B+树和m阶的B-树的差异在于
    * 有n棵子树的结点中含有n个关键字,每个关键字不保存数据,只用来索引,所有数据都保存在叶子节点
    * 所有的叶子结点中包含了全部关键字的信息,及指向含这些关键字记录的指针,且叶子结点本身依关键字的大小自小而大顺序链接
    * 所有的非终端结点可以看成是索引部分,结点中仅含其子树(根结点)中的最大(或最小)关键字
#### 10.Btree 怎么分裂的,什么时候分裂,为什么是平衡的
* 索引分裂
    * 索引块的分裂,当一次DML(INSERT,DELETE,UPDATE)事务操作修改了索引块上的数据,但是旧有的索引块没有足够的空间来容纳新修改的数据,那么将分裂出一个新索引块,旧有块的部分数据放到新开辟的索引块上去
 
#### 11.ACID 是什么
* 原子性(Atomicity)
    * 整个事务中的所有操作,要么全部完成,要么全部不完成,不可能停滞在中间某个环节
* 一致性(Consistency)
    * 一个事务可以封装状态改变(除非它是一个只读的),事务必须始终保持系统处于一致的状态,不管在任何给定的时间并发事务有多少
* 隔离性(Isolation)
    * 隔离状态执行事务,使它们好像是系统在给定时间内执行的唯一操作
* 持久性(Durability)
    * 在事务完成以后,该事务对数据库所作的更改便持久的保存在数据库之中,并不会被回滚
#### 12.Mysql 怎么优化 table scan 的
#### 13.如何写 sql 能够有效的使用到复合索引
* 在查询使用时,最好将条件顺序按找索引的顺序,这样效率最高
* 尽量创建使用索引列为1-2列的索引
#### 14.mysql 中 in 和 exists 区别
* in
    * 确定给定的值是否与子查询或列表中的值相匹配.in在查询的时候,首先查询子查询的表,然后将内表和外表做一个笛卡尔积,然后按照条件进行筛选.所以相对内表比较小的时候,in的速度较快
* exists
    * 指定一个子查询,检测行的存在.遍历循环外表,然后看外表中的记录有没有和内表的数据一样的.匹配上就将结果放入结果集中
* 区别
    * in 是把外表和内表作hash 连接,而exists是对外表作loop循环,每次loop循环再对内表进行查询
#### 15.数据库自增主键可能的问题
* 不可拆库,因为id会重复
* 自增主键不连续

## 消息队列
#### 1.用过哪些 MQ,和其他 mq 比较有什么优缺点,MQ 的连接是线程安全的吗,你们公司的MQ 服务架构怎样的
#### 2.MQ 系统的数据如何保证不丢失
#### 3.rabbitmq 如何实现集群高可用
* 集群模式
    * 单一模式: 最简单的情况,非集群模式.
    * 普通模式: 默认的集群模式.
      *　对于 Queue 来说,消息实体只存在于其中一个节点,A、B 两个节点仅有相同的元数据,即队列结构.
      * 当消息进入 A 节点的 Queue 中后,consumer 从 B 节点拉取时,RabbitMQ 会临时在 A、B 间进行消息传输,把 A 中的消息实体取出并经过 B 发送给 consumer. 所以 consumer 应尽量连接每一个节点,从中取消息
      * 对于同一个逻辑队列,要在多个节点建立物理 Queue.否则无论 consumer 连 A 或 B,出口总在 A,会产生瓶颈.该模式存在一个问题就是当 A 节点故障后,B 节点无法取到 A 节点中还未消费的消息实体.如果做了消息持久化,那么得等 A 节点恢复,然后才可被消费
    * 镜像模式: 把需要的队列做成镜像队列,存在于多个节点,属于 RabbitMQ 的 HA 方案
* 集群节点
    * 内存节点: 只保存状态到内存(持久的 queue 的持久内容将被保存到 disk)
    * 磁盘节点: 保存状态到内存和磁盘,内存节点虽然不写入磁盘,但是它执行比磁盘节点要好,集群中,只需要一个磁盘节点来保存状态 就足够了,如果集群中只有内存节点,那么不能停止它们,否则所有的状态,消息等都会丢失
#### 4.rabbitmq 
* Producer:数据的发送方
* Consumer:数据的接收方
* Exchange:消息交换机,它指定消息按什么规则,路由到哪个队列 
    * direct
        * 消息中的路由键(routing key)如果和 Binding 中的 binding key 一致, 交换器就将消息发到对应的队列中
    * fanout
        * 每个发到 fanout 类型交换器的消息都会分到所有绑定的队列上去
    * topic 
        * topic 交换器通过模式匹配分配消息的路由键属性,将路由键和某个模式进行匹配,此时队列需要绑定到一个模式上
* Queue:消息队列载体,每个消息都会被投入到一个或多个队列
* Binding:绑定,它的作用就是把 exchange 和 queue 按照路由规则绑定起来
* Routing Key:路由关键字,exchange 根据这个关键字进行消息投递
* vhost:虚拟主机,一个 broker 里可以开设多个 vhost,用作不同用户的权限分离
* channel:消息通道,在客户端的每个连接里,可建立多个 channel,每个 channel 代表一个会话任务

## Redis,Memcached
#### 1.redis 的 list 结构相关的操作
1.	BLPOP key1 [key2 ] timeout
    * 移出并获取列表的第一个元素, 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止.
2.	BRPOP key1 [key2 ] timeout
    * 移出并获取列表的最后一个元素, 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止.
3.	BRPOPLPUSH source destination timeout
    * 从列表中弹出一个值,将弹出的元素插入到另外一个列表中并返回它； 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止.
4.	LINDEX key index
    * 通过索引获取列表中的元素
5.	LINSERT key BEFORE|AFTER pivot value
    * 在列表的元素前或者后插入元素
6.	LLEN key
    * 获取列表长度
7.	LPOP key
    * 移出并获取列表的第一个元素
8.	LPUSH key value1 [value2]
    * 将一个或多个值插入到列表头部
9.	LPUSHX key value
    * 将一个值插入到已存在的列表头部
10.	LRANGE key start stop
    * 获取列表指定范围内的元素
11.	LREM key count value 
    * 移除列表元素
12.	LSET key index value
    * 通过索引设置列表元素的值
13.	LTRIM key start stop 
    * 对一个列表进行修剪(trim),就是说,让列表只保留指定区间内的元素,不在指定区间之内的元素都将被删除.
14.	RPOP key
    * 移除并获取列表最后一个元素
15.	RPOPLPUSH source destination 
    * 移除列表的最后一个元素,并将该元素添加到另一个列表并返回
16.	RPUSH key value1 [value2]
    * 在列表中添加一个或多个值
17.	RPUSHX key value
    * 为已存在的列表添加值
#### 2.Redis 的数据结构都有哪些
* String
* Hash
* List
* Set
* Key
#### 3.Redis 的使用要注意什么,讲讲持久化方式,内存设置,集群的应用和优劣势,淘汰策略等.
#### 4.redis2 和 redis3 的区别,redis3 内部通讯机制
#### 5.当前 redis 集群有哪些玩法,各自优缺点,场景
#### 6.Memcache 的原理,哪些数据适合放在缓存中

#### 7.redis 和 memcached 的内存管理的区别

#### 8.Redis 的并发竞争问题如何解决,了解 Redis 事务的 CAS 操作吗
#### 9.Redis 的选举算法和流程是怎样的

## 搜索
#### 1.elasticsearch 了解多少,说说你们公司 es 的集群架构,索引数据大小,分片有多少,以及一些调优手段.elasticsearch 的倒排索引是什么
* 索引
    * 是指向一个或者多个物理分片的逻辑命名空间 
        * 通过setting中的number_of_shards可以设置分配的主分片数(默认5个)
        * 通过setting中的number_of_replicas可以设置分配分片副本数
* 分片
    * 一个底层的工作单元,它仅保存了全部数据中的一部分
    * 一个分片是一个 Lucene 的实例,以及它本身就是一个完整的搜索引擎
* 倒索引
    * 适用于快速的全文搜索.一个倒排索引由文档中所有不重复词的列表构成,对于其中每个词,有一个包含它的文档列表
* 调优
    * 线程池
        * cache:这是无限制的线程池,为每个传入的请求创建一个线程
        * fixed:这是一个有着固定大小的线程池,大小由size属性指定,允许你指定一个队列(使用queue_size属性指定)用来保存请求,直到有一个空闲的线程来执行请求.如果Elasticsearch无法把请求放到队列中(队列满了),该请求将被拒绝
        * index:此线程池用于索引和删除操作.它的类型默认为fixed,size默认为可用处理器的数量,队列的size默认为300
        * search:此线程池用于搜索和计数请求.它的类型默认为fixed,size默认为可用处理器的数量乘以3,队列的size默认为1000
        * suggest:此线程池用于建议器请求.它的类型默认为fixed,size默认为可用处理器的数量,队列的size默认为1000
        * get:此线程池用于实时的GET请求.它的类型默认为fixed,size默认为可用处理器的数量,队列的size默认为1000
        * bulk:此线程池用于批量操作.它的类型默认为fixed,size默认为可用处理器的数量,队列的size默认为50
        * percolate:此线程池用于预匹配器操作.它的类型默认为fixed,size默认为可用处理器的数量,队列的size默认为1000
    * 用G1垃圾回收机制代替默认CMS
#### 2.elasticsearch 索引数据多了怎么办,如何调优,部署
#### 3.lucence 内部结构是什么
