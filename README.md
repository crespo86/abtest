# A/B test Final

<p style="text-align: left;"> sanghyun lee</p>

## Understanding the circumstance

Udacity courses currently have two options on the home page: "start free trial", and "access course materials". In this option, Udacity concentrate the first option "start free trial". The process about this option is like this.

<img src="https://raw.githubusercontent.com/crespo86/abtest/master/before%20udacity.png" width="800">

Udacity want to put a process which guide student, who have less time to take classes to choose "access course materials", after click "start free trial".

<img src="https://raw.githubusercontent.com/crespo86/abtest/master/after%20udacity.png" width="800">

Using thie new process, Udacity want to reduce the number of frustrated students who left the free trial because they didn't have enough time <**hypothesis**> and want to know it is practically effective or not.

## Experiment Design

## Hypothesis
Before move on, I need to set Hypothesis.

H0 (Hypothesis Null) : The new process has no effect to change number of frustrated students who left the free trial because they didn't have enough time

H1 (Alternative Hypothesis) : The new process has effect to change number of frustrated students who left the free trial because they didn't have enough time

Also, I need another Hypothesis. In upper image udacity want to put a new process on the "click free trial", which means it can effect to the number of students who are not frustrated through "free-trial".

H0 (Hypothesis Null) : The new process has no effect to change numver of not frustrated students who happy with free trial.

H1 (Alternative Hypothesis) : The new process has effect to change numver of not frustrated students who happy with free trial.

In this test, I expect that first H0 is reject and second H0 is not reject in the same time.

### Metric Choice

- Invariant metrics (Number of clicks, Number of cookies)
  - As the upper image, I want to look at the data **after people click the "start free-trial"**, so data before people click the "start free-trial" can be invariant metrics.  
  - To make same size of control and experiment data, I have to make both's number of clicks similarly. Thus **Number of clicks** have to be invariant metric.
  - The **Unit of diversion** of this test is ""Cookie"", so I made **Number of cookies** to be invariant metric.
  - **Click-through-probability** is ( Number of clicks / Number of Cookies ). I already decide this two metrics to set invariant metrics. Therefore **Click-through-probability** have to be a invariant metric.
  - However, **Click-through-probability** is totally related with other 2 metrics, so I decide not to take this metric as an invariant metric.

- Evaluation Metrics (Gross conversion, Net conversion)
  - Other 4 metrics are can be changed by the experiment. I choose some metrics which are significantly related to this test's subject.
  - **Number of user-ids"** is the count of user who start free-trial. As the hypothesis, Alteritive hypothesis expect change Number of user-ids so it can be an evaluation Metric. However we set Number of clicks invariantly, Gross conversion and Number of user-id have same meaning. In those two metric, Gross conversion might be normal distribution, so I decide choose Gross conversion and drop number of user-ids.
  - **Gross conversion** is ( Number of user-ids / Number of clicks after 14days from free-trial ). According to the hypothesis, the process lead some studant not to take free-trial and it means it might reduce Numver of user-ids. Therefore I want to see this metric gonna be significantly reduce or not. As first Hypothesis, I want to see this metrics gonna be decreased.
  - **Net conversion** is ( Number of user-ids who paid / Number of clicks after 14days from free-trial ). I choose this metric as a evaluation metric for second Hypothesis. I expect that this metric not to change.
  - **Retention** is ( Number of user-ids who paid / Number of user-ids ). It related with Gross conversion and Net conversion (Number of clicks is invariant metric). Which means, It can be increased of decreased depend on difference of Variant of Gross conversion and net conversion. I don't choose this metric as an evaluation metric. Cuz, IF Gross conversion and Net conversion are both effected by this new process, this metric can calculate the difference of this two effect, So board menber or owner of Udacity can decide what they decide to do or not to do. However this is not show First and second Hypothesis. which means whether this metric is decreased or increased or unchanged, I cannot make an intuition of first and second Hypothesis. The meaning of decreasing this metric is that diff of variance of user-ids is getting lower than variance of User-ids who paid.

### Measuring Standard Deviation

- My Evaluation Metrics can apply analytic estimate and not to do another empirical estimate, since Unit of Analysis of My Evaluation Metrics are both Number of Clicks which is same to Unit of diversion.

            | Gross conversion | Net Conversion
:-----------|-----------------:|--------------: 
 Probability | 0.20625 | 0.1093125
 Std         | 0.4046 | 0.3120 
 SE          | 0.0202 | 0.0156 

- For calculate Gross convention and Net Conversioin's SE, I have to rescale the data. In given data, there are 40000 cookie per day and 3200 clicks per day. And I want to use 5000 cookie as my sample which is 400 clicks (calculated the ratio).
- 40000 : 5000 = 3200 : x -> x = 400


### Sizing

- I don't use Bonferroni correction.

- Get appropriate Size
  - I used [this site](http://www.evanmiller.org/ab-testing/sample-size.html) to get appropriate sample size.
  - Given alpha is 0.05 and beta is 0.2
  - I used Gross conversion and Net conversion, since only this two metrics are significantly related with pageviews. (they are divided by clicks and clicks are related with pageviews invariably.)

            | Gross conversion | Net Conversion
:-----------|-----------------:|--------------:
 Baseline conversion rate | 0.20625 | 0.1093125
 Minimum Detectable Effect  | 0.01 | 0.0075
  Sample size          | 25,835 | 27,413

  - the maximum sample size is 27,413. However this is the size of click, so I have to trans this click count to pageviews ( divided by 0.08) so, the number of pageviews are 342662.5
  - Last, for A/B test I need sample for A and B Both, So I make double. 0.5 is not a human so, I used 342663. Thus, The requied sample size is **685,326**.

  - This is not a high risk. 
  - For company side, this can effect just some of **new students**, so It cannot be a huge part of revenue.
  - This is not an implement of new program. It is just direction(link), So It cannot make huge problems using Udacity homepage.
  - This new process dosen't have some ethically important data of student. So It cannot make huge problems of students personal infomation.
  - However, It exactly have some possible problems, so I do not use this all 100%.

## Experiment Analysis

### Sanity Checks

Before I analysis the test, I need to do sanity checks for my invariable metrics.

            | Number of cookies | Number of clicks
:-----------|-----------------:|--------------:
 cont | 345,543 | 28,378
 exp  | 344,660 | 28,325
 P      | 0.5 | 0.5
 SE      | 0.0006 | 0.0021
 M     | 0.0012 | 0.00412
 Inner bound      | 0.4988 | 0.4959
 outer bound      | 0.5012 | 0.5041
 observe          | 0.5006 | 0.5005

 - To calculate SE, I used p 0.5 (cuz I made amount of two sample even) and use _sqrt(P * (1-P)/(cont+exp))_.
 - Observed value of Number of cookies is **0.5006** and located between inner bound (0.4988) and outer bound (0.5012) so It can be passed.
 - Observed value of Number of clicks is **0.5005** and located between inner bound (0.4959) and outer bound (0.5041) so It can be passed.

### Result Analysis

Since I pass all sanity check, I can analysis my evaluation metrics.

|gross conversion | cont    | exp    | retention | cont   | exp    | net conversion| cont    | exp    |
|-------------|---------|--------|-----------|--------|--------|-------------|---------|--------|
| enroll      | 3785    | 3423   | pay       | 2033   | 1945   | pay         | 2033    | 1945   |
| clicks      | 17293   | 17260  | enroll    | 3785   | 3423   | clicks      | 17293   | 17260  |
| e/c         | 0.2189  | 0.1983 | p/e       | 0.5371 | 0.5682 | p/c         | 0.1176  | 0.1127 |
| diff        | -0.0206 |        | diff      | 0.0311 |        | diff        | -0.0049 |        |
| p pooled    | 0.2086  |        | p pooled  | 0.5519 |        | p pooled    | 0.1151  |        |
| se          | 0.0044  |        | se        | 0.0117 |        | se          | 0.0034  |        |
| m           | 0.0086  |        | m         | 0.023  |        | m           | 0.0067  |        |
| low         | -0.0291 |        | low       | 0.0081 |        | low         | -0.0116 |        |
| upper       | -0.012  |        | upper     | 0.0541 |        | upper       | 0.0019  |        |
| statistically | significant|   | stastically | significant|  | statistically | not significant| |
|practically | significant|      | practically | not significant | | practically | not significant| |

I tried sign test using [this site](http://graphpad.com/quickcalcs/binomial1.cfm).

|           | Gross conversion | Retention | Net conversion |
|-----------|----------------:|----------:|----------------:|
| successes |               19 |        13 |             10 |
| trial     |               23 |        23 |             23 |
| P         |              0.5 |       0.5 |            0.5 |
| P-value   |           0.0026 |    0.0026 |         0.0026 |
|statistically| significant| not significant| not significant|

- In effect size test, Gross conversion metric's diff is -0.0206 which is in low and upper bound. Also it is not in +- 0.01, so it is statistically and practically significant. retention metric's diff is 0.0311 which is in low and upper bound. However it is in += 0.01, si it is statistically significant and practically not significant. Net conversion's upper and low bound incloud 0, and it is in +- 0.0075, so it is both not significant.

- In sign test, just Gross conversion got under 0.05 P-value, So, It is statistically significant.

- just Retention, the two test result is different. Actually I don't know why they are different. However I can say why retention metric is not significant in sign test. I calculate each Gross conversion diff and net conversion diff's variance. and Net conversion's variance is more than Gross conversion. Retention is really related with both two metric, so even if gross conversion is highly significant, this metric get more effect from Net conversion.

- I don't use Bonferroni correction because..
  - This A/B test need take twice both. (reject first H0, and leave Second H0)
  - Bonferroni correction is used if the test need any rejected metrics when multifple metric used. 
  - In this test, even if first H0 is rejected, we cannot use this when second H0 is decreased. So We don't have to use Bonferroni correction.

### Recommendation

- I recommend udacity take the process.
- In Gross conversion, we can get significant result. which means we reject the Null of hypothesis. The process will reduce the students who frustrated after enroll free-trial.
- In other two metric, we cannot get significant result. However it has a good meaning. these metrics are related the student who are ready to pay. As I mentioned before, I think this is not fit to this project's hypothesis. However It show **there is no side effect for student who are ready to pay**. (if this score get negative effect, I have to think about adapt the new prosess more.)

### Follow up experiment

- I'm just think about Udacity global market. (Because I am the one!)
- English is good because most of computer programming knowledge is from english document so I have to study this language for my progress.
- However when I used forum, there is a problem. **Udacity teachers work in american time! (maybe)** Whenever I submit my assignment or question on the forum, it have to responsed at least tomorrow. Usually 2 am or 3 am. 
- I don't know How many people in Asia (normally in China) using Udacity. However If it is large or getting larger of udacity want to make asia student more, it is good to make some teacher for asian time!
- I want to make hypothesis like this "using teacher for asian time make more asian student", but it take longlong time which means it is not good subject for A/B test. So I changed it "using teacher for asian time make more participation rate of asian student." As I mentioned, MOOC is getting huge in over the world, and increasing company need good reputation as much as revenue.

- hypothesis : using teacher for asian time make more asian participation rate.
- H-null : using teacher for asian time cannot make more asian participantion rate.
- Unit of diversion : user-ids of asian region (it can addressed by IP, or credit card information and so on.)
- invariant metrics : number of user-ids of asian region. number of class
- variant metrics : number of submit(test), number of user-ids who used forum, number of discussion.

Plz do this test!! and make teacher for asian timeline ^^
