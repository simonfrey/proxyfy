# Proxyfy
Wrapper around gimmeproxy - API compatible to http.Client


# Import
`import("github.com/L1am0/proxyfy")`

# Usage
You have to setup proxyfy via an initalizer.
There are two different ones available:

## Simple

`proxyfy := proxyfy.NewProxyfy(apiKey,schema string)`

Here is already a part of the config set:
```go
GimmeProxyConfig{
	ApiKey:         apiKey,
	Protocol:       scheme,
	MaxCheckPeriod: 30,
	Get:            true,
	Post:           true,
	SupportsHTTPS:  true,
	Referer:true,
	MinSpeed: 2000,
}
```

## Advanced

`proxyfy := NewProxyfyAdvancedConfig(gimmeConfig GimmeProxyConfig)`

The gimmeConfig is defined via the following struct:
```go
type GimmeProxyConfig struct {
	ApiKey         string
	Get            bool
	Post           bool
	Cookies        bool
	Referer        bool
	UserAgent      bool
	SupportsHTTPS  bool
	AnonymityLevel int
	Protocol       string
	Port           string
	Country        string
	MaxCheckPeriod int
	Websites       string
	MinSpeed       float64
	NotCountry     string
	IPPort         bool
	Curl           bool
}
```

For documentation on the different values visit: https://gimmeproxy.com/#api

# Example
Fire 30 Get requests and Print the StatusCode

```go
package main

import(
	"proxyfy"
	"fmt"
)
func main() {
	proxyfy := proxyfy.NewProxyfy("", "http")

	for i := 0; i < 30; i++ {
		resp, err := proxyfy.Get("https://t3n.de")
		if err != nil {
			fmt.Println(err)
			continue
		}
		fmt.Println(resp.StatusCode)
	}

}
```

# License
MIT License