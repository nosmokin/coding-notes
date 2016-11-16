### Quirks Detection
```javascript
var hasDontEnmuQuirk = function() {
    var o = {
        toString: function() {}
    };
    for (var prop in o) {
        if (prop == "toString") {
            return false;
        }
        return true;
    }
}();
```
### 能力检测
```javascript
function isHostMethod(object, property) {
    var t = typeof object[property];
    return t == 'function' || (!!(t == 'object' && object[property])) ||
        t == 'unknown';
}
```

### 是否支持Netscape风格插件
```javascript
var hasNSPlugins = !!(navigator.plugins
    && navigator.plugins.length);
```

### 是否具有DOM1级规定的能力
```javascript
var hasDOM1 = !!(document.getElementById
    && document.createElement
    && document.getElementsByTagName);
```

### 识别呈现引擎
```javascript
var client = function() {
    var engine = {
        //呈现引擎
        ie: 0,
        gecko: 0,
        webkit: 0,
        khtml: 0,
        opera: 0,
        //具体版本号
        ver: null
    };

    var browser = {
        //浏览器
        ie: 0,
        firefox: 0,
        safari: 0,
        konq: 0,
        opera: 0,
        chrome: 0,
        //具体版本号
        ver: null
    };
    //检测呈现引擎和浏览器
    var ua = navigator.userAgent;
    if (window.opera) {
        engine.ver = browser.ver = window.opera.version();
        engine.opera = browser.opera = parseFloat(engine.ver);
    } else if (/AppleWebKit\/(\S+)/.test(ua)) {
        engine.ver = RegExp["$1"];
        engine.webkit = parseFloat(engine.ver);
        if(/Chrome\/(\S+)/.test(ua)){
            browser.ver = RegExp["$1"];;
            browser.chrome = parseFloat(browser.ver);
        } else if (/Version\/(\S+)/.test(ua)) {
            browser.ver = RegExp["$1"];;
            browser.safari = parseFloat(browser.ver);
        } else {
            var safariVersion = 1;
            if(engine.webkit < 100){
                safariVersion = 1;
            } else if (engine.webkit < 312) {
                safariVersion = 1.2;
            } else if (engine.webkit < 412) {
                safariVersion = 1.3;
            } else {
                safariVersion = 2;
            }
            browser.safari = browser.ver = safariVersion;
        }
    } else if (/KHTML\/(\S+)/.test(ua)) {
        engine.ver = browser.ver = RegExp["$1"];
        engine.khtml = browser.konq = parseFloat(engine.ver);
    } else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)) {
        engine.ver = RegExp["$1"];
        engine.gecko = parseFloat(engine.ver);
        if (/Firefox\/(\S+)/.test(ua)){
            browser.ver = RegExp["$1"];;
            browser.firefox = parseFloat(browser.ver);
        }
    } else if (/MSIE ([^;]+)/.test(ua)) {
        engine.ver = browser.ver = RegExp["$1"];
        engine.ie = browser.ie = parseFloat(engine.ver);
    }
    return {
        engine: engine,
        browser: browser
    };
}();
```
