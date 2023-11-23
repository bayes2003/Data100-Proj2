This is my solution for UCB [Data100](https://ds100.org) project2 Spam/Ham Classification. The notebook is original from [sp22](https://github.com/DS-100/sp22).

Accuracy of the final model on the training data = 0.99821  
4-fold cross-validation average accuracy on the training data = 0.97743

[Run this notebook on Kaggle](https://www.kaggle.com/code/bayes2003/data100-proj2)

## Approach

I focus only on finding words with ability to distinguish emails. Roughly speaking, we need to find words with high frequency of occurrence in spam emails. But a word with a high frequency of occurrence in spam emails may also have a high frequency of occurrence in ham emails, such as a stop word ("the", "a", "and", "in"). So frequency of occurrence is not an appropriate metric for our goal.

Note that our goal is to find "spam words" such that
- If the word appears in an email, that email is likely to be spam, **while it is not likely to be ham**.

Using conditional probability, this means 

$$
P(spam \mid word) \rightarrow 1
$$

Since

$$
P(ham \mid word) = 1 - P(spam \mid word)
$$

Then

$$
P(ham \mid word) \rightarrow 0
$$

We can see that conditional probability is an appropriate metric of our goal.

Meanwhile, finding "ham words" will also be helpful. Therefore, we need to find words such that

$$
P(spam \mid word) \rightarrow 1
$$

or 

$$
P(ham \mid word) \rightarrow 1
$$

Let's define a word's "ability to distinguish emails" as 

$$
d = \max(P(spam \mid word), P(ham \mid word))
$$

To calculate the conditional probability, we use the formula

$$
P(A \mid B) = \frac{P(AB)}{P(B)}
$$

and estimate the probability with the frequency.
