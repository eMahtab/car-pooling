# Car Pooling





# Implementation : Cumulative Sum
```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        if(trips == null || trips.length == 0)
            return true;
        int lastDropLocation = Integer.MIN_VALUE;
        for(int[] trip : trips)
            lastDropLocation = Math.max(lastDropLocation, trip[2]);
        
        int[] journey = new int[lastDropLocation + 1];
        for(int[] trip : trips) {
            journey[trip[1]] += trip[0];
            journey[trip[2]] -= trip[0];    
        }
        for(int i = 0; i <= lastDropLocation; i++) {
            if(i != 0)
            journey[i] += journey[i-1];
            if(journey[i] > capacity)
                return false;
        }
        return true;
    }
}
```

# References :
https://leetcode.com/problems/car-pooling
