# 9Router

**Deskripsi:** AI Infrastructure Management Platform  
**URL:** https://enow.arzastore.com  
**Port:** 20128  
**Tech Stack:** Node.js + Nginx reverse proxy

## Fitur
- Management AI infrastructure
- Routing & load balancing
- Monitoring & analytics

## Database
- Type: (check saat restore)

## Backup
Backup otomatis setiap hari jam **00:00 WIB**:
- Source code → GitHub private repo
- Database dumps → folder `backups/`

## Restore di VPS Baru

### 1. Clone repo
```bash
cd /opt
git clone git@github.com:arkhindi12/9router.git
cd 9router
```

### 2. Install dependencies
```bash
npm install
```

### 3. Setup environment
```bash
cp .env.example .env
# Edit .env sesuai kebutuhan
nano .env
```

### 4. Restore database (jika ada)
```bash
# Pilih backup terakhir
ls -lt backups/
# Restore sesuai DB type (MySQL/Postgres/SQLite)
```

### 5. Start aplikasi
```bash
pm2 start ecosystem.config.js
pm2 save
```

### 6. Setup Nginx
```bash
# Copy config dari backup atau buat baru
sudo nano /etc/nginx/sites-available/enow.arzastore.com
sudo ln -s /etc/nginx/sites-available/enow.arzastore.com /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 7. SSL (Certbot)
```bash
sudo certbot --nginx -d enow.arzastore.com
```

## Verifikasi
```bash
curl http://localhost:20128
pm2 logs 9router
```

---
*Auto-generated backup documentation*  
*Last updated: 2026-06-06*
