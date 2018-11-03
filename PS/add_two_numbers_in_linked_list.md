# Problem
https://leetcode.com/problems/add-two-numbers

# Solution (recent try)
```java
// add l1 into l2
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode n1 = l1;
    ListNode n2 = l2;
    int passed = 0;
    while(n1 != null && n2 != null) {
        int sum = n1.val + n2.val + passed;
        n2.val = sum % 10;
        passed = sum / 10;
        if((n1.next != null || passed == 1) && n2.next == null) {
            n2.next = new ListNode(0);  
        }            
        n1 = n1.next;
        n2 = n2.next;
    }
    while(n2 != null) {
        int sum = n2.val + passed;
        n2.val = sum % 10;
        passed = sum / 10;
        if(n2.next == null && passed == 1) {
            n2.next = new ListNode(0);    
        }
        n2 = n2.next;
    }
    return l2;
}
```

Time complexity: O(max(m, n))

Space complexity: O(1)

# Solution
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode result = new ListNode(0);
    ListNode pr = result; // pointer of result
    ListNode p1 = l1;
    ListNode p2 = l2;
    int carry = 0;
    while(p1 != null || p2 != null) {
        int sum = (p1 == null ? 0 : p1.val) + (p2 == null ? 0 : p2.val) + carry;
        carry = sum / 10;
        
        pr.next = new ListNode(sum % 10);
        pr = pr.next;

        if(p1 != null) {
            p1 = p1.next;    
        }
        if(p2 != null) {
            p2 = p2.next;        
        }
    }
    if(carry > 0) {
        pr.next = new ListNode(carry);
    }

    return result.next;
}
```


Time complexity: O(max(m, n))

Space complexity: O(max(m, n))

## 2018.10.10 풀면서 느낀점
Old Solution is below.
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode result = new ListNode(0);
    ListNode pr = result; // pointer of result
    ListNode p1 = l1;
    ListNode p2 = l2;
    int carry = 0;
    while(p1 != null || p2 != null) {
        int sum = (p1 == null ? 0 : p1.val) + (p2 == null ? 0 : p2.val) + carry;
        pr.val = sum % 10;
        carry = sum / 10;
        if(carry == 1 || (p1 != null && p1.next != null) || (p2 != null && p2.next != null)) {
            pr.next = new ListNode(0);
            pr = pr.next;
        }
        if(p1 != null) {
            p1 = p1.next;    
        }
        if(p2 != null) {
            p2 = p2.next;        
        }
    }
    if(carry == 1 && pr != null) {
        pr.val = carry;
    }

    return result;
}
```
result.next를 리턴하면 복잡한 조건문을 줄일 수 있다! 큰 깨달음
