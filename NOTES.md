# Demo ollama on OpenShift

## Notes

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
curl -sL ${OLLAMA_HOST}/api/pull -d '{"name": "all-minilm"}'
curl -sL ${OLLAMA_HOST}/api/embed -d '{ "model": "all-minilm", "input": "hello" }'
```

Test `granite3-dense:8b`

```sh
PROMPT="hello"
curl -sL ${OLLAMA_HOST}/api/pull -d '{"name": "granite3-dense:8b"}'
curl -sL ${OLLAMA_HOST}/api/generate -d '{"model": "granite3-dense:8b", "prompt": "'${PROMPT}'", "stream": false }' | jq .response
```

View available models

```sh
curl ${OLLAMA_HOST}/api/tags | jq
```

Run gradio chat client (locally)

```sh
python -m venv venv
. venv/bin/activate
pip install -r requirements.txt

export OLLAMA_HOST
python client/app.py
```
