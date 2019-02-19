# Dex Example App

## TODO

- Nicer frontend for dex app
- Figure out internal URLs, redirects (can use localhost, avoid editing /etc/hosts?)
- Use ID token to get AWS STS credentials and generate IAM credentials

## Query Provider

- Use `curl -v dex:9000/dex/.well-known/openid-configuration` to inspect openid config

## Issuer & Callback URLs

- Issuer URLs and callback URLs must match
- To make matters more complicated, we have 2 different callbacks in place
- Callback from ID provider (Github) to dex: `http://dex:9000/dex/callback`
- Callback from dex to dex client: `http://dex-app:5555/callback`

### Host Mapping

- Unless running on Linux we can't use `127.0.0.1` since URLs in the docker network are different
- E.g. `dex-app` will use `dex:9000/dex` to talk to the issue and expect the callback to be `http://dex:9000/dex/callback`
- However your browser will not know this hostname and fail to load the callback URL
- Edit `/etc/hosts` to configure host aliases so they match the ones used by docker internally:

```txt
127.0.0.1 dex dex-app dex-proxy
```
