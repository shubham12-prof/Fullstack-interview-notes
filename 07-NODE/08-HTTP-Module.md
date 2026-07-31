# HTTP Module

Node's built-in module for creating HTTP servers and making HTTP requests, without any external framework — the foundation frameworks like Express are built on top of.

```js
const http = require("http");

const server = http.createServer((req, res) => {
  console.log(req.method, req.url); // e.g. GET /users

  if (req.url === "/" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello, World!");
  } else if (req.url === "/users" && req.method === "POST") {
    let body = "";
    req.on("data", (chunk) => (body += chunk)); // request body arrives as a stream
    req.on("end", () => {
      const data = JSON.parse(body);
      res.writeHead(201, { "Content-Type": "application/json" });
      res.end(JSON.stringify({ created: data }));
    });
  } else {
    res.writeHead(404, { "Content-Type": "text/plain" });
    res.end("Not Found");
  }
});

server.listen(3000, () => console.log("Server running on port 3000"));
```

**Making outbound requests:**

```js
const https = require("https");

https.get("https://api.example.com/data", (res) => {
  let data = "";
  res.on("data", (chunk) => (data += chunk));
  res.on("end", () => console.log(JSON.parse(data)));
});

// Modern alternative: Node 18+ has a built-in global fetch()
const res = await fetch("https://api.example.com/data");
const json = await res.json();
```

**Why frameworks like Express exist:** the raw `http` module requires manually parsing URLs, routing by string comparison, parsing request bodies, and setting headers by hand — Express (and similar frameworks) add routing, middleware, and body-parsing conveniences on top of this same underlying module.

**Interview note:** both the request (`req`) and response (`res`) objects are **streams** (`req` is a readable stream of the incoming body, `res` is a writable stream you send data through) — understanding Streams (see its own file) clarifies why request bodies arrive in `'data'` chunks rather than as a single value.
