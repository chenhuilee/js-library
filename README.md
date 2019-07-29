# test

#### //判斷是否為行動設備
```js
function isMobileDev() {
    if (/ipad/i.test(navigator.userAgent.toLowerCase())) {
        //return "ipad";    // 目前是用ipad瀏覽
        return true;
    }
    else if (/iphone|ipod|android|blackberry|mini|windows\sce|palm/i.test(navigator.userAgent.toLowerCase())) {
        //return "mobile";  // 目前是用手機瀏覽
        return true;
    }
    else {
        //return "pc";      // 目前是用電腦瀏覽
        return false;
    }
}
```

#### //string.Blength() 傳回字串的byte長度 https://dotblogs.com.tw/aquarius6913/2013/04/25/102272

```js
String.prototype.Blength = function () {
    var arr = this.match(/[^\x00-\xff]/ig);
    return arr == null ? this.length : this.length + arr.length;
}
```
