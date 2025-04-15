# Managing Odoo Service on Hetzner Linux Console

This document provides instructions on how to manage your Odoo service on a Hetzner Linux console.

## 0. Basic Setup

Refer to this guide for the initial Odoo setup:

[How to Install Odoo 18 on Ubuntu 24.04 LTS Server](https://www.cybrosys.com/blog/how-to-install-odoo-18-on-ubuntu-24-04-lts-server)

### Navigation & Terminal Commands

*   **Switch Terminal Windows:** `Alt + Left/Right Arrow Keys`
*   **Tabs and Windows Controls (tmux)** `c  create window`
`w  list windows`
`n  next window`
`p  previous window`
`f  find window`
`,  name window`
`&  kill window`

#### Login Details for New Terminal (can be used for sftp as well)
*   **URL:** `188.245.252.105`
*   **Username:** `root`
*   **Password:** `nwqAaM33dMN9rHvrJhat`
*   Vdfinqm7ccjtfHKvUbXm
*   **CMD Command to enable reverse ssh:(put this on the local machine)** `ssh -R :8443:localhost:5087 root@188.245.252.105`

#### Using Tmux

Tmux is a terminal multiplexer that allows you to open multiple terminal windows within a single tab.

*   **Start a Tmux session:** `tmux`
*   **Activate Tmux commands:** `Ctrl + b`

#### Tmux Commands:

*   **Scrolling:**
    1.  `Ctrl + b` then `[`
    2.  Use arrow keys to scroll
    3.  Press `q` to exit scrolling mode
*   **Split Terminal Vertically:** `Ctrl + b` then `%`
*   **Split Terminal Horizontally:** `Ctrl + b` then `"`
*   **Exit a Tmux Window:** `exit`

## Important Steps

1. **No need to install already installed libraries.**
2. **Start from Step 5.**
3. **Pay attention to the name of the user.**
4. **Pay attention to the directory names.**
5. **Pay attention to the permissions using the Linux permission command (`chmod` and `chown`).**
6. **Use this commit hash to download odoo** `196dfc4b8b2cd090807746ef94799c6e464be979`
7. **Change directory to `/opt/odoo18/odoo`:**
   ```bash
   cd /opt/odoo18/odoo
   ```
8. **Copy existing configuration files instead of creating new ones:**
   ```bash
   sudo cp /etc/odoo3.conf /etc/<name of new conf file>.conf
   sudo nano /etc/<name of new conf file>.conf
   ```
   - Remember to change the `db_user`, any paths that need to be changed, log file path and name, and the port number.
9. **Copy the service file from `odoo3.service` and modify it:**
   ```bash
   sudo cp /etc/systemd/system/odoo3.service /etc/systemd/system/<name of new service file>.service
   sudo nano /etc/systemd/system/<name of new service file>.service
   ```
   - Change the user and paths inside the service file.

## Nginx Configuration

1. **Copy the existing nginx configuration file:**
   ```bash
   sudo cp /etc/nginx/sites-available/odoo3 /etc/nginx/sites-available/<name of new company>
   ```
2. **Create a symbolic link to `sites-enabled`:**
   ```bash
   sudo ln -s /etc/nginx/sites-available/<name of new company> /etc/nginx/sites-enabled/
   ```
3. **Check for errors and syntax errors:**
   ```bash
   sudo nginx -t
   ```
4. **Restart nginx to apply changes:**
   ```bash
   sudo systemctl restart nginx
   sudo systemctl restart nginx.service
   ```

# Basic Management Commands
## 1. Service Management

Use the following commands to manage the Odoo service on the Linux console.  Replace `<odoo name>` with the appropriate name (e.g., `odoo18`, `lawter`, `bukhari`, `gefer`).

### Start the Odoo Service
sudo systemctl start <odoo name>.service // usually odoo + number / name of company or name of company without odoo
#### 1 -> lawter
#### 2 -> bukhari
#### 3 -> gefer

### Stop the Odoo Service
sudo systemctl stop odoo18.service

### Restart the Odoo Service
sudo systemctl restart odoo18.service

### Check the Odoo Service Status
sudo systemctl status odoo18.service

## 2. Configuration Files
### Odoo Configuration File
The primary configuration file for Odoo is:

/etc/odoo<name>.conf

## 3. Log Files
Odoo Logs
Odoo logs are crucial for troubleshooting and debugging. The default log file is located at:

/var/log/odoo/odoo<name>.log

### View Logs in Real-Time
sudo tail -f /var/log/odoo/odoo.log

## to overwrite a specific file use 
sudo wget -O filename RawGithubLink
