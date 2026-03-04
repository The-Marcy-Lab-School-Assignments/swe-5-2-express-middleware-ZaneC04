# Short Response Questions

Answer each question below in your own words. Aim for 3–5 sentences per answer. Be specific — use the exact terms and concepts from the lesson.

Your responses will each be evaluated out of 6 points. You can earn 3 points for writing quality and 3 points for the accuracy and precision of the technical content per question.

---

## Question 1: Express vs `node:http`

Express is described as a framework that "wraps" `node:http`. What does that mean? Compare how you would handle a `GET /api/users` request in `node:http` versus in Express. What does Express do for you automatically that you had to write manually with `node:http`?

**Your answer here**:

- Express is a framework that "wraps" `node.http` which refers to Express abstracting the different processes of `node:http` such as creating servers and sending responses.
- For a `GET /api/users` request in `node:http`, you would have to check the request's URL and method as shown below:

```js
if (req.method === "GET" && req.url === "/api/users") {
  res.writeHead(200, { "Content-Type": "application/json" });
  res.end(JSON.stringify(users));
  return;
}
```

- For Express, the process is simplified. Rather than manually checking the method and URL, the process is done automatically by calling `app.get()` which will run the callback function and respond using `res.send()` for the specified endpoint:

```js
app.get("/api/users", (req, res) => {
  res.send(users);
});
```

---

## Question 2: Endpoints, Controllers, and Middleware

What are **controllers** and **middleware** in Express? What are each responsible for and how do they work together to handle incoming requests?

**Your answer here**:

- A **controller** is the callback function that is called when a incoming request matches the specified URL. Controllers are responsible for creating and sending responses for their specified endpoint.
- **Middleware** refers to a function that intercepts all incoming requests and executes additional logic before a controller sends a response to the client. When a request is sent to an endpoint, any middleware will intercept the request, execute any logic before invoking `next()` and sending that request to a controller to provide a response.

---

## Question 3: Query Strings and Route Parameters

How are **query strings** and **route parameters** similar? How are they different? In your answer, provide an example of when you would use each.

**Your answer here**:

- **Query strings** and **route parameters** both are values provided in the URL after the initial URL. Where they differ though is you provide a route parameter with a `/` after the URL (`/api/users/3`) and access that value using `req.params`. For query strings, you provide the value with a `?` following the URL (`/api/users?name=ben`) and the name of the parameter with a `=` sign. You can then access that value using `req.query.name`, where `name` is the query's parameter name.
- Query strings can be utilized for sorting by a parameter (colors, topics, etc.), while route parameters can be used for getting a singular value (a person with the name "ben", the id of a person, etc.).

## Question 4: Same-Origin Requests

For API fetch calls from a client-side application, explain the difference between fetching from endpoints with relative paths like `/api/quotes` and fetching from endpoints with a full URL like `https://dog.ceo/api/breeds/image/random`. Why do we not send a fetch using a url like `http://localhost:8080/api/quotes`?

**Your answer here**:

- We do not send a fetch with a specific URL like `http://localhost:8080/api/quotes` in a client-side application as hardcoding the URL can cause issues once the application is deployed and the filepath and URL changes to be something
  such as `http://quotegallery.com/api/quotes`. Since the URL is hardcoded, the deployed app will search for the exact filepath that will no longer exist due to the URL changing. Instead, declaring a relative path such as `api/quotes` will ensure the host can find the path despite the rest of the URL being different.
