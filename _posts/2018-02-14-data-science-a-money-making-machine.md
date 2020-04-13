---
layout: post
title: Data Science – A Money Making Machine?
bigimg: /img/bitcoin.png 
#gh-repo: SubmitCode/Comparison-Of-Algorithms
#gh-badge: [star, fork, follow]
published: true
tags: [AI]
comments: true
---
**Imagine you are sitting at home and a piece of software is running somewhere on a cloud that makes money for you – 24 hours a day, 7 days a week, always at full capacity and never sick. The idea is appealing. Is something like this possible? In the media, we constantly hear of high-frequency traders who win millions by trading within a very short period of time. Is it possible for a team of young, enthusiastic data scientists to create a profitable trading algo in their free time? In this short post, we would like to present our data science journey from the idea to the implementation.**

We live in a wonderful time of digitalization right now. For us, data scientists, this means an abundance of data. It has never been as easy as today to get your hands on data – a true land of plenty for a data scientist. To implement an algorithm, we first need the “basic feed” of any data scientist – data, data, and more data. This is why we first get data from various cryptoexchanges. Why cryptoexchanges? Simply because there is no other place where you can get such good quality data for free. Exchanges such as GDAX, Gemeni, Bitstamp even offer websocket feeds and publish the entire order book. By contrast, comparable data from well-known exchanges, such as the New York Stock Exchange or Xetra, are unaffordable for a private investor. Since the quantities of data are sometimes huge (for example, the GDAX exchange receives several hundred messages per second), we decided to use Splunk. The advantage of Splunk is that it is very easily scalable and we could save and analyze differently structured and formatted data very easily. In addition, we could easily set up alarms and create dashboards, which was a plus for later operation.

After an initial analysis, we detected clear price differences among various exchanges, which we thought we could benefit from. So we analyzed the order book in detail. However, after deducting the trading fees, we were left with next to nothing. Of course, we did not want to give up at this point. We continued our research and loaded more data from other exchanges in our system. We also tried to get better prices through “intelligent” placement of limit orders. Lo and behold: We found a strategy that is profitable at least “on paper”. Now came the tricky part. We had to write a code that would trade as fast as possible and simultaneously on various exchanges. We decided to use Python and a service-oriented architecture with a Message Que (ZeroMQ) for this.

One of the challenges of bitcoin arbitrage of similar systems is that, on the one hand, the bitcoins have to be transferred from one exchange to another, and, on the other hand, the money has to be transferred from one exchange to another. Modern APIs provide this option, but sadly not all the exchanges we wanted to trade on. As a result, our algorithm still needed people to make the transfers. We found a solution for this as well though: With the help of our “new” robotics team, we were able to automate this step using UiPath. This way, the algorithm worked 100% automatically, without manual interventions.

You may be wondering how much profit such a strategy can bring. There is no “sweeping” answer to this, and the following factors need to be considered in order to make an estimate:

- What is the daily payout limit of the exchange?
- How long does it take to transfer the fiat money from one trading account to another?
- Do I hedge the physical bitcoins with a short futures position? Keep in mind: You get about USD 40,000 in margin per bitcoin that you short. 

The example shown here illustrates very well that data science is a link between many fields. In the beginning, data analysis knowledge was needed. Later, it was important to develop software and set up the right IT infrastructure. And last but not least, it was and is important to know the exact regulatory requirements and understand payment transactions. This interdisciplinary focus is precisely the strength of the Inventx Data Science Team, comprising computer scientists, mathematicians, technical experts and experienced project managers.