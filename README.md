# FullStackJavaScript Flow 4b

## GraphQL
### https://github.com/grem848/mini-project-fullstackjs2019
### https://github.com/pernillelorup/mini-project-native-app


>## Explain shortly about GraphQL, its purpose and some of its use cases

### GraphQL Explained & Purpose
* GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. 

* GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

* GraphQL got its start at big old Facebook, but even much simpler apps can often bump into the limitations of traditional REST APIs.

* Provides a query language like REST that can fetch all needed data in one easy fetch unlike REST.


### GraphQL Use Cases

* For large complicated fetches with lots of data and arrays GraphQL provides an easy way to query

* With GraphQL you also don't risk overfetching, because you write the specific data you want. 


<br>

>## Explain some of the Server Architectures that can be implemented with a GraphQL backend

GraphQL can be used to setup endpoints for fetching data from a database.

<br>

>## What is meant by the terms over- and under-fetching in relation to REST

### Over-fetching
Over-fetching is fetching too much data, meaning there is data in the reponse you don't use.

### Under-fetching
Under-fetching is not having enough data after calling to an endpoint, leading you to call a second endpoint with is inefficient.

In both cases, they are performances issues : you either use more bandwidth than you should, or you are making more HTTP requests that you should.

GraphQL fixes this by letting you select the data you need in a simple way, it could also be achieved with REST by using DTO's.
GraphQL doesn't allow overposting, due to the built-in schema validation.

<br>

>## Explain shortly about GraphQL’s type system and some of the benefits we get from this


<br>

>## Explain shortly about GraphQL Schema Definition Language, and provide a number of examples of schemas you have defined.


<br>

>## Provide a number of examples demonstrating data fetching with GraphQL. You should provide examples both running in a Sandbox/playground and examples executed in an Apollo Client


<br>

>## Provide a number of examples demonstrating creating, updating and deleting with Mutations. You should provide examples both running in a Sandbox/playground and examples executed in an Apollo Client.


<br>

>## Explain the Concept of a Resolver function, and provide a number of simple examples of resolvers you have implemented in a GraphQL Server.


<br>

>## Explain the benefits we get from using a library like Apollo-client, compared to using the plain fetch-API


<br>

>## In an Apollo-based React Component, demonstrate how to perform GraphQL Queries, including:
* **Explain the structure of the Query Component***
* **Explain the purpose of ApolloClient and the ApolloProvider component**
* **Explain the purpose of the gql-function (imported from graphql-tag)**

<br>

>## In an Apollo-based React Component, demonstrate how to perform GraphQL Mutations?


<br>

>## Demonstrate and highlight important parts of a “complete” GraphQL-app using Express and MongoDB on the server side, and Apollo-Client on the client.



