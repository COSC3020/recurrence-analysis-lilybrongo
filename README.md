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

The runtime complexity of the mystery() function would be $\Theta(n^5)$
The base case would be when n <= 1, $T(1) = \Theta(1)$. Knowing this, when $n > 1$, the function makes 3 recursive calls and also executes a nested loop. The 3 recursive calls would have a runtime of $3 * T(n/3)$. NExt we have to take into consideration the time complexity of the loop. The first loop runs $n^2$, the second or middle loop runs $n$ times for each of the iterations. Moving inward to the third or inner loop, this one runs $n^2$ times for each of the middle loop iterations. Knowing these three iteration times, we can combine them into $n^2 * n * n^2 = n^5$. Using this total, we can combine the recursive case of $3 * T(n/3)$ with the $n^5$, so we have $3 * T(n/3) + n^5$ when $n > 1$. 

Calculations:
$T(n) = 3T(n/3) + n^5

$T(n/3) = 3T(n/9) + (n/3)^5$
$T(n/3) = 3((3T(n/9)) + (n/3)^5) + n^5$
$T(n/3) = 9T(n/9) + 3(n/3)^5 + n^5$




Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.
