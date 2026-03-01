# How to Configure a Reverse Proxy

## Scenario

You have an application running locally:

```
http://127.0.0.1:3000
```

You want Nginx to expose it on:

```
http://your-server-ip
```

---

# Step 1 — Create a Server Block

Create file:

```bash
sudo nano /etc/nginx/sites-available/myapp
```

Add:

```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:3000;
        
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

---

# Step 2 — Enable the Config

```bash
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
```

Remove default config (optional but recommended):

```bash
sudo rm /etc/nginx/sites-enabled/default
```

---

# ✅ Step 3 — Test Configuration

```bash
sudo nginx -t
```

If OK:

```
syntax is ok
test is successful
```

---

# Step 4 — Reload Nginx

```bash
sudo systemctl reload nginx
```

---

# 🎯 Done

Now:

```
http://your-server-ip
```

will forward traffic to:

```
127.0.0.1:3000
```

---

# What Reverse Proxy Gives You

* Hide internal ports
* SSL termination
* Load balancing
* Security filtering
* Centralized logging

---

# Common Production Additions

## Increase timeouts (for APIs)

```nginx
proxy_read_timeout 60s;
```

## WebSocket support

```nginx
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
```