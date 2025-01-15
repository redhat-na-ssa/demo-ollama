# Demo ollama on OpenShift

## Testing

### OpenShift

```sh
oc apply -k deploy

OLLAMA_HOST=http://$(oc get route -n ollama --output=custom-columns=':.spec.host' --no-headers)
echo ${OLLAMA_HOST}
```

Pull and test the `minilm` embeddings model.

```sh
curl -sL ${OLLAMA_HOST}/api/pull -d '{"name": "all-minilm"}'
curl -sL ${OLLAMA_HOST}/api/embed -d '{ "model": "all-minilm", "input": "hello" }'
```

Pull and test the `granite3-dense:8b` LLM.

```sh
PROMPT="hello"
curl -sL ${OLLAMA_HOST}/api/pull -d '{"name": "granite3-dense:8b"}'
curl -sL ${OLLAMA_HOST}/api/generate -d '{"model": "granite3-dense:8b", "prompt": "'${PROMPT}'", "stream": false }' | jq .response
```

View available cached models.

```sh
curl ${OLLAMA_HOST}/api/tags | jq
```

### Local testing

```sh
cd ollama
podman-compose up

OLLAMA_HOST=http://localhost:11434
```

Run gradio chat client

```sh
export OLLAMA_HOST
python client/00-ollama-chat.py
```
Localhost (compose)
