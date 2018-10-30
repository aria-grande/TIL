# Problem
This is a demo task.

Write a function:

`class Solution { public int solution(int[] A); } `

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

For example, given A = [1, 3, 6, 4, 1, 2], the function should return 5.

Given A = [1, 2, 3], the function should return 4.

Given A = [−1, −3], the function should return 1.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..100,000];

each element of array A is an integer within the range [−1,000,000..1,000,000].

# Solution
```java
public int solution(int[] A) {
    final int LEN = A.length;
    boolean[] shown = new boolean[LEN + 1];
    shown[0] = true;
    for(int num : A) {
        if(num <= LEN && num > 0) {
            shown[num] = true;    
        }
    }
    int missed = 0;
    for(boolean numberShown : shown) {
        if(numberShown) {
            missed++;
        }
        else {
            break;
        }
    }
    return missed;
}
```

Time complexity: O(N)

Space complexity: O(N)
# Report
- 1st attempt: https://app.codility.com/demo/results/trainingHHDJ86-M9D/
- 2nd attempt: https://app.codility.com/demo/results/trainingCTFZP3-FVN/
