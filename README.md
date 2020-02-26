
# statistics
## Odds, probablity and log odds
Total = 10
Heads = 8
Tails = 2
Odds of head = 8/2
Odds of tails = 2/8
prob of head = 8/10
prob of tails = 2/10

### derive Odds from Probablity 
Odds of head 8/2 = = prob of head/1- prob of head = (8/10)/(2/10) = 8/2
Odds of Tail 2/8 = = prob of tail/1- prob of tail = (2/10)/(8/10) = 2/8

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
https://www.youtube.com/watch?v=LsK-xG1cLYA

So let's start by using decision trees and random forests to
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

## Adaboost details 
how to
create a forest of stumps using adaboost first we'll start with some data we
create a forest of stumps with adaboost to predict if a patient has heart
disease. 
Predictors :  chest_pain, artery_status and weight 
1] give each sample a weight that indicates how important it is to be correctly classified.
   at the start all samples get the same weight one divided by the total number of samples in this case that's 1/8 and
   that makes the samples all equally important.

   however after we make the first stump these weights will change in order to 
   guide how the next stump is created.

2] calculate gini index of all features. 
  the first stump in the forest this is done by finding the variable chest pain.
  blocked arteries or patient weight that does the best job classifying the
  samples note because all of the weights are the same we can ignore them right

  Now we calculate the Gini index for the three stumps.
  the Gini index for patient weight is the lowest so this will be the first stump.

3] in the forest now we need to determine how much say this stump will have in the final
   classification remember some stumps get more say in the final classification than others.
   we determine how much say a stump has in the final classification based on how well it 
   classified the samples. 
   The total error for a stump is the sum  of the weights associated with the incorrectly classified samples.
   in this case the total error is 1/8 
   note because all of the sample weights add up to one. 
   total error will always be between zero for a perfect stump and one for a horrible stump.
   we use the total error to determine the amount of say this stump has in the final classification with the following
   formula 
   ```(Amount of Say) =  1/2 * log( (1 - total_error)/ total error).```
   
   we can draw a graph of the amount of say by plugging in a bunch of numbers 
   between 0 & 1 . when a stump does a good job and the total error is small 
   then the amount of say is a relatively large positive value. 
   when a stump is no better than flipping a coin ie total error equals 0.5
   then the amount of say will be zero and 
   when a stump does a terrible job and the total error is close to one in other 
   words if the stump consistently gives you the opposite classification then the 
   amount of say will be a large negative value so if a stump votes for heart disease 
   the negative amount of say will turn that vote into not heart disease.
   
   4] After 1st tree/stun calculate new sample weights for each data point 
   
   ```sample with wrong class = (e^(Amount of say))/N```
   ```sample with correct class = (e^-(Amount of say))/N```
   
   **Note if total error is 1 or 0 then this equation will freak out in practice a 
   small error term is added to prevent this from happening.

	to review the three ideas behind adaboost our one adaboost combines a lot 
	of weak learners to make classifications the weak learners are almost always 
	stumps to some stumps get more say in the classification than others and three 
	each stump is made by taking the previous stumps mistakes into account if we 
	have a way to Gini function then we use it with the sample weights otherwise 
	we use the sample weights to make a new dataset that reflects those weights 
