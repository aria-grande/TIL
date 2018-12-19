# Problem
https://leetcode.com/problems/add-strings/description/

# Solution

https://leetcode.com/submissions/detail/195777015/

```java
public String addStrings(String num1, String num2) {
    char[] nums1 = num1.toCharArray();
    final int len1 = nums1.length;
    char[] nums2 = num2.toCharArray();
    final int len2 = nums2.length;

    char[] sum = new char[Math.max(nums1.length, nums2.length)];
    final int sumLen = sum.length;

    int up = 0;
    for(int i = 0; i < Math.max(nums1.length, nums2.length); i++){
        int n1 = i < len1 ? Character.getNumericValue(nums1[len1- 1 - i]) : 0;
        int n2 =  i < len2 ? Character.getNumericValue(nums2[len2 - 1 - i]) : 0;
        int value = n1 + n2 + up;
        sum[sumLen - 1 - i] = (char)(value % 10 + '0');
        up = value / 10;
    }
    return up == 1 ? "1" + String.valueOf(sum) : String.valueOf(sum);
}
```
