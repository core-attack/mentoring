# CI/CD

# DEV

```
gcloud container clusters get-credentials your_company-staging-cluster --region=us-central1-c

kubectl create namespace your_company-dev

kubectl delete secret your_company-api-dev-config -n your_company-dev
kubectl create secret generic your_company-api-dev-config --from-file=appsettings.secrets.json --dry-run=client -o yaml | kubectl apply -f - -n your_company-dev
kubectl rollout restart deployment your_company-api-dev-deployment -n your_company-dev

kubectl delete secret your_company-filter-worker-dev-config -n your_company-dev
kubectl create secret generic your_company-filter-worker-dev-config  --from-file=your_company-filters-worker-secrets.json --dry-run=client -o yaml | kubectl apply -f - -n your_company-dev

kubectl delete secret your_company-events-api-dev-config -n your_company-events-dev
kubectl create secret generic your_company-events-api-dev-config --from-file=appsettings.secrets.json --dry-run=client -o yaml | kubectl apply -f - -n your_company-events-dev
kubectl rollout restart deployment your_company-events-api-dev-deployment -n your_company-events-dev
```

# add role
```
gcloud iam roles create StorageObjectsCreateRole \
    --project your_project \
    --title "storage.objects.create permission" \
    --description "Grants storage.objects.create permission" \
    --permissions storage.objects.create

gcloud iam roles create ContainerClusterRolesCreate \
    --project your_project \
    --title "Container Cluster Roles Create" \
    --description "This role allows to debug pod and has only the container.clusterRoles.create permission" \
    --permissions container.clusterRoles.create

gcloud iam roles create ContainerClusterRolesUpdate \
    --project your_project \
    --title "Container Cluster Roles Update" \
    --description "This role allows to debug pod and has only the container.clusterRoles.update permission" \
    --permissions container.clusterRoles.update

gcloud iam roles create ContainerClusterRoleBindingsCreate \
    --project your_project \
    --title "Container ClusterRoleBindings Create" \
    --description "This role allows to debug pod and has only the container.clusterRoleBindings.create permission" \
    --permissions container.clusterRoleBindings.create

gcloud iam roles create ContainerClusterRoleBindingsUpdate \
    --project your_project \
    --title "Container ClusterRoleBindings Update" \
    --description "This role allows to debug pod and has only the container.clusterRoleBindings.update permission" \
    --permissions container.clusterRoleBindings.update

gcloud iam roles create StorageObjectsCreateRole \
    --project refundkeeper \
    --title "storage.objects.create permission" \
    --description "Grants storage.objects.create permission" \
    --permissions storage.objects.create

gcloud iam roles create ContainerClusterRolesCreate \
    --project refundkeeper \
    --title "Container Cluster Roles Create" \
    --description "This role allows to debug pod and has only the container.clusterRoles.create permission" \
    --permissions container.clusterRoles.create

gcloud iam roles create ContainerClusterRolesUpdate \
    --project refundkeeper \
    --title "Container Cluster Roles Update" \
    --description "This role allows to debug pod and has only the container.clusterRoles.update permission" \
    --permissions container.clusterRoles.update

gcloud iam roles create ContainerClusterRoleBindingsCreate \
    --project refundkeeper \
    --title "Container ClusterRoleBindings Create" \
    --description "This role allows to debug pod and has only the container.clusterRoleBindings.create permission" \
    --permissions container.clusterRoleBindings.create

gcloud iam roles create ContainerClusterRoleBindingsUpdate \
    --project refundkeeper \
    --title "Container ClusterRoleBindings Update" \
    --description "This role allows to debug pod and has only the container.clusterRoleBindings.update permission" \
    --permissions container.clusterRoleBindings.update
```

# check managed certificate status
```
kubectl describe managedcertificate your_company-api-demo-managed-certificate -n your_namespace
```

# delete managed certificate status
```
kubectl delete managedcertificate your_company-api-demo-managed-certificate -n your_namespace
```

