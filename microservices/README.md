# Microservices

## Concept

* Microservices architecture refers to an approach for developing applications as a set of small loosely coupled services that uses a lightweight network protocol to communicate with each other [4]. As opposed to monolithic applications, in which the application comprises a single software artifact, a Microservices application is composed by a set of services, each one designed to perform a single and well-defined task. These services allow the development team to decouple several parts of the application using different frameworks, languages and hardware for each part of the system.
* The approach is targeted to the internal organization of an application not the application external boundaries such as its communication with other applications or services. By breaking the application complexity into a set of services, a change can affect only one component and not the whole application itself. Besides that, each service can be provided considering its hardware constraints using only the necessary resources and using the best technology for each purpose, leading to cost reduction with development and infrastructure 

## Success cases

* Gilt - http://www.infoq.com/news/2015/04/scaling-microservices-gilt. 

* Netflix - https://www.nginx.com/blog/microservices-at-netflix-architectural-best-practices

## Framework for Performance Test Specification

* This is a project that I created as an alternative to improve the performance test execution on Microservices.
* The main idea is to wrap in the service the test specification (the parameters that will be used to send a request to the service) along with some validation data that is used to validate the service response. This specification is kept under the same URI that the service use to provide the operation and its returned when the client sends an OPTIONS request. 
* With this approach we can keep the test specification up to date with new changes in the service and the test client can obtain the specification in an automated way. 
* This framework is specially useful for application with some dozens of microservices, in this scenario, keep each service specification consistent is a hard task. After each new change you will need to change the test client to keep the consistency with the service.
* For more information please refer to: https://github.com/asdcamargo/fpts

## Some References

* http://martinfowler.com/articles/microservices.html
* https://spring.io/blog/2015/07/14/microservices-with-spring
* http://www.3pillarglobal.com/insights/building-a-microservice-architecture-with-spring-boot-and-docker-part-i
* https://opensource.com/resources/what-are-microservices
* http://www.ibm.com/developerworks/websphere/library/techarticles/1601_clark-trs/1601_clark.html?ca=drs-&cm_mmc=dw-_-trs-_-social-_-generic
* NAMIOT, Dmitry; SNEPS-SNEPPE, Manfred. On Micro-services Architecture. International Journal of Open Information Technologies, v. 2, n. 9, p. 24-27, 2014
* Newman, Sam. Building Microservices. " O'Reilly Media, Inc.", 2015.




