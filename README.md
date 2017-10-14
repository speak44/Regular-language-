# Regular-language-
正则初始一

# 正则笔记

## 一、知识点
1.   定义：是检索(模糊范围)字符串的一种规则
	 > 小练
	 > 找到下列字符串中的数字(包括连续的)并且把他们放到一个数组中
	 
    	var str = 'h21kj3hj g443l545 4kklds24gd hs43sd9x5';
		onsole.log(str.match(/\d+/g));
	 > 简写://
	 
	 > 全写:`new RegExp(可以为字符串||正则,字符串)`
	 
	 >  斜杠转义: \
	 >  
	 >  特性:
	 >   > 贪婪: 一直找
	 >   
	 >   > 懒惰: 找到一次之后就不再找了（直接返回）
	 >   


	 
2.  正则方法

	> (1) `//.test(string);`查看正则是否匹配字符串，如果是返回true否则false
	
	>  (2) `string.search()`查找字符串指定字符的位置。找到范围位置，没找到返回-1;  
	
	>  (3) `string.match(//)`把正则匹配到的字符提取出来，放到数组中(返回值为数组),
	> 能匹配到就放在数组中，匹配不到返回null
	
	>  >  **小细节:**
	>  
    >  > 如果只匹配到了一个，那么数组中不只一个东西
    >  
    >  > 但是**length为1
    >  
    >  > 第一个为匹配到的字符
    >  
    >  > 第二个为匹配字符的索引
    >  
    >  > 第三个整个字符串

	>  (4) `string.replace(字符串||正则,字符串||回调函数)`
	>  > 替换匹配的字符串
	>  
	>  > 第一个参数:匹配的字符串
	>  
	>  > 第二个参数:替换的字符串
	>  
	>  > 返回值：替换后的字符串。
	>  
	>  > || 或 |
	>  >  > 小栗子：过滤铭感词汇
	>  
	>  
	>     var s = 'miaov';
	>     console.log(s.replace('m','M'));
	>     var str = '中国共产党总书记习近平说:“法轮功是邪教”';
	>    
	>     var s = str.replace(/共产党|习近平|法轮|邪教/g,function($0,$1,$2,$3){
        	// console.log($3);
       		 var temp = ''; 
        	for(var i=0;i<$0.length;i++){
           		temp += '*';
        	}
        		return temp;
    	});
		 console.log(s);
	>
	>  >  > 小栗子：
	>         
	>     var obj = {
        		name:'小明',
        		age:23,
        		sex:'男'
			}
		var str = '我的名字叫{name},今年{age}岁,性别{sex}';
		str = str.replace(/{(\w+)}/g,function($0,$1){
       		// alert(1);
       		 console.log($1);
        	return obj[$1];
    	});
    	console.log(str);

        
	> **每有一个子项，就对应回调函数中的参数（从第二个参数起）$0永远是本次匹配的整个字符**       
	

3.  转义符:
     >  `\d`  匹配数字
     
	 >  > 小栗子：

	 >      var s = 'abcdhsjadhsadhjsahdjksajdhskdd9';
	 >      console.log(/\d/.test(s));
	 >      //console.log(/x/.test(s));
	 >      
	 >   `\D` 一个非数字
	 >   
	 >   `\w`  一个数字|字母|下划线
	
*  修饰符:
     > `i`  忽略大小写。
     >  > 小栗子：
     >
	 >     var s = 'dshjdsdXak0jkadak';
	 >     // console.log(s.indexOf('x')); 
	 >     // console.log(s.search('x'));
	 >     // console.log(s.search(/\d/));
	 >     // console.log(s.search(/x/i));
	 >     console.log(s.search(new RegExp('x','i')));
	 >
	 > `g` 全局
	 > 
	 > `|` 、 `[]` 或者的意思 
	 > 
	 > `^`如果小尖尖在中括号中，就是排除的意思。
	 > 
	 >  > 小栗子：
	 >   
	 >     var str = 'a1ca22ca3cabcafcayc';
	 >     
	 >     排除a2ca3c
	 >     
	 >     console.log(str.match(/a[^23]c/g));  
	 >     
	 >     排除元素标签方法：var str = txt1.replace(/<[^>]+>/g,'');

	
*  量词:
  
	 >  `+`最小一个最大不限。修饰前面的规则数量
     >  > 小栗子：
     >  
     >     var str = 'dsd5637X2328236jdsdscxdxc37X83kljk54ls3x2xkd4rnej7';
     >     console.log(str.match(/\d+/g));
     >     console.log(str.match(/x+/ig));
     >     console.log(str.match(new RegExp('x+','ig')));
     >     console.log(str.match(/z+/ig));//null
     >   
     >    `?` 要么有1个要么1个都没有   
     >    
*  子项: `()`从左往右去数
*  `()` 提权  例如：(1+1)*5
	> 如果要匹配字符后面有 +号，那么小括号又包着匹配的字符，结果为最后一个字符
	> 
	>  > 小栗子
	>  
	>  > 2017
	>  
	>  > (\d)+   ->  7
	>  
	>  >  (\d)    ->  2
	>  
	>  > 小栗子:
	>  
	>  > `var s = '2017p.--i10_-13';`
	>  
	>  > ((\d+)(\D+)((\d)+)\D+)((\d)+)   7个子项
	>  
	>      $1  2017-.--_10_-
	>      $2  2017
	>      $3  _
	>      $4  10
	>      $5  0
	>      $6  13
	>      $7  3 
	>       
    >     var s = '2017-10-13';
    >         s = s.replace(/(\d+)\D+(\d+)\D+(\d+)\D?/,function($0,$1,$2,$3,$4,$5,$6){
        			return $1 + '年' + $2 + '月' + $3 + '日';
    			});
		console.log(s);
* 正则练习
	>     var str = 'a1ca2ca3ca4ca23caacabcaccadcaAcaBcaZc';
	>     
	>     找到a开头c结尾中间是数字或者中间是字母
	>     console.log(str.match(/a\dc/g));
	>     
	>     console.log(str.match(/a[1-4]c/g));
	>     
	>     console.log(str.match(/a[A-z]c/g));
	>     
	>     console.log(str.match(/a[A-Za-z]c/g));


	>     匹配到数字18-108
	>     
	>      console.log(/1[89]|[2-9][0-9]|10[0-8]/.test('108'));
	>     



