# Appendix A: Math Review

A certain familiarity with certain mathematical concepts will help you when trying to analyze algorithms. This section is meant as a review for some commonly used mathematical concepts, notation, and methodology.  Where possible analogies between mathematical and programming concepts are drawn

## Mathematical Notations and Shorthands

### Shorthands

| shorthand | meaning |
| :--- | :--- |
| iff | if and only if |
| $$\therefore$$  | therefore |
| $$\approx$$  | approximately |
| $$ab$$  | a \* b |
| $$a(b)$$  | a \* b |
| $$|a|$$  | absolute value of a |
| $$\lceil{a}\rceil$$  | ceiling, round a up to next biggest whole number. Example: $$\lceil{2.3}\rceil = 3$$ |
| $$\lfloor{a}\rfloor$$  | floor, round a down to the next smallest whole number. Example: $$\lfloor{2.9}\rfloor = 2$$  |

### Variables

In math, like programming, we use variables. Variables can take on some numeric value and we use it as a short hand in a mathematical expression. Before using a variable, you should define what it means \(like declaring a variable in a program\)

#### For example:

"Let _**n**_ represent the size of an array"

This means that the variable n is a shorthand for the size of an array in later statements.

### Functions

Similar to functions in programming, mathematics have a notation for functions. Mathematically speaking, a function has a single result for a given set of arguments. When writing out mathematical proof, we need to use the language of math which has its own syntax

As a function works with some argument, we first define what the arguments mean then what the function represents.

**For example:**

Let $$n$$ represent the size of the array  - \(n is the name of the argument\). 

Let $$T(n)$$ represent the number of operations needed to sort the array - T is the name of the function, and it accepts a single variable $$n$$ 

We pronounce $$T(n)$$ as "T at n". Later we will assoicate $$T(n)$$ with a mathematical expression that we can use to make some calculation. The expression will be a mathematical statement that can be used to calculate the number of operations needed to sort the array. If we supply the number 5, then $$T(5)$$ would be the number of operations needed to sort an array of size 5

**Summary**

$$T(n)$$ - read it as _**T at n**_, we call the function $$T$$ .

$$T(n) = {n^2} + n + 2$$ means that $$T(n)$$  is the same as the mathematical expression $${n^2} + n + 2$$.  Think of $$T(n)$$ as being like the function prototype, and $${n^2} + n + 2$$ as being like the function declaration.

$$n $$ can take on any value \(unless there are stated limitations\) and result of a function given a specific value is calculated simply by replacing n with the value

$$T(5) = {5^2} + 5 + 2 = 32$$ \( we pronounce T\(5\)  as "T at 5"\)

### Sigma Notation

Sigma notation is a shorthand for showing a sum. It is similar in nature to a for loop in programming.

**General summation notation.**

$$\sum\limits_{i=1}^{n} t_i = t_1 + t_2+ ... + t_n$$ 

The above notation means that there are n terms and the summation notation adds each of them together.

Typically the terms $$t_i$$,​​ is some sort of mathematical expression in terms of $$i$$ \(think of it as a calculation you make with the loop counter\). The $$i$$ is replaced with every value from the initial value of 1 \(at the bottom of the $$\sum$$ \), going up by 1, to n \(the value at the top of the \sum∑\)

**Example:**

$$\sum\limits_{i=1}^{5} i = 1 + 2 + 3 + 4 + 5$$ 

### Mathematical Definitions and Identities <a id="mathematical-definitions-and-identities"></a>

Mathematical identities are expressions that are equivalent to each other. Thus, if you have a particular expression, you can replace it with its mathematical identity.

### Exponents

#### **Definition**

​​ $${x^n}$$ means $$(x)(x)(x)...(x)$$ \(n x's multiplied together\)

#### I**dentities**

$${x^ax^b}={x^{a+b}}$$   


$$\frac{x^a}{x^b} = {x^{a-b}}​$$   


$${({x^a})^b} = {x^{ab}}$$

$${x^a}+{x^a} = 2{x^a} \neq {x^{2a}}$$   


$${2^a}+{2^a} = 2({2^a}) = {2^{a+1}}$$ 

### Logarithms

{% hint style="info" %}
In computer text books, unless otherwise stated $$log$$ means $$log_2$$ ​​ as opposed to $$log_{10}$$ ​​ like math text books
{% endhint %}

#### Definition

$${b^n} = a$$ iff $$ log_ba = n$$ In otherwords $$log_ba$$ is the exponent you need to raise $$b$$ by in order to get $$a$$ 

#### Identities

$$\log_ba = \frac{\log_ca}{\log_cb}$$ , where $$c > 0$$   


$$\log {ab} = \log a + \log b$$   


$$\log (\frac{a}{b}) = \log a - \log b$$   


$$\log {a^b} = {b}{\log a} $$ 

$$\log x < x$$  for all $$x > 0$$ 

$$\log 1 = 0$$ 

$$\log 2 = 1$$ 

### Series

A series is the sum of a sequence of values. We usually express this using sigma notation \(see above\).

#### I**dentities**

$$\sum\limits_{i=0}^{n} c(f(i)) = c \sum\limits_{i=0}^{n}f(i)$$ ​, where $$c$$ is a constant

$$\sum\limits_{i=0}^{n} {2^i} = {2^{n+1}} - 1$$ 

$$\sum\limits_{i=0}^{n} {a^i} = \frac{a^{n+1}- 1}{ a - 1}​$$ 

$$\sum\limits_{i=0}^{n} {a^i} \leq \frac{1}{a-1}$$ 

$$\sum\limits_{i=1}^{n} {i} = \frac{n(n+1)}{2}​$$ 

$$\sum\limits_{i=1}^{n}{i^2} = \frac{n(n+1)(2n+1)}{6}$$ 

$$\sum\limits_{i=1}^{n}{f(n)} = nf(n)​ $$ 

$$\sum\limits_{i=n_0}^{n} f(i) = \sum\limits_{i=1}^{n} f(i) - \sum\limits_{i=1}^{n_0 - 1} f(i)$$ 

