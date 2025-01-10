# Demo ollama on OpenShift

This repo contains information on how to deploy ollama on OpenShift.

## Requirements

- OpenShift >= 4.15
- A worker node with a GPU - **Highly Recommended**
  - AWS
    - `g4dn.2xlarge`
    - `g5.2xlarge`

## Quickstart

```sh
oc apply -k deploy
```

See [Additional Info](NOTES.md)

## Links

- [Github - ollama](https://github.com/ollama/ollama)
- [docker.io - ollama container](https://hub.docker.com/r/ollama/ollama)
- [Github - ollama UBI container](https://github.com/williamcaban/ollama-ubi)
