# Javascript Snippets

If variable was not undefined OR If the desired variable exists

```js
    if (typeof L !== "undefined") {......}
```

custom theme copyright text in console 

```js
function initConsoleMsg() {
    if (navigator.userAgent.toLowerCase().indexOf("chrome") > -1) {
        const t = ["background: #1A1818;", "color: #fab162", "padding: 12px 20px"].join(";");
        console.log("%c Tappezzeria Novecento | To my father!❤️ Code and Design by Giacomo Mottin. https://www.linkedin.com/in/giacomo-mottin-bb38bba0/", t)
    } else
        window.console && window.console.log("Tappezzeria Novecento | To my father!❤️ Code and Design by Giacomo Mottin. https://www.linkedin.com/in/giacomo-mottin-bb38bba0/")
}
initConsoleMsg();
```

