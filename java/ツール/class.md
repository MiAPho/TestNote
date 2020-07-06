```java
public class Calc{
    public static void main(String[] args){
        int a=10; int b=2;
        int total=CalcLogic.tasu(a,b);
        int delta=CalcLogic.hiku(a,b);
        //Math.max(a,b),Math.mini(a,b),Integer.parseInt("10")
        //Arrays.toString(arr)
        System.out.println("足すと"+total+"、引くと"+delta);
    }
}
```
****
```java
public class CalcLogic{
	public static int tasu(int a,int b){
		return (a+b);
	}
	public static int hiku(int a,int b){
		return (a-b);
	}
}

