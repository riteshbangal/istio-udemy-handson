$ kubectl -n istio-system port-forward service/kiali 20001

$ kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"


Deployment and Service for Ingress Gateway
Gateway object to enable Ingress gateway to receive traffic
Virtual Service to link services and routing rules to Ingress Gateway
selector:
  istio: ingressgateway ---> image: docker.io/istio/proxyv2:1.17.2

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

------------------------------------------------------------------------------------------
# SSL Certs and Gateway
1. Get the self signed certificates

$ export DOMAIN_NAME=bookinfo.com
$ mkdir bookinfo-certs
$ cd bookinfo-certs

$ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=$DOMAIN_NAME Inc./CN=$DOMAIN_NAME' -keyout $DOMAIN_NAME.key -out $DOMAIN_NAME.crt 

$ openssl req -out myclient.$DOMAIN_NAME.csr -newkey rsa:2048 -nodes -keyout myclient.$DOMAIN_NAME.key -subj "/CN=myclient.$DOMAIN_NAME/O=myclient from $DOMAIN_NAME"

$ openssl x509 -req -days 365 -CA $DOMAIN_NAME.crt -CAkey $DOMAIN_NAME.key -set_serial 0 -in myclient.$DOMAIN_NAME.csr -out myclient.$DOMAIN_NAME.crt

2. Bring it inside the cluster --> Kubernetes Secret

$ kubectl create -n istio-system secret tls bookinfo-credential --key=myclient.bookinfo.com.key --cert=myclient.bookinfo.com.crt

3. Configure the Gateway --> Point to the secret

4. Test the flow:

$ curl --cacert bookinfo.com.crt "https://myclient.bookinfo.com:443/app"
$ curl -kv "https://myclient.bookinfo.com:443/app"

$ curl -H "Host:myclient.bookinfo.com" --resolve "myclient.bookinfo.com:443:$INGRESS_IP" --cacert bookinfo.com.crt "https://myclient.bookinfo.com:443/app"


------------------------------------------------------------------------------------------
Try: Fix MTLS - ec2-3-125-207-155.eu-central-1.compute.amazonaws.com
$ kubectl create -n istio-system secret tls  mywebapp-mtls-credential --cert=client.crt --key=client.key

$ curl -H "Host:myclient.bookinfo.com" "https://ec2-3-125-207-155.eu-central-1.compute.amazonaws.com"



------------------------------------------------------------------------------------------
Reference: https://github.com/tetratelabs/istio-weekly/tree/main/istio-weekly/005

