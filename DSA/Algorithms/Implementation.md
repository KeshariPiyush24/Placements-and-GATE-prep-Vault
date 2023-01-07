
# You are not a labor think like engineer

Q1 -> https://leetcode.com/problems/find-consecutive-integers-from-a-data-stream/description/

Solution ->

```java
class DataStream {
	
	int freq;
	int v;
	int k;
	
	public DataStream(int value, int k1) {
		freq = 0;
		v = value;
		k = k1;
	}
	
	public boolean consec(int num) {
		if (num == v) freq++;
		else freq = 0;
		if (freq >= k) return true;
		return false;
	}

}
```