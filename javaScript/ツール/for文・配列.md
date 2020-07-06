```java
let team=['A','B','C','D','E'];
for(let t1 of team){
		for(let t2 of team){
				console.log(t1+'vs'+t2);
		}
}


let team=['A','B','C','D','E'];
for(let i=0;i<team.length;i++){
	for(let j=0;j<team.length;j++){
		console.log(team[i]+'vs'+team[j]);
	}
}

let team=['A','B','C','D','E'];
let opps=['A','B','C','D','E'];
for(let t1 of team){
	opps.shift();
	for(let t2 of opps){
		console.log(t1+'vs'+t2);
	}
}
```
- console.log()
コンソールに出力する
- .shift()
配列の先頭行を取り出している

