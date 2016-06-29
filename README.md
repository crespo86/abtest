# A/B test Final

<p style="text-align: left;"> sanghyun lee</p>

## Understanding the circumstance

Udacity courses currently have two options on the home page: "start free trial", and "access course materials". In this option, Udacity concentrate the first option "start free trial". The process about this option is like this.

<img src="/before udacity.png" width="800">

Udacity want to put a process which guide student, who have less time to take classes to choose "access course materials", after click "start free trial".

<img src="/after udacity.png" width="800">

Using thie new process, Udacity want to reduce the number of frustrated students who left the free trial because they didn't have enough time <**hypothesis**> and want to know it is practically effective or not.

## Experiment Design

### Metric Choice

- Invariant metrics (Number of clicks, Number of cookies)
  - As the upper image, I want to look at the data **after people click the "start free-trial"**, so data before people click the "start free-trial" can be invariant metrics.  
  - To make same size of control and experiment data, I have to make both's number of clicks similarly. Thus **Number of clicks** have to be invariant metric.
  - The **Unit of diversion** of this test is ""Cookie"", so I made **Number of cookies** to be invariant metric.
  - **Click-through-probability** is ( Number of clicks / Number of Cookies ). I already decide this two metrics to set invariant metrics. Therefore **Click-through-probability** have to be a invariant metric.
  - However, **Click-through-probability** is totally related with other 2 metrics, so I decide not to take this metric as an invariant metric.

- Evaluation Metrics (Gross conversion, Net conversion, retention)
  - Other 4 metrics are can be changed by the experiment. I choose some metrics which are significantly related to this test's subject.
  - **Number of user-ids"** is the count of user who start free-trial. For me, this metric is not lead any intuition alone. I don't want to use this alone. 
  - **Gross conversion** is ( Number of user-ids / Number of clicks after 14days from free-trial ). According to the hypothesis, the process lead some studant not to take free-trial and it means it might reduce Numver of user-ids. Therefore I want to see this metric gonna be significantly reduce or not. 
  - **Net conversion** is ( Number of user-ids who paid / Number of clicks after 14days from free-trial ). For the first time, I thought there are two kinds of student in this test. first is regretful student and second is sufficient student. I thought this new process is only for refretful student, so I don't need to check Net conversion metric. However I cannot conviced there is **no impect for sufficient student**, which means this process can lead more sufficient student than before. Thus I took this metric too. (want to know this metric is increased significantly or not)
  - **Retention** is ( Number of user-ids who paid / Number of user-ids ). It related with Gross conversion and Net conversion (Number of clicks is invariant metric). Thus I decide to take this metric as an invariant metric.
  
### Measuring Standard Deviation

- My Evaluation Metrics can apply analytic estimate and not to do another empirical estimate, since Unit of Analysis of My Evaluation Metrics are both Number of Clicks which is same to Unit of diversion. 

            | Gross conversion | Net Conversion | Retention
:-----------|-----------------:|--------------:|--------------:  
 Probability | 0.20625 | 0.1093125 | 0.53
 Std         | 0.4046 | 0.3120 | 0.4991
 SE          | 0.0202 | 0.0156 | 0.0549

- For calculate Gross convention and Net Conversioin's SE, I have to rescale the data. In given data, there are 40000 cookie per day and 3200 clicks per day. And I want to use 5000 cookie as my sample which is 400 clicks (calculated the ratio).
- 40000 : 5000 = 3200 : x -> x = 400
- for calculate Retention's SE, I rescaled as I did before. So I used 82.5 as number of enrollments.
- 40000 : 5000 = 660 : y -> y = 82.5

### Sizing

- I don't use Bonferroni correction because..
  - I just have 2 metrics which is not that many.
  - The metrics are too related so Bonferroni correction can make this test too conservative.

- Get appropriate Size
  - I used [this site](http://www.evanmiller.org/ab-testing/sample-size.html) to get appropriate sample size.
  - Given alpha is 0.05 and beta is 0.2
  - I used Gross conversion and Net conversion, since only this two metrics are significantly related with pageviews. (they are divided by clicks and clicks are related with pageviews invariably.)

            | Gross conversion | Net Conversion 
:-----------|-----------------:|--------------: 
 Baseline conversion rate | 0.20625 | 0.1093125 
 Minimum Detectable Effect  | 0.01 | 0.0075 
  Sample size          | 25,835 | 27,413 | 0.0549

  - the maximum sample size is 27,413. However this is the size of click, so I have to trans this click count to pageviews ( divided by 0.08) so, the number of pageviews are 342662.5
  - Last, for A/B test I need sample for A and B Both, So I make double. 0.5 is not a human so, I used 342663. Thus, The requied sample size is **685,326**.





