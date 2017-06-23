# Automated Fight Rescheduling using Gradient Boosted Tree Regression
#### Joshua E. Jodesty

#### Background & Hypothesis:

Flight delays are an ongoing problem and are expensive and inconvenient for passengers, airlines, and
Air Traffic Control (ATC). Developing a system that reduces flight delays involves an understanding of the
complex relationships between airlines, ATC, and airports, as well as ATC’s application of regulations
stipulated by the National Airspace System (NAS). Flight delays are difficult to reduce because delays,
runway congestion, and ATC operations have a cyclic causality pattern. All causes of this pattern affect
each other. This pattern implies that solutions for reducing delays are biased in favor of certain
stakeholders in the aviation industry. Each stakeholder defends their own objectives. Although ATC
plays a primary role in breaking this cycle of inconvenience, their primary objective is to prevent flight
collisions and expedite air traffic flow. This objective is misaligned with airlines’ primary objective to
increase revenue curtailed by flight delays. Reducing flight delays can increase airline revenue with the
opportunity to maximize flight frequency and/or customer satisfaction (Note: It is less likely for
customer satisfaction to improve with increased flight frequency because it will also result in increased
air-traffic congestion which will lengthen flight delays).

Despite these conflicts of interest, ATC and airlines share the incentive to reduce runway congestion.
Therefore, reducing congestion is the most effective way to break the causality pattern and placate
opposing stakeholders since reducing congestion is mutually beneficial to both ATC and airlines. The ATC
reduces congestion by using flight plans submitted by the airlines to reschedule, reroute, and prolong
take-off of flights when runways are congested. Although these operations are crucial to reduce runway
congestion, these techniques can also contribute to the congestion it is intended to reduce due to the
cyclical causality of flight delays and runway congestion.

#### Proposal:
I developed a scalable data pipeline using Apache Spark’s Scala API that can train a cross-validated
Gradient Boosted Tree Regressor to estimate runway congestion time. When deployed, ATC can
automate flight rescheduling and rerouting by providing an application with a model that feeds flight
plans and airline leased terminal times as dependent variables, appling a function that choses the flight
plan with the lowest estimated runway congestion time, and replies to airlines with modified flight
plans. 

#### Technology Suite:
I used a Docker containerized distribution of Apache Spark to build the data pipeline. Although I’m
spinning a single node cluster configuration and my dataset isn’t large, I have the ability to improve
model performance by scaling the pipeline to connect to the head node of spun cluster to process more
data. I used Spark's Scala API for data pre-processing, feature engineering, and machine learning, and
model evaluation. I decided conducted exploratory data analysis and model evaluation within this
container using Python’s Seaborn and SciKit-Learn.

#### Dataset:
I trained this model using "On-Time Performance" data provided by the United States Bureau of
Transportation Statistics. This data contains domestic flight information by major airlines for non-stop
domestic flights. In order to procure normally distributed data and avoid memory constraints of my
personal machine, I filtered the dataset only include flights routed through airports in New York state
and flights between November 2015 and October 2016 to encapsulate holidays that impact air and
runway traffic.
