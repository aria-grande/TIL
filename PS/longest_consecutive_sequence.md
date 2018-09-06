# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-hard/116/array-and-strings/833/
```
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.
```

# Solution
number와 length of consecutive sequence를 담고 있는 hashmap을 이용할 것이다.
'연속된 수'이므로 sequence 내 number **n**에 대해 **n-1**과 **n+1** 값들을 토대로 계산 및 업데이트 하는 방식으로 접근한다.

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        int max = 0;
        Map<Integer, Integer> boundary = new HashMap<Integer, Integer>();
        for(int num : nums) {
            if(!boundary.containsKey(num)) {
                int left = boundary.containsKey(num - 1) ? boundary.get(num - 1) : 0;
                int right = boundary.containsKey(num + 1) ? boundary.get(num + 1) : 0;
                
                int len =  right + left + 1;
                boundary.put(num, len);
                
                boundary.put(num - left, len);
                boundary.put(num + right, len);
                System.out.println(String.format("num = %d left = %d right = %d, old max = %d", num, left, right, len));
                max = Math.max(len, max);
            }
        }
        return max;
    }
}
```

Time complexity: O(N)

Space complexity: O(N)
