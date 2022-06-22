---
title: 'A general introduction to multi-armed bandits'
date: 2022-06-20
permalink: /posts/2022/06/MAB/
---

Suppose you are in Vegas facing three lottery machines, each with a different probability of winning a prize: 

![](lotterys.png)

You would like to figure out which one wins the most, so you try out these machines: 

![](lotteryresult.png)

After trying out many times, you start thinking about strategies:  

![](ideas.png)

What would be the answer to these questions?

Congratulations, you have entered the field of multi-armed bandits!

### Best-arm identification vs. regret minimization
A *multi-armed bandit* is a machine with multiple slots where each slot has multiple options. When choosing an option, an outcome will be observed. The above two ideas actually correspond to two branches of multi-armed bandit problems. The first corresponds to what’s called “best-arm identification” problems. In this setting, people care about finding the “best one”, and they are usually interested in the question “how many plays do I need to take to find the best one?”. In the bandit community, this number is called the *sample complexity*. The second corresponds to what’s called “regret minimization” problems. In this setting, people care about the process, and they would hope that they lose the least amount of money during each play of the machine. The amount of money they lose comparing to playing the best one is called the *regret*. 

The second idea is pretty natural to think about since it might actually cost much to find the best machine. Intuitively, to find the best one, you need to play each machine many times to get a sense of how good it is. This is fine if you happen to play the best machine, but for the not-so-good machines playing them many times will make you lose a lot of money. On the other hand, there are strategies that actually lose less money even if you don’t know the best one. This strategy seems magical, right? But it turns out that it gives the best long-term benefit by avoiding to play the bad machine, while this actually takes longer to find the “best one” since it more or less does not care what the literally best one is, as long as it keeps playing the good enough machines.  

### Another view of A/B testing

The story of lottery machine ends here (it will come back later), but the story of bandits has just started. Bandits can be useful far more than just for lottery. In fact, bandit problems come all over the places in statistics, computer science, biomedical sciences, economics, etc. In statistics, A/B testing is a popular topic and there are hundreds of articles and YouTube videos to explain how it works. Also, it is one of the essential tools used in large tech companies like Amazon, Meta, Google, etc. On the other hand, in bandit language, A/B testing is just a special case of multi-armed bandit, and we present another view of the A/B testing here. 

A/B testing is a experimental method for testing new products, e.g. the layout of a webpage, effect of a new drug, etc. In A/B testing, random group of people receive two versions of the same design. One is called “control”, which is usually the old design, and the other one is called “treatment”, which is usually the new design. Suppose we are testing a new design of a webpage where the “BUY NOW” button becomes red when it is clicked, and we are interested in whether this will increase the chance that people will click this button. 

![](AB.png)

How should we assign the group of people and how large of a crowd do we need in order to determine whether we are confident to say that the click rate has increased? We start off by assuming that every individual is identical and independent. On one hand, in A/B testing, with this assumption, one will perform a hypothesis test and look at the p-value and see how large each group needs to make the p-value less than 0.05. On the other hand, we can view this scenario as a two-armed bandit, where each person assigned to “control” corresponds to playing the “control” arm, and each person assigned to “treatment” corresponds to playing the “treatment” arm. 

In this case, the size of each group corresponds to the number of times we play the arm, and we are essentially finding the “best arm”, which corresponds to the better design of the two. We notice that this is exactly the “best-arm identification” setting, and with tools in the bandit literature, we can find exactly the smallest size that each group needs in order to control the p-value to be less than 0.05.  

The benefit of this view is the generalization. By extending two-armed bandits to multi-armed bandits, we could use similar tools to easily generalize A/B testing to multivariate testing. Also, in biomedical sciences, people conduct clinical trials when developing a medicine. This is again a two-armed bandit where each slot corresponds to a patient and an action corresponds to perform either treatment or control to this patient. With the tools from bandits, we can find the optimal allocation of treatment to the patients. 
