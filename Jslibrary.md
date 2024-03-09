# JS Library Snippets

## OWL Carousel

Owl Carousel Config

```js
    $(".timer-box .owl-carousel").owlCarousel({
        loop: false, // for loop and automatic clone items
        rtl: true, // for persian or arabic language
        margin: 24, // for margin and spacing between items
        nav: true,
        dots: true,  // show/hide pagination dots
        dotsContainer: ".owljs-dots-timer", //  class name of the container that will store dot elements
        autoplay: true,    // set auto play to true
        autoplayHoverPause: true,
        navText: ["", ""], //  customize navigation text (prev / next)
        responsiveClass: true,
        responsive: {
            0: {
            items: 1,
            },
            420: {
            items: 2,
            },
            576: {
            items: 2,
            },
            767: {
            items: 3,
            },
            991: {
            items: 4,
            },
            1200: {
            items: 6,
            },
        },
    });
```

Custom Navigation Buttons Owl Carousel

```js
    var owlFeatureBox = $(".timer-box .owl-carousel"); // get main owl-carousel class name
    owlFeatureBox.owlCarousel();
    $(".timer-box-prev").click(function () { //  Custom Previous Button For Nav
        owlFeatureBox.trigger("next.owl.carousel");
    });
    $(".timer-box-next").click(function () { //   Custom Next Button For Nav
        owlFeatureBox.trigger("prev.owl.carousel", [300]);
    });
```

