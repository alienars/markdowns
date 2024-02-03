# CSS Snippets

## vertically middle

```css
    .class{
        position : absolute;
        top : 50%;
        margin-top : -15px;
    }
```
```css
    .class{
        display: flex;
        justify-content: center;
        align-items: center;
    }
```
```css
    .class{
        vertical-align:middle
        margin-top : calc(50vh-100px);
    }
```

## CSS Variables

```css
    :root {
        --blue: #1e90ff;
        --white: #ffffff;
    }
    body { 
        background-color: var(--blue); 
    }
```

## FlexBox

```css
    .container{
        display : flex;
        flex-direction: row; /* in a row side by side */
        flex-direction: column; /* in a column top on top */
        flex-direction: row-reverse; /* The order of the items is reversed */
        flex-direction: column-reverse; /* The order of the items is reversed */
        flex-wrap: wrap; /* If the width of the container is smaller than the sum of the items together, the items in a row will move to the next line */
        flex-wrap: wrap-reverse; /* If the width of the container is smaller than the sum of the items together, the items in a row should go to the previous line */
        flex-flow: row wrap; /* shorthand of flex-direction & flex-wrap */
        justify-content: flex-start; /* [123      ] */
        justify-content: flex-end; /* [      123] */
        justify-content: center; /* [   123   ] */
        justify-content: space-between; /* [1   2   3] */
        justify-content: space-around; /* [ 1  2  3 ] */
        justify-content: space-evenly; /* [  1  2  3  ] */
        /* The direction perpendicular to the direction of the items | row or column */
        align-items: flex-start; /* top */
        align-items: flex-end; /* bottom */
        align-items: center; /* vertically center */
        align-items: stretch;
        /* just like justify-content */
        /* with the difference that it was to create space between items but this is to create space between horizontal lines, also don't forget flex-wrap: wrap; */
        align-content: flex-start; /* top */
        align-content: flex-end; /* bottom */
        align-content: center; /* vertically center */
        align-content: stretch;
        align-content: space-between; /* [1   2   3] but vertically */
        align-content: space-around; /* [ 1  2  3 ] but vertically */
    }
    /* sds */
    .items{

    }
```