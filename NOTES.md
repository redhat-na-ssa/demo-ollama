# Demo ollama on OpenShift



## Testing

Localhost (compose)

```sh
cd ollama
podman-compose up

OLLAMA_HOST=http://localhost:11434
```

OpenShift

```sh
oc apply -k deploy

OLLAMA_HOST=http://$(oc get route -n ollama --output=custom-columns=':.spec.host' --no-headers)
echo ${OLLAMA_HOST}
```

Test `minilm`

```sh
curl ${OLLAMA_HOST}/api/pull -d '{"name": "all-minilm"}'
curl ${OLLAMA_HOST}/api/embed -d '{ "model": "all-minilm", "input": "hello" }'
```

Test `granite3-dense:8b`

```sh
PROMPT="hello"
curl ${OLLAMA_HOST}/api/pull -d '{"name": "granite3-dense:8b"}'
curl ${OLLAMA_HOST}/api/generate -d '{"model": "granite3-dense:8b", "prompt": "'${PROMPT}'", "stream": false }'
```

View available models

```sh
curl ${OLLAMA_HOST}/api/tags | jq
```

Run gradio chat client

```sh
python client/00-ollama-chat.py
```
