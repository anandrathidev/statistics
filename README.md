
# statistics
## What is P value 
p value : https://www.youtube.com/watch?v=5Z9OIYA8He8 : see StatQuest: P Values, clearly explained

p valus is sum of all probablities of similar probablity or rarer probablity. 
example lets say probablity of 5 times Head HHHHH = 1/32
then p valis for 5H = 5H + 5T + rarere than 5h which is 0 
so p value is = 1/32 + /32 = 1/16.

## Confidence intervals
many people misunderstand confidence intervals 
but that's only because they didn't learn about bootstrapping first.

bootstrap refresher imagine we wait a bunch of
female mice in this case we weighed 12 of them we didn't weigh every single
female Mouse on the planet just 12 now we can take these 12 measurements and we
can use them to calculate the sample mean now the sample mean is not the mean
for all mice the entire planet it's just the mean of the mice that we sampled
however we can use bootstrapping and the data that we have here to determine what
values would be reasonable for the global worldwide mean of all female mice
on the planet now that we've calculated the sample mean we can bootstrap the
sample to bootstrap the sample we randomly select 12 weights from the
original sample and duplicates are okay here's an example of a bootstrap sample
we can see that this measurement on the far left.
was sampled twice in our bootstrap sample and the measurement to its right
wasn't included in our bootstrap sample this is called sampling with replacement
now we calculate the mean of the random sample after we've calculated the mean
of our first random sample all we have to do is repeat steps 1 and 2 until
we've calculated a lot of means sometimes more than 10,000 .
that's all there is to bootstrapping now.

let's talk about confidence intervals
usually when you see a confidence interval out in the wild it's called a 
95% confidence interval a 95% confidence interval is just an interval that covers
95% of the means 

## Randomforest vs ADAboost
so let's start by using decision trees and random forests to
explain the three main concepts behind adaboost.
1. Tree size
RF : Trees has no size limit
     in a random forest each time you make a
     tree you make a full-sized tree some trees might be bigger than others
     but there's no predetermined maximum depth.
ADAboost: The trees are usually just a node and two leaves.
	 A tree with just one node and two leaves is called a stump so 
	 this is really a forest of stumps rather than trees.
     stumps are technically weak learners however that's the way adaboost likes it.

2.  Equal votes
RF: random forest in a random forest each tree has an equal vote on the final
    classification.
Adaboost: Some stumps get more say in the final classification than others 
          in this illustration the larger stumps get more say in the final. 

3.  RF  Each decision tree is made independently of the others 
in other words it doesn't matter if this tree was made first or this one

Adaboost :stumps made with adaboost order is important.
the errors that the first stump makes influence how the second stump is made
and the error is that the second stone makes influence how the third stump is
made etc etc etc.

