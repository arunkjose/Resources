---

# **Linux Network Configuration Cheatsheet**

---

## `ip` – Modern replacement for `ifconfig`

### View all network interfaces:
```bash
ip a
```
or
```bash
ip addr show
```

### Display specific interface info:
```bash
ip addr show eth0
```
---

## `ifconfig` – Legacy command (deprecated but still widely used)

### Show all interfaces:
```bash
ifconfig
```

### Show a specific interface:
```bash
ifconfig eth0
```
---

## `netstat` – Legacy tool for network statistics (replaced by `ss`)

### Show all network connections:
```bash
netstat -ant
```

### Show listening ports:
```bash
netstat -tuln
```
### Show interface statistics:
```bash
netstat -i
```

> Requires `net-tools` package. Install via:  
> `sudo apt install net-tools`

---

## `ss` – Socket statistics (modern alternative to `netstat`)

### Show all TCP connections:
```bash
ss -t -a
```

### Show all listening connections (TCP & UDP):
```bash
ss -tuln
```

### Filter by port (e.g., 22):
```bash
ss -tuln sport = :22
```

---
