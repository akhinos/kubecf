
### Set the system_domain

#### When using Minikube

```sh
echo "system_domain: $(minikube ip).xip.io" \
  > "$(bazel info workspace)/dev/scf/system_domain_values.yaml"
```
