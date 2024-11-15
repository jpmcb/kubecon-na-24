The following are the notes / yamls / instructions for my talk
"Building Massive-Scale Generative AI Services with Kubernetes and Open Source".

Good luck!

---

1. Apply Ubuntu demo pod to cluster

```
k apply -f demo-pod.yaml
```

2. Get onto demo Ubuntu pod

```
k exec -n default -it demo-pod -- bash
```

3. Apt update and get a few tools for demo purposes

```
apt update
apt install curl -y
apt install dnsutils -y
```

4.1 Inspect the service with DNS utils

```sh
dig vllm-service.vllm-ns.svc.cluster.local
```

4.2 Note the models available on the API:

```sh
curl vllm-service.vllm-ns.svc.cluster.local/v1/models
```

4.3 Use the service's API to do some inference:

```sh
curl vllm-service.vllm-ns.svc.cluster.local/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "TheBloke/Mistral-7B-Instruct-v0.2-AWQ",
        "messages": [
            {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```

---

# Cleanup

```
k delete -f demo-pod.yaml
```
