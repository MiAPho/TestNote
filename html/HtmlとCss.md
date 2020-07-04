```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>title</title>
    <link rel="stylesheet" href="http://yui.yahooapis.com/3.18.1/build/cssreset/cssreset-min.css">
    <link rel="stylesheet" href="css/main.css"/>
  </head>
  <body>
    <div class="blue">blue</div>
    <div class="red">red</div>
    <div id="box">
      <div class="blue">blue</div>
      <div class="red">red</div>
      <div class="red">red</div>
      <div class="blue">blue</div>
    </div>
  </body>
</html>
```
****
```css
body{
  text-align: center;
  color:white;
}
body>div{
  width:200px;
  height:200px;
}
.blue{
  background: blue;
}
.red{
  background: red;
}
body>div:nth-child(-n+2){
  line-height: 200px;
}
body>div:nth-child(2){
  border-radius: 50%;
}
#box>div{
 float:left;
 width:50%;
 height:50%;
 line-height: 100px;
}
/*
use flex-box
#box{
  display:flex;
  flex-wrap: wrap;
  line-height: 100px;
}
#box>div{
  flex-basis:50%;
}
*/
