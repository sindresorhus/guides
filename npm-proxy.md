# Use npm through a corporate proxy

In some situations you might need use `npm install <cmd>` over a HTTP proxy. Set the proxy URL in the global npm config to make it work:

```console
$ npm config set proxy http://proxy.company.com:8080
$ npm config set https-proxy http://proxy.company.com:8080
```
