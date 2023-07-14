## Use Bard to Create Math LaTex 

One of the more esoteric declarative languages out there is [LaTex for mathematics](https://en.wikibooks.org/wiki/LaTeX/Mathematics). It allows creating and formatting mathematical expressions for documents, books, and other publications. Increasingly it has found usage outside the halls of academia, especially since it is now supported on [Github markdown](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions) and Jupyter notebooks. As more people become involved in machine learning and data science, math LaTex becomes increasingly useful to larger groups. 

However, Math LaTex has a [bit of a learning curve](https://www.overleaf.com/learn/latex/Mathematical_expressions) and you may only have so much time to learn so many things. Thankfully, we can try to describe to Bard what we want to express mathematically and get a Math LaTex expression out of it. 

Let's say we want to take the fraction $ \frac{x^2}{3} $ and express it as math LaTex. Let's try to describe that expression to Bard and ask it to create some Math LaTex out of it: 

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

If we want to test out this math LaTex expression, we can use [this editor](https://latexeditor.lagrida.com) to get a preview. Sure enough, when we render this expression we see everything is correct!

![](https://latex.codecogs.com/gif.latex?%5Cbegin%7Bpmatrix%7D%200%20%26%202%20%26%203%20%5C%5C%203%20%26%20%5Cboldsymbol%7B%5Csigma%7D%20%26%201%20%5C%5C%206%20%26%20%5Cboldsymbol%7B%5Ctheta%7D%20%26%205%20%5Cend%7Bpmatrix%7D) 
