# PROBLEM
https://leetcode.com/problems/can-place-flowers/description/

# SOLUTION
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int p=0;
        final int LEN = flowerbed.length;
        int cnt = 0;
        
        if(n == 0) {
            return true;
        }
        
        if(LEN == 1) {
            if(flowerbed[0] == 0) {
                return n <= 1;
            }
            return false;
        }
        
        while(p < LEN) { 
            if(flowerbed[p] == 0) {
                if(p == LEN-1 && flowerbed[p-1] == 0) {
                    cnt++;
                    p++;
                } else if(p < LEN - 1 && flowerbed[p+1] == 0) {
                    cnt++;
                    p += 2;
                } else {
                    p++;
                }
            } else if(p < LEN - 1 && flowerbed[p+1] == 0) {
                p += 2;
            } else {
                p++;
            }
        } 
        return cnt >= n;
        
    }
}

TIME COMPLEXITY: O(N)

SPACE COMPLEXITY: O(1)
