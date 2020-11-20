

### 1.概述

​	FormData类型是在XMLHttpRequest 2级定义的, 它是为序列化列表以及创建与表单格式相同的数据(用于XHR传输)
提供便利。

### 2.构造函数

​	创建一个formData对象实例几种方式

##### 1.创建一个空对象实例

```js
var formdata = new FormData();  // 此时可以调用append()方法来添加数据
```

##### 2.使用已有表单来初始化一个对象实例

```js
<form id="myForm" action="" method="post">
    <input type="text" name="name">名字
    <input type="password" name="psw">密码
    <input type="submit" value="提交">
</form>
//我们可以使用这个表单元素作为初始化参数，来实例化一个formData对象
// 获取页面上的form表单
var form = document.getElementById('myForm');
// 用表单来初始化
var formdata = new FormData(form);
// 根据name来访问表单中的字段
var name = formdata.get(name) // 获取用户名
var psw = formdata.get(psw) // 获取密码
// 可以在此基础上添加其他数据
formdata.append('token','sdadas')
```

### 3.操作方法

````js
FormData里面的存储数据形式为, key／value组成的一条数据 key是惟一的 一个key可以对应多个value值
如果使用表单初始化, 每一个表单字段对应一条数据, 它们的HTML name属性值是key值, 它们的value属性对应value值
// 获取值
get(key)  // 返回key为name的第一个值
getAll(key); // 返回key为name的所有值 是一个数组
// 设置修改值
set(key,value)  // 如果key值不存在 则为创建了一条新数据
// 删除值
delete(key)
// 判断是否存在对应的key值
has(key)  // 存在返回true 反之返回false
// 遍历 了解
可以通过entries()来获取一个迭代器, 然后遍历所有的数据
 		fd.append('k',1)
        fd.append('k',2)
        fd.append('k',3)
        fd.append('k1',4)
        fd.append('k',5);
var i = formdata.entries();
i.next()// 返回 	 一个对象 done 为false vale为数据 一个数组[key, value]  按照 添加的数据顺序返回
					//直到 done 为true 返回到最后一个value为undefined 
````



### 4.发送数据

````js
// var xhr = new XMLHttpRequest();
// xhr.open("post",url);
// xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
// xhr.send(formData);
// 实现文件的异步上传
````

### 5.JQuery实例

````js
$({
    method : 'post',
    url : 'http://wwww.XXX:XXX/api/XXX',
    data :  formdata,
    dataType : 'JSOn',
    cache : false,  // 不缓存
    processData: false,  // jquery不要去处理发送的数据
    contentType: false,  // jquery不要去设置Content-Type请求头
    success : function(res){
        // 成功回调
    }
    
})


/**        了解
 * 将以base64的图片url数据转换为Blob文件格式
 * @param urlData 用url方式表示的base64图片
 */
function convertBase64UrlToBlob(urlData) {
    var bytes = window.atob(urlData.split(',')[1]); //去掉url的头，并转换为byte
    //处理异常,将ascii码小于0的转换为大于0
    var ab = new ArrayBuffer(bytes.length);
    var ia = new Uint8Array(ab);
    for(var i = 0; i < bytes.length; i++) {
        ia[i] = bytes.charCodeAt(i);
    }
    return new Blob([ab], {
        type: 'image/png'
    });
}
````

