# ptthx

HTTP client wrapper of std HTTP package for the unindustrious

## examples

simple get request

```go
package main

import (
	"context"
	"fmt"

	"github.com/AnimeshRy/ptthx"
)

func main() {
	cli := ptthx.New("test")

	var result map[string]interface{}

	// by default used application/json content type and json encoder/decoder

	err := cli.Get(context.Background(), "http://httpbin.org/get", &result)
	if err := nil {
		panic(err)
	}

	fmt.Println(result)
}
```

simple post form

```go
package main

import (
	"context"
	"fmt"
	"net/url"

	"github.com/AnimeshRy/ptthx"
)

func main() {
	cli := ptthx.New("test")

	data := make(url.Values)
	data.Set("test", "1")
	data.Set("test2", "2")

	var result map[string]interface{}

	err := cli.Post(context.Background(), "https://httpbin.org/post", data, &result,
		ptthx.WithEncoder(httpcli.FormURLEncodedEncoder),
		ptthx.SetHeaders("content-type", "application/x-www-form-urlencoded"))
	if err != nil {
		panic(err)
	}

	fmt.Println(result)
}
```

or

```go
package main

import (
	"context"
	"fmt"
	"net/url"

	"github.com/AnimeshRy/ptthx"
)

func main() {
	cli := httpcli.New("test",
		ptthx.WithEncoder(ptthx.FormURLEncodedEncoder),
		ptthx.SetHeaders("content-type", "application/x-www-form-urlencoded"),
	)

	data := make(url.Values)
	data.Set("test", "1")
	data.Set("test2", "2")

	var result map[string]interface{}

	err := cli.Post(context.Background(), "https://httpbin.org/post", data, &result)
	if err != nil {
		panic(err)
	}

	fmt.Println(result)
}
```
