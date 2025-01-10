# Demo with ollama on Openshift

## Prereqs

- Openshift >= 4.16
- A worker node with a GPU
  - AWS
    - `g4dn.2xlarge`
    - `g5.2xlarge`

```sh
oc apply -k resources/ollama
```

Testing

```sh
OLLAMA_HOST=http://$(oc get route -n ollama --output=custom-columns=':.spec.host' --no-headers)
```

```sh
curl ${OLLAMA_HOST}/api/pull -d '{"name": "granite3-dense:8b"}'
curl ${OLLAMA_HOST}/api/pull -d '{"name": "all-minilm"}'
```

```sh
curl ${OLLAMA_HOST}/api/tags | jq
```

```sh
curl ${OLLAMA_HOST}/api/embed -d '{ "model": "all-minilm", "input": "hello" }'
```

```sh
curl ${OLLAMA_HOST}/api/generate -d '{"model": "granite3-dense:8b", "prompt": "hello", "stream": false }'
```

```sh
python src/00-ollama-chat.py
```

Visit http://localhost:7260
