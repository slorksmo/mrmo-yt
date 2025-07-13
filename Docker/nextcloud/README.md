# 📦 Nextcloud Docker Setup

This project sets up a complete **Nextcloud stack** with:

- ✅ MariaDB (Database)
- ✅ Redis (Cache)
- ✅ Cron service
- ✅ Apache (internal webserver)
- ✅ Ready for integration with **Cloudflare Tunnel**
- ✅ All data stored in `/home/mrmo/nextcloud`

---

## 📁 Folder Structure

```
/home/mrmo/nextcloud
├── db      → MariaDB data
├── redis   → Redis cache
└── html    → Nextcloud files
```

You can back up this folder or move it to an NFS/NAS mount (like TrueNAS).

---

## 🚀 Getting Started

```bash
mkdir -p /home/mrmo/nextcloud/{db,redis,html}
cd /home/mrmo/nextcloud
docker compose up -d
```

Then open Nextcloud in your browser:  
`http://<YOUR-IP>:8080`

---

## ☁️ Connect to Cloudflare Tunnel

Set up your Cloudflare Tunnel to forward:

```
cloud.momaher.site → http://<nextcloud-IP>:80
```

In your `config.yml` for cloudflared:

```yaml
ingress:
  - hostname: cloud.momaher.site
    service: http://10.10.10.4:80
  - service: http_status:404
```

---

## 🔄 Add Trusted Domain in Nextcloud

Inside the container:

```bash
docker exec -it <nextcloud_container_name> bash
php occ config:system:set trusted_domains 1 --value=cloud.momaher.site
php occ config:system:set overwrite.cli.url --value=https://cloud.momaher.site
```

---

## 💾 Optional: Mount TrueNAS or NAS storage

If you want to store your Nextcloud data (html, db, etc.) on **TrueNAS**:

### Option 1: NFS Mount (recommended)

```bash
sudo apt install nfs-common -y
sudo mount -t nfs 10.10.10.2:/mnt/TrueNASPool/nextcloud /home/mrmo/nextcloud
```

Make it permanent by adding to `/etc/fstab`:

```
10.10.10.2:/mnt/TrueNASPool/nextcloud /home/mrmo/nextcloud nfs defaults 0 0
```

### Option 2: CIFS/SMB Mount

```bash
sudo apt install cifs-utils -y
sudo mount -t cifs //10.10.10.2/nextcloud /home/mrmo/nextcloud -o username=nasuser,password=secret,vers=3.0
```

---

## ✅ Tips

- Make sure folder permissions allow Docker to write:
  ```bash
  sudo chown -R 1000:1000 /home/mrmo/nextcloud
  ```
- Use `docker exec -it <container> bash` for advanced config
- Add backup/rsync/NAS automation as needed

---

## 🔐 Secure with HTTPS

Use **Cloudflare Tunnel** or **Nginx Proxy Manager** + Let's Encrypt to enable full HTTPS access.
