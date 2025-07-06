# NGINX Kubernetes Package with KPT and Kustomize

This project demonstrates how to manage, customize, and deploy Kubernetes resources using **KPT** and **Kustomize** together.

It includes:
- A `Kptfile` with mutators (to apply labels and namespaces) and validators
- A `kustomization.yaml` file to manage resources and apply JSON6902 patches

## 📁 Project Structure

.
├── Kptfile
├── kustomization.yaml
└── packages/
    ├── base/
    │   ├── nginx_deployment.yaml
    │   └── nginx_service.yaml
    └── ns/
        └── nginx_namespace.yaml

## ⚙️ Tools Used

**KPT**: for mutating and validating resources declaratively

**Kustomize**: for patching and managing overlays

**KRM Functions**:

**set-labels**: adds labels to resources

**set-namespace**: sets namespace on resources

**kubeval**: validates resource schema

## 🔁 Workflow

# 1. Render the KPT Pipeline
Apply KPT pipeline functions to mutate and validate your resource files:

kpt fn render

This runs the functions defined in the Kptfile, applying labels and namespaces.

# 2. Customize with Kustomize
Apply patches and combine resources with:

kustomize build .

**This command:**

Loads all YAMLs from the resources list

Applies patches to remove app1 and env labels/selectors

Adds common labels and namespace metadata

# 3. Apply to the Cluster
Apply the fully rendered manifests:

kpt live init ./packages
kpt live apply ./packages

# 4. Clean Up
To delete the applied resources from the cluster:

kpt live destroy ./packages

## ✅ Outcome
Kubernetes resources are standardized and validated using kpt

Patch-driven cleanup and customizations are managed by kustomize

The system is modular, reusable, and GitOps-ready


