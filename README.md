<!---
{
  "id": "e8add8e9-7a67-4b50-af89-6c1ce6558e0d",
  "teaches": "Using `curl` to Interact with Web APIs",
  "depends_on": ["e46ffb8b-00d6-44a2-ad40-552ea03b4e3a"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-04-07",
  "keywords": ["curl", "web", "HTTP", "GET", "POST", "REST"]
}
--->

# Using `curl` to Interact with Web APIs

## Introduction

`curl` is a command-line tool designed for transferring data to or from a server using a variety of protocols, with HTTP(S) being among the most frequently used. The name `curl` stands for "Client URL". It enables users to construct arbitrary HTTP requests directly from the command line, making it an essential utility for developers, testers, and system administrators.

In scientific and technological terms, `curl` acts as a user-agent similar to a web browser, but without a graphical interface. When a user issues a command such as `curl https://example.com`, the tool opens a TCP connection to the destination server, constructs an HTTP request (typically a `GET` by default), and sends it across the network. The server's response—typically in HTML, JSON, XML, or plain text—is received and rendered as standard output in the terminal.

`curl` supports nearly every HTTP verb (`GET`, `POST`, `PUT`, `DELETE`, etc.) and can include headers, cookies, and authentication tokens. It also supports TLS for secure communication, making it suitable for accessing both public and secured APIs. `curl` is widely used in RESTful web development to test API endpoints manually before integrating them into a frontend or another backend service.

In this exercise, you will use `curl` to send both `GET` and `POST` requests to two public APIs. You will learn to modify headers, include JSON payloads, and inspect the response structure. This activity will strengthen your understanding of HTTP communication, status codes, and API conventions.

## Tasks

0. **Check if curl is installed**

   Open a terminal and confirm that `curl` is available by typing:

   ```bash
   curl --version
   ```

   If it is not installed, you will need to install it using your system's package manager. On Debian-based systems (such as Ubuntu), you can install it using:

   ```bash
   sudo apt update && sudo apt install curl
   ```

1. **Call a public GET endpoint with curl**

   We begin by using a public API to retrieve a simple resource. The Dog CEO API returns random pictures of dogs. Issue the following command:

   ```bash
   curl https://dog.ceo/api/breeds/image/random
   ```

   This command sends an HTTP `GET` request to the server. The server responds with a JSON object containing an image URL. Note the structure of the response. Can you identify which part is the message and which indicates success or failure?

2. **Inspect the full HTTP exchange with `-v`**

   Repeat the previous command, but now add the `-v` flag to enable verbose mode:

   ```bash
   curl -v https://dog.ceo/api/breeds/image/random
   ```

   This will show the exact request headers sent to the server and the response headers received. Observe which protocol version is used (e.g., HTTP/1.1 or HTTP/2), the content-type of the response, and the status code.

3. **Simulate an error by calling a nonexistent resource**

   Modify the request path slightly to call a non-existing endpoint:

   ```bash
   curl https://dog.ceo/api/breeds/image/doesnotexist
   ```

   This results in an HTTP 404 or another error code. Read the error message returned by the API and reflect on how a real-world application could handle such an error.

4. **Send a POST request to a placeholder API**

   Use the JSONPlaceholder API, a mock service for testing and prototyping REST APIs. Issue the following `POST` request:

   ```bash
   curl -X POST https://jsonplaceholder.typicode.com/posts \
        -H "Content-Type: application/json" \
        -d '{"title": "foo", "body": "bar", "userId": 1}'
   ```

   This command constructs a complete HTTP `POST` request with a JSON payload in the body. The server responds with the submitted data and an automatically generated ID. Carefully inspect the response and compare it to the data you sent.

5. **Try modifying the headers or method manually**

   As an extension, try changing the method to `PUT` or removing the `Content-Type` header. What happens if the API does not receive the expected format? How does the server respond?

## Questions

1. What is the difference between the `-X` and `-d` flags in curl?
2. What happens when you send a request with the wrong `Content-Type` header?
3. What does HTTP 404 mean? When do you encounter it with public APIs?
4. Why does the JSONPlaceholder API return an `id` even though it doesn't store data persistently?
5. How does `curl` differ from a graphical web browser when accessing resources?
6. What is the purpose of specifying `-H "Content-Type: application/json"` in a POST request?
7. Why might verbose mode (`-v`) be useful when debugging HTTP requests?
8. What HTTP status codes would indicate client errors? Server errors?

## Advice

`curl` is an excellent first tool when exploring or debugging APIs. During development, it allows you to quickly confirm whether an endpoint is working, what the response structure looks like, and how the headers are formatted. You can combine it with tools like `jq` to make the JSON output more readable, which helps when examining larger payloads. The ability to manually specify headers with `-H`, view full HTTP exchanges with `-v`, and test endpoints with different HTTP methods makes it an invaluable part of any developer's toolkit. Start simple and progress toward using `curl` in shell scripts or automated tests as your understanding grows.

