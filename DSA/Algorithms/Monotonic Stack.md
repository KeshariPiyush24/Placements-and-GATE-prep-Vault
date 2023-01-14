# Good read on monotonic stack

https://leetcode.com/problems/sum-of-subarray-minimums/solutions/178876/stack-solution-with-very-detailed-explanation-step-by-step


# Questions

## [Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/solutions/3050209/java-monotonic-stack-solution-explained-with-intuition/)

```java
	class Solution {
	  public int sumSubarrayMins(int[] arr) {
	    int n = arr.length;
	
	    Stack < Integer > ms = new Stack < > ();
	    int[] nsl = new int[n];
	    for (int i = 0; i < n; i++) {
	      while (!ms.isEmpty() && arr[i] < arr[ms.peek()]) // non-strict
	        ms.pop();
	      nsl[i] = ms.isEmpty() ? i : ms.peek();
	      ms.push(i);
	    }
	    ms.clear();
	    int[] nsr = new int[n];
	    for (int i = n - 1; i >= 0; i--) {
	      while (!ms.isEmpty() && arr[i] <= arr[ms.peek()]) // strict
	        ms.pop();
	      nsr[i] = ms.isEmpty() ? i : ms.peek();
	      ms.push(i);
	    }
	
	    long sum = 0;
	    int MOD = (int) 1e9 + 7;
	
	    for (int i = 0; i < n; i++) {
	      int leftDis = i == nsl[i] ? i + 1 : i - nsl[i]; // i == nsl[i] means that no previous elements were smaller than current element
	      int rightDis = i == nsr[i] ? n - i : nsr[i] - i; // i == nsr[i] means that no next elements were smaller than current element
	      sum = (sum + ((1 l * leftDis * rightDis) % MOD * arr[i]) % MOD) % MOD;
	    }
	
	    return (int) sum;
	  }
	}
```