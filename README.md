# ollama
## Experiment with ollama on Openshift
### Prereqs
- Openshift >= v4.17.x
- A worker node with a GPU (ec2 instance types `g4dn.2xlarge` or `g5.2xlarge`)
- 

```bash
oc apply -k resources/ollama
```

Testing

```bash
OLLAMA_HOST=http://$(oc get route -n ollama --output=custom-columns=':.spec.host' --no-headers)
```

```bash
curl $OLLAMA_HOST/api/pull -d '{"name": "granite3-dense:8b"}'
curl $OLLAMA_HOST/api/pull -d '{"name": "all-minilm"}'
```

```bash
curl $OLLAMA_HOST/api/tags | jq
```

```bash
curl $OLLAMA_HOST/api/embed -d '{ "model": "all-minilm", "input": "hello" }'
```

```bash
curl $OLLAMA_HOST/api/generate -d '{"model": "granite3-dense:8b", "prompt": "hello", "stream": false }'
```

```bash
python src/00-ollama-chat.py
```

Visit http://localhost:7260

