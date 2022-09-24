[![Go](https://img.shields.io/badge/--00ADD8?logo=go&logoColor=ffffff)](https://golang.org/)  [![Go Reference](https://pkg.go.dev/badge/github.com/floscodes/go-http-router.svg)](https://pkg.go.dev/github.com/floscodes/go-http-router)
# Easy to use router for http-services


### Set routes and link them to functions

```go
func main() {
	router := router.New()

	router.Handle("/hello", hello)

	fmt.Println("Server is listening")
	http.ListenAndServe(":8080", router)

}

func hello(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("Hello!"))
}
```

You can specify the allowed methods like this:
```go
router.Handle("/hello", hello).Methods("POST", "GET")
```

The router will accept trailing slashes typed by the client by default, even if none is set in the handling path.
You can disable that this way for a certain route...
```go
router.Handle("/hello", hello).AcceptTrailingSlash(false)
```
... or disable it for all routes:
```go
router.AcceptTrailingSlash(false)
```

### Serve static files

```go
router.ServeStatic("/static", "./static")
```

If the request does not contain a specific filename, the router will automatically look for `index.html`.

Optionally you can set a custom index file:
```
router.ServeStatic("/static", "./static").IndexFile("template.html")
```
