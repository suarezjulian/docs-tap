# Architecture

## <a id='yaml-files'></a>Working with yaml files

The Tanzu CLI apps plugin supports working with `yaml` files in which workloads are defined. However, it should be made clear that only one wokload is to be declared per file.

For example, a valid file would be like this:

```yaml
---
apiVersion: carto.run/v1alpha1
kind: Workload
metadata:
  name: spring-petclinic
  labels:
    app.kubernetes.io/part-of: spring-petclinic
    app.tanzu.vmware.com/workload-type: java
    apps.tanzu.vmware.com/workload-type: java
    app: webhook
spec:
  source:
    git:
      url: https://github.com/spring-projects/spring-petclinic
      ref:
        branch: main
```

And an invalid one would look like:

```yaml
---
apiVersion: carto.run/v1alpha1
kind: Workload
metadata:
  name: spring-petclinic
  labels:
    app.kubernetes.io/part-of: spring-petclinic
    app.tanzu.vmware.com/workload-type: java
    apps.tanzu.vmware.com/workload-type: java
    app: webhook
spec:
  source:
    git:
      url: https://github.com/spring-projects/spring-petclinic
      ref:
        branch: main

---
apiVersion: carto.run/v1alpha1
kind: Workload
metadata:
  name: spring-data-examples
  labels:
    app.kubernetes.io/part-of: spring-data-examples
    app.tanzu.vmware.com/workload-type: java
    apps.tanzu.vmware.com/workload-type: java
    app: webhook
spec:
  source:
    git:
      url: https://github.com/spring-projects/spring-data-examples
      ref:
        branch: main
```

## <a id='autocompletion'></a>Autocompletion

To enable command autocompletion, the Tanzu CLI offers the `tanzu completion` command.

Add the following command to the shell config file according to the current setup:

### Bash

```bash
tanzu completion bash >  $HOME/.tanzu/completion.bash.inc
```

### Zsh

```sh
echo "autoload -U compinit; compinit" >> ~/.zshrc
tanzu completion zsh > "${fpath[1]}/_tanzu"
```
