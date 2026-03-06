# Copy Public Key to a Server

## Option 1 (recommended)

```bash
ssh-copy-id user@server_ip
```

Examples 1:

```bash
ssh-copy-id username@host
```
```bash
ssh-copy-id user@192.168.1.10
```
```bash
ssh-copy-id -i mykey.rsa.pub username@host
```
```bash
ssh-copy-id -i /home/admion/agent_keys/id_rsa.pub user@192.168.101.1
```
```bash
ssh-copy-id -i /home/admion/agent_keys/id_rsa.pub -o "IdentityFile hostkey.rsa" user@192.168.101.1
```

---

Examples 2:

```bash
 ssh-copy-id -i /home/andtokm/DiskS/ProjectsUbuntu/Python/resources/test_ssh_keys2/id_ed25519.pub  test@172.18.0.2
```
where
```
    /home/andtokm/DiskS/ProjectsUbuntu/Python/resources/test_ssh_keys2/id_ed25519.pub - path to public key
    test          - remote Linux machine user
    172.18.0.2    - remote Linux machine IP addess
```

---

## Option 2 (manual)

Copy the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Add it to the server:

```
~/.ssh/authorized_keys
```

Example:

```bash
nano ~/.ssh/authorized_keys
```

Paste the key and save.

---

# Test SSH Login

```bash
ssh user@server_ip
```
```bash
ssh -i /home/admion/agent_keys/id_rsa  user@server_ip
```

If everything is configured correctly, you will log in without a password.

---

# Check Permissions (important)

On the server:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys