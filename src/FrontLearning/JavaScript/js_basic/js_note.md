﻿# js基础

## js输出
​    document.write   向body中写字符串
​    console.log      向控制台输出
​    alert            弹出警告框输出
## js编写位置
​    1.外联文件

        <script src="引入的文件位置"></script>
​    2.内联文件
​        <script type="text/javascript">
​            js代码编写的位置
​        </script>
​    3.内嵌代码(结构与行为耦合，不使用)
​        <input type="button" onclick="alert('弹出')"></input>
​        <a href="javascript:alert('弹出');"></a>
## js基本语法
​    严格区分大小写
​    语句分号结尾
​    没有添加分号时浏览器自动添加，但是消耗资源并且可能添加出错
## js字面量和变量
​    字面量即为常量
​    变量可被字面量赋值
​    变量声明和赋值可分开或一起
​        var a;
​        a = 1;
​    或者
​        var a = 1;
## js标识符
​    所有可以自定义的变量都叫做标识符，并且遵循以下规范：
​        1.只能以字母数字，下划线，$构成
​        2.不能以数字开头
​        3.不能使用ES的关键字和保留字
​        4.一般使用驼峰命名法
​    标识符以unicode编码表示，因此可以使用UTF-8的所有内容，但是一般只使用英文
## js基本数据类型
​    1.string
​    2.number
​        可以表示整数与浮点数
​        2进制浮点数以分数表示，不准确
​        NaN与Infinity是数值的字面量，表示非数与无穷
​        typeof 参数  检测某个值的类型
​    3.boolean
​        只有两个值：true  false
​    4.null
​        表示一个空对象
​        var a = null;
​        console.log(typeof a);
​        结果为object
​    5.undefined
​        已经声明的变量未赋值则成为undefined
​        var a;
​        console.log(typeof a);
​        结果为undefined
## 强制类型转换
​    1.string
​        两种办法：a.toString()   String()
​            toString只能用于对象，因此null和undefined无法调用
​            String()对于Number, String, Boolean来说会调用底层的toString()方法，对于null和undefined会直接进行转换
​    2.number
​        三种方法：Number(), parseInt(), parseFloat()
​            Number()：
​                对于字符串来说如果只包含数字，直接转换成数字，如果包含非数字转换成NaN，如果是""或者"  "则转换成0
​                对于boolean值，true转换成1，false转换成0
​                对于null，转换成0
​                对于undefined，转换成NaN
​            parseInt()：
​                首先将所有内容转换成字符串再开始解析。
​                从左到右依次解析，需要非整数直接舍去，第一位非整数返回NaN
​            parseFloat()：
​                与parseInt()相似，只是遇到第一位小数点不会忽略会转换成小数，其余与之相同
​    3.boolean
​        一种方法：Boolean()
​            对于数字：只有0跟NaN会转换成false
​            对于字符串：只有""会转换成false
​            对于null和undefined，只会转换成false
## 进制
​    16进制在数字前加0x
​    8进制在数字前加0
​        在某些浏览器中键入以下代码：
​            var a = "070";
​            console.log(parseInt(a));
​        结果会输出56。因为浏览器将其当做8进制，解决方法是输入第二个参数，强制以10进制输出
​            parseInt(a, 10);
​    2进制在数字前加0b
​        某些浏览器无法解析2进制如IE浏览器，同时也不常用
## 运算符
​    运算符有以下种类：typeof，+，-，*，/，%，所有的运算符都不改变原始变量而是返回进行运算后的结果,并且NaN与任何值进行运算结果都为NaN
​        typeof:
​            typeof返回一个变量或者字面量的类型，返回值为string
​            var a = typeof 2;
​            console.log(a);
​            console.log(typeof a);
​            结果为：number与string
​        +：
​            数字的加法运算
​            遇到非number的值，会将其转换成number
​            遇到string的值，会转换成string然后进行接串操作，可应用于长字符串的换行与隐性string类型转换
​        其余运算符进行相应数学运算并且在遇到非number值时，会全部转换成number值后再进行运算操作，此特性可用于隐式number类型转换，但还有更简单的方法
​            var a = "123";
​            console.log(a / 1);
​            console.log(typeof (a / 1));
​            结果为123和number类型

一元运算符
    正号+和负号-
        两者能够进行相应的数学运算同时在遇到非number的值时会将其强制转换成number值再进行运算，此特性可用于隐式number类型转换
            var a = "123";
            console.log(+a);
            console.log(typeof +a);
            结果为123和number类型
自增与自减
    ++
        分为前++(++a)和后++(a++)，对于a值来说都是增加1，但是表达式的返回值不同，前++返回新值，后++返回原值
    --
​        特性与自增相同，只是对于a值来说是减少1
逻辑运算符
​    包括!, &&, ||三种运算符
​        !：两次取非会得到原值的布尔值，可以利用这个特性进行隐式布尔值转换
​            var a = "123";
​            console.log("a = " + !!a);
​            结果为true，与Boolean(a)相同
​        &&：两个值都为true结果才为true
​        ||：两个值都为false结果才为false
​    在JS中&&与||都是属于短路操作，即当一个值满足要求时才会继续执行第二个操作，第一个值不满足要求时不执行第二个操作
​    当参数不是boolean值时先会将参数转换成boolean值后再按照以上规则输出原值
​        &&：
​            当第一个值为true时，返回第二个值
​            当第一个值为false时，返回第一个值
​            console.log("123" && "456");
​            结果为"456"
​            console.log(NaN && "111");
​            结果为NaN
​        ||：
​            当第一个值为false时，返回第二个值
​            当第一个值为true时，返回第一个值
​            console.log(NaN || "111");
​            结果为"111"
​            console.log("123" || "456");
​            结果为"123"
赋值运算符
​    有以下几种：=, +=, -=, /=, *=
​    var a += 3;
​    var a = a + 3;
​    两者等价，对于其他的赋值运算符，与+=规则相同
关系运算符
​    有以下几种：<, >, <=, >=
​    有一方为number值时，将非number值转换成number值再进行比较
​    NaN与任何值进行任何比较结果都为false， 包括NaN本身
​        console.log(NaN >= NaN);
​        结果为false
​    当两方都为string时，按位比较字符编码，因此在两者都为string类型值为数字时进行比较，结果可能不符合预期，可应用于英文名字的排序
​        console.log("11" > "2");
​        结果为false
unicode编码
​    在js中使用时在编码前加\u对编码进行转义输出
​        console.log("\u0031");
​        结果为1，编码为16进制
​    在HTML中使用时以 &#编码; 的格式输出
​        &#0048;
​        结果为1，编码为10进制
相等运算符
​    包括==, !=, ===, !==
​    ==, !=
​        两者类型相同时判断是否相等，类型不同时进行类型转换再判断是否相等，转换成哪种类型无法确定
​        由于undefined衍生于null，因此两者相等
​            console.log(undefined == null);
​            结果为true
​        NaN与任何值进行运算结果都为false，包括自己
​            console.log(NaN == NaN);
​            结果为false
​    ===, !==
​        除不进行类型转换外，规则与==, !==类似
​        当两者类型不同时，===直接返回false，!==直接返回true
​        NaN的规则在此处同样适用
​            console.log(NaN === NaN);
​            结果为false
​        undefined与null在这种运算符下，才会不相等
​            console.log(undefined === null);
​            结果为false
三元运算符
​    语法格式为(表达式)?(语句1):(语句2);
​        当表达式结果为true时执行语句1，否则执行语句2
​        当表达式结果为非boolean值时，会转换成boolean值后再对表达式进行判断
逗号运算符
​    用来分割不同语句，可以同时声明多个变量
运算符优先级
​    按照优先级表进行先后运算，可以使用()改变优先级
代码块
​    将多个语句用{}包含起来，这一堆语句称为代码块，它只具有分组的作用，没有其他用途
​        {
​            var a = 1;
​            console.log("a");
​        }
​            console.log("a");
​        结果为1 /n 1
条件判断语句
​    语法1：满足条件只执行紧接着的第一条语句，后面语句与判断语句无关
​        if(表达式)
​            语句1;
​    语法2：满足条件执行代码块中的代码，代码块外的代码与判断语句无关
​        if(表达式){
​            语句1;
​            语句2;
​        } 
​    语法3：满足条件执行前一个代码块中的代码，否则执行后一个代码块中的代码
​        if(表达式){
​            语句...
​        }else{
​            语句...
​        }
​    语法4：从上到下依次判断，当满足一个表达式后后面的代码不再执行
​        if(表达式){
​            语句...
​        }else if{
​            语句...
​        }else if{
​            语句...
​        }else if{
​            语句...
​        }else{
​            语句...
​        }
​    语法5：条件判断语句可以嵌套
​        if(表达式){
​            语句...
​        }else{
​            语句...
​            if(表达式){
​                语句...
​            }
​        }
条件分支语句
​    语法：
​        switch(表达式){
​            case 值1: 
​                语句...
​                break;
​            case 值2: 
​                语句...
​                break;
​            case 值3: 
​                语句...
​                break;
​            default:
​                语句...
​                break;
​        }
​    break;语句用来跳出switch语句，当没有此语句时，如果表达式的值满足某个case时，后面的语句都会执行
​        var a = 1;
​        switch(a){
​            case 1:
​                console.log("1");
​            case 2:
​                console.log("2");
​            default:
​                console.log("其他");
​        }
​        结果为1, 2, 其他
while循环
​    while语句：
​        语法1：
​            while(true){    //1.将表达式写死
​                if(条件表达式){  //2.当满足某种条件时退出
​                    break;
​                }
​                语句...
​            }
​        语法2：
​            var i = 0;     //1.初始化变量
​            while(i < 10){  //2.当不满足条件时退出循环
​                语句...
​                i++;        //3.更新变量
​            }
​    do{}while()语句：
​        语法：
​            do{
​                语句...
​            }while(表达式)
​        与while语句的唯一不同是，while语句先对表达式进行判断，当不满足条件时不继续执行后面的代码块，而do{}while()语句是先执行do后面的代码块再判断表达式，不满足时不执行第二次
​            var i = 11;
​            while(i <= 10){
​                console.log(i);
​            }
​            结果为无
​            do{
​                console.log(i);
​            }while(i <= 10)
​            结果为11
for循环
​    语法：
​        for(初始化变量; 条件表达式; 更新变量){

        }
    作用与while循环相同，写法也可与while循环语法2相同，只要初始化变量与更新变量分别写在for循环外部与内部
        var a = 0;
        for(; a< 10;){
            a++;
        }
    当for循环表达式不写任何内容时则成为死循环
        for(;;){
    
        }
break和continue
    break; 用来跳出循环或者switch
        用在循环语句时跳出最近的循环，不能跳出if语句
    continue; 用来跳过当前循环，执行下一次循环
        不能跳出if语句
    label：在循环语句的前一行使用label语句用来标识某一个循环
    两者都可增加参数，参数是循环的标识名，可以跳出所指定的循环
    good:
        for(var i=1; i<10; i++){
            console.log(i);
            for(var j=1; j<10; j++){
                break good;       
            }
        }
        结果只有一个1
    bad:
        for(var i=1; i<10; i++){
            console.log(i);
            for(var j=1; j<10; j++){
                if(i==2){
                    continue bad;       
                }
            }
        }
        结果为1,3,4,5,6,7,8,9
优化程序效率
    可以考虑在循环语句中增加break;来提高程序运行效率
    使用console.time("字符串标志");来标记一个计时器
    使用console.timeEnd("字符串标志");来结束某个计时器并打印出计时器经过的时间
    console.time("a");
    console.timeEnd("a");
    结果是名为a的计时器经过的时间，单位是ms，只能用在浏览器中
对象
    对象属于复合数据类型，有三种，分别是：
        1.内建对象
            由ES标准中内建的对象，在任何的ES实现中都可以使用，如Math, String, Boolean, Number, Function, Object...
        2.宿主对象
            由js运行的环境所提供的对象，一般指浏览器，如DOM, BOM...
        3.自定义对象
            由开发人员自定义的对象
    创建对象
        var obj = new Object();
        new所调用的函数是一个构造函数constructor()，构造函数是专门用来创建对象的函数
    使用typeof语句会返回object
    增加属性
        语法：
            对象.属性名 = 属性值;
            obj.name = "111";
        属性名可以不遵循标识符的规范，不遵循规范时需要其他方式来增删查改，但是一般尽量遵守规范，属性值可以是任何数据类型，包括null,undefined,object，当是object时可以无限嵌套
            var obj2 = new Object();
            obj2.name = "333";
            obj.test = obj2;
    修改属性
        语法：
            对象.属性名 = 属性值;
            obj.name = "222";
        与增加属性方法类似，只是将已有值覆盖
    查询属性
        语法：
            对象.属性名
            console.log(obj.name);
            结果为222
        当对象的属性为另一个对象时.重复使用来获取对象的对象的属性值
            console.log(obj.test.name);
            结果为"333"
    删除属性
        语法：
            delete 对象.属性
            delete obj.name;
            console.log(obj.name);
            结果为undefined
        当查询对象的某个属性不存在时，会返回undefined
    当属性名没有遵循标识符规范时需要使用[]来增删查改相应属性，属性名可以是变量或者字符串
        语法：
            对象[属性名] = 属性值;
            obj["123"] = 345;  //字符串
            var test = "123";
            console.log(obj[test]);  //变量
            结果为345
    in语句
        用来查询某个对象是否有相应属性名,属性名必须是字符串或者是变量，有则返回true，没有返回false
        语法：
            属性名 in 对象;
            console.log("123" in obj);
            结果为true
基本和引用数据类型
    在js中，内存分为栈内存和堆内存，因为基本数据大小一般比较小，js专门将这些数据存放在固定的内存范围内即栈内存来保存变量与变量值，而引用数据大小一般较大，js需要创建新内存空间即堆内存来保存对象的内容
    当声明变量时，会在栈内存最下层中新建一个变量
    取值时按照声明顺序取值
    当调用new新建对象时会在堆内存中创建新的内存空间来新建一个对象
    由于新建的内存地址不确定，取对象时需要用相应内存地址取用相应的对象
    给变量赋值为基本数据类型时，会直接修改栈内存中变量对应的变量值为相应的变量值
    给变量赋值为引用数据类型时，会直接修改栈内存中变量对应的变量值为内存地址
    两个变量的内存地址指向同一个对象时，修改一个变量的对象的值，另一个变量的对象的值也会发生改变
        var obj1 = new Object();
        obj.name = "111";
        var a = obj1,b = obj1;
        a.name = "222";
        console.log(b.name);
        结果为222
对象字面量
    可以使用对象字面量来新建对象，效果与new Object()相同
    语法：
        {属性名: 属性值, 属性名: 属性值...};
        var obj = {name: "a", age: "16", gender: "男"};
    属性名可以使用引号包起来，但是一般不使用，当属性名不遵循标识符规范时，需要使用引号包起来，最后一个属性写完后不加逗号
函数
    函数也是对象，它具有普通对象具有的所有功能
    声明函数：
        新建函数对象：
            语法：
                var func = new Function("需要执行的代码块");
                在构造函数中可以加入字符串参数代码使得调用函数时可以直接执行
                var func = new Function("console.log(111)");
                func();
                结果为111
        函数声明：
            语法：
                function func([形参1,形参2, 形参3...]){
                    语句...
                }
        函数表达式:
            语法：
                var func = function([形参1,形参2, 形参3...]){
                    语句...
                }
形参与实参
    声明函数时传递的参数叫形参，作用相当于在函数内部声明变量
    调用函数时传递的参数叫实参，作用相当于给函数的形参赋值
    当实参数量大于形参时，多出来的实参会被忽略
    当实参数量小于形参时，未赋值的形参会是undefined类型
    实参可以是任意数据类型包括对象与函数，当实参数量过多时，可以考虑将部分实参封装成一个对象传入
    将函数当做实参传入另一个函数：
        function func1(){
            console.log("a");
            return "1";
        }
        function func2(a){
            console.log(a);
        }
        func2(func1);       //结果为func1对象本身，结果为func1函数的内容
        func2(func1());     //结果为func1的函数返回值,结果为1
返回值
    使用return语句可以让函数返回特定的值，此时函数中return后面跟的所有语句都不执行
    语法：
        return [返回值];

        function test(a, b){
            return a+b;
        }
        var result = test(1, 2);
        console.log(result);
        结果为3
    当return后不加参数时，相当于函数返回undefined
    函数中不使用return时，也相当于返回undefined
    返回值可以是任意类型，包括对象和函数
        function func1(){
            function func2(){
                console.log("func2");
            }
            return func2;
        }
        var a = func1();
        console.log(a);
        结果为func2函数本身的内容
        console.log(a());       //与console.log(func1()());相同
        结果为"func2"
立即执行函数
    语法：
        (function([形参1, 形参2...]){
            语句...
        })([实参1, 实参2...])
    当写成以下形式时，js会将前半部分当成代码块，无法识别函数声明
        function([形参1, 形参2...]){
            语句...
        }([实参1, 实参2...])
方法
    由于对象的属性可以是任何值，因此也可以将一个函数赋值给一个对象的属性，此时这个函数属性就被叫做方法，需要注意的是，函数与方法只是名称上的不同，其他没有任何区别
        var obj = new Object();
        obj.name = "111";
        obj.callName = function(){
            console.log(obj.name);
        }
        obj.callName();
        结果为"111"
    调用对象中的函数，被称为调用这个对象的方法
枚举语句
    语法：
        for(var 声明变量 in 对象){
            语句...
        }
        for(var i in obj){
            console.log(i);     //i为obj对象的属性名
            console.log(obj[i]);        //obj[i]为obj对象的属性值
        }
    对象中有多少个属性，这个循环便会执行多少次
作用域
    全局作用域
        直接写在script标签中的代码都属于全局作用域，它在打开页面时创建，在关闭页面时销毁
        全局作用域中所有的变量可以在页面的任意部分被访问到
            var a = 1;
            function func1(){
                console.log(a);
            }
            结果为1
        全局作用域中所有声明的变量都会被创建成window对象的属性
            var a = 1;
            console.log(window.a);
            结果为1
        变量的提前声明
            当使用var来声明或者声明并赋值变量时，无论声明位置在何处，声明本身这个语句会在当前script标签中的最顶端被执行
                console.log(a);
                var a = 1;
                结果为undefined而不是报错，因为var a;这条语句已经在代码最顶端被执行过了
                console.log(a);
                a = 1;
                报错，a未被声明
        函数的提前声明
            无论函数在何处被声明，函数声明本身会在任何代码前被执行
                func1();
                function func1(){
                    console.log("1");
                }
                结果为"1"
            但是对于函数表达式来说，由于使用var来声明函数，因此只符合变量提前声明的特性
                func1();
                var func1 = function(){
                    console.log("1");
                }
                结果报错，undefined不是一个函数
    函数作用域
        函数作用域在函数执行时创建，在执行完毕后销毁，在函数作用域内部与全局作用域相似
        当在函数中使用变量时会先向当前作用域查找，没有则向上一级作用域查找，直到全局作用域，如果全局作用域中没有此变量时报错
            var a = 1;
            function func1(){
                function func2(){
                    console.log(a);
                }
                func2();
            }
            func1();
            结果为1
        在函数作用域中可以访问到全局作用域的变量，反之不成立
            function func1(){
                var a = 1;
            }
            console.log(a);
            结果为报错，a未定义
        在函数作用域中变量声明提前与函数声明提前同样适用（当函数有形参时相当于在函数内部声明了变量）
            function func1(){
                console.log(a);
                var a = 1;
            }
            func1();
            结果为undefined
            function func1(){
                var a = 1;
                func2();
                function func2(){
                    console.log(a);
                }
            }
            结果为1
this
    当调用函数时，解析器会隐式传入一个参数this，它是一个对象
    1.当以函数的形式调用时，this永远是全局作用域window
    2.当以对象的方法调用时，this是调用这个方法的对象
    3.当以构造函数调用时，this就是新创建的对象
    作用：
        var name = 1, obj1 = {name: 2, sayName: func}, obj2 = {name:3, sayName: func};
        func(){
            console.log(this.name);
        }
        func();
        obj1.sayName();
        obj2.sayName();
        结果为1, 2, 3
        可以使用this来使方法/函数内的值发生变化
创建对象
    有几种方法被用来方便地创建对象
    instanceof语句来输出对象的类名
    工厂方法：
        function createPerson(name, age){
            var obj = new Object();
            obj.name = name;
            obj.age = age;
            retrun obj;
        }
        function createDog(name, age){
            var obj = new Object();
            obj.name = name;
            obj.age = age;
            retrun obj;
        }
        var person = createPerson("aaa", 16);
        var dog = createDog("bbb", 18);
        console.log(instanceof person);
        console.log(instanceof dog);
        结果都为Object
        缺点：无法得知所创建的是一个什么对象，所以出现了构造函数来解决这个问题
    构造函数：
        function Person(name, age){
            this.name = name;
            this.age = age;
            this.sayName = function(){
                console.log(this.name);
            }
        }
        function Dog(name, age){
            this.name = name;
            this.age = age;
            this.sayName = function(){
                console.log(this.name);
            }
        }
        var person1 = new Person("aaa", 16);
        var person1 = new Person("ccc", 14);
        var dog = new Dog("bbb", 18);
        console.log(instanceof person1);
        console.log(instanceof dog);
        结果分别为Person， Dog
        构造函数与普通函数在使用上的区别就是是否使用了new，构造函数又被称为类，对类作new操作等到的结果被称为实例
        构造函数的执行流程：
            1.立即新建1个对象
            2.将构造函数的this值赋值为新创建的对象
            3.依次执行构造函数内的代码
            4.将新建的对象返回
        构造函数改进:
            按照上述代码编写会在给对象创建方法时重复创建函数，当实例化类次数增加时会浪费大量内存，因此需要将重复创建的方法函数变成只创建一次
                console.log(person1.sayName == person2.sayName);
                结果为false，证明的确重复创建了函数
            可以将方法声明在全局作用域中
                function Person(name, age){
                    this.name = name;
                    this.age = age;
                    this.sayName = func;
                }
                function func(){
                    console.log(this.name);
                }
                var person1 = new Person("aaa", 16);
                var person2 = new Person("bbb", 18);
                console.log(person1.sayName == person2.sayName);
                结果为true,证明是同一个函数
            但是这种办法会污染全局命名空间并且不够安全，有可能会被其他函数覆盖
    原型对象：
        每一个类都可以有一个原型对象prototype，它是一个对象，并且这个类的实例会有一个原型属性__proto__，它的值是这个实例的类的原型对象地址
        因此修改类的原型对象的属性也会改变这个类的实例的原型属性所指向的那个原型对象
        可以利用原型的特性为类开辟出一个新的公共空间让这个类的每一个实例都可以使用这个公共空间的值或者方法而不会污染全局命名空间
            function Person(name, age){
                this.name = name;
                this.age = age;
            }
            Person.prototype = function(){
                console.log(this.name);
            }
            var person1 = new Person("a",12);
            console.log(person1.__proto__ == Person.prototype);
            结果为true
        所有对象都有原型属性__proto__，由于原型对象也是对象，因此也具有原型属性__proto__
            console.log(Person.prototype.__proto__);
            结果为object
        Object的实例的原型没有原型
            var a = new Object();
            console.log(a.__proto__.__proto__);
            结果为null
        所有对象都是Object对象的实例，包括原型对象，因此原型的回溯最多到Object实例的原型为止，也就是原型对象的原型为止
        实例中变量查找顺序：
            1.先在被实例化的类中的变量之间查找，如果找到则输出，否则进入它的原型对象
            2.在类中的原型对象中的变量之间查找，如果找到则输出，否则进入它的原型对象
            3.在原型对象的原型中的变量之间查找，如果找到则输出，否则输出undefined
        使用in语句来查找属性是否属于某个对象时会向它的原型中查找
        如果不想查找原型中的属性，使用hasOwnProperty方法
            function Person(){}
            Person.prototype.a = 1;
            var person = new Person();
            person.b = 1;
            console.log("a" in person);
            console.log(person.hasOwnProperty("a"));
            console.log(person.hasOwnProperty("b"));
            结果为true, false, true
        当在页面中打印一个对象时，实际上输出的是这个对象的valueOf方法的返回值，因此可以通过修改对象的valueOf方法来修改打印对象时的结果
            function Person(name){
                this.name = name;
            }
            Person.prototype.valueOf = function(){
                return "name = " + this.name;
            };
            var person = new Person("a");
            console.log(person);
            结果为name = "a"        //根据实际测试，结果与浏览器相关
        当将对象强制转换成数字时会首先调用valueOf方法，当此方法返回自己时再调用toString
        当对象强制转换成字符串时只调用toString方法
## 垃圾回收
    当创建对象之后对所有这个对象的变量赋值为null时，这个对象就永远无法被操作，这个对象就称为垃圾
    js拥有自动的垃圾回收机制，不需要也不能手动地回收垃圾，能做的只有将不再使用的对象赋值为null
##数组
    数组也是一个对象，与对象的区别在于数组只能通过索引来查找值，并且存储效率要比普通对象更高，所以具有所有对象具有的特性
    创建数组
        var arr = new Array();
    arr具有三个对象属性，constructor(构造函数的引用), length(数组长度), prototype(原型对象的引用)
    可以使用：
        数组[数组.length] = 值;
    来方便地向数组最后一位添加内容
    可以通过修改数组长度来删除一些数据
        arr[0] = 0;
        arr[1] = 1;
        arr[2] = 2;
        arr[3] = 3;
        arr.length = 3;
        console.log(arr[3]);
        结果为undefined
    当访问数组中不存在的数据时，会返回undefined而不是报错
    可以使用数组字面量方便地创建数组
        语法：[]
        var arr = [];
    在数组字面量中可以直接加入参数来给数组赋值
        var arr = [0, 1, 2, 3];
        console.log(arr);
        结果为0,1,2,3
    同样也能向数组类添加参数来直接给数组赋值
        var arr1 = new Array(0, 1, 2, 3);
        console.log(arr1);
        结果为0,1,2,3
    但是当参数只有一个时，结果会有所不同
        var arr = [10];         //创建一个第一个值为10的数组
        var arr1 = new Array(10);       //创建一个长度为10的数组
        console.log(arr);
        console.log(arr1);
        结果分别为10和,,,,,,,,,
数组常用方法
    1.push
        向数组最后添加一个或多个元素并将数组长度返回
    2.pop
        删除数组最后一个元素并将该元素返回
    3.unshift
        向数组开头添加一个或多个元素并将数组长度返回
    4.shift
        删除数组开头的元素并将该元素返回
    5.forEach
        按顺序遍历整个数组
        支持IE8以上或者其他的浏览器
        由自己创建但不由自己调用的函数称为回调函数
        语法：
            数组.forEach(function(value, index, arr){

            });
        
        它会在回调函数中以实参的形式传递3个参数：
        1.当前循环中的元素
        2.当前循环中的索引
        3.调用forEach函数的数组
    6.slice
        从一个数组中截取特定范围的元素并将这些元素以数组的形式返回，不改变原数组
        语法：
            数组.slice(start, end);
        第一个参数是截取开始的索引，返回数组会包括开始索引的元素
        第二个参数是截取结束的索引，返回数组不会包括结束索引的元素
            var arr = [0,1,2,3,4,5];
            var arr1 = arr.slice(0,4);
            console.log(arr1);
            结果为0,1,2,3
        参数可以是负值，如果为负就是从后往前计数
            var arr = [0,1,2,3,4,5];
            var arr1 = arr.slice(-3,-1);
            console.log(arr1);
            结果为3,4
    7.splice
        删除或者添加元素，直接改变原数组,返回值为删除的元素
        语法：
            数组.splice(start, number[,元素1, 元素2...]);
        第一个参数为从哪个索引开始删除元素
        第二个参数为删除几个元素
        从第三个参数开始的参数都是是在第一个参数的索引之前添加这些元素
            var arr = [0,1,2,3,4,5];
            arr.splice(0,1,7,8,9);
            console.log(arr);
            结果为7,8,9,1,2,3,4,5
    8.concat
        可以将两个或者多个数组连接成一个数组
        不会改变原数组
        语法：
            数组.concat(任意数据类型[，任意数据类型...]);
            var arr = [1,2,3,4];
            var result = arr.concat([5,6,7,8],1,"a", false, null, undefined, {});
            console.log(result);
            结果为1,2,3,4,5,6,7,8,1,"a",false,null,undefined,{}
    9.join
        将数组中的元素转换成字符串，可以添加参数指定元素之间的连接符，无参数时默认为逗号,
        不会改变原数组
        语法：
            数组.join([字符串])；
            var arr = [1,2,3,4];
            var result = arr.join(" ");
            console.log(result);
            结果为"1 2 3 4"
    10.reverse
        调换数组中元素的排列顺序
        会修改原数组，并且修改后的数组与返回值相同
        语法：
            数组.reverse();
            var arr = [1,2,3,4];
            var result = arr.reverse()
            console.log(result);
            console.log(arr);
            结果都为4,3,2,1
    11.sort
        给数组中的元素排序，默认以unicode编码顺序排列，因此直接对数组中的数字排序会产生预料外的结果
        可以传递一个回调函数作为sort的参数，回调函数中有两个形参分别表示数组中一前一后的两个元素，具体是哪两个元素需要根据循环确认
        函数的返回值决定是否交换这个两个元素，当返回值大于0时交换，小于0时不交换，等于0时认为两个值相等不交换
        会直接修改原数组的元素，与方法的返回值相同
        语法：
            数组.sort([回调函数]);
            var arr = [5,3,6,767,34,2];
            arr.sort();
            console.log(arr);
            结果为2,3,34,5,6,767
            arr.sort(function(a, b){
                return a-b;
            });
            console.log(arr);
            结果为2,3,5,6,34,767
## call和apply
​    函数对象都具有这两个方法，可以向这两个方法中的第一个参数传入一个对象用来修改这个方法的this对象
​    如果函数对象需要形参
​        call方法中第二个参数开始依次输入要传递给函数对象的实参
​        将需要传递的实参封装成一个数组作为apply的第二个参数将实参传递给函数对象
​    语法：
​        函数.call(对象[,参数1...]);
​        函数.apply(对象[,数组]);
​        var obj = {};
​        function a(a){
​            console.log("a = " + a);
​            console.log(this);
​        }
​        a(1);
​        a.call(obj, 1);
​        a.apply(obj, [1]);
​        结果为
​            window,1
​            object,1
​            object,1
arguments
​    在调用函数时，浏览器还会隐式传递一个参数arguments，它是一个类数组对象，不是数组对象
​    使用索引来查询调用函数时传入的参数
​    拥有length属性来表示传入参数的数量
​    拥有callee属性表示当前指向的函数引用，可以用来编写递归函数
​        function a(){
​            console.log(arguments.length);
​            console.log(arguments[0]);
​            console.log(arguments[1]);
​            console.log(arguments.callee);
​        }
​        a(1,2);
​        结果为2,1,2,a函数本身
global对象
​    ECMAScript中非常特别的对象，理论上存在但是又无法获取. 
​    不属于其他任何对象的属性或者对象都是这个对象的属性和方法
​    也就是说所有在全局作用域中定义的属性与对象可以说都是这个对象的属性和方法
​    ECMAScript没有指出如何访问global对象，但是浏览器会将这个对象当作window的一部分加以实现
​    常用方法：
​        1.encodeURL() 用来将整个url编码成浏览器能够识别的字符串，即将一些特殊字符进行编码，如：空格->%20，url中合法特殊字符不会被编码
​        2.encodeURLComponent() 用来将某一段url编码成浏览器能够识别的字符串，url中合法特殊字符也会被编码
​        3.decodeURL()   encodeURL的反向操作，规则与之相同
​        4.decodeURLComponent()  encodeURLComponent的反向操作，规则与之相同
Date对象
​    用来操作与时间有关的对象
​    var date = new Date();      //实例化Date对象的值就是执行这行代码时的时间
​    var date = new Date("12/11/2016 0:0:0");  //当输入参数时以参数对应的含义输出时间，按照mm/dd/yyyy h:m:s的格式输入
​    常用方法：
​        1.getDate() 获取时间的日
​        2.getDay()  获取时间的星期，值为0-6，从周日计算
​        3.getMonth() 获取时间的月份，值为0-11，从1月计算
​        4.getFullYear() 获取时间的年份
​        5.getTime() 获取时间的时间戳，为格林尼治标准时间1970/1/1 0:0:0开始到特定世界为止经过的毫秒
​    Date.now();     //执行这行代码时的时间戳，可用来计算一段代码的性能
Math对象
​    Math对象与其他内建对象不同，它不是构造函数而是一个工具类，不需要实例化，直接使用
​    语法：
​        Math.方法();
​    常用属性：
​        E 自然对数
​        PI 圆周率
​    常用方法：
​        1.ceil()
​            向上取整
​        2.floor()
​            向下取整
​        3.round()
​            四舍五入
​        4.random()
​            获取0-1之间的随机数
​            当想获取x-y之间的随机数时有公式Math.random()*(y-x)+x
​        5.max()
​            获取多个数中的最大值
​        6.min()
​            获取多个数中的最小值
​        7.sqrt()
​            对某个数开根号
​        8.pow(x, y)
​            求x的y次幂
包装类
​    js提供了3个包装类将3种基本数据类型转换成基本数据类型对象，但是在日常开发中不要使用这种方式，因为在转换后进行比较时会产生预期外的结果
​        1.String
​            将基本数据类型string转换成string对象
​            var str = new String("a");
​            console.log(typeof str);
​            结果为object
​        2.Number
​            将基本数据类型number转换成number对象
​            var num = new Number(1);
​            console.log(typeof num);
​            结果为object
​        3.Boolean
​            将基本数据类型boolean转换成boolean对象
​            var bool = new Boolean(true);
​            console.log(typeof bool);
​            结果为object
​    当对这三种基本数据类型操作包装类中的方法或者属性时，浏览器会临时创建一个基本数据类型对象再调用这些方法，然后再将其转换成基本数据类型
​        var a = 1;
​        a.toString();
​        console.log(typeof a);
​        结果为string
​        //执行这两行代码时不会报错，因为实际在对临时创建的基本数据类型对象进行属性赋值操作，语句执行完毕后临时对象就被销毁，因此第二次执行时结果为undefined
​        a.name = "a";
​        console.log(a.name);
​        结果为undefined     
String对象
​    string的底层是用字符数组进行表示的，因此许多数组可以使用的方法在字符串中同样可以使用
​        var str = "abcdef";
​        console.log(str[0]);
​        结果为"a"
​    常用属性:
​        length
​            表示字符串的长度
​    常用方法：（全都不改变原字符串）
​        1.charAt()
​            返回指定位置的字符，与用索引表示相同
​        2.charCodeAt()
​            返回指定位置的字符unicode编码
​        3.fromCharCode()
​            返回指定unicode编码对应的字符
​        4.concat()
​            连接多个字符串，与使用加号+连接字符串相同
​        5.indexOf()
​            返回指定字符在字符串中第一次出现的索引，当没有时返回-1
​            参数：
​                第一个参数：需要查找的字符
​                第二个参数：从第几个索引开始进行查找
​        6.lastIndexOf()
​            与indexOf相似，但是它返回的是字符在字符串中最后一次出现的索引，没有时返回-1
​            参数：
​                第一个参数：需要查找的字符
​                第二个参数：从第几个索引开始进行查找
​        7.toUpperCase()
​            将所有字符转化成大写
​        8.toLowerCase()
​            将所有字符转化成大写
​        9.slice()
​            截取指定范围内的字符串，与数组中的slice相似
​            参数：
​                第一个参数：索引开始处，包括这个索引
​                第二个参数：索引结束处，不包括这个索引
​            参数可以是负数，当为负数时从字符串后往前数
​            不输入第二个参数时，截取第一个参数开始至后面全部的字符串
​                var str = "abcdef";
​                var result = str.slice(0,-2);
​                console.log(result);
​            结果为"abcd"
​        10.subString()
​            与slice相似，不同在于参数为负数时默认输入是0，当第一个参数大于第二个参数时会交换两个参数的位置
​                var str = "abcdef";
​                var result = str.subString(1, -3);
​                结果为"a"
​        11.subStr()
​            同样为截取一段字符串，与前两个方法的区别在于参数不同，这个方法不是ES标准，不推荐使用
​                参数：
​                第一个参数：索引开始处，包括这个索引
​                第二个参数：需要截取的字符数量
​        12.split()
​            与数组的join方法相反。将字符串以特定方式转换成数组
​                参数：
​                第一个参数：将字符串以哪个字符进行拆分充当新数组的元素
​                    var str = "abtcdtef";
​                    var result = str.split("t");
​                    console.log(result);
​                    结果为ab,cd,ef
​                当参数为空串时，将每个字符都拆分成一个元素存入新数组
​                第二个参数：决定返回的数组长度
​    正则运算相关的方法：
正则表达式对象
​    用来匹配字符串是否满足要求       
​    语法：
​        var reg = new RegExp("正则表达式", "匹配模式");
​        匹配模式可以是
​        "i" ----忽略大小写
​        "g" ----全局匹配
​    方法：    
​        1.test()
​            测试指定字符串是否满足正则的匹配要求，满足返回true，否则返回false
​    正则表达式字面量
​        语法：
​            var reg = /正则表达式/匹配模式;
​        使用字面量更方便，使用构造函数更灵活，因为可以使用变量
​    正则表达式语法：
​        1.|
​            表示或 
​            /a|b/.test("ac"); //true
​        2.[]
​            与|含义相同
​            /[ab]/.test("bc"); //true
​        3.[^]   //忽略，有误
​            是否含有除了中括号外的内容
​            /^ab/.test("ab");  //false
        4. .
            表示任意字符
                5.\
            表示转义，将特殊符号转化成字符
                6.*
            表示0个或多个字符
                7.+
            表示1个或多个字符
                8.^
            表示开头的某个字符
                9.$
            表示结尾的某个字符
                10.\w
            表示任意字母数字_
                11.\W
            除了任意字母数字_
                12.\d
            表示任意数字
                13.\D
            除了任意数字
                14.\s
            表示空格
                15.\S
            除了空格
                16.\b
            表示单词分隔符
                17.\B
            除了单词分隔符
                18.{}
            限制字符出现的次数
            /^a{3,5}$/.test("aaaaaa");    //false
                19.()
            将几个字符当做整体
            /^(ab){2,3}$/.test("abababab"); //false
                常用语法：
            [a-z]   小写字母
            [A-Z]   大写字母
            [A-z]   英文字母
            [0-9]   数字
        可以使用正则的字符串方法：
                1.split()
            将字符串以正则表达式作为间断符号拆分成数组
                var str = "1a2s3d4f5g6h7jk8";
                console.log(str.split(/[1-9]/));
                结果为a,s,d,f,g,h,jk
            正则不设置匹配模式为g也会全局拆分
                2.search()
            查询正则表达式中的字符位置，不存在则返回-1，与indexOf相似
                var str = "1a2s3d4f5g6h7jk8";
                console.log(str.search(/[a-z]/));
                结果为0
            正则设置匹配模式为g也不会全局匹配
                3.match()
            返回满足正则表达式匹配的字符
                var str = "1a2s3d4f5g6h7jk8";
                console.log(str.match(/[a-z]/));
                结果为a
            如果需要返回全局匹配的结果需要设置匹配模式为g，返回为数组
                console.log(str.match(/[a-z]/g));
                结果为a,s,d,f,g,h,j,k
                4.replace()
            将正则表达式匹配到的字符串用新字符串代替
            参数：
                第一个参数：需要被替换的原字符串，可以用正则表达式
                第二个参数：需要替换的新字符串，可以是空串
                var str = "1a2s3d4f5g6h7jk8";
                console.log(str.replace(/[a-z]/, "!"));
                结果为"1!2s3d4f5g6h7jk8"
            如果需要返回全局匹配的结果需要设置匹配模式为g
                console.log(str.replace(/[a-z]/g, "!"));
                结果为"1!2!3!4!5!6!7!!8"
## DOM简介
​    DOM全称document object model
​    文档
​        整个HTML文件就是一个文档
​    对象
​        HTML文件中的每个节点都在JS中是一个对象
​    模型
​        JS使用模型来表示各个对象之间的关系
​    JS中有宿主对象document，它是window对象的属性，也就是文档对象本身
​    DOM中的对象又称为节点对象，共有4种节点分别为：
​        每个节点中都拥有三个属性分别是:
​                    nodeName      nodeType     nodeValue
​        文档节点    #document       9               null

        元素节点     标签名          1               null
    
        属性节点      属性名         2               属性值
    
        文本节点      #text         3               文本内容
    常用属性：
        1.body
            该属性封装的是body元素对象的引用
        2.documentElement
            属性值为HTML元素对象
        3.all
            属性值为当前页面中的所有元素节点的数组
            这个属性值本身为undefined，它的typeof值也为undefined
        4.URL
            获取当前页面的url
        5.domain
            获取当前页面的域名部分
        6.referrer
            获取是哪个页面链接跳转到当前页面，没有则返回空字符串
    常用方法：
        语法：
            document.方法();
        1.getElementById()
            通过ID值获取对应的节点
            IE8中不区分大小写
            IE7中会匹配表单元素的name值
        2.getElementsByTagName()
            通过标签名获取一组节点
            返回值是一个HTMLCollection，即使只获取到一个节点时，也封装成HTMLCollection返回
        3.getElementsByName()
            通过name的值获取一组节点
            返回值是一个nodelist，与数组相似，可以使用forEach方法，即使只获取到一个节点时，也封装成nodelist返回
        4.getElementsByClassName()
            通过class属性获取一组节点
            返回值是一个HTMLCollection，即使只获取到一个节点时，也封装成HTMLCollection返回
            仅支持IE8以上
        5.querySlector()
            通过CSS选择器返回一个节点，当能匹配多个节点时，返回满足匹配的第一个节点
            仅支持IE7以上
        6.querySlectorAll()
            通过CSS选择器返回一组节点
            返回值是一个nodelist，与数组相似，可以使用forEach方法，即使只获取到一个节点时，也封装成nodelist返回
            仅支持IE7以上
        HTMLCollection：支持通过索引或者字符串来查找需要的节点，在后台则分别使用它的item()与namedItem()方法来获取
        NodeList: 与HTMLCollection类似的一个node集合，他们的值都是动态的，每次去取这些值的属性都会引发一次文档查询，因此需要尽量减少直接访问
事件
    当用户与浏览器进行任何交互时都会产生相应的事件
    JS可以通过给事件绑定相应函数来使事件触发时执行相应的函数,相应函数会在执行事件时才会被执行，因此相应函数内部使用的变量可能会与预期不一致
        var div = document.getElementByTagName("test");
        for(var i = 0; i < div.length; i++){
            div[i].onclick = function(){
                console.log(i);
            }
        }
        结果永远会是div的长度的值
    绑定事件有两种方法：
        第一种：
            <button id="btn" onclick="alert('a')"></button>
            结构与行为耦合，不使用  
        第二种：
            <button id="btn"></button>
            <script>
                var btn = document.getElementById("btn");
                btn.onclick = function(){
                    alert("a");
                }
            </script>
            常用方式
文档加载顺序
    浏览器加载HTML文件时是自上向下加载，因此当js代码写在文档之前时可能需要无法获取到节点的情况
    使用window.onload绑定响应函数可以使响应函数内的代码都在整个文档加载完成之后执行
    或者将JS代码写在HTML文档的最后来保证文档先于JS代码加载
元素节点
    元素节点拥有一个方法和属性来获取它们内部的节点,除了元素的class属性以外,所有的属性都可以以元素节点对象属性的方式获取,class的值需要用className属性来获取，因为class是js中的保留字
    常用方法：
        1.getElementById()
            通过ID值获取当前元素节点内部对应的节点
        2.getElementsByTagName()
            用来获取当前元素节点内部的特定标签的元素节点
            返回值是一个HTMLCollection，与数组相似，不能使用forEach方法，即使只获取到一个节点时，也封装成HTMLCollection返回
        3.getElementsByName()
            通过name的值获取当前元素节点内部的一组节点
            返回值是一个nodelist，与数组相似，可以使用forEach方法，即使只获取到一个节点时，也封装成nodelist返回
        4.getElementsByClassName()
            通过class属性获取当前元素节点内部的一组节点
            返回值是一个HTMLCollection，与数组相似，不能使用forEach方法，即使只获取到一个节点时，也封装成HTMLCollection返回
            仅支持IE8以上
        5.querySlector()
            通过CSS选择器返回当前元素节点内部的一个节点，当能匹配多个节点时，返回满足匹配的第一个节点
            仅支持IE7以上
        6.querySlectorAll()
            通过CSS选择器返回当前元素节点内部的一组节点
            返回值是一个nodelist，与数组相似，可以使用forEach方法，即使只获取到一个节点时，也封装成nodelist返回
            仅支持IE7以上
        7.hasChildNodes()
            返回当前节点内部是否拥有1个或多个子节点
    常用属性：
        innerHTML
            获取当前元素节点中的HTML代码
        innerText
            获取当前元素节点中的文本
        childNodes
            获取当前元素节点中所有的子节点并以数组形式返回，按照ES标准如果当前元素节点中有空格时也会被包括在内
            IE8及以下浏览器没有实现这一标准，因此只会获取到内部的元素节点
        children
            获取当前元素节点中的所有子元素节点
        firstChild
            获取当前元素节点中的第一个子节点
        firstElementChild
            获取当前元素节点中的第一个子元素节点, 仅支持IE8以上
        lastChild
            获取当前元素节点中的最后一个子节点
        lastElementChild
            获取当前元素节点中的最后一个子元素节点, 仅支持IE8以上
        parentNode
            获取当前元素节点的父节点
        previousSibling
            获取当前元素节点的前一个兄弟节点
        previousElementSibling
            获取当前元素节点的前一个兄弟元素节点, 仅支持IE8以上
        nextSibling
            获取当前元素节点的后一个兄弟节点
        nextElementSibling
            获取当前元素节点的后一个兄弟元素节点, 仅支持IE8以上
    当响应函数给某个节点绑定时，这个响应函数中的this就是这个节点
DOM的增删改
    常用方法：
        1.createElement()
            新建一个元素节点，参数是元素节点的标签名
            语法:
                document.createElement("标签名");
        2.createTextNode()
            新建一个文本节点，参数是文本节点的内容
            语法:
                document.createTextNode("文本内容");
        3.appendChild()
            向一个父节点中添加一个子节点
            语法：
                父节点.appendChild(子节点);
        4.insertBefore()
            向一个子节点前添加一个新的节点
            语法：
                父节点.insertBefore(新节点, 原节点);
        5.removeChild()
            移除一个子节点
            语法：
                父节点.removeChild(子节点);
        6.replaceChild()
            将原节点替换成新节点
            语法：
                父节点.replaceChild(新节点, 原节点);
        7.cloneNode()
            返回值是一个节点的拷贝，接受一个布尔值作为参数，true则为深度拷贝，false为浅拷贝
            语法1：
                节点:cloneNode(boolean)
        8.normalize()
            返回一个经过一定处理后的节点, 这个过程会合并文本节点并删除空白的文本节点
        9.splitText(str)
            返回一个按照参数进行分割的多个文本节点, 此方法只可被用于文本节点
    由于许多方法都要通过父节点调用对应的方法来操作节点，因此可使用：
        子节点.parentNode.removeChild(子节点);
    类似的方法来对节点进行直接操作而不需要获取它的父节点
    对DOM的增删改操作可以用父节点的innerHTML的字符串操作来代替，由于是整体修改所以这个父节点包括它的子节点绑定的函数都会失效
        代码1：
            <html>
                <head>
                </head>
                <body>
                    <div>
                        <input type="checkbox" id="checkallbox"/>AAAAA
                    </div>
                </body>
            </html>
            <script>
            var input = document.createElement("input");
            var checkallbox = document.getElementById("checkallbox");
            input.type="checkbox";
            checkallbox.parentNode.insertBefore(input, checkallbox);
            </script>
        代码2
            <html>
                <head>
                </head>
                <body>
                    <div>
                        <input type="checkbox" id="checkallbox"/>AAAAA
                    </div>
                </body>
            </html>
            <script>
            var div = document.getElementByTagName("div")[0];
            div = "<input type='checkbox'/>" + div.innterHTML;
            </script>
    两部分代码功能基本相同，唯一区别是如果input标签绑定了响应函数，在代码2中会失效
DOM的遍历
    document.createNodeIterator(root, whatToShow, filter, entityReferenceExpansion)
        参数一: 指定开始遍历的根节点，只能遍历body标签中的节点，其他标签会被跳过
        参数二: 标识要访问标签元素的哪些节点，它是一个数字代码，语义化信息保存在NodeFilter类型中
                NodeFilter.SHOW_ALL         显示所有节点
                NodeFilter.SHOW_ELEMENT     显示元素节点
                NodeFilter.SHOW_ATTRIBUTE   显示属性节点
                NodeFilter.SHOW_TEXT        显示文本节点
                NodeFilter.SHOW_DOCUMENT    显示文档节点
                NodeFilter.SHOW_COMMENT     显示注释节点
        参数三: 是一个NodeFilter对象，或者一个返回接受或者拒绝特定标签的函数
                NodeFilter对象是一个只有acceptNode方法的对象，该方法是一个迭代回调函数，有一个node参数，迭代器中有几个节点则会被执行几次
                返回值应是NodeFilter.FILTER_ACCEPT或者NodeFilter.FILTER_SKIP
                通过返回值来判断是否能够访问当前回调函数中的标签元素
                var filter = {
                    acceptNode: function(node){
                        return node.tagName.toLowerCase() == "p" ? NodeFilter.FILTER_ACCEPT : NodeFilter.FILTER_SKIP
                    }
                也可以是一个与acceptNode方法相似的函数
        参数四: 标识是否要扩展实体引用，在html中没有意义
        nodeIterator有两个方法nextNode()与previousNode()来访问迭代器中的节点
        刚创建好的迭代器一开始是指向一个标识根节点的指针，第一次调用nextNode会指向第一个子节点
        当越界时返回值为null
        支持IE9+和其他浏览器
    document.createTreeWalker(root, whatToShow, filter, entityReferenceExpansion)
        可以实现在经过过滤的root节点中任意跳跃，非常灵活
        参数与上一个函数一致，唯一有区别的在于第三个参数的Nodefilter函数增加一个有效的返回值NodeFilter.FILTER_REJECT
        此时迭代器会跳过这个节点及其后代元素而不是像NodeFilter.FILTER_SKIP那样单纯跳过当前节点，仍然进行深度遍历
        在createNodeIterator的第三个参数中返回NodeFilter.FILTER_REJECT作用与NodeFilter.FILTER_SKIP相同
        相较于NodeIterator对象，TreeWalker对象多出一些重要方法:
            parentNode()
            firstChild()
            lastChild()
            nextSibling()
            previousSibling()
        通过这些方法可以实现在TreeWalker对象中任意跳转到目标元素
        W3C标准DOM2，但是IE不支持
DOM范围
    可以通过范围来选择文档中的一个区域而不必考虑节点的界限(选择在后台完成，对用户是不可见的)
    以下属性可以获取到当前范围在文档中的位置信息
        startContainer  
            包含范围起点的节点，即起点的父节点
        startOffset     
            范围起点在startContainer中的偏移量
            如果起点是文本节点，注释节点，cdata节点则值是范围起点节点距离startContainer需要跳过的字符串
            如果起点是元素节点，则值是范围起点节点在startContainer中的子节点索引
        endContainer
            包含范围终点的节点，即终点的父节点
        endOffset
            范围终点在startContainer中的位置
            值计算规则与startOffset相同
        commonAncestorContainer
            起点节点与终点节点共同的最近的那个祖先节点
    通过以下方法可以进行选择范围操作
        selectNode
            选中传入参数的那个节点及内部节点
        selectNodeContents
            选中传入参数的那个节点的内部节点
        setStartBefore(refnode)
            将范围起点设置为refnode之前，refnode就成为了范围选区的第一个节点
            startContainer变成refnode的父节点，startOffset的值变成refnode在父节点中的索引
        setStartAfter(refnode)
            将范围起点设置为refnode之后，refnode就成为了范围选区外的节点，下一个节点是范围选区内第一个节点
            startContainer变成refnode的父节点，startOffset的值变成refnode在父节点中的索引加1
        setEndBefore(refnode)
            将范围终点设置为refnode之前，refnode就成为了范围选区的最后一个节点
            startContainer变成refnode的父节点，startOffset的值变成refnode在父节点中的索引
        setEndAfter(refnode)
            将范围起点设置为refnode之后，refnode就成为了范围选区外的节点，下一个节点是范围选区内第一个节点
            startContainer变成refnode的父节点，startOffset的值变成refnode在父节点中的索引加1
        setStart()
            传入两个参数，第一个参数是参照节点，第二个参数是偏移量
            参照节点会被当做startContainer,偏移量会变成startOffset
        setEnd()
            传入两个参数，第一个参数是参照节点，第二个参数是偏移量
            参照节点会被当做endContainer,偏移量会变成endOffset
    创建范围之后可以使用以下方法对选中内容进行操作
        deleteContents()
            将选中的内容从文档中删除
        extractContents()
            将选中的内容从文档中提取出来并作为返回值返回
        cloneContents()
            拷��一份选中的内容并作为返回值返回
        insertNode()
            将一个节点插入到范围的最开始处
        surroundContents()
            将范围内容插入到这个节点之内
        collapse()
            可以将选中的范围进行折叠，使范围起点与终点都指向同一个位置
            传入一个布尔值作参数，true表示折叠到原范围的起点，false表示折叠到原范围的终点
        compareBoundaryPoints()
            传入两个参数，第一个参数是需要比较哪两个点的一个常量，值可以是Range.START_TO_START,Range.START_TO_END,Range.END_TO_START,Range.END_TO_END
            第二个参数是需要比较的范围，如果调用这个方法的范围与传入的范围的需要比较的点是前者在前则返回-1，相同返回0，前者在后则返回1
        detach()
            在使用完范围后最好使用此方法来使范围从文档中分离，然后再删除引用，方便垃圾回收机制清理
IE8及以下的文本范围
    创建文本范围
        在input，button，textarea，body等几个元素可以使用createTextRange来创建文本节点
    选取文本范围
        findText()
            传入一个字符串参数，如果找到了对应的范围则返回值为true否则为false同时让范围包围这段文本
        moveToElementText()
            传入一个DOM节点，让范围包含这个节点的文本信息与标签信息，与selectNode作用类似
        move()
        moveStart()    
        moveEnd()
        expand()
            这些方法都传入两个参数，第一个参数是移动单位，第二个参数是移动单位的数量
            移动单位可以是以下值
                character：逐个字符移动
                word：逐个单词移动
                sentence： 逐个句子(一系列以叹号问号句号结尾的字符)移动
                textedit：移动到当前选区开始或结束的位置
        move会将范围折叠
        expand会将部分文本的范围变成完整文本的范围
    修改范围内的内容
        有text与pasteHTML()
        前者改变文本，后者可以包括标签
    折叠范围
        与其他浏览器相同使用collapse()来折叠范围
        但是没有collapsed属性来判断是否折叠，但是可以使用boundingWidth属性来判断范围宽度是否为0
    比较范围
        compareEndPoints()
            用法与作用同compareBoundaryPoints类似
            第一个参数是字符串，表示需要比较哪两个点如: StartToEnd等格式
            第二个参数是待比较的范围
    复制范围
        duplicate()
            作用与cloneContents()相同
操作样式
    在css的属性中如果有用-来间接的情况，在style需要使用驼峰命名法来修改属性名从而设置或者读取对应的样式
    1.style
        语法：
            节点对象.style.属性值
        通过这个属性能够修改和读取到节点的内联样式，当节点没有内联样式时获取到的是空字符串
        如果在其他地方的css样式中设置了!important，那么通过js操作这个属性会失效
    2.currentStyle
        此属性只能在IE浏览器中使用并且是只读的，当未给某个节点设置长度值时会返回auto
        语法：
            节点对象.currentStyle.属性值
    3.getComputedStyle()
        此方法是window的方法，可以直接使用，而且也是只读的
        在获取width属性时当未设置具体样式的情况下，会返回节点对象实际呈现的结果而不是auto
        语法：
            getComputedStyle(节点对象, 伪元素（常设置为null）)[样式名]
        此方法支持IE8以上以及其他浏览器
    常用属性：
        1.clientHeight
            获取元素的视图高度，包括元素的内容高度与内边距高度，返回值是一个数字，只读, 在根标签的此属性就是指代视口大小，与此规则无关
        2.clientwidth
            获取元素的视图宽度，包括元素的内容宽度与内边距宽度，返回值是一个数字，只读, 在根标签的此属性就是指代视口大小，与此规则无关
        3.offsetHeight
            获取元素的真实高度，包括元素的内容高度，内边距高度与边框高度，当被父元素隐藏或者滚动时不会影响这个值，返回值是一个数字，只读，在IE11以下浏览器中的根标签的此属性就是指代视口大小，与此规则无关
        4.offsetWidth
            获取元素的真实宽度，包括元素的内容宽度，内边距宽度与边框宽度，当被父元素隐藏或者滚动时不会影响这个值，返回值是一个数字，只读，在IE11以下浏览器中的根标签的此属性就是指代视口大小，与此规则无关
        5.offsetParent
            获取当前元素的定位父元素，即设置了position的最近父元素，当所有父元素都没有设置时，返回body元素, 但是在除了火狐的浏览器中当position设置为fixed，返回null. 
            在IE7包括IE7时，position为absolute与relative时返回html，body与html间的margin清除后可看做body. 在IE7以下时当祖先元素开启hasLayout返回最近开启的元素
        5.offsetTop
            获取当前元素相对于定位父元素的上侧偏移量(相对于offsetParent的内边距)，即使父元素自身有偏移量也不改变这个值的大小，返回值是一个数字，只读
        6.offsetLeft
            获取当前元素相对于定位父元素的左侧偏移量(相对于offsetParent的内边距)，即使父元素自身有偏移量也不改变这个值的大小，返回值是一个数字，只读
        7.scrollHeight
            获取当前元素的真实高度,包括元素的内容高度与内边距高度，当被父元素隐藏或者滚动时不会影响这个值，返回值是一个数字，只读
        8.scrollWidth
            获取当前元素的真实宽度,包括元素的内容宽度与内边距宽度，当被父元素隐藏或者滚动时不会影响这个值，返回值是一个数字，只读
        9.scrollTop
            获取当前元素的右侧滚动条滚动的像素，返回值是一个数字，只读
        10.scrollLeft
            获取当前元素的下侧滚动条滚动的像素，返回值是一个数字，只读
        公式：scrollHeight - scrollTop = clientHeight 可以证明滚动条滚动到最底端
        11. getBoundingClientRect
            基于border-box
            获取一个元素四个角的相对位置与高宽, 在IE7及以下没有width与height属性
            获取绝对位置可以让相对位置加上滚动的像素
事件对象
    当给某个元素对象绑定响应函数后，浏览器在执行这个响应函数后会向这个函数自动传递一个实参，该实参封装了与此事件有关的任何数据
    可以给响应函数添加形参来调用这个事件对象
        var div = document.getElementByTagName("div")[0];
        div.onclick = function(event){
            
        }
    IE8及以下浏览器不会传递此实参，因此会无法获取到
    IE与chrome浏览器也会将这个实参保存在window.event中，可以用来兼容IE8及以下浏览器
        var div = document.getElementByTagName("div")[0];
        div.onclick = function(event){
            event = event || window.event;
        }
    浏览器的滚动条在chrome中被认为是documentElement的scrollTop和scrollLeft的值，而在IE与firefox被认为是body的scrollTop和scrollLeft的值
    因此可以使用：
        var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
        var scrollLeft = document.body.scrollLeft || document.documentElement.scrollLeft;
    来兼容三种浏览器
    常用属性：
        1.clientX
            返回触发此事件时鼠标在视图中的X坐标
        2.clientY
            返回触发此事件时鼠标在视图中的Y坐标
        3.pageX
            返回触发此事件时鼠标在触发此事件的元素中的X坐标，仅支持IE8以上及其他浏览器
        4.pageY
            返回触发此事件时鼠标在触发此事件的元素中的Y坐标，仅支持IE8以上及其他浏览器
    IE浏览器的浏览器默认行为不能使用return false;来阻止某些浏览器默认行为如文字拖拽
    在IE浏览器中可以设置obj.setCapture来让所有的操作都被设置的obj捕获，其他对象就不会执行任何响应函数
    同样可以设置document.releaseCapture来取消事件捕获,这个可以与其他浏览器的在响应函数中return false;一起使用来达到取消浏览器默认行为的作用
    return false与event.returnValue=false作用相同
    对于其他默认行为由于IE不支持event.preventDefault，因此可以使用
        event.preventDefault && event.preventDefault();
        return false;
    来做到兼容所有浏览器
    当事件由addEventListener绑定时，不能使用return false取消默认行为而需要event.preventDefault，对于不支持此方法的IE，使用event.returnValue=false
事件冒泡
    当某个元素的事件触发时，相同的事件会一层层向这个元素的父元素传递，如果不希望这个元素向外进行事件冒泡有两种方法来取消冒泡
    是否传递是根据dom树结构来决定而不是页面上是否包裹，只要是父元素，不管是否与子元素重叠都会将子元素的事件冒泡给父元素
    1.event.cancelBubble=true
        不属于W3C标准，但是更方便，新版本的chrome与firefox都已经支持
    2.event.stopPropogation()
        W3C标准，但是IE不支持
    示例代码：
        <html>
            <head>
                    <style>
                        #outer{
                            width: 500px;
                            height: 500px;
                            padding: 10px;
                            border: 20px solid gray;
                            background-color: blue;
                            position:relative;
                        }
                        #inner{
                            width: 400px;
                            height: 400px;
                            padding: 10px;
                            border: 20px solid rgb(0, 0, 0);
                            background-color: green;
                            position:relative;
                        }
                        #content{
                            width: 300px;
                            height: 300px;
                            padding: 10px;
                            border: 20px solid red;
                            background-color: yellow;
                        }
                    </style>
                    <script>
                        window.onload=function(){
                            var outer = document.getElementById("outer");
                            var inner = document.getElementById("inner");
                            var content = document.getElementById("content");
                            content.onclick = function(event){
                                alert("content");
                            };
                            inner.onclick = function(event){
                                alert("inner");
                                event.cancelBubble = true;
                            };
                            outer.onclick = function(event){
                                alert("outer");
                            };
                        }
                        
                    </script>
            </head>
            <body>
                <div id="outer">
                    <div id="inner">
                        <div id="content">
    
                        </div>
                    </div>
                </div>
            </body>
        </html>
        结果为弹出两个框分别为content与inner
事件委派
    当在给节点添加新节点并且需要让这个新节点与其他兄弟节点有同样的响应函数时可以使用事件委派的功能
    当事件触发时响应函数的形参属性event.target会指定实际触发此函数的节点
    将响应函数绑定到父元素上，并且使用响应函数的形参的属性进行节点判断可以完成新增子节点不需要重新绑定响应函数的功能
    <html>
        <head>
            <script>
                window.onload = function(){
                    var ul = document.getElementByTagName("ul")[0];
                    as[i].onclick = function(event){
                        if(event.target.className == "a"){
                            alert("我是a");
                        }
                    };
                }
            </script>

        </head>
        <body>
            <ul>
            <li><a class="a" href="javascript:;">1</a></li>
            <li><a class="a" href="javascript:;">2</a></li>
            <li><a class="a" href="javascript:;">3</a></li>
            <li><a class="a" href="javascript:;">4</a></li>
            <li><a class="a" href="javascript:;">5</a></li>
            </ul>
        </body>
    </html>
事件绑定
    当对同一个节点的事件重复绑定响应函数时后绑定的函数会覆盖前绑定的函数导致前绑定的函数不会被执行
        a.onclick = function(){
            console.log(1);
        };
        a.onclick = function(){
            console.log(2);
        };
        结果为2
    使用addEventListener来为节点添加监听函数，响应函数可以绑定多次，并且会按顺序执行,支持IE8以上或者其他的浏览器，响应函数内部的this是节点对象
    解绑使用removeEventListener
        参数：
            --事件名，不带on
            --响应函数
            --布尔值，决定事件是否在捕获阶段执行，默认为false，在冒泡阶段执行
        语法：
            对象.addEventListener("", 响应函数, false/true)
    想要兼容IE8及以下浏览器时使用attachEvent，同样可以绑定多次，但是顺序为后绑定先执行，响应函数内部的this是window
    解绑使用detatchEvent
        参数：
            --事件名，带on
            --响应函数
        语法：
            对象.addEventListener("", 响应函数)
    可以定义一个bind函数来兼容两者
        参数：
            --需要绑定响应函数的节点对象
            --事件名，不带on
            --响应函数
        function bind(obj, eventStr, func){
            obj.addEventListener ? obj.addEventListener(eventStr, func) : obj.attachEvent("on" + eventStr, function(){func.call(obj)});
        }
事件传播
    浏览器在实现时对于事件传播微软与网景有不同的理解方式
    --微软认为事件由子元素向父元素传播
    --网景认为事件由父元素向子元素传播
    W3C标准实现时参考两种方法给出了事件执行的阶段：
    --捕获阶段
        事件先从父元素向子元素传递
    --目标阶段
        捕获阶段完成后事件在目标阶段执行
    --冒泡阶段
        然后事件再从子元素向父元素传递
    当需要设置某个事件在捕获阶段执行时，将addEventListener()的第三个参数设置为true即可，IE8及以下浏览器没有实现捕获阶段所以没有办法设置
一些事件
    1.onmousewheel
        当鼠标滚轮滑动时触发此事件，事件结果由event.wheelDelta返回向上滚时返回120，向下滚时返回-120，可以只关注正负，同时不被firefox支持
        想在firefox中监听此事件需要使用addEventListener("DOMMouseScroll", func)来监听鼠标滚轮的操作，事件结果由event.detail返回，向上滚动时返回-3，向下滚动时返回3
        当浏览器中有滚动条时鼠标滚动操作会默认滚动滚动条，在IE与chrome中可以使用return false来取消默认行为，firefox需要使用preventDefault来取消
        obj.onmousewheel = function(event){
            event = event || window.event;
            if(event.wheelDelta > 0 || event.detail <0){
                //向上滚动
            }else{
                //向下滚动
            }
        };
        test.addEventListener && test.addEventListener("DOMMouseScroll", test.onmousewheel, false);
    2.键盘事件
        只有可以获取焦点的事件或者document绑定键盘事件才可以触发
        onkeydown
            当一直按着时，事件会被连续触发，当连续触发的时候，第一次和第二次间隔会稍微长一些后面的才会快速触发，为了防止误操作
            在文本框键入字母属于文本框的默认行为
            事件属性：
             event.altKey
             event.ctrlKey
             event.shiftKey
             当这三个键被按下时它们的值会被赋值为true否则为false
    3.mouseenter    鼠标移入
    4.mouseleave    鼠标移出
    5.mouseover      鼠标移入
    6.mouseout      鼠标移出
    7.contextmenu       上下文菜单事件，可以通过阻止默认行为来自定义上下文菜单
    8.beforeunload     通常在切换页面时触发
    9.DOMContextLoad    在DOM树渲染完成后触发，不管CSS，JS文件是否渲染完毕
    以上四个事件触发机制: 当鼠标移动至绑定监听器的元素或者子元素时就会被触发
    区别: 前两者不会冒泡后两者会
事件模拟
    普通浏览器,还包括IE10及以上
    API:
    document.createEvent(eventname)
        传入一个字符串当做参数，这个字符串在DOM2与DOM3标准中有不同的形式，DOM3中将复数变成单数，建议不要再使用DOM2的标准
            1. UIEvents 一般化的UI事件，鼠标与键盘事件都继承自此事件，在DOM3中是UIEvent
            2. MouseEvents 鼠标事件，在DOM3中是MouseEvent
            3. MutationEvents   一般化的DOM变动事件，在DOM3中是MutationEvent
            4. HTMLEvents    一般化的HTML事件，没有对应的DOM3事件
        在DOM2中没有键盘事件，但是在DOM3中实现了KeyboardEvent
        返回值是一个对应的event对象，根据不同的事件子类有不同的初始化方法
        以MouseEvent为例，初始化方法为initMouseEvent，传入参数与事件类型有关，详细内容需要参考mdn文档
        在DOM3中还定义了自定义事件CustomEvent，返回的对象通过initCustomEvent初始化
    element.dispatchEvent(event)
        传入一个事件对象
        用来触发事件对象定义的事件
    IE9及以下
    API:
    document.createEventObject()
        没有参数
        返回值是一个event对象，event的所有属性与方法都需要自定义，没有预设参数
    element.fireEvent(eventname, event)
        第一个参数是事件名，如onclick等
        第二个参数是自定义的event，
BOM
    1.Window
        代表浏览器窗口并且保存浏览器的全局对象
        window.open 当弹窗被浏览器内置工具屏蔽时会返回null，被工具屏蔽会报错
    2.Navigator
        代表浏览器信息
        由于历史原因大部分属性没有意义，只剩下userAgent可以判断浏览器类型
            /chrome/i.test(navigator.userAgent)
            /firefox/i.test(navigator.userAgent)
        IE11的userAgent中没有IE信息必须使用"ActiveXObject" in window来进行判断
        edge仍然可以使用userAgent来判断有无edge
    3.Location
        代表浏览器地址栏信息
        如果直接打印location，则能获取到当前网址栏的信息
        修改location属性为一个完整路径或相对路径则页面会直接跳转
        --assign()
            直接跳转到某个页面，与直接修改location一样
        --reload()
            用于重新加载当前页面，与刷新按钮一样，传递true作为参数时会强制清空缓存
        --replace()
            与assign类似但是它不会生成历史记录，无法回退
    4.History
        代表历史记录，只能前进后退
        --length
            当次访问的历史次数，关闭浏览器时清零
        --back()
            回到上一个页面
        --forward()
            前往下一个页面
        --go()
            使用整数作为参数来指定需要跳转到的页面
    5.Screen
        代表用户当前屏幕
    这些属性都保存在window中，可以直接使用
定时器
    window.setInterval(func, num)
    返回值为此定时器的标识
    window.clearInterval(定时器标识)
延时调用
    window.setTimeout(func, num)
    经过num毫秒后调用，只调用一次
json
    JSON是一个特定格式的字符串，几乎所有语言都能识别
    能够转换成每个语言的对象，主要用于数据交互
    javascript object notation
    JSON与js对象格式相同但是属性和值必须加引号
    JSON分类：
        对象
        数组
    JSON中可以使用的值：
        数字
        字符串
        布尔值
        null
        对象
        数组
    JSON ---> js对象
    JSON.parse()
        使用JSON对象作为参数，返回js对象
    js对象 ---> JSON
    JSON.stringify()
        使用js对象作为参数，返回JSON
    兼容IE7及以下使用eval来代替不能使用的JSON.parse(),或者引入JSON2库
    eval()
        如果执行的字符串中有{}，则会被当做代码块，如果不希望被当做代码块被解析，在{}前后使用()
        由于效率与安全问题，尽量不要使用
左右查询
    对等号左右两边查询即左右查询，右查询没有找到时会直接报错，左查询没有找到时会在全局创建
表单脚本
    表单对应的是HTMLFormElement类型，继承自HTMLElement，并且有一些额外的属性和方法
        acceptCharset: 服务器能够处理的字符集，等价于HTML中的accpet-charset特性
        action：接受请求的url，等同于表单的action
        elements：表单中所有控件的集合(HTMLCollection)
        enctype: 请求的编码类型，等同于HTML中的enctype
        length：表单中控件的数量
        method：等价于HTML中的方法，通常是get或post
        name：表单的名称
        reset():将所有表单域重置为默认值
        submit():提交表单
        target：用于发送请求和接收相应的窗口名称，等价于HTML中的target
    可以通过常规的DOM操作来获取表单元素，也可以通过document.forms来获取一个页面中所有表单的HTMLCollection
    提交表单
        当表单提交时会触发submit事件
    重置表单
        让表单重置时会触发reset事件，在体验上最好不要主动触发重置事件，会严重影响用户体验，必要时使用回退到上一个页面代替
    表单字段
        可以通过常规的DOM操作来获取表单内控件，也可以使用表单内属性elements返回一个表单控件的集合
        这个集合是一个HTMLFormControlsCollection，它继承自HTMLCollection并重新封装了namedItem方法
        当通过控件的name来访问时，如document.forms[0].elements['color'], 它的返回值是一个NodeList
        也可以通过访问表单的属性来访问，如document.forms[0]['color']，但这是向后兼容的方式，最好不要使用
    表单控件的共有属性
        除了fieldset以外所有表单控件都公用一组属性
            disabled    布尔值，表示当前控件是否被禁用
            form    表示指向当前表单的指针
            name    表示当前控件的名称
            readOnly    布尔值，表示是否只读
            tabIndex    表示tab键切换的序号
            type    表示控件类型，在input中就是type类型，在button中默认是submit，在单选列表中是select-one，在多选列表中是select-mltiple
            value   表示将会提交给服务器的值
    表单控件的共有方法
        每个表单控件都拥有两个方法
            focus   使当前控件获取焦点
            blur    使当前控件失去焦点
        当对隐藏的控件调用这些方法时会抛出错误
    表单控件的共有事件
        除了支持鼠标，键盘，更改，HTML事件外所有控件都支持三个事件
            change  对于input与textarea来说，失去焦点且值改变时触发，对select来说，切换就触发
            blur    与change事件的先后顺序不定，不能提前假定某个事件一定先触发
            focus
文本框脚本
    在表单中有两种文本框text与textarea，两者特性大致上是相同的，但是仍然有些重要的区别
        text可以设置maxlength来指定文本框最大能够输入的字符数量，size指定能够显示的最大字符数量即文本框大小，value指定文本初始值
        textarea的文本初始值只能在<textarea></textarea>之间设定，文本框大小通过rows和cols来设置，不能设置最多能接受的字符数量
    对于这两种文本框都最好使用value值来设定文本内容而不要使用标准DOM方法:
        用setAttribute设置input的value
        获取第一个子节点修改textarea的value
    两个文本框都支持select方法，可以用来全选文本
    相对应的两个文本框都会触发select事件，除了IE8及以下的浏览器会在选中并释放鼠标触发，IE在选中时就触发
    HTML5中还支持部分选中文本的api: setSelectionRange(start, end)接收两个参数表示偏移量
    在IE8及以下想要部分选中需要使用文本范围的技术
    剪切板操作
        clipboardData对象
            在IE中是window属性，其他浏览器中是event的属性并且只有触发剪切板相关事件才能访问
        剪切板事件
            beforecopy
            copy
            beforepaste
            paste
            beforecut
            cut
            其中before相关的事件在IE中只要显示了文本相关的上下文菜单都会被触发，在其他浏览器中是在copy,paste,cut等事件触发前触发
        剪切板方法
            setData()
                第一个参数在普通浏览器中是MIME类型但在IE是text或URL
                第二个参数是想要复制进剪切板的内容
            getData()
                第一个参数在普通浏览器中是MIME类型但在IE是text或URL，但是对普通浏览器使用text也会被识别成text/plain
            clearData()
                清除剪切板中的数据
选择框脚本
    通过select元素创建的是选择框，除了表单字段中列举的属性和方法它还具有以下属性和方法：
        add(new, ref)   向控件中插入new，位置在ref之前
        multiple        布尔值，表示表单是否允许多选
        options         控件中所有option的HTMLCollection
        remove          移除给定位置的选项
        selectedIndex   可读写number，基于0的选中项的索引，没有选中项则为-1，对于支持多选的只保留第一个选中项的索引，被赋值是指定项被选中其他项会取消选中
        size            选择框中可见的行数，与等价于HTML中的size属性
    每个option都有以下属性:
        index           当前选项在option中的索引
        label           当前选项的label
        selected        可读写布尔值，当前选项是否被选中，对单选
        text            文本节点的内容
        value           value值
错误处理机制
    try-catch语句
    finally子语句是可选的，且必定执行，无论catch语句有没有执行
    当有finally存在时，try与catch中的return会失效
    错误类型
        Error
        EvalError
        RangeError
        ReferrenceError
        SyntaxError
        TypeError
        URLError
        其中，Error是基类型，其他错误类型都继承自该类型
        当没有把eval当做函数调用时会抛出EvalError错误
        当超出数组范围或者值不合法时会抛出RangeError
        当对象找不到时会抛出ReferenceError
        当eval中执行的代码有语法错误时会抛出SyntaxError，如果在外部有语法错误会直接停止执行一般不会抛出此错误
        当实际变量类型与预期不一致时会抛出TypeError
        当使用decodeURL和encodeURL中的url格式错误时会抛出URLError
    与try-catch相配的还有throw操作符
        当遇到throw操作符时代码会停止运行，只有当try-catch捕获到时才会继续运行
        抛出错误类型的实例时能够更加真实的模拟浏览器错误
    自定义错误
        通过原型链继承可以自定义错误类型，只要继承自error的对象都会被浏览器当做错误对象处理
        当自定义错误时需要为新错误类型指定name与message
## JSON
    JSON.stringify
        第一个参数是一个JSON对象
        第二个参数是个过滤数组或者函数，函数的两个形参是key, value, 对于每个key，函数返回值就是最终键值对的值
        第三个参数是个数字，表示缩进的空格数
    toJSON
        每个对象都可以创建toJSON方法，在对这个对象使用JSON.stringify会先调用这个方法获取的返回值再对此进行操作
    JSON.stringify的处理流程
        1. 如果第一个参数有toJSON方法就先调用，否则不调用
        2. 将toJSON的返回值或者第一个参数当做下一步的输入值
        3. 如果有第二个参数就用来过滤上一步的输出值，如果没有就将结果当做下一步的输入值
        4. 如果有第三个参数则按照这个值格式化上一步的输出值没有直接将最后的值返回
    JSON.parse
        第一个参数是JSON字符串
        第二个参数是还原函数，有两个形参分别是key跟value，对于每个key，函数返回值就是最终结果的每个键值对中的值


