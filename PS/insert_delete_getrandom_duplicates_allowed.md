# Problem

https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/
```
Design a data structure that supports all following operations in average O(1) time.

Note: Duplicate elements are allowed.
insert(val): Inserts an item val to the collection.
remove(val): Removes an item val from the collection if present.
getRandom: Returns a random element from current collection of elements. 
           The probability of each element being returned is linearly related to the number of same value the collection contains.
```
# Solution
- 빠르게 만들기 어렵다.
- 로직을 개선 해야 함.
```java 
class RandomizedCollection {

    Map<Integer, Integer> elemCount;
    int totalElems;
    
    /** Initialize your data structure here. */
    public RandomizedCollection() {
        totalElems = 0;
        elemCount = new HashMap<>();
    }
    
    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    public boolean insert(int val) {
        int count = elemCount.getOrDefault(val, 0);
        elemCount.put(val, count + 1);        
        totalElems++;
        return count == 0;
    }
    
    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    public boolean remove(int val) {
        int count = elemCount.getOrDefault(val, 0);
        if(count > 0) {
            elemCount.put(val, count - 1);
            totalElems--;
        }
        return count != 0;
    }
    
    /** Get a random element from the collection. */
    public int getRandom() {
        int randomIdx = (int) (Math.random() * totalElems) + 1;
        for(int elem : elemCount.keySet()) {
            int count = elemCount.get(elem);
            if(randomIdx <= count) {
                return elem;
            }
            randomIdx -= count;
        }
        return -1;
    }
}

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection obj = new RandomizedCollection();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```
