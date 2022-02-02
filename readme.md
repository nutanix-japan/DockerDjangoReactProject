# Sample Application with Postgres Backend

This is a sample app to showcase use of Postgres database deployed by Nutanix.

All ideas are from this [blog post](https://www.datagraphi.com/blog/post/2021/2/10/kubernetes-guide-deploying-a-machine-learning-app-built-with-django-react-and-postgresql-using-kubernetes).

We modified some parts of implementation yaml, docker repos, Ingress configuration and OpenShift routes to deploy on Openshift on Nutanix.

## Note

- Ingress does not work in Single Node OCP Cluster - still checking why - working around by creating OCP routes resource
- iSCSI drivers do not work in Single Node OCP - see this Nutanix [technote](https://portal.nutanix.com/page/documents/kbs/details?targetId=kA07V000000LWXJSA4) for fix. 