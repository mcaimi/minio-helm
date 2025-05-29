# MinIO Helm Chart

Deploy a minimal instance of MinIO Object Storage software for demo/training purposes.

Currently supports:

- Single-instance deployment (no HA yet)
- Vanilla Kubernetes or Openshift
- Persistent Storage

## Important

Since the release of MinIO RELEASE.2025-05-24T17-08-30Z, the web console only supports basic Object Browsing capabilites. To manage users and policies unfortunately you now need to use the `mc admin` command line tool.

## TODO

- Better support ArgoCD for deployments
- HA

