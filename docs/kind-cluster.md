# KIND Cluster Setup

The testing pipeline is running in local kind cluster with registry and its dependencies like OLM, Tekton and others. The following steps must be performed
to prepare the kind clusters for use by the pipeline. 

## Prerequisites
The KIND Cluster Setup is done by `ansible`. One can to install `ansible` via 
```
$ pip3 install ansible
```
Then one has to install additional `ansible` collection `kubernetes.core` and its dependency python `kubernetes` package
```
$ pip3 install kubernetes
$ ansible-galaxy collection install kubernetes.core
```

## Kind Cluster Instllation

### Install
```
$ ansible-pull ansible/upstream-community.yaml \
  -U https://github.com/redhat-openshift-ecosystem/operator-pipelines.git \
  -C upstream-community-dev  \
  -i localhost, \
  --tags install \
  -e prerequisite=true \ 
  -e kind_cluster=true
```

### Verify installation
```
$ ansible-pull ansible/upstream-community.yaml \
  -U https://github.com/redhat-openshift-ecosystem/operator-pipelines.git \
  -C upstream-community-dev  \
  -i localhost, \
  --tags verify \
  -e prerequisite=true \ 
  -e kind_cluster=true
```

### Cleanup kind cluster

```
$ ansible-pull ansible/upstream-community.yaml \
  -U https://github.com/redhat-openshift-ecosystem/operator-pipelines.git \
  -C upstream-community-dev  \
  -i localhost, \
  --tags clean \
  -e prerequisite=false \
  -e kind_cluster=true
```

### Uninstall everything (prerequisite and Kind cluster)
```
$ ansible-pull ansible/upstream-community.yaml \
  -U https://github.com/redhat-openshift-ecosystem/operator-pipelines.git \
  -C upstream-community-dev  \
  -i localhost, \
  --tags clean \
  -e prerequisite=true \
  -e kind_cluster=true
```

### Destroy KIND cluster

```
$ ansible-pull ansible/upstream-community.yaml \
  -U https://github.com/redhat-openshift-ecosystem/operator-pipelines.git \
  -C upstream-community-dev  \
  -i localhost, \
  --tags kind_delete
```
