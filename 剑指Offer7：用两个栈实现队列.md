## **题目**
> 用两个栈来实现一个队列，完成队列的Push（队尾插入节点）和Pop（队头删除节点）操作。队列中的元素类型为int类型

---
## **题目分析（尝试以abcd入队出队为例）**
1. 队列压入元素时，使用栈stack1；队列弹出元素时，将栈stack1中所有元素弹出（此时栈stack1空），并压入到stack2中，然后再弹出stack2栈顶的元素。

2. 如果队列继续弹出，弹出stack2的栈顶元素。队列压入元素，依然压入到stack1 中。
3. 当队列继续弹出元素，而stack2为空时，再次将stack1元素弹入到stack2中。循环往复。。

## **Java实现**

```
import java.util.Stack;

public class Solution {
	Stack<Integer> stack1 = new Stack<Integer>();
	Stack<Integer> stack2 = new Stack<Integer>();

	public void push(int node) {
		stack1.push(node);
	}

	public int pop() {
		if (stack1.empty() && stack2.empty()) {
			// throw new EmptyStackException();
			throw new RuntimeException("栈空");
		}
		if (stack2.empty()) {
			while (!stack1.empty()) {
				stack2.push(stack1.pop());
			}
		}
		return stack2.pop();
	}
}
```
<font color=#0000ff size=5 face="黑体"> 特别注意标准库中stack和queue的API！！</font>
<font color=#0000ff size=4 face="黑体">
1 Stack：栈
empty()：是否栈空
peek()：栈顶
pop()：出栈
push()：入栈
 2 Queue：队列
 add()：入队
 peek()：队头，队列为空，返回null
 pool() ：出队，队列为空，返回null
</font>

## 扩展：用两个队列实现栈

```
import java.util.LinkedList;
import java.util.Queue;

public class Solution {
	Queue<Integer> queue1 = new LinkedList<>();
	Queue<Integer> queue2 = new LinkedList<>();

	public void push(int node) {
		if(queue2.isEmpty()){
			queue1.add(node);
		}
		else{
			queue2.add(node);
		}
	}

	public int pop() {
		if(queue1.size() == 0 && queue2.size() == 0)
			throw new RuntimeException();
		int num;
		if(queue1.isEmpty()){
			while(queue2.size() > 1){
				queue1.add(queue2.poll());
			}
			num = queue2.poll();
		} else {
			while(queue1.size() > 1){
				queue2.add(queue1.poll());
			}
			num = queue1.poll();
		}
		return num;
	}
}
```

<font color=#ff4500 size=5 face="黑体"> 仅供参考，未测试！！</font>