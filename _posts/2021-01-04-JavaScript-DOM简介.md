# DOM文档对象模型

## DOM简介

     宿主对象  DOM  BOM
     DOM  Document Object Model 文档对象模型

     js中通过DOM来对HTML文档进行操作
     只要理解了DOM就可以随心所欲的操作WEB页面

     文档 - 表示的就是整个的HTML网页文档
     对象 - 表示将网页中的每一个部分都转换成为了一个对象
     模型 - 使用模型来表示对象之间的关系,这样方便我们获取对象 

``` html

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <!-- 
        节点:Node,构成网页的最基本的组成部分  网页中的每一部分都可以称作一个节点
        事件:就是文档或浏览器窗口中发生的一些特定的瞬间
     -->

    <!-- <button id="btn" onclick="alert('讨厌');">button</button> -->
    <!-- <button id="btn" ondblclick="alert('讨厌');">button</button> -->
    <!-- <button id="btn" onmousemove="alert('讨厌');">button</button> -->


    <!--
    <script>
        var btn = document.getElementById("btn");
        btn.innerHTML = "I'm a btn";
    </script> 
    -->
    <button id="btn">I'm a button</button>
    <script>
        var btn = document.getElementById("btn");
        btn.onclick = function () {
            alert("NO!");
        }
    </script>
</body>

</html>
```
