## Day 1 - Valid Parentheses

Hola,

This is one of the basic problem which helps us to test our knowledge on **Stack DS**.

**Problem:** [Valid Parentheses](https://www.codingninjas.com/codestudio/problems/795104)

**Solution:**

```
import java.util.Stack;
public class Solution {
    public static boolean isValidParenthesis(String expression) {
        // Write your code here
        Stack<Character> stack = new Stack<>();
        for(char ch : expression.toCharArray()) {
            if (stack.isEmpty() && (ch ==')' || ch == ']' || ch == '}')) {
                return false;
            } else if (!stack.isEmpty() && ((ch ==')' && stack.peek() == '(') || (ch == ']' &&   
                           stack.peek() == '[') || (ch == '}' && stack.peek() == '{'))) {
                stack.pop();
            } else {
                stack.push(ch);
            }
        }
        return stack.isEmpty();
    }
}
``` 

If you would like to receive daily notifications on my content, you can join in my telegram group [Join In Telegram Group](https://t.me/+764RyZ8uGVw3MzQ1)


You can follow me at [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/)


Gracias.



