# 🚀 ZigChain Node — Docker + Kubernetes Deployment

A portable, containerized ZigChain node setup built for easy deployment on any server or Kubernetes cluster.

This repository packages your ZigChain binary (`zigchaind`) and node data (`.zigchain/`) into a Docker image, 
pushes it to Docker Hub, and runs it using Kubernetes manifests.

---

## 📦 Features

- ✅ Portable ZigChain node in a single Docker image  
- 🛠️ Automatic first-time initialization (no manual setup needed)  
- 💾 Auto-creates valid `priv_validator_state.json` (no empty file crashes)  
- ☸️ Kubernetes-ready: includes deployment and service manifests  
- 🔁 Self-restarting and cluster-compatible  
- 🔐 Public/private Docker registry support

---

## 🗂️ Project Structure

zigchain-docker/
│
├── Dockerfile # ZigChain Docker build definition
├── .dockerignore # Ignored files during Docker build
├── README.md # Documentation (this file)
│
└── k8s/ # Kubernetes manifests
├── deployment.yaml # Pod definition (runs the ZigChain node)
├── service.yaml # Exposes RPC (26657), P2P (26656), API (1317)
└── pvc.yaml (optional) # Persistent storage for node data
