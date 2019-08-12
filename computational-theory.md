# Computational Theory

## Complexity Theory

Over the course of this semester, we have considered many different problems, data structures and algorithms. Aside from knowing what good solutions are to common problems, it is also useful to understand the theoretical aspects of computation.  This section of the notes deal with computational theory.  Computational theory is actually divided into several branches.  This section of the notes will focus on the branch called complexity theory which essentially classifies the difficulty of problems based on the complexity of their solution.  The difficulty is based on resource requirements \(such as time or space requirements\).

There are many complexity classes but for our discussion we are going to be focusing on just a few of these.  In particular we are going to look at the computation classes for _**decision problems**_.  Decision problems are problems where for any given input, you will end up with a "yes" or "no" answer.  These are the simplest answers.

### Undecidable Problems <a id="undecidable-problems"></a>

Some problems like the halting problems are undecidable. The halting problem is described simply as this... is it possible to write a program that will determine if any program has an infinite loop.

The answer to this question is as follows \(a proof by contradiction\)

 Suppose that we can write such a program. The program InfiniteCheck will do the following. It will accept as input a program P. If P gets stuck in an infinite loop it will print "program stuck" and terminate. If it P does not have an infinite loop and thus terminates, the InfiniteCheck program will go into an infinite loop.

Now, what if we give the InfiniteCheck the program InfiniteCheck as the input for itself.

If this is the case, then if InfiniteCheck has an infinite loop, it will terminate.

If infiniteCheck terminates, it will be stuck in an infinite loop because it terminated.

As these statements are contradictory. and thus, such a program cannot exist.

### P class Problems <a id="p-class-problems"></a>

P class problems are decision problems that can be solved in polynomial time.  Note that linear is polymial time, but so is constant and quadratic... polynomial is essentially $$n^c$$ where _c_ is a constant.   For example, matrix multiplication is a polynomial class problem even though the solution is $$n^2$$ 

### NP class Problems <a id="p-class-problems"></a>

When we talk about "hard" problems then, we aren't talking about the impossible ones like the halting problem. We are instead talking about problems where it may be possible to find a solution, just that no good solution is currently known.

The NP, in NP class stands for non-deterministic polynomial time. A non-deterministic machine is a machine that has a choice of what action to take after each instruction and furthermore, should one of the actions lead to a solution, it will always choose that action.  For all intents and purposes though, the way we describe an NP class problem is as follows:

A problem is in the NP class if we can **verify** that a given positive solution to our problem is correct in polynomial time. In other words, you don't have to find the solution in polynomial time, just verify that a particular positive solution is correct in polynomial time.

Note that all problems of class P are also class NP.  If we can solve the problem in P time then the solution is effectively the checker to ensure it is correct..

### NP-Complete Problems <a id="np-complete-problems"></a>

A subset of the NP class problems is the NP-complete problems. NP-complete problems are problems where any problem in NP can be polynomially reduced to it. That is, a problem is considered to be NP-complete if it is able to provide a mapping from any NP class problem to it and back.

### NP-Hard <a id="np-hard"></a>

A problem is NP-Hard if any problem NP problem can be mapped to it and back in polynomial time. However, the problem does not need to be NP... that is a solution does not need to be verified in polynomial time



