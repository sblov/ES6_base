# ES6

### let、const

#### let

​	没有预解析，不存在变量的提升；在代码块内，只要在let定义变量之前使用，都会报错

​	同一个作用域里，不能重复定义变量

​	对于for循环，for循环里面是父级作用域，里面又有一个子级

```javascript
for(let i=j = 0 ; i <10;i+	+,j++){
 		let i = `Num-`;
        console.log(`${i}${j}`);
 } 
```

#### const:

​    	常量不能修改

​	定义完变量必须有值，不能后赋值

​	Object.freeze(),让对象中的内容不能被修改

```javascript
	const arr = [1,2,3,4];
    arr.push(5);
    console.log(arr);
    const arr2 = Object.freeze([1,2,3]);
    arr.push(4);//push失效
	console.log(arr2);
```

### 解构赋值

​    	左右两边的数据格式要保持一致

​	解构时可以给默认值

```javascript
let [a,[b,c],d='d'] = [1,[2,3]];//当赋值没有对应的值时，相当于undefined处理，或者赋值默认值
console.log(a,b,c,d);

let json = {
    name: "lov",
    age: 21
};
let {name,age:g} = json;
console.log(name,g);

function getInfo([id,token]){
    console.log(id,token);
    return {'type':'login','info':'success'};
}
let {type,info} = getInfo(['lov',001]);
console.log(type,info);
```

### 字符串

​	``:字符串模板

​	新增api

```javascript
let str = "a b c d e f g";
console.log(str.includes('a'));

console.log(navigator.userAgent.includes('Chrome')?'chrome':'other');

console.log(str.startsWith('a'));
console.log(str.endsWith('g'));
console.log(str.repeat(3));
console.log('a'.padStart(4,'x'));
console.log('a'.padEnd(4,'x'));    
```

### 函数

#### 函数默认参数

​	函数参数默认定义，不能再let或const声明 

```javascript
function show(a='a',b='b'){
       console.log(a,b);
}
show()

function get({a='a',b='b'}={}){
    console.log(a,b);
}
get({a:1,b:2});
get({});
get();
```
#### 扩展运算符

```javascript
let arr = ['aaa','bbb','ccc'];
let arr2 = [...arr];
let arr3 = Array.from('a-b-c-d-e');
console.log(arr3);
console.log(arr2);
console.log(...arr);

function show(a,b,...c){
    console.log(a,b,c);
}
show(1,7,4,8,3,9);
function show2(a,b,c){
    console.log(a,b,c);
}
show2(...[4,7,2]);
```

#### 箭头函数

​	该函数中的this为定义时的this，而不是运行时的所在对象
​	该函数中没有arguments
​	该函数不能当构造函数

```javascript
let show = (a='a')=>{
    console.log(a);
};
show();

let json = {
    id:1,
    show(){
        setTimeout(()=>{
            console.log(this.id);
        },2000);
    }
}

json.show();
```

### 数组

#### 循环

​	forEach、map、filter、some、every、reduce、reduceRight

```javascript
let arr = ['aaa','bbb','ccc'];

			arr.forEach(     //普通的for，没有返回值
				function(val,index,arr){
				console.log(this,val,index,arr);//this未指定时默认为window
				}
				,document //指定this
			);	

			// map,filter-------------
			let arr2 = [
				{title:'aaa',read:100,hot:false},
				{title:'bbb',read:90,hot:true},
				{title:'ccc',read:10,hot:false},
				{title:'ddd',read:100,hot:true}
			];

			let rs = arr2.map(   		//数据交互映射，默认情况与forEach相同，有返回值
				(val,index,arr)=>{
					let json  = {};
					json.title = `${val.title}`;
					json.read = `${val.read}`;
					json.hot = `${val.hot}`;
					return json;
				}
			);
			console.log(rs);

			let rs2 = arr2.filter(   		//返回符合条件内容
				(val,index,arr)=>{
					return val.hot;
				}
			);
			console.log(rs2);

			// some,every--------------
			let rs3 = arr.some(   		//查找数组中某一元素符合条件，则返回true
				(val,index,arr)=>{
					return val == 'bbb';
				}
			);
			console.log(rs3);

			let rs4 = arr.every(   		//查找数组中，所以元素符合条件时，则返回true
				(val,index,arr)=>{
					return val == 'bbb';
				}
			);
			console.log(rs4);
			// reduce,reduceRight------

			let arr3 = [1,2,3,4,5];

			let rs5 = arr3.reduce( //从左往右循环，reduceRight反之
				(prev,cur,index,arr)=>{ //prev默认为0，之后为每一次return的结果；cur为当前对应的值
					return prev+cur;
				}
			);
			console.log(rs5);

			// for...of...-------------

			for(let val of arr){
				console.log(val);
			}
			for(let index of arr.keys()){
				console.log(index);
			}
			for(let item of arr.entries()){
				console.log(item);
			}
			for(let [key,val] of arr.entries()){
				console.log(key,val);
			}
```

#### other -NEW_API

​	**Array.from()**

​	把类数组对象转换成数组，只要具备length就能转换

```javascript
			let json = {
				0: 'aaa',
				1: 'bbb',
				2: 'ccc',
				length: 3
			}

			let rs = Array.from(json);
			console.log(rs);
```

​	**Array.of()**

​	将一组值转换为数组

```javascript
			let arr = Array.of(1,2,3,4);
			console.log(arr);
```

​	**find()**	

​	找出第一个符合条件的数组成员，没有返回undefined

​	**findIndex()**	

​	找出第一个符合条件的数组成员的index，没有返回-1

```javascript
			let arr = ['aaa','bbb','ccc'];

			let rs = arr.findIndex(
				(val,index,arr)=>{
					return val == 'ccc';
				}
			);

			console.log(rs);
```

​	**fill()**

```javascript
			let arr = new Array(10);
			arr.fill('default',1,3); //在index为1-3间填充‘default’

			console.log(arr);
```

​	includes()

```javascript
			let arr = ['aaa','bbb','ccc'];
			console.log(arr.includes('aaa'));
```



​	

