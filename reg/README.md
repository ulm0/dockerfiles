# Reg

> [`reg`](https://github.com/genuinetools/reg) is a tool developed by genuine tools

This project packs `reg` to use it as a simple frontend for your docker registry

## Run

All you need to have is `docker` installed and set some env vars

```sh
docker run -d --name registry_frontend -e REGISTRY_URL=my.registry.com -e REGISTRY_USER=myuser -e REGISTRY_PASSWORD=mypassword -p 8080:8080 ulm0/reg
```

### Options

- `CLAIR` = Default `false`. Set to `true` if you want to use clair vulnerability reports. 
- `CLAIR_SERVER` = Default `""`. If `CLAIR` is set to `true` you need to set this including scheme  (e.g. `https://clair.registry.com`)
- `REGISTRY_URL` = Default `""`. Sets registry url to serve, assumes is https, so no scheme is needed.
- `REGISTRY_USER` = Default `""`. User to interact with the registry.
- `REGISTRY_PASSWORD` = Default `""`. Password for the given user.
