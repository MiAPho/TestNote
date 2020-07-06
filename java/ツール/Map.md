```java
Map<キーの型,型の値> マップ変数=new HashMap<>();
HashMap<Integer,Integer> data=new LinkedHashMap<>();  順番の概念あり
```
HashMap<●,■>が備えるメソッド

|操作|戻り値|メソッド|意味|
|:--:|:--:|:--:|:--:|
|追加|■|put(●,■)|マップに●と■のペアを格納する|
|取得|■|get(●)|キー値●に対応する値を取得(なければnull)|
|調査|int|size()|格納されているペア数を数える|
||boolean|isEmpty()|要素数がゼロであるかを判定|
||boolean|containsKey(●)|指定データがキーに含まれているかを判定|
||boolean|containsValue(■)|指定データが値に含まれているかを判定|
|削除|void|clear()|要素をすべて削除する|
||■|remove(●)|指定した内容の要素を削除する|
|その他|Set<●>|keySet()|格納されているキーの一覧を返す|
  
```java
import java.util.HashMap;
import java.util.Random;
public class Main7 {
	public static void main(String[] args) {
		Random rand=new Random();
		HashMap<Integer,Integer> map=new HashMap<>();
		final int MINNUM=1,MAXNUM=100,COUNT=100;
		System.out.printf("%d~%dの乱数を%d回発生させたよ%n",MINNUM,MAXNUM,COUNT);
		for(int i=0;i<COUNT;i++) {
			int num=rand.nextInt(MAXNUM)+MINNUM;
			if(map.containsKey(num)) {
				map.put(num, map.get(num)+1);
			}else {
				map.put(num, 1);
			}
		}
		System.out.println("***result***");
		System.out.println(map.size()+"種類の数値が出ました。");
		for(int i=MINNUM;i<=MAXNUM;i++) {
			if(map.containsKey(i)) {
				System.out.println(i+"..."+map.get(i));
			}
		}
	}
}
