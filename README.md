# go-cors
简单粗暴的解决GoWeb跨域


### go默认web服务使用

```go
package main

import (
	"log"
	"net/http"

	"github.com/wuwenbao/gocors"
)

func main() {
	mux := http.NewServeMux()

	mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("cors"))
	})

	cors := gocors.NewCors(
		mux,
		gocors.WithOrigin("*"),
		gocors.WithMethods("*"),
		gocors.WithHeaders("*"),
	)
	
	log.Fatal(http.ListenAndServe(":8080", cors))
}
```

### 第三方gorilla/mux

```go
package main

import (
	"log"
	"net/http"

	"github.com/gorilla/mux"
	"github.com/wuwenbao/gocors"
)

func main() {
	router := mux.NewRouter()

	router.Methods("GET").Path("/").HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("cors"))
	})

	cors := gocors.NewCors(
		router,
		gocors.WithOrigin("*"),
		gocors.WithMethods("*"),
		gocors.WithHeaders("*"),
	)
	
	log.Fatal(http.ListenAndServe(":8080", cors))
}
```
