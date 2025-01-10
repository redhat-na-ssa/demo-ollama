# Demo ollama on OpenShift

## Requirements

- OpenShift >= 4.16
- A worker node with a GPU
  - AWS
    - `g4dn.2xlarge`
    - `g5.2xlarge`

```sh
oc apply -k deploy
```

## Testing

Localhost (compose)

```sh
cd ollama
podman-compose up
OLLAMA_HOST=http://localhost:11434
```

OpenShift

```sh
OLLAMA_HOST=http://$(oc get route -n ollama --output=custom-columns=':.spec.host' --no-headers)
echo ${OLLAMA_HOST}
```

```sh
curl ${OLLAMA_HOST}/api/pull -d '{"name": "all-minilm"}'
curl ${OLLAMA_HOST}/api/embed -d '{ "model": "all-minilm", "input": "hello" }'
```

```sh
PROMPT="hello"
curl ${OLLAMA_HOST}/api/pull -d '{"name": "granite3-dense:8b"}'
curl ${OLLAMA_HOST}/api/generate -d '{"model": "granite3-dense:8b", "prompt": "'${PROMPT}'", "stream": false }'
```

```sh
curl ${OLLAMA_HOST}/api/tags | jq
```

```sh
python client/00-ollama-chat.py
```
