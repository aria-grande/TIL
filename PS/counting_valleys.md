# Problem
https://www.hackerrank.com/challenges/counting-valleys/problem

# Solution
차례로 문자열을 읽으면서 U이면 level을 증가 시키고, D면 level을 감소시킨다. <br/>
level이 음수에서 양수가 되는 순간 valley count를 증가 시킨다.

```java
int countingValleys(int n, String s) {
    int valleyCnt = 0;
    int level = 0;
    boolean nowValley = false;
    for(char c : s.toCharArray()) {
        if(c == 'U') {
            level++;
            if(nowValley && level >= 0) {
                valleyCnt++;
                nowValley = false;
            }
        } else if (c == 'D') {
            level--;
            if(level < 0 && !nowValley) {
                nowValley = true;
            }
        }
    }
    return valleyCnt;
}
```

Time complexity: O(n)<br/>
Space complexity: O(1)
