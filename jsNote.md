# <center>js 笔记</center>

1. 数据类型

	1.1 Number

		不区分整数和浮点,统一用Number表示
		十六进制表示法(只可以表示整数): 以 0x 开始,0-9,a-f表示
		exp:
		运算符: +,-,*,/,%
		其他: NaN 表示 Not a Number 当无法计算时用NaN表示
			Infinity: Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity
		

	1.2 字符串

		以单引号或双引号括起来的任意文本

		转义:
			转义字符\可以转义很多字符，比如\n表示换行，\t表示制表符，字符\本身也要转义，所以\\表示的字符就是\。

			ASCII字符可以用\x##形式的十六进制表示
				exp：'\x41' 完全等同于 'A'
	
			Unicode字符可以用\u####表示
				exp:'\u4e2d\u6587' 完全等同于 '中文'

		多行字符串:
			由于多行字符串用\n写起来比较费事，所以最新的ES6标准新增了一种多行字符串的表示方法，用反引号 ` ... ` 表示：
				exp:`这是一个
				多行
				字符串`;

		模板字符串: '...' (注意为反引号 `)
			普通字符串连接: +
				exp: var name = 'jack';
				var message = '你好,' + name + '!';

			模板字符串: '...' (注意为反引号 `)
				exp: var name = 'jack';
				var message = '你好, ${name}!';

		操作字符串:
			var s = 'jack';
			1. 字符串长度:s.length // 4
			2. 获取字符串指定位置字符:s[2] // c
				字符串不可变性:s[2] = v; s任然为 'jack'
			3. 常用方法
				1. 将字符串全部转为大写: toUpperCase()
				2. 将字符串全部转为小写: toLowerCase()
				3. 搜索指定字符串出现的位置: indexOf()
				4. 返回指定索引区间的子串: substring()

	1.3 布尔值

		值:true 或 false
		运算符: &&(与),||(或),!(非)

	1.4 比较运算符
	
		要特别注意相等运算符==。JavaScript在设计时，有两种比较运算符：
	
		第一种是==比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；

		第二种是===比较，它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较。

		由于JavaScript这个设计缺陷，不要使用==比较，始终坚持使用===比较。
		
		另一个例外是NaN这个特殊的Number与所有其他值都不相等，包括它自己：
		
		NaN === NaN; // false
		唯一能判断NaN的方法是通过isNaN()函数：
		
		isNaN(NaN); // true
		最后要注意浮点数的相等比较：
		
		1 / 3 === (1 - 2 / 3); // false
		这不是JavaScript的设计缺陷。浮点数在运算过程中会产生误差，因为计算机无法精确表示无限循环小数。要比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值：
		
		Math.abs(1 / 3 - (1 - 2 / 3)) < 0.0000001; // true

	1.5 null和undefined

		null表示一个“空”的值，它和0以及空字符串''不同，0是一个数值，''表示长度为0的字符串，而null表示“空”。
		
		在其他语言中，也有类似JavaScript的null的表示，例如Java也用null，Swift用nil，Python用None表示。但是，在JavaScript中，还有一个和null类似的undefined，它表示“未定义”。

	1.6 数组(Array)

		数组是按顺序排列的集合,集合的每个值称为元素.javaScript的数组可以包括任意数据类型.

		创建方法: 
			[1, 2, 3.14, 'Hello', null, true]	
			new Array(1,2,3)

		访问:
			arr[index];(引索超出范围,返回undefined)

		操作:
			var arr = [1,2,'1',true];
			1. 获取Array的长度:arr.length; // 4
			2. 通过引索修改数组:arr[2] = 3; // [1,2,3,true]
				通过 arr.length = 6 或 arr[5] = '你好',都可改变数组长度,结果分别为[1,2,'1',true,undefined,undefined],[1,2,'1',true,undefined,''你好'']
			3. 搜索指定元素位置:indexOf() // 没有元素返回 -1,注意 '1' 与 1 不同
			4. 截取部分元素:slice() // 包含开始,不包含结尾,若参数为空则等于复制数组
			5. 在Array的末尾添加若干元素:push() // arr.push(1,2)
			6. 删除Array最后一个元素:pop() // pop()空数组,返回undefined
			7. 在Array的头部添加若干元素:unshift()
			8. 删除Array的第一个元素:shift()
			9. 排序:sort() //默认升序
			10. 反转数组元素顺序:reverse()
			11. 修改数组:splice(开始引索,删除个数,要添加的元素,要添加的元素,...,要添加的元素) // arr.splice(2,3,'4','5') 从引索2开始,删除3个元素,添加'4','5'到数组arr
				删除的范围超出数组无影响,返回值为被删除元素
			12. 连接两个数组:concat() // 还可以 arr.concat(1,2,[1,2,3])
			13. 按指定字符串将数组中的元素连接:join() //若元素不是字符串类型,则先转为字符串类型

	1.7 对象

		对象:一组由键-值组成的无序集合
			exp:
				var person = {
					name: 'Bob',
					age: 20,
					tags: ['js','web','mobile']
				}
			键:都为字符串类型,又称为对象的属性
			值:任意数据类型

		1. 获取对象:
			对象.属性名 //若属性名包含特殊字符,需要用''括起来
			或 对象['属性名']
				exp:
					person.name 或 person['name']
			访问不存在的属性,返回 undefined

		2. 添加属性:
			对象.属性名 = 值
				exp:person.birth = '1996'

		3. 删除属性:
			delete 对象.属性名
				exp:delete person.birth

		4. 检查对象是否拥有某一属性
			属性 in 对象 // in检查的结果包含继承得到的属性,若只想检查自己本身是否包含指定属性,使用hasOwnProperty()方法
				exp: 'name' in person //注意,必须用单引号''包括属性名

	1.8 变量

		var 变量名 = 值;

		若一个变量没有通过var申明就被使用,那么该变量就自动被申明为全局变量

		strict模式:在strict模式下运行的JavaScript代码，强制通过var申明变量，未使用var申明变量就使用的，将导致运行错误。

		启用:
			在javascript代码的第一行写上:'use strict'
	