# 移动端技巧

根据rem来控制不同设备适应

```js
(function(){
    function w() {
        var r = document.documentElement; //根元素html
        var a = r.getBoundingClientRect().width;
        if (a > 750 ){
            a = 750;
        } 
        rem = a / 7.5;
        r.style.fontSize = rem + "px";
    }
    var t;
    w();
    window.addEventListener("resize", function() {
        clearTimeout(t);
        t = setTimeout(w, 300);
    }, false);
})();
```

> 然后在重置css中设置

```css
/*重置样式*/
html{font-size:calc(100vw/7.5)}
```

