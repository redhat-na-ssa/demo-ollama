# Demo ollama on OpenShift

This repo contains information on how to deploy ollama on OpenShift.

## Requirements

- OpenShift >= 4.15
- A GPU worker node with at least 16GB of GPU memory.
  - AWS
    - `g4dn.2xlarge`
    - `g5.2xlarge`

## Installation Quickstart

Use CPU only

```sh
# setup ollama
until oc apply -k deploy; do : ; done
```

Use Nvidia GPU

```sh
# setup nvidia gpu nodes (prerequisite)
until oc apply -k deploy/nvidia-gpu-autoscale; do : ; done
```

```sh
# setup ollama w/ gpu
until oc apply -k deploy; do : ; done
until oc apply -k deploy/ollama-gpu; do : ; done
```

Setup Web Terminal (optional)

```sh
until oc apply -k deploy/web-terminal; do : ; done
```

See [these additional notes on how to pull and test models](NOTES.md).

## Links

- [Containerfile / Dockerfile](ollama/Dockerfile)
- [Github - ollama](https://github.com/ollama/ollama)
- [docker.io - ollama container](https://hub.docker.com/r/ollama/ollama)
- [Github - ollama UBI container](https://github.com/williamcaban/ollama-ubi)
