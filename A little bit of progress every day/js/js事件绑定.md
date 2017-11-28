## js事件绑定

### 一、在DOM元素中直接绑定
JavaScript支持在标签中直接绑定事件

语法：onXXX="JavaScript Code"
- onXXX为事件名称。例如，鼠标单击事件 onclick
- JavaScript Code 为处理事件的JavaScript代码，一般是函数

示例：
```
// 原生函数
<input onclick="alert('message')" type="button" value="点击我，弹出警告框" />

// 自定义函数
 <input onclick="myAlert()" type="button" value="点击我，弹出警告框" />
```


### 二、在JavaScript代码中绑定
语法：elementObject.onXXX=function(){
    // 事件处理代码
}

- elementObject 为DOM对象，即DOM元素。
- onXXX 为事件名称。

### 三、绑定事件监听函数
语法： elementObject.addEventListener(eventName,handle,useCapture);

语法： elementObject.attachEvent(eventName,handle);

- elementObject：DOM元素
- eventName： eventName，addEventListener事件名称没有‘on’
- handle： 事件名称
- useCapture：Boolean类型，是否使用捕获，一般用false（冒泡）

[参考链接](https://www.cnblogs.com/javawebstudy/p/5266168.html)



