```java
import java.util.*;
public class Q6{
	public static void main(String[] args){
		int[] nums={1,2,3,4,5};
		for(int i=0;i<nums.length-1;i++){
			int index=new Random().nextInt(nums.length-i);
			int temp=nums[index];
			nums[index]=nums[nums.length-1-i];
			nums[nums.length-1-i]=temp;
		}
		System.out.println(Arrays.toString(nums));
	}
}

