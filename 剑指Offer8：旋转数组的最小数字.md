<font color=#0000ff size=5 face="黑体">题目描述</font>
> 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

---
## 二分查找法实现
> 二分查找需要注意的三种特例情况
> 1 数组中有相同数字的特例（22222122）
> 2 数组为null的情况
> 3 排序数组本身是数组旋转的一个特例。
```
public class Solution {
	public int minNumberInRotateArray(int[] array) {
		// 
		if (array == null || array.length == 0)
			return 0; // 题目规定，其实并不是0
		int lo = 0;
		int hi = array.length - 1;
		
		// mid = lo 解决了排序数组本身的情况
		int mid = lo;
		while (array[lo] >= array[hi]) {
			if (hi - lo == 1) { // 只有两个数的时候，右边的自然是最小数了
				mid = hi;
				break;
			}
			mid = (lo + hi) / 2;
			
			// 解决lo == mid == hi 的情况
			if (array[lo] == array[mid] && array[mid] == array[hi]) {
				return minInOrder(array, lo, hi);
			}
			if (array[mid] >= array[lo])
				lo = mid;
			else if (array[mid] <= array[hi])
				hi = mid;
		}

		return array[mid];
	}

	// 顺序查找
	private int minInOrder(int[] array, int lo, int hi) {
		int min = array[lo];
		for (int i = lo + 1; i <= hi; ++i) {
			if (min > array[i])
				min = array[i];
		}
		return min;
	}
}
```


---
### <font color=#0000ff size=5 face="黑体">利用ArrayList和Collections.sort()</font>
原因：Java Collections.sort()，使用的其实是归并排序！！！
当然使用这种方法非常简单。
```
import java.util.*;
public class Solution {
    public int minNumberInRotateArray(int [] array) {
    	List<Integer> list = new ArrayList<>();
        for(int i : array){
            list.add(i);
        }
        Collections.sort(list);
        return list.get(0);
    }
}
```







---
## <font color=#0000ff size=5 face="华文行楷">对年龄排序</font>
下面方法实现的前提是可以使用辅助内存，数字大小在较小的范围内。
> 思想：
> 首先使用辅助数组统计出各年龄出现的次数，在给原来的数组从小到大赋值。
```
	public void sortAges(int ages[], int length){
		if(ages == null || length <= 0)
			return ;
		final int oldestAge = 99;
		int[] timeOfAge = new int[oldestAge + 1];
		
		for(int i= 0; i <= oldestAge; ++i){
			timeOfAge[i] = 0;
		}
		for(int i = 0; i < length; ++i){
			int age = ages[i];
			if(age < 0 || age > oldestAge)
				throw new RuntimeException();
			++timeOfAge[age];
		}
		
		int index = 0;
		for(int i = 0; i <= oldestAge; ++i){
			for(int j = 0; j < timeOfAge[i]; ++j){
				ages[index] = i;
				++index;
			}
		}
	}
```

<font color=#0000ff size=5 face="华文行楷">查找算法</font>
顺序查找、二分查找、哈希表查找、二叉树查找
> 面试题中要求在排序的数组（或者部分排序的数组）中查找一个数字或统计某个数字出现的次数，可以尝试二分查找算法。

> 哈希表最主要的优点是可以在0（1）时间查找到某元素，但是需要额外的空间来实现。

