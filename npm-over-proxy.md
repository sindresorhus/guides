# Use `npm` over proxy servers

In some situations you will need use `npm install (wathever)` over a http proxy. Whe you need do it, you can run this command on terminal:

```sh
npm config set proxy http://proxy.company.com:8080
npm config set https-proxy http://proxy.company.com:8080
```
