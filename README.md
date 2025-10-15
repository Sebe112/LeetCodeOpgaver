# LeetCodeOpgaver
LeetCodeOpgaver :)


Problem 27:

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return k.
Custom Judge:

The judge will test your solution with the following code:

int[] nums = [...]; // Input array
int val = ...; // Value to remove
int[] expectedNums = [...]; // The expected answer with correct length.
                            // It is sorted with no values equaling val.

int k = removeElement(nums, val); // Calls your implementation

assert k == expectedNums.length;
sort(nums, 0, k); // Sort the first k elements of nums
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.

 

Example 1:

Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).
Example 2:

Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
 

Constraints:

0 <= nums.length <= 100
0 <= nums[i] <= 50
0 <= val <= 100

Min (dårlige) solution:

Tids complexitet O(N)

public class Solution {
    public int RemoveElement(int[] nums, int val) {
        int k = 0;
        for (int i = 0; i < nums.Length; i++) {
            if (nums[i] != val) {
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }
}

Problem 55:

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.



Example 1:

Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
Example 2:

Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
 

Constraints:

1 <= nums.length <= 104
0 <= nums[i] <= 105

Min (decent) solution

Tids complexitet O(N^2)

public class Solution {
    public bool CanJump(int[] nums) {
        bool isTrue = true;
        if (nums.Length == 1) {
            return true;
        }
        if (nums[0] == 0) {
            return false;
        }
        for (int i = 0; i < nums.Length; i++)
        {
            int t = i + 1;
            if (isTrue == false) {
                return false;
            }
            if (nums[i] >= nums.Length) {
                return true;
            }
            if (nums.Length - t - nums[i] == 0) {
                return true;
            }
            if (nums[i] == 0) {
                isTrue = false;
                for (int j = i - 1; j >= 0; j--) {
                    if (j + nums[j] > i) {
                        isTrue = true;
                        break;
                    }
                }
            }
        }
        return true;
    }
}


Problem 2:

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 

Example 1:

Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]

Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
 

Constraints:

The number of nodes in each linked list is in the range [1, 100].
0 <= Node.val <= 9
It is guaranteed that the list represents a number that does not have leading zeros.

Min solution

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public int remainder = 0;

    public ListNode AddTwoNumbers(ListNode l1, ListNode l2) {
        var res = l1.val + l2.val + remainder;
        remainder = 0;
        while (res > 9) {
            remainder +=  1;
            res = res - 10;
        }

        if (l1.next == null && l2.next != null) {
            return new ListNode(res, AddTwoNumbers(new ListNode(0, null), l2.next));
        }
        else if (l1.next != null && l2.next == null) {
            return new ListNode(res, AddTwoNumbers(new ListNode(0, null), l1.next));
        }
        else if (l1.next != null && l2.next != null) {
            return new ListNode(res, AddTwoNumbers(l1.next, l2.next));
        }
        else {
            if (remainder > 0 ) {
                return new ListNode(res, new ListNode(remainder, null));
            }
            return new ListNode(res, null);
        }
    }
}

Problem 121

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

 

Example 1:

Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
Example 2:

Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
 

Constraints:

1 <= prices.length <= 105
0 <= prices[i] <= 104
 
Min solution

public class Solution {
    public int MaxProfit(int[] prices) {
        int x = 0;
        int y = prices[0];
        for (int i = 0; i < prices.Length; i++) {
            if (prices[i] < y) {
                y = prices[i];
            }

            else if((prices[i] - y) > x) {
                x = prices[i] - y;
            }
        }
        return x;
    }
}

Problem 122

You are given an integer array prices where prices[i] is the price of a given stock on the ith day.

On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can sell and buy the stock multiple times on the same day, ensuring you never hold than one share of the stock.

Find and return the maximum profit you can achieve.

 

Example 1:

Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
Example 2:

Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
Example 3:

Input: prices = [7,6,4,3,1]
Output: 0
Explanation: There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.
 
min soultuion

public class Solution {
    public int MaxProfit(int[] prices) {
        int count = 0;
        if (prices.Length == 1) {
            return 0;
        }
        for (int i = 0; i < prices.Length-1; i++) {
            if (prices[i] < prices[i+1]) {
                count += prices[i+1] - prices[i];
            }
        }
        return count;
    }
}

problem 11

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

 

Example 1:

![alt text](image.png)
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
Example 2:

Input: height = [1,1]
Output: 1
 
Constraints:

n == height.length
2 <= n <= 105
0 <= height[i] <= 104

min solution

public class Solution {
    public int MaxArea(int[] height) {
        int left = 0;
        int right = height.Length - 1;
        int maxArea = 0;

        while (left < right) {

            int width = right - left;
            int currentArea = Math.Min(height[left], height[right]) * width;
            
            maxArea = Math.Max(maxArea, currentArea);

            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxArea;
    }
}

problem 41

Given an unsorted integer array nums. Return the smallest positive integer that is not present in nums.

You must implement an algorithm that runs in O(n) time and uses O(1) auxiliary space.

 

Example 1:

Input: nums = [1,2,0]
Output: 3
Explanation: The numbers in the range [1,2] are all in the array.
Example 2:

Input: nums = [3,4,-1,1]
Output: 2
Explanation: 1 is in the array but 2 is missing.
Example 3:

Input: nums = [7,8,9,11,12]
Output: 1
Explanation: The smallest positive integer 1 is missing.
 

Constraints:

1 <= nums.length <= 105
-231 <= nums[i] <= 231 - 1

min solution

public class Solution {
    public int FirstMissingPositive(int[] nums) {
        int answer = 1;
        int i = 0;
        Array.Sort(nums);
        while (i < nums.Length) {
            if (nums[i] >= 1 && answer == nums[i]) {
                answer = nums[i] + 1;
            }
            i++;
        }
        return answer;
    }
}

problem 1364

Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i].

Return the answer in an array.

 

Example 1:

Input: nums = [8,1,2,2,3]
Output: [4,0,1,1,3]
Explanation: 
For nums[0]=8 there exist four smaller numbers than it (1, 2, 2 and 3). 
For nums[1]=1 does not exist any smaller number than it.
For nums[2]=2 there exist one smaller number than it (1). 
For nums[3]=2 there exist one smaller number than it (1). 
For nums[4]=3 there exist three smaller numbers than it (1, 2 and 2).
Example 2:

Input: nums = [6,5,4,8]
Output: [2,1,0,3]
Example 3:

Input: nums = [7,7,7,7]
Output: [0,0,0,0]
 
Constraints:

2 <= nums.length <= 500
0 <= nums[i] <= 100

my solution

public class Solution {
    public int[] SmallerNumbersThanCurrent(int[] nums) {
        int[] array1 = new int[nums.Length];
        int i = 0;
        int count = 0;
        foreach (int number in nums) {
            count = 0;
            foreach (int numbers in nums) {
                if (number > numbers) {
                    count += 1;
                }
            }
            array1[i] = count;
            i++;
        }
        return array1;
    }
}