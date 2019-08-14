# Randomized Quicksort

The quicksort algorithm works as follows \(in the general sense\):

```cpp
quickSort(int array[]){
    if(array has more than one element){
        select a pivot p from array
        partition the array into 3 parts:
            Smaller = all values smaller than pivot
            Equal = all values bigger than pivot
            Bigger = all values bigger than pivot
            //quick sort all values smaller and bigger than array and then
            //append all partitions back together
            array=[quickSort(Smaller), Equal, quickSort(Bigger)];
    }
    return array;
}
```

### 

For now, we are going to select the first element in the array as the pivot.  This isn't necessarily how we would do it and there are other options but it will make the discussion easier to visualize.

### Worst case analysis

With each call to quickSort, we pick one pivot and then we partition the rest of the array by comparing it against the pivot.  The number of comparison we do pretty much determines how long it takes.

#### Upper Bound

Whenever we pick a value to be a pivot, it will always end up in the Equal partition and it won't be compared against anything else again in future quickSort\(\) recursive calls.  Every other value in the array is compared against the pivot at most one time.  Thus, every pair of values are only compared exactly one time.  There are $$\binom n 2 $$pairs in the array where n is the size of the array. Thus, T\(n\) &lt;= $$ \binom n 2$$ and thus, T\(n\) is $$O(n^2)$$

#### Lower Bound

To get a lower bound, we find a specific input for our array that will cause at least $$c n^2$$comparisons where c is some constant.  We are picking our pivot from the front of the array.  Thus if we create an array that was sorted from biggest to smallest... that is array\[0\] &gt; array\[1\] &gt; array\[2\] .... This will mean that the Bigger partition will contain n-1 items, Equal will have 1 while smaller will be empty.  This would mean that the quicksort call using bigger would only one 1 comparison less than its caller function.  Given how the recursion work the total number of comparisons can be described as:

 $$ (n + (n-1) + (n-2) + ....1) ={ {(n)(n-1)}\over 2}$$.  Thus T\(n\) &gt;= $$cn^2$$ and thus, T\(n\) is $$\Omega (n^2)$$

### Average-case analysis

To perform the average case analysis, lets begin by creating a sample space with $$S_n$$ set of all permutations of 1 to n.  We assume that all permutations are equally likely.

Now, firstly notice that it doesn't matter what the exact values in array are as long as we can refer to them as smallest, second smallet etc. Also notice that there are no equality in this sample set.  This is not a bad assumption because equality allows multiple values to be placed into the Equal set which doesn't make it into the next recursive call causing the sample size in successive calls to be smaller. Thus, our specification would lead to an over estimate of the runtime which is good.

Let $$t_n(S)$$represent number of comparisons needed for input $$S \in S_n$$.  As we are using the first element as the pivot and every permutation is equally likely it means that the chance of us choosing any of the n values is equally likely.  In other words, the probability that 1 is the pivot is 1/n, the probality that 2 is the pivot is also 1/n etc.

As quicksort is recursive, we need to not only account for the number of comparisons in a single partioning of the array but also in its recursive calls. 

If the arrays are size are  &lt;= 1, no comparisons occur, thus

$$t_0(S) = 0$$  

$$t_1(S)=0$$

For n &gt; 1, the number of comparisons needed are as follows:

$$t_n(S) = \sum\limits_{i=1}^{n} {({1\over n})( (n-1) + t_{i-1}(Smaller) +t_{n-i}(Bigger))}$$

In the above expression, any value is equally likely to be at the front \(ie smallest, is as likely as second smallest and so on\).  no matter what the pivot is, we have to compare it against n-1 other values.  We then split the array into Smaller and Bigger.  if we picked the smallest as pivot for example, we would end up calling the recursion with nothing in the Smaller partition and n-1 values in Bigger.  

The above leads to the following for the expected values:

$$E[t_0] = 0, E[t_1] = 0$$

$$E[t_n] = \sum \limits_{i=1}^{n} { {1\over n} ( (n-1) + E[t_{i-1}] + E[t_{n-i}])}$$

$$E[t_n] = (\sum \limits_{i=1}^{n} { {1\over n}  (n-1)} )+{1\over n}(\sum\limits_{i=1}^{n}{ (E[t_{i-1}])} )+  {1\over n}(\sum\limits_{i=1}^{n}{( E[t_{n-i}])})$$

$$E[t_n] = {{n(n-1)}\over n }+{1\over n}(E(t_0) + E(t_1) +...E(t_{n-1})) +{1\over n}( E(t_{n-1})+....E(t_1)+E(t_0))$$

$$E[t_n] = (n-1) + 2E(t_0) + 2E(t_1) + 2E(t_2)...2E(t_{n-1})$$

$$E[t_n] = (n-1) + 2(0) + 2E(t_1) + 2E(t_2)...2E(t_{n-1})$$

$$E[t_n] = (n-1) + {2\over n}\sum\limits_{i=1}^{n-1}{E(t_i)}$$

### Randomized Quicksort

In the previous analysis, we make some pretty general assumptions, such every permutation is equally likely.  This however might not be true.  So how do we get a random distribution regardless of the data?  The thing that determines the size of the partition used in recursive call is the pivot.  Currently algorithm chooses first element as pivot.  Instead of picking first element as pivot, pick a random element as pivot.  Instead of relying on the input to be uniformly distributed, we use the random selection so that on a fixed input, the choice of pivot is still random.  Thus the expected worst case run time is $$\Theta (nlogn)$$

Randomized quicksort is an example of Las Vegas algorithm.  These are randomized algorithms with a guaranteed correct result \(quicksort will always give correctly sorted array\) but there may be some flux to run time and can depend on the pivots that were randomly chosen.

Another kind of randomized algorithm are called Monte Carlo algorithms.  With those algorithms you are guaranteed a run time but not that the result is definitely correct.



