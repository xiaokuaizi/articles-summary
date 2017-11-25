### 对象深拷贝

#### 方法一：JSON.parse(JSON.stringify(obj))

```
var obj = { 
        a: 1,
        b:[1,2],
        c:{
            name:"ddd",
            d:[3],
            e:function(){console.log(1)}
        }
    }
var newObj = JSON.parse(JSON.stringify(obj))

```
运行结果：

![](https://xiaokuaizi.github.io/images-github/20171125-1.jpeg)

##### 对象obj.c中的函数e被忽略

优点：

- 对于某些对象来说，实现方式简单

缺点：
- 抛弃对象的constructor
- RegExp对象是无法通过这种方式深复制
- 函数无法被拷贝

#### 方法二：递归

```
var deepCopy = function(obj){
    
    var newObj;
    if(Object.prototype.toString.call(obj) === '[object Object]'){
         newObj = {};
          for( var i in obj){
            newObj[i] = arguments.callee(obj[i]);
          }
    }else if(Object.prototype.toString.call(obj) === '[object Array]'){
          newObj = [];
          for( var i in obj){
            newObj.push(arguments.callee(obj[i]));
          }
    }else{
        newObj = obj;
    }
    return newObj;
};

var obj = { 
        a: 1,
        b:[1,2],
        c:{
            name:"ddd",
            d:[3],
            e:function(){console.log(1)}
        }
    }

var newObj = deepCopy(obj)

```

运行结果：

![](https://xiaokuaizi.github.io/images-github/20171125-2.jpeg)


##### 知识扩展

$.extend实现：

[官网地址](https://github.com/jquery/jquery/blob/master/src/core.js)

```
jQuery.extend = jQuery.fn.extend = function() {
    var options, name, src, copy, copyIsArray, clone,
        target = arguments[ 0 ] || {},
        i = 1,
        length = arguments.length,
        deep = false;
  
    // Handle a deep copy situation
    if ( typeof target === "boolean" ) {
        deep = target;
  
        // Skip the boolean and the target
        target = arguments[ i ] || {};
        i++;
    }
  
    // Handle case when target is a string or something (possible in deep copy)
    if ( typeof target !== "object" && !jQuery.isFunction( target ) ) {
        target = {};
    }
  
    // Extend jQuery itself if only one argument is passed
    if ( i === length ) {
        target = this;
        i--;
    }
  
    for ( ; i < length; i++ ) {
  
        // Only deal with non-null/undefined values
        if ( ( options = arguments[ i ] ) != null ) {
  
            // Extend the base object
            for ( name in options ) {
                src = target[ name ];
                copy = options[ name ];
  
                // Prevent never-ending loop
                if ( target === copy ) {
                    continue;
                }
  
                // Recurse if we're merging plain objects or arrays
                if ( deep && copy && ( jQuery.isPlainObject( copy ) ||
                    ( copyIsArray = jQuery.isArray( copy ) ) ) ) {
  
                    if ( copyIsArray ) {
                        copyIsArray = false;
                        clone = src && jQuery.isArray( src ) ? src : [];
  
                    } else {
                        clone = src && jQuery.isPlainObject( src ) ? src : {};
                    }
  
                    // Never move original objects, clone them
                    target[ name ] = jQuery.extend( deep, clone, copy );
  
                // Don't bring in undefined values
                } else if ( copy !== undefined ) {
                    target[ name ] = copy;
                }
            }
        }
    }
  
    // Return the modified object
    return target;
};
```

#### 方法三：$.extend

```
var obj = { 
        a: 1,
        b:[1,2],
        c:{
            name:"ddd",
            d:[3],
            e:function(){console.log(1)}
        }
    }
var newObj =  $.extend(true,{},obj)
```
运行结果： 同上

##### 定义：
将一个或多个对象的内容合并到目标对

#### 用法：

![](https://xiaokuaizi.github.io/images-github/20171125-3.jpeg)

###### Object.assign,Object.assign经代码测试均属于浅拷贝

