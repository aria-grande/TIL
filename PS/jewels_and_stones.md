# Problem
```
You're given strings J representing the types of stones that are jewels, and S representing the stones you have.
Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in J are guaranteed distinct, and all characters in J and S are letters. 
Letters are case sensitive, so "a" is considered a different type of stone from "A".
```
https://leetcode.com/problems/jewels-and-stones/description/

# Solution 1(without stream)
```java
public int numJewelsInStones(String J, String S) {
  Set<Character> set = new HashSet<Character>();
  for(char jc : J.toCharArray()) {
    set.add(jc);
  }
  int count = 0;
  for(char sc : S.toCharArray()) {
    if(set.contains(sc)) {
      count++;
    }
  }
  return count;
}
```

# Solution 2(with stream)
```java
public int numJewelsInStones(String J, String S) {
  Set<Character> set = new HashSet<Character>(Arrays.asList(J.chars().mapToObj(x -> (char) x).toArray(Character[]::new)));
  return (int) S.chars()
      .filter(x -> set.contains((char) x))
      .count();
}    
```

J의 길이를 N, S의 길이를 M이라 할 때,

Time complexity: O(N+M)

Space complexity: O(N)
