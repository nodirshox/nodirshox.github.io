---
layout: post
title: "Microservices for kids"
categories: ["tutorial", "programming"]
permalink: /microservices-for-kids
---

The number of Internet users is increasing rapidly. So in order to handle massive loads, we need such a technology which can be used. In the past, we had or even now most applications have a **monolithic** structure. This architecture is easy to use for small functional applications. All codebase stay in one bundle(repository). Once an application getting complex logic, it will be hard to add another function or debugging. Another disadvantage is to handle high loads. Yes, you can say that you can upgrade memory of server. But, it is costly.

In such a scenario, we can apply **Microservice** architecture to our application. There are plenty of plus sides:

1. All services separated and can be developed n number of developer in any language.
2. If one functions fails to perform, rest of logic still works.
3. It easy apply load balancing solutions.
4. You can choose multiple databases for your application.
5. You can use latest HTTP protocol. For example, HTTP2/3
6. Easy to scale.

Now, you can imagine how it works by analyzing picture below.

![Microservices](/assets/2020-12-20-microservice/microservice.jpg)

**ncube.com**

API Gateway - connects all endpoints into a single point. This means, all your services call to API Gateway using RPC calls. We can use GRPC, then time transmission will increase by 10x by comparing simple REST API. GRPC uses HTT2 protocol and you need code Proto in order to keep type of messages. Golang language is perfect for building API Gateway for its high speed.

Here useful links:

[https://grpc.io/](https://grpc.io/){:target="_blank"}

[https://ncube.com/blog/microservices-vs-monolithic-which-architecture-suits-best-for-your-project](https://ncube.com/blog/microservices-vs-monolithic-which-architecture-suits-best-for-your-project){:target="_blank"}

[https://microservices.io/patterns/apigateway.html](https://microservices.io/patterns/apigateway.html){:target="_blank"}

[https://microservices.io/](https://microservices.io/){:target="_blank"}

[https://github.com/nodirshox/nodejs-service](https://github.com/nodirshox/nodejs-service){:target="_blank"}

[Link](https://ergashevn.blogspot.com/2020/12/microservices-for-kids.html){:target="_blank"}