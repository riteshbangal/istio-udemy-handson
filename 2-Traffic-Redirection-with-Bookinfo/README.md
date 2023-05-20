$ kubectl -n istio-system port-forward service/kiali 20001

$ kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"


$ export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT
$ curl -s "http://${GATEWAY_URL}/productpage" | grep -o "<title>.*</title>"


$ kubectl rollout restart deployment details-v1
$ while true; do curl -skI  http://localhost/productpage | grep "HTTP"; sleep 1; done


$ 
$ curl -I https://app-gw.eintuition.net/api/portfolio?username=riteshbangal

$ cd /Users/riteshbangal/Geeks/workshop/istio/Certificates/nginx/server/v2
..v2> $ curl -ksI --cert client.crt --key client.key https://ec2-3-125-207-155.eu-central-1.compute.amazonaws.com/ | grep  HTTP


$ sudo vim /etc/hosts
$ sudo dscacheutil -flushcache
