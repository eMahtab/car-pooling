# Car Pooling
## https://leetcode.com/problems/car-pooling
There is a car with capacity empty seats. The vehicle only drives east (i.e., it cannot turn around and drive west).

You are given the integer capacity and an array trips where trip[i] = [numPassengersi, fromi, toi] indicates that the ith trip has numPassengersi passengers and the locations to pick them up and drop them off are fromi and toi respectively. 

The locations are given as the number of kilometers due east from the car's initial location.

Return true if it is possible to pick up and drop off all passengers for all the given trips, or false otherwise.

 
```
Example 1:

Input: trips = [[2,1,5],[3,3,7]], capacity = 4
Output: false

Example 2:

Input: trips = [[2,1,5],[3,3,7]], capacity = 5
Output: true

Example 3:

Input: trips = [[2,1,5],[3,5,7]], capacity = 3
Output: true

Example 4:

Input: trips = [[3,2,7],[3,7,9],[8,3,9]], capacity = 11
Output: true
``` 

### Constraints:
```
1 <= trips.length <= 1000
trips[i].length == 3
1 <= numPassengersi <= 100
0 <= fromi < toi <= 1000
1 <= capacity <= 105
```


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
https://www.youtube.com/watch?v=nO95uYKB-lo (Good explanation)
