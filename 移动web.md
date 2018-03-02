# 移动端

- [监听页面返回的方法](#监听页面返回的方法)
- [缓存的保存与读取](#缓存的保存与读取)
- [时间戳与时间之间的转换](#时间戳与时间之间的转换)

## 公共方法`common.js`

> 根据rem来控制不同设备适应

```js
// 自执行
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
    w();
    var t;
    window.addEventListener("resize", function() {
        clearTimeout(t);
        t = setTimeout(w, 1000/60);
    }, false);
})();
```

> 然后在重置css中设置

```css
/*重置样式*/
html{font-size:calc(100vw/7.5)}
```

公共方法



```js
var juejin_cF = (function(){
    /*listenBackward
        监听页面返回事件
    * */
    var listenBackward = function(callbackFunc){
       ...
    }
    
    var pushHistory = function () { 
       ...
    } 
    
    /*saveJson_localStorage
        保存缓存
        参数：保存的缓存名称，保存的内容()
    * */
    var saveJson_localStorage = function (target_item,data_json){
        ...
    }
    
    /*readJson_localStorage
        读取缓存
        参数：读取的缓存名称
        返回值：读取的内容   
    * */
    //读取缓存，传入要读取的词条(字符串)
    var readJson_localStorage = function (target_item){
        ...
    }
    
    /*get_localDateStr：
        时间戳转为yy-mm-dd格式日期
        参数：时间戳
        返回值：相应yy-mm-dd格式日期
    * */
    //获取yyyy-mm-dd格式日期，传入时间戳
    var get_localDateStr = function (dateTime){
       ...
    }
        
    /*turnToFunc：
        将字符串转为函数
        参数：字符串
        回调：相应名称的函数
     * */   
    //将字符串转为函数并调用
    var turnToFunc = function (fn_str){ 
        ...
    }
    
    /*pageConfig
        返回页面配置信息
     * */
    var pageConfig = function(){
        ...
    }

    /*
    * getTemplate(id tplID)  参数,模板容器的id
    * getTemplate.assign(key,value)  赋值,将数据赋值到模板中
    * getTemplate.display(str elementID)   加载模板内容,将模板内容放置到elementID中
    *           如果elementID为空，说明模板容器与放置容器是同一个
    * getTemplate.action.setLimitR/setLimitL(str)  设置左右定界符
    *
    */
    var getTemplate = function(tplID){
        ...
    };
    
    /**处理模板数据
     * 参数：
     * arrayParam   数组（原始数据，需含id字段），
     * domId        目标容器id，
     * templateId   调用模板的id，
     * domClass     需要定义给模板容器的类，
     * link         需跳转的页面路由
     * 备注：根据数组各元素id生成模板容器（作为目标容器的子节点）
     */
    var modifyTemplates = function (arrayParam,domId,templateId,domClass){
        ...
    }
    
    /**引用模板
     * 参数：json格式数据（obj）,对应节点id
     * 
     */
    var setTemplates = function (tmpObj,targetId,raw){
      ...
    }

    /**商品描述文字处理
     * 参数：商品数据(json数组),需要处理的字段(key),保留的长度(字数)
     * 返回：处理后的商品数据
     */
    var textProcess = function (arrayData,key_Name,viewLength){
        ...
    }
    
    /**
     * 通过元素内容获取数组下标
     * 参数：
     * 返回：
     */
    var getIndex = function(arrayData,keyName,str){
        ...
    }
    
    /**
     * 数组元素赋值
     * 参数：
     * 返回：
     */
    var setValue = function(arrayData,keyName,str,index){
       ...
    }

    return {
        listenBackward:listenBackward,
        saveJson_localStorage:saveJson_localStorage,
        readJson_localStorage:readJson_localStorage,
        get_localDateStr:get_localDateStr,
        turnToFunc:turnToFunc,
        pageConfig:pageConfig,
        modifyTemplates:modifyTemplates,
        textProcess:textProcess,
        getIndex:getIndex,
        setValue:setValue
    }
})();
```

### 监听页面返回的方法

```js
/*listenBackward
监听页面返回事件
* */
function lisenBackward (cb) {
    pushHistory()
    window.addEventListener('popstate', function (e) {
        turnToFunc(cb);
    }, false)
}

function pushHistory () {
	var state = { 
    	title: "title", 
    	url: "#"
    }; 
    window.history.pushState(state, "title", "#"); 
}
```

[↑返回top](#移动端技巧)


### 缓存的保存与读取

```js
/* saveLocalStorage
	保存缓存
	参数：保存的缓存名称，保存的内容()
* */

function saveLocalStorage (name, content) {
    window.localStorage.setItem(name, JSON.stringify(content))
}

/*readJson_localStorage
 	读取缓存
 	参数：读取的缓存名称
 	返回值：读取的内容 	
* */
//读取缓存，传入要读取的词条(字符串)

function getLocalStorage (name) {
    return JSON.parse(window.localstorage.getItem(name))
}
```

[↑返回top](#移动端技巧)

### 时间戳与时间之间的转换

```js
/*getTime：
 	时间戳转为yy-mm-dd格式日期, 或者 hh : mm : ss
 	参数：时间戳
 	返回值：相应yy-mm-dd格式日期
* */
//获取yyyy-mm-dd格式日期，传入时间戳
function getTime (dateTime){
	var tempDay = new Date(dateTime * 1000);
	var tempDate = tempDay.getFullYear()+'-'+(tempDay.getMonth()+1)+'-'+tempDay.getDate();
	return tempDate;
}
function add0 (t) {return t > 10 ? t : '0' + t} 
function getTime2 (dateTime){
	var tempDay = new Date(dateTime * 1000);
    var hours = tempDay.getHours();
    var minutes = tempDay.getMinutes();
    var seconds = tempDay.getSeconds();
    var tempDate = add0(hours)+':'+add0(minutes)+':'+add0(seconds);
	return tempDate;
}
```

[↑返回top](#移动端技巧)
