# 🚀 NGINX Setup & Reverse Proxy (Windows)

This guide covers all **9 steps** for installing, running, configuring, and troubleshooting NGINX on Windows as a reverse proxy gateway for microservices.

---

# 1️⃣ Download & Install NGINX

### Step 1 — Download  
https://nginx.org/en/download.html

### Step 2 — Extract  
Recommended folder (no spaces):

```
D:\nginx
```

Folder contains:
- nginx.exe  
- conf/nginx.conf  
- logs/  
- html/

---

# 2️⃣ Start, Stop & Manage NGINX

```
nginx               → start server
nginx -s stop       → stop immediately
nginx -s quit       → graceful stop
nginx -s reload     → reload config after edit
nginx -t            → test nginx.conf for errors
tasklist | findstr nginx  → check running processes
taskkill /F /IM nginx.exe → kill all nginx if stuck
```

---

# 3️⃣ Fix Port 80 Error (10013)

Edit:
```
conf/nginx.conf
```

Change:
```
listen 80;
```
To:
```
listen 9000;
```

Restart:
```
nginx -s stop
nginx
```

---

# 4️⃣ Configure Reverse Proxy (API Gateway)

Add inside `server {}` block:

```nginx
server {
    listen 9000;
    server_name localhost;

    location /api/sources/     { proxy_pass http://localhost:8085/; }
    location /api/fetcher/     { proxy_pass http://localhost:8081/; }
    location /api/processor/   { proxy_pass http://localhost:8084/; }
    location /api/alerts/      { proxy_pass http://localhost:8080/; }
    location /api/notify/      { proxy_pass http://localhost:8083/; }
    location /api/user-alerts/ { proxy_pass http://localhost:8086/; }
    location /api/history/     { proxy_pass http://localhost:8082/; }
}
```

Reload:
```
nginx -s reload
```

---

# 5️⃣ Test NGINX & Routing

Open:
```
http://localhost:9000
```

Test API:
```
http://localhost:9000/api/sources/getSources
```

---

# 6️⃣ Recommended Folder Structure

```
D:/
└── nginx/
    ├── nginx-1.28.0/
    │   ├── conf/
    │   ├── html/
    │   ├── logs/
    │   └── nginx.exe
```

---

# 7️⃣ Useful Commands (Windows)

```
tasklist | findstr nginx      → check nginx processes
netstat -ano | findstr :9000  → check port usage
taskkill /PID <ID> /F         → kill a process
notepad conf/nginx.conf       → open config
```

---

# 8️⃣ Troubleshooting

### NGINX won't start  
✔ Syntax error  
✔ Extra/missing braces `{}`  
✔ Port conflict  
Run:
```
nginx -t
```

### Port blocked  
```
netstat -ano | findstr :9000
taskkill /PID <ID> /F
```

---

# 9️⃣ Why This README Exists

This README provides:
- Full installation steps  
- Full NGINX command reference  
- Complete reverse proxy configuration  
- All port fix solutions  
- Troubleshooting & testing  
- A repeatable setup guide for any developer  

It ensures **any developer** (including future you) can set up NGINX consistently and quickly.

---
