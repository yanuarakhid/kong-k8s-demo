# Init config
1. openssl req -new -x509 -nodes -newkey ec:<(openssl ecparam -name secp384r1) -keyout ./tls.key -out ./tls.crt -days 1095 -subj "/CN=kong_clustering"
2. kubectl create secret tls kong-cluster-cert --cert=./tls.crt --key=./tls.key -n kong
3. kubectl create secret generic kong-enterprise-license --from-file=license=license.json -n kong
4. helm repo add kong https://charts.konghq.com
5. helm repo update
8. kubectl get ns
9. kubectl create ns kong
10. kubectl create ns postgre
11. kubectl apply -f postgresql/postgresql.yaml -n postgre
12. helm install kong-cp kong/kong -n kong --values ./kong-cp.yaml
13. helm install kong-dp kong/kong -n kong --values ./kong-dp.yaml