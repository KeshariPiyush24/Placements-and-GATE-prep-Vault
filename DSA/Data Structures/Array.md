
# Easy

## [Reverse the array](https://www.codingninjas.com/codestudio/problems/reverse-the-array_1262298)

```JAVA TI:"Solution" "FOLD"
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
```

## [Find the maximum and minimum element in an array](https://practice.geeksforgeeks.org/problems/find-minimum-and-maximum-element-in-an-array4428/1)

```JAVA TI:"Solution" "FOLD"
	class Compute 
	{
	    static pair getMinMax(long a[], long n)  
	    {
	        int N = (int) n;
	        long max = a[0];
	        long min = a[0];
	        for (long i : a) {
	            max = Math.max(max, i);
	            min = Math.min(min, i);
	        }
	        return new pair(min, max);
	    }
	}
```


# Medium

## [Find the "Kth" max and min element of an array](https://practice.geeksforgeeks.org/problems/kth-smallest-element/0)

```JAVA TI:"Solution" "FOLD"
	class Solution {
	    
	    public static int randomPartition(int[] arr, int l, int r) {
	        int randIndex = (int) (l + Math.random() * (r - l + 1));
	        swap(arr, randIndex, r);
	        return partition(arr, l, r);
	    }
	    
	    static void swap(int[] arr, int i, int j) {
	        if (arr[i] == arr[j]) return;
	        arr[i] ^= arr[j];
	        arr[j] ^= arr[i];
	        arr[i] ^= arr[j];
	    }
	    
	    public static int partition(int[] arr, int l, int r) {
	        int pivotElement = arr[r];
	        int partitionIndex = l;
	        
	        for (int i = l; i < r; i++) {
	            if(arr[i] < pivotElement) {
	                swap(arr, partitionIndex, i);
	                partitionIndex++;
	            }
	        }
	        
	        arr[r] = arr[partitionIndex];
	        arr[partitionIndex] = pivotElement;
	        
	        return partitionIndex;
	    }
	    
	    public static int quickSelect(int[] arr, int l, int r, int k) {
	        int partitionIndex = randomPartition(arr, l, r);
	        if (partitionIndex == k) return arr[k];
	        else if (partitionIndex < k) return quickSelect(arr, partitionIndex + 1, r, k);
	        else return quickSelect(arr, l, partitionIndex - 1, k);
	    }
	    
	    
	    public static int kthSmallest(int[] arr, int l, int r, int k) 
	    { 
	        int temp = quickSelect(arr, l, r, k - 1);
	        return temp;
	    } 
	}
```
