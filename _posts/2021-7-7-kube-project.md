---
layout: post
author: bagnaram
title: "Kube Sticky Project"
date: 2021-7-7
published: true
---

One of the main things I missed going from RedHat Openshift to vanilla
Kubernetes is the concept of switching projects. An Openshift project is simply
a context associated with a particular namespace. However projects/namespaces
can be switched and all subsequent commands will inherit that namespace scope.
This saves me the trouble of attaching `-n namespace` to each and every command.
I decided to write a quick and dirty ZSH plugin to take care of this by adding a
`kubectl project` command.

Getting the current project.

```text
kubectl project
Current project: default
Usage: _kcl project <namespace>
```

```text
kubectl get pods
No resources found in default namespace.
```

Switching project
```text
kubectl project test
Set current project to test
```

All subsequent commands inherit the project's namespace.
```text
kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
test-fddbfcd5c-kjmvk              1/1     Running   1          13m
```

The plugin that can be added to your shell init.
```bash
function _kcl() {
  if [[ -z "$1" && -z "$2" ]]; then
    \kubectl -n $KUBESPACE "$@"
    return 0
  fi
  if [[ ! -z "$1" && "$1" == "project" && -z "$2" ]]; then
      echo "Current project: $KUBESPACE"
      echo "Usage: $0 project <namespace>"
      return 1
  fi
  if [[ ! -z "$1"  && "$1" == "project" && ! -z $2 ]]; then
    export KUBESPACE="$2"
    echo "Set current project to $KUBESPACE"
    return 0
  else
    \kubectl -n $KUBESPACE "$@"
    return 0
  fi
}
alias kubectl='_kcl'
```
