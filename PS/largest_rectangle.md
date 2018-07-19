# Problem
https://www.hackerrank.com/challenges/largest-rectangle/problem


# Solution
brute-force 한 방법으로 먼저 풀어본다.
각 빌딩의 높이를 height로 지정하여 heights를 iterate 하고,<br/>
해당 빌딩을 기준으로 좌로, 우로 가는 포인터를 둬 연속적으로 카운트 할 수 있는 빌딩의 갯수를 구해 height를 곱해준다.<br/>
이 값들의 max 값을 구하면 된다.

```java
long largestRectangle(int[] heights) {
    long max = 0;
    for(int i = 0; i < heights.length; ++i) {
        int height = heights[i];
        int buildingCount = 1;
        for(int left = i - 1; left >= 0; --left) {
            if(height > heights[left]) {
                break;
            }
            buildingCount++;
        }
        for(int right = i + 1; right < heights.length; ++right) {
            if(height > heights[right]) {
                break;
            }
            buildingCount++;
        }
        max = Math.max(max, height * buildingCount);
    }        
    return max;
}
```

heights의 길이를 N이라 할 때,<br/>
Time complexity: O(N^2)<br/>
Space complexity: O(1)
