# konfi-infra
![Argocd Badge](https://argocd.denic0la.ch/api/badge?name=konfi&revision=true&showAppName=true)
The Infrastructure as Code (IaC) repository for the Konfi project.
Uses [Kustomize](https://kustomize.io/) to manage Kubernetes manifests.

## Self-Hosting
Selfhosting is possible but not recommended. 
The Project is running on [konfi.denic0la.ch](https://konfi.denic0la.ch/) and free without stealing or selling any of your data.
To Selfhost you need to build the konfi-ui/Dockerfile and konfi-back/Dockerfile since they both are on private registries
