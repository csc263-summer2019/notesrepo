# Average Case Analysis

When we we perform worst case analysis, we find the longest path through a piece of code and assume that it is the path the program will take.  We establish the circumstance under which the longest path would be taken and analyze based on that.

{% hint style="info" %}
Before beginning this section you may wish to look at [Appendix B](../appendix-b-probability-review.md) for a quick probability theory review
{% endhint %}

With average case it is different.  Average case analysis looks at how a piece of code will behave on average.

Thus, our steps are as follows:

* define sample space $$S_n$$as the set of all inputs of size n
* define a random variable $$t_n(S)$$ as the number of steps required to process input $$S \in S_n$$with our algorithm
* determine the likelihood of each input S
* calculate the expected value of $$E[t_n]$$
* This expected value is the average number of steps our algorithm will take and thus we can use it for our run time.

## Linear Search Example

Let us consider a simple example:

```cpp
/* this function is passed a key, an array and the size of the
   array n.  Function returns index of where key is found, -1 
   if it is not found)*/
int linearSearch(int key, int array[],int n){
    int rc=-1;                          //1 op
    int i=0;                            //1 op
    for(int i=0;i < n && rc==-1;i++){   //1 + 4(number of iterations)
        if(key == array[i]){            //1(number of iterations)
            rc=i;                       //1 op only done if key is found
        }
    }
    return rc;                          //1 op

```

In a successful worst case search, we find key in the very last element.  In a non-successful search we search the entire array and we don't find it.

We can describe the number of steps taken by above function in the worst case as:

$$T(n) = 5n + 5$$ \(assuming key is found in last element\)

For average case though, we are going to assume we will find it \(unsuccessful search always results in going through all n elements\).  

Let $$S_n$$represent the set of all inputs of size n.  Now.. clearly what we don't want is to use every single permutation of an n element integer array.  Instead, lets consider what matters... what we care about is not so much what is in each element of the array but rather where the key is located as that is what will stop the loop.  Thus, our sample space $$S_n =\{key==array[0], key==array[1], key==array[2],...key==array[n-1]\}$$.  It is also possible to include key not in array in this set but we would need to determine the likelihood of that compared to successful searches, so for now, let us assume only that search will be successful.

Now we have defined our sample space.  What we want to do is define a random variable.

Let $$t_n(S)$$ represent the number of steps needed to find the key if key was located in element the $$S'th$$ element of the array.  Thus S = 1 if key==array\[0\], S=2 if key==array\[1\] etc.  $$t_n(1) = 5 + 5, t_n(2) = 5+ 5(2), t_n(3)=5*5(3)$$ ... etc.

Now... what about the probability distribution?  \(ie how likely is key to be in S'th element\).  In our case we assume that every element of the array is equally likely.  Since there are n elements, we assume that there are $$\frac{1}{n}$$chance of key being located at any given index.

Next we calculate the expected value of random variable $$t_n$$

$$E[t_n] = \sum\limits_{i=1}^n {t_n(i)*pr(i)} $$   
$$E[t_n]= \sum\limits_{i=1}^n {((5)+(5i))*\frac{1}{n}} $$   
 $$E[t_n]= {\sum\limits_{i=1}^n {(5)(\frac{1}{n})}} + {\sum\limits_{i=1}^n (5i)( \frac{1}{n})}$$   
 $$E[t_n]=5 + (\frac{5}{n})(\frac{n(n+1)}{2})$$  
 $$E[t_n]=5 + (\frac{5(n+1)}{2}) = 2.5n + 7.5$$ 

Thus, our on average, our linear search would require $$2.5n + 7.5$$operations. 







