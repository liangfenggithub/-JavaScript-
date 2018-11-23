#基于javascript的正则表达式的练习
## 定义
1. 正则表达式是一个用来描述或者匹配一系列符合某个语法的字符串的语言。
2. 很多工具中，包括编辑器，正则表达式用来被检索、替换和拆分某个模式的文本内容。（对于我来说实用的功能是可以用来删除注释）
3. 许多语言都支持正则表达式 
4. 正则表达式防君子不防小人，用于表单验证只是放置别人大意输错，并不能保证数据绝对安全。
## 2. 创建正则表达式
正则表达式在js中是以对象来存在的，有两种方法可以闯将正则表达式对象。
### 使用对象构造函数创建
var reg = new RegExp("du");
### 使用定界符创建
var reg2 = /com/;//其中 "/" 为反斜线 
### 正则匹配
使用正则表达式对象的test方法来进行匹配，test方法参数为要匹配的值。
### 例子
```javascript
 <script type="text/javascript">
  //1. 通过构造函数创建正则表达式
  var reg = new RegExp("du");

  //2. 通过字面量的方式创建正则表达式
  var reg2 = /com/;//其中 "/" 为反斜线 

  //3. 通过正则规则匹配具体数据
  var str = "www.baidu.com";
  var res = reg.test(str);
  var res2 = reg2.test(str);
  document.write(res+ "<br>");
  document.write(res2);

 </script>
```

## 原子
正则表达式是一种模糊匹配的方式，只要被匹配的字符串有有部分满足条件则匹配成功。使用模糊匹配就用到原子。常用原子如下，小写和大写功能相反。
1. d 匹配数字
2. D 匹配非数字
3. w 匹配字母、数字、下划线
4. W 匹配非数字、非字母、非下划线。
5. s 匹配空白字符：空格、tab、换行
6. S 匹配非空白字符。
### 例子：
```javascript
  //特点：只要被匹配内容中有任何一部分是符合正则要求的，那么就是可以匹配成功的。
  // 1.d 匹配一个数字
  var reg = /\d/; //代表一个数字
  var reg2 = /m\d/ //代表m字母后跟一个数字

  //2. D 匹配一个非数字，与小写功能相反
  var reg3 = /\D/;

  //3. w 任意数字 字母或者下划线
  var reg4 = /\w/;

  //4. W 任意非数字非字母或者非下划线，与小写w相反
  var reg5 = /\W/;

  //5. s 任意空白字符：空格 tab 换行
  var reg6 = /\s/;

  //6. S 任意非空白字符
  var reg7 = /\S/;

  //7. 原子组合使用
  var reg8 = /\d\d\d\w\s/;//匹配四个数字一个字符一个空白字符
  var str2 = "1234a ";


  var str = "www.baidu.com2018";
  var res = reg.test(str);
  var res2 = reg2.test(str);
  var res3 = reg3.test(str);
  var res4 = reg4.test(str);
  var res5 = reg5.test(str);
  var res6 = reg6.test(str);
  var res7 = reg7.test(str);
  var res8 = reg8.test(str2);

  document.write(res + "<br>");
  document.write(res2+ "<br>");
  document.write(res3+ "<br>");
  document.write(res4+ "<br>");
  document.write(res5+ "<br>");
  document.write(res6+ "<br>");
  document.write(res7+ "<br>");
  document.write(res8+ "<br>");
 </script>
```
## 元字符
元字符也是用来模糊匹配的特殊字符，一共有两个：句号和竖线
1. “.” 点用来匹配除换行符外的任意内容，用于匹配单行内的任意内容。
2. “|” 与逻辑或相同，只要一个满足条件就匹配成功。
另外如果要匹配元字符可以使用转移字符反斜线“\”。
  //注意，正则比较死脑筋，没有变通性，比如：在中国贩卖宾度50g以上，就可以判处死刑。这句话是正常的，但是被也会被reg4匹配上，因此一些网站上还配合人工检测。再举个例子：小黄网上找了个对象，其中黄网也被匹配
```javascript
<script type="text/javascript">
  //元字符 有两个 . 和 |
  //1. . 点用来匹配除换行符外的任意内容，用于匹配单行内的任意内容。
  var reg = /./;
  // \ 反斜杠表示转义. 可以使用转义字符匹配真正的字符 
  var reg2 = /\./; //匹配句号
  var reg3 = /\//; //匹配斜线

  //2. | 与逻辑或相同
  var reg4=/违法字符|发票|海洛因|病毒|黄网|黄赌毒/;//用于检测违法字符
  var str2 = "大量出售第三方发票，有意者联系qq1234253234";

  //注意，正则比较死脑筋，没有变通性，比如：在中国贩卖宾度50g以上，就可以判处死刑。这句话是正常的，但是被也会被reg4匹配上，因此一些网站上还配合人工检测。再举个例子：小黄网上找了个对象，其中黄网也被匹配
  //3. 匹配
  var str = 'www.baidu.com';
  var res = reg.test(str);
  var res2 = reg2.test(str);
  var res3 = reg3.test(str);
  var res4 = reg4.test(str2);

  document.write(res + "<br>");
  document.write(res2 + "<br>");
  document.write(res3 + "<br>");
  if(res4){
   document.write("<p>开门，查水表</p>")
  }
  document.write(res4 + "<br>");
 </script>
```
## 原子表
中括号[]表示原子表，原子表只表示匹配一个内容，相当于或|，中括号内可以填写动态范围。具体有以下几中常用方式
1. [张王李] 只要是括号中的任意一个就匹配成功
2. [^张王李] 只要不是括号中的任意一个就匹配成功
3. [0-9] 匹配0-9的数字
4. [a-z] 匹配任意小写字母，同样范围可自定义，比如[a-c]或者[c-f]
5. [A-Z] 匹配任意大写字母，同样范围可自定义
6. [A-Za-z] 匹配任意大小写字母
7. [A-Za-z0-9] 匹配任意大小写字母或者0-9数字
### 例如：
```javascript
 <script type="text/javascript">
  //原子表只表示匹配一个内容相当于或|
  //1. [] 原子表，只要是括号中的任意一个就匹配成功
  var reg = /[张王李]三/;//匹配张三 王三 李三
  var str = "张三是一个人人都会说的名字";

  //2. [^] 原子表，只要不是括号中的任意一个就匹配成功
  var reg2 = /[^张王李]三/; //不匹配张三 王三 李三
  var str2 = "小明是一个人人都会说的名字，一般他是一个三好学生";// 个 三
  
  //3. [0-9] 匹配0-9的数字
  var reg3 = /[0-9]/;//也可以是[3-6],范围自己定义
  var str3 = "我今年27了，一事无成";

  //4. [a-z] 匹配任意小写字母，同样范围可自定义，比如[a-c]或者[c-f]
  var reg4 =/[a-z]/;
  var str4 = "我今年很难过a";
  
  //5. [A-Z] 匹配任意大写字母
  var reg5 = /[A-Z]/;
  var str5 = "我今年很难过C";

  //6. [A-Za-z] 匹配任意大小写字母
  var reg6 = /[A-Za-z]/;
  var str6 = "我今年很难过a";

  //7. [A-Za-z0-9] 匹配任意大小写字母或者0-9数字
  var reg7 = /[a-zA-Z0-9]/;
  var str7 = "人生每天都是这么难，还是只是难这一阵a";

  var res = reg.test(str);
  var res2 = reg2.test(str2);
  var res3 = reg3.test(str3);
  var res4 = reg4.test(str4);
  var res5 = reg5.test(str5);
  var res6 = reg6.test(str6);
  var res7 = reg7.test(str7);
  document.write(res + "<br>");
  document.write(res2 + "<br>");
  document.write(res3 + "<br>");
  document.write(res4 + "<br>");
  document.write(res6 + "<br>");
  document.write(res7 + "<br>");

 </script>
```
## 量词
量词可以用来表示重复多个原子，量词关键词有大括号{}，星号*，问号？和加号+，主要有以下6种：
1. \d{3} 表示前面的原子重复三次，和\d\d\d效果一致，其中\d可以为其他原子。
2. \d{3,} 表示前面的原子最少有三个数字，其中\d可以为其他原子。
3. 原子{3,6} 表示前面有3-6个原子。此原子可以是\d \D \s \S \w \W任意原子，下不赘述
4. 原子* 星号表示0个或者任意个原子，原子同上。
5. 原子？ 问号表示0个或1个，原子同上。
6. 原子+ 加号表示最少一个原子。原子同上。
### 注意
量词,表示在其前面原子的数量，只控制与其紧挨的原子，其余不管
### 示例：
```javascript
<script type="text/javascript">
  
  //花括号{}、星号*，问号？为量词表达式 
  var reg = /余额\d\d\d元/;//假设要匹配到123，可以使用3个\d,但是要匹配100个数字怎么办，这就用到了量词。
  //1. \d{n} 表示匹配n个数字，\d也可以是其他原子
  var reg2 = /余额\d{3}元/;// \d{3}表示\d重复三次，和\d\d\d效果一样
  var str= "您的银行卡余额123元";
  
  //2. \d{n,} 逗号表示 最少 n个数字，\d也可以是其他原子
  var reg3 = /\d{4,}/; //表示匹配最少4个数字
  var str3 = "happy new years 6666";

  //3. \d{n,m} 表示 匹配n-m个原子
  var reg4 = /\d{5,7}/;//匹配5-7个数字，\d也可以是其他原子
  var str4 = "let's go don't cry,even i died. 123456";
   var str44 = "您的银行卡余额150000元";
   var reg44 = /余额\d{5,}/;
   var res44 = reg44.test(str44);
   if(res44 == false){
    alert('你连10000元都没有，还指望别人喜欢你，没钱没有人愿意嫁给你');
   }

   //4. * 表示的数量相当于非洲人的老婆：0个或者任意个
   var reg5 = /\d*/; //表示匹配任意个数字

   //5. ? 表示的数量相当于中国人的老婆，0个或者1个
   var reg6 = /\d?/; //表示匹配0个或者1个数字

   //6. + 表示最少一个
   var reg7 = /\d+/;
   var str7 = "程序员最少有111台电脑";//匹配最少一个数字
   
  var res = reg.test(str);
  var res2 = reg2.test(str);
  var res3 = reg3.test(str3);
  var res4 = reg4.test(str4);
  var res5 = reg5.test(str); //无论是否有数字都行，
  var res6 = reg6.test(str); 
  var res7 = reg7.test(str7); 
  document.write(res+"<br>");
  document.write(res2+"<br>");
  document.write(res3+"<br>");
  document.write(res4+"<br>");
  document.write(res5+"<br>");
  document.write(res6+"<br>");
  document.write(res7+"<br>");

 </script>
```
## 贪婪和吝啬
贪婪：正则在默认匹配的时候默认匹配和返回的是符合条件的最长结果， 
吝啬：在量词后加上问号，就表示默认匹配和返回的是最短的匹配结果
exec：正则对象.exec方法和test相同，都是匹配方法，不过exec返回结果更多。
### 注意
1. 任何量词默认是贪婪的，找最长的匹配结果，
2. 任何量词都可以加上问号，变为吝啬
### 例如：
```javascript
var reg = /ld\d{3,6}/; //贪婪
  var reg2 = /ld\d{3,6}?/; //吝啬
  var str = "hello world12345";//被上述reg匹配到了哪个？是ld123 还是ld1234 还是ld12345？？？
  //exec和test相同都是匹配函数，只是匹配的更加精细。
  var res = reg.exec(str); //返回是一个数组，也就是一个对象。
  var res2 = reg2.exec(str); 
  console.log(res);
  document.write("贪婪匹配中的字符是"+ res[0] + "<br>");
  document.write("贪婪带匹配的源字符是"+ res.input+ "<br>");
  document.write("贪婪是从源字符的第几个开始匹配到的："+ res.index + "<br>");
  document.write("吝啬匹配中的字符是"+ res2[0] + "<br>");
  document.write("吝啬带匹配的源字符是"+ res2.input+ "<br>");
  document.write("吝啬是从源字符的第几个开始匹配到的："+ res2.index + "<br>");

  //例如爬虫，需要匹配到下边字符串中的第一对p标签，那么就需要用到吝啬了
  var str3 = "<p>我是第一个p标签</p><p>第二个标签</p>";
  var reg3 = /<p>.*<\/p>/;//表示任意个(*)任意个（.）字符,
  var reg4 = /<p>.*?<\/p>/;//在量词*后加上？就限制为吝啬，只进行最小匹配，也就是第一对标签
  var res3 = reg3.exec(str3);
  var res4 = reg4.exec(str3);
  document.write("贪婪匹配中的字符是"+ res3[0] + "<br>");
  document.write("吝啬匹配中的字符是"+ res4[0] + "<br>");
```
## 边界匹配
边界匹配就是限定盘匹配条件的开头和结尾，^表示匹配开头，$表示匹配结尾。具体看例子
### 例如
```javascript
  //假设要写一个匹配用户表单中的手机号验证规则
  var reg = /\d{11}/;//表示11位手机号。
  var str = "12312312333";//这个输入可以用reg匹配没问题，但是当输入变为str2时，就不行了，
  var str2 = "我的手机号是12312312333";
  //边界匹配解决以上问题
  var reg2 = /^\d{11}$/;

  var res = reg.test(str);
  var res2 = reg.test(str2);
  var res3 = reg2.test(str2);

  document.write(res+ "<br>");
  document.write(res2+ "<br>");
  document.write(res3+ "<br>");
```
## 常用规则练习
```javascript
//1. 匹配手机号
  var reg = /^1\d{10}$/;//表示从开始到结束只有以1开头的共11位数字
  //2. 匹配身份证号
  var reg2 = /^\d{17}[\dxX]$/;//表示从开始到结束只有18位数字或者17位数字加上x字母

  //3. qq号
  var reg5 = /^[1-9]\d{4,10}$/;//第一位1-9，剩下4-10位数字
 var str = "12345";
  var str2 = "13365612311";
  var str3 = "123456789123455679";

  var res = reg.test(str);
  var res2 = reg.test(str2);
  var res3 = reg2.test(str3);

  document.write(res+ "<br>");
  document.write(res2+ "<br>");
  document.write(res3+ "<br>");
```




## 定义
1. 正则表达式是一个用来描述或者匹配一系列符合某个语法的字符串的语言。
2. 很多工具中，包括编辑器，正则表达式用来被检索、替换和拆分某个模式的文本内容。（对于我来说实用的功能是可以用来删除注释）
3. 许多语言都支持正则表达式 
4. 正则表达式防君子不防小人，用于表单验证只是放置别人大意输错，并不能保证数据绝对安全。
## 2. 创建正则表达式
正则表达式在js中是以对象来存在的，有两种方法可以闯将正则表达式对象。
### 使用对象构造函数创建
var reg = new RegExp("du");
### 使用定界符创建
var reg2 = /com/;//其中 "/" 为反斜线 
### 正则匹配
使用正则表达式对象的test方法来进行匹配，test方法参数为要匹配的值。
### 例子
```javascript
 <script type="text/javascript">
  //1. 通过构造函数创建正则表达式
  var reg = new RegExp("du");

  //2. 通过字面量的方式创建正则表达式
  var reg2 = /com/;//其中 "/" 为反斜线 

  //3. 通过正则规则匹配具体数据
  var str = "www.baidu.com";
  var res = reg.test(str);
  var res2 = reg2.test(str);
  document.write(res+ "<br>");
  document.write(res2);

 </script>
```

## 原子
正则表达式是一种模糊匹配的方式，只要被匹配的字符串有有部分满足条件则匹配成功。使用模糊匹配就用到原子。常用原子如下，小写和大写功能相反。
1. d 匹配数字
2. D 匹配非数字
3. w 匹配字母、数字、下划线
4. W 匹配非数字、非字母、非下划线。
5. s 匹配空白字符：空格、tab、换行
6. S 匹配非空白字符。
### 例子：
```javascript
  //特点：只要被匹配内容中有任何一部分是符合正则要求的，那么就是可以匹配成功的。
  // 1.d 匹配一个数字
  var reg = /\d/; //代表一个数字
  var reg2 = /m\d/ //代表m字母后跟一个数字

  //2. D 匹配一个非数字，与小写功能相反
  var reg3 = /\D/;

  //3. w 任意数字 字母或者下划线
  var reg4 = /\w/;

  //4. W 任意非数字非字母或者非下划线，与小写w相反
  var reg5 = /\W/;

  //5. s 任意空白字符：空格 tab 换行
  var reg6 = /\s/;

  //6. S 任意非空白字符
  var reg7 = /\S/;

  //7. 原子组合使用
  var reg8 = /\d\d\d\w\s/;//匹配四个数字一个字符一个空白字符
  var str2 = "1234a ";


  var str = "www.baidu.com2018";
  var res = reg.test(str);
  var res2 = reg2.test(str);
  var res3 = reg3.test(str);
  var res4 = reg4.test(str);
  var res5 = reg5.test(str);
  var res6 = reg6.test(str);
  var res7 = reg7.test(str);
  var res8 = reg8.test(str2);

  document.write(res + "<br>");
  document.write(res2+ "<br>");
  document.write(res3+ "<br>");
  document.write(res4+ "<br>");
  document.write(res5+ "<br>");
  document.write(res6+ "<br>");
  document.write(res7+ "<br>");
  document.write(res8+ "<br>");
 </script>
```
## 元字符
元字符也是用来模糊匹配的特殊字符，一共有两个：句号和竖线
1. “.” 点用来匹配除换行符外的任意内容，用于匹配单行内的任意内容。
2. “|” 与逻辑或相同，只要一个满足条件就匹配成功。
另外如果要匹配元字符可以使用转移字符反斜线“\”。
  //注意，正则比较死脑筋，没有变通性，比如：在中国贩卖宾度50g以上，就可以判处死刑。这句话是正常的，但是被也会被reg4匹配上，因此一些网站上还配合人工检测。再举个例子：小黄网上找了个对象，其中黄网也被匹配
```javascript
<script type="text/javascript">
  //元字符 有两个 . 和 |
  //1. . 点用来匹配除换行符外的任意内容，用于匹配单行内的任意内容。
  var reg = /./;
  // \ 反斜杠表示转义. 可以使用转义字符匹配真正的字符 
  var reg2 = /\./; //匹配句号
  var reg3 = /\//; //匹配斜线

  //2. | 与逻辑或相同
  var reg4=/违法字符|发票|海洛因|病毒|黄网|黄赌毒/;//用于检测违法字符
  var str2 = "大量出售第三方发票，有意者联系qq1234253234";

  //注意，正则比较死脑筋，没有变通性，比如：在中国贩卖宾度50g以上，就可以判处死刑。这句话是正常的，但是被也会被reg4匹配上，因此一些网站上还配合人工检测。再举个例子：小黄网上找了个对象，其中黄网也被匹配
  //3. 匹配
  var str = 'www.baidu.com';
  var res = reg.test(str);
  var res2 = reg2.test(str);
  var res3 = reg3.test(str);
  var res4 = reg4.test(str2);

  document.write(res + "<br>");
  document.write(res2 + "<br>");
  document.write(res3 + "<br>");
  if(res4){
   document.write("<p>开门，查水表</p>")
  }
  document.write(res4 + "<br>");
 </script>
```
## 原子表
中括号[]表示原子表，原子表只表示匹配一个内容，相当于或|，中括号内可以填写动态范围。具体有以下几中常用方式
1. [张王李] 只要是括号中的任意一个就匹配成功
2. [^张王李] 只要不是括号中的任意一个就匹配成功
3. [0-9] 匹配0-9的数字
4. [a-z] 匹配任意小写字母，同样范围可自定义，比如[a-c]或者[c-f]
5. [A-Z] 匹配任意大写字母，同样范围可自定义
6. [A-Za-z] 匹配任意大小写字母
7. [A-Za-z0-9] 匹配任意大小写字母或者0-9数字
### 例如：
```javascript
 <script type="text/javascript">
  //原子表只表示匹配一个内容相当于或|
  //1. [] 原子表，只要是括号中的任意一个就匹配成功
  var reg = /[张王李]三/;//匹配张三 王三 李三
  var str = "张三是一个人人都会说的名字";

  //2. [^] 原子表，只要不是括号中的任意一个就匹配成功
  var reg2 = /[^张王李]三/; //不匹配张三 王三 李三
  var str2 = "小明是一个人人都会说的名字，一般他是一个三好学生";// 个 三
  
  //3. [0-9] 匹配0-9的数字
  var reg3 = /[0-9]/;//也可以是[3-6],范围自己定义
  var str3 = "我今年27了，一事无成";

  //4. [a-z] 匹配任意小写字母，同样范围可自定义，比如[a-c]或者[c-f]
  var reg4 =/[a-z]/;
  var str4 = "我今年很难过a";
  
  //5. [A-Z] 匹配任意大写字母
  var reg5 = /[A-Z]/;
  var str5 = "我今年很难过C";

  //6. [A-Za-z] 匹配任意大小写字母
  var reg6 = /[A-Za-z]/;
  var str6 = "我今年很难过a";

  //7. [A-Za-z0-9] 匹配任意大小写字母或者0-9数字
  var reg7 = /[a-zA-Z0-9]/;
  var str7 = "人生每天都是这么难，还是只是难这一阵a";

  var res = reg.test(str);
  var res2 = reg2.test(str2);
  var res3 = reg3.test(str3);
  var res4 = reg4.test(str4);
  var res5 = reg5.test(str5);
  var res6 = reg6.test(str6);
  var res7 = reg7.test(str7);
  document.write(res + "<br>");
  document.write(res2 + "<br>");
  document.write(res3 + "<br>");
  document.write(res4 + "<br>");
  document.write(res6 + "<br>");
  document.write(res7 + "<br>");

 </script>
```
## 量词
量词可以用来表示重复多个原子，量词关键词有大括号{}，星号*，问号？和加号+，主要有以下6种：
1. \d{3} 表示前面的原子重复三次，和\d\d\d效果一致，其中\d可以为其他原子。
2. \d{3,} 表示前面的原子最少有三个数字，其中\d可以为其他原子。
3. 原子{3,6} 表示前面有3-6个原子。此原子可以是\d \D \s \S \w \W任意原子，下不赘述
4. 原子* 星号表示0个或者任意个原子，原子同上。
5. 原子？ 问号表示0个或1个，原子同上。
6. 原子+ 加号表示最少一个原子。原子同上。
### 注意
量词,表示在其前面原子的数量，只控制与其紧挨的原子，其余不管
### 示例：
```javascript
<script type="text/javascript">
  
  //花括号{}、星号*，问号？为量词表达式 
  var reg = /余额\d\d\d元/;//假设要匹配到123，可以使用3个\d,但是要匹配100个数字怎么办，这就用到了量词。
  //1. \d{n} 表示匹配n个数字，\d也可以是其他原子
  var reg2 = /余额\d{3}元/;// \d{3}表示\d重复三次，和\d\d\d效果一样
  var str= "您的银行卡余额123元";
  
  //2. \d{n,} 逗号表示 最少 n个数字，\d也可以是其他原子
  var reg3 = /\d{4,}/; //表示匹配最少4个数字
  var str3 = "happy new years 6666";

  //3. \d{n,m} 表示 匹配n-m个原子
  var reg4 = /\d{5,7}/;//匹配5-7个数字，\d也可以是其他原子
  var str4 = "let's go don't cry,even i died. 123456";
   var str44 = "您的银行卡余额150000元";
   var reg44 = /余额\d{5,}/;
   var res44 = reg44.test(str44);
   if(res44 == false){
    alert('你连10000元都没有，还指望别人喜欢你，没钱没有人愿意嫁给你');
   }

   //4. * 表示的数量相当于非洲人的老婆：0个或者任意个
   var reg5 = /\d*/; //表示匹配任意个数字

   //5. ? 表示的数量相当于中国人的老婆，0个或者1个
   var reg6 = /\d?/; //表示匹配0个或者1个数字

   //6. + 表示最少一个
   var reg7 = /\d+/;
   var str7 = "程序员最少有111台电脑";//匹配最少一个数字
   
  var res = reg.test(str);
  var res2 = reg2.test(str);
  var res3 = reg3.test(str3);
  var res4 = reg4.test(str4);
  var res5 = reg5.test(str); //无论是否有数字都行，
  var res6 = reg6.test(str); 
  var res7 = reg7.test(str7); 
  document.write(res+"<br>");
  document.write(res2+"<br>");
  document.write(res3+"<br>");
  document.write(res4+"<br>");
  document.write(res5+"<br>");
  document.write(res6+"<br>");
  document.write(res7+"<br>");

 </script>
```
## 贪婪和吝啬
贪婪：正则在默认匹配的时候默认匹配和返回的是符合条件的最长结果， 
吝啬：在量词后加上问号，就表示默认匹配和返回的是最短的匹配结果
exec：正则对象.exec方法和test相同，都是匹配方法，不过exec返回结果更多。
### 注意
1. 任何量词默认是贪婪的，找最长的匹配结果，
2. 任何量词都可以加上问号，变为吝啬
### 例如：
```javascript
var reg = /ld\d{3,6}/; //贪婪
  var reg2 = /ld\d{3,6}?/; //吝啬
  var str = "hello world12345";//被上述reg匹配到了哪个？是ld123 还是ld1234 还是ld12345？？？
  //exec和test相同都是匹配函数，只是匹配的更加精细。
  var res = reg.exec(str); //返回是一个数组，也就是一个对象。
  var res2 = reg2.exec(str); 
  console.log(res);
  document.write("贪婪匹配中的字符是"+ res[0] + "<br>");
  document.write("贪婪带匹配的源字符是"+ res.input+ "<br>");
  document.write("贪婪是从源字符的第几个开始匹配到的："+ res.index + "<br>");
  document.write("吝啬匹配中的字符是"+ res2[0] + "<br>");
  document.write("吝啬带匹配的源字符是"+ res2.input+ "<br>");
  document.write("吝啬是从源字符的第几个开始匹配到的："+ res2.index + "<br>");

  //例如爬虫，需要匹配到下边字符串中的第一对p标签，那么就需要用到吝啬了
  var str3 = "<p>我是第一个p标签</p><p>第二个标签</p>";
  var reg3 = /<p>.*<\/p>/;//表示任意个(*)任意个（.）字符,
  var reg4 = /<p>.*?<\/p>/;//在量词*后加上？就限制为吝啬，只进行最小匹配，也就是第一对标签
  var res3 = reg3.exec(str3);
  var res4 = reg4.exec(str3);
  document.write("贪婪匹配中的字符是"+ res3[0] + "<br>");
  document.write("吝啬匹配中的字符是"+ res4[0] + "<br>");
```
## 边界匹配
边界匹配就是限定盘匹配条件的开头和结尾，^表示匹配开头，$表示匹配结尾。具体看例子
### 例如
```javascript
  //假设要写一个匹配用户表单中的手机号验证规则
  var reg = /\d{11}/;//表示11位手机号。
  var str = "12312312333";//这个输入可以用reg匹配没问题，但是当输入变为str2时，就不行了，
  var str2 = "我的手机号是12312312333";
  //边界匹配解决以上问题
  var reg2 = /^\d{11}$/;

  var res = reg.test(str);
  var res2 = reg.test(str2);
  var res3 = reg2.test(str2);

  document.write(res+ "<br>");
  document.write(res2+ "<br>");
  document.write(res3+ "<br>");
```
## 常用规则练习
```javascript
//1. 匹配手机号
  var reg = /^1\d{10}$/;//表示从开始到结束只有以1开头的共11位数字
  //2. 匹配身份证号
  var reg2 = /^\d{17}[\dxX]$/;//表示从开始到结束只有18位数字或者17位数字加上x字母

  //3. qq号
  var reg5 = /^[1-9]\d{4,10}$/;//第一位1-9，剩下4-10位数字
 var str = "12345";
  var str2 = "13365612311";
  var str3 = "123456789123455679";

  var res = reg.test(str);
  var res2 = reg.test(str2);
  var res3 = reg2.test(str3);

  document.write(res+ "<br>");
  document.write(res2+ "<br>");
  document.write(res3+ "<br>");
```




