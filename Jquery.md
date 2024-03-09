# Jquery Snippets

will only run once the page Document Object Model (DOM) is ready for JavaScript code to execute

```js
    $( document ).ready(function() {
        console.log( "ready!" );
    });
```

will run once the entire page (images or iframes), not just the DOM, is ready.

```js
    $( window ).on( "load", function() {
        console.log( "window loaded" );
    });
```

if element with contdown id is exist run codes 

```js
    if ($("#countdown").length > 0) { ...... }
```

toggle class to i element child of element with parent class trigger with hovering on it

```js
    $(".parent").on("mouseenter", function () {
        $(this).find("i").toggleClass("white");
    });
    $(".parent").on("mouseleave", function () {
        $(this).find("i").toggleClass("white");
    });
```

if bootstrap navbar is active on mobile size dropdown of navbar is open

```js
    if($("#burger-menu-btn").attr("aria-expanded") == "true"){ ...... }
```

Go To Top Of Page Button

```js
    $("#gotop").on("click", function () {
        window.scrollTo({ top: 0, behavior: "smooth" });
    });
```

copy to clipboard button

```js
    $(".copy-btn").click(function () {
        let value = $(this).find("span").html(); //  get the text from span in element with class .copy-btn
        let tempInput = $("<input>"); 
        $("body").append(tempInput);
        tempInput.val(value).select();
        document.execCommand("copy");
        tempInput.remove();
        let $this = $(this); // Pour the value into another variable for use inside setTimeout function
        if ($(this).find("span").text() == "کپی شد!"){
          
        }else{
          $this.find(".copied").show(); //  Change the text of btn when clicked (show text copied)
          $this.find(".code").hide(); //  Change the text of btn when clicked (hide text copy)
          $(this).find("i").toggleClass("animated");
          $(this).find("i").toggleClass("tada");
        }
        setTimeout(function () {
          $this.find(".copied").hide(); //  Change the text of btn when clicked (hide text copied)
          $this.find(".code").show(); //  Change the text of btn when clicked (show text copy)
          $this.find("i").toggleClass("animated");
          $this.find("i").toggleClass("tada");
        }, 1500);
    });
```

countdown timer

```html
    <div id="countdown" target-date="4/31/2024 06:0 AM"></div>
```

```js
    CountDownTimer($("#countdown").attr("target-date"), "countdown");
    function CountDownTimer(dt, id) {
        var end = new Date(dt);
        var _second = 1000;
        var _minute = _second * 60;
        var _hour = _minute * 60;
        var _day = _hour * 24;
        var timer;
        function showRemaining() {
            var now = new Date();
            var distance = end - now;
            if (distance < 0) {
                clearInterval(timer);
                document.getElementById(id).innerHTML = "EXPIRED!";
                return;
            }
            var days = Math.floor(distance / _day);
            var hours = Math.floor((distance % _day) / _hour);
            var minutes = Math.floor((distance % _hour) / _minute);
            var seconds = Math.floor((distance % _minute) / _second);

            document.getElementById("countdown-day").innerHTML = days; //  Output the result in an element with id="days"
            document.getElementById("countdown-hour").innerHTML = hours; //  Output the result in an element with id="demo"
            document.getElementById("countdown-min").innerHTML = minutes; // 
            document.getElementById("countdown-sec").innerHTML = seconds;
        }
        timer = setInterval(showRemaining, 1000);
    }
```

execute a specific function 10 times simultaneously with different inputs, so that we can send three inputs to the desired function for each time

```js
    class CircleTimer {
        constructor(name) {
          this.name = name;
        }
        myFunction(elementId, elementBoxId) {
          console.log(elementId,elementBoxId) // main function
        }
      }

      function executeFunctionMultipleTimes(functions) {
        var promises = [];

        for (var i = 0; i < functions.length; i++) {
          var obj = functions[i].obj;
          var func = functions[i].func;
          var inputs = functions[i].inputs;

          var promise = new Promise(function (resolve, reject) {
            setTimeout(
              function (obj, fn, args) {
                try {
                  var result = fn.apply(obj, args);
                  resolve(result);
                } catch (error) {
                  reject(error);
                }
              },
              0,
              obj,
              func,
              inputs
            );
          });
          promises.push(promise);
        }
        return Promise.all(promises);
      }

      var obj1 = new CircleTimer("Object 1"); //  Create an instance of the object with a given name
      var obj2 = new CircleTimer("Object 2");
      
      var functions = [
        {
          obj: obj1,
          func: obj1.myFunction,
          inputs: [$("#timer1"), $("#timer-box1")],
        },
        {
          obj: obj2,
          func: obj2.myFunction,
          inputs: [$("#timer2"), $("#timer-box2")],
        },
      ];

      executeFunctionMultipleTimes(functions)
        .then(function () {
          console.log("All functions executed successfully:", results);
        })
        .catch(function (error) {
          console.error("Error occurred during execution:", error);
        });
      
```