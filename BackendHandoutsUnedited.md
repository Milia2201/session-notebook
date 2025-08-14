# Backend Basics

## Learning Objectives

- [ ] Knowing that JavaScript can be executed outside of the browser
- [ ] Knowing Node.js is a runtime environment for JavaScript
- [ ] Understanding that the browser und Node.js provide environment specific APIs
- [ ] Knowing the terms server, backend and frontend
- [ ] Having a general understanding of the request - response mechanism

---

## JavaScript outside of the Browser

So far we have only used JavaScript in the browser. But JavaScript can also be used outside of the browser.

Node.js is a runtime environment for JavaScript. It allows us to run JavaScript outside of the browser. Node.js has some differences to the browser. For example, Node.js does not have a DOM. But it provides some APIs that are not available in the browser. For example, Node.js provides an API to access the file system.

One thing that Node.js can do is to create a web server. A web server is a program that listens for requests and sends responses back to the client. The web server can be used to serve web pages or to provide an API for a web application.

## Running a Node Program

To run a Node program you need to use the `node` command. The `node` command takes the path to a JavaScript file as an argument. The following `node` command will execute the JavaScript file `index.js` in the root of the project: `node index.js`.

For convenience, our templates include a script in the package.json that allows you to run the program with **`npm run start`**. The template includes a development mode, that automatically restarts the program when you make changes to the code. To start the development mode you can use **`npm run dev`**. Take a look at the `package.json` file to see how the scripts are defined.

## A Basic Node.js Program

A Node.js program can be almost anything. It can be a web server, a command line tool or a script that does some calculations. Try out to create a Node.js program that prints "Hello World" to the console or does some calculations.

```js
console.log("Hello World");
```

```js
const answer = 32 + 4;
console.log(answer);
```

Run the program with the `node` command. For example, if you save the program in a file called `index.js` you can run the program with `node index.js`.

> 💡 You can use the `console.log` function to print values to the console. In the case of Node.js the console is the terminal and not the browser console.

## Node.js Servers

You can use Node.js to create web servers. To do so you can use the `http` module provided by Node.js.

You can import a native node module by using the `node:` prefix. For example, to import the `http` module you can use the following code:

```js
import { createServer } from "node:http";
```

You don't need to install the `http` module. It is included in Node.js.

### Creating a Server

The `http` module provides a function called `createServer` that takes a callback function as an argument. The callback function is called whenever a request is made to the server. The callback function is called with two arguments: `request` and `response`. The `request` object contains information about the request that was made to the server. The `response` object is used to send a response back to the client.

```js
import { createServer } from "node:http";

export const server = createServer((request, response) => {
  response.statusCode = 200;
  response.end("Hello World");
});
```

The `response.statusCode` property is used to set the status code of the response. The `response.end` method takes a string as an argument. The string is sent back to the client.

You can access the `request` object to get information about the request that was made to the server. For example, you can access the `url` property of the `request` object to get the URL that was requested.

```js
import { createServer } from "node:http";

export const server = createServer((request, response) => {
  if (request.url === "/") {
    response.statusCode = 200;
    response.end("Hello World");
  } else {
    response.statusCode = 404;
    response.end("Not Found");
  }
});
```

> 💡 Online you will find the abbreviations `req` and `res` for `request` and `response`. This is a common convention but `req` and `res` are very hard to distinguish so we will use the full names in this bootcamp.

### Starting the Server (Listening for Requests)

To start the server you need to call the `listen` method on the server object. The `listen` method takes two arguments: the port number and an optional callback function. The callback function is called when the server is ready to accept requests.

To separate the code that creates the server from the code that starts the server you can export the server object from a `server.js` file and start the server in `index.js`:

```js
// index.js
import { server } from "./server.js";

const port = 8000;
server.listen(port, () => {
  console.log(`Server running at http://127.0.0.1:${port}/`);
});
```

> 💡 When you call `listen`, Node.js will keep the program running instead of exiting immediately. This is necessary because the program needs to keep running in order to accept requests.

## Resources

- [Node.js Website](https://nodejs.org/)
- [`http.createServer()` in the Node.js Docs](https://nodejs.org/api/http.html#httpcreateserveroptions-requestlistener)
- [`server.listen()` in the Node.js Docs](https://nodejs.org/api/http.html#serverlisten)

Handout:
https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/backend-basics/backend-basics.md?plain=1

--------------------------------------------------------------------------------------------------------------------------------------------
# Backend API Routes

## Learning Objectives

- [ ] knowing what serverless functions are
- [ ] understanding what a server-side API is meant for
- [ ] knowing how to implement Next.js API routes
  - [ ] static API routes
  - [ ] dynamic API routes
- [ ] knowing how to debug API routes with `console.log()`

---

## Serverless functions

There are different approaches to creating backend functions for web applications.

A traditional web server for example built with the Node.js framework Express is a program running on a server or virtual machine that listens for incoming HTTP requests - like a waiter at a restaurant waiting for customers to place their orders. The code for the Express server is typically written in a so called monolithic structure, where all the different functions and endpoints are managed by the same program.

On the other hand Serverless Functions are like little helpers that are only executed on-demand, i.e. when they are needed. They wait for specific things to happen, like when a web applications gets a HTTP request or when a database gets updated. When that happens, the serverless function runs its code to do the specific job it was programmed to do and is terminated afterwards.
Serverless cloud provider, like Vercel, take care of all the details like setting up the computer resources needed to run the code and shutting them down when the job is done. It's like having a team of chefs come into the kitchen, cook a dish, and then clean everything up when they are finished. This makes it easier for developers to write code without having to worry about managing servers or resources.

> 💡 This is a very basic explanation. If you're interested in learning more about
> Vercel Serverless Functions, you can read about it [here](https://vercel.com/docs/concepts/functions/serverless-functions)

---

## What a server-side API is meant for

As we already learned in the JS Fetch session an API (Application Programming Interface) can be seen from different perspectives and occur on various levels.

APIs running on a server environment are called server-side APIs. They are provided by a _server_, opposing to the APIs provided by the browser (which is also called the _client_). A common use-case for such server-side APIs is to create, read, update and delete data; so called CRUD operations.

> 💡 Take a look at handout of the JS Fetch Session to refresh your knowledge of APIs.

---

## Next.js API routes

Our main goal is to build a database and to handle its data in our web application. To do this we have to create our own API routes inside of the web application and decide what information and data the routes return. Luckily, Next.js provides us with a cool feature using simple and intuitive syntax.

It follows a simple folder structure: Any file inside the folder e.g. `pages/api/test/file.js` is mapped to the respective url with the same path e.g. `/api/test/file` and will be treated as an API endpoint instead of a page.

In Next.js, an API route is simply a JavaScript module that exports a default function. For example, a file called `pages/api/hello.js` creates the API endpoint `/api/hello` that responds with a JSON message of "Hello Web Developer!". The handler function takes two arguments: a request object and a response object, which are used to start the serverless program on vercel and handle incoming requests and send responses back to the client.

```js
export default function handler(request, response) {
  response.status(200).json({ message: "Hello Web Developer!" });
}
```

> 💡 Further information about [Next.js API Routes](https://nextjs.org/docs/api-routes/introduction).

---

### Dynamic API Routes

Next.js supports Dynamic API Routes to create API endpoints that can handle dynamic parameters in the URL path and follows the same file naming rules used for pages.

For example, if you want to create an API endpoint that can handle requests for individual jokes, you could create a file called `/pages/api/jokes/[id].js`. This creates a dynamic API route where the id parameter can be any value. If you want to get a single joke, depending on the jokes `id` used in the browser route, we can acess the `id` route parameter by destructuring it from `request.query` object.

```js
export default function handler(request, response) {
  const { id } = request.query;
  //...
}
```

> 💡 Further information about [Next.js Dynamic API Routes](https://nextjs.org/docs/api-routes/dynamic-api-routes).

---

## How to log/debug with `console.log()`

You can use the `console.log()` function to debug your web application and understand what is happening within your API Routes. Since the API handlers are executed on the server, the console output will be displayed in your terminal (localhost) where you started the development server (`npm run dev`) or in the Vercel web interface (vercel deployment).

local: shown in terminal / server console
![Example of `console.log()`in API route file](assets/log-messages-api-route-file.png)

Vercel: shown in web interface
![Example of `console.log()`in API route file](assets/log-messages-api-route-file-runtime-log.png)

![Example shown in Vercel web interfach](assets/vercel-runtime-log.png)

> 💡 Further information about [Vercel Runtime Logs](https://vercel.com/docs/concepts/observability/runtime-logs)

---

## Resources

- [Next.js API Routes](https://nextjs.org/docs/api-routes/introduction)
- [Vercel Serverless Functions](https://vercel.com/docs/concepts/functions/serverless-functions)
- [Vercel Runtime Logs](https://vercel.com/docs/concepts/observability/runtime-logs)

- Handout:
- https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/backend-api-routes/backend-api-routes.md?plain=1
--------------------------------------------------------------------------------------------------------------------------------------------
# Backend MongoDB

## Learning Objectives

- [ ] Knowing the difference between a database and a server
- [ ] Knowing the difference between relational and non-relational databases
- [ ] Understanding MongoDB basics and important terms
- [ ] Having basic knowledge of database design:
  - [ ] how to structure collections (foreign keys, references)
  - [ ] how to structure documents (nested objects)
  - [ ] one to one (1:1)
  - [ ] one to many (1:n)
  - [ ] many to many (n:m)
- [ ] Knowing what MongoDB Atlas is
  - [ ] Creating an account for MongoDB Atlas
  - [ ] Creating a cluster and database
  - [ ] Setting up database user and security settings

---

## Introduction: Databases

### What is a Database?

Let's recall what a server is:

- a program running 24/7 that is designed to **provide services to other computers or devices**,
- it can host a variety of services, such as a web server, an email server, a file server, or **a database server**,
- we have used Next.js API routes as a server to _serve_ data (from a `data.js` file in the same project).

Now consider what a database server is:

- it is a program that is specifically designed to **host and manage a database**,
- it manages the data stored in the database,
- it ensures that it is available to users and applications that need to access it.
- The data storage in a database is persistent.

### Relational vs. non-relational Databases

There are some [differences between relational and non-relational databases](https://www.mongodb.com/compare/relational-vs-non-relational-databases)
(aka SQL vs NoSQL):

**Relational**:

- data is stored in tables (like Excel, Numbers, Spreadsheets, …),
- the tables are connected to each other,
- constraint: we must decide for each column what we do if we don't have data for all entries in this column

**Non-relational**:

- data is stored in JSON-like structures,
- data is stored in key/value pairs,
- each data set in the database can have unique keys

> 💡 You can find an [in-depth explanation and comparison here](https://www.mongodb.com/compare/relational-vs-non-relational-databases).

---

## MongoDB

- As a non-relational database, MongoDB is less strict and easy to use.
- The name MongoDB comes from "hu_mongo_us" \_d_ata_b_ase.
- The name was chosen to reflect the scalability and flexibility of the database.

### MongoDB Terminology

**Database**:

- A MongoDB database is a collection of data that is organized and stored in a specific way, using the MongoDB database management system.
- A MongoDB database can have multiple sets of data called _collections_.

**Collection**:

- A collection is a grouping of MongoDB entries called _documents_.
- A collection is a equivalent of a table in a relational database system.
- A collection exists within a single database.

**Document**:

- A MongoDB document is a _JSON-like data structure that consists of key-value pairs_.
- Documents can have different _fields_.
- These key-value pairs are called _fields_.

**Field**:

- In MongoDB, a field is a _key-value_ pair that is stored in a _document_.
- The field key is a string that identifies the field, and the field value is the data stored in the field.

## Database Design

General Guidance:

- Design your collections and documents around the data you need to store and the queries you need to perform.
- Use arrays to store lists of related data within a single document.
- Try to avoid deeply nested data structures. If your documents become too complex start to split the data into multiple collections and connect the data with references (see the example below).
- If you want to reference an object that is stored in a different collection, you can use foreign keys:
  - If you have a **users** collection and a **jokes** collection, you can use a foreign key in the **jokes** collection to store a reference to the user who created each joke.
  - This allows you to store information about the user who created each joke, without duplicating data in the jokes collection.

### Database Relationships

There are three different relationships between documents:

**One-To-One**

- A one-to-one relationship in MongoDB exists when one document in one collection is related to exactly one document in another collection.
- This can be implemented by storing a reference to the related document in any of the two collections. The direction does not matter in this case. One-to-one relationships only make sense in certain special cases. For simplicity sake, think about adding the fields of one collection into the other instead.

**One-To-Many**

- A one-to-many relationship in MongoDB exists when a document in one collection is related to multiple documents in another collection.
- This can be implemented by storing a reference to the "one" collection document in the connected "many" collection documents.

**Many-To-Many**

- A many-to-many relationship in MongoDB exists when multiple documents in one collection is related to multiple documents in another collection, and vice versa.
- This is usually achieved by creating an intermediary collection which documents have a reference to both connected collections (i.e. they are split into two one-to-many relationships).

> 📙 Read more about these [relationships in the MongoDB documentation](https://www.mongodb.com/docs/manual/tutorial/model-embedded-one-to-one-relationships-between-documents/).

### Example Visualization

The following three collections visualize the best practices and relationships mentioned above.

![Database Collections Example](assets/images/database_collections.png)

```json5
// Jokes collection:
{
  "_id": ObjectId("joke1ID"),
  "userId": ObjectId("user1ID"),
  "joke": "Why do programmers hate nature? It has too many bugs.",
}

// Users collection:
{
  "_id": ObjectId("user1ID"),
  "username": "jane.doe",
  "email": "jane.doe@example.com",
}

// Comments collection:
{
  "_id": ObjectId("comment1ID"),
  "jokeId": ObjectId("joke1ID"),
  "userId": ObjectId("user1ID"),
  "comment": "That's a good one!"
}
```

Notes:

- Each document in the collections has an `_id` field that is a unique identifier.
- Each joke document has a `joke` field that stores the text of the joke and a `userId` field that stores the ID of the user who created the joke. This establishes a **one-to-many** relationship between the joke and the user collection (one joke is owned by one user, but one user can own many jokes).

- Each user document has a `username` field that stores the user's username and an `email` field that stores the user's email address.

- Each comment document has a `jokeId` field that stores the ID of the joke that the comment is associated with, a `userId` field that stores the ID of the user who created the comment, and a `comment` field that stores the text of the comment.
- The `jokeId` field and `userId` field implement **one-to-many** relationships between the comments, jokes, and users collections, as a joke can have multiple comments and a user can create multiple comments, but each comment can only be associated with one joke and one user.

---

## MongoDB Atlas Introduction

- We want our app to be accessible from the internet.
- This is why we need to make our database accessible from the internet.
- We depend on external providers to host our database.
- We will use MongoDB Atlas, a cloud provider for mongo databases.

**[Follow the instructions in the challenges document](./challenges-backend-mongodb.md)** to set up your database on MongoDB Atlas.

## Resources

- [Differences between relational and non-relational databases](https://www.mongodb.com/compare/relational-vs-non-relational-databases)
- [In-depth explanation and comparison relational/non-relational](https://www.mongodb.com/compare/relational-vs-non-relational-databases)

- Handout:
- https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/backend-mongodb/backend-mongodb.md?plain=1
- 
--------------------------------------------------------------------------------------------------------------------------------------------
# Backend Read

## Learning Objectives

- [ ] Knowing about ORM and (`mongoose` as) ODM
- [ ] Understanding how to write a `mongoose` Schema
- [ ] Knowing how to connect an application with a (local) database using `mongoose`
- [ ] Knowing how to read data with a `mongoose` model

---

## What and why mongoose

In order to access a MongoDB from your app, we'll need a JavaScript API. This API is sometimes called a database driver (imagine it like your printer drive).

We will use a library called `mongoose`. That's an ODM (Object Document Mapper).

### Difference between ORM and ODM

ORM (_Object Relation Mapping_):

- technique to perform CRUD operations to mainly relational databases (MySQL, PostgreSQL, etc.),
- uses an _object-oriented paradigm_
- like excel spreadsheet with rows and columns => you cannot add a field to one entry that doesn't exist for all
- is mapped to a single object for all entries.

ODM (_Object Document Mapping_):

- like ORM for non-relational databases (MongoDB)
- uses a _document-oriented paradigm_

### Reasons to use `mongoose` as ODM

- It helps building a **schema** and querying the database (it's also our db driver).
- It has to run on the server, because database access is not secure in the browser.
  - Remember: We already have a server (= Next.js API routes).

---

## DB Connect

In order to read data from a database and consume it in our app, we need two things:

- a database with documents (e.g. about jokes)
- a connection between this database and the Next.js app with `mongoose`.

To create the connection, follow these steps:

1. install `mongoose` with `npm install mongoose`
2. create a `.env.local` file at the root of your project with the following content:
   `MONGODB_URI=mongodb+srv://<user>:<password>@<cluster-name>/jokes-database?retryWrites=true&w=majority`
   - Files called `.env` contain environment variables: secrets like usernames and passwords **you don't want to share with anybody**.
   - These files should be ignored by git inside of the `.gitignore` file.
   - Note the structure of the content: the variable is called `MONGODB_URI` and has the value `MONGODB_URI=mongodb+srv://<user>:<password>@<cluster-name>/jokes-database?retryWrites=true&w=majority`.
     - `user` is the name of the database user you have created in the MongoDB Atlas interface.
     - `password` is the password you have chosen for this user.
     - `cluster-name` is the name of your cluster: this value can vary and will look something like `cluster0.mu12zrz.mongodb.net`.
     - `jokes-database` is the name of your database.
     - Replace the placeholders, including the `<` and `>` characters, with the actual values.
3. create a `db/connect.js` file and copy the
   [content from the Next.js mongoose example](./assets/dbConnect.js)
   - Note that this file uses the `MONGODB_URI` we have just set up in `.env.local` to create a connection.
   - No need to change anything here.

---

## Schema and Models

We need to declare a
[Schema that describes the data type of the documents in a collection](https://mongoosejs.com/docs/guide.html).

We use this Schema to create a Model that we can use to interact with the database.

Note the difference between _Schema_ and _Model_

- the _Schema_ describes the structure of a document
- the _model_ gives us a programming interface for interacting with the database (like searching the database, updating, etc.)

### Writing a Schema

We write a Schema in the corresponding file placed in the `db/models` folder like this:

- When creating a `new Schema`, we pass an object with the key-value-pairs we want our documents to have, like `joke` which is a `String` and `required`.
- We don't need to define the `id` because `mongoose` will automatically create one.
- Export the Schema to make it available in our application.

```js
// db/models/Joke.js
import mongoose from "mongoose";

const { Schema } = mongoose;

const jokeSchema = new Schema({
  joke: { type: String, required: true },
});

const Joke = mongoose.models.Joke || mongoose.model("Joke", jokeSchema);

export default Joke;
```

Further notes:

- The name of the collection the model works upon is being generated from the models name, in this case "Joke" => "jokes".
- You can call the `mongoose.model` method with a third argument that holds the collection name.
- We have to check whether the model with the name "Joke" has already been compiled and if yes, take the already compiled model. That's why we use the logical OR (`||`) operator.

---

## Using the Model: Querying the DB (.find, .findById)

In our Next.js API route, we can now write a request handler which

- connects to the database with `dbConnect()`,
- uses the Model to search a document, and
- returns the data.

```js
// api/jokes/index.js
import dbConnect from "../../../db/connect";
import Joke from "../../../db/models/Joke";

export default async function handler(request, response) {
  await dbConnect();

  if (request.method === "GET") {
    const jokes = await Joke.find();
    return response.status(200).json(jokes);
  } else {
    return response.status(405).json({ message: "Method not allowed" });
  }
}
```

`mongoose` comes with a `.findById()` method you can use in a dynamic route:

```js
// api/jokes/[id].js
import dbConnect from "../../../db/connect";
import Joke from "../../../db/models/Joke";

export default async function handler(request, response) {
  await dbConnect();
  const { id } = request.query;

  if (request.method === "GET") {
    const joke = await Joke.findById(id);

    if (!joke) {
      return response.status(404).json({ status: "Not Found" });
    }

    response.status(200).json(joke);
  }
}
```

Note that MongoDB returns an `_id` instead of `id`, so you might need to adapt your frontend to get the correct information.

> 📙 You can find a reference to [all methods of a Model in the mongoose documentation](https://mongoosejs.com/docs/api/model.html).

---

## Gathering linked collections with `.populate()`

Imagine your MongoDB has two collections: `jokes` and `comments` on these jokes. They are linked by the `commentIds`.

When reading the `jokes`, you want to get the comments as well. You can easily achieve this by linking both schemas and when you query the database, you simply add `.populate()` with method chaining.
First, link the schemas for `Joke` and `Comment`:

```js
// link the schemas
const jokeSchema = new Schema({
  joke: { type: String, required: true },
  comments: { type: [Schema.Types.ObjectId], ref: "Comment" },
});

const commentSchema = new Schema({
  _id: Schema.Types.ObjectId,
  comment: { type: String, required: true },
  author: { type: String, required: true },
});

const Joke = mongoose.models.Joke || mongoose.model("Joke", jokeSchema);
const Comment =
  mongoose.models.Comment || mongoose.model("Comment", commentSchema);
```

Second, when reading from the database, populate the comments:

```js
const joke = await Joke.findById(id).populate("comments");
```

> 📙 Read more about [populate in the mongoose docs](https://mongoosejs.com/docs/populate.html).

---

## Resources

- [ORM vs. ODM](https://medium.com/spidernitt/orm-and-odm-a-brief-introduction-369046ec57eb)

- Handout:
- https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/backend-read/backend-read.md?plain=1
- 
--------------------------------------------------------------------------------------------------------------------------------------------
# Backend Create

## Learning Objectives

- [ ] Understanding CRUD and REST APIs
- [ ] Building a Create REST API route

---

## CRUD and REST

### CRUD

The acronym CRUD [kɹʌd] covers the four basic operations of persistent storage

- **Create**, _create a record_,
- **Read** or **Retrieve**, _read a record_,
- **Update**, _update a record_, and
- **Delete** or **Destroy**, _delete a record_.

These operations can be expressed using different terms depending on context or environment.

| CRUD                      | MongoDB                    | SQL      | HTTP Method | typical Rest URL (with HTTP Method)     |
| ------------------------- | -------------------------- | -------- | ----------- | --------------------------------------- |
| **Create**                | `insertOne` / `insertMany` | `INSERT` | POST        | `/todos`                                |
| **Read** or **Retrieve**  | `findOne` / `find`         | `SELECT` | GET         | `/todos/[todoId]` (one), `/todos` (all) |
| **Update**                | `updateOne` / `updateMany` | `UPDATE` | PUT / PATCH | `/todos/[todoId] `                      |
| **Delete** or **Destroy** | `deleteOne` / `deleteMany` | `DELETE` | DELETE      | `/todos/[todoId]`                       |

> 💡 Note that the **Create** operation refers to the HTTP method `POST`. You'll need the corresponding HTTP method whenever you want to perform one of the **CRUD** operations.

### REST

REST is short for "Representational State Transfer" and refers to architectural principles and constraints how to structure your API.

We use CRUD operations and HTTP methods with a REST API.

> 💡 This is a very basic and incomplete explanation. If you're interested in learning more about
> what makes an API RESTful, you can read about it [here](https://restfulapi.net/).

---

## Create with Mongoose

To create a new entry in your database, you need to define a `POST` API route and call the `.create` method on our Joke model:

```js
// pages/api/index.js
if (request.method === "POST") {
  try {
    const jokeData = request.body;
    await Joke.create(jokeData);

    response.status(201).json({ status: "Joke created" });
  } catch (error) {
    console.log(error);
    response.status(400).json({ error: error.message });
  }
}
```

Note that the `POST` route alone does not create a new entry in your database: you need to tell your form's submit handler to use this route.

> 📙 Read more in the [mongoose docs](https://mongoosejs.com/docs/models.html#constructing-documents)

---

## Sending `POST` requests and revalidating data

Since we are mutating our jokes data array, we must perform two actions:

- sending data to our backend to add them to the database
- updating our app so that it uses the updated data from the database

If we don't **revalidate** our data, the app won't reflect the changes we did to our database. `useSWR` provides us with a method called `mutate` to trigger this revalidation for a given API endpoint, e.g. "/api/jokes". We can destructure it from the hook call just like `data` or `isLoading`:

```js
const { mutate } = useSWR("/api/jokes/");
```

In order to perform a POST HTTP request with `fetch`, we need to provide an **options object** to the `fetch` call which includes the following information:

- method: a verb like "POST", "PUT" or "DELETE" which defines the type of HTTP request method
- the "Content-Type" provided in the request headers,
- body: the data that is sent to the server

A typical "POST" request looks like this:

```js
const response = await fetch("/api/jokes", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
});
```

> 💡 The `body` key represent the `request.body` in the API route above: this is where the actual data is passed from frontend to the API (and then to the backend aka database).

After a successful "POST" fetch which triggered our new POST API endpoint, we can tell `useSWR` to revalidate the data by calling the `mutate` function. The whole submit process looks like this:

```js
import useSWR from "swr";

export default function JokeForm() {
  const { mutate } = useSWR("/api/jokes");

  async function handleSubmit(event) {
    event.preventDefault();

    const formData = new FormData(event.target);
    const jokeData = Object.fromEntries(formData);

    const response = await fetch("/api/jokes", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(jokeData),
    });

    if (response.ok) {
      mutate();
    }
  }

  return (
		//...
  );
}

```

## Resources

- [What is REST?](https://restfulapi.net/)
- [swr docs](https://swr.vercel.app/docs/mutation)

  Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/backend-create/backend-create.md?plain=1
--------------------------------------------------------------------------------------------------------------------------------------------
# Backend Update and Delete

## Learning Objectives

- [ ] Understanding the Update and Delete part of CRUD operations
- [ ] Being able to implement `UPDATE` and `DELETE` API routes

---

## Update

To update an entry in your database, you need to do two things:

- define a `PUT` API route and
- connect the submit handler of an edit form to this API route.

### Update with Mongoose

First, define a `PUT` API route:

```js
// /api/jokes/[id].js
if (request.method === "PUT") {
  const jokeData = request.body;
  // Get the joke data from the request body
  await Joke.findByIdAndUpdate(id, jokeData);
  // Find the joke by its ID and update the joke using its ID and the new data.
  return response.status(200).json({ status: `Joke ${id} updated!` });
  // Return an OK status on successful update
}
```

### `PUT` using `fetch`

Second, tell the submit handler of your edit form

- to use the `PUT` API route (i.e. send a request to your database to edit an entry),
- wait for the database to respond and update the UI if necessary or
- navigate the user to a different page via `push()`.

> 💡 Note: `PUT` and `PATCH` are semantically different. According to convention, we would use `PUT` to update our entire document, and `PATCH` to update individual fields. In our demo, we're using `PUT`, simply because we only ever have _one_ field to update.

Go to the `page` or `component` where you want to write the submit handler of your edit form. We need the `mutate` method to update the Joke component after a successful update.

```js
// /components/Joke/index.js
export default function Joke() {
  //...
  const { data, isLoading, mutate } = useSWR(`/api/jokes/${id}`);

  async function handleEdit(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
    const jokeData = Object.fromEntries(formData);

    const response = await fetch(`/api/jokes/${id}`, {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(jokeData),
    });

    if (response.ok) {
      mutate();
    }
  }
  return; //...
}
```

---

## Delete

To delete an entry in your database, you need to do two things:

- define a `DELETE` API route and
- connect a handler function which uses this API route.

### Delete with Mongoose

First, define a `DELETE` API route:

```js
if (request.method === "DELETE") {
  await Joke.findByIdAndDelete(id);
  // Find and delete the joke by its ID.
  response.status(200).json({ status: `Joke ${id} successfully deleted.` });
  // Confirm deletion with a status message.
}
```

### `DELETE` using `fetch`

We write a handler function which calls `fetch()` with the appropriate arguments and pass it to a delete button:

```jsx
// /components/Joke/index.js

  async function handleDelete() {
    const response = await fetch(`/api/jokes/${id}`, {
      method: "DELETE",
    });
    // Send a DELETE request to the server for a specific joke.
    if (response.ok) {
      // If the response is successful redirect to the home page
      router.push("/");
    }
  }

return (
  <button type="button" onClick={handleDelete}>
    Delete
  </button>
);
);
```

We don't want to use `mutate` with "DELETE" requests, since the deleted data cannot be refetched and a revalidation would result in an error.

## Resources

- [useSWRMutation (SWR Docs)](https://swr.vercel.app/docs/mutation#useswrmutation)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/backend-update-and-delete/backend-update-and-delete.md?plain=1
--------------------------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------------------------
