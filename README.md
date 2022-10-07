# Sample Application with Postgres Backend

This is a sample app to showcase use of Postgres database deployed by Nutanix.

All ideas are from this [blog post](https://www.datagraphi.com/blog/post/2021/2/10/kubernetes-guide-deploying-a-machine-learning-app-built-with-django-react-and-postgresql-using-kubernetes).

We modified some parts of implementation yaml, docker repos, Ingress configuration and OpenShift routes to deploy on Openshift on Nutanix.

## Note

- Ingress does not work in Single Node OCP Cluster - still checking why - working around by creating OCP routes resource
- iSCSI drivers do not work in Single Node OCP - see this Nutanix [technote](https://portal.nutanix.com/page/documents/kbs/details?targetId=kA07V000000LWXJSA4) for fix. 

## Implementation

```bash
   oc create ns era-demo
   oc apply -f k8s/app_secrets.yaml  ## create app password as kubernetes secrets
   oc apply -f k8s/app_variables.yaml  ## create database and app connectivity paramets
   oc apply -f k8s/pg_service.yaml   ## create ExternalName service reference to operator deployed Era VM
   oc apply -f k8s/job_django.yaml   ## create table, run migrations, etc
   oc apply -f k8s/component_django.yaml ## create backend django app
   oc apply -f k8s/component_react.yaml  ## create frontend react app
   oc apply -f k8s/ingress_service.yaml  ## create ingress if your OCP cluster has a working Ingress
   oc apply -f k8s/routes.yaml           ## if you OCP cluster has no ingress, just create routess
```
