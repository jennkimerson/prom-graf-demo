# prom-graf-demo

A basic set of CRDs that set up Prometheus and Grafana in OpenShift, along with persistent storage. It assumes:

* You are logged in to an OCP4 cluster
* You have a copy of `oc`
* There is a namespace called `ceph-build-metrics` on the OCP cluster

While it's possible to call `oc create -f <file>` on each CRD individually, a simple Python tool is provided to help you combine multiple CRDs into a single document. The tool will exclude the `PersistentVolumeClaim`s by default.

To create all resources on the cluster:

    ./combine_crds.py > all.yml
    oc create -f ./all.yml

To delete all resources - except the storage - from the cluster:

    ./combine_crds.py -p > all_but_pvcs.yml
    oc delete -f ./all_but_pvcs.yml

To delete _everything_:

    oc delete -f ./all.yml
