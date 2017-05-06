# P7 - A/B Testing
---
## Experiment Design
### Metric Choice

> List which metrics you will use as invariant metrics and evaluation metrics here. (These should be the same metrics you chose in > the "Choosing Invariant Metrics" and "Choosing Evaluation Metrics" quizzes.)

> For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.

1. Number of cookies ( Invariant )
Cookies are information kept by browsers for every site. Cookies as assigned when a user visit a site (URL) for the first time and persist within each browser until it expires or be cleared. So the number of unique cookies is mostly driven by the number of users and the number of different browsers people use to visit the site. Our experiment of showing the question should have no effect on the number of users or their browsing behaviour (how many different device and browser they use, or the frequency of clearing their cookies). Hence, we expect it to be invariant in our experiment.

2. Number of user-ids
This experiment is likely to results less user to enrol in the free trail. So it can't be used as an invariant metrics for validation.
It is also a poor choice for evaluation. The absolute difference of enrollment (user-id) between the experiment group and control group could
simple be a result of the difference in the number of people who click the 'Start free trail' button while the experiment doesn't have any real effect
on its intended goal.

3. Number of clicks ( Invariant )
The questionnaire is shown after users have clicked the "Start free trail" button. Hence, we don't expect any difference in the number of clicks. Therefore,
it can be used as an invariant metrics for validation.

4. Click-through-probability ( Invariant )
Click-through-probability is the ratio of Number of clicks and Number of cookies. As both number of cookies and number of clicks are expected to be invariant, we
will expect Click-through-probability to be invariant too.

5. Gross conversion (Evaluation)
If the experiment is effective, we expect the gross conversion to decrease. However, we hope the change in gross conversion it not significantly.

6. Retention (Evaluation*)
If the experiment is effective, we would expect the experiment group to have a higher retention as the experiment. (As it turns out, this metrics required too long to complete for the given alpha and beta, and hence not used in the final evaluation )

7. Net conversion (Evaluation)
Net conversion is essentially the product of gross conversion and retention. So given the gross conversion is likely to decrease and retention to increase, it is hard to tell how the net conversion is likely to change. However, it is clear that the intention of the experiment is to increase the net conversion. By setting the expectation upfront, more student will spend sufficient time on completing the course in the trail period and as a consequence stays beyond the trail period.

I will launch the experiment if the net conversion is both statistically and practically higher in experiment group than control as we are hoping the positive changes in retention will out weight its negative effect on gross conversion.

### Measuring Standard Deviation
>List the standard deviation of each of your evaluation metrics. (These should be the answers from the "Calculating standard deviation" quiz.)

>For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly, give your reasoning in each case.

| Metrics | Standard Deviation | Comparable to empirical ? |
|-|-|
| Gross conversion | 0.0202 | Yes |
| Retention | 0.0549 | No |
| Net conversion | 0.0156 | Yes |

The analytical estimate tends to be near the empirically estimates when the unit of diversion is the
same as the unit of analysis. Hence, I expect the estimate for gross conversion and net Conversion to be
comparable to empirical estimate. And the empirical and analytical estimate for Retention is not likely to
be comparable.

### Sizing
#### Number of Samples vs. Power

> Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately. (These should be the answers from the "Calculating Number of Pageviews" quiz.)

No. I will not use Bonferroni correction duration my analysis. Because the evaluation metrics is highly correlated, using Bonferroni correction, in this case, seems to be too conservative.

Using alpha = 0.05 and beta = 0.2, a total of 685,275 page views is required to conduct this experiment.

#### Duration vs. Exposure
> Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment. (These should be the answers from the "Choosing Duration and Exposure" quiz.)

> Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?

I don't think this particular experiment is particularly risky. Asking a single question before enrollment is not likely to cause bad user experiment.  

However, it is always a good practice to expose the experiment to a smaller subset of traffic whenever possible. There could be a bad implementation problem that causes user unable to complete the enrollment. And no matter how careful you are, there are always risks involved (i.e. Black Swan events).

Therefore, I would divert 50% of the traffic to this experiment. Based on this, the experiment would take 35 days to complete.

## Experiment Analysis
### Sanity Checks
>For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check. (These should be the answers from the "Sanity Checks" quiz.)

>For any sanity check that did not pass, explain your best guess as to what went wrong based on the day-by-day data. Do not proceed to the rest of the analysis unless all sanity checks pass.

| Invariant Metrics | Lower bound | Upper bound | Observed | Passes |
|-|-|-|-|
| Number of cookies | 0.4988 | 0.5012 | 0.5006 | Yes |
| Number of clicks on "Start free trail" | 0.4959 | 0.5041 | 0.5005 | Yes |
| Click-through-probability on "Start free trail" | -0.0013 | 0.0013 | 0.0001 | Yes |

### Result Analysis
>Effect Size Tests
For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant. (These should be the answers from the "Effect Size Tests" quiz.)

| Invariant Metrics | Lower bound | Upper bound | Statistically significant | Practically significant |
|-|-|-|-|
| Gross conversion | -0.029123 | -0.011986 | Yes | Yes |
| Net conversion | -0.011605 | 0.001857 | No | No |

### Sign Tests
>For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant. (These should be the answers from the "Sign Tests" quiz.)

| Invariant Metrics | p-value | Statistically significant |
|-|-|
| Gross conversion | 0.0026  | Yes |
| Net conversion | 0.6776 | No |

### Summary
>State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.

I didn't use Bonferroni correction. The two metrics Gross conversion and net conversion is most likely to be highly corrected.
Using Bonferroni correction will cause the tests to be too conservative.

There is no discrepancy between the effect size test and sign test. The difference in gross conversion is significant is both tests, and the difference in net conversion is not in both case.

### Recommendation
>Make a recommendation and briefly describe your reasoning.

Based on the result, I do *NOT* recommend launch the experiment.

While the gross conversion did decrease as expected.  Obviously, our goal here is not to decrease the gross conversion (we would always want higher gross conversion given everything stays the same). The experiment aims to increase in retention significantly while hoping than the gross conversion didn't change much, and hence results in higher net conversion. Given that the increase in Net conversion is not significant, I will not launch the experiment.

## Follow-Up Experiment
>Give a high-level description of the follow-up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.

#### description
This experiment we have examined in this project asked the student on the amount of time they had available to devote to the course. While time is an important factor, Lack of prerequisite skills and experience could also
students' frustration.

In addition to the time commitment, I propose to have questions that ask the students about their previous experience, for example, whether the student has any coding experience in Python. If the user doesn't have any of the specified skills, then asking the whether the student whether they want to enrol in the more appropriate course or degree instead (i.e. introduction to programming)

#### unit of diversion
The proposed experiment is essentially the same as the one we have examined in the project. Hence, the
same unit of diversion could be used (cookies)


#### Invariant metrics
We could use the same metrics used in this project including, number of clicks, number of unique cookies,
and Click-through-probability.

#### Evaluation metrics
We could use the same metrics used in this project, most importantly, the net conversion.

#### hypothesis
_null hypothesis_: asking questions regarding student background before the student will not change the net conversion significantly.
_alternative hypothesis_: asking questions regarding student background before the student will increase the net conversion significantly.
