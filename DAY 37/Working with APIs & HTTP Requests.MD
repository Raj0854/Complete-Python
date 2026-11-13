
# Day 37 – Working with APIs & HTTP Requests

## 1. Introduction to APIs

### What is an API?

API stands for **Application Programming Interface**.

An API allows two different software applications to communicate and exchange data with each other.

For example:
- A weather application gets weather information from a weather API.
- A payment application communicates with a payment gateway API.
- A mobile application gets user information from a server through an API.
- A website can retrieve product information from an e-commerce API.

### Real-World Example

Imagine a restaurant:

1. You are the customer.
2. You give your order to the waiter.
3. The waiter sends your order to the kitchen.
4. The kitchen prepares the food.
5. The waiter brings the food to you.

An API works similarly:

1. Client application sends a request.
2. API receives the request.
3. Server processes the request.
4. Server sends a response.
5. Client application uses the returned data.

### Important API Terminology

| Term | Meaning |
|---|---|
| Client | Application sending a request |
| Server | Application processing the request |
| API | Interface used for communication |
| Endpoint | Specific URL where an API resource is available |
| Request | Message sent by the client |
| Response | Data returned by the server |
| HTTP | Protocol used for communication |
| JSON | Common format for exchanging data |

### Example

```text
Client Application
       |
       | HTTP Request
       v
     API Server
       |
       | Processes Request
       v
     Database
       |
       | Returns Data
       v
     API Response
       |
       v
Client Application
```

---

## 2. What is a REST API?

REST stands for **Representational State Transfer**.

A REST API is a commonly used approach for building APIs that communicate over HTTP.

REST APIs generally use HTTP methods to perform operations on resources.

Example API endpoint:

```text
https://jsonplaceholder.typicode.com/posts
```

This endpoint provides access to post-related data.

### Common HTTP Methods

| Method | Purpose | Example |
|---|---|---|
| GET | Retrieve data | Get all users |
| POST | Create data | Create a new user |
| PUT | Replace existing data | Replace user details |
| PATCH | Partially update data | Update user's name |
| DELETE | Delete data | Delete a user |

### Important Difference

- GET retrieves information.
- POST creates a new resource.
- PUT generally replaces an existing resource.
- PATCH updates selected fields.
- DELETE requests removal of a resource.

---

## 3. Understanding HTTP Requests and Responses

HTTP stands for **Hypertext Transfer Protocol**.

It defines how clients and servers communicate.

An HTTP request can contain:

1. URL
2. HTTP method
3. Headers
4. Query parameters
5. Request body

An HTTP response can contain:

1. Status code
2. Response headers
3. Response body

### Example Request

```http
GET /posts/1 HTTP/1.1
Host: jsonplaceholder.typicode.com
Accept: application/json
```

### Example Response

```json
{
    "userId": 1,
    "id": 1,
    "title": "Example Post",
    "body": "This is an example post."
}
```

### What are HTTP Status Codes?

Status codes tell us whether an HTTP request was successful or encountered a problem.

| Status Code | Meaning |
|---|---|
| 200 | OK – Request successful |
| 201 | Created – Resource created |
| 204 | No Content – Successful response without a body |
| 301 | Moved Permanently |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 429 | Too Many Requests |
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |

### Status Code Categories

- 1xx – Informational
- 2xx – Successful
- 3xx – Redirection
- 4xx – Client errors
- 5xx – Server errors

---

## 4. Setting Up the Requests Library

Python provides several ways to communicate with APIs.

One of the most popular third-party libraries is `requests`.

### Install Requests

Open the terminal:

```bash
python -m pip install requests
```

### Verify Installation

```bash
python -c "import requests; print(requests.__version__)"
```

Example output:

```text
2.x.x
```

The exact version may be different.

### Import the Library

```python
import requests

print("Requests library imported successfully!")
```

Expected output:

```text
Requests library imported successfully!
```

**Important:** The `requests` library is a third-party package. It must be installed before using it.

---

## 5. Making Your First GET Request

The GET method is used to retrieve information from an API.

We will use JSONPlaceholder, a free testing API.

Website:

```text
https://jsonplaceholder.typicode.com
```

### Example 1: Get All Posts

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

response = requests.get(url, timeout=10)

print("Status Code:", response.status_code)
print("Response:", response.text[:300])
```

Expected output:

```text
Status Code: 200
Response: [
  {
    "userId": 1,
    "id": 1,
    "title": ...
```

The exact response formatting may vary.

### Understanding the Code

- `requests.get()` sends an HTTP GET request.
- `url` stores the API endpoint.
- `timeout=10` limits how long the request waits for a response.
- `response.status_code` returns the HTTP status code.
- `response.text` returns the response body as a string.

### Example 2: Get a Single Post

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

response = requests.get(url, timeout=10)

print("Status:", response.status_code)
print(response.text)
```

Expected output:

```text
Status: 200
{
  "userId": 1,
  "id": 1,
  "title": "...",
  "body": "..."
}
```

---

## 6. Understanding the Response Object

When we send an HTTP request using `requests`, we receive a Response object.

It contains useful information about the server's response.

### Important Response Attributes

| Attribute | Purpose |
|---|---|
| `response.status_code` | Returns HTTP status code |
| `response.text` | Returns response body as text |
| `response.content` | Returns response body as bytes |
| `response.json()` | Converts JSON response into Python data |
| `response.headers` | Returns response headers |
| `response.url` | Returns final request URL |
| `response.ok` | Indicates whether status is below 400 |
| `response.reason` | Returns status description |

### Practical Example

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

response = requests.get(url, timeout=10)

print("Status Code:", response.status_code)
print("Reason:", response.reason)
print("URL:", response.url)
print("Success:", response.ok)
print("Content Type:", response.headers.get("Content-Type"))
print("Response Length:", len(response.text))
```

Expected output will include:

```text
Status Code: 200
Reason: OK
Success: True
Content Type: application/json; charset=utf-8
```

The exact response length and URL depend on the response.

---

## 7. Working with JSON API Responses

Most REST APIs return data in JSON format.

JSON stands for **JavaScript Object Notation**.

Python provides the `json` module, but the Requests library also provides a convenient `.json()` method.

### Example 1: Convert API Response into Python Data

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

response = requests.get(url, timeout=10)

data = response.json()

print(data)
print(type(data))
```

Expected output:

```text
{'userId': 1, 'id': 1, 'title': '...', 'body': '...'}
<class 'dict'>
```

The exact title and body are provided by the API.

### Example 2: Access Individual Values

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

response = requests.get(url, timeout=10)

data = response.json()

print("User ID:", data["userId"])
print("Post ID:", data["id"])
print("Title:", data["title"])
print("Body:", data["body"])
```

### Example 3: Get All Posts and Display Titles

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

response = requests.get(url, timeout=10)

posts = response.json()

for post in posts:
    print("Post ID:", post["id"])
    print("Title:", post["title"])
    print("-" * 40)
```

### Example 4: Filter Posts by User ID

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

response = requests.get(url, timeout=10)

posts = response.json()

user_id = 1

for post in posts:

    if post["userId"] == user_id:

        print("Post ID:", post["id"])
        print("Title:", post["title"])
```

---

## 8. Query Parameters in API Requests

Query parameters are additional values passed through a URL to filter or customize API results.

They generally appear after a question mark (`?`).

Example:

```text
https://example.com/users?city=Delhi&age=25
```

Here:

- `city=Delhi` is a query parameter.
- `age=25` is another query parameter.
- `&` separates multiple parameters.

### Using Query Parameters with Requests

The Requests library provides the `params` argument.

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

params = {
    "userId": 1
}

response = requests.get(
    url,
    params=params,
    timeout=10
)

print("Requested URL:", response.url)

posts = response.json()

for post in posts:
    print(post["id"], post["title"])
```

Expected result:

The API returns posts associated with user ID 1.

### Multiple Query Parameters

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

params = {
    "userId": 1,
    "id": 1
}

response = requests.get(
    url,
    params=params,
    timeout=10
)

print(response.url)
print(response.json())
```

**Important:** Use `params` instead of manually constructing query strings. Requests handles URL encoding for you.

---

## 9. Understanding API Headers

HTTP headers provide additional information about a request or response.

Examples:

- Content-Type
- Accept
- Authorization
- User-Agent

### Example: Sending Headers

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

headers = {
    "Accept": "application/json",
    "User-Agent": "Python-API-Learning"
}

response = requests.get(
    url,
    headers=headers,
    timeout=10
)

print("Status:", response.status_code)
print(response.json())
```

### Important Headers

| Header | Purpose |
|---|---|
| Accept | Specifies acceptable response format |
| Content-Type | Specifies request or response body format |
| Authorization | Carries authentication credentials |
| User-Agent | Identifies the client application |

Some APIs require headers for authentication.

Never expose API keys, passwords or access tokens in public code repositories.

---

## 10. Handling HTTP Errors

An API request may fail for several reasons:

- Incorrect endpoint
- Missing permissions
- Invalid request data
- Server problems
- Internet connection problems

### Example 1: Checking Status Code

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/999999"

response = requests.get(url, timeout=10)

if response.status_code == 200:
    print("Request successful")

elif response.status_code == 404:
    print("Resource not found")

else:
    print("Request failed:", response.status_code)
```

Expected output:

```text
Resource not found
```

### Example 2: Using raise_for_status()

The `raise_for_status()` method raises an exception when an HTTP error response is received.

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/999999"

try:

    response = requests.get(url, timeout=10)

    response.raise_for_status()

    print(response.json())

except requests.exceptions.HTTPError as error:

    print("HTTP Error:", error)
```

Expected output will contain an HTTP 404 error message.

**Important:** `raise_for_status()` raises exceptions for unsuccessful HTTP status codes such as 404 and 500. It does not raise an exception for a normal 3xx response.

---

## 11. Handling Different Request Exceptions

The Requests library provides different exceptions for different problems.

| Exception | Meaning |
|---|---|
| `HTTPError` | HTTP error response |
| `ConnectionError` | Connection could not be established |
| `Timeout` | Request took too long |
| `RequestException` | General Requests-related error |

### Practical Example

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

try:

    response = requests.get(url, timeout=5)

    response.raise_for_status()

    data = response.json()

    print("Title:", data["title"])

except requests.exceptions.Timeout:

    print("The request timed out.")

except requests.exceptions.ConnectionError:

    print("Unable to connect to the server.")

except requests.exceptions.HTTPError as error:

    print("HTTP error:", error)

except requests.exceptions.RequestException as error:

    print("Request error:", error)

except ValueError:

    print("Invalid JSON response.")
```

### Why Use Timeout?

Without a timeout, a request may wait for an unexpectedly long time.

Always set a reasonable timeout when making API requests.

### Handling Invalid JSON

Sometimes a server may return text or HTML instead of valid JSON.

```python
import requests

try:

    response = requests.get(
        "https://jsonplaceholder.typicode.com/posts/1",
        timeout=10
    )

    response.raise_for_status()

    data = response.json()

    print(data)

except requests.exceptions.RequestException as error:

    print("Request failed:", error)

except ValueError:

    print("The response is not valid JSON.")
```

---

## 12. Sending POST Requests

The POST method is commonly used to create a new resource.

For JSON APIs, Requests provides the `json` parameter.

### Example: Create a New Post

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

new_post = {
    "title": "Learning Python APIs",
    "body": "Python makes API integration simple.",
    "userId": 1
}

response = requests.post(
    url,
    json=new_post,
    timeout=10
)

print("Status Code:", response.status_code)
print("Created Data:", response.json())
```

Expected output will contain a response similar to:

```text
Status Code: 201
Created Data: {
    'title': 'Learning Python APIs',
    'body': 'Python makes API integration simple.',
    'userId': 1,
    'id': 101
}
```

The exact returned structure is controlled by the API.

### Difference Between data and json

| Parameter | Purpose |
|---|---|
| `json=` | Sends data encoded as JSON |
| `data=` | Sends form data or supplied request body data |

### Example: Sending Form Data

```python
import requests

url = "https://httpbin.org/post"

form_data = {
    "username": "raj",
    "course": "Python"
}

response = requests.post(
    url,
    data=form_data,
    timeout=10
)

print("Status:", response.status_code)
print(response.json()["form"])
```

This example uses HTTPBin, a testing service that returns information about the request it receives.

---

## 13. Sending PUT Requests

PUT is generally used to replace an existing resource.

### Example

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

updated_post = {
    "id": 1,
    "title": "Updated Python Title",
    "body": "This post has been updated.",
    "userId": 1
}

response = requests.put(
    url,
    json=updated_post,
    timeout=10
)

print("Status:", response.status_code)
print(response.json())
```

Expected status:

```text
Status: 200
```

---

## 14. Sending PATCH Requests

PATCH is used to update selected fields instead of replacing the complete resource.

### Example

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

updated_data = {
    "title": "Only Title Updated"
}

response = requests.patch(
    url,
    json=updated_data,
    timeout=10
)

print("Status:", response.status_code)
print(response.json())
```

Expected status:

```text
Status: 200
```

### PUT vs PATCH

| PUT | PATCH |
|---|---|
| Generally replaces the resource | Updates selected fields |
| Sends the complete representation | Sends only changed fields |
| Used for full updates | Used for partial updates |

---

## 15. Sending DELETE Requests

DELETE is used to request removal of a resource.

### Example

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

response = requests.delete(url, timeout=10)

print("Status Code:", response.status_code)

if response.status_code == 200:
    print("Resource deleted successfully.")

elif response.status_code == 204:
    print("Resource deleted. No response body.")

else:
    print("Delete request status:", response.status_code)
```

### Important Note About JSONPlaceholder

JSONPlaceholder is a testing API.

Its POST, PUT, PATCH and DELETE endpoints simulate changes and return example responses. They do not permanently save, update or delete records on a real database.

---

## 16. Understanding Path Parameters and Query Parameters

Both are used to identify or filter API resources, but they serve different purposes.

### Path Parameter

A path parameter identifies a specific resource.

Example:

```text
https://jsonplaceholder.typicode.com/posts/5
```

Here, `5` identifies the post.

### Query Parameter

A query parameter filters or customizes results.

Example:

```text
https://jsonplaceholder.typicode.com/posts?userId=2
```

Here, `userId=2` filters posts by user.

### Comparison

| Path Parameter | Query Parameter |
|---|---|
| Usually identifies a resource | Usually filters or customizes results |
| Appears in URL path | Appears after `?` |
| Example: `/posts/5` | Example: `/posts?userId=2` |

---

## 17. API Authentication and API Keys

Some APIs require authentication before allowing access.

An API key is a unique value used to identify or authorize an application.

Other APIs may use:

- Bearer tokens
- OAuth 2.0
- Basic authentication
- Session-based authentication

### Example: Bearer Token Header

```python
import requests

api_url = "https://example.com/api/profile"

token = "YOUR_API_TOKEN"

headers = {
    "Authorization": f"Bearer {token}",
    "Accept": "application/json"
}

response = requests.get(
    api_url,
    headers=headers,
    timeout=10
)

print(response.status_code)
```

This is a demonstration. Replace the example URL and token with credentials from an API you are authorized to use.

### Store API Keys in Environment Variables

Do not directly write real API keys in source code.

```python
import os
import requests

api_key = os.getenv("MY_API_KEY")

if not api_key:

    print("API key not found.")

else:

    headers = {
        "Authorization": f"Bearer {api_key}"
    }

    print("API authentication header prepared.")
```

### Setting an Environment Variable in Windows PowerShell

For the current terminal session:

```powershell
$env:MY_API_KEY="your_real_api_key"
```

Then run the Python program from the same terminal.

### Security Rules

1. Never upload API keys to GitHub.
2. Never share private tokens.
3. Use environment variables for secrets.
4. Use `.gitignore` to exclude local secret files.
5. Follow the API provider's authentication rules.

---

## 18. Understanding API Pagination

Some APIs return thousands of records.

Returning everything in one response can be slow and inefficient.

Pagination divides data into smaller groups called pages.

For example:

```text
Page 1 → Records 1 to 10
Page 2 → Records 11 to 20
Page 3 → Records 21 to 30
```

APIs may implement pagination using:

- Page number
- Limit and offset
- Cursor
- Next-page URL

### Example: Page and Limit Parameters

```python
import requests

url = "https://example.com/api/products"

params = {
    "page": 1,
    "limit": 10
}

response = requests.get(
    url,
    params=params,
    timeout=10
)

print(response.url)
```

This is a conceptual example. The actual API must support these parameter names.

### Important

Always check the API documentation to understand its pagination method.

---

## 19. Understanding API Rate Limits

An API provider may restrict how many requests an application can send within a specific period.

This restriction is called a rate limit.

Example:

```text
100 requests per minute
```

If the limit is exceeded, the API may return:

```text
429 Too Many Requests
```

### Best Practices

- Avoid unnecessary API calls.
- Cache responses when appropriate.
- Respect rate-limit instructions.
- Check the `Retry-After` response header when provided.
- Use reasonable delays when making repeated requests.

### Simple Delay Example

```python
import requests
import time

url = "https://jsonplaceholder.typicode.com/posts"

for page in range(1, 4):

    response = requests.get(url, timeout=10)

    if response.ok:
        print("Request successful:", page)

    else:
        print("Request failed:", response.status_code)

    time.sleep(1)
```

This example demonstrates a delay between requests. It does not implement pagination because JSONPlaceholder's posts endpoint does not use the `page` parameter in this example.

---

## 20. Practical Programs

### Program 1: Display All Users

```python
import requests

url = "https://jsonplaceholder.typicode.com/users"

try:

    response = requests.get(url, timeout=10)

    response.raise_for_status()

    users = response.json()

    for user in users:

        print("ID:", user["id"])
        print("Name:", user["name"])
        print("Email:", user["email"])
        print("City:", user["address"]["city"])
        print("-" * 40)

except requests.exceptions.RequestException as error:

    print("API Error:", error)
```

### Program 2: Search a User by ID

```python
import requests

user_id = int(input("Enter user ID: "))

url = f"https://jsonplaceholder.typicode.com/users/{user_id}"

try:

    response = requests.get(url, timeout=10)

    response.raise_for_status()

    user = response.json()

    print("Name:", user["name"])
    print("Username:", user["username"])
    print("Email:", user["email"])
    print("Phone:", user["phone"])

except requests.exceptions.HTTPError:

    print("User not found.")

except requests.exceptions.RequestException as error:

    print("Request failed:", error)

except ValueError:

    print("Please enter a valid numeric ID.")
```

### Program 3: Count Posts by User

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

try:

    response = requests.get(url, timeout=10)

    response.raise_for_status()

    posts = response.json()

    post_count = {}

    for post in posts:

        user_id = post["userId"]

        post_count[user_id] = post_count.get(user_id, 0) + 1

    for user_id, count in post_count.items():

        print(f"User {user_id}: {count} posts")

except requests.exceptions.RequestException as error:

    print("API Error:", error)
```

### Program 4: Search Posts by Keyword

```python
import requests

keyword = input("Enter keyword: ").lower()

url = "https://jsonplaceholder.typicode.com/posts"

try:

    response = requests.get(url, timeout=10)

    response.raise_for_status()

    posts = response.json()

    found = False

    for post in posts:

        title = post["title"].lower()
        body = post["body"].lower()

        if keyword in title or keyword in body:

            print("Post ID:", post["id"])
            print("Title:", post["title"])
            print("-" * 40)

            found = True

    if not found:
        print("No matching posts found.")

except requests.exceptions.RequestException as error:

    print("API Error:", error)
```

---

# 21. Mini Project – Public API Data Explorer

## Project Description

Create a menu-driven Python application that communicates with JSONPlaceholder.

The application should allow users to:

1. View all posts.
2. View a single post.
3. Search posts by user ID.
4. Search posts by keyword.
5. Create a new post.
6. Update a post.
7. Delete a post.
8. Exit the application.

This project will use GET, POST, PUT, PATCH and DELETE requests.

**Important:** JSONPlaceholder is a mock testing service. Create, update and delete operations return simulated responses and do not permanently modify its database.

## Project Folder Structure

```text
Day-37/
│
├── Day-37-Practical.md
│
└── API-Explorer/
    │
    ├── main.py
    └── requirements.txt
```

## Step 1: Create requirements.txt

```text
requests
```

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

## Step 2: Create main.py

```python
import requests

BASE_URL = "https://jsonplaceholder.typicode.com"


def make_request(method, endpoint, data=None, params=None):

    url = BASE_URL + endpoint

    try:

        response = requests.request(
            method,
            url,
            json=data,
            params=params,
            timeout=10
        )

        response.raise_for_status()

        if response.status_code == 204:
            return {}

        return response.json()

    except requests.exceptions.Timeout:

        print("Request timed out.")

    except requests.exceptions.ConnectionError:

        print("Unable to connect to the API.")

    except requests.exceptions.HTTPError as error:

        print("HTTP Error:", error)

    except requests.exceptions.RequestException as error:

        print("Request Error:", error)

    except ValueError:

        print("Invalid JSON response.")

    return None


def view_all_posts():

    posts = make_request("GET", "/posts")

    if posts is None:
        return

    for post in posts:

        print("\nPost ID:", post["id"])
        print("Title:", post["title"])
        print("User ID:", post["userId"])
        print("-" * 40)


def view_single_post():

    post_id = input("Enter post ID: ")

    if not post_id.isdigit() or int(post_id) <= 0:
        print("Invalid post ID.")
        return

    post = make_request("GET", f"/posts/{post_id}")

    if post is None:
        return

    if not post:
        print("Post not found.")
        return

    print("\nPost ID:", post["id"])
    print("Title:", post["title"])
    print("Body:", post["body"])
    print("User ID:", post["userId"])


def search_by_user():

    user_id = input("Enter user ID: ")

    if not user_id.isdigit() or int(user_id) <= 0:
        print("Invalid user ID.")
        return

    posts = make_request(
        "GET",
        "/posts",
        params={"userId": user_id}
    )

    if posts is None:
        return

    if not posts:
        print("No posts found.")
        return

    for post in posts:

        print("\nPost ID:", post["id"])
        print("Title:", post["title"])


def search_by_keyword():

    keyword = input("Enter keyword: ").strip().lower()

    if not keyword:
        print("Keyword cannot be empty.")
        return

    posts = make_request("GET", "/posts")

    if posts is None:
        return

    found = False

    for post in posts:

        if (
            keyword in post["title"].lower()
            or keyword in post["body"].lower()
        ):

            print("\nPost ID:", post["id"])
            print("Title:", post["title"])

            found = True

    if not found:
        print("No matching posts found.")


def create_post():

    title = input("Enter title: ").strip()
    body = input("Enter body: ").strip()

    if not title or not body:
        print("Title and body are required.")
        return

    new_post = {
        "title": title,
        "body": body,
        "userId": 1
    }

    result = make_request(
        "POST",
        "/posts",
        data=new_post
    )

    if result is not None:

        print("Post creation response:")
        print(result)


def update_post():

    post_id = input("Enter post ID: ")

    if not post_id.isdigit() or int(post_id) <= 0:
        print("Invalid post ID.")
        return

    title = input("Enter new title: ").strip()

    if not title:
        print("Title cannot be empty.")
        return

    updated_data = {
        "title": title
    }

    result = make_request(
        "PATCH",
        f"/posts/{post_id}",
        data=updated_data
    )

    if result is not None:

        print("Post update response:")
        print(result)


def delete_post():

    post_id = input("Enter post ID: ")

    if not post_id.isdigit() or int(post_id) <= 0:
        print("Invalid post ID.")
        return

    result = make_request(
        "DELETE",
        f"/posts/{post_id}"
    )

    if result is not None:

        print("Delete request completed.")
        print("Response:", result)


def main():

    while True:

        print("\n========== API DATA EXPLORER ==========")

        print("1. View All Posts")
        print("2. View Single Post")
        print("3. Search Posts by User ID")
        print("4. Search Posts by Keyword")
        print("5. Create Post")
        print("6. Update Post")
        print("7. Delete Post")
        print("8. Exit")

        choice = input("\nEnter your choice: ").strip()

        if choice == "1":

            view_all_posts()

        elif choice == "2":

            view_single_post()

        elif choice == "3":

            search_by_user()

        elif choice == "4":

            search_by_keyword()

        elif choice == "5":

            create_post()

        elif choice == "6":

            update_post()

        elif choice == "7":

            delete_post()

        elif choice == "8":

            print("Thank you for using API Data Explorer.")
            break

        else:

            print("Invalid choice. Try again.")


if __name__ == "__main__":

    main()
```

## Step 3: Run the Project

Open the terminal inside the `API-Explorer` folder.

```bash
python main.py
```

Expected menu:

```text
========== API DATA EXPLORER ==========

1. View All Posts
2. View Single Post
3. Search Posts by User ID
4. Search Posts by Keyword
5. Create Post
6. Update Post
7. Delete Post
8. Exit

Enter your choice:
```

### Important Project Notes

- The project requires an active internet connection.
- The API must be reachable for requests to work.
- A successful DELETE response does not prove that a record was permanently deleted on JSONPlaceholder.
- POST, PUT and PATCH operations are simulated.
- In this learning project, the API response is displayed directly instead of maintaining a local database.

---

# 22. Student Practice Exercises

## Beginner Level

1. Install the Requests library.
2. Send a GET request to retrieve all posts.
3. Display the status code of an API response.
4. Retrieve a single post using its ID.
5. Display the title and body of a post.
6. Retrieve all users and display their names.
7. Print the URL of a request.
8. Display the Content-Type response header.

## Intermediate Level

1. Retrieve posts belonging to a particular user.
2. Display only posts containing a particular keyword.
3. Count how many posts each user has created.
4. Create a new post using POST.
5. Update a post using PUT.
6. Change only the title using PATCH.
7. Send a DELETE request for a particular post.
8. Handle HTTP errors using `raise_for_status()`.
9. Handle timeout and connection exceptions.
10. Send custom headers with an API request.

## Advanced Level

1. Build a menu-driven user information explorer.
2. Create a program that fetches posts and generates a summary report.
3. Implement a reusable API request function.
4. Read API configuration from environment variables.
5. Build a paginated data-fetching example using an API that supports pagination.
6. Implement retry handling for temporary server failures, respecting rate limits.
7. Create a program that exports API response data into a JSON file.
8. Build an application that fetches API data and exports selected records into a CSV file.

---

# 23. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is an API?
2. What is the difference between an API and an endpoint?
3. What is a REST API?
4. What is HTTP?
5. What is the difference between GET and POST?
6. What is the difference between PUT and PATCH?
7. What does HTTP status code 404 mean?
8. What does HTTP status code 500 mean?
9. What is JSON?
10. How do you convert an API response into Python data?
11. What is the purpose of `response.json()`?
12. Why should we use a request timeout?
13. What is the purpose of `raise_for_status()`?
14. What are query parameters?
15. What are HTTP headers?
16. What is an API key?
17. Why should API keys not be uploaded to GitHub?
18. What is API pagination?
19. What is API rate limiting?
20. How does the Requests library handle connection errors?

### Practical Assessment

Ask the student to independently:

- Fetch data from a public API.
- Parse the JSON response.
- Extract selected fields.
- Filter records.
- Send a POST request.
- Send a PATCH request.
- Send a DELETE request.
- Handle HTTP and connection errors.
- Build a small API-based application.

---

# 24. Completion Criteria

Day 37 is complete when the student can:

- Explain API communication between client and server.
- Understand HTTP methods and status codes.
- Install and import the Requests library.
- Send GET, POST, PUT, PATCH and DELETE requests.
- Work with JSON API responses.
- Use query parameters and headers.
- Handle HTTP errors, timeouts and connection failures.
- Understand API authentication and basic security.
- Explain pagination and rate limiting.
- Build and run the Public API Data Explorer project independently.
