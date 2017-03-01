# Download the App Engine SDK for Go
https://cloud.google.com/appengine/docs/standard/go/download

# Add PATH
```
echo "export PATH=\$PATH:/Users/howdy/go_appengine" >> .bash_profile
```

# Create File

## tree
```
Tatsuyas-MacBook:firstgo howdy$ tree
.
├── app.yaml
└── hello.go

```

## app.yaml
```
application: helloworld
version: 1
runtime: go
api_version: go1
handlers:
- url: /.*
  script: _go_app
```

## hello.go
```
package hello

import (
	"fmt"
	"net/http"
)

func init() {
	http.HandleFunc("/hello", handler)
}

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "Hello, world!")
}
```

# Run
goapp serve firstgo

# Browser
http://localhost:8080/hello
