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