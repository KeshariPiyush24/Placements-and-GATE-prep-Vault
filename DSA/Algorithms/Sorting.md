
# Selection sort

We find the minimum element in the unsorted array and then swap then minimum element with the initial index.

- Worst time complexity -> $\mathcal{O}(n^2)$
- Best time complexity -> $\mathcal{O}(n^2)$
- Average time complexity -> $\mathcal{O}(n^2)$
- Auxiliary Space -> $\mathcal{O}(1)$

```JAVA TI:"Selection sort" "FOLD"
	void selectionSort(int[] arr, int n) {
		for (int i = 0; i < n; i++) {
			int minIndex = i;
			for (int j = i + 1; j < n; j++) {
				if (arr[j] < arr[minIndex]) {
					minIndex = j;
				}
			}
			swap(arr, minIndex, i);
		}
	}
```

# Bubble sort

Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in wrong order.


## Not optimized

- Worst time ->  $\Theta(n^2)$
- Best time  -> $\Theta(n^2)$
- Average time -> $\Theta(n^2)$
- Auxiliary Space -> $\mathcal{O}(1)$

```java
void bubblesort(int[] arr, int n) {
	for (int i = 0; i < n - 1; i++) {
		for (int j = 0; j < n - 1 - i; j++) {
			if (arr[j] > arr[j + 1]) {
				swap(arr, j, j + 1);
			}
		}
	}
}
```


## Optimize if array is sorted

- Worst time ->  $\Theta(n^2)$
- Best time  -> $\Theta(n)$
- Average time -> $\Theta(n^2)$
- Space -> $\mathcal{O}(1)$

```java
void bubblesort(int[] arr, int n) {
	boolean swapped = false;
	for (int i = 0; i < n - 1; i++) {
		for (int j = 0; j < n - 1 - i; j++) {
			if (arr[j] > arr[j + 1]) {
				swap(arr, j, j + 1);
				swapped = true;
			}
		}
		
		if (!swapped) {
			return;
		}
	}
}
```