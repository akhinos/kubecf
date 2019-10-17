# Foundation: Kube: GKE (Google Kubernetes Engine)

At least for Diego we need a node OS with XFS support.

The `--image-type UBUNTU` selects an OS with XFS support.

Create the cluster like this:

```
project="scfv3"
clustername="scfv3-test"
scopes="https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append"
gcloud beta container --project "$project" clusters create "$clustername" \
      --zone "europe-west4-a" \
      --no-enable-basic-auth \
      --cluster-version "1.12.8-gke.10" \
      --machine-type "custom-6-13312" \
      --image-type "UBUNTU" \
      --disk-type "pd-standard" \
      --disk-size "100" \
      --metadata disable-legacy-endpoints=true \
      --scopes "$scopes" \
      --preemptible \
      --num-nodes "1" \
      --enable-cloud-logging \
      --enable-cloud-monitoring \
      --enable-ip-alias \
      --network "projects/$project/global/networks/default" \
      --subnetwork "projects/$project/regions/europe-west4/subnetworks/default" \
      --default-max-pods-per-node "110" \
      --addons HorizontalPodAutoscaling,HttpLoadBalancing \
      --enable-autoupgrade \
      --enable-autorepair \
      --no-shielded-integrity-monitoring
```
