
# Implementation

## Video -> https://www.youtube.com/watch?v=aBxjDBC4M1U


```java
	public class DisjointSet {
	  private int[] parent;
	  private int[] rank;
	  private int[] size;
	
	  public DisjointSet(int n) {
	    parent = new int[n];
	    rank = new int[n];
	    size = new int[n];
	    for (int i = 0; i < n; i++) {
	      parent[i] = i;
	      rank[i] = 0;
	      size[i] = 1;
	    }
	  }
	
	  public int find(int x) {
	    if (parent[x] != x) {
	      parent[x] = find(parent[x]);
	    }
	    return parent[x];
	  }
	
	  public void unionByRank(int x, int y) {
	    int xRoot = find(x);
	    int yRoot = find(y);
	    if (rank[xRoot] < rank[yRoot]) {
	      parent[xRoot] = yRoot;
	    } else if (rank[yRoot] < rank[xRoot]) {
	      parent[yRoot] = xRoot;
	    } else {
	      parent[yRoot] = xRoot;
	      rank[xRoot]++;
	    }
	  }
	
	  public void unionBySize(int x, int y) {
	    int xRoot = find(x);
	    int yRoot = find(y);
	    if (xRoot == yRoot) {
	      return;
	    }
	    if (size[xRoot] < size[yRoot]) {
	      parent[xRoot] = yRoot;
	      size[yRoot] += size[xRoot];
	    } else {
	      parent[yRoot] = xRoot;
	      size[xRoot] += size[yRoot];
	    }
	  }
	
	}
```




# Questions

## [1061. Lexicographically Smallest Equivalent String](https://leetcode.com/problems/lexicographically-smallest-equivalent-string/description/)

```java
	class Solution {
	
	  class DisjointSet {
	    int[] parent;
	
	    public DisjointSet() {
	      parent = new int[26];
	      for (int i = 0; i < 26; i++)
	        parent[i] = i;
	    }
	
	    int find(int node) { // finds ultimate parent of the given node
	      if (parent[node] == node) return node;
	
	      return parent[node] = find(parent[node]); // path compression
	    }
	
	    void union(int u, int v) {
	      int par1 = find(u);
	      int par2 = find(v);
	
	      parent[Math.max(par1, par2)] = Math.min(par1, par2);
	    }
	  }
	
	  public String smallestEquivalentString(String s1, String s2, String baseStr) {
	    int n = s1.length();
	    DisjointSet obj = new DisjointSet();
	    for (int i = 0; i < n; i++) {
	      char c1 = s1.charAt(i);
	      char c2 = s2.charAt(i);
	      obj.union(c1 - 'a', c2 - 'a');
	    }
	
	    StringBuilder res = new StringBuilder();
	    for (char c: baseStr.toCharArray())
	      res.append((char)(obj.find(c - 'a') + 'a'));
	
	    return res.toString();
	  }
	}
```