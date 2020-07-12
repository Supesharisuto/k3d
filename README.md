# Install MongoDB

```
$ ark install mongodb
Using kubeconfig: /Users/anthonyhathuc/.kube/config
Node architecture: "amd64"
Client: "x86_64", "Darwin"
2020/07/12 10:35:52 User dir established as: /Users/anthonyhathuc/.arkade/
"stable" has been added to your repositories

VALUES values.yaml
Command: /Users/anthonyhathuc/.arkade/bin/helm3/helm [upgrade --install mongodb stable/mongodb --namespace default --values /var/folders/jk/p28yy1kn2yl6zqmzgj58tgd40000gn/T/charts/mongodb/values.yaml --set persistence.enabled=false]
Release "mongodb" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: mongodb
LAST DEPLOYED: Sun Jul 12 10:36:01 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
This Helm chart is deprecated

Given the `stable` deprecation timeline (https://github.com/helm/charts#deprecation-timeline), the Bitnami maintained Helm chart is now located at bitnami/charts (https://github.com/bitnami/charts/).

The Bitnami repository is already included in the Hubs and we will continue providing the same cadence of updates, support, etc that we've been keeping here these years. Installation instructions are very similar, just adding the _bitnami_ repo and using it during the installation (`bitnami/<chart>` instead of `stable/<chart>`)

```

```bash
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm install my-release bitnami/<chart>           # Helm 3
$ helm install --name my-release bitnami/<chart>    # Helm 2
```

To update an exisiting _stable_ deployment with a chart hosted in the bitnami repository you can execute

```bash
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm upgrade my-release bitnami/<chart>
```

Issues and PRs related to the chart itself will be redirected to `bitnami/charts` GitHub repository. In the same way, we'll be happy to answer questions related to this migration process in this issue (https://github.com/helm/charts/issues/20969) created as a common place for discussion.

** Please be patient while the chart is being deployed **

MongoDB can be accessed via port 27017 on the following DNS name from within your cluster:

    mongodb.default.svc.cluster.local

To get the root password run:

    export MONGODB_ROOT_PASSWORD=$(kubectl get secret --namespace default mongodb -o jsonpath="{.data.mongodb-root-password}" | base64 --decode)

To connect to your database run the following command:

    kubectl run --namespace default mongodb-client --rm --tty -i --restart='Never' --image docker.io/bitnami/mongodb:4.2.4-debian-10-r0 --command -- mongo admin --host mongodb --authenticationDatabase admin -u root -p $MONGODB_ROOT_PASSWORD

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace default svc/mongodb 27017:27017 &
    mongo --host 127.0.0.1 --authenticationDatabase admin -p $MONGODB_ROOT_PASSWORD
=======================================================================
=                  MongoDB has been installed.                        =
=======================================================================

