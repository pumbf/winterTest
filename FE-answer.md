# 前端考核题答案

#### 第4题

```html
<script type="text/javascript">
    var ul = document.querySelector('ul');  
    var myFun = function () {
        //code...
    };
</script>
```

小明想写出一段代码来给网页中的ul标签里面增加5000个li的元素并且为每一个li元素绑定一个myFun的方法  请写出一种你觉得最节省性能的方案来处理这个问题  (ul元素已经获取)

#### 第4题答案

```javascript
var lis = '';
for(var i = 0; i < 5000; i++) {
  lis += '<li></li>';
}
ul.addEventListener(function(event) {
  var target = event.target;
  if(target.tagName === 'li') {
	myFun.call(target, event);
  }
})
ul.innerHTML = lis;
```

#### 第5题

使用ajax请求当前目录下的test.txt文件, 代码如下: 

```JavaScript

var req = new XMLHttpRequest();

req.open('GET', 'test.txt', true);

req.send(null);

req.onreadystatechange = function () {

    if (req.readyState === 4 && req.status === 200) {

        console.log(req.responseText);

    }

}
```

(1)必做题: 请说明onreadystatechange 函数的作用

(2)选做题: 将当前异步请求的方式改为同步(即将req.open的第三个参数改为false), 请问还能在控制台输出响应文本吗? 如果不能, 请说原因, 并在下方写出改正后能输出响应文本的代码.

#### 第5题答案

(1) onreadystatechange 用于监听 readyState 发生改变的事件, 以在请求完成拿到返回数据时能处理数据

(2)不能, 同步请求会等到请求完成( `readyState === 4`)时才能运行 `req.onreadystatechange  = ….`, 此后事件无法被触发

```JavaScript

var req = new XMLHttpRequest();

req.onreadystatechange = function () {
    if (req.readyState === 4 && req.status === 200) {
        console.log(req.responseText);
    }
}

req.open('GET', 'test.txt', true);

req.send(null);

```

#### 第8题

写一段js代码去掉一个数组里面的重复项

```JavaScript
 var arr =[1,2,3,3,4,4,5,6];
```

#### 第8题答案

+ 利用对象的键不能重复的特性

  ```javascript

  function unique(arr) {
    
    var hash = {};
    
    return arr.filter(function(item) {
      
      if(hash[item]) {
        return false;
      }
      
      return hash[item] = true;
    })
    
  }
  ```

+ indexOf 查找数组元素

  ```JavaScript

  function unique(arr) {
    
    var result = [];
    var len = arr.length;
    
    for(var i = 0; i < len; i++) {
  	var item = arr[i];
      
      if(result.indexOf(item) !== -1){
        continue;
      }
      
      result.push(item);
    }
    
    return result;
    
  }


  ```

#### 第9题

```javascript
var name = "aaaaa";
var youName = {
    name:"bbbbb",
    theName:function(){
        function dis(){
            console.log("this.name="+this.name);
        };
        dis();
    },
};
youName.theName();       //this.name = ?
var ccc = youName.theName;
ccc();                   //this.name = ?
```

#### 第9题答案

```JavaScript
'this.name=aaaaa'

'this.name=aaaaa'
```



#### 第11题

```JavaScript
var arr = [];
  for (var i = 0; i < 10; i++) {
      arr[i] = function () {
          console.log(i);
      }
  }

  arr[1]() = ? arr[2]() = ?
```

#### 第11题答案

```JavaScript
arr[1]() // 10
arr[2]() // 10
```



#### 第13题

```JavaScript
var scope="global";  
function t(){  
   console.log(scope);
   var scope="local";  
   console.log(scope); 
}  
t();
```

#### 第13题答案

```JavaScript
undefined
local
```



#### 第13题

```HTML
<ul id="target">
	<li>1</li>
    <li>2</li>
    <li>3</li>
	<li>4</li>
</ul>
```

编写一个函数将列表子元素顺序反转.

#### 第13题答案

```JavaScript
var target = document.querySelector('#target');

var frag = document.createDocumentFragment();

var i = 0, 
    len = target.children.length;

for(i = len - 1; i >= 0; i --) {
    frag.appendChild(target.children[i]);
}

target.appendChild(frag); 

```

#### 第14题

canvas 坐标变换有哪几种方法?

#### 第14题答案

`translate`, `scale`, `rotate`