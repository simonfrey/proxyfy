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
`GimmeProxyConfig{
	ApiKey:         apiKey,
	Protocol:       scheme,
	MaxCheckPeriod: 30,
	Get:            true,
	Post:           true,
	SupportsHTTPS:  true,
	Referer:true,
	MinSpeed: 2000,
}`

## Advanced

`proxyfy := NewProxyfyAdvancedConfig(gimmeConfig GimmeProxyConfig)`

The gimmeConfig is defined via the following struct:
`type GimmeProxyConfig struct {
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
}`
For documentation on the different values visit: https://gimmeproxy.com/#api


# License
MIT License