
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

## [2421. Number of Good Paths](https://leetcode.com/problems/number-of-good-paths/solutions/3057170/java-lengthy-but-easy-to-understand-solution-using-dsu/)

```java
class Solution {
  int[] parents;

  // find by path compression
  private int find(int x) {
    if (x != parents[x])
      parents[x] = find(parents[x]);
    return parents[x];
  }

  public int numberOfGoodPaths(int[] vals, int[][] edges) {
    int n = vals.length;

    // initialize parents array (assume in staring every node is connected only to itself)
    parents = new int[n];
    for (int i = 0; i < n; i++) parents[i] = i;

    // create adjacency list
    Map < Integer, Set < Integer >> graph = new HashMap < > ();
    for (int[] edge: edges) {
      int u = edge[0], v = edge[1];
      graph.computeIfAbsent(u, k -> new HashSet < > ()).add(v);
      graph.computeIfAbsent(v, k -> new HashSet < > ()).add(u);
    }

    // create an array of nodes(index) and sort them on the basis of values stored in them
    Integer[] nodes = new Integer[n];
    for (int i = 0; i < n; i++) {
      nodes[i] = i;
    }
    Arrays.sort(nodes, Comparator.comparingInt(i -> vals[i]));

    int ret = n; // variable to store result (initialized with n because every node can be start and end for a good path)

    for (int i = 0; i < n;) { // increment will be done by the while loop
      // compute for all the nodes with same value as of node[i]
      int j = i;
      while (j < n && vals[nodes[j]] == vals[nodes[i]]) j++;

      // create connected components of nodes with same value using adjacent nodes with value less than or equals to vals[node[i]]
      for (int k = i; k < j; k++) {
        int x = nodes[k];
        for (int neighbor: graph.getOrDefault(x, new HashSet < > ())) { // find neighbor of node k using adjacency list
          if (vals[x] >= vals[neighbor]) { // if neighbor has value more than current node than it is of no use (not good path)
            parents[find(x)] = find(neighbor); // union current node and the neighbor
          }
        }
      }

      /**
          Now all the nodes of a connected components will have same parent.
          We will traverse all the nodes in range i....j and increase the count of it's parent node by 1.
          So after the loop terminates we will have info about which same value nodes are part of same connected component
       */
      Map < Integer, Integer > temp = new HashMap < > ();
      for (int k = i; k < j; k++) {
        int root = find(nodes[k]);
        temp.put(root, temp.getOrDefault(root, 0) + 1);
      }

      // calculate number of good paths using temp
      for (int v: temp.values()) {
        ret += v * (v - 1) / 2; // every node can be start and all the remaining node can be end of the good path
      }

      // start from the node with different value than current nodes
      i = j;
    }

    return ret;
  }
}
```