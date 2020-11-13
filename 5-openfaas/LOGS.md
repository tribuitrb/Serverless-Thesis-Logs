
```
kubectl apply -f https://raw.githubusercontent.com/openfaas/faas-netes/master/namespaces.yml

mkdir openfaas && cd $_

helm repo add openfaas https://openfaas.github.io/faas-netes/

helm repo update \
 && helm upgrade openfaas --install openfaas/openfaas \
    --namespace openfaas  \
    --set functionNamespace=openfaas-fn \
    --set generateBasicAuth=true 

```

```
NAME: openfaas
LAST DEPLOYED: Fri Nov 13 07:59:54 2020
NAMESPACE: openfaas
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that openfaas has started, run:

  kubectl -n openfaas get deployments -l "release=openfaas, app=openfaas"
To retrieve the admin password, run:

  echo $(kubectl -n openfaas get secret basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode)
```

```
PASSWORD=$(kubectl -n openfaas get secret basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode)

echo "OpenFaaS admin password: $PASSWORD"

OpenFaaS admin password: AYUVOHj8RQpd

export OPENFAAS_URL=http://127.0.0.1:8080
kubectl port-forward --address 127.0.0.1,10.102.196.109 -n openfaas svc/gateway 8080:8080 &
```

Install OpenFaaS
```
curl -sSL https://cli.openfaas.com | sudo -E sh
```

Login with the CLI
```
echo -n $PASSWORD | faas-cli login -g $OPENFAAS_URL -u admin --password-stdin
faas-cli version
```