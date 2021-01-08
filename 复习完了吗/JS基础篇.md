# JS基础

1.  ```js
   var setPerson=function(person){ 
   	person.name="kevin"; //这个person是新的person，也就是第二个指针，指向同一个对象
       person={name:"nick"};//局部对象，函数执行完就销毁 
   }; 
   var person={name:"alan"};
   setPerson(person); 
   alert(person.name);//kevin
   ```

   函数内部的person和函数外的person（他们是不同的指针）指向的是同一个对象，但是对象是**按值传递的**。

   ------
   
   
   
2. ```javascript
   Array(3) // [, , ,]
   ```

   这种创建数组的方式，返回一个具有 3 个空位的数组，注意，**空位不是`undefined`**，一个位置的值等于`undefined`，依然是有值的。空位是没有任何值，在浏览器中显示'empty'。

   ```js
   var array1=Array(3);
   array1[2]=2;
   var result=array1.map(element => "1");
   console.log(result);// [,,'1']
   ```

   ES5 对空位的处理，大多数情况下会忽略空位。

   - **`forEach()`, `filter()`, `reduce()`, `every()` 和`some()`都会跳过空位**。
   - `map()`会跳过空位，但会保留这个值
   - `join()`和`toString()`会将空位视为`undefined`，而`undefined`和`null`会被处理成空字符串。

   ------

   

3.  布尔操作符

   - ！：逻辑非，0/空字符串/null/undefined/NaN转为true，非零/字符串/对象转为false。

   - &&：逻辑与，如果第一个是false，就不管第二个了
   - ||：逻辑或，第一项为true，则返回第一项的结果，如果第一项是false,则不论第二项是什么，都返回

   ------

   

4. join() 方法用于把数组中的所有元素放入一个字符串。

   ------

   

5. 阻止默认和阻止冒泡   

   - event.stopPropagation()可以阻止事件的传播，取消进一步的事件冒泡或者捕获。IE中的事件对象   cancelBubble属性值为true,可以取消事件冒泡。

   - preventDefault() 阻止事件的默认行为，只有cancelabel属性的值设为true时，才可以使用preventDefalut。

   ------

6. DOM 事件绑定：

   - addEventListener有三个参数：第一个参数表示事件名称（不含 on，如 “click”）；第二个参数表示要接收事件处理的函数；第三个参数为 useCapture。

   - IE用了attachEvent(),和detachEvent(),接收两个参数,事件名称和事件处理程序函数。由于IE8及以前只支持事件冒泡;通过attachEvent()添加的事件处理程序都会被添加到冒泡阶段

     IE下绑定监听器：attachEvent(event, function)：event 必须。字符串，指定事件的名称。注意: 使用 “on” 前缀。 例如，使用 “onclick” ,而不是使用 “click”

     IE下移除侦听器：btn.detachEvent("onclick",handler);   

   - 事件触发器也是分为高级浏览器和IE两派，而dispatchEvent正是用于高级浏览器的事件触发。 dispatchEvent是作为高级浏览器(如chrome、Firfox等)的事件触发器来使用的。

   ------

   

   ------

7. 类型检测

   **Typeof**

   ![typeof](C:\Users\NHT\Desktop\前端复习\img\typeof.PNG)

   值得注意的一点：”其他任何对象“包括Array

   简单点记：function是“function”，其他的基本数据类型都是它们本身，其他都是”object“（包括null，Array，object）。

   缺点：有些浏览器的版本，使用他会产生不准确的结果。比如safari(至第四版)，对正则表达式用typeof，结果是function。

   **instanceOf**：对象和构造函数必须在同个全局作用域中

   **要想准确获得一个正确的类型**：`Object.prototype.toString.call(xx)`，原理是，每个类内部都用一个[[class]]属性，这个属性指定了构造函数名。可以用来准确区分原生或者非原生（开发人员自定义的）对象。

   ------

8. **关于操作数组本身**

   必须要注意的问题是，增删数组本身，会改变它自身的length，从而影响遍历。

   为了避免这个问题，试用了很多遍历的API都行不通。

   最终，用这个方法完美解决：**倒着遍历**

   ```js
   // 删除数组中与item相等的元素，在原数组上操作
   function removeWithoutCopy(arr, item) {
       for(let i=arr.length-1;i>0;i--){
           if(arr[i]===item){
               arr.splice(i,1); // 第一个参数是删除的下标，第二个参数是删除的个数
           }
       }
       return arr;
   }
   removeWithoutCopy([1,2,3,4,2,2],2)
   ```

   ------

9. slice、扩展运算符...拷贝数组，是**浅拷贝**

10. 定时器重复执行任务：setInterval，只执行一次：setTimeout

   ------

   

------

13. 函数表达式定义函数不要用具名函数

    ```js
    var sum = function g(){
        ...
    }
    g(); // 报错
    ```

2. 事件模型：**先捕获后冒泡**

   addEventListener有第三个参数，默认为false，即“事件在冒泡阶段执行”

3. 垃圾回收机制：

   标记清除法：进入执行环境内的和离开的都要标记

   引用计数法：跟踪记录每个值被引用的次数，引用为0就应该清除。 
   
16. ```javascript
    var x = 10;
    var obj = {
        x: 20,
        fn: function() {
            var x = 30;
            return this.x;
        }
    }
    console.log(obj.fn()); // 20
    console.log((obj.fn)()); // 20
    // 下面开始，this得不到维持，就不知道是谁在调用函数，所以指向window
    console.log((obj.fn = obj.fn)());// 10
    console.log((obj.fn,obj.fn)());// 10
    console.log(obj.fn.apply(window));// 10
    ```

17. **forEach**使用return只是跳出了当前的循环，使用break会报语法错误。forEach  无法在所有元素都传递给调用的函数之前终止遍历，除非主动用try抛出错误。

18. 使用new来创建对象(调用构造函数)时，如果return的是非对象(数字、字符串、布尔类型等)会忽而略返回值；如果return的是对象，则返回该对象 (注：若return null也会忽略返回值）。 

    ```javascript
    function Person(name) {
        this.name = name;
        return {}
    }
    let p = new Person('Tom'); 
    console.log(p)// {}
    ```

19. Node的事件模块中，目前只包含一个类:EventEmitter。这个类在Node的内置模块中被大量使用，在Node中，所有能触发事件的对象都是 EventEmitter 类的实例。要使用EventEmitter，首先必须要继承它。

    发布订阅模式

    ```javascript
    class EventEmitter {
        constructor () {
            this._eventpool = {};
        }
        // on监听事件
        on (event, callback) {
            this._eventpool[event] ? this._eventpool[event].push(callback) : this._eventpool[event] = [callback]
        }
        // emit触发事件
        emit (event, ...args) {
            this._eventpool[event] && this._eventpool[event].forEach(cb => cb(...args))
        }
        // 关闭事件（删除发布者）
        off (event) {
            if (this._eventpool[event]) {
                delete this._eventpool[event]
            }
        }
        // 只执行一次就关闭
        once (event, callback) {
            this.on(event, (...args) => {
                callback(...args);
                this.off(event)
            })
        }
    }
    ```

20. ajax原理：创建XMLHttpRequest对象，发送异步请求

    ```
    1.创建xhr对象（XMLHttpRequest/ActiveXObject(Microsoft.XMLHttp)）
    
    2.判断数据传输方式(GET/POST)转换数据格式
    
    3.打开链接 open()
    
    4.发送 send()
    
    5.当ajax对象完成第四步（onreadystatechange）数据接收完成，判断http响应状态（status）200-300之间或者304（缓存）执行回调函数
    ```

# ES6

- let、const、var区别

  > `var` 存在提升，我们能在声明之前使用。`let`、`const` 因为暂时性死区的原因，**不能在声明前使用** 
  >
  > `var` 在全局作用域下声明变量会导致变量挂载在 `window`上，其他两者不会 
  >
  > `let` 和 `const` 作用基本一致，但是后者声明的变量不能再次赋值 

  **var**

  - 声明变量的作用域限制在其声明位置的上下文中，而非声明变量总是全局的
  - 由于变量声明（以及其他声明）总是在任意代码执行之前处理的，所以在代码中的任意位置声明变量总是等效于在代码开头声明

  **let**

  - 允许你声明一个作用域被限制在块级中的变量、语句或者表达式
  - let绑定不受变量提升的约束，这意味着let声明不会被提升到当前
  - 该变量处于从块开始到初始化处理的“暂存死区”

  **const**

  - 声明创建一个值的只读引用 (即指针)
  - 基本数据当值发生改变时，那么其对应的指针也将发生改变，故造成 `const`申明基本数据类型时，再将其值改变时，将会造成报错， 例如 `const a = 3` ; `a = 5`时 将会报错
  - 但是如果是复合类型时，如果只改变复合类型的其中某个`Value`项时， 将还是正常使用
  
- 箭头函数与普通函数的区别

  - 箭头函数是匿名函数，不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误（无prototype）
  - 箭头函数不绑定this，会捕获其所在的上下文的this值，作为自己的this值
  - 箭头函数是没有arguments的
  - 箭头函数不支持generator语法

- 变量的解构赋值

- promise、async await、Generator的区别

    https://www.cnblogs.com/cqhaibin/p/10085301.html 

- ES6的继承与ES5相比有什么不同

- js模块化（commonjs/AMD/CMD/ES6）

   https://blog.csdn.net/zhenghaohan1999/article/details/102968432 
   
   

