
### Set the system_domain

#### When using Kind

```sh
echo "system_domain: scf.suse.dev" \
  > "$(bazel info workspace)/dev/scf/system_domain_values.yaml"
```
