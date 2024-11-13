# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```
The if(n <= 1) statement is constant as well as var count = 0;
The first and third for loop contain:
i < n*n
k < n*n
this ultimately means that they have a complexity of $n^2$ due to their iterations. 

The second loop, for(var j = 0; j < n; j++), has an interation of just $n$ because of the j<n.

We would then get $n * n^2 * n^2$.

Since there are also 3 recursive calls each divided by 3, this gives us a complexity of $3T(n/3)$. 

After combining the found complexities we would get $T(n) = 3T(n/3) + n^5$ for when n > 1. Along with this, our base case should be T(n) = 1 for when n <= 1. 

The origional problem size of n, will be $T(n) = 3T(n/3) + n^5$. 

With each of the three recursive calls, this is n/3. So we will have to have $T(n) = 3(3T(n/9) + (n/3)^5) + n^5$. Which would then be, $T(n) = 3^2(T(n/9) + 3 * ((n/3)^5)) + n^5. Then simplifying through we would then get $3^2(T(n/9) + (n^5 / 3^5)) + n^5. 

Finally we have to look at when the problem size becomes n/9. This would give us $T(n) = 3^3(T(n/27) + 3^2 * (n^5 / 3^5) + 3(n^5/3^5) + n^5. 

We can see that there is a pattern of $T(n) = 3^i (n/3^i) + n^5/3^4(i-2) + ... + n^5$

Knowing this pattern, I then need to be able to acheive the base case of T(1). This means that if I use log-base3(n) this will help me acheive the necessary base case because log-base 3 (3) is equal to 1. According to the Master Method, I can then compare the exponents in this problem. After plugging in the log-base3 we get an exponent of 1, and with the n^5 there is an exponent of 5. By comparing those, 5 > 1 so we are able to use the n^5 for the final complexity. Since the Master Method allowed us to see that the relationship was 5>1 we can then come to the conclusion of the final compelxity of $O(n^5)$


Referrenced recurrence-analysis-howardthegr8one-1 respository to get an understanding of what the full proof would look like. Also referrenced geeksforgeeks: https://www.geeksforgeeks.org/how-to-analyse-complexity-of-recurrence-relation/ which gave me a better understanding of recurrence relation analysis. I found the master method was best explained so I worked off of this for my explanation. 

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.
