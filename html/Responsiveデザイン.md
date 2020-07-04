	```html
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>レスポンシブデザイン</title>
  <link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/3.18.1/build/cssreset/cssreset-min.css">
<link rel="stylesheet" href="css/main.css" />
</head>
<body>
  <div id="container">
    <header>
      <h1>Hello Responsive Web Design!</h1>
    </header>
    <main>
      <h2>Image</h2>
      <img class="imgFull" src="images/girl.jpg" alt="sample Image" />
      <h2>YouTube</h2>
      <div class="youtubeContainer">
        <iframe width="1280" height="720" src="https://www.youtube.com/embed/upRxE7a-tHM" frameborder="0" allowfullscreen></iframe>
      </div>
      <h2>float Items</h2>
      <ul id="floatItems">
        <li><img src="images/float1.jpg" alt="sample Image"/></li>
        <li><img src="images/float2.jpg" alt="sample Image"/></li>
        <li><img src="images/float3.jpg" alt="sample Image"/></li>
        <li><img src="images/float4.jpg" alt="sample Image"/></li>
      </ul>
    </main>
    <footer>
      &copy;Joytas All Rights Reserved.
    </footer>
  </div>
</body>
</html>
```
********
```CSS
header{
  position:relative;
  width:100%;
  padding-top:34%;
}
header h1{
  position: absolute;
  top:0;
  right:0;
  width:100%;
  height:100%;
  background-image:url(../images/headerImg.png);
  background-size:cover;
  box-sizing: border-box;
  padding:10%;
  font-size:3.5vw;
  color:#345;
}
main h2{
  background: #345;
  color:white;
  text-align: center;
  font-size:3vw;
  padding:5px 0;
}
.imgFull{
  display: block;
  width:100%;
}
.youtubeContainer{
  position: relative;
  width:80%;
  padding-top:45%;
  margin:2vh auto;
}
.youtubeContainer iframe{
  position: absolute;
  top:0;
  right:0;
  width:100% !important;
  height:100% !important;
}

#floatItems img{
  display: block;
  width:50%;
border:1px solid #333;
  box-sizing: border-box;
  float:left;
}
footer{
  text-align: right;
  padding-right:10px;
  color:#345;
}
/*1200px以上で適用*/
@media screen and (min-width:1200px){
  header h1{
    font-size:3vw;
  }
}
/*600px以下で適用*/
@media screen and (max-width:600px){
  header h1{
    font-size:4vw;
  }
  main h2{
    font-size:3.5vw;
  }
}

/*480px以下で適用*/
@media screen and (max-width:480px){
  #floatItems img{
  
  width:100%;

 }
}

```
