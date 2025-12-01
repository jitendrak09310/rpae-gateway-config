# 🚀 NGINX Setup & Configuration on Windows  
This repository explains how to install, run, and configure **NGINX as a reverse proxy gateway** for microservices on Windows.

## 📦 1. Download & Install NGINX
Download from: https://nginx.org/en/download.html
Extract to: C:\nginx

## 🟢 2. Start & Stop NGINX
nginx               → Start  
nginx -s stop       → Stop  
nginx -s quit       → Graceful stop  
nginx -s reload     → Reload config  
nginx -t            → Test config  

## 🔁 4. Configure Reverse Proxy
Edit conf/nginx.conf:
server {
    listen 9000;
    server_name localhost;
    location /api/sources/ { proxy_pass http://localhost:8085/; }
}

## 🧪 Test
http://localhost:9000/api/sources/getSources
