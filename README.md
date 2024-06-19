# Open Zaak charts

This repository contains a Helm chart for [Open Zaak](https://github.com/open-zaak).

View the detailed installation instructions and configuration here:

- [Open Zaak](./charts/open-zaak/README.md)
- [Open Notificaties](./charts/open-notificaties/README.md)

## TLDR Example
### Installation
Add the Helm repository, update it, get example values files.
```bash
helm repo add  fundaments-open-zaak  https://fundaments.github.io/open-zaak-charts/
helm repo update  fundaments-open-zaak
wget https://raw.githubusercontent.com/fundaments/open-zaak-charts/main/examples/openzaak_values.yaml
wget https://raw.githubusercontent.com/fundaments/open-zaak-charts/main/examples/notificaties_values.yaml
```
Update the values files with your own values.
You may need to add `ingress.className`.

Install the charts:
```bash
helm install  --debug  --wait  --namespace open-notificaties  --create-namespace  --values notificaties_values.yaml  open-notificaties  fundaments-open-zaak/open-notificaties
helm install  --debug  --wait  --namespace open-zaak          --create-namespace  --values openzaak_values.yaml      open-zaak          fundaments-open-zaak/open-zaak
```
Check if the configuration is correct:
- https://open-notificaties.example.com/view-config/
- https://open-zaak.example.com/view-config/

Check if you can login to the admin interface (username: `admin`, password from values files):
- https://open-zaak.example.com/admin/
- https://open-notificaties.example.com/admin/

### Uninstallation
```bash
helm uninstall  --namespace open-zaak  open-zaak
kubectl delete  --namespace=open-zaak          pvc  -l app.kubernetes.io/instance=open-zaak
kubectl delete  namespace  open-zaak       
helm uninstall  --namespace open-notificaties  open-notificaties
kubectl delete  --namespace=open-notificaties  pvc  -l app.kubernetes.io/instance=open-notificaties
kubectl delete  namespace  open-notificaties
```
