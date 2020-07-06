メソッドを抜けるという意味でも使える
その場合 voidのメソッドである必要がある

void の中では
returnで数値（int）等を返せない。


break;は直近のループしか抜けれない
```java
outer:while(true){
	for(i=0;i<10;i++){
		if(i==8){
			break outer;
		}
	}
}
```
上記の方法ならwhileを抜けることも可能
