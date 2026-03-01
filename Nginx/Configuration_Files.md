# Where Nginx Configuration Files Are Located

Main config file:

```
/etc/nginx/nginx.conf
```

This file includes other configs.

---

## Important Directories

### 🔹 Server blocks (virtual hosts)

```
/etc/nginx/sites-available/
/etc/nginx/sites-enabled/
```

* `sites-available` → all configs
* `sites-enabled` → active configs (symlinks)

Enable a site:

```bash
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
```

Disable a site:

```bash
sudo rm /etc/nginx/sites-enabled/myapp
```

---

### 🔹 Global config parts

```
/etc/nginx/conf.d/
```

Used for additional global configs.

---

### 🔹 Logs

```
/var/log/nginx/access.log
/var/log/nginx/error.log
```

---

### 🔹 Default web root

```
/var/www/html
```