---
title: "The Dangers of Guaranteed Data"
date: 2015-09-27
description: Data Providers, Error Handling, Architecture
---

Imagine you’ve built an application that helps users decide when to buy stocks. In order to build this, you’ve leveraged the services of a third party that when given a particular stock returns to you a ‘yes’ or ‘no’ answer as to whether you should purchase the stock. This system works wonderfully on the surface. Helping people to make more money than they would have otherwise. However, what happens when the service you’ve integrated stops conforming to the standard you had expected? It turns out more goes wrong that just missing opportunities to classify that data. It can have drastic, trust-destroying, consequences for your end users.

# What Went Wrong

The team I was working on had been leveraging a service similar to the example given above. We had been using it to help our customers discover which of their prospects were interested in the products and services they were attempting to sell. It even worked in the opposite case and give users insight into which of their prospects were disinterested, or even those they had incorrect information for. This system required an inherent amount of trust between our users and our system. They relied on our system to tell them which leads were hot, cold or bad. Without this trust, what advantages does our product have over the competitors?

The rub was, hundreds of these records were going unclassified every day. This was due to the fact that we had assumed our service would behave in one way and one way only. In reality, there was much more variance in the responses we got. Framing it in the context of the example given. It would be as if instead of just ‘no’, the service returned to you ‘No, but this stock may rise in value in the next 30 days.’. You can see, that we were missing out on huge amounts of contextual information as a result of not accounting for such variances. Such a lack of insight led to hundreds of interactions for our clients going unanalyzed. Even worse still, due to the lack of visibility we had no idea that this was even a problem.


# Things We Could Have Done Better

Firstly, don’t take any attributes in your data for granted. We had always assumed that fields we were leveraging were either well formed and useful or useless. This black and white way of thinking was dangerous and severely limited us in terms of the amount of data we could successfully process. The amount of contextual information provided by the sentence ‘No, but this stock may rise in value in the next 30 days’ could potentially be the difference between a huge capital gain and none at all.

Secondly. Log everything. If you’re dealing with data that is supposedly guaranteed, log your success and failure cases. It was only after we introduced extensive logging into this area of our system that we were able to identify this key pitfall. Even better, use logging in conjuction with tools like [SumoLogic][sumologic] or [Splunk][splunk] to help visualize and identify issues with your system.

Lastly, be aware of failure or issue rates on a per-user basis. Originally we were observing the success rate of the system as a whole. Error rates were low, and users were generally content. However, had we been more granular in our approach, we would have seen that some users experiences exponentially higher failure rates than others. Was this because they were using the product incorrectly? Most likely no, they just got to be the unlucky soul that was interacting with malformed data that particular day.

# In Conclusion

In conclusion, regardless of your focus or intent with the data you analyze, don’t take it for granted. Don’t assume guaranteed attributes will always be guaranteed. Defensively parse your data and log every edge case you can think of. Ensure you’re examining the data at the most granular level you can. Just catching one of these particular edge cases can help to make your system more reliable. Even more importantly, it can help to build trust between you and your end user.

[sumologic]: https://www.sumologic.com/
[splunk]: http://www.splunk.com/
