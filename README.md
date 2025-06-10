# 🚀 Self-Hosted Homelab Deployment via GitHub + Portainer

![Docker](https://img.shields.io/badge/docker-containers-blue?logo=docker)
![Portainer](https://img.shields.io/badge/portainer-dashboard-0db7ed?logo=portainer)
![GitHub](https://img.shields.io/badge/github-automated--deploy-181717?logo=github)

> A fully automated homelab deployment stack powered by Docker Compose, version-controlled through GitHub, and easily managed with Portainer.

---

## 📸 Preview

![Homepage Screenshot](https://github.com/mrmo-yt/homelab-github-deploy/assets/demo/homepage-preview.png)

---

## 📦 Services Included

Here are all the Dockerized services currently deployed and managed via your Proxmox-based Homelab:

| Service         | Description                                |
|------------------|--------------------------------------------|
| Actual Budget   | Budgeting tool                             |
| Change-Detection| Website change monitoring                  |
| FileZilla       | FTP Server                                  |
| GoTTY           | Terminal sharing over Web                   |
| Grafana         | Metrics dashboard                           |
| IT-Tools        | Useful developer tools                      |
| InfluxDB        | Time-series database                        |
| Kdenlive        | Video editor container                      |
| MinIO           | S3-compatible object storage                |
| OpenTTD         | Multiplayer transport simulation game       |
| Paperless-NGX   | Document management                         |
| Pingvin-Share   | Self-hosted file sharing                    |
| Plex Media Server | Media streaming server                   |
| PrusaSlicer     | 3D printing slicer                          |
| PyLoad          | Download manager                            |
| Remmina         | Remote desktop client                       |
| Syncthing       | Continuous file synchronization             |
| Transmission    | BitTorrent client                           |
| Uptime-Kuma     | Uptime monitoring                           |
| Watch Tower     | Docker container auto-updater               |
| Wordpress       | CMS blogging platform                       |

---

## 📁 File Structure

```bash
homelab-github-deploy/
├── docker-compose.yml       # Container definitions
├── deploy.sh                # Pull + redeploy script
└── README.md                # This file ✨
```

---

## 🚀 Getting Started

### 1. Clone the repository:
```bash
git clone https://github.com/mrmo-yt/homelab-github-deploy.git
cd homelab-github-deploy
```

### 2. Make the deploy script executable:
```bash
chmod +x deploy.sh
```

### 3. Run the stack:
```bash
./deploy.sh
```

> ✅ Make sure Docker and Docker Compose are installed on your server.

---

## 🔁 Optional: Auto-Update with Cron (Server-Side)

Edit crontab:
```bash
crontab -e
```
Add this line to auto-update every 5 minutes:
```cron
*/5 * * * * cd /path/to/homelab-github-deploy && ./deploy.sh
```

---

## 🌐 Access Your Services

- Homepage: [http://your-server-ip:3000](http://your-server-ip:3000)
- Portainer: [http://your-server-ip:9000](http://your-server-ip:9000)

---

## ☁️ Powered By

<div align="center">
  <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="80"/>
  <img src="https://avatars.githubusercontent.com/u/37877329?s=200&v=4" alt="Portainer" width="80"/>
  <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png" alt="GitHub" width="60"/>
</div>

---

## 🙌 Author

- **GitHub:** [@mrmo-yt](https://github.com/mrmo-yt)
- Designed for self-hosted labs running on Proxmox

---

## 📜 License

MIT License