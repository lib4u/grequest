# Grequests 
![logo(1)](https://github.com/user-attachments/assets/3bef5ed3-a40b-4634-9de4-a2dd43d57f3d)



Simple and lightweight golang library for http requests. based on powerful net/http
grequest is inspired by the Request library for Python and Guzzle in PHP, the goal is to make a simple and convenient library for making http requests in go

The library has a flexible API with methods that return a pointer to the library structure, which allows you to declaratively describe a request using a chain of methods.

Library also contains ready-made methods for working with json, request body, cookies and working with files over the network and  to the **lightweight nature of the library and the absence of third-party dependencies**, you can easily connect it to your projects.
## Features 

**😎 Simple HTTP client**
- No third party dependencies
- Directly uses net/http
- Lightweight library
- Ensures safe handling and completion of HTTP responses.
- Limit for executing a request with context.WithTimeoutis already set

**🖊 Body and request**:
  - Set the request body 
  - Easily configure JSON payloads in the request body.
  - Retrieve server response status codes as integers or strings.
  - Supports GET, POST, PUT, DELETE, and other methods.
  - Ability to install advanced methods

**📄 JSON handling**:
  - Retrieve JSON from response bodies and transform it into structures.
  - Parse JSON from response bodies into string maps.
  - Send Json in body request

**⚙️ Header management**:
  - Convenient manipulation of request and response headers.
  - Get all headers in string map
  - Set request headers
  - Retrieve and set the `Content-Type`.

**🍪 Cookie handling**:
  - Send cookies with requests.
  - Retrieve and save cookies to a file for later use.
  
**📁 File handling**:
  - Save files from responses.
  - Downloading a file directly from a URL with the extension
  - Upload files to a server.

**📝 Form data submission** 
- Set web forms fields
- Support Multipart form data
- Support Form Url encoded


**🔒 Proxy support**:
  - Configure a proxy server for requests.

**🔑 Authentication** 
- Basic Authentication
- Bearer Authentication 
- Token Authentication

## Examples
Simple get request anf get string response
```go
req := app.Get("https://jsonplaceholder.typicode.com/todos/1").Do()
	response := req.Body().GetStrings()
	fmt.Println(response)
```
Get a response and writing it to a json structure
```go
type AutoGenerated struct {
	UserID    int    `json:"userId"`
	ID        int    `json:"id"`
	Title     string `json:"title"`
	Completed bool   `json:"completed"`
}
...
   var myJsonResponse AutoGenerated
	req := app.Get("https://jsonplaceholder.typicode.com/todos/1").Do()
	err := req.Body().GetWithJsonStruct(&myJsonResponse)
	if err != nil {
		fmt.Println("do ..")
	}
	fmt.Println(myJsonResponse.Title)
```
Simple post request with json payload body and get status of response
```go
data := LoginRequest{
		Username: "example",
		Password: "12345",
	}
	req := app.Post("https://example.site/login").Body().SetJson(data).Do()
	fmt.Println(req.Status().GetCode())
```
Simple save file from response
```go
// file will saved as ../files/image.png
app.Get("https://example.com/image.png").Do().Body().SaveFile()
//OR
app.Get("https://example.com/image.png").Do().Body().Path("/user/files").SaveFile()
//OR 
app.Get("https://example.com/image.png").Do().Body().ToFile("path/savedimage.png")
```
