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

- Evaluation Metrics (Gross conversion, Net conversion)
  - Other 4 metrics are can be changed by the experiment. I choose some metrics which are significantly related to this test's subject.
  - **Number of user-ids"** is the count of user who start free-trial. For me, this metric is not lead any intuition alone. I don't want to use this alone. 
  - **Gross conversion** is ( Number of user-ids / Number of clicks after 14days from free-trial ). According to the hypothesis, the process lead some studant not to take free-trial and it means it might reduce Numver of user-ids. Therefore I want to see this metric gonna be significantly reduce or not. 
  - **Net conversion** is ( Number of user-ids who paid / Number of clicks after 14days from free-trial ). For the first time, I thought there are two kinds of student in this test. first is regretful student and second is sufficient student. I thought this new process is only for refretful student, so I don't need to check Net conversion metric. However I cannot conviced there is **no impect for sufficient student**, which means this process can lead more sufficient student than before. Thus I took this metric too.
  - **Retention** is ( Number of user-ids who paid / Number of user-ids ). like Click-though-probablity, It totally related with Gross conversion and Net conversion (Numver of clicks is invariant metric). Thus I decide not to take this metric as an invariant metric.
  


