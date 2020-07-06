```java
import java.util.*;
  2 public class Lesson3{
  3   public static void main(String[] args){
  4     String word=new Scanner(System.in).next();
  5     String word2=word.replaceAll("[aiueo]","");
  6     System.out.println(word2);
  7   }
  8 }

