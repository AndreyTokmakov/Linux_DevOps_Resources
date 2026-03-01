# What is `ip route`?

`ip route` is used to view and manage the Linux routing table.
It is part of the **iproute2** package.

---

# Installation (Ubuntu only)

```bash
sudo apt update
sudo apt install iproute2
```

Verify:

```bash
ip -V
```

---

# View Routing Table

### Show main routing table

```bash
ip route
```

or

```bash
ip route show
```

### Detailed output

```bash
ip -d route
```

### Show all routing tables (policy routing)

```bash
ip route show table all
```

---

# Check How Traffic Will Be Routed

Very useful for debugging:

```bash
ip route get 8.8.8.8
```

It shows:

* which gateway will be used
* which interface
* which source IP address

---

# Add Routes

### Add default gateway

```bash
sudo ip route add default via 192.168.1.1
```

### Add route to a network

```bash
sudo ip route add 10.0.0.0/24 via 192.168.1.254 dev eth1
```

### Add route to a single host

```bash
sudo ip route add 10.0.0.5 via 192.168.1.254
```

---

# Delete Routes

```bash
sudo ip route del default
sudo ip route del 10.0.0.0/24
```

---

# Replace Existing Route

Safer than add (won’t fail if route exists):

```bash
sudo ip route replace default via 192.168.1.1
```

---

# ⚖Metrics (Priority)

If multiple routes exist:

```bash
sudo ip route add default via 192.168.1.1 metric 100
sudo ip route add default via 10.0.0.1 metric 200
```

Lower metric = higher priority.

---