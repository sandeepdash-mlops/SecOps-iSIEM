# ISIEM Containers for Docker

![Docker](https://img.shields.io/badge/docker-supported-blue)
![Platform](https://img.shields.io/badge/platform-kubernetes-informational)
![License](https://img.shields.io/badge/license-open--source-green)

Slack • Email

---

## Description

The `isiem/isiem-docker` repository provides resources to deploy the **ISIEM cybersecurity platform** using Docker containers.

This setup enables easy installation and orchestration of the full **ISIEM stack**, including:

* **ISIEM Manager**
* **ISIEM Dashboard** (based on OpenSearch Dashboards)
* **OpenSearch Indexer** for indexing and search

These container images are **customized and built locally** by modifying the original Wazuh Docker images.

---

## Architecture

```
+--------------------+
|  ISIEM Dashboard   |
| (Web Interface)    |
+---------+----------+
          |
          v
+--------------------+
|  ISIEM Indexer     |
|   (OpenSearch)     |
+---------+----------+
          |
          v
+--------------------+
|  ISIEM Manager     |
| Event Processing   |
+--------------------+
```

---

## Capabilities

* Full deployment of the **ISIEM stack** using Docker
* **Docker Compose** support for orchestration
* **Scalable architecture** with multi-node support
* **Persistent data storage** through configurable volumes
* **Ready-to-use configurations** for production or testing environments

---

## Prerequisites

Before getting started, ensure the following tools are installed on your system:

* Docker
* Docker Compose
* Linux environment (recommended for container builds)

---

## Quick Start

### Build the customized images locally

Navigate to the build directory:

```bash
cd isiem-docker/isiem-build-docker-images
```

Run the build script:

```bash
./build-images.sh
```

This process builds Docker images for all ISIEM components on your local system.

Alternatively, you can build individual images manually:

```bash
docker build -t isiem/manager ./manager
docker build -t isiem/indexer ./indexer
docker build -t isiem/dashboard ./dashboard
```

Run the stack using Docker Compose:

```bash
docker compose up -d
```

---

## Deployment

This project is primarily designed for **Kubernetes environments**, but Docker Compose can be used for **local testing and development**.


## 💬 Connect
If you found this project helpful or have any questions, feel free to reach out!


📱 Phone: (+91) 7008-62-6663

📧 Email: sandeepdashmlops@gmail.com

💻 GitHub: https://github.com/sandeepdash-mlops

---

This README provides a structured walkthrough on how to develop inhouse siem solution in a customized way and build Docker images for the Wazuh central components (manager, indexer, and dashboard) and the Wazuh agent as part of the customized SIEM platform.
