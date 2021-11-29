# tanzu-packages-on-vSphere-with-Tanzu

## Install kapp controller

Install KAPP on the workload cluster using the documentation or use a command similar to install the latest version

```
kubectl apply -f https://github.com/vmware-tanzu/carvel-kapp-controller/releases/download/v0.30.0/release.yml
```

## Install Tanzu Package repository

```
kubectl create ns tanzu-standard
tanzu package repository add tanzu-standard --url projects.registry.vmware.com/tkg/packages/standard/repo:v1.4.0 -n tanzu-standard
tanzu package repository list -n tanzu-standard
tanzu package repository get tanzu-standard -n tanzu-standard
```

## Install Tanzu package - cert-manager

```
tanzu package available list -n tanzu-standard
tanzu package available list cert-manager.tanzu.vmware.com -n tanzu-standard
tanzu package available get cert-manager.tanzu.vmware.com/1.1.0+vmware.1-tkg.2 -n tanzu-standard
tanzu package install cert-manager -p cert-manager.tanzu.vmware.com -v 1.1.0+vmware.1-tkg.2 -n tanzu-standard
# Validate cert-manager is successfully running
tanzu package installed list -n tanzu-standard
kubectl get pods -A
```

## Install Tanzu package - Contour

```
tanzu package available list contour.tanzu.vmware.com -n tanzu-standard
tanzu package install contour -p contour.tanzu.vmware.com -v 1.17.1+vmware.1-tkg.1 --values-file contour-data-values.yaml -n tanzu-standard
# Validate Contour pod(s) are successfully running
tanzu package installed list -n tanzu-standard
kubectl get pods -A
```

## Install Tanzu package - Multus (optional) 

```
tanzu package available list multus-cni.tanzu.vmware.com -n tanzu-standard
tanzu package available get multus-cni.tanzu.vmware.com/3.7.1+vmware.1-tkg.1 -n tanzu-standard
tanzu package install multus-cni -p multus-cni.tanzu.vmware.com -v 3.7.1+vmware.1-tkg.1 --values-file multus-data-values.yaml -n tanzu-standard
# Validate Multus pods(s) are successfully running
tanzu package installed list -n tanzu-standard
kubectl get pods -A
```

## Install Tanzu package - Prometheus

```
tanzu package available list grafana.tanzu.vmware.com -n tanzu-standard
tanzu package install grafana -p grafana.tanzu.vmware.com -v 7.5.7+vmware.1-tkg.1 --values-file prometheus-data-values.yaml -n tanzu-standard
# Validate Prometheus pods(s) are successfully running
tanzu package installed list -n tanzu-standard
kubectl get pods -A
```

## Install Tanzu package - Grafana 

```
tanzu package available list grafana.tanzu.vmware.com -n tanzu-standard
tanzu package install prometheus -p prometheus.tanzu.vmware.com -v 2.27.0+vmware.1-tkg.1 --values-file grafana-data-values.yaml -n tanzu-standard
# Validate Grafana pods(s) are successfully running
tanzu package installed list -n tanzu-standard
kubectl get pods -A
```
