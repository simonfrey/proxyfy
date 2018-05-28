# Proxyfy

![Proxyfy Logo](https://image.flaticon.com/icons/svg/148/148800.svg)

---

Wrapper around gimmeproxy.com - API compatible to http.Client

With proxyfy you can simply add proxied requests to your go client.

It is as simple as changing `http.Get("https://github.com")` to `proxyfy.Get("https://github.com")`. From now on all the request get forwarded trough a random proxy.

*For getting more than the 240 free request, please visit gimmeproxy.com and get yourself an API key.*

---

# Usage
You have to setup proxyfy via an initalizer.
There are two different ones available:

## Simple

```go
proxyfy := proxyfy.NewProxyfy(apiKey,schema string)
```

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

```go
proxyfy := NewProxyfyAdvancedConfig(gimmeConfig GimmeProxyConfig)
```

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
Fire 30 GET requests and print the http response code

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

# Available Functions

## GetAllProxys
GetAllProxys returns a slice containing all proxies that are available

```go 
func (c *Proxyfy) GetAllProxys() []*url.URL 
```

## Do
Do executes the given *http.Request using a random proxy

```go
func (c *Proxyfy) Do(req *http.Request) (resp *http.Response, err error)
```

Similar to `http.Do()`

## Get
Get is a wrapper around Do(). Executes a GET request using a random proxy

```go
func (c *Proxyfy) Get(url string) (resp *http.Response, err error)
```
Similar to `http.Get()`

## Head

Head is a wrapper around Do(). Executes a HEAD request using a random proxy

```go
func (c *Proxyfy) Head(url string) (resp *http.Response, err error) 
```

Similar to `http.Head`

## Post

Post is a wrapper around Do(). Executes a POST request using a random proxy

```go
func (c *Proxyfy) Post(url string, contentType string, body io.Reader) (resp *http.Response, err error)
```

Similar to `http.Post`

## PostForm

PostForm is a wrapper around Post(). Executes a Post request using a random proxy and sending data as x-www-form-urlencoded

```go
func (c *Proxyfy) PostForm(url string, data url.Values) (resp *http.Response, err error) 
```

Similar to `http.PostForm`

## NewProxyfyAdvancedConfig
NewProxyfyAdvancedConfig sets up proxyfy with an advanced configuration.

```go
func NewProxyfyAdvancedConfig(gimmeConfig GimmeProxyConfig) *Proxyfy
```

Also have a look in the part Usage of this README

## NewProxyfy

NewProxyfy sets up proxyfy with a minimal amount of input data

```go
func NewProxyfy(apiKey, scheme string) *Proxyfy
```

Also have a look in the part Usage of this README

---

**License**

MIT License

**Icons**

 Icons made by Smashicons from www.flaticon.com is licensed by CC 3.0 BY