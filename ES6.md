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

### 字符串新增

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

