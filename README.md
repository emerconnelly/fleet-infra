# fleet-infra

My homelab infra, with horrible commit messages.

## hardware

### network

### servers

[Talos Linux](https://www.talos.dev/v1.7/introduction/what-is-talos) bare-metal [Kubernetes](https://kubernetes.io/docs/concepts/overview) cluster running on mini-desktop PCs. Cheap and simple, unlike my ex.

- 3 control-plane nodes
  - Dell 9020 Optiplex Micro
  - CPU: [Intel i7-4785T 4-core 3.2GHz 8M Cache](https://www.intel.com/content/www/us/en/products/sku/80814/intel-core-i74785t-processor-8m-cache-up-to-3-20-ghz/specifications.html)
  - RAM: [Crucial 8GB DDR3 1600 CL11](https://eu.crucial.com/memory/ddr3/ct102464bf160b)
  - Storage
    - 256GB M.2 SSD
    - [Crucial MX500 2TB SATA SSD](https://www.crucial.com/ssd/mx500/ct2000mx500ssd1)
- 1 worker node
  - [Intel NUC10I5FNKN1](https://mitxpc.com/products/bxnuc10i5fnkn1)
  - CPU: [Intel i5-10210U 4-core 4.2GHz 6M Cache](https://www.intel.com/content/www/us/en/products/sku/195436/intel-core-i510210u-processor-6m-cache-up-to-4-20-ghz/specifications.html)
  - RAM: [Samsung 64GB DDR4 2666 CL19](https://semiconductor.samsung.com/us/dram/module/sodimm/m471a4g43mb1-ctd)
  - Storage: 256GB M.2 NVMe SSD

## repository management

### Renovate [![Renovate Dashboard](https://img.shields.io/badge/Dashboard-555?logo=renovate&logoColor=497b9c&labelColor=000)](https://developer.mend.io/github/emerconnelly/fleet-infra)

- Automatically creates detailed PRs for new versions of Flux `HelmRelease`s, container image tags, & K8s `.yaml` resources
- Configured as a [GitHub app](https://github.com/apps/renovate) (migrate to GitHub Action cause it looks cooler?)

## k8s external

### Cloudflare [![Cloudflare DNS Records](https://img.shields.io/badge/DNS_Records-555?logo=cloudflare&logoColor=f38020&labelColor=000)](https://dash.cloudflare.com/923309f860b1a7e801fd81224c5f56c9/emerconnelly.com/dns/records) [![Cloudflare Audit Log](https://img.shields.io/badge/Audit_Log-555?logo=cloudflare&logoColor=f38020&labelColor=000)](https://dash.cloudflare.com/923309f860b1a7e801fd81224c5f56c9/audit-log) [![Cloudflare API Tokens](https://img.shields.io/badge/API_Tokens-555?logo=cloudflare&logoColor=f38020&labelColor=000)](https://dash.cloudflare.com/profile/api-tokens)

- Automated HTTPS cert lifecycle using [`cert-manager`](https://cert-manager.io/docs/installation/helm)'s [ACME DNS01 Challenge Provider](https://cert-manager.io/docs/configuration/acme/dns01) via [Let's Encrypt](https://letsencrypt.org) with my domain [emerconnelly.com](https://www.emerconnelly.com)

### Tailscale [![Tailscale Machines](https://img.shields.io/badge/Machines-555?logo=tailscale&logoColor=fff&labelColor=242424)](https://login.tailscale.com/admin/machines) [![Tailscale ACL Editor](https://img.shields.io/badge/ACL_Editor-555?logo=tailscale&logoColor=fff&labelColor=242424)](https://login.tailscale.com/admin/machines)

- Secure external access by exposing ingress, egress, & the K8s API to my [tailnet](https://tailscale.com/kb/1136/tailnet)
- Controlled via [`tailscale-operator`](https://tailscale.com/kb/1236/kubernetes-operator)

### HCP Vault Secrets [![HCP Vault Secrets](https://img.shields.io/badge/Vault_Secrets-555?logo=hashicorp&logoColor=fff&labelColor=000)](https://portal.cloud.hashicorp.com/services/secrets?project_id=c9dc34a9-87d7-4e2d-9a1c-3d3e759f8261)

- Cloud-based secrets manager
- Controlled via [`vault-secrets-operator`](https://github.com/hashicorp/vault-secrets-operator)

## k8s internal

### Kubernetes Dashboard [![Kubernetes Dashboard](https://img.shields.io/badge/Dashboard-555?logo=kubernetes&logoColor=326ce5&labelColor=000)](https://k8s-dashboard.homelab.emerconnelly.com)

- K8s web UI & resource explorer

### Headlamp [![Headlamp Main](https://img.shields.io/badge/Main-555)](https://headlamp.homelab.emerconnelly.com/c/main)

- K8s web UI & resource explorer

### OpenObserve [![OpenObserve Home](https://img.shields.io/badge/Home-555)](https://openobserve.homelab.emerconnelly.com/web)

- Full-stack observability (logs, traces, metrics), ~71:1 compression ratio, & a web UI for queries & dashboards

### Prometheus [![Prometheus Targets](https://img.shields.io/badge/Targets-555?logo=prometheus&logoColor=e6522c&labelColor=000)](https://prometheus.homelab.emerconnelly.com/targets)

- Time-series database for collecting & alterting on application & infrastructure metrics
- Deployed via `kube-prometheus-stack`

### Grafana [![Grafana Dashboards](https://img.shields.io/badge/Dashboards-555?logo=grafana&logoColor=f46800&labelColor=000)](https://grafana.homelab.emerconnelly.com/dashboards)

- Visualize metrics, logs, & traces from multiple sources
- Deployed via `kube-prometheus-stack`

### Cilium

- K8s CNI utilizing eBPF, & `kube-proxy` replacement
- K8s K8s Ingress & Gateway API controller
- Load balancer via L2 advertisments using gratuitous ARP 

#### Cilium Hubble [![Cilium Hubble](https://img.shields.io/badge/Hubble-555?logo=cilium&logoColor=f9c31f&labelColor=000)](https://hubble.homelab.emerconnelly.com)

- Visual map & event log of the Cilium CNI

### Traefik [![Traefik Dashboard](https://img.shields.io/badge/Dashboard-555?logo=traefikproxy&logoColor=24a1c1&labelColor=000)](https://traefik.homelab.emerconnelly.com/dashboard/)

- K8s Ingress & Gateway API controller

### MinIO [![MinIO Main Tenant](https://img.shields.io/badge/Main_Tenant-555?logo=minio&logoColor=c72e49&labelColor=000)](https://main.minio.homelab.emerconnelly.com)

- Deploy highly-available & fully API-compliant S3 storage tenants
- Controlled via [`minio-operator`](https://min.io/docs/minio/kubernetes/upstream/operations/installation.html)
