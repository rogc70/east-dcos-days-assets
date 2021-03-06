## Lab 7 - Scaling to More Nodes

Sometimes you need more Kubernetes infrastructure to run more applications. DC/OS can easily scale the cluster. 

There are several ways to scale Kubernetes in DC/OS. 

## From the UI

From the UI, go to Services > Kubernetes and choose "Edit" in top right. 

Under "kubernetes" in left hand menu, change the number of "node count" to 2 and the "public node count" to 1


![](https://i.imgur.com/0YJxn1r.png)

## From the CLI

Export the current package configuration into a JSON file called config.json

```
$ dcos kubernetes cluster  describe --cluster-name=kubernetes-cluster1 | grep -v '^Using' > config.json

```

Use an editor such as vi to change the config file and update "node_count" and "public node count"
to the new number of nodes

```
"kubernetes": {
    "cloud_provider": "(none)",
    "high_availability": true,
    "network_provider": "dcos",
    "node_count": 2,
    "public_node_count": 1,
    "reserved_resources": {
      "kube_cpus": 2,
      "kube_disk": 10240,
      "kube_mem": 2048,
      "system_cpus": 1,
      "system_mem": 1024
    }
```

Scale the cluster 

```
dcos kubernetes update --options=config.json
```
