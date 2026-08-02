## HyperText Transfer Protocol

`Hypertext transfer protocol` is a protocol used to exchange the information over the internet in the form of text. Now the data might be of the different type but typically the text is transffered for example, image is transfered as BLOB (binary large object).

Before we understand any topics, there has to have a need of it? Why its needed? If you dont have this question, ask your mom why she gave you birth and you will know it.
## What’s the need of it?

Lets say `bob` and `alice` are two computer over the network. What problems they could have when they want to communicate over the network.
- By considering they follow a client/server architecture.

1. Bob wants to say hello to alice, where will bob send msg? Bob has to know the address of the alice to send right?
2. Lets say, bob randomly met alice on road while travelling, and alice gave him his address (dont ask me why bob didnt give him at that moment just understand the flow).
	1. Now bob sends the msg to her address but alice doesnt know its from bob, how will she be able to identify that its from bob?
	2. If bob has written that its from bob’s machine then she will know right?
3. Lets say, bob sent the drawing in the binary bits (dont ask me how will he send, just understand it, he drew and clicked photo and sent) how will she know that its and image and not to open it as a text (just understand in context of browser ;’), so if bob has mentioned that its an image it could work.
4. Lets assume alice is server in this one, But can bob try to get the alice’s photo from her computer? Nope bob cant because its alice’s computer, however if alice would have setup in the computer that bob can have the access to her image than yes, he could. (in context of CORs)

are you happy now? it seems a lot optimized compare to before tho, ahahah

There are a lot of scenarios i can make to understand that, there needs to be have some set of rules by which we need to send the data over network, thats when HTTP comes into the picture to fulfill this need.
- Protocols basically means a set of rules.
- & Http provides set of rules to follow while transfering data over network.

- - -
## Http:

As i mentioned its a protocol for transfering the data over the network. Http didn’t just poped out and became a standard for data transfer over network

### Evolution of it:

- HTTP/0.9: Supported get request, no headers, plaintext only.
- HTTP/1.0: added headers, status code, different content types, & allowed sending images and videos.
- HTTP/1.1: introduced **persistent connections**, **chunked transfer**, and **caching** support. Still widely used.
- HTTP/2: allows header compression, much faster and single connection multiple requests parallelly.

Now i know this became a bit boring when i introduced the Evolution but its important -

If i had to tell you in my language,
- The initial version (0.9) was like trial but kinda breakthough like with that we learnt that how can we retrive the information from other computers like get requests like not rich content but yeah we can get information in plaintext only.
- Then came major breakthrough in HTTP/1.0 very imp, it had headers, status codes, content type. Basically you send other computer data and along with that you tell that computer what to expect and other related information like what type of data it is etc..
- But the problem was everytime we send data in 1.0 we need to open and close the connection, this was solved in 1.1 by allowing communication over the same one time connection.
- But it also had the problem that it we need to send each request sequentially, which was time taking and unefficient, then came HTTP-2.0 which had like support to send multiple requests together parallaly.

### Important Properties:

HTTP is stateless, meaning it doesnt store user information with it. Now it has its own pros & cons.
- Like we cant do state management and then we use various methods like cookies, session etc.. To store it on client/server and handle it.

Uses port number 80 for http- static stuff, 443 - for https
Https is a secured version of http, it is like more secure, it has SSL certificates, encryption etc.. You just need to know this otherwise it will become cipher/cloud rabbit hole.

- - -

## Now what is this headers, status codes, we talked about?

Whenever a request is sent from one computer to another computer it has some sets of information about,
- The source computer
- The content in the request
- The destination computer
So these information are packed into request as an object and sent over network to the destination computer.

At the same time, whenever other computer receives it and sends the response, it also contains some information about the response’s content, its type, who send it etc..

- - -

These are called request and response structures.
Lets see them one by one.

## REQUEST STRUCTURE:

An HTTP request from the **client → server** has three main parts:
`1️⃣ Request Line -> 2️⃣ Headers -> 3️⃣ (Optional) Body`

### Example — Requesting a webpage:

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
Connection: keep-alive
```
#### Breakdown:

| Part                         | Description                                                               |
| ---------------------------- | ------------------------------------------------------------------------- |
| **GET /index.html HTTP/1.1** | Request line → method (`GET`), resource (`/index.html`), protocol version |
| **Host: www.example.com**    | The server’s domain name                                                  |
| **User-Agent:**              | Info about browser or client                                              |
| **Accept:**                  | What type of content the client can handle                                |
| **Connection: keep-alive**   | Keep the connection open (persistent)                                     |


## RESPONSE:

An HTTP response from **server → client** also has three parts:
`1️⃣ Status Line   2️⃣ Headers   3️⃣ (Optional) Body (actual data)`

### Example — Server responding with a web page:

```
HTTP/1.1 200 OK
Date: Sat, 04 Oct 2025 12:00:00 GMT
Server: Apache/2.4.41
Content-Type: text/html
Content-Length: 1256
Connection: keep-alive

<html>
  <head><title>Welcome</title></head>
  <body>
    <h1>Hello, Harsh!</h1>
  </body>
</html>

```

| Part                | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| **HTTP/1.1 200 OK** | Status line → version, status code (`200`), message (`OK`)   |
| **Headers**         | Metadata about response (server, content type, length, etc.) |
| **Body**            | Actual content sent to browser (HTML here)                   |

These are nothing but a bunch of headers:
- - -
## 💡 What Are HTTP Headers?

HTTP **headers** are key-value pairs sent along with every **request** and **response**.
They carry **extra information** — like what data type is being sent, who’s sending it, how to cache it, etc.

Think of headers as the **metadata** of the message.
- - -
## 📤 Request Headers (Client → Server)

These are sent by the **browser/client** to give the server context.

| Header              | Meaning                                             | Example                               |
| ------------------- | --------------------------------------------------- | ------------------------------------- |
| **Host**            | The domain name of the server                       | `Host: www.google.com`                |
| **User-Agent**      | Info about the browser or client making the request | `User-Agent: Mozilla/5.0`             |
| **Accept**          | What type of content the client can handle          | `Accept: text/html, application/json` |
| **Accept-Language** | Preferred language                                  | `Accept-Language: en-US`              |
| **Accept-Encoding** | What compression formats are supported              | `Accept-Encoding: gzip, deflate`      |
| **Connection**      | Whether to keep the connection alive                | `Connection: keep-alive`              |
| **Authorization**   | Authentication credentials (e.g., token, password)  | `Authorization: Bearer <token>`       |
| **Content-Type**    | Type of data sent in the body (used in POST/PUT)    | `Content-Type: application/json`      |
| **Content-Length**  | Length of the body in bytes                         | `Content-Length: 254`                 |
| **Cookie**          | Sends cookies to the server                         | `Cookie: sessionid=abc123`            |
- - -
## Response Headers (Server → Client)

Sent by the **server** to give the client information about the response.

| Header                          | Meaning                             | Example                                  |
| ------------------------------- | ----------------------------------- | ---------------------------------------- |
| **Content-Type**                | Type of data being sent             | `Content-Type: text/html; charset=UTF-8` |
| **Content-Length**              | Size of the response body in bytes  | `Content-Length: 5123`                   |
| **Server**                      | Info about the server software      | `Server: Apache/2.4.41`                  |
| **Date**                        | When the response was generated     | `Date: Sat, 04 Oct 2025 12:00:00 GMT`    |
| **Cache-Control**               | How caching should be handled       | `Cache-Control: no-cache`                |
| **Set-Cookie**                  | Sends a cookie to the client        | `Set-Cookie: sessionid=xyz789; HttpOnly` |
| **Location**                    | Used for redirects                  | `Location: https://newsite.com`          |
| **Access-Control-Allow-Origin** | CORS header, defines who can access | `Access-Control-Allow-Origin: *`         |
| **Connection**                  | Close or keep connection open       | `Connection: keep-alive`                 |

- - -

## 🌐 What Are HTTP Methods?

**HTTP methods** tell the server **what action** the client wants to perform on a resource (like a webpage, image, or API endpoint).

They are written in the **request line** — e.g.:

`GET /index.html HTTP/1.1`

---
## Common HTTP Methods

| Method      | Purpose                                           | Has Body?   | Safe? | Idempotent? | Example                             |
| ----------- | ------------------------------------------------- | ----------- | ----- | ----------- | ----------------------------------- |
| **GET**     | Retrieve data from the server                     | ❌           | ✅     | ✅           | Get a list of users                 |
| **POST**    | Send new data to the server (create something)    | ✅           | ❌     | ❌           | Submit a form or add a new record   |
| **PUT**     | Update or replace an existing resource completely | ✅           | ❌     | ✅           | Update user info                    |
| **PATCH**   | Partially update an existing resource             | ✅           | ❌     | ✅           | Update just one field (e.g., email) |
| **DELETE**  | Remove a resource from the server                 | ❌ (usually) | ❌     | ✅           | Delete a post or user               |
| **HEAD**    | Same as GET but returns only headers (no body)    | ❌           | ✅     | ✅           | Check if a file exists              |
| **OPTIONS** | Ask the server what methods are allowed           | ❌           | ✅     | ✅           | Used in CORS preflight requests     |

- - -
## STATUS  CODES:

These are nothing but a universally agreed set of codes that indicates the result of our request.

Generally how they are used?
`1.x.x` - used for infromative task
`2.x.x` - used for the successful req
`3.x.x` - used when its redirected req
`4.x.x` - used for client error
`5.x.x` - used for server errors

- - -
Most commonly used ones:

200 - successful get req
201 - succesful post req, like insertion of data.
204 - no content but sucess, generally used to get info from the server or confirmation.

301 - res moved to new url and you might consider switching althou for backword compatability we havent changed.
302 - temporary redirect
304 - cached response, no changes done.

400 - bad req, sent empty field, wrong data etc..
401 - not authorized
403 - forbidden trying to access something but denied, for ex- taking uuid of other guy and trying to insert.
404 - resource not found.
405 - method not allowed
429 - too many requests (rate limiting on ip/device)

500 - internal server error
501 - server hasnt implemented this functionality
502 - bad gateway
503 - service in maintainance or not available rn.

- - -
## ⚡ HTTP Caching — Why and How

Okay, let’s talk about **caching**. Imagine this:

Bob is super impatient and wants to load Alice’s profile picture **every time he visits her page**. But… downloading the same big image every time is **wasteful** and slow.

**Solution? Cache it.**

> Caching = “Hey browser, save a copy of this stuff locally, so next time I don’t have to download it again if it hasn’t changed.”

---

### 🧠 How Caching Works Under the Hood

1. **Server says:**
    “Hey browser, you can keep this copy for 1 day” → using `Cache-Control: max-age=86400`
2. Browser **saves the response** (HTML, CSS, JS, image, whatever).
3. Next time Bob visits the same page:
    - Browser checks if the cached copy is still valid.
    - Server can also give **validation info** like:
        - **ETag** → a unique fingerprint/hash of the resource. Example: `ETag: "abc123"`
        - **Last-Modified** → tells when this file was last changed. Example: `Last-Modified: Sat, 04 Oct 2025 12:00:00 GMT`
    - Browser sends a **conditional request** to server:
        `GET /profile-pic.jpg HTTP/1.1 If-None-Match: "abc123"`
        - Here, If-None-Match header is computed whenever you send a request, and that tag is matched with the ETag that was generated, browser caches some requests whichever has the cache-control set for that duration, and checks if the ETag and If-None-Match are matched? And also the time? If they are send the same response with the 304 status code- meaning cached response and no change.

4. Server checks:
    - If the resource hasn’t changed → sends **304 Not Modified** → **no need to download again** ✅
    - If changed → sends **200 OK** with new content → browser updates cache.

---

### 🔹 Important Headers for Caching

| Header            | Meaning                                                                |     |
| ----------------- | ---------------------------------------------------------------------- | --- |
| **Cache-Control** | How long browser can keep a resource (`max-age`, `no-cache`)           |     |
| **ETag**          | Unique fingerprint of the resource → used to check if resource changed |     |
| **Last-Modified** | When resource was last changed → used for validation                   |     |
| **Expires**       | Old-school way to tell browser until when resource is valid            |     |

### 💡 Benefits of Caching

- **Speed:** Browser can load page faster without downloading everything again.
- **Bandwidth saving:** Less data transferred → saves internet usage.
- **Server load reduction:** Fewer requests hitting the server → server chill mode 😎.
- **Better user experience:** Pages feel snappy and responsive.

- - -
## ⚡ HTTP Compression — Why and How

Imagine this:

Bob wants to send **a huge image or HTML file to Alice** over the internet.

- Without compression → takes **long time**, uses more bandwidth.
- With compression → **shrinks the size**, faster transfer, less data → Alice gets it quicker.

This is exactly what **HTTP compression** does.

---
### 🔹 How It Works

1. **Browser says:**
    - “Hey server, I can handle compressed responses”
    - Using header:
        `Accept-Encoding: gzip, deflate, br`
    - This tells server: “I support gzip, deflate, brotli compression.”

2. **Server compresses response:**
    - If the server supports compression, it compresses the data **before sending**.
    - Adds a header to tell browser how it compressed it:
        `Content-Encoding: gzip`

3. **Browser receives compressed data:**
    - Browser **decompresses it automatically**.
    - User sees the page normally — doesn’t know it was compressed.

---

### 🔹 Example

**Request (browser → server):**
`GET /index.html HTTP/1.1 Host: www.example.com Accept-Encoding: gzip, deflate`

**Response (server → browser):**
`HTTP/1.1 200 OK Content-Encoding: gzip Content-Type: text/html Content-Length: 1256  <compressed HTML data here>`

✅ Browser decompresses automatically → renders HTML.

---

### 🔹 Why It’s Important

1. **Faster load times:** Smaller data = faster download → better user experience.
2. **Bandwidth savings:** Less data transfer → saves internet cost and server load.
3. **Works with caching:** Compressed responses can still be cached by browser.
4. **No change to page:** Browser decompresses automatically → no extra work for client.

- - -
## Multipart Form Data

**What it is:**

- Used when the client needs to **send multiple pieces of data in one request**, like a form with **text + files** (images, PDFs, etc.).
- Each part has its **own headers** and **content**, separated by a **boundary string**.
---

### How it works under the hood

1. Browser/client prepares **a unique boundary** for this request:
    `----WebKitFormBoundary7MA4YWxkTrZu0gW`
2. Each field in the form is **packed with headers and content**:
    `--boundary Content-Disposition: form-data; name="username"  Harsh --boundary Content-Disposition: form-data; name="profilePic"; filename="me.png" Content-Type: image/png  (binary image data here) --boundary--`
3. Server parses the **boundary**, reads each part, and handles it appropriately (text, file, etc.).

✅ That’s how browsers can **send files + text together** in a single POST request.

- - -
## 🌐 2️⃣ Event Streaming (Server-Sent Events)

**What it is:**

- Lets **server send continuous updates to the client** over a single HTTP connection.
- Example: real-time notifications, live scores, or yes… ChatGPT streaming responses.

---

### How it works under the hood

1. Client initiates a **GET request** with `Accept: text/event-stream`:
`GET /events HTTP/1.1 Host: example.com Accept: text/event-stream`

2. Server responds with:
`HTTP/1.1 200 OK Content-Type: text/event-stream Cache-Control: no-cache Connection: keep-alive  data: Hello Harsh! data: Here comes your next update`

- **`data:` lines** = the actual events sent by the server.
- **Connection stays open** → server can push new events anytime.

2. Client (browser or JS) **listens to events**:

`const evtSource = new EventSource("/events"); evtSource.onmessage = function(event) {     console.log("New event:", event.data); };`

✅ Result: Real-time updates without the client repeatedly asking the server.


this is so optimized hahah.

this is so awesome, hahahah. i love this.
- kinda like it
- its good as welll/
- never mind
