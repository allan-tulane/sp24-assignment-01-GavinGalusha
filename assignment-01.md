

# CMPS 2200 Assignment 1

**Name:**______Gavin Galusha___________________


In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not? 
.  
.  It is in O(2^n). This is because In big O notation, any gunction g(n) is in O(f(n)) if there is a constant c, c > 0, and n_sub_0 > 0, n_sub_0 < n, such that c * g(n) <= f(n). For this case, 2^{n+1} = 2 * 2^n. If we choose n_sub_0 as 1, and c1 to be 2, 2 * 2^n <= c * 2^n
.  
.  
. 
  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     
.  
.  
.  No. $2^{2^n}$ simplifies to 4^n, which clearly grows faster than 2^n. Using the same logic as last question, we can not find constants c and n_sub_0 such that 2^2^n or 4^2 is not <= c * 2^n.
.  
.  
  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    
.  
.  No it is not. For similar reasoning, n^1.01 grows faster. We can not find constants c and n_sub_0 such that n^1.01 is not <= c * $\mathrm{log}^2 n$
.  
.  

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?  
.  
.  
.  Yes. To determine if $n^{1.01} \in \Omega(\mathrm{log}^2 n)$ we must find constants c and n_sub_0 such that c > 0, n_sub_0 > 0, and c * $\Omega(\mathrm{log}^2 n)$ <= n^{1.01} for c = 1, and n_sub_0 = 400
.  
  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  
.  
.  No. We can prove this by claiming there are no constants c and n_sub_0 to complete the equation, or by simply realizing that O(n) is not in O(log^k(n)), and n^(1/2) is in O(n) so by transitivity O^(1/2) is not in O(log^3(n))
.  
.  
  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  
.  
Yes. $\sqrt{n}$ is in $\Omega((\mathrm{log} n)^3)$ because we can find constants c and n_sub_0 such that c * $\sqrt{n}$ <= $\Omega((\mathrm{log} n)^3)$. Take c = 1/100 and n_sub_0 = 1000

2. **SPARC to Python** (12 pts)

Consider the following SPARC code of the Fibonacci sequence, which is the series of numbers where each number is the sum of the two preceding numbers. For example, 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610 ... 
$$
\begin{array}{l}
\mathit{foo}~x =   \\
~~~~\texttt{if}{}~~x \le 1~~\texttt{then}{}\\
~~~~~~~~x\\   
~~~~\texttt{else}\\
~~~~~~~~\texttt{let}{}~~(ra, rb) = (\mathit{foo}~(x-1))~~,~~(\mathit{foo}~(x-2))~~\texttt{in}{}\\  
~~~~~~~~~~~~ra + rb\\  
~~~~~~~~\texttt{end}{}.\\
\end{array}
$$ 

  - 2a. (6 pts) Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. (6 pts) What does this function do, in your own words?  

.  
.  
.  
.  This function solves the fibbonaci sequence recursively. The sequence is defined by adding the previous two numbers in the sequence to eachother to determine the next number. To do this, we have function calls that go all the way back to the base cases of x = 0 and x = 1, in which case we will return the actual values of x. For every other value of x, the function initiates a recursive call to determine the two previous values in the sequence.
.  
.  
.  
.  
  

3. **Parallelism and recursion** (26 pts)

Consider the following function:  

```python
def longest_run(myarray, key)
   """
    Input:
      `myarray`: a list of ints
      `key`: an int
    Return:
      the longest continuous sequence of `key` in `myarray`
   """
```
E.g., `longest_run([2,12,12,8,12,12,12,0,12,1], 12) == 3`  
 
  - 3a. (7 pts) First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. (4 pts) What is the Work and Span of this implementation?  

.  
.  
.  Work is O(n)
.  Span is also O(n)
.  
.  
.  
.  
.  


  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?  
.  
.  
.  
.  The function splits the work into two have at each recursive steps, and then adds them together, the W(n) = 2W(n/2) + d
.  
.  
.  Therefore the Work and Span end up being both O(n)
.  
.  
.  
.  


  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  

.  
.  
.  
.  
.  The recurrence relation is W(n) = 2W(n/2) + O(1), leading to a total work of O(n)
.  
.  Due to the parallel nature, The span is dominated by the depth of the recursion tree, because each time S(n) = S(n/2) + O(1) And the Total Span is O(log(n))
.  

