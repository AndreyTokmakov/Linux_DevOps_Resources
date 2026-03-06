# Generate SSH Keys

SSH keys allow secure authentication without using passwords.

## Generate a new SSH key

Run the following command:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Explanation:

* `-t ed25519` — key type (recommended modern algorithm)
* `-C` — comment (usually your email)

Example output:

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
```

Press **Enter** to accept the default location.

---

## Enter a passphrase (optional but recommended)

```
Enter passphrase (empty for no passphrase):
```

A passphrase protects your private key.

---

## Result

Two files will be created:

```
~/.ssh/id_ed25519       # private key
~/.ssh/id_ed25519.pub   # public key
```

Private key → **keep secret**
Public key → **copy to servers**


# Recommended Key Types

| Type    | Status           |
| ------- | ---------------- |
| ed25519 | recommended      |
| rsa     | widely supported |
| ecdsa   | less common      |

Modern recommendation:

```bash
ssh-keygen -t ed25519
```