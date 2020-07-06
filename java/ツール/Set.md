```java
import java.util.*;
 
public class Main{
    public static void main(String[] args) {
        List<integer> list = new ArrayList<integer>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(1);
        
        Set<integer> set = new HashSet<integer>(list);
        
        for(Integer value : set)
        {
            System.out.println(value);
        }
    }
}
```
