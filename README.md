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

Use Nvidia GPUs

```sh
# setup nvidia gpu nodes
until oc apply -k deploy/nvidia-gpu-autoscale; do : ; done

# setup ollama
until oc apply -k deploy; do : ; done
until oc apply -k deploy/ollama-gpu; do : ; done
```

See [these additional notes on how to pull and test models](NOTES.md).

## Links

- [Github - ollama](https://github.com/ollama/ollama)
- [docker.io - ollama container](https://hub.docker.com/r/ollama/ollama)
- [Github - ollama UBI container](https://github.com/williamcaban/ollama-ubi)
