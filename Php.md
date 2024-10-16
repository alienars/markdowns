# PHP Snippets

## auto translate

```php
    <?php
    if($_COOKIE['lang'] !='fa'){
        ?>

        <script>
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
        </script>

        <?php
    }
    ?>
```