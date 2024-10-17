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

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

## Recurrence Relation

This function calls mystery() three times. It calls the exact same value of mystery(n/3) regardless of the time, which means each call gets called a further three times until n<=1. 

For each call of mystery, the for loop with k is called $n^2$ times, the for loop with j is called $n$ times, and the for loop for i is called $n^2$ times. $n^2 * n * n^2 = n^5$

So the recurrence relation can be written as follows: $3T(n/3) + n^5$

## Time Complexity

To find the time complexity, we find a form after a few iterations
$3(3T(n/9) + (n/3)^5) + n^5 = 9T(n/9) + 3(n/3)^5 + n^5 $

$9(3T(n/27) + (n/9)^5) + n^5 + 3(n/3)^5 = 27T(n/27) + 9(n/9)^5 + 3(n/3)^5 + n^5$

So we can write out a geometric series to represent this pattern

$T(n) = 3^i(n/3^i) + 3^i-1(n/3^i-1)^5 + ... + n^5$

$3^i(n/3^i)$ is always less than $n^5$, as $n$ is always less than n^5 when only multiplied by a constant.
$3^i-1(n/3^i-1)^5$ is always less than $n^5$ as $n/3^i-1 < n$, and since multiplying $3^i-1$ and $n/3(i-1)$ does not get back to n, n^5 will always be greater than $3^i-1(n/3^i-1)^5$

For all cases, the worst case is always $n^5$, so the time complexity of this function is $O(n^5)$

## Help and Plagarism Statement

Help from Daniel Collins with knowing the expected form of the proof, since he took the class last semester. Michael Stoll got me on the right track with proving the geometric series.

I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.
