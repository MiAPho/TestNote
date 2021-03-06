```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8"/>
  <title>パネルパズル</title>
  <style>
  #table{
    margin:0 auto;
    background:#eee;
    padding:10px;
  }
  td{
    font-size:24px;
    text-align: center;
    width:60px;
    height:60px;
    line-height: 60px;
    border:2px solid #333;
    border-radius: 15px;
    background: #ddfeff;
  }
  td.empty{
    background-color:#eee;
    border-color:#eee;
  }
  td.ok{
    border-color:lightgreen;
  }
  #startBt{
    display:block;
    width:200px;
    margin:0px auto;
    height:50px;
    box-shadow:0 3px 0 5px #777;

  }
  #startBt:hover{
    cursor: pointer;
    opacity: 0.8;
  }
  #msgBox{
    width:200px;
    margin:10px auto;
    text-align: center;
    font-size:20px;
    height:30px;
    line-height: 30px;

  }
  </style>
</head>
<body>
<table id="table"></table>
<p id="msgBox"></p>
<button id="startBt">START</button>
<script>
    "use strict";
    window.onload=()=>{
        let size=4;
        let shuffleCount;
        let panels;
        let isShuffled;
        let table=document.getElementById("table");
        let msgBox=document.getElementById("msgBox");
        let startBt=document.getElementById("startBt");
        
        let createStage=()=>{
            for(let i=0;i<size;i++){
                let tr=document.createElement("tr");
                for(let j=0;j<size;j++){
                    let td=document.createElement("td");
                    let index=i*size+j;
                    td.posId=index;
                    td.textContent=index==size*size-1 ? "":index+1;
                    td.onclick=click;
                    if(index==size*size-1){
                        td.classList.add("empty");
                    }
                    panels.push(td);
                    tr.appendChild(td);
                }
                table.appendChild(tr);
            }
        };
        let init=()=>{
            shuffleCount=size*1000;
            isShuffled=false;
            panels=[];
            table.textContent=null;
            msgBox.textContent=null;
            createStage();
        };
        let check=()=>{
            let okCount=0;
            for(let i=0;i<panels.length;i++){
                if(panels[i].posId==parseInt(panels[i].textContent)-1){
                    okCount++;
                    panels[i].classList.add("ok");
                }else{
                    panels[i].classList.remove("ok");
                }
            }
            if(isShuffled && okCount===size*size-1){
                msgBox.textContent="Complete!";
            }
        };
        let swap=(p1,p2)=>{
            let temp=panels[p1].textContent;
            panels[p1].textContent=panels[p2].textContent;
            panels[p2].textContent=temp;
            panels[p1].classList.add("empty");
            panels[p2].classList.remove("empty");
            check();
        };
        let click=(e)=>{
            let pos=e.target.posId;
            if(pos-size>=0 && panels[pos-size].textContent==""){
                swap(pos,pos-size);
            }else if(pos+size<size*size && panels[pos+size].textContent==""){
                swap(pos,pos+size);
            }else if((pos+1)%size!=0 &&panels[pos+1].textContent==""){
                swap(pos,pos+1);
            }else if(pos%size!=0 && panels[pos-1].textContent==""){
                swap(pos,pos-1);
            }
        };
        let shuffle=(shuffleCount)=>{
           for(let i=0;i<shuffleCount;i++){
               click({target:{posId:Math.floor(Math.random()*size*size)}});
           } 
           isShuffled=true;
        };
        startBt.addEventListener("click",()=>{
            init();
            shuffle(shuffleCount);
        });
        init();
    };
</script>
</body>
</html>

