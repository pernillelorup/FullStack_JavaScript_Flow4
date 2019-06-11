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

### Issue & Solution
In both cases, they are performances issues : you either use more bandwidth than you should, or you are making more HTTP requests that you should.

GraphQL fixes this by letting you select the data you need in a simple way, it could also be achieved with REST by using DTO's.
GraphQL doesn't allow overposting, due to the built-in schema validation.

<br>

>## Explain shortly about GraphQL’s type system and some of the benefits we get from this
### GraphQL Query

1. hero is our "root" object
2. For the object returned by hero, we select the name and appearsIn fields
```
{
  hero {
    name
    appearsIn
  }
}
```
### GraphQL Query Result

This returns hero with the name and appearsIn data.
```
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ]
    }
  }
}
```
* You get the exact info you ask for, where in REST if hero has more fields those would also usally be fetched.

* Benefit is that we can reduce the amount of code and simplify our queries.

<br>

>## Explain shortly about GraphQL Schema Definition Language, and provide a number of examples of schemas you have defined.

### GraphQL comes with a set of default scalar types out of the box:

* Int: A signed 32‐bit integer.
* Float: A signed double-precision floating-point value.
* String: A UTF‐8 character sequence.
* Boolean: true or false.
* ID: The ID scalar type represents a unique identifier, often used to refetch an object or as the key for a cache. The ID type is serialized in the same way as a String; however, defining it as an ID signifies that it is not intended to be human‐readable.

### Schema example

```js
const typeDefs = `
  scalar Coordinates // custom scalar
  scalar Date // custom scalar
  
  type Query {
    getAllUsers: [User]
    getUserByUsername(userName: String!): User
    getUserByID(id: String!): User
    getAllLocationBlogs: [Blog]
    getBlogByID(id: String!): Blog
    isUserinArea(areaname: String!, username: String!): UserInArea
    getDistanceToUser(lon: Int!, lat: Int!, username: String! ): DistanceToUser
  }

  type Mutation {
    addUser(input: UserInput): User
    addLocationBlog(input: BlogInput): Blog
    likeLocationBlog(input: LikeBlogInput ): Blog
  }

  type User {
    _id: ID
    firstName: String!
    lastName: String!
    userName: String!
    password: String!
    email: String!
  }

  type Blog {
    likedBy: [User]
    info: String
    pos: BlogPosition
    author: User
    created: Date
  }
  
    input UserInput {
    firstName: String!
    lastName: String!
    userName: String!
    password: String!
    email: String!
  }

  input BlogInput {
    info: String!
    img: String
    pos: BlogPositionInput!
    author: String!
  }
```

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



