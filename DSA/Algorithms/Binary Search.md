
## Easy


## Medium

[2528. Maximize the Minimum Powered City](https://leetcode.com/problems/maximize-the-minimum-powered-city/solutions/3014943/c-python-binary-search-sliding-window-greedy-clear-explanation/)

```java
	import java.util.Arrays;
	
	class Solution {
	    public long maxPower(int[] stations, int r, int k) {
	        int n = stations.length;
	        long left = Arrays.stream(stations).mapToLong(x -> (long) x).min().getAsLong();
	        long right = Arrays.stream(stations).mapToLong(x -> (long) x).sum() + k;
	        long maxMinPower = 0;
	        while (left <= right) {
	            long mid = left + (right - left) / 2;
	            if (isPossible(stations, r, k, mid, n)) { // is it possible to have mid as the maxMinPower?
	                left = mid + 1;
	                maxMinPower = mid;
	            } else {
	                right = mid - 1;
	            }
	        }
	        return maxMinPower;
	    }
	
	    boolean isPossible(int[] stations, int r, int k, long maxMinPower, int n) {
	        // initialize with sum from 0th to (r - 1)th city power (rth city will be included in the loop)
	        long powerInCurrentWindow = Arrays.stream(stations).limit(r).mapToLong(x -> (long) x).sum(); // sum of i-r...i+r stations which gives power for the ith city
	        long[] additionalStationsInstallationTracker = new long[n]; // tracks the position of additional stations installations
	        for (int i = 0; i < n; i++) {
	            if (i + r < n) {
	                powerInCurrentWindow += stations[i + r];
	            }
	            if (powerInCurrentWindow < maxMinPower) {
	                long extraStationsRequired = maxMinPower - powerInCurrentWindow;
	                if (extraStationsRequired > k) return false;
	                powerInCurrentWindow = maxMinPower;
	                k -= extraStationsRequired;
	                additionalStationsInstallationTracker[Math.min(n - 1, i + r)] += extraStationsRequired;
	            }
	            if (i - r >= 0) {
	                powerInCurrentWindow -= (stations[i - r] + additionalStationsInstallationTracker[i - r]);
	            }
	        }
	        return true;
	    }
	}
```