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

   - `forEach()`, `filter()`, `reduce()`, `every()` 和`some()`都会跳过空位。
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

6.  DOM 事件绑定：

   - addEventListener有三个参数：第一个参数表示事件名称（不含 on，如 “click”）；第二个参数表示要接收事件处理的函数；第三个参数为 useCapture。

   - IE用了attachEvent(),和detachEvent(),接收两个参数,事件名称和事件处理程序函数。由于IE8及以前只支持事件冒泡;通过attachEvent()添加的事件处理程序都会被添加到冒泡阶段

     IE下绑定监听器：attachEvent(event, function)：event 必须。字符串，指定事件的名称。注意: 使用 “on” 前缀。 例如，使用 “onclick” ,而不是使用 “click”

     IE下移除侦听器：btn.detachEvent("onclick",handler);   

   - 事件触发器也是分为高级浏览器和IE两派，而dispatchEvent正是用于高级浏览器的事件触发。 dispatchEvent是作为高级浏览器(如chrome、Firfox等)的事件触发器来使用的。

   ------

   

7. 实现三栏布局：两栏定宽，第三个自适应：

   子项使用flex-grow：1，占满剩余空间

   ------

8. Typeof

   ![typeof](C:\Users\NHT\Desktop\前端复习\img\typeof.PNG)

   值得注意的一点：”其他任何对象“包括Array

   简单点记：null，Array，object都是”object“，function是“function”，其他的基本数据类型都是它们本身。
   
   ------
   
9.  **关于操作数组本身**

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
   
10. slice、扩展运算符...拷贝数组，是**浅拷贝**

11. 定时器重复执行任务：setInterval，只执行一次：setTimeout

    ------

    

12. 客户端三种储存方式：

    (1) 存储大小

    - cookie数据大小不能超过4k。
    - sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

    (2) 有效时间

    - localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
    - sessionStorage 数据在当前浏览器窗口关闭后自动删除。
    - cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

    (3) 数据与服务器之间的交互方式

    - cookie的数据会自动的传递到服务器，服务器端也可以写cookie到客户端
    - sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

    ------

13. 函数表达式定义函数不要用具名函数

    ```js
    var sum = function g(){
        ...
    }
    g(); // 报错
    ```

14.  

