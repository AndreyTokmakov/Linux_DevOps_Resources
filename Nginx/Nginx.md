# Install Nginx

```bash id="7s4k9m"
sudo apt update
sudo apt install nginx
```

Check version:

```bash id="w2n6qa"
nginx -v
```

---

# Start Nginx as a Service (systemd)

Start:

```bash id="l0r5te"
sudo systemctl start nginx
```

Check status:

```bash id="b3x8ny"
sudo systemctl status nginx
```

Enable auto-start on boot:

```bash id="v9k2ds"
sudo systemctl enable nginx
```

Restart:

```bash id="u6m1cx"
sudo systemctl restart nginx
```

Stop:

```bash id="p4q7az"
sudo systemctl stop nginx
```

---

# Verify It’s Working

Open in a browser:

```
http://localhost
```

Or from the server:

```bash id="n8j3lw"
curl http://localhost
```

If everything is correct, you should see:

**Welcome to nginx!**

---

# If It’s Not Accessible

Check if port 80 is listening:

```bash id="t2f6he"
ss -tulnp | grep 80
```

If firewall is enabled:

```bash id="k5m9vr"
sudo ufw allow 'Nginx Full'
sudo ufw status
```
