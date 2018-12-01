# ##  1.BigSpinach_utils.js

```javascript
var utils = (function () {
    //=>把类数组转换为数组（兼容所有的浏览器）
    function toArray(classAry) {
        var ary = [];
        try {
            ary = Array.prototype.slice.call(classAry);
        } catch (e) {
            for (var i = 0; i < classAry.length; i++) {
                ary[ary.length] = classAry[i];
            }
        }
        return ary;
    }

    //=>把JSON格式的字符串转换为JSON格式的对象
    function toJSON(str) {
        return "JSON" in window ? JSON.parse(str) : eval('(' + str + ')');
    }

    return {
        toArray: toArray,
        toJSON: toJSON
    }
})();
```



##  ### 数据类型检测

> 基于Object.prototype.toString.call(item);
>
> 返回 的是数据格式类型为 [object xxoo]
>
> ​				[object String]
>
> 配合 RegExp 编写一个判断数据类型的方法
>
> new RegEx('\\[ object '+'String\\]').test(Object.prototype.toString.call('字符串'));
>
> new RegEx('\\[ object '+'Function\\]').test(Object.prototype.toString.call(fn));



```javas
~function () {
    var obj = {
        isNumber: 'Number',
        isString: 'String',
        isBoolean: 'Boolean',
        isNull: 'Null',
        isUndefined: 'Undefined',
        isPlanObject: 'Object',
        isArray: 'Array',
        isRegExp: 'RegExp',
        isFunction: 'Function'
    };
    var check = {};
    for (var key in obj) {
        if (obj.hasOwnProperty(key)) {
            check[key] = (function (classValue) {
                return function (val) {
                    return new RegExp('\\[object ' + classValue + '\\]').test(Object.prototype.toString.call(val));
                }
            })(obj[key]);
        }
    }
    window.check = check;
}();

```



![1541751101573](C:\Users\82113\AppData\Local\Temp\1541751101573.png)

![1541751194990](C:\Users\82113\AppData\Local\Temp\1541751194990.png)





### 全兼容的getElementsByClassName()

```javascript
Node.prototype.queryElementsByClassName = function queryElementsByClassName() {
    if (arguments.length === 0) return [];
    var strClass = arguments[0],
        nodeList = utils.toArray(this.getElementsByTagName('*'));
    strClass = strClass.replace(/^ +| +$/g, '').split(/ +/);
    for (var i = 0; i < strClass.length; i++) {
        var reg = new RegExp('(^| +)' + strClass[i] + '( +|$)');
        for (var k = 0; k < nodeList.length; k++) {
            if (!reg.test(nodeList[k].className)) {
                nodeList.splice(k, 1);
                k--;
            }
        }
    }
    return nodeList;
};	
```

