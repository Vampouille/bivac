# Bivac Openshift Teamplate
Template to install bivac in openshift without helm

* Install template:
```bash
oc create -f bivac-template.yaml
```
* Instanciate template:
```bash
oc process bivac \
  -p SCHEDULE="0 2 * * *" \
  -p BIVAC_TARGET_URL=s3:s3.amazonaws.com/<BUCKET NAME> \
  -p AWS_ACCESS_KEY_ID=<AWS ACCESS KEY> \
  -p AWS_SECRET_ACCESS_KEY=<AWS SECRET KEY> \
  -p RESTIC_PASSWORD=<RESTIC PASSWORD> \
  -p K8S_WORKER_SERVICE_ACCOUNT=default \
  -p NAMESPACE=<OPENSHIFT NAMESPACE> | oc create -f -
```
* Delete cronjob:
```bash
oc delete cronjob bivac
oc delete rolebinding bivac
oc delete role bivac
oc delete serviceaccount bivac
```
* Delete template:
```bash
oc delete template bivac
```
