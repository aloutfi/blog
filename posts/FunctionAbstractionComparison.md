# Function Abstractions Comparison (FaaS)

Context: As a developer who has never used functions before, should I use Amazon Lambda or Google Cloud Functions to learn about how they work?

Before I even talk about Function Abstractions, lets define what FaaS is first:

> FaaS is about running backend code without managing your own server systems or your own long-lived server applications.
>
> FaaS offerings do not require coding to a specific framework or library. They (FaaS functions) are regular applications when it comes to language and environment.
>
> Horizontal scaling is completely automatic, elastic, and managed by the provider.
>
> Functions in FaaS are typically triggered by event types defined by the provider OR are triggered as a response to inbound HTTP requests

 From Martin Fowler’s article about [Serverless Architecture](https://martinfowler.com/articles/serverless.html#unpacking-faas)

Essentially, FaaS is an event-driven concept that allows for the execution of some piece of functionality based on some type of stimuli. Since these functions are all executing code in the same environment, the cloud provider is able to increase or decrease the number of them that are running to fit end-user computing needs.

## AWS Lambda vs Google Cloud Functions

For the sake of simplicity, I am keeping my evaluation criteria limited to supported languages, logging, and community support.

### AWS Lambda

| Supported Languages                                          | Logging                                     | Community                    |
| ------------------------------------------------------------ | ------------------------------------------- | ---------------------------- |
| Node.js, Python, Java, Go, C# via the .NET core. Custom runtime support was added in 2018. | Function metrics are sent to AWS CloudWatch | Launched in November of 2014 |



#### Google Cloud Functions

| **Supported Languages**     | **Logging**                                                  | **Community**            |
| --------------------------- | ------------------------------------------------------------ | ------------------------ |
| Node.js, Python, .NET, Ruby | As `stdout` to Google Cloud Console can be configured to utilize Google Stackdriver | Launched in July of 2018 |



#### Supported languages:

More languages supported does not always mean better. For example: an application running in C would be ill-suited for FaaS as much of C happens at a lower level than the supported languages. While AWS Lambda technically supports all languages via the custom runtime it is a good lession in just because you can doesn’t mean you should.

If I needed to run Ruby code it would be much easier to run on Google Cloud Functions due to the fact that the language is directly supported.

#### Logging:

Both Lambda and Cloud Functions utilize their providers logging systems. It is nice that GCP shows logging directly in console.

#### Community:

AWS has more users and Lambda has been around for significantly longer than Cloud Functions. 

#### Startup Time.

Per the [2021 Cockroach Labs Cloud Report](https://resources.cockroachlabs.com/guides/2021-cloud-report),  I thought that GCP would have the least amount of latency, leading me to  believe Google Cloud Functions would be better in terms of “cold starts”. That said, I found an [article](https://www.simform.com/aws-lambda-vs-azure-functions-vs-google-functions/) that found the contrary:

AWS Function Startup Time: ~39 ms

GCP Function Startup Time: ~100-493 ms

Azure Function Startup Time: ~3640 ms.

AWS Lambda is the clear winner.

#### Pricing

Both providers have a free tier that allows for discovery and non-heavy usage. From there, usage considerations are determined to consider monthly totals. 

#### Triggering

Both AWS and GCP function abstractions support triggering via REST API calls and triggers from internal components. However, AWS Lambda does not depend on event sources.



## Conclusion:

I was tempted to chose AWS Lambda based off community support. It has been around for much longer, and is the subject of much more research. Much of the original literature about serverless that is available is based off of AWS Lambda, including the [article](https://martinfowler.com/articles/serverless.html#unpacking-faas) from Martin Fowler’s bliki.

> "If one is to understand “the great mystery” one must study all it’s aspects, not just the dogmatic narrow view of the Jedi” - Chancellor Palpatine 

That said, what would I be missing out on looking at a newer implementation. Learning about functions from both abstractions would provide a valuable lesson for me a as a developer to compare both systems and understand their usage.

One thing I need to be careful about when deciding whether or not to employ FaaS is its ability to become an anti-pattern. As this document deals with the nature of FaaS vs when to use it, I am leaving this topic out of scope. That said, I will mention that FaaS is a better solution than containerization when the task being run does not have complex requirements that would need to be installed on an operating system level. An example of an application better suited for containerization is a python machine learning application that invokes the execution of code written in R. Having more exposure to different function abstractions would allow me to further discover criteria I would use to determine usage.

As a developer who has never used functions before, I would therefore opt to implement a task on AWS Lambda and then implement it a Google Cloud Function. 