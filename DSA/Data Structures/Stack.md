
# Implementation


# Questions

## [Celebrity Problem](https://practice.geeksforgeeks.org/problems/the-celebrity-problem/1)

Video By Sumit Sir -> https://youtu.be/CiiXBvrX-5A

```java
	class Solution {
	    int celebrity(int[][] knows, int n) {
	        Stack<Integer> st = new Stack<>();
	        for (int i = 0; i < n; i++)
	            st.push(i);
	        while (st.size() > 1) {
	            int a = st.pop();
	            int b = st.pop();
	            if (knows[a][b] == 1 && knows[b][a] == 0)
	                st.push(b);
	            else if (knows[b][a] == 1 && knows[a][b] == 0)
	                st.push(a);
	        }
	
	        if (st.size() == 0) return -1;
	
	        int potentialCelebrity = st.pop();
	
	        for (int i = 0; i < n; i++) {
	            if (i != potentialCelebrity && (knows[i][potentialCelebrity] == 0 || knows[potentialCelebrity][i] == 1))
	                return -1;
	        }
	
	        return potentialCelebrity;
	    }
	}
```