```java
import java.util.*;
public class Switch{
	public static void main(String[] args){
		System.out.println("あなたの運勢は");
		int fortune=new Random().nextInt(3)+1;
		switch(fortune){
			case 1:
				System.out.println("大吉");
				break;
			case 2:
				System.out.println("中吉");
				break;
			case 3:
				System.out.println("吉");
				break;
		    default:
				System.out.println("凶");
				break;
		}
	}
}

