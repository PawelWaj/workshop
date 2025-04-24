# workshop
# ${{values.appName}}

${{values.appDescription}}

## Kubernetes Application

This application was created using the Backstage Kubernetes Application Template. 

## Deployment

The Kubernetes manifests are located in the `k8s` directory and will be deployed by ArgoCD.

## Configuration

- Application Name: ${{values.appName}}
- Team: ${{values.teamName}}
- Container Image: ${{values.image}}
- Replicas: ${{values.replicas}}
- Custom Label: ${{values.customLabel}}