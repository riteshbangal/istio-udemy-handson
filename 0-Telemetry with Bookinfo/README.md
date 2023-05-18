$ kubectl apply -f 1-bookinfo-namespace.yaml -n bookinfo
$ kubectl apply -f 2-bookinfo.yaml -n bookinfo
$ kubectl apply -f 3-bookinfo-gateway.yaml -n bookinfo
$ kubectl apply -f 4-destination-rule-all.yaml -n bookinfo
$ kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"


$ export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT
$ curl -s "http://${GATEWAY_URL}/productpage" | grep -o "<title>.*</title>"



