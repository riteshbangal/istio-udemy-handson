
$ kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"


$ export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT
$ curl -s "http://${GATEWAY_URL}/productpage" | grep -o "<title>.*</title>"



