# Google CloudDNS Provider

This DNS provider allows you to create and manage DNS entries in [Google CloudDNS](https://cloud.google.com/dns). 

## Generate Service Account

You need to provide a service account key with sufficient permissions for CloudDNS.
For details how to create a service account key see https://cloud.google.com/iam/docs/creating-managing-service-account-keys. 

## Required permissions

The user needs permissions on the managed zone to list and change DNS records.
The easiest way is assign the Cloud DNS API IAM role `roles/dns.admin` to the
service account. In the GCP Console the role is named `DNS Administrator`.
For more details see https://cloud.google.com/dns/docs/access-control.

## Using the service account key

Create a `Secret` resource with the data field `serviceaccount.json`.
The value is the base64 encoded content of the JSON file the source account key.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: google-credentials
  namespace: default
type: Opaque
data:
  # replace '...' with json key from service account creation (encoded as base64)
  # see https://cloud.google.com/iam/docs/creating-managing-service-accounts
  serviceaccount.json: ...
``` 