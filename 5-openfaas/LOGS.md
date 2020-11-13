
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

```
mkdir func && cd $_

docker login


faas-cli new --lang python3 hello-openfaas --prefix="tribuitrb"

[root@master func]$ faas-cli new --lang python3 hello-openfaas --prefix="tribuitrb"
2020/11/13 12:20:20 No templates found in current directory.
2020/11/13 12:20:20 Attempting to expand templates from https://github.com/openfaas/templates.git
2020/11/13 12:20:24 Fetched 12 template(s) : [csharp dockerfile go java11 java11-vert-x node node12 php7 python python3 python3-debian ruby] from https://github.com/openfaas/templates.git       
Folder: hello-openfaas created.
  ___                   _____           ____
 / _ \ _ __   ___ _ __ |  ___|_ _  __ _/ ___|
| | | | '_ \ / _ \ '_ \| |_ / _` |/ _` \___ \
| |_| | |_) |  __/ | | |  _| (_| | (_| |___) |
 \___/| .__/ \___|_| |_|_|  \__,_|\__,_|____/
      |_|


Function created in folder: hello-openfaas
Stack file written: hello-openfaas.yml

Notes:
You have created a Python3 function using the Classic Watchdog.

To include third-party dependencies create a requirements.txt file.

For high-throughput applications, we recommend using the python3-flask
or python3-http templates.
```

Run
```
faas-cli up -f hello-openfaas.yml
```

```
faas-cli new --lang python3 hello-python --prefix="tribuitrb"

faas-cli up -f hello-python.yml
```

# Ref

https://github.com/openfaas/of-watchdog/blob/master/README.md