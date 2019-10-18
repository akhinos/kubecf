
## Expose SCFv3

### GKE

Make the CF router available via a load balancer:

```
kubectl expose service -n scf scf-router-v1-0 --type=LoadBalancer --name=scf-router-lb
```

The load balancer's public IP should have these DNS records:

```
app1.scf.suse.dev
app2.scf.suse.dev
app3.scf.suse.dev
login.scf.suse.dev
api.scf.suse.dev
uaa.scf.suse.dev
doppler.scf.suse.dev
log-stream.scf.suse.dev
```

If you are testing locally and have no control over a DNS zone, you can enter host aliases in your `/etc/hosts`:

```
192.168.99.112 app1.scf.suse.dev app2.scf.suse.dev app3.scf.suse.dev login.scf.suse.dev api.scf.suse.dev uaa.scf.suse.dev doppler.scf.suse.dev log-stream.scf.suse.dev
```
