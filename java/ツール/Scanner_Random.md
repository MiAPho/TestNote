```java
Scanner s=new Scanner(System.in);
Random rand=new Random();
int len=s.nextInt();
org=rand.nextInt(21)-10;

s.close();//スキャナークローズ　　メモリ消去

System.exit(0);//アプリ強制終了(０は正常終了を意味する)

```
***
# ScannerのnextLin()は改行を読み込むためintの後は注意

