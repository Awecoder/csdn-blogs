> 题目
>  输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位予数组的后半部分。
## 题目分析
### 解决思路
<font color =#0000ff size = 4>解决方法</font>：设置两个指针，第一个指针初始化指向数组的第一个数字，向后移动；第二个指针初始化指向数组的最后一个数字，向前移动。当第一个指针指向偶数，第二个指针指向奇数，交换两个数字。

### Java实现
```
package offer;
public class Test14 {

    public static void reorderOddEven(int[] array) {
        // 对于输入的数组为空，或者长度小于2的只接返回
        if (array == null || array.length < 2) {
            return;
        }
        // 从左向右记录偶数的位置
        int start = 0;
        // 从右向左记录奇数的位置
        int end = array.length - 1;
        // 开始调整奇数和偶数的位置
        while (start < end) {
            // 找偶数
            while (start < end && (array[start] & 0x1) != 0) {
                start++;
            }
            // 找奇数
            while (start < end && (array[end] & 0x1) == 0) {
                end--;
            }
 
            if(start < end){
				int tmp = array[start];
				array[start] = array[end];
				array[end] = tmp;
            }     
        }
    }
    /**
     * 输出数组的信息
     *
     * @param arr 待输出数组
     */
    public static void printArray(int[] arr) {
        if (arr != null && arr.length > 0) {
            for (int i : arr) {
                System.out.print(i + " ");
            }
            System.out.println();
        }
    }
    public static void main(String[] args) {
        int[] array = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
        reorderOddEven(array);
        printArray(array);
    }
}
```
<font color =#0000ff size = 4>特别注意：</font>本题判断奇数和偶数采用位与方式，更好。

```
(array[start] & 0x1) != 0
```

### 可扩展性

```
public class Test14 {

	public static void reorderOddEven(int[] array) {
		if (array == null || array.length < 2) {
			return;
		}
		
		int start = 0;
		int end = array.length - 1;
		while (start < end) {
			while (start < end && isEven(array[start])) {
				start++;
			}
			while (start < end && !isEven(array[end])) {
				end--;
			}

			if (start < end) {
				int tmp = array[start];
				array[start] = array[end];
				array[end] = tmp;
			}
		}
	}

	public static boolean isEven(int n) {
		return (n & 0x1) != 0;
	}
}
```

## 扩展题目
> 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。
### 思路
【1】类似冒泡排序 n^2
【2】创建临时数组，以空间换时间。
```
public class Solution {
    public void reOrderArray(int [] array) {
        if(array == null || array.length < 2)
            return ;
        
        int length = array.length;
        int[] arr = new int[length];
        int j = 0;
        
        for(int i = 0; i < length; i++){
            if((array[i] & 0x1) != 0){
                arr[j++] = array[i];
            }
        }
        
        for(int i = 0; i < length; i++){
            if((array[i] & 0x1) == 0){
                arr[j++] = array[i];
            }
        }
        
        for(int i = 0; i < length; i++){
            array[i] = arr[i];
        }    
    }
}
```