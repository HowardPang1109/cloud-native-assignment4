# cloud-native-assignment4

本專案包含兩個應用程式：
- `frontend`：以 Nginx 提供靜態頁面
- `backend`：以 Flask 實作簡單 API

---

## 🐳 Docker Build 指令說明

### 🔧 frontend（nginx）

```bash
cd frontend
docker build -t your_dockerhub_username/2025cloud:frontend .
```

### 🔧 backend（flask）

```bash
cd backend
docker build -t your_dockerhub_username/2025cloud:backend .
```

---

## 🚀 Docker Run 指令說明

### ▶️ frontend

```bash
docker run -d -p 8080:80 your_dockerhub_username/2025cloud:frontend
```

瀏覽器開啟 http://localhost:8080

### ▶️ backend

```bash
docker run -d -p 5000:5000 your_dockerhub_username/2025cloud:backend
```

瀏覽器開啟 http://localhost:5000

---

## 🧩 GitHub Actions 自動化流程整合

- push 或 PR 時會自動觸發 `Build and Push Docker Images` workflow
- 成功推送 image 至：
  - `howard921109/2025cloud:frontend`
  - `howard921109/2025cloud:backend`
- Actions 記錄頁：[workflow 記錄](https://github.com/HowardPang1109/cloud-native-assignment4/actions)

---

## ✅ PR 測錯驗證



- 故意在 Dockerfile 中將 `RUN apt-get` 改為 `RUN apt-getttt`，使得 build 無法成功。
- GitHub Action 成功偵測錯誤並在 Actions log 中顯示錯誤訊息。


## 🤖 GitHub Action 自動化流程圖解

```mermaid
graph TD
  A[git push 到 GitHub] --> B[GitHub Action 啟動]
  B --> C[自動執行 docker build]
  C --> D[建立兩個 image]
  D --> E[推送到 DockerHub:2025cloud]
  E --> F[Tag: frontend / backend]
  F --> G[可供下載與部署]
```

---

## 🌿 Docker Image Tag 設計原則

- frontend：`yourname/2025cloud:frontend`
- backend：`yourname/2025cloud:backend`

說明：
- 將兩個不同角色的應用整合在同一個 Repo (即 cloud-native-assignment4) 下，有利於集中管理與 CI/CD 整合
- 分別以 `frontend` 與 `backend` 為 Tag 區隔服務角色

---

## 📂 專案目錄結構

```bash
cloud-native-assignment4/
├── frontend/
│   ├── index.html
│   └── Dockerfile
├── backend/
│   ├── app.py
│   └── Dockerfile
└── .github/
    └── workflows/
        └── docker.yml
```

---

## 🧪 測試方式

### 查看容器是否正常執行：

```bash
docker ps
```

### 查看 image 是否存在：

```bash
docker images
```

---
