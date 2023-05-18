$ kubectl apply -f prometheus.yaml
$ kubectl apply -f kiali.yaml
$ kubectl -n istio-system port-forward service/kiali 20001

Reference: https://istio.io/latest/docs/tasks/observability/kiali