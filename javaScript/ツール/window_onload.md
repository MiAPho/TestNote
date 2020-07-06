- ページを読み込んだ後にwindow.onload内を読み込む 
- スコープを作ることで、変数名を気にしなくても住む
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
<button id="a">A</button>
<button id="b">B</button>
<div id="result"></div>
<script>
    window.onload=()=>{
        document.getElementById('a').onclick=myHandler;
        document.getElementById('b').onclick=myHandler;
    };
    function myHandler(e){
        console.dir(e);
        document.getElementById('result').textContent=e.target.textContent+'が選ばれた';
    }
</script>
</body>
</html>
```
```html
<script>
window.onload=function(){
    let prices=[120,50,180];
    let result=this.document.getElementById("result");
    let fruits=document.getElementsByClassName("fruits");
    let numberChange=()=>{
        var sum=0;
        for(var i=0;i<fruits.length;i++){
          sum+=fruits[i].value*prices[i];
        }
        result.textContent=sum+"円です！";
    };
    for(let i=0;i<fruits.length;i++){
        fruits[i].addEventListener("change",numberChange);
        fruits[i].addEventListener("keyup",numberChange);
        fruits[i].addEventListener("mouseup",numberChange);
    }
    //function numberChange(){
    //    let sum=0;
    //    for(let i=0;i<fruits.length;i++){
    //        sum+=fruits[i].value*prices[i];
    //    }
    //    result.textContent=sum+"円です!";
    //}
}
</script>
```
