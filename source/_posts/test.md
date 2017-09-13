---

test

---

﻿[TOC]

## 简述

函数节流，throttle
函数去抖，debounce

以resize事件为例：
- 函数节流：降低触发回调的频率，比如限定200ms触发一次，函数节流的核心是，让一个函数不要执行的太频繁，减少一些过快的调用来节流。
- 函数去抖：对于一定时间段的连续的函数调用，只让其执行一次。


## 场景

throttle：
（需要间隔一定时间触发回调来控制函数调用频率）
- DOM元素拖拽（mousemove）
- 鼠标移动距离（mousemove）
- 射击游戏 （mousedown／keydown）
- canvas模拟画布（mousemove）
- 输入框联想（keyup）
- 滚动监听（scroll）

debounce：
（对于连续的事件响应我们只需要执行一次回调）
- resize／scroll 统计触发事件
- 文本验证或输入联想

## 实现

防抖：
```javascript
function _debounce(func, wait) {
    let timer;
    return () => {
        let _this = this,
            _args = arguments;
        clearTimeout(timer);
        timer = setTimeout(() => func.apply(_this, _args), wait);
    }
}

let debounce = _debounce(() => console.log('TODO ...'), 500);

window.onresize = e => debounce();
```

节流：
```javascript
function _throttle(func, wait) {
    let last, deferTimer;
    return () => {
        let _this = this,
            _args = arguments,
            now = +new Date();
        if(last && now < last + wait) {
            clearTimeout(deferTimer);
            deferTimer = setTimeout(() => {
                last = now;
                func.apply(_this, _args);
            }, wait);
        } else {
            last = now;
            func.apply(_this, _args);
        }
    }
}

let throttle = _throttle(() => console.log('TODO ...'), 100);

window.onresize = () => throttle();
```

以上是根据窗口的resize事件做简单的防抖和节流，具体场景需要差别对待，但基本思路如此。

## 参考

[实例解析防抖和节流函数](http://bubkoo.com/2017/01/18/debouncing-throttling-explained-examples/)
[debouncing-throttling-explained-examples](https://css-tricks.com/debouncing-throttling-explained-examples/)


