# Project Guidelines: konfi-infra

## Project Overview
`konfi-infra` is a Kubernetes infrastructure repository that uses **Kustomize** to manage deployments across different environments (stages).

### Project Structure
- `base/`: Contains the core Kubernetes resource definitions.
  - `back/`: Backend deployment and service.
  - `ui/`: Frontend (UI) deployment and service.
  - `database/`: MySQL database deployment, service, and PVC.
  - `nginx/`: Nginx reverse proxy configuration and deployment.
- `stages/`: Contains environment-specific overlays.
  - `dev/`: Development environment configurations, including ingress, configmaps, and patches (e.g., scaling down all deployments).
  - `prod/`: Production environment configurations.
- `spec/`: Contains project specifications (e.g., `Brunch.yaml`).

### Deployment Strategy
The project follows a "base and overlay" pattern. The `base/kustomization.yaml` aggregates all core components, which are then referenced and modified by overlays in the `stages/` directory.

### Development Guidelines
- Always use Kustomize patches for environment-specific changes.
- For global patches (applying to all resources of a kind), prefer JSON patches (`- op: add, path: ...`) over Strategic Merge Patches to avoid name mismatch issues.
- The `dev` environment is automatically scaled down to not waste compute via GitHub Actions `.github/workflows/weekly-scale-down.yml``). These workflows toggle the `patch-stop-all.yaml` patch in `stages/dev/kustomization.yaml`.
- Ensure that any new components are added to the `base/` directory and referenced in the relevant `kustomization.yaml` files.
- Secrets are managed via `SealedSecrets` in some environments (e.g., `stages/dev/sealedsecret_database-config.yaml`).
