## Use Bard to Create Math LaTex 

One of the more esoteric declarative languages out there is [LaTex for mathematics](https://en.wikibooks.org/wiki/LaTeX/Mathematics). It allows creating and formatting mathematical expressions for documents, books, and other publications. Increasingly it has found usage outside the halls of academia, especially since it is now supported on [Github markdown](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions) and Jupyter notebooks. As more people become involved in machine learning and data science, math LaTex becomes increasingly useful to more folks. 

However, Math LaTex has a [bit of a learning curve](https://www.overleaf.com/learn/latex/Mathematical_expressions) and your time may be limited to learn yet something else. Thankfully, we can try to describe to Bard what we want to express mathematically and get a Math LaTex expression made for us. 

Let's start simple. Say we want to take the fraction `x^2/3` and express it as math LaTex. Let's try to describe that expression to Bard and ask it to create some math LaTex out of it: 

**PROMPT:**

> Show the fraction x^2 / 3 as math latex

**RESPONSE:**

> Sure, here is the fraction x^2 / 3 as math LaTeX:
>
> `\frac{x^2}{3}`
> 
>To write a fraction in LaTeX, you use the `\frac` command. The `\frac` command takes two arguments: the numerator and the denominator. In this case, the numerator is x^2 and the denominator is 3.
>
>The `\frac` command also has a number of optional arguments that you can use to control the appearance of the fraction. For example, you can use the `\displaystyle` argument to tell LaTeX to display the fraction on a separate line.
>
>Here is the code for the fraction `x^2 / 3` in display math mode:
>
> `\[ \displaystyle \frac{x^2}{3} \]`
>
>The `\displaystyle` argument tells LaTeX to display the fraction on a separate line and to use the larger display style for the math.
>
>I hope this helps! Let me know if you have any other questions.

If we want to test out this math LaTex expression, we can use [an editor like this one](https://latexeditor.lagrida.com) to get a preview. Sure enough, when we render this expression we see everything is correct!

![](https://latex.codecogs.com/svg.latex?%5Cdpi%7B120%7D%20%5Cdisplaystyle%20%5Cfrac%7Bx%5E2%7D%7B3%7D%20%5C) 

Here's another one. Let's ask for the normal distributions probability density function (PDF) in math LaTex. 

**PROMPT:**
> Can you give me the math latex for a normal distribution pdf? 

**RESPONSE:**

>Sure, here is the math LaTeX for a normal distribution pdf:
>
>```
>[
>f(x; \mu, \sigma^2) = \frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left( -\frac{(x - \mu)^2}{2 \sigma^2} \right)
>]
>```
>
>The `f(x; \mu, \sigma^2)` part of the code is the probability density function for a normal distribution. The \mu part of the code is the mean of the distribution. The \sigma^2 part of the code is the variance of the distribution.
>
>The `\frac{1}{\sqrt{2 \pi \sigma^2}}$` part of the code is the normalization constant for the distribution. The `\exp\left( -\frac{(x - \mu)^2}{2 \sigma^2} \right)` part of the code is the Gaussian function.
>
>The `\[` and `\]` symbols tell LaTeX that the math code should be displayed on a separate line. This is called "display math" mode.
>
>I hope this helps! Let me know if you have any other questions.

If I copy that math LaTex into an editor, it renders like this: 

![](https://latex.codecogs.com/svg.latex?%5Cdpi%7B120%7D%20f%28x%3B%20%5Cmu%2C%20%5Csigma%5E2%29%20%3D%20%5Cfrac%7B1%7D%7B%5Csqrt%7B2%20%5Cpi%20%5Csigma%5E2%7D%7D%20%5Cexp%5Cleft%28%20-%5Cfrac%7B%28x%20-%20%5Cmu%29%5E2%7D%7B2%20%5Csigma%5E2%7D%20%5Cright%29)

Not bad! Let's now ask it to use Euler's number instead of the `exp()` function. 

**PROMPT:**

> Can you change the normal distribution PDF to use Euler's number instead of exp()?

**RESPONSE:**

>Sure, here is the math LaTeX for a normal distribution pdf using Euler's number instead of exp():
>
>[
>f(x; \mu, \sigma^2) = \frac{1}{\sqrt{2 \pi \sigma^2}} \cdot e^{\frac{-(x - \mu)^2}{2 \sigma^2}}
>]
>
>The only difference between this code and the previous code is that we have replaced the `exp()` function with the `e()` function. The e() function is Euler's number, which is a mathematical constant that is approximately equal to 2.718281828.
>
>I hope this helps! Let me know if you have any other questions.
>
>Here is a breakdown of the code:
>
>The `f(x; \mu, \sigma^2)` part of the code is the probability density function for a normal distribution.
>The `\mu` part of the code is the mean of the distribution.
>The `\sigma^2` part of the code is the variance of the distribution.
>The `\frac{1}{\sqrt{2 \pi \sigma^2}}$` part of the code is the normalization constant for the distribution.
>The `e^{\frac{-(x - \mu)^2}{2 \sigma^2}}$` part of the code is the Gaussian function.
>The `\[` and `\]` symbols tell LaTeX that the math code should be displayed on a separate line. This is called "display math" mode.

And it renders like this, spot on! 

![](https://latex.codecogs.com/svg.latex?%5Cdpi%7B120%7D%20f%28x%3B%20%5Cmu%2C%20%5Csigma%5E2%29%20%3D%20%5Cfrac%7B1%7D%7B%5Csqrt%7B2%20%5Cpi%20%5Csigma%5E2%7D%7D%20%5Ccdot%20e%5E%7B%5Cfrac%7B-%28x%20-%20%5Cmu%29%5E2%7D%7B2%20%5Csigma%5E2%7D%7D) 

Let's do something a bit more specific. When I learned math LaTex, I always had a difficult time remembering the syntax for matrices. Let's say I want to declare a matrix *A* that has three rows of elements. Rather than try to remember the syntax, I can just describe the dimensions of the matrix and what populates it. 

**PROMPT:**

>Declare a matrix A in math latex that is  3 x 3 in dimensions, where the first row is 0,2, and 3. The second row is 3, 5, and 1. The third row is 6, 4, and 5. 

**RESPONSE:**

>
>Sure, here is the code to declare a matrix A in math LaTeX that is 3 x 3 in dimensions, where the first row is 0,2, and 3. The second row is 3, 5, and 1. The third row is 6, 4, and 5:
>
>```
>\[\mathbf{A} = \begin{pmatrix}
>0 & 2 & 3 \\
>3 & 5 & 1 \\
>6 & 4 & 5
>\end{pmatrix}\]
>```
>
>The `\mathbf` command is used to declare a matrix in LaTeX. The `\mathbf` command takes one argument: the name of the matrix. In this case, we have used the `\mathbf{A}` command to declare the matrix A.
>
>The elements of the matrix are separated by commas. The rows of the matrix are separated by \\ symbols.
>
>The \[ and \] symbols tell LaTeX that the math code should be displayed on a separate line. This is called "display math" mode.
>
>I hope this helps! Let me know if you have any other questions.

That math latex will render like this: 

![](https://latex.codecogs.com/svg.latex?%5Cdpi%7B120%7D%20%5Cmathbf%7BA%7D%20%3D%20%5Cbegin%7Bpmatrix%7D%200%20%26%202%20%26%203%20%5C%5C%203%20%26%205%20%26%201%20%5C%5C%206%20%26%204%20%26%205%20%5Cend%7Bpmatrix%7D%5C)

Pretty cool that I was able to describe the matrix in plain English and it created the Math LaTex for me. Now let's say I want to replace two of the digits with two Greek symbols, and also to use square brackets rather than round brackets. 

**PROMPT:**

>That's good! Can you replace the 2 with sigma, and the 4 with delta? Also, can you use square brackets instead of round brackets? 

**RESPONSE:**

>Sure, here is the code to declare a matrix A in math LaTeX that is 3 x 3 in dimensions, where the first row is 0, σ, and 3. The second row is 3, 5, and 1. The third row is 6, δ, and 5:
>
>\mathbf{A} = \begin{bmatrix}
>0 & \sigma & 3 \\
>3 & 5 & 1 \\
>6 & \delta & 5
>\end{bmatrix}
>
>The only difference between this code and the previous code is that we have replaced the 2 with σ and the 4 with δ. We have also used square brackets instead of round brackets.
>
>I hope this helps! Let me know if you have any other questions.

Here is how it now renders. Sure enough, we got exactly what we asked for! 

![](https://latex.codecogs.com/svg.latex?%5Cdpi%7B120%7D%20%5Cmathbf%7BA%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%200%20%26%20%5Csigma%20%26%203%20%5C%5C%203%20%26%205%20%26%201%20%5C%5C%206%20%26%20%5Cdelta%20%26%205%20%5Cend%7Bbmatrix%7D) 

You can also tell it to replace an element at a specific location in the matrix. 

**PROMPT:**

> Good! Can you replace the third element in the second row with the expression 2x + 1? 

**RESPONSE:**

>Sure, here is the code to declare a matrix A in math LaTeX that is 3 x 3 in dimensions, where the first row is 0, σ, and 3. The second row is 3, 5, and 2x + 1. The third row is 6, δ, and 5:
>
>```
>\[\mathbf{A} = \begin{bmatrix}
>0 & \sigma & 3 \\
>3 & 5 & 2x + 1 \\
>6 & \delta & 5
>\end{bmatrix}\]
>```
>
>The only difference between this code and the previous code is that we have replaced the third element in the second row with the expression 2x + 1.

Sure enough, our render shows success: 

![](https://latex.codecogs.com/svg.latex?%5Cdpi%7B120%7D%20%5Cmathbf%7BA%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%200%20%26%20%5Csigma%20%26%203%20%5C%5C%203%20%26%205%20%26%202x%20&plus;%201%20%5C%5C%206%20%26%20%5Cdelta%20%26%205%20%5Cend%7Bbmatrix%7D) 

Awesome. We can use Bard to navigate esoteric languages like math LaTex and describe verbally what we want to create. Along the way, we can learn this syntax by studying the outputs, and copy/paste the expressions into their destination document. 
