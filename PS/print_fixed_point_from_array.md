# Problem
https://www.geeksforgeeks.org/find-fixed-point-value-equal-index-given-array-duplicates-allowed/

Given a sorted array of unique values, find an element where its value is equal to the index.

# Solution

```python
def printIndexedElements(arr, sp, ep):
  if(sp > ep):
    return
    
  mid = (sp + ep) / 2
  if(arr[mid] < mid):
    printIndexedElements(arr, mid + 1, ep)
  elif arr[mid] > mid:
    printIndexedElements(arr, sp, mid - 1)
  else:
    printIndexedElements(arr, sp, mid - 1)
    print(arr[mid])
    printIndexedElements(arr, mid + 1, ep)
```

Time complexity: O(log n) in average, O(n) in worst case

Space complexity: O(1), O(n) considers call stack
