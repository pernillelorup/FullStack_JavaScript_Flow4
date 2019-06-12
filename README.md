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

```js
import React from "react"
import gql from "graphql-tag";
import { Query } from "react-apollo";



const GET_DOG_PHOTO = gql`
  query Dog($breed: String!) {
    dog(breed: $breed) {
      id
      displayImage
    }
  }
`;

const DogPhoto = ({ breed }) => (
  <Query query={GET_DOG_PHOTO} variables={{ breed }}>
    {({ loading, error, data }) => {
      if (loading) return null;
      if (error) return `Error! ${error}`;

      return (
        <img alt="dog" src={data.dog.displayImage} style={{ height: 100, width: 100 }} />
      );
    }}
  </Query>
);

export default DogPhoto;
```

<br>

>## Provide a number of examples demonstrating creating, updating and deleting with Mutations. You should provide examples both running in a Sandbox/playground and examples executed in an Apollo Client.


<br>

>## Explain the Concept of a Resolver function, and provide a number of simple examples of resolvers you have implemented in a GraphQL Server.

### Resolver Explained
The resolver function accesses a database and then constructs and returns an object.
For example below you can see that the resolver fetches all Users and returns them, the schema then is set to take a liste of Users.

```js
const resolvers = {
	Query: {
		getAllUsers: async () => {
			return await userFacade.getAllUsers();
		},
		getUserByUsername: async (_, { userName }) => await userFacade.findByUsername(userName),
		getUserByID: async (_, { id }) => await userFacade.findById(id),
		getAllLocationBlogs: async () => await blogFacade.getAllLocationBlogs(),
		getBlogByID: async (_, { id }) => await blogFacade.likeLocationBlog(id),
		isUserinArea: async (_, { areaname, username }) => {
			var obj = await queryFacade.isUserinArea(areaname, username).catch((err) => {
				return { msg: err.message };
			});
			if (obj !== undefined) {
				return { status: obj.status, msg: obj.msg };
			}
		},
		getDistanceToUser: async (_, { lon, lat, username }) => {
			var obj = await queryFacade.getDistanceToUser(lon, lat, username).catch((err) => {
				return { msg: err.message };
			});
			if (obj !== undefined) {
				return { distance: obj.distance, to: obj.username  };
			}
		},
	},
	Mutation: {
		addUser: async (_, { input }) => {
			return await userFacade.addUser(input.firstName, input.lastName, input.userName, input.password, input.email);
		},
		addLocationBlog: async (_, { input }) => {
			return await blogFacade.addLocationBlog(input.info, input.img, input.pos, input.author);
		},
		likeLocationBlog: async (_, { input }) => {
			return await blogFacade.likeLocationBlog(input.blogID, input.userID);
		},
	}
};
```

<br>

>## Explain the benefits we get from using a library like Apollo-client, compared to using the plain fetch-API

* The Apollo client provides React-Apollo, which makes the frontend familiar to us react devs.
* Apollo makes the use of GraphQL easy, for example it allows for dynamic querying because we can use dynamic variables.

**Check Dog Photo example above**


<br>

>## In an Apollo-based React Component, demonstrate how to perform GraphQL Queries, including:
* **Explain the structure of the Query Component***
```js
  type Query {
    getAllUsers: [User]
    getUserByUsername(userName: String!): User
    getUserByID(id: String!): User
    getAllLocationBlogs: [Blog]
    getBlogByID(id: String!): Blog
    isUserinArea(areaname: String!, username: String!): UserInArea
    getDistanceToUser(lon: Int!, lat: Int!, username: String! ): DistanceToUser
  }
```
* **Explain the purpose of ApolloClient and the ApolloProvider component**

Apollo Client is a community-driven effort to build an easy-to-understand, flexible and powerful GraphQL client. Apollo has the ambition to build one library for every major development platform that people use to build web and mobile applications and so far the ones below exist:
* JavaScript
  * React
  * Angular
  * Vue
  * Meteor
  * Ember
* Web Components
  * Polymer
  * lit-apollo
* Native mobile
  * Native iOS with Swift
  * Native Android with Java
```js
<ApolloProvider client={client}>
  <div>
    <h2>Building Query components (DOG) 🚀</h2>
    <Dogs/>
  </div>
</ApolloProvider>
      
const client = new ApolloClient({
  //uri: `https://32ypr38l61.sse.codesandbox.io/`
  uri: `http://localhost:4000/`
});
```

* **Explain the purpose of the gql-function (imported from graphql-tag)**

<br>

>## In an Apollo-based React Component, demonstrate how to perform GraphQL Mutations?

```js


const getAuthorsQuery = gql`
  {
    getAllAuthors {
      name
      id
    }
  }
`;

const addBookMutation = gql`
  mutation($name: String!, $genre: String!, $authorId: ID!) {
    createBook(input: { name: $name, genre: $genre, authorId: $authorId }) {
      name
      id
    }
  }
`;
```


```js
import React, { Component } from "react";
import { graphql, compose } from "react-apollo";
import {
  getAuthorsQuery,
  addBookMutation,
  getBooksQuery
} from "../queries/queries";

class AddBook extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name: "",
      genre: "",
      authorId: ""
    };
  }
  displayAuthors() {
    var data = this.props.getAuthorsQuery;
    if (data.loading) {
      return <option disabled>Loading authors</option>;
    } else {
      return data.getAllAuthors.map(author => {
        return (
          <option key={author.id} value={author.id}>
            {author.name}
          </option>
        );
      });
    }
  }
  submitForm(e) {
    e.preventDefault();
    // use the addBookMutation
    this.props.addBookMutation({
      variables: {
        name: this.state.name,
        genre: this.state.genre,
        authorId: this.state.authorId
      },
      refetchQueries: [{ query: getBooksQuery }]
    });
  }
  render() {
    return (
      <form id="add-book" onSubmit={this.submitForm.bind(this)}>
        <div className="field">
          <label>Book name:</label>
          <input
            type="text"
            onChange={e => this.setState({ name: e.target.value })}
          />
        </div>
        <div className="field">
          <label>Genre:</label>
          <input
            type="text"
            onChange={e => this.setState({ genre: e.target.value })}
          />
        </div>
        <div className="field">
          <label>Author:</label>
          <select onChange={e => this.setState({ authorId: e.target.value })}>
            <option>Select author</option>
            {this.displayAuthors()}
          </select>
        </div>
        <button>+</button>
      </form>
    );
  }
}

export default compose(
  graphql(getAuthorsQuery, { name: "getAuthorsQuery" }),
  graphql(addBookMutation, { name: "addBookMutation" })
)(AddBook);
```

<br>

>## Demonstrate and highlight important parts of a “complete” GraphQL-app using Express and MongoDB on the server side, and Apollo-Client on the client.



