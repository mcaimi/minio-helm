# MinIO Helm Chart

Deploy a minimal instance of MinIO Object Storage software for demo/training purposes.

Currently supports:

- Single-instance deployment (no HA yet)
- Vanilla Kubernetes or Openshift
- Persistent Storage

## Important

Since the release of MinIO RELEASE.2025-05-24T17-08-30Z, the web console only supports basic Object Browsing capabilites. To manage users and policies unfortunately you now need to use the `mc admin` command line tool.

```bash
# Add admin credentials to the alias registry
$ mc alias rm local
$ mc alias set local root <root password set in values.yaml>

# create a new user
$ mc admin user add local <random access key> <random secret key>
# apply a policy
$ mc admin policy attach readwrite --user <user access key>
```

### Bucket-scoped permissions

To limit access from users to specific buckets, MinIO supports dedicated policies.

For example:

1- The user "developer" has been created
2- The bucket "pipelines" is available in the server

Create this custom policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetBucketLocation"
      ],
      "Resource": [
        "arn:aws:s3:::pipelines"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": [
        "arn:aws:s3:::pipelines/*"
      ]
    }
  ]
}
```

And attach it to the user handle:

```bash
$ mc admin policy create local pipelines-rw-access policy-file.json
$ mc admin policy attach local pipelines-rw-access --user developer
```

## TODO

- Better support ArgoCD for deployments
- HA

