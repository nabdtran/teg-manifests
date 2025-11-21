# teg-manifests

## Repository Structure & Purpose

This repo contains three key files/folders for deploying Envoy Gateway with Helm:

1. **teg-envoy-gateway-manifest.yaml**
	- This is the full Kubernetes manifest generated from the Helm chart. You can apply it directly with `kubectl apply -f teg-envoy-gateway-manifest.yaml`.
	- Useful for GitOps, review, or environments where Helm is not available.

2. **teg-envoy-gateway-helm/**
	- This is the unpacked Helm chart directory. It contains all templates, example values, and chart metadata.
	- Use this to customize deployments, update values, or template new manifests with `helm template`.

3. **values.yaml**
	- The values file used for templating the chart. Edit this to change configuration before rendering manifests.
	- Allows you to generate custom manifests for different environments.

**Workflow:**
- Edit `values.yaml` as needed.
- Use `helm template` with the chart and values to generate a manifest.
- Apply the manifest with `kubectl apply -f ...`.
# teg-manifests
