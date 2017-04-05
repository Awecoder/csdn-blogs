> 题目：定义栈的数据结构，请在该类型中实现一个能够得到站的最小元素的min函数。在该栈中，调用min、push以及pop的时间复杂度都是O（1）。

## 题目分析
我们要实现的两种效果是：
数据结构仍然是栈的性质（后进先出），同时局部依次取出最小的功能。

<font color = ##0000ff size = 4>处理方法：最小元素放到另外一个辅助栈中。</font>
1 数据栈正常压入弹出数据，维持栈的LIFO性质；
2 辅助栈用来保持最小的数据栈数据在栈顶。（min栈每次插入数据都与min栈栈顶元素比较，如果小于栈顶元素（即新最小值）压入新数据，否则压入原来的min栈栈顶元素）---与数据栈元素个数对应，显示当前数据的最小值。
![这里写图片描述](http://img.blog.csdn.net/20170404153314390?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![这里写图片描述](http://img.blog.csdn.net/20170404153325198?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTElaSE9OR1BJTkcwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
## Java实现

```
import java.util.EmptyStackException;
import java.util.Stack;

public class Solution {
	Stack<Integer> data = new Stack<>();
	Stack<Integer> min = new Stack<>();

	public void push(int node) {
		data.push(node);

		if (min.empty()) { // 考虑min栈空情况
			min.push(node);
		} else {
			int num = min.peek();
			if (node < num) {
				min.push(node);
			} else {
				min.push(num);
			}
		}
	}

	public void pop() {
		if (data.empty())
			throw new EmptyStackException();
		data.pop();
		min.pop();

	}

	public int top() {
		if (data.empty())
			throw new EmptyStackException();

		return data.peek();
	}

	public int min() {
		if (min.empty())
			throw new EmptyStackException();

		return min.peek();
	}
}
```