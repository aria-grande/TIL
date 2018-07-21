# Problem
https://www.hackerrank.com/challenges/dynamic-array/problem


# Solution
```java
void dynamicArray(int n, List<List<Integer>> queries) {
    List<Integer>[] seqList = new ArrayList[n];
    for(int i = 0; i < n; ++i) {
        seqList[i] = new ArrayList<Integer>();
    }

    int lastAnswer = 0;
    for(List<Integer> query : queries) {
        int operator = query.get(0);
        int x = query.get(1);
        int y = query.get(2);

        List<Integer> seq = seqList[(x ^ lastAnswer) % n];
        if(operator == 1) {
            seq.add(y);
        } 
        else if (operator == 2) {
            lastAnswer = seq.get(y % seq.size());
            System.out.println(lastAnswer);
        }
    }
}
```
쿼리의 갯수를 Q, 시퀀스의 갯수를 N라 할 때,<br/>
Time complexity: O(Q)<br/>
Space complexity: O(N*N)<br/>
