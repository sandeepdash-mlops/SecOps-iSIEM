<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a2332,100:2496ED&height=200&section=header&text=i-SIEM%20Containers&fontSize=70&fontColor=ffffff&fontAlignY=38&desc=Custom%20Docker%20Images%20for%20the%20i-SIEM%20Platform&descAlignY=58&descSize=20&descColor=90caf9" alt="i-SIEM Docker Banner"/>

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![Wazuh](https://img.shields.io/badge/Wazuh_Based-005571?style=for-the-badge&logo=wazuh&logoColor=white)](https://wazuh.com/)
[![OpenSearch](https://img.shields.io/badge/OpenSearch-005EB8?style=for-the-badge&logo=opensearch&logoColor=white)](https://opensearch.org/)
[![Docker Compose](https://img.shields.io/badge/Docker_Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docs.docker.com/compose/)
[![License](https://img.shields.io/badge/License-Open_Source-green?style=for-the-badge)](https://opensource.org/licenses)

</div>

---

## 🐳 What is this?

This repository contains **custom-built Docker images** for the i-SIEM platform — a self-hosted, in-house SIEM solution built on top of Wazuh.

Rather than using stock, off-the-shelf images, these images are **locally modified and rebuilt** from the original Wazuh Docker images to reflect i-SIEM's branding, configuration, and deployment requirements. This gives complete control over every layer of the container stack — from the base image to the final runtime configuration.

The images cover all three core components of the i-SIEM platform and are designed to deploy seamlessly into both **Kubernetes environments** and **Docker Compose** setups for local testing.

---

## 🎯 Why Custom Images?

Using vendor-provided images out of the box means accepting their defaults — their configurations, their branding, their constraints. Building custom images means:

- 🔧 **Full control** over configuration baked into the image at build time
- 🎨 **i-SIEM branding** applied consistently across all components
- 🔒 **Security hardening** applied at the image layer, not just at runtime
- 📦 **Reproducible builds** — every deployment uses an identical, version-controlled image
- 🚫 **No dependency on external registries** — images built and stored locally

---

## ⚙️ Components

| Component | Base | Role |
|---|---|---|
| **i-SIEM Manager** | Wazuh Manager | Core event processing, rule engine, alert generation |
| **i-SIEM Indexer** | OpenSearch | Log indexing, full-text search, data persistence |
| **i-SIEM Dashboard** | OpenSearch Dashboards | Web UI, visualizations, security monitoring interface |

All three images are built locally and work together as a unified stack.

---

## 🧰 Tech Stack

| Domain | Technologies |
|---|---|
| Containerization | Docker, Docker Compose |
| Orchestration | Kubernetes (primary), Docker Compose (local/dev) |
| SIEM Engine | Wazuh (customized — i-SIEM) |
| Search & Indexing | OpenSearch |
| Visualization | OpenSearch Dashboards (i-SIEM branded) |
| Image Build | Custom Dockerfiles, local build scripts |

---

## 💡 Key Engineering Decisions

- **Local image builds** — no external registry dependency; full supply chain control
- **Single build script** to build all three components in the correct order with consistent tagging
- **Docker Compose support** retained for fast local iteration before promoting to Kubernetes
- **Volume-backed persistence** so container restarts do not result in data loss
- **Multi-node ready** architecture — the indexer component supports horizontal scaling

---

## 🚀 Deployment Steps

### Prerequisites

Ensure the following are installed on your system before proceeding:
- Docker
- Docker Compose
- Linux environment (recommended)

---

### Step 1 — Build All Custom Images

Navigate to the build directory and run the build script:

```bash
cd isiem-docker/isiem-build-docker-images
./build-images.sh
```

This builds Docker images for all i-SIEM components on your local system.

Alternatively, build individual component images manually:

```bash
docker build -t isiem/manager ./manager
docker build -t isiem/indexer ./indexer
docker build -t isiem/dashboard ./dashboard
```

---

### Step 2 — Run the Stack

```bash
docker compose up -d
```

> **Note:** Docker Compose is recommended for local testing and development. For production use, deploy these images into a Kubernetes cluster using the manifests in the [SecOps-SIEM-Kubernetes](https://github.com/sandeepdash-mlops/SecOps-SIEM-Kubernetes) repository.

---

## 🔗 Related Repository

This image repository works hand-in-hand with the main deployment repository:

👉 **[SecOps-SIEM-Kubernetes](https://github.com/sandeepdash-mlops/SecOps-SIEM-Kubernetes)** — Kubernetes manifests, alert integrations, GCS log archival, and full on-premise SIEM deployment.

---

## 💬 Connect

If you found this project helpful or have any questions, feel free to reach out!

📧 **Email:** sandeepdashmlops@gmail.com

💻 **GitHub:** [github.com/sandeepdash-mlops](https://github.com/sandeepdash-mlops)

---

<div align="center">

*Custom-built images for engineers who want full ownership of every layer of their security stack.*

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2496ED,50:1a2332,100:0d1117&height=100&section=footer"/>

</div>
