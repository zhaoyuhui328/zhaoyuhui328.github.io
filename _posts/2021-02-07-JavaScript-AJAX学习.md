# AJAX

AJAX 异步的JS和XML

## AJAX主要在网页中的主要应用场景

    1.检查用户名等是否合格（注册页面）
    2.二级分类
    3.滚动（滚到底部出现新的内容）
    4.动态变化（不会刷新）
    5.关键字提醒

### AJAX简介

    在浏览器中向服务器发送异步请求
    最大优势：不用刷新即可获取数据
    提高了网页加载的速度

### XML(几乎被JSON所取代)

    XML叫做可扩展标记语言
    主要用来传输和存档数据
    而HTML主要是用来呈现数据

### AJAX特点

    优点：
        无需刷新页面
        根据用户事件更新部分页面内容
    缺点：
        没有浏览历史，不能退回
        存在跨域问题（同源）
        SEO不友好

### HTTP协议(超文本传输协议)

------ 浏览器与万维网服务器之间互相通信的规则

      浏览器————>服务器（请求报文）
      服务器————>浏览器（响应报文）

1.请求报文

    行  POST(GET)/URL  HTTP/1.1(HTTP版本)
    头  Host: aiguigu.com  
        Cookie: name = guigu 
        Content-type: application/X-www-form-urlencoded
        User-Agent-chrome 83
    空行
    体(GET请求为空)  username = admin & password = admin

2.响应报文

    行  HTTP/1.1 200/404/401(响应状态码) ok
    头  Content-Type: text/html;charset  = utf-8
       Content-length: 2048
       Content-encoding: gzip
    空行
    体 html语句

查看通信报文 Network
Headers Response

### Express框架的基本使用

1.引入express

    `const express = require('express');`

2.创建应用对象

    ` const app = express() `

3.创建路由规则

    request是对请求报文的封装
    response是对响应报文的封装

```javascript
app.get('/',(request,response)=>{
    // 设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    // 设置响应
    response.send('HELLO EXPRESS');
});
```

4.监听端口启动服务

``` javascript
 app.listen(8000,()=>{
     console.log("服务已启动，8000端口监听中");
 });
```

### AJAX前后端交互4大步（以GET为例）

1.创建对象
    ` const xhr = new XMLHttpRequest(); `

2.初始化 设置请求方法和url
    ` xhr.open('GET','http://127.0.0.1:8000/server'); `

3.发送
    `xhr.send();`

4.事件绑定（处理服务端返回的结果）

```javascript
xhr.onreadystatechange = function() {
    if(xhr.readyState === 4) {
        if(xhr.status >= 200 && xhr.status <300) {
            // console.log(xhr.status); //状态码
            // console.log(xhr.statusText); // 状态字符串
            // console.log(xhr.getAllResponseHeaders()); // 所有头
            // console.log(xhr.response);
            result.innerHTML = xhr.response;
        }
    }
}
```

### AJAX传输案例

1.GET

``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX GET 请求</title>
    <style>
        #result {
            width: 200px;
            height: 200px;
            border: solid 1px #90b;
        }
    </style>
</head>

<body>
    <button>点击发送请求</button>
    <div id="result"></div>
    <script>
        // 获取button元素
        const btn = document.getElementsByTagName('button')[0];
        const result = document.getElementById('result');
        btn.onclick = function() {
            // 1.创建对象
            const xhr = new XMLHttpRequest();
            // 2.初始化  设置请求方法和url
            xhr.open('GET', 'http://127.0.0.1:8000/server?a=100');

            // 3.发送
            xhr.send();
            // 4.事件绑定 处理服务端返回的结果
            // on when 当...的时候
            // readystate 是xhr对象中的属性，表示状态0 1 2 3 4 
            // change 改变
            xhr.onreadystatechange = function() {
                // 判断(服务端返回了所有结果)
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        // 处理结果 行 头 空行 体
                        // 1.响应行
                        // console.log(xhr.status); // 状态码
                        // console.log(xhr.statusText); // 状态字符串
                        // console.log(xhr.getAllResponseHeaders()); //所有响应头
                        // console.log(xhr.response);
                        result.innerHTML = xhr.response;
                    }
                }
            }
        }
    </script>
</body>

</html>
```

2.POST

``` HTML
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            border: solid 1px red;
        }
    </style>
</head>

<body>
    <div id="result"></div>
    <script>
        const result = document.getElementById('result');
        result.addEventListener("mouseover", function() {
            // 1.创建对象
            const xhr = new XMLHttpRequest();
            // 2.初始化 设置类型和URL
            xhr.open('POST', 'http://127.0.0.1:8000/server');
            // 设置请求头
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencode');
            xhr.setRequestHeader('name', 'atguigu');
            // 3.发送
            xhr.send('a=100&b=200&c=300');
            // 4.事件绑定
            xhr.onreadystatechange = function() {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        result.innerHTML = xhr.response;
                    }
                }
            }
        })
    </script>
</body>

</html>
```

3.JSON

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result {
            width: 200px;
            height: 200px;
            border: solid 1px red;
        }
    </style>
</head>

<body>
    <div id="result"></div>
    <script>
        const result = document.getElementById('result');
        window.onkeydown = function() {
            // 1.发送请求
            const xhr = new XMLHttpRequest();
            xhr.responseType = 'json';
            // 初始化
            xhr.open('GET', 'http://127.0.0.1:8000/json-server');
            // 发送
            xhr.send();
            // 事件绑定
            xhr.onreadystatechange = function() {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        // console.log(xhr.response);
                        // result.innerHTML = xhr.response;
                        // 手动对数据进行转化
                        // let date = JSON.parse(xhr.response);
                        // result.innerHTML = date.name;
                        // 自动转化
                        console.log(xhr.response);
                        result.innerHTML = xhr.response.name;
                    }
                }
            }
        }
    </script>
</body>

</html>
```

4.IE缓存问题

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IE缓存问题</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            border: solid 1px blue;
        }
    </style>
</head>

<body>
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.getElementsByTagName('button')[0];
        const result = document.querySelector('#result');

        btn.addEventListener('click', function() {
            const xhr = new XMLHttpRequest();
            xhr.open("GET", 'http://127.0.0.1:8000/ie?t=' + Date.now());
            xhr.send();
            xhr.onreadystatechange = function() {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        result.innerHTML = xhr.response;
                    }
                }
            }
        })
    </script>
</body>

</html>
```

5.超时与网络异常

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>请求超时与网络异常</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            border: solid 1px yellow;
        }
    </style>
</head>

<body>
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.getElementsByTagName('button')[0];
        const result = document.querySelector('#result');
        btn.addEventListener('click', function() {
            const xhr = new XMLHttpRequest();
            // 超时设置 2s
            xhr.timeout = 2000;
            xhr.ontimeout = function() {
                    alert("网络异常！");
                }
                // 网络异常回调
            xhr.onerror = function() {
                alert("请检查你的网络！");
            }
            xhr.open("GET", 'http://127.0.0.1:8000/delay');
            xhr.send();
            xhr.onreadystatechange = function() {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        result.innerHTML = xhr.response;
                    }
                }
            }
        })
    </script>
</body>

</html>
```

6.取消请求

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>取消请求</title>
</head>

<body>
    <button>点击发送</button>
    <button>点击取消</button>
    <script>
        const btns = document.querySelectorAll('button');
        let x = null;
        btns[0].onclick = function() {
            x = new XMLHttpRequest();
            x.open('GET', 'http://127.0.0.1:8000/delay');
            x.send();
        }

        // abort()
        btns[1].onclick = function() {
            x.abort();
        }
    </script>
</body>

</html>
```

7.重复请求问题

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>重复请求问题</title>
</head>

<body>
    <button>点击发送</button>
    <button>点击取消</button>
    <script>
        const btns = document.querySelectorAll('button');
        let x = null;
        // 标识变量
        let isSending = false; // 是否正在发送AJAX请求


        btns[0].onclick = function() {
            // 判断标识变量
            if (isSending) x.abort(); // 如果正在发送请求，则取消该请求，创建一个新的请求

            x = new XMLHttpRequest();
            // 修改标识变量的值
            isSending = true;
            x.open('GET', 'http://127.0.0.1:8000/delay');
            x.send();
            x.onreadystatechange = function() {
                if (x.readyState === 4) {
                    // 修改标识变量
                    isSending = false;
                }
            }
        }

        // abort()
        btns[1].onclick = function() {
            x.abort();
        }
    </script>
</body>

</html>
```

以上7个问题所用到的JS脚本

```JavaScript
// 1.引入express
const express = require('express');

// 2.创建应用对象
const app = express();

// 3.创建路由规则
// request是对请求报文的封装
// response是对响应报文的封装
app.get('/server', (request, response) => {
    // 设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    // 设置响应
    response.send('HELLO AJAX -2');
});

//IE缓存问题
app.get('/ie', (request, response) => {
    // 设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    // 设置响应
    response.send('HELLO IE - 3');
});

//延时调用
app.get('/delay', (request, response) => {
    // 设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    // 设置响应
    setTimeout(() => {
        response.send('延时响应');
    }, 3000);
});

app.all('/server', (request, response) => {
    // 设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    // 设置响应
    response.send('HELLO AJAX POST');
});

app.all('/json-server', (request, response) => {
    // 设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // 响应一个数据
    const date = {
        name: 'atguigu'
    };
    let str = JSON.stringify(date);
    // 设置响应
    response.send(str);
});


// 4.监听端口启动服务
app.listen(8000, () => {
    console.log("服务已启动, 8000端口监听中....");
})
```
