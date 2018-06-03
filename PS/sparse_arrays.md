# Problem
https://www.hackerrank.com/challenges/sparse-arrays/problem
```
Given a collection of input strings of length N and a collection of query strings of length Q,
return the collection of integers that is consist of occurrences of each query strings.
```

# Solution
Brute-force한 방법으로 풀게 되면 각 쿼리에 대해 input이 존재하는지 매번 iterate 및 비교를 해야하므로 시간 복잡도는 O(N^Q)이다.<br/>
하지만, input string을 key로, 빈도수 value로 하여 map에 저장해두면, 결괏값을 만들기 위한 시간 복잡도는 O(N+Q)로 많이 줄어들게 된다.<br/>
### Java
```java
int[] matchingStrings(String[] inputs, String[] queries) {
  Map<String, Integer> countMap = new HashMap<String, Integer>();
  for(String s : inputs) {
    int cnt = countMap.containsKey(s) ? countMap.get(s) : 0;
    countMap.put(s, ++cnt);
  }
  
  final int Q = queries.length;
  int[] matchedCount = new int[Q];
  for(int i = 0; i < Q; ++i) {
    String query = queries[i];
    matchedCount[i] = countMap.containsKey(query) ? countMap.get(query) : 0;
  }
  return matchedCount;
}
```
### Ruby
```ruby
def matching_strings(inputs, queries)
  counts = {}
  inputs.each { |input| counts[input] = (counts[input] || 0) + 1 }
  queries.map { |q| counts[q] || 0 }
end
```

Time complexity: O(N+Q)<br/>
Space complexity: O(N+Q)
