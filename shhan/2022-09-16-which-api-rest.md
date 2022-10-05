# [Which API?] 1 - REST

## 1. Preface

In this series of "_Which API?_", I will try to explain and compare the three most used API technologies:

- REST
- GraphQL
- gRPC

First, we will talk about REST.

> How do you design a REST API? When should you use REST?

These are probably the most popular interview questions asked when applying for any web development position. To answer these questions, let's dive into the topic.

## 2. Definition

#### API

Let's start by defining what an API is. An _application programming inteface (API)_ is a set of definitions and protocols for building and integrating application software; it can also be described as a way to communicate between two machines - the _client_ (consumer) calls the _server_ (provider).

An API allows a server to expose a uniform interface that the client can consume. This means that the internal details of an API system is hidden away from the user, and API developers can change the implementation freely as long as they conform to their own API.

#### REST

_Representational state transfer (REST)_ is a particular type of API technology focused on transferring data in a stateless and reliable manner.

> A web API conforming to the REST constraints is called a _RESTful API_.

In a RESTful API, when a client requests a resource using a REST API, the server _transfers_ back the _current state_ of the resource in a standardized _representation_.

In other words:

1. The server does not depend on client state to fulfill a request; instead, it will return relevant data that is persisted in the server
2. The server will return relevant data about a resource in a format that is understood by the client

Let's further explore these concepts by going over the principles set out by REST architecture.

## 3. REST Principles

To make an API service RESTful, certain principles and constraints must be satisfied.

#### Client-Server Separation

The client-server model enforces the principle of _separation of concerns_: separating the user interface concerns from the data storage concerns. As a result, the client and server can scale independently of each other.

#### Stateless

All calls with a REST API must be stateless. This means that every interaction is independent, and each request and response provides all the information required to complete the interaction. Every request by the client is interpreted by the server as a brand new ask — the server remembers nothing about past requests. Stateless transfer significantly reduces the memory load of the server and allows the system to scale without having to worry about overloading the server with too many requests.

Because each request sent to the server requires all the information to complete the request, you might have seen HTTP request headers like so:

```JSON
{
    "Accept": "application/json",
    "Content-Type": "application/json",
    ...
}
```

#### Uniform Interface

REST APIs should follow a common protocol for all requests and responses. Applications and servers are written in different languages that don't work together without an intermediary. Therefore, a uniform interface is a common language for any client to communicate with a REST API.

REST APIs are implemented over the HTTP protocol and use HTTP methods to manipulate data. To use HTTP with REST API, the client sends a request in a specific format, like shown below:

```HTML
GET http://example.com/person/1
```

In this example, `GET` identifies the HTTP method being used and `http://example.com/person/1` specifies the targets resource. The available HTTP methods include `POST`, `GET`, `PUT`, `DELETE`. Additionally, the id `1` identifies a unique resource, so that each unique resource is identifiable by a single URL.

After receiving a request, a server returns information about the target resource in a JavaScript Object Notation (JSON) format, which is easily consumed by browser clients and is readable by humans.

#### Cacheable

Caching occurs when media is stored on a client’s device when visiting a website. When a client returns to that site, the cached data is loaded quickly from local storage instead of being fetched again from the server. Caching saves server resources and bandwidth while decreasing page load time, which is why most large websites do it.

## 4. Why or why not REST?

We have concluded that REST is easy-to-use, flexible, scalable, and incorporate native web technologies. So why would any developer _not_ use REST?

The fact is that while REST is dominant in web APIs, other APIs may have different requirements that REST doesn't fulfill. For example, gRPC is widely used for large scale microservice architecture, as it is optimized for performance.

Therefore, developers should consider the below drawbacks of REST when implementing an API.

#### Over-fetching / Under-fetching

The most common issue of REST is that the client cannot compose / decompose requests to fetch only the required information about a resource. As a result, many developers face the situation of having to call multiple endpoints to fulfill a user request, or a user request fetching too much information.

#### Backend-driven Development

As endpoints and payloads are determined by the server, the development process tends to be driven by the backend. It is usually up to the frontend developer to utilize the available endpoints to fetch the required information to display on the UI.

---

To address the issues outlined above, Facebook (now Meta) developed a client-driven data query language called GraphQL. We will discuss how GraphQL evolved from the REST architecture in our next blog.
