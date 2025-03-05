# Review questions

## Microservice
- What are monolithic and microservice architecture? When should each be used?
What are the main advs and disadvs of each?
- What is the right process & organization structure to work with microservice?
- How to look at an app architecture from dif perspectives?
- What are the common ways to structure the logical view? What are the advs & disadvs of each?
- What is the key constraint of microservice architecture? What are its advs?
- What is a service? What does a service's API consist of?
- Is service size important? What are the signs of well and badly designed service?
- What are the steps to define the microservice architecture of an app?

## IPC
- What are the main types of interaction styles, categorized by dif dimensions?
- What types of API changes are backward compatible? How to handle major, breaking changes?
- What are the dif types of messaging formats? What are the advs and disadvs of each?
- What are the dif types of communication mechanisms between services?
What are the characteristics, advs, disadvs of each?
- How to define different types of async APIs?
- How to handle partial failure and protect callers when using RPC? How to recover from an unavailable service?
- What are the dif types of service discoveries? What are the main components, advs & disadvs of each type?
- How to match a response to a request when using async messaging?
- What are the main considerations when choosing a message broker?
- How to scale out receiver while preserving message ordering?
- What are the techniques to handle duplicate messages?
- How to ensure that a message is published as part of a transaction?
- What are the dif ways to replace sync interaction to improve availability?
What are the mechanism and tradeoff regarding each?
- (Chap 5) What data should be included in a domain event?

## Queries in microservices
- What are the dif ways to implement queries in microservices?
What should be the considerations when choosing between them? What is the architecture of each type?

## External API
- What are the main issues with client-invoking-services approach?
- What are the main functions of a typical API gateway?
- Which team should own the API gateway?
- What should be considered when designing an API gateway?
- What are the advs and disadvs of API gateway pattern? What advs does BFF pattern have over API gateway?

## Production-ready services
- What quality attributes should be ensured before deploying services to production?
- What aspects of security should be considered?
- What approach does monolith use to handle security for FE and API client?
- How does microservices handle authentication? Where can authorization be implemented and what is the tradeoff of each?
- What types of token can be used to handle authorization? What is the challenge with each type and how to handle it?
- What problem is solved by externalized config?
- What are the dif approaches to implement externalized config? What are the advs and disadvs of each?
- What is the goal of observability?
- Which observability aspects should be considered?
- What is the function of a health check endpoint?
- What is log aggregation? Which functions should a log infra support?
- Why is distributed tracing needed? How is it implemented?
- Why do we need application metrics? What are the dif types of metrics? What is its typical architecture?
- What are the attributes of a common metric sample?
- What is the responsibility of devs to have application metrics available?
What are the dif ways to send to metric service?
- Why do we need exception tracking when we already have logging? How is it implemented?
- What is audit logging? Why do we need it? Which info should be recorded? What are the dif ways to implement it?
- What is microservice chassis? What are the adv & disadv of it?
- What is a service mesh? Why do we need it? What functions does it serve?

## Deployment
- Why do we need automated deployment process & infra?
- What are the main functions of a production env?
- How to prevent bugs in new deployment from affecting users?
- What are the main deployment patterns? Which pattern should be considered first?
- What are the main advs and disadvs of deploying as a language-specific package & VM/container & serverless?
- What should be performed by the deployment pipeline in each pattern?
- What is Docker? What is the function of a Dockerfile? What is included in its content?
- What are the necessary steps to push and run a Docker image? What are the common arguments in `docker run` command?
- What is Kubernetes? What are its main functions? What are the main concepts and components in its architecture?
- What are the steps to deploy a service using Kubernetes? How to make a service accessible from the outside of a cluster?
- How to upgrade a running service in Kubernetes? How to roll back the deployment if bugs occur?
- What is Istio? What are the key concepts and components in its architecture?
How to utilize it to separate deployment from release?
- What is AWS Lambda? What are the dif ways to invoke a Lambda function?
