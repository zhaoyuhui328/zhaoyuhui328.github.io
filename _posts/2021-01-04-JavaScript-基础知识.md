**JS基本语法**
============================
	•    jS代码中严格区分大小写  不然会报错
	•   不加";"，浏览器会自动添加  但会消耗系统资源（性能问题）  有时也会加错";" 所以一定要记得加";"

###字面量和变量
	•  字面量为不可改变的值 一般不会直接使用 
	•   变量可以用来保存字面量  而且变量可以任意变化
	•  在JS中用var关键字来声明变量 
	• 例如： 
	 var a; //或者 var=a;
	 a = 123;
	 console.log(a);


###JS数据类型（6种）
	• String  字符串
	• Number 数值
	• Boolean 布尔值
	• Null 空值
	• Undefine 未定义
	• Object 对象（引用数据类型）

#####1.String 字符串数据类型
	• String 字符串需要用引号引起来。（单引号双引号都可以） 但引号不能嵌套，可以用单引号套双引号或者双引号套单引号
	• 在字符串中 ，可以使用 \ 作为转义字符    例如：
	var str = "我说:\"今天天气真不错！\"";
	•     \n 表示换行  \t相当于tab键     注意：\\表示\
	
	•     例子 var str="hello";
	
	•     加上双引号叫字符串   不加双引号叫变量

#####2.Number 数据类型
	•        在js中  所有数值都是Number类型   包括整数和浮点数
	•         可以使用一个运算符typeof来检查一个变量的类型
	•         例：console.log(typeof a);
	•         JS中可以表示数字的最大值   console.log(Number.MAX_VALUE)
	•         如果表示的数字超过了最大值  会反馈一个Infinity表示无穷
	•     NaN 是一个特殊的数字  Not a  Number    使用typeof也会返回number
	•     JS中整数的运算可以保证精确    进行浮点运算  可能得到一个不精确的值
	

#####3.Null和Undefine数据类型
	• NULL只有一个值null   专门用来表示空对象
	•         使用typeof检查null值时，会返回object
	• Undefined也是只有一个值undefined   例：var = a; 未给a赋值   就会返回这个值
	

#####4.Boolean布尔型数据类型
	•   Boolean布尔值  只有两个   true真  false假  主要用于逻辑判断
	•         例：var bool = true ;

#####5.Object数据类型
    JS对象：（object）
      对象属于一种复合的数据类型，可以保存多个数据类型

    ~ 对象的分类：
	1.内建对象：
	           - 由ES标准中定义的对象，在任何的ES的实现中都可以用
	           - 比如 ： Math String Funtion等
	2.宿主对象：
	           - 由JS的运行环境提供的对象，目前来讲主要是由浏览器提供的对象
	           - 比如： BOM（浏览器对象模型） DOM（文档对象模型）
	3.自定义对象：
	           - 由开发人员自己创建的对象
	
	• 对象的基本操作：
          1.创建对象
                var obj = new Object();
            // 使用new关键字调用的函数是构造函数constructor   构造函数是专门用来创建对象的函数   
       
       2.添加属性
           语法：对象.属性名 = 属性值;
               - 例  obj.name = "***";

        3.读取对象中的属性：
             语法：对象.属性名
                 -  例  console.log(obj.name);
    
        4.修改对象的属性值：
             语法：对象.属性名 = 新值; 
    
        5.删除对象的属性值：
            语法: delete obj.name; 

	• 属性名和属性值
	  -  属性名： 不强制要求遵守标识符的规范 但是尽量按照标识符的规范来写。
	                  如果使用  不能用“  .“的操作  语法：对象["属性名"] = 属性值
	                  使用“[ ]”这种形式去操作属性，更加的灵活，在“[ ]”内传递一个变量，这             
	                  样变量值是多少就会读取那个属性。
	 - 属性值： 可以是任意的数据类型  甚至可以是一个对象  或者是一个函数
	
	 in 运算符   - 可以检查一个对象中是否含有指定的属性   有 - true     无 - false
	                 语法： console.log ( " 属性名 "  in  对象 );
	• 对象字面量
	     使用对象字面量来创建一个对象
	              语法：var obj = { };
	     使用对象字面量，可以在创建对象时，直接指定对象的属性
	              语法：var obj = {属性名 ：属性值 ，属性名：属性值……..}；
	              最后一个属性不用加“，”
	• 枚举对象中的属性：
	 var obj = {
	        .....
	    }
	
	    使用for ... in  语句
	    语法  : for(var 变量 in 对象){
	                 ...;
	            }
	    for ... in语句  对象中有几个属性，循环体就会执行几次  每次执行时，会将对象中的一个属性的名字赋值给变量


	• Date对象：
	
	- 在JS中使用Date对象来表示一个时间
	   // 创建 var d = new Date();
	
	   // 创建一个指定的时间对象
	    var d2 = new Date("12/03/2016 11:10:30"); //格式  月/日/年 时:分:秒
	
	    getDate() -获取当前日期是几日；
	
	    getDay() -获取当前对象是周几；  会返回一个0-6的值  0为周日
	
	    getMonth() -获取当前日期是几月； 0-11 0表示1月
	
	    getFullYear() -获取当前日期的年份；
	
	    getTime() -获取当前日期对象的时间戳
	
	   时间戳:  指得是从格林威治标准时间的1970年1月1日0时0分0秒到当前日期所花费的毫秒                    
	                数（1s=1000ms）
	   time = Date.now();   //获取当前时间的时间戳
	
	
	• Math对象：
	    -  Math和其他的对象不同，他不是一个构造函数，它属于一个工具类不用创建对象，它   
	       里边封装了数学相关的属性和方法
	   - 比如: Math.PI 表示圆周率      Math.abs() 计算绝对值
	          Math.ceil 向上取整(1.4 = 2)    Math.floor() 向下取整(1.6 = 1)
	          Math.random() 可以生成一个0-1之间的随机数
	        Math.random()*10  0-10(不包括0和10)
	          Math.round(Math.random()*10)  包括0-10
	          Math.max()  获取多个数的最大值   Math.min()  获取多个数的最小值
	          Math.paw(x,y)  返回x的y次幂的值

###基本数据类型和引用数据类型区别:
	• JS中的变量都是保存到栈内存中的
                 基本数据类型的值直接在栈内存中存储，
                 值与值之间是独立存在，修改一个变量不会影响其他的变量

	• 对象是保存到堆内存中的
                 每创建一个新的对象，就会在堆内存中开辟一个新的空间
                 而变量保存的是对象的内存地址（对象的引用），如果两个变量保存的是同一对象的 
               引用， 当一个通过一个变量来修改属性时，另一个也会受到影响


###对象的属性和对象的方法的区别
      方法是定义在对象上的操作，属性是记录对象性质和状态的变量
      比如：  
           - 属性：一个人有头有脚是人的属性
           - 方法：一个人会跑会跳是这个人的方法        方法表示一个人的行为

###垃圾回收(GC)
     - 程序运行过程中会产生垃圾  积攒过多后会导致运行变慢
       所以需要一个垃圾回收机制，来处理运行过程中产生的垃圾

    在JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁
    我们不需要也不能进行垃圾回收的操作

    我们需要做的只是要将不再使用的对象设置为null即可

###作用域：一个变量作用的范围
    - 在JS中一共有两种作用域
       1. 全局作用域   
             - 直接编写在script标签中的JS代码，都在全局作用域
             - 全局作用在页面打开时创建，在页面关闭时销毁
             - 在全局作用域中有一个全局对象window   代表一个浏览器的窗口   由浏览器创建，可以直                
             接使用
             - 在全局作用域中:
               创建的变量都会作为window对象的属性保存
               创建的函数都会作为window对象的方法保存

             全局变量在页面的任意的部分都能被访问到

      2.函数作用域
            - 调用函数时，创建函数作用域 ；函数执行完毕后 ，函数作用域销毁
            - 每调用一次函数就会创建一个新的函数作用域，他们之间是相互独立的
            - 在函数作用域中可以访问到全局作用域的变量
               但是在全局作用域中无法访问到函数作用域的变量
            - 在函数中要访问全局变量可以使用window对象
            - 在函数中，不是用var声明的变量都会成为全局变量


###函数
	•  使用函数声明来创建函数
          语法: 
                function 函数名([形参1,形参2,.....,形参N]){
                          语句....
                }

	• 使用函数表达式来创建一个函数   //   也基本不使用
         语法:
                  var 函数名 = function 函数名([形参1,形参2,.....,形参N]){
                                语句....
                      }

	• 函数的参数: 
                 function sum(a,b){......}    //可以在函数的()中指定一个或多个形参（形式参数）

                 sum(1,2)  // 在调用函数时，可以在()中指定实参（实际参数）

               调用函数时解析器不会检查实参的类型，所以要注意  是否有可能传递非法的参数，如果  
          有，需要对参数的类型进行检查

               多余的实参不会被赋值

               实参可以时任何数据类型，也可以时一个对象。

	• 函数的返回值:
                在函数中，return后的语句都不会执行
                如果return后没有返回值  或者不写return  则会返回undefine
                返回值可以是任何数据类型，返回值也可以返回对象，也可以返回函数

	• 立即执行函数
         语法 ：   (function(){
                            alert(".....");
                      })(); 


	• 构造函数
         创建一个构造函数，专门用来创建Person对象的

         与普通函数的区别是调用方式的不同
          普通函数是直接调用 而构造函数需要使用new关键字来调用
    
         构造函数流程：
                1.立刻创建一个新的对象
                2.将新建的对象设置为函数中的this
                3.逐行执行函数中的代码
                4.将新建的对象作为返回值返回

          语法: 
               function Person(name , age , gender){
                   this.name = name;
                   this.age = age;
                   this.gender = gender;
               }
        

          使用同一个构造函数创建的对象，我们称之为一类对象。（例：Person类的实例）
          我们将通过一个构造函数创建的对象，称为是该类的实例


          使用instanceof可以检查一个对象是否是一个类的实例
             语法:  
                 对象 instanceof 构造函数
          如果是  返回true  如果不是 返回false 


	• 原型prototype
         我们所创建的每一个函数，解析器都会向函数中添加一个属性prototype
          这个属性对应着一个对象，这个对象就是我们所谓的原型对象
         如果函数作为普通函数调用prototype没有任何作用
         当函数以构造函数的形式调用时，它所创建的对象中都会有一个隐含的属性，
         指向该构造函数的原型对象，我们可以通过__proto__来访问该属性

        原型对象就相当于一个公共的区域，所有同一类的实例都可以访问到这个原型对象，
         我们可以将对象中共有的内容，统一设置到原型对象中。
 
        当我们访问对象的一个属性或方法时，它会现在对象自身中寻找，如果有则直接使用，
        如果没有则会去原型对象中寻找，如果有则直接使用

        以后我们创建构造函数时，可以将这些对象共有的属性和方法，统一添加到构造函数的原型对象中，
       这样不用分别为每一个对象添加，也不会影响到全局作用域，就可以使每个对象都具有这些属性和方法 


     可以时用hasOwnProperty()来检查对象自身中是否含有该属性
     Console.log ( mc.hasOwmProperty('age') )

	• 原型对象也是对象，所以它也有原型。
	     当我们使用一个对象的属性或方法时，会先在自身中寻找
	              自身中如果有，则直接使用
	              如果没有则去原型对象中寻找，如果原型对象中有，则使用
	              如果没有则去原型的原型中寻找，直到找到Object对象的原型，
	                  Object对象的原型没有原型，如果在Object中依然没有找到，则返回undefined






	•   函数的方法:
              call()和apply()
              call()方法可以将实参在对象之后依次传递
              apply()方法需要将实参封装到一个数组中统一传递 
   

	•    arguments()
           在调用函数时，浏览器每次都会传递两个隐含的参数:
           1.函数的上下文对象this
           2.封装实参的对象arguments   - arguments是一个类数组(伪数组)对象
               arguments[0]  表示第一个参数

###函数中的this
       1.this是什么？
          * 任何函数本质上都是通过某个对象来调用的，如果没有直接指定就是window
          * 所有函数内部都有一个变量this
          * 它的值是调用函数的当前对象
        
        2.如何确定this的值?
          * test(): window
          * p.test(): p
          * new test(): 新的创建对象
          * p.call(obj): obj
```
<!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=de    vice-width, initial-scale=1.0">
        <title>Document</title>
        <script>
            function Person(color) {
                console.log(this);
                this.color = color;
                this.getColor = function () {
                    console.log(this);
                    return this.color;
                };
                this.setColor = function () {
                    console.log(this);
                    this.color = color;
                };
            }
            Person("red"); //this是谁？ window
            var p = new Person("yellow");
            p.getColor(); //this是谁？ p
            var obj = {};
            p.setColor.call(obj, "black"); //    this是谁? obj
            var test = p.setColor;
            test(); //this是谁？ window
            function fun1() {
                function fun2() {
                    console.log(this);
                }
                fun2(); //this是谁？ window
            }
            fun1();
        </script>
    </head>
    <body>
    <body/>
    <html/>
```
###数组(Array)
        也是一个对象  存储数据
        数组使用数字来作为索引操作元素
        索引:  从0开始的整数就是索引
                    数组的存储性能比普通对象要好


	• 语法: 
                    var arr = new Array();
	          数组[索引] = 值;

	• 获取数组的长度：(lenth)
                     arr.lenth
          对于非连续的数组，使用lenth会获取到数组的最大的索引+1   所以尽量不要创建非连续的数
        组

	• 使用字面量来创建数组:
                语法: var arr = [];

        数组的元素可以是任意类数据类型   可以是对象 可以是函数

	• 多维数组  var arr = [[......]]


	• arr.push(... , ... , ...);   //向数组的最后一个添加一个或多个元素
	• arr.pop();   //删除数组的最后一个元素  调用一次删除一次
	• arr.unshift()  //向数组开头添加一个或多个元素，并返回新的数组长度   插入后，索引会依次调整
	• arr.shift()   //删除数组的第一个元素  调用一次删除一次
	• arr.join("连接符 // 如果不使用连接符，默认为,")  //将数组转换成一个字符串  该方法不会改变原数组。
	• arr.sort()  // 按照unicode编码进行排序

	• 数组的遍历
         for(var i = 0 ; i < arr.lenth ; i++){
                console.log(arr[i]);
         }


         forEach()  //只支持IE8以上的浏览器
         forEach()方法需要一个函数作为参数
         语法: 
                 arr.forEach(function(value , index , obj){
                       ...
                 });
         浏览器会在回调函数中传递三个参数：
         第一个是当前正在遍历的元素
         第二个参数是当前正在遍历的元素的索引
         第三个参数就是当前正在遍历的数组

	• slice()和splice()

	slice()
                        - 可以用来从数组中提取指定的元素
                   - 该方法不会改变原数组，而是将截取到的数组封装到一个新的数组中返回
                   - 参数： 1.截取开始的位置的索引，包含开始索引
                                  2.截取结束的位置的索引，不包含结束索引

       splice()
                  - 可以用于删除数组中指定的元素
                  - 使用splice()会影响到原数组，会将指定元素从原数组中删除，并将被删除的元素作为
                   返回值返回
                  - 参数:  1.第一个表示开始位置的索引
                               2.第二个表示删除的数量
                                  arr.splice(j,1);

###强制类型转换
             类型转换主要时将其他数据类型转换为 String  Number  Boolean

    1.转换为String  
     <1> 调用被转换数据类型的toString()方法  a.toString()
          该方法不会影响原变量   可以新赋值一个值 例：b = a.toString();
          要改原来的话  可以 例：a = a.toString();
          但是null和undefined没有toString方法  使用时会报错
     <2> 调用Sring()函数,并将被转换的变量定义为他的参数
       

    2.转换为Number
      一. <1> 使用Number()函数，并将被转换的变量定义为他的参数
          <2> 字符串转Number时，若是纯数字，则可以直接转换    若字符串有非数字的内容，则转换
              为NaN
                若字符串中是space或没有东西  则转换为0
          <3> Boolean转数字   true 为1   false为2
          <4> null为0
          <5> undefined 为NaN
      二.     parseInt()   把一个字符串转换为一个整数
                parseFloat()  把一个字符串转换为一个浮点数

    3.转化为Boolean
        使用Boolean()函数



    *   任何值和NaN做运算 都是NaN
    *   任何值和字符串相加 都会转换成字符串  然后拼串


###正则表达式
      正则表达式用于定义一些字符串的规则。   
      计算机可以根据正则表达式，来检查一个字符串是否符合规则，获取将字符串符合规则的
      内容提取出来
	- 语法：
	      var 变量 = new RegExp("正则表达式" , "匹配模式");
     test()  - 使用这个方法可以用来检测一个字符串是否符合正则表达式的规则，
                  符合返回 true    不符合返回false
    使用字面量
             语法：var 变量 = /正则表达式/匹配模式

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        var reg = /a|b/; //[ab] == a|b   [a-z]  [A-Z] [A-z]
        console.log(reg.test("abc"));
        var str = "1a2b3c4d5e6f7";
        var result = str.split(/[A-z]/);
        console.log(result);
        var str = "1a2b3c4d5e6f7";
        var result = str.search(/[A-z]/g);
        console.log(result);
        var str = "1a2b3c4d5e6f7";
        var result = str.match(/[A-z]/g);
        console.log(result);
        // 1.被替换的内容 2.新的内容
        var str = "1a2b3c4d5e6f7";
        var result = str.replace(/[A-z]/g, "@");
        console.log(result);
        var reg = /a{3}/; // {m,n} m~n次 {m,} m次以上 +至少一个  *0个或多个 ?0个或1个
        // /^a / 以a开头  /a$/ 以a结尾
        console.log(reg.test("abababc"));
        // 创建一个正则表达式，用来检查一个手机号是否合法
        var phoneStr = "13567890111";
        var phoneReg = /^1[3-9][0-9]{9}$/;
        console.log(phoneReg.test(phoneStr));
        // . 表示任意字符  检查 "." 时需要使用转义字符 "\."   在这儿不需要用\\来表示\
        //  \时字符串中的转义字符  ， \\来表示\
        //  \w [A-z0-9_]   \W 除了字母数字     \d任意的数字     \D除了数字 
        //  \s 空格  \S 除了空格     \b 单词边界  \B除了单词边界
        // 接收一个用户的收入
        var str = prompt("请输入你的用户名：");
        console.log(str);
        //  去除开头和结尾的空格
        //   /^\s*|\s*$/g
        // 电子邮件  248081983@qq.com
        var email = "abc.abc@abc.com";
        var emailReg = /^\w{3,}(\.\w+)*@[A-z0-9]+(\.[A-z]{2-5}){1,2}$/;
        console.log(emailReg.test(email));
    </script>
</head>
<body>
</body>
</html>
```
