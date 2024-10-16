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

Testing whether images with specific links are available or not and displaying a special element if the images are available or not for various reasons

```js
    const imageUrls = [
        "https://test.test/email-template/mail-icons/logo.png",
        "https://test.test/email-template/mail-icons/facebook-circle.png",
        "https://test.test/email-template/mail-icons/twitter-circle.png",
        "https://test.test/email-template/mail-icons/instagram-circle.png",
        "https://test.test/email-template/mail-icons/linkedin-circle.png"
    ];
    let accessibleCount = 0;
    function checkImage(url) {
        return new Promise((resolve, reject) => {
            const img = new Image();
            img.onload = () => resolve(true);
            img.onerror = () => reject(false);
            img.src = url;
        });
    }
    Promise.all(imageUrls.map(url => checkImage(url).catch(error => error)))
        .then(results => {
            accessibleCount = results.filter(result => result === true).length;
            if (accessibleCount === imageUrls.length) {
                document.getElementById('cloudflare-off').style.display = 'flex';
            } else {
                document.getElementById('cloudflare-on').style.display = 'flex';
            }
        });
```



auto translate

```js
    $(document).ready(function () {
        function translate(to) {
            var sourceLang = 'fa';
            var targetLang = to;


            $('.translate , .infoTranslate p , .infoTranslate h1,.infoTranslate h2,.infoTranslate h3 ').each(function() {
                var sourceText = $(this).text();
                if (sourceText == 'جک'){
                    $(this).text('Jack');
                }else {
                    var url = "https://translate.googleapis.com/translate_a/single?client=gtx&sl=" + sourceLang + "&tl=" + targetLang + "&dt=t&q=" + encodeURI(sourceText);

                    $.getJSON(url, function (data) {
                        var translatedText = data[0][0][0];
                        $(this).text(translatedText); // Update the span with translated text
                    }.bind(this)); // Maintain the context of 'this' inside the getJSON callback
                }
            });
        }
        translate('<?=$_COOKIE['lang']?>');
    });
```



Date Converter (miladi > shamsi) 

```js
    !(function (t, n) {
        "object" == typeof exports && "undefined" != typeof module
            ? (module.exports = n())
            : "function" == typeof define && define.amd
                ? define(n)
                : ((t = t || self).farvardin = n());
    })(this, function () {
        "use strict";
        return {
            isInvalid: function (t, n, r) {
                var o = [t, n, r].find(function (t) {
                    return isNaN(t);
                });
                if (isNaN(o) && void 0 !== o) throw new Error("Invalid Arguments passed");
            },
            outputToWhich: function (t, n, r, o) {
                switch (o) {
                    case "array":
                    default:
                        return this.outputToArray(t, n, r);
                    case "object":
                        return this.outputToObject(t, n, r);
                    case "json":
                        return this.outputToJson(t, n, r);
                    case "string":
                        var e = n < 10 ? "0" + n : n,
                            i = r < 10 ? "0" + r : r;
                        return this.outputToString(t, e, i);
                }
            },
            outputToArray: function (t, n, r) {
                return [t, n, r];
            },
            outputToObject: function (t, n, r) {
                return { year: t, month: n, day: r };
            },
            outputToJson: function (t, n, r) {
                return JSON.stringify(this.outputToObject(t, n, r));
            },
            outputToString: function (t, n, r) {
                return t + "/" + n + "/" + r;
            },
            gregorianToSolar: function (t, n, r, o) {
                var e,
                    i,
                    u,
                    s,
                    a,
                    p,
                    c = 3 < arguments.length && void 0 !== o ? o : "array";
                return (
                    (e = [0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 334]),
                        1600 < t ? ((i = 979), (t -= 1600)) : ((i = 0), (t -= 621)),
                        (a = 2 < n ? t + 1 : t),
                        (p =
                            365 * t + parseInt((a + 3) / 4) - parseInt((a + 99) / 100) + parseInt((a + 399) / 400) - 80 + r + e[n - 1]),
                        (i += 33 * parseInt(p / 12053)),
                        (p %= 12053),
                        (i += 4 * parseInt(p / 1461)),
                    365 < (p %= 1461) && ((i += parseInt((p - 1) / 365)), (p = (p - 1) % 365)),
                        (u = p < 186 ? 1 + parseInt(p / 31) : 7 + parseInt((p - 186) / 30)),
                        (s = 1 + (p < 186 ? p % 31 : (p - 186) % 30)),
                        this.isInvalid(i, u, s),
                        this.outputToWhich(i, u, s, c)
                );
            },
            solarToGregorian: function (t, n, r, o) {
                var e,
                    i = 3 < arguments.length && void 0 !== o ? o : "array",
                    u = void 0,
                    s = void 0,
                    a = void 0,
                    p = void 0,
                    c = void 0;
                for (
                    979 < t ? ((u = 1600), (t -= 979)) : (u = 621),
                        p =
                            365 * t +
                            8 * parseInt(t / 33) +
                            parseInt(((t % 33) + 3) / 4) +
                            78 +
                            r +
                            (n < 7 ? 31 * (n - 1) : 30 * (n - 7) + 186),
                        u += 400 * parseInt(p / 146097),
                    36524 < (p %= 146097) && ((u += 100 * parseInt(--p / 36524)), 365 <= (p %= 36524) && p++),
                        u += 4 * parseInt(p / 1461),
                    365 < (p %= 1461) && ((u += parseInt((p - 1) / 365)), (p = (p - 1) % 365)),
                        a = p + 1,
                        e = [0, 31, (u % 4 == 0 && u % 100 != 0) || u % 400 == 0 ? 29 : 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
                        s = 0;
                    s < 13 && !(a <= (c = e[s]));
                    s++
                )
                    a -= c;
                return this.isInvalid(u, s, a), this.outputToWhich(u, s, a, i);
            },
        };
    });

    function dateChanger(numberFa) {
        // Regular expression patterns for the date formats
        let patterns = [
            /\b(\d{4})-(\d{2})-(\d{2})\b/g, // YYYY-MM-DD
            /\b(\d{2})-(\d{2})-(\d{4})\b/g, // DD-MM-YYYY
            /\b(\d{4})\/(\d{2})\/(\d{2})\b/g, // YYYY/DD/DD
            /\b(\d{2})\/(\d{2})\/(\d{4})\b/g, // DD/MM/YYYY
            /\b(\d{4})-(\d{1})-(\d{2})\b/g, // YYYY-M-DD
            /\b(\d{2})-(\d{1})-(\d{4})\b/g, // DD-M-YYYY
            /\b(\d{4})\/(\d{1})\/(\d{2})\b/g, // YYYY/M/DD
            /\b(\d{2})\/(\d{1})\/(\d{4})\b/g, // DD/M/YYYY
            /\b(\d{4})-(\d{2})-(\d{1})\b/g, // YYYY-MM-D
            /\b(\d{1})-(\d{2})-(\d{4})\b/g, // D-MM-YYYY
            /\b(\d{4})\/(\d{2})\/(\d{1})\b/g, // YYYY/MM/D
            /\b(\d{1})\/(\d{2})\/(\d{4})\b/g, // D/MM/YYYY
            /\b(\d{4})-(\d{1})-(\d{1})\b/g, // YYYY-M-D
            /\b(\d{1})-(\d{1})-(\d{4})\b/g, // D-M-YYYY
            /\b(\d{4})\/(\d{1})\/(\d{1})\b/g, // YYYY/M/D
            /\b(\d{1})\/(\d{1})\/(\d{4})\b/g, // D/M/YYYY
        ];


        const elements = document.getElementsByTagName("*");
        for (const pattern of patterns) {
            for (let i = 0; i < elements.length; i++) {
                const element = elements[i];
                for (let j = 0; j < element.childNodes.length; j++) {
                    const node = element.childNodes[j];
                    if (
                        node.nodeType === Node.TEXT_NODE &&
                        node.parentNode.nodeName !== "INPUT" &&
                        node.parentNode.nodeName !== "TEXTAREA"
                    ) {
                        let text = node.nodeValue;
                        const matches = text.matchAll(pattern);
                        for (const match of matches) {
                            let year = match[1].length == 4 ? match[1] : match[3];
                            let day = match[1].length == 4 ? match[3] : match[1];
                            let month = match[2];
                            let convertedDate = farvardin.gregorianToSolar(parseInt(year), parseInt(month), parseInt(day), "string");
                            if (numberFa === true) {
                                text = text.replace(match[0], convertedDate.toString().convertDigits("fa"));
                            } else {
                                text = text.replace(match[0], convertedDate);
                            }
                            node.nodeValue = text;
                        }
                    }
                }
            }
        }
    }
    dateChanger();
```