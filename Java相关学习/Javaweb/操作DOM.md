# DOM

DOM是一个树形结构。

要改变HTML的结构，就需要通过JavaScript来操作DOM。

操作一个DOM节点实的操作：

- 更新：更新该DOM节点的内容，相当于更新了该DOM节点表示的HTML的内容；
- 遍历：遍历该DOM节点下的子节点，以便进行进一步操作；
- 添加：在该DOM节点下新增一个子节点，相当于动态增加了一个HTML节点；
- 删除：将该节点从HTML中删除，相当于删掉了该DOM节点的内容以及它包含的所有子节点。

在操作一个DOM节点前，我们需要通过各种方式先拿到这个DOM节点。

最常用的方法是

`document.getElementById()`

+ 由于ID在HTML文档中是唯一的，所以`document.getElementById()`可以直接定位唯一的一个DOM节点。

`document.getElementsByTagName()`以及CSS选择器`document.getElementsByClassName()`。

+ 总是返回一组DOM节点。要精确地选择DOM，可以先定位父节点，再从父节点开始选择，以缩小范围。

```js
// 返回ID为'test'的节点：
var test = document.getElementById('test');

// 先定位ID为'test-table'的节点，再返回其内部所有tr节点：
var trs = document.getElementById('test-table').getElementsByTagName('tr');

// 先定位ID为'test-div'的节点，再返回其内部所有class包含red的节点：
var reds = document.getElementById('test-div').getElementsByClassName('red');

// 获取节点test下的所有直属子节点:
var cs = test.children;

// 获取节点test下第一个、最后一个子节点：
var first = test.firstElementChild;
var last = test.lastElementChild;
```

## 更新DOM

拿到一个DOM节点后，可以对它进行更新。

修改节点文本：

1. 修改`innerHTML`属性，不但可以修改一个DOM节点的文本内容，还可以直接通过HTML片段修改DOM节点内部的子树：

   ```js
   // 获取<p id="p-id">...</p>
   var p = document.getElementById('p-id');
   // 设置文本为abc:
   p.innerHTML = 'ABC'; // <p id="p-id">ABC</p>
   // 设置HTML:
   p.innerHTML = 'ABC <span style="color:red">RED</span> XYZ';
   // <p>...</p>的内部结构已修改
   ```

2. 修改`innerText`或`textContent`属性，这样可以自动对字符串进行HTML编码，保证无法设置任何HTML标签：

   ```js
   // 获取<p id="p-id">...</p>
   var p = document.getElementById('p-id');
   // 设置文本:
   p.innerText = '<script>alert("Hi")</script>';
   // HTML被自动编码，无法设置一个<script>节点:
   // <p id="p-id">&lt;script&gt;alert("Hi")&lt;/script&gt;</p>
   ```



## 插入DOM

获得了某个DOM节点，可以在这个DOM节点内插入新的DOM

如果这个DOM节点是空的，例如，`<div></div>`，那么，直接使用`innerHTML = '<span>child</span>'`就可以修改DOM节点的内容，相当于“插入”了新的DOM节点。

如果这个DOM节点不是空的，那就不能这么做，因为`innerHTML`会直接替换掉原来的所有子节点。

方法：

1. 使用`appendChild`，把一个子节点添加到父节点的最后一个子节点。

```
<!-- HTML结构 -->
<p id="js">JavaScript</p>
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
</div>

var js = document.getElementById('js'),
var list = document.getElementById('list');
list.appendChild(js);

//结果
<!-- HTML结构 -->
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
    <p id="js">JavaScript</p>
</div>
```

使用这个方法插入的节点首先会在原来的位置删除，再插入到新的位置。也可以从零创建一个新的节点，然后再插入到指定位置。

```js
var
    list = document.getElementById('list'),
    haskell = document.createElement('p');
haskell.id = 'haskell';
haskell.innerText = 'Haskell';
list.appendChild(haskell);
```

2. 把子节点插入到指定的位置可以使用`parentElement.insertBefore(newElement, referenceElement);`，子节点会插入到`referenceElement`之前。



## 删除DOM

要删除一个节点，首先要获得该节点本身以及它的父节点，然后，调用父节点的`removeChild`把自己删掉。

