# 🌐 ASTC – Add Site To Config

**Automated Nginx, SSL, and DNS management from the command line.**

ASTC is a lightweight shell utility designed to make hosting multiple containerized or local web apps easier.  
With just a single command, you can create a new Nginx reverse proxy configuration, issue an SSL certificate with Let's Encrypt, and manage your sites—all without editing files manually.

---

## 🚀 Features

- **Quick Site Setup:** Automatically configures Nginx for a given domain and port.
- **Automatic SSL:** Issues and renews Let's Encrypt certificates for domains and subdomains.
- **DNS Verification:** Checks that your domain is pointed to your server before creating configs.
- **Site Listing:** View all configured domains and their ports in a clean, formatted table.
- **SSL Renewal:** Mass renew all certificates at once.
- **SSL Repair:** Force delete and reissue broken SSL certificates.
- **Update System:** Pull the latest ASTC version and changelog from GitHub with one command.
- **Auto-Domain Discovery:** Populates domain list automatically from Nginx configs if missing.

---

## 📦 Installation

```bash
sudo curl -fsSL https://raw.githubusercontent.com/Aesth3tical/astc/main/astc -o /usr/local/bin/astc
sudo chmod +x /usr/local/bin/astc

# Create ASTC config directory
sudo mkdir -p /etc/astc
```

Optional (recommended): Install Certbot and Nginx
```bash
sudo apt update && sudo apt install -y nginx certbot python3-certbot-nginx
```

---

## ⚡ Usage

### **Basic Commands**

| Command                                | Description                                                   |
|----------------------------------------|---------------------------------------------------------------|
| `astc --add -d domain.com -p 1025`     | Add a new site on port 1025 with SSL setup                   |
| `astc --rem -d domain.com`             | Remove site configuration                                    |
| `astc --ls`                            | List all configured domains and ports                        |
| `astc --check-dns -d domain.com`       | Check if domain points to this server                        |
| `astc --renew-all`                     | Renew SSL certificates for all configured domains            |
| `astc --fix-ssl -d domain.com`         | Delete and reissue SSL certificate for a domain              |
| `astc --update`                        | Update ASTC to the latest version                            |
| `astc --changelog`                     | View latest changes pulled from GitHub                       |
| `astc --help`                          | Display command help menu                                    |

---

## 🔧 Example

```bash
# Add new site and point it to a running container
astc --add -d example.mydomain.com -p 1031

# Verify DNS
astc --check-dns -d example.mydomain.com

# List all configured domains
astc --ls

# Force SSL fix
astc --fix-ssl -d example.mydomain.com
```

---

## 📜 Requirements

- **Ubuntu/Debian-based OS** (tested on Ubuntu 20.04/22.04)
- **Nginx** installed and running
- **Certbot** with Nginx plugin
- **Root privileges** for modifying configs and SSL
- **Domain DNS A record** pointing to your server’s public IPv4 address

---

## 🔄 Auto-Update

ASTC checks for updates every **24 hours** and notifies you if a new version is available.  
Manually update anytime with:

```bash
astc --update
```

---

## 🛠 File Locations

- `/usr/local/bin/astc` → Executable script
- `/etc/astc/sites.txt` → Tracked domain list
- `/etc/astc/changelog.md` → Latest changelog
- `/etc/nginx/sites-available/` → Individual Nginx configs
- `/etc/nginx/sites-enabled/` → Active site symlinks

---

## ⚠️ Disclaimer

ASTC directly manipulates Nginx configuration files and SSL certificates.  
While built for safety, use at your own risk on production systems.  
Always ensure you have backups of your Nginx configs before making bulk changes.

---

## 📌 Version

**v1.0** – Initial public release  
- Add, remove, list sites  
- SSL management (auto-renew, fix broken certs)  
- DNS checking  
- Auto-update & changelog support