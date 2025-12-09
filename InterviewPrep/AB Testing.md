In this article, I will walk you through the end-to-end cycle of running an Experiment. For a basic A/B Testing introduction please refer to my previous article. This article will cover the Chapter -2 summary from the book — Trustworthy Online Controlled Experiments.

### End to End Example —

Let’s study an end-to-end example of an eCommerce site that sells widgets. We want to study the impact of adding the coupon code field to the revenue.

When translating the above-proposed UI change, it is very important to think about the whole process as the funnel (as shown below in the image) where there is a lot of back and forth swirling between different states as well as repeat visitors who skip intermediate steps.

![](https://miro.medium.com/v2/resize:fit:1164/1*HV8YIDcGZrTOnEOoytv4SA.png)

Image copied from the book

### Step- 1: State the Hypothesis

Our hypothesis is adding a coupon code field to the checkout page will degrade revenue.

### Step-2: Define goal metrics, in the case of one key metric, it can be used directly as the OEC.

Note: Aim is to increase the overall revenue, doing the summation of revenue itself is not recommended as it depends on the number of users on each variant. so we normalized the key metrics by actual sample size making revenue per user a good OEC.

### Now the question arises — which users to consider in the denominator for revenue per user metric??:

> a. All users who visited the site — Makes sense but there is one problem in this scenario- it will include all those users as well who never initiated checkout where the actual change was made, so they never got the chance to see that change. Hence it might not be a good way in this scenario to consider all the users.
> 
> b. Only users who complete the purchase process — This choice is also not right since it is considering only the users who completed the purchase , as the number of user increases the revenue per user may drop even though total revenue increases.
> 
> c. Only users who start the purchase process.- This seems like a good choice as it eliminates the drawback of both the above choices. As we are considering only the affected users and not the unaffected users ( users who never started the checkout process) that may dilute the results.

### So the refined Hypothesis will be —

> Adding a coupon code field to the checkout page will degrade revenue-per-user who start the purchase process.

Let's understand the technical aspects of our hypothesis.

The first step is to characterize the metric by understanding the baseline mean value and the standard err ( in other words — how variable the estimate of our metric will be). we can use either mean or percentile or any other summary statistics for measurement.

The sensitivity (i.e True positive: measures how often a test correctly generates a positive result for people who have the condition that’s being tested for) or ability to detect statistically significant differences, improves with lower standard errors of the mean.

### But now the question arises — how do we detect statistically significant differences?

There can be two ways —

> By allocating more traffic to the variants
> 
> By running the experiments for longer duration.

But there is a drawback with the second option, if we run experiments for too long then our unique user growth after few weeks will become sub-linear due to repeat users.

While running an experiment, instead of characterizing a metric for a single sample, we take multiple samples- control and treatment.

*Our Null hypothesis is (H0)— The means are the same for the pair of treatment and control groups. If it is unlikely, we reject our null hypothesis and claim that the result is statistically significant (Alternate Hypothesis — Ha).*

How do we determine this difference? There are many ways to do that. Some of them are listed below.

> 1- So we calculate the **P-value** — which is the probability of the event occuring by chance or due to something rarer or extreme, given the null hypothesis is true.

In our scenario — we calculate the difference of the p-value which is the probability of observing such difference or more extreme assuming the null hypothesis is true.

if the p-value is smaller than a significance level (alpha — 0.5) we reject the null hypothesis and claims that our experiment has an effect (or the results is statistically significant)

> 2- By checking whether the **Confidence Intervals (CI)** overlaps with zero.

CI: A 95 % CI is the range that covers the true difference (mentioned above in the hypothesis) 95% of the time and with a fairly large sample size it is usually centered around the observed difference between the two variants ( treatment and control) with an extension of 1.96 Std err on each side.

So Inorder for you to conclude with a high probability that your experience has resulted in a bigger change than you need to have enough statistical power.

> Now the question arises- what is statistical power? — It is the probability of detecting a meaningful difference between the variants when there is really one. so what does it mean in terms of hypothesis?? — statistically rejecting Null hypothesis which states there is no difference.

*In general, we use 80–90% power.*

We have been talking about statistically meaningful, statistically significant so what range is considered to be significant enough??

Well, it depends on case to case, for some cases even 1% change can leave a big impact on the revenue while in some cases even 10% might not be enough.

## Get Deepti Goyal’s stories in your inbox

Join Medium for free to get updates from this writer.

Subscribe

Few points to know before designing an experiment — — ( *tip: Common interview question*)

### 1 — What is our randomization unit ??

In this case, let’s take users as our randomization unit.

### 2 — What population of randomization units do we want to target ??

Here we can decide based on business knowledge decide what should be our target population. We can segment it on different sectors such as — geographic region, platform and device type, etc. Depending on what is our intended population we decide on our target population. In our example — let’s assume we are targeting all the users.

### 3 — What should be the size of our experiment??

The size directly impacts the precision. So if we want to detect a small change or to be more confident in the conclusion, it is advisable to run a larger experiment with more users.

To determine the right size, we need to consider the following situations —

### a — What should be our OEC (overall evaluation criteria)??

OEC needs to be identified carefully. For example, in our case, if we use a purchase indicator( i.e did the user purchase yes/no indicator) instead of revenue per user as our OED, the std error will be smaller and hence we might not need as many users to be exposed to the experiment.

### b— What should be our significance level??

If we increase our significance level saying that we no longer care about 1% change, only the high level bigger changes, we could reduce the sample size because bigger changes are easier to detect. For example, if we set our alpha i.e significance level to be 10% then we can conclude our results with 90% confidence rather than 99% confidence in the case of 1% alpha.

### c — what should be our p-value??

Similar to alpha if we want to use to lower the p-value threshold such as 0.01 to be more certain that a change occurred before we reject the Null hypothesis, we need to increase the sample size.

Few other considerations are — -

> I — How safe our experiment is?
> 
> If we are uncertain about the users reaction and we might loose our potential users in that cases we need to start with a smaller proportion of the users first.
> 
> II — balancing traffic requirements?
> 
> Does this experiment shares traffic with other experiments. we need to balance our traffic either by running them sequentially or parallely.

### 4 — how long do we run the experiment??

Factors to consider for the duration of experiments are —

> a — **Users**: users may vary over time. The longer the experiment runs, the more users the experiments get resulting in increased statistical power. however, this user accumulation rate is sub-linear as the same user may return. For example, if you have N users on day one you might have fewer than 2N users after 2 days since the same user can visit on both days.
> 
> b — **Day-of-week effect**: we need to capture the weekly cycle, as traffic might differ based on whether it's a weekday or weekend. It is recommended to run the experiment for a minimum of one week to capture the weekly cycle effect.
> 
> c — **Seasonality**: Traffic might vary based on seasonality. there might be more traffic in December due to the Christmas holidays or more traffic during summers due to the summer vacation of kids.
> 
> d — **Primacy and novelty effect**: some experiments might have a larger or smaller initial effect that takes time to stabilize. For example — users may try a new flashy button and might not find it useful and we see a decrease in CTR (click-through rate). On the other hand, there might be features that take time in adaptation. Users might take some time to get used to it. you might not notice an immediate effect but it can be beneficial in longer terms.

Our Experiment design is now ready yippie :)

let's summarize what all do we have —

> Randomization unit: user
> 
> Target audience: all user
> 
> To have 80% power to detect at least 1% change (Alpha: significance level) in revenue per user, we will conduct a power analysis to determine size.
> 
> Duration: We will run the experiment minimum for a week to capture the weekly cycle with a 34/33/33 % split among control/ Treatment 1 and Treatment 2.

Now we need to run the experiment and for that, we need both **Instrumentations** for logging user interaction data with the website and **Infrastructure** to be able to run the experiment ranging from experiment config to variant assignment.

Now what?? All done??

Well, any experiment is incomplete without **sanity checks**. To do that we need to look at **invariant metrics** as they are not going to change between the control and the treatment. Two main types of invariant metrics are —

> **Trust related guardrail metric** ( where the expectations are that the control and treatment samples to be sized based on the configuration or they have the same cache-hit ratios), **Organizational** **guardrail** **metrics** such as latency.

Yippie — we are done with running the experiment. We have done our sanity checks. All set to go.

Last but not least — The interpretation of results is also very important. We should be able to conclude or translate from our results whether to launch or change or not. Factors to keep in mind are —

> Do you need to make tradeoffs between different metrics? Example — if User engagement goes up and revenue goes down should we launch? Another example — if CPU utilization increases the cost of running the service may outweighs the benefit of the change.
> 
> What is the cost of launching this change?? We should consider both -> cost to fully build out the feature before launch and ->cost for ongoing engineering maintenance after launch.
> 
> What is the downside of making wrong decision?
