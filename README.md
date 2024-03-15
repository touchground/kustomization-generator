# kustomization-generator
Generates Kustomization base and overlay folders and files structure

## Requirements:
- yq - v4.42.1
- kustomize - v5.3.0

## Inputs:
* <b>base_path</b>: [Required] base folder where contains basic k8s manifest files.
* <b>environments</b>: The environments to create overlays for. Comma-delimited string. Example: dev,staging,prod'

others are not required.

## Usage
```yaml
on:
  workflow_dispatch:

jobs:
  copy-commit:
    runs-on: ubuntu-latest

    steps:
      - uses: touchground/kustomization-generator@main
        with:
          base_path: './k8s/base'
          environments: 'dev,staging,prod'
          namespace: "default"
          labels: "app=nginx,env=dev
```

## Folders and files structure
```bash
├── base
│   ├── configmap.yaml 
│   ├── deployment.yaml
│   ├── kustomization.yaml      <= Generated
│   └── service.yaml
└── overlays
    ├── dev
    │   └── kustomization.yaml  <= Generated
    └── prod
        └── kustomization.yaml  <= Generated
```

