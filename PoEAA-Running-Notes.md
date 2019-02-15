## General
1. This book is about how you decompose an enterprise application into layers and how these layers work together.
2. This book in general deals with Enterprise Applications i.e. applications that deals with huge and complex data.
3. Enterprise Applications include payroll, patient records, shipping tracking, cost analysis, credit scoring, insurance, supply chain, accounting, customer service  and foreign exchange trades.
4. Enterprise Applications don't include automobile fuel injection, word processor, elevator controllers, chemical plant controllers, telephone switches, operating systems, compilers and games.
5. Enterprise Applications usually involve persistent data. Data is persistent because it needs to be available for multiple runs of the programs and in most cases for many years to come.
6. Enterprise Applications usually need to integrate with other applications.
7. Choosing an architecture for an enterprise app. will depend upon the type of the appl., for instance a b2c online retailer will have a different arch. from an system that automates the processing of leasing agreements and this will be different from an app., like that of an expense tracking system which might have to be integrated with other applications or might have to make webservice calls to consume data from an airline ticketing system.
8. Many architectural decisions are about performance.
9. For most performance issues, the preferred way is to get to the system up and running, instrument it, and then use disciplined optimization process based on measurement.
10. Response time: is the amount of time a system takes to process a request from the outside. This may be a UI action, like clicking a button or a server API call.
11. Responsiveness: is about how quickly a system acknowledges a request as opposed to processing it. This is imp. because in many systems users become frustrated if a system has low responsiveness even if the response time is good. Providing a progress bar during file copy is an example of good responsiveness.
12. Latency: is the minimum time required to get any form of response. An application dev can't do much about latency because it depends upon the request and response speeds between networks, the best way is to keep remote calls as minimal as possible.
13. Throughput: is how much stuff you can do in a given amount of time. For a file copy, it's measured in bytes per sec whereas in an enterprise app. it is measured as transactions per second.
14. Performance can be about Response time or Responsiveness or Throughput. From a user perspective, responsiveness is crucial.
15. Load: is about how much stress a system is under which maybe no.of users connected to the system right now. Response Time and Load are used together. For e.g., the response time of a system could be 0.5 seconds w/ 10 users and 2 seconds w/ 20 users.
16. Load Sensitivity: is an expression of how the response time varies w/ load.
17. Efficiency is performance divided by resources. A system that can get 30 tps on 2 cpu's is more efficient than a system that can get 40 tps on 4 identical cpu's. 
18. Capacity of an system is the maximum effective throughput or load a system can take above which the performance dips below acceptable threshold.
19. Scalability is a measure of how adding resources (usually hardware) affects performance. A scalable system is one which allows you to add hardware and get a increase in performance.
20. Vertical Scalability means adding more power to a single server such as more memory. Also called as scaling up.
21. Horizontal Scalability means adding more servers. Also called as scaling out.
22. When building enterprise applications, it is often better to build for hardware scalability rather than capacity or even efficiency. Because scalability gives the option to increase performance if needed and it is easier to do.
23. Often designers do complicated things that will improve the capacity on a particular hardware platform when it might actually be cheaper to buy ore hardware.

