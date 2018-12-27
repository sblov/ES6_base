# ES6

### let、const

#### let

​	let只相对于区域，而var直接是全局window	

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

​	**includes()**

```javascript
			let arr = ['aaa','bbb','ccc'];
			console.log(arr.includes('aaa'));
```

### 对象

```javascript
		   let name = 'lov';
           let age = 21;
            
           let json = {
                name, //name:name
                age,  //age:age
                show(){  //最好别用箭头函数，会有this指向问题
                    console.log(`name:${name}`);
                }
            }
            
            console.log(json);
            json.show();
            
            // Object.is() 比较两个值是否相等
            console.log(NaN == NaN); //false
            console.log(Number.isNaN(NaN));
            console.log(Object.is(NaN,NaN));

            console.log(+0 == -0);
            console.log(Object.is(+0,-0));

            // Object.assign() 合并对象
            let json_1 = {a: 1};
            let json_2 = {b: 2,a: 4};
            let json_3 = {c: 3};

            let rs = Object.assign({},json_1,json_2,json_3);
            console.log(rs);

            let arr = ['a','b','c'];
            let rs_1 = Object.assign([],arr);
            console.log(rs_1);

            // Object.keys()
            // Object.entries()
            // Object.values()
            let {keys,values,entries} = Object;

            let json_4 = {a:1,b:2,c:3};
            for(let key of keys(json_4)){
                console.log(key);
            }
            for(let value of values(json_4)){
                console.log(value);
            }
            for(let entry of entries(json_4)){
                console.log(entry);
            }

            // 对象中的扩展运算符
            let {a,...b} = json_4;
            console.log(a,b);
            console.log({...json_4});
```

### Promise

​	解决异步回调函数问题，解决传统的回调嵌套问题

```javascript
			let a = 1;
            let promise = new Promise((resolve,reject)=>{
                if(a == 10){
                    resolve('success');    // true调用resolve
                }else{
                    reject('fail');         //false调用reject
                }
            });
            /*promise.then(res=>{
                console.log(res);   //suucess
            },err=>{    
                console.log(err);   //fail
            });
            promise.catch(err=>{    //catch
                console.log(`err:${err}`);
            })*/
            promise.then(res=>{
                console.log(res);   
            }).catch(err=>{    
                console.log(`err:${err}`);
            });

            // Promise.resolve('aaa') 将现有的内容转换为promise对象，并为resolve状态，new Promise(resolve=>{resolve('aaa')})
            // Promise.reject() 将现有的内容转换为promise对象，并为reject状态

            // Promise.all() 打包所有的promise，且必须都是 resolve
            // Promise.race() 返回第一个值，为reject则抛出error
            let p1 = Promise.resolve('aaa');
            let p2 = Promise.resolve('bbb');
            let p3 = Promise.resolve('ccc');
            let p4 = Promise.reject('ddd');

            Promise.all([p1,p2,p3]).then(res=>{
                console.log(res);
            });
            Promise.race([p2,p4,p1]).then(res=>{
                console.log(res);
            }).catch(err=>{
                console.log(err);
            });
            
            //demo
            let status = 1;
            let userLogin = (resolve,reject)=>{
                setTimeout(()=>{
                    if(status == 1){
                        resolve({data:'xxx',msg:'xxx',token:'xxxx'});
                    }else{
                        reject('login fail');
                    }
                },1000);
            };
            let getInfo = (resolve,reject)=>{
                setTimeout(()=>{
                    if(status == 1){
                        resolve({data:'INFOxxx',msg:'xxx',token:'xxxx'});
                    }else{
                        reject('login fail');
                    }
                },1000);
            };

            new Promise(userLogin).then(res=>{
                console.log('login success');
                console.log(res);
                return new Promise(getInfo);
            }).then(res=>{
                console.log('Info success');
                console.log(res);
            })
```

### 模块

​	添加type="module"
​    	import导入模块路径，可以是相对，绝对
​    	import ... from '...js'
   	 import '...js'，相当于引入整个js文件
  	通过as在模块或import中起别名
   	 import有代码提升的效果，代码块会先执行import
​    	export导出需要用{}引用，export default导出可直接引用
​    	导入的模块内容发生改变时，引用也会同步改变
​    	import(): 动态引入，类似node的require()，不可用于if语句	

```javascript
		// import * as mod_1 from './mod_1.js'
        // import {sqrt,aaa,b as bbb,c} from './mod_1.js'
        import json,{sqrt,aaa,b as bbb,c,ch} from './mod_1.js'
            console.log(json);
            console.log(sqrt(20));
            console.log(aaa,bbb,c);
            
            console.log(`ch:${ch}`);
            setTimeout(()=>{
                console.log(`ch:${ch}`);
                
            },2000);
            
            // 动态引入
            import('./mod_1.js').then(res=>{
                    console.log(res);
                });
            
            // 结合promise.all
            Promise.all([
                import('./mod_1.js'),
                import('./mod_3.js')
            ]).then(res=>{
                // console.log(mod_1,mod_1);
                console.log(res);
            });
```

### Class

​	方法名可以用表达式
​    	class没有预解析
​    	对于setter与getter，内部不可直接调用对应属性	

```javascript
		// origin
        /*function Person(name,age){
            this.name = name;
            this.age = age;
        };
        Person.prototype.showName = function(){
            return `name:${this.name}`;
        };*/
        
        //const Person = class{}; 
        let showA = 'showAge';
        class Person{ //type => function
            constructor(name,age){ //构造函数默认执行
                console.log('constructor......');
                this.name = name;
                this.age = age;
            }
            showName(){
                return `name:${this.name}`;
            }
            [showA](){
                return `age:${this.age}`;
            }
            set com(val){          //setter
                
                console.log('set com');
            }
            get com(){              // getter

                return 'dd';    
            }

            static showMsg(){       //静态方法
                console.log('show every thing');
            }
        };

        let person = new Person('lov',12);
        console.log(person[showA](),person.showAge());

        person.com = 'lob';
        console.log(person.com);

        Person.showMsg();
```

#### 继承	

```javascript
		 /*// 父类
        function Person(name){
            this.name = name;
        }
        Person.prototype.showName = function(){
            return `name:${this.name}`;
        }
        
        //子类
        function Student(name,skill){
            Person.call(this,name);
            this.skill = skill;
        }
        Student.prototype = new Person();
        
        */
       
       class Person{
           
           constructor(name){
               this.name = name;
            }
            showName(){
                return `name:${this.name}`;

            }
        }
        
        class Student extends Person{
            constructor(name,skill){
                super(name);
                this.skill = skill;
            }
            showName(){ //overload
                return super.showName(); 

            }
        }

        let stud = new Student('lov','gaming');
        console.log(stud.showName());
```

### Symbol& generator

#### Symbol

​	新数据类型：Symbol
​        Symbol返回的值是唯一值
​        在for..in.. 循环中无法获取symbol类型	

```javascript
		let sy = Symbol('aaa');
       let sy2 = Symbol('aaa');
       console.log(typeof sy);
       console.log(Object.is(sy,sy2));

       let json = {
           a: 1,
           b: 2,
           [sy]: 'json'
       }
       // 无法循环出symbol类型
       for(let item in json){
           console.log(item);
       }
```

#### generator函数

​        解决异步，深度嵌套，Promise到aysnc的过渡特性
​        函数中，根据yield顺序执行

```javascript
		function * gen(){
           yield 'aaa';
           yield 'bbb';
           return 'ccc';
       }
       let g = gen();
    //    console.log(g.next());
    //    console.log(g.next());
    //    console.log(g.next());   //当返回的json中的done为true时停止
    //    console.log(g.next());

       for(let val of g){   //for...of..自动遍历 ，不会遍历return的内容
           console.log(val);
       }
    //    解构访问
       let [a,b,c] = gen();
       console.log(a,b,c);
    //    扩展访问
       console.log(...gen());
    //    Array.from()
       console.log(Array.from(gen())); 
```

### async&await

​    	await只能放到async函数中
​    	相比generator语义化更强
​    	await后面可以时promise对象，也可以时数字，字符串，布尔
​    	async函数返回是一个promise对象
​    	只要await语句后面的Promise状态变成reject，那么整个async函数会中断执行

```javascript
		async function fn() {
            await 'aa';
            // throw new Error('error');
            try {
                let p1 = await Promise.reject('error'); // try-catch
                let p2 = await Promise.resolve('success');
            } catch (error) { }
            console.log(p1);
            console.log(p2);    
            return 'aaa';
        }
        fn().then(res=>{
            console.log(res);
        }).catch(err=>{
            console.log(err);
        });
```

### Set&WeakSet

​    	java中set相似，不能有重复值
​    	set中存储数组，weakset存储json，但都可通过add添加json为数组元素

```javascript
		let setArr = new Set(['a','a','b','c']);
        console.log(setArr);
        setArr.delete('a'); 
        setArr.add('d');
        console.log(setArr);
        console.log(setArr.has('a'));
        console.log(setArr.size);
        
        for(let item of setArr.entries()){
            console.log(item);
        }
        setArr.forEach((value,index) => {
            console.log(value,index);
        });

        setArr = new Set([...setArr].map(val=>val.repeat(2)));
        console.log(setArr);

        setArr.clear();
        console.log(setArr);   

        let wSet = new WeakSet();
        wSet.add({a:1,b:2});
        console.log(wSet);
```



### Map&WeakMap

​	Map：类似于json，但json的key只能为字符串，但map可为任何类型

​	WeakMap：key只能为对象

```javascript
		let map = new Map();
		let json = {
			a: 'aaa',
			b: 'bbb'
		}
		map.set('a','aaa');
		map.set(json,'json');

		console.log(map);
		console.log(map.get(json));
		// console.log(map.delete('a'));
		console.log(map.has('a'));
		// console.log(map.clear());
		
		for(let [key,value] of map){ 	// 默认调用entries()
			console.log(key,value);
		}

		map.forEach((value,key)=>{
			console.log(value,key);
		})

		// WeakMap 中key只能为对象
		let wMap = new WeakMap();

		wMap.set(json,'json');
		console.log(wMap);
```

### 数值&Math

​	进制

```javascript
		//二进制（binary）
		let b1 = 0b010101;

		console.log(b1);
		// 八进制(octal)
		let o1 = 0o12345;
		console.log(o1);
```

​	Number：对于大部分数值操作，都归纳到Number对象中

```javascript
		let a = 1;
		console.log(Number.isNaN(a));
		console.log(Number.isFinite(a));	//判断是否为数字
		console.log(Number.isInteger(a));	//判断是否为整数
```

​	安全整数：-(2^53-1)到(2^53-1)

```javascript
		let a = 2**53;
		console.log(a-1);
		console.log(Number.isSafeInteger(a));
		console.log(Number.isSafeInteger(a-1));
		console.log(Number.MAX_SAFE_INTEGER);
		console.log(Number.MIN_SAFE_INTEGER);
```

​	Math

```javascript
		// trunc 截取整数部分
		console.log(Math.trunc(4.555));
		// sign 判断正负数，0
		console.log(Math.sign(-50));
		console.log(Math.sign(50));
		console.log(Math.sign(0));
		console.log(Math.sign(-0));
		// cbrt 立方根
		console.log(Math.cbrt(8));	
```

### 正则

#### 	捕获

```javascript
		let  str = '2018-12-23';

		// ?<> 命名捕获
		let reg = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;

		let {year,month,day}  = str.match(reg).groups;
		console.log(str.match(reg));
		console.log(year,month,day);

		// 反向捕获 \k<>
		let reg2 = /^(?<msg>lov)-\k<msg>-\1$/;
		console.log(reg2.test('a-a-a'));
		console.log(reg2.test('msg-msg-msg'));
		console.log(reg2.test('lov-lov-lov'));

		// 结合replace的捕获 $<>
		str = str.replace(reg,'$<year>/$<month>/$<day>');
		let rs = str.replace(reg,(...args)=>{
			let {year,month,day} = args[args.length-1];
			return `$<year>/$<month>/$<day>`;
		});
		console.log(str);
		console.log(rs);
```

### 标签函数

```javascript
		function fn(){
			console.log(arguments);
		}
		fn('lov');
		fn`lov`;
```

```javascript
----------fn('lov')-----------------
Arguments ["lov", callee: ƒ, Symbol(Symbol.iterator): ƒ]
0: "lov"
callee: ƒ fn()
length: 1
Symbol(Symbol.iterator): ƒ 
values()__proto__: Object
----------fn`lov`-------------------
Arguments [Array(1), callee: ƒ, Symbol(Symbol.iterator): ƒ]
0: ["lov", raw: Array(1)]
callee: ƒ fn()
length: 1
Symbol(Symbol.iterator): ƒ values()
__proto__: Object

```

### Proxy

​	与java中的proxy相似，增强对象的一些功能

​	proxy是代理模式的一种

```javascript
		let obj = {
			name: 'lov'
		};

		let Pobj =  new Proxy(
			obj,
			{
				get(target,property){
					if(property in target){
						console.log(`get-${property}`);
						return target[property];
					}else{
						console.warn(`${property} is not exist`);
						return 'orz';
					}
				}
			}
		);
		console.log(Pobj.name);
		console.log(Pobj.age);
```

#### 	Proxy_demo

```javascript
		const DOM = new Proxy({},	//所有对象
			{
				get(target,property){
					return function(attr={},...children){	//返回函数
						//通过property新建元素
						const el = document.createElement(property);

						// 为元素添加属性值
						for(let key of Object.keys(attr)){
							el.setAttribute(key,attr[key]);
						}
						// 添加子节点
						for(let child of children){
							if(typeof child == 'string'){
								child = document.createTextNode(child);
							}
							el.appendChild(child);
						}

						// 返回节点
						return el;
					}
				}
			}
		);

		let oDiv = DOM.div(
			{id:'div1',class:'container'},
			'Lov','Welcome','!',
			DOM.a({href:'www.baidu.com'},'Baidu'), //嵌套
			DOM.a({},
				DOM.li({},'1-------'),
				DOM.li({},'2-------'),
				DOM.li({},'3-------'),
				DOM.li({},'4-------')
			)
		);

		console.log(oDiv);

		window.onload = function(){
			document.body.appendChild(oDiv);
		}

```

#### 	**set**、**delete**、**has**	

```javascript
			let obj = new Proxy({},{
            set(target,prop,value){ // 在属性赋值时调用
            //    console.log(target,prop,value);
                if(prop == 'age'){
                    if(!Number.isInteger(value)){
                        throw new TypeError('Must be Integer!');
                    }
                    if(value > 200){
                        throw new RangeError('Out of Range!');
                    }
                }
                target[prop] = value;
                console.log(`${prop} set success.`);
            },
            deleteProperty(target,prop){
                delete target[prop];
                console.log(`${prop} has been deleted!`);
            },
            has(target,prop){
                console.log(`Has ${prop} in Target ?`);
               
                return prop in target;
            }

        });

        obj.a = 1;
        obj.age = 200;

        delete obj.a;
        console.log('a' in obj);
```

####  	**apply**

```javascript
		function fn(a,b){
            return a+b;
        }

        let newFn  = new Proxy(fn,{
            apply(target,context,args){
                // console.log(target,context,args);
                // console.log(...arguments);
                return Reflect.apply(...arguments)**2; 
            }
        })

        console.log(newFn(1,3));
```

### Reflect

​	将js语言方面的东西直接放到reflect上，通过reflect直接调用

```javascript
		function fn(...args){
            console.log(this);
            console.log(args);
        }

        // fn(1,2,3);
        // fn.call('aaa',1,2,3);
        // fn.apply('aaa',[1,2,3]);
        // Reflect.apply(目标方法,this对象,参数)
        Reflect.apply(fn,'aaa',[1,2,3])
        
        // console.log('apply' in  Object);
        console.log(Reflect.has(Object,'apply'));

        let json = {
            a:1,
            b:2
        }

        Reflect.deleteProperty(json,'a');
        console.log(json);
```

