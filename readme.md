
Q：[ios键盘被覆盖](https://segmentfault.com/q/1010000012033973)

A：解决ios系统里 input/textarea/contenteditable 固定底部，点击输入框键盘被覆盖统一解决方案：（亲测）

针对ios系统兼容
1.version < ios11：利用原生的scrollIntoView()&&scrollIntoViewIfNeeded();

```
$('input').focus(function(){
    settimeout(()=>{
        $('input')[0].scrollIntoView();
        $('input')[0].scrollIntoViewIfNeeded();
    }, 500)
})
```
2.ios11.0 <= version < ios12：利用定位方法以及原生方法
```
$('input').focus(function(){
    $('input').css({'position':'absolute'});
    setTimeout(function(){
        $('input')[0].scrollIntoView();
        $('input')[0].scrollIntoViewIfNeeded();
    },500);
})
$('input').blur(function(){
    $('input').css({'position':'fixed'});
    setTimeout(function(){
        $('input')[0].scrollIntoView();
        $('input')[0].scrollIntoViewIfNeeded();
    },500);
})
```
3.>= ios12：系统兼容得很好，只需要处理好微信input失焦后会卡顿需要模拟点击页面才会还原。
```
$('input').blur(function(){
    let scrollTop = document.body.scrollTop;
    window.scroll(0 ,scrollTop);
})
```
