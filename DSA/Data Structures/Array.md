
## Easy

# [Reverse the array](https://www.codingninjas.com/codestudio/problems/reverse-the-array_1262298)

<details>
	<summary>Solution</summary>
	<pre><code class="java">
	import java.util.*;
	import java.io.*;
	import java.util.ArrayList;
	
	public class Solution {
		public static void reverseArray(ArrayList < Integer > arr, int m) {
			int i = m + 1;
			int j = arr.size() - 1;
	
			while (i < j) {
				Collections.swap(arr, i, j);
				i++;
				j--;
			}
		}
	}
	</code></pre>
</details>