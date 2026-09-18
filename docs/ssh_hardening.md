# 🔐 SSH Hardening (Port 2222)

## Overview
SSH was hardened to reduce attack surface and enforce secure authentication.

---

## SSH Configuration Changes
The following settings were applied in `/etc/ssh/sshd_config`:

- Port 2222
- PermitRootLogin no
- PasswordAuthentication no


These changes:
- Move SSH off the default port (22)
- Prevent root login
- Enforce key-based authentication
<img width="315" height="73" alt="image" src="https://github.com/user-attachments/assets/2842bac7-f3dc-4e49-a88d-6a733dc8cd55" />


---

## Restart SSH
``bash
- sudo systemctl restart ssh
- sudo systemctl status ssh
<img width="440" height="118" alt="image" src="https://github.com/user-attachments/assets/471b8dd9-ae4b-47e5-9203-573d4a216067" />



## 🧱🔥🚫 Firewall Rules
- sudo ufw allow 2222/tcp
- sudo ufw reload
- sudo ufw status
<img width="304" height="142" alt="image" src="https://github.com/user-attachments/assets/32e29125-05e2-4940-9d35-cb72e0b115af" />

## ✔️ Verification
### Check SSH is listening:
``bash
- sudo ss -tlnp | grep ssh
<img width="316" height="107" alt="image" src="https://github.com/user-attachments/assets/f67c2402-21b5-4de3-a143-76ace0694ec5" />

### Expected output:
- LISTEN ... 0.0.0.0:2222
<img width="283" height="102" alt="image" src="https://github.com/user-attachments/assets/7850ad21-e170-4e51-bfc8-921d89e5e32b" />


## Testing SSH
### From Kali or host:
``bash
- ssh -p 2222 username@10.10.10.10
<img width="340" height="104" alt="image" src="https://github.com/user-attachments/assets/3b8c47fc-abcb-4a5c-8cdd-b351326f2024" />


## 📘 What I Learned
- How to secure SSH access
- How to enforce key-based authentication
- How to configure UFW firewall rules
- How to verify SSH service and ports

