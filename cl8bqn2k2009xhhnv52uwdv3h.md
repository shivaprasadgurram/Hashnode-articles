## Day 2 - Next Greater Element I

Hola,

The basic naive approach is solving this problem in O(n^2) time complexity, where for every element in array 1 we iterate through every element in array 2 and as soon as we find match then we look for greater element to it's right in array 2 if not present then it is going to be -1.

But we can solve this problem in O(n) using Map and Stack data structures together, the algorithm that going to consider is **"monotonic stack"**.

[What is monotonic stack?](https://medium.com/techtofreedom/algorithms-for-interview-2-monotonic-stack-462251689da8)


**Problem:** [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

**Solution:** [Watch YouTube video]()


```
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Map<Integer, Integer> map = new HashMap<>();
        Stack<Integer> stack = new Stack<>();
        for(int element : nums2) {
            while(!stack.isEmpty() && stack.peek() < element) {
                map.put(stack.pop(), element);
            }
            stack.push(element);
        }
        int[] res = new int[nums1.length];
        int index = 0;
        for(int i : nums1) {
            res[index++] = map.getOrDefault(i, -1);
        }
        return res;
    }
``` 

If you would like to receive daily notifications on my content, you can join in my telegram group [Join In Telegram Group](https://t.me/+764RyZ8uGVw3MzQ1)


You can follow me at [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/)


Gracias.


