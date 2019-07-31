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

#### 轉英文大寫
```js
// OnKeyUp="LmtUpperStr(this);"
function LmtUpperStr(o) {
    o.value = o.value.toUpperCase();
}
```

#### 定義數字格式
```js
/*
* Number.prototype.format(n, x)
* @param integer n: length of decimal
* @param integer x: length of sections
*/
Number.prototype.format = function (n, x) {
    var re = '\\d(?=(\\d{' + (x || 3) + '})+' + (n > 0 ? '\\.' : '$') + ')';
    return this.toFixed(Math.max(0, ~ ~n)).replace(new RegExp(re, 'g'), '$&,');
};
```

#### 
```js
String.prototype.trim = function () {
    return this.replace(/^\s+|\s+$/g, "");
}
String.prototype.ltrim = function () {
    return this.replace(/^\s+/, "");
}
String.prototype.rtrim = function () {
    return this.replace(/\s+$/, "");
}
```

#### 移除字串左右空白字元
```js
function trim(s) {
    return s.replace(/^\s*|\s*$/g, "")
}
```

#### 傳回字串的byte長度
```js
//string.Blength() https://dotblogs.com.tw/aquarius6913/2013/04/25/102272
String.prototype.Blength = function () {
    var arr = this.match(/[^\x00-\xff]/ig);
    return arr == null ? this.length : this.length + arr.length;
}
```

#### 轉英文大寫
```js
// OnKeyUp="LmtUpperStr(this);"
function LmtUpperStr(o) {
    o.value = o.value.toUpperCase();
}
```

#### 計算Byte數, 中文字算2個byte,英文字算1個byte
```js
// onkeyup="LmtStrBLen(this,40)"
function LmtStrBLen(o, maxlen) {
    //    var maxlen = o.getAttribute ? parseInt(o.getAttribute("maxlength")) : "";
    var s = o.value;
    //    if (o.getAttribute && s.Blength() > maxlen) {
    if (s.Blength() > maxlen) {
        //            window.event.keyCode = 0;
        alert("本欄位輸入長度不可超過 " + maxlen + " 位元。");
        s = SubStrBLen(s, 0, maxlen);
        o.value = s;
    }
}
```

#### 計算字數, 不管中文字,英文字都算一個字
```js
// onkeyup="LmtStrCLen(this,40)"
function LmtStrCLen(o, maxlen) {
    var s = o.value;
    if (s.length > maxlen) {
        //        window.event.keyCode = 0;
        alert("本欄位輸入長度不可超過 " + maxlen + " 個字。");
        s = s.slice(0, maxlen);
        o.value = s;
    }
}
```

#### 字串長度切割, 以bytes計算
```js
function SubStrBLen(str, startInBytes, lengthInBytes) {
    // http://stackoverflow.com/questions/11200451/extract-substring-by-utf-8-byte-positions
    var resultStr = '';
    var startInChars = 0;
    var end = startInChars + lengthInBytes - 1;
    for (n = startInChars; startInChars <= end; n++) {
        ch = str.charCodeAt(n);
        end -= (ch < 128) ? 1 : (str.charAt(n)).Blength();
        resultStr += str.charAt(n);
    }
    return resultStr;
}
```

#### 限整數欄位 (0-9)
```js
// onKeyPress='validateNumber(event)'
function validateNumber(evt) {
    if (evt.keyCode != 8) {
        var theEvent = evt || window.event;
        var key = theEvent.keyCode || theEvent.which;
        key = String.fromCharCode(key);
        var regex = /[0-9]/;
        if (!regex.test(key)) {
            theEvent.returnValue = false;
            if (theEvent.preventDefault) theEvent.preventDefault();
        }
    }
}
```

#### 限實數欄位 (可負值,小數點)
```js
// onKeyPress='validateDecimal(event)'

function validateDecimal_old(evt) {
    if (evt.keyCode != 8) {
        var theEvent = evt || window.event;
        var key = theEvent.keyCode || theEvent.which;
        key = String.fromCharCode(key);
        regex = /^(\-?)\d*(\.?\d*)$/;
        if (!regex.test(key)) {
            theEvent.returnValue = false;
            if (theEvent.preventDefault) theEvent.preventDefault();
        }
    }
}

function validateDecimal(evt) {
    var thisEvent = evt || window.event;
    var keycode = (thisEvent.keyCode ? thisEvent.keyCode : thisEvent.which);
    if (keycode == 8) {
        thisEvent.returnValue = false;
        if (thisEvent.preventDefault) thisEvent.preventDefault();
    }
    else {
        var key = String.fromCharCode(keycode);
        regex = /^(\-?)\d*(\.?\d*)$/;
        if (!regex.test(key)) {
            thisEvent.returnValue = false;
            if (thisEvent.preventDefault) thisEvent.preventDefault();
        }
    }
}
```

#### 數值欄空白自動填入0
```
//onblur="validateEmptyNumber(this)"
function validateEmptyNumber(o) {
    if (o.value == '') {
        o.value = 0;
    }
}
```

####  驗證 email 格式
```
// onblur='validateEmail(this);' 
function validateEmail(o) {
    var mailformat = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    // /^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$/
    if (!mailformat.test(o.value)) {
        alert('Email 格式錯誤 !!');
        o.focus();
        return false;
    }
}
```

#### 
```
// 欄位必須有值
// onblur='validateRequireField(this);' 
function validateRequireField(o) {
    if (o.value == "") {
        alert("請輸入數值");
        o.select();
        return false;
    }
}
```

#### 中文值檢測
```
function isChinese(name) {
    if (name.length == 0)
        return false;
    for (i = 0; i < name.length; i++) {
        if (name.charCodeAt(i) > 128)
            return true;
    }
    return false;
}
```

#### 讀取網址參數,如 http://www.abc.com/test.php?modseq=100 取得modseq的get參數值，即tSeq=100 
```
function getQueryString(paramName) {
    //paramName 為 參數名稱
    paramName = paramName.replace(/[\[]/, "\\\[").replace(/[\]]/, "\\\]").toUpperCase();
    var reg = "[\\?&]" + paramName + "=([^&#]*)";
    var regex = new RegExp(reg);
    var regResults = regex.exec(window.location.href.toUpperCase());
    if (regResults == null) return "";
    else return regResults[1];
}
```

#### 系統時間
```
function ShowTime() {
    var d = new Date();
    return d.getTime();
}
```

#### 數字加入"," 符號
```
// nStr : 數字(字串)
// dec : 小數位數
function addCommas(nStr, dec) {
    if (dec == null) dec = 2;
    nStr = parseFloat(nStr).toFixed(dec);    //將小數位數補0 或四捨五入為指定位數
    nStr += '';                              //將nStr 由數字轉為字串
    x = nStr.split('.');                     //將nStr 切割為整數字串及小數字串並存入x[0] 及x[1]
    x1 = x[0];                               //宣告x1 為整數字串
    x2 = x.length > 1 ? '.' + x[1] : '';     //宣告x2 為小數字串並處理(整數字串若(x.length > 1) 成立傳回('.' + x[1]) 否則傳回(''))
    var rgx = /(\d+)(\d{3})/;                //宣告正則運算式：找到符合"(1或多個數字) + (3個數字)" 條件的字串
    // 找到時 1或多個數字) ==> 傳回給正則運算變數$1
    //        3個數字     ==> 傳回給正則運算變數$2                    
    // 重複測試正則運算式
    while (rgx.test(x1)) {                   
        //測試成功時x1= $1 + ',' + $2
        x1 = x1.replace(rgx, '$1' + ',' + '$2');            
    }
    return x1 + x2;                                                   
}
```


#### 
```
function select(sel) {
    var temp = null;
    if (temp == null) {
        temp = sel;
        sel.style.backgroundColor = "red";
    }
    else {
        temp.style.backgroundColor = "#FFFFFF";
        sel.style.backgroundColor = "red";
        temp = sel;
    }
}
```

#### 
```
function SetRecPos() {
    if (varIsEditing == false && window.event.srcElement.tagName.toUpperCase() == "TD") {
        SetRowColor(varCurrPos, 0);
        varCurrPos = window.event.srcElement.parentElement.rowIndex;
        SetRowColor(varCurrPos, 1);
    }
}
```
```
// These two functions need no customization.
function MouseOverColor(row) { row.style.backgroundColor = '#FFFFB0'; }
function MouseOutColor(row) { row.style.backgroundColor = ''; }
function MouseEvents(objRef, evt) {
    if (evt.type == "mouseover") {
        objRef.style.backgroundColor = "#FFFFB0";
    }
    else {
        if (evt.type == "mouseout") objRef.style.backgroundColor = "";
    }
}
```
#### 畫面全螢幕
```
// onload="ResizeFullScreen();"
function ResizeFullScreen() {
    window.resizeTo(screen.availWidth, screen.availHeight);
    window.moveTo(0, 0);
}
```

#### show formId 
```
function showTitle() {
    document.title = document.forms(0).id;
}
```

#### //列印 HTML
```
function printDiv(divName) {
    var printContents = document.getElementById(divName).innerHTML;
    var originalContents = document.body.innerHTML;
    document.body.innerHTML = printContents;
    window.print();
    document.body.innerHTML = originalContents;
}
```

#### // open new window
```
function OpenWindow(url, height, width, name) {
    if (!name) name = 'MyWindow';
    var screenLeft = 0, screenTop = 0;
    var defaultParams = {}

    if (typeof window.screenLeft !== 'undefined') {
        screenLeft = window.screenLeft;
        screenTop = window.screenTop;
    } else if (typeof window.screenX !== 'undefined') {
        screenLeft = window.screenX;
        screenTop = window.screenY;
    }

    var features_dict = {
        toolbar: 'no',
        location: 'no',
        directories: 'no',
        status: 'no',
        menubar: 'no',
        scrollbars: 'no',
        resizable: 'no',
        left: screenLeft + ($(window).width() - width) / 2,
        top: screenTop + ($(window).height() - height) / 2,
        width: width,
        height: height
    };
    features_arr = [];
    for (var k in features_dict) {
        features_arr.push(k + '=' + features_dict[k]);
    }
    features_str = features_arr.join(',')

    //            var qs = '?' + $.param($.extend({}, defaultParams, params));
    var win = window.open(url, name, features_str);
    win.focus();
    return false;
}
```
