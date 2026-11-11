
# Born2beRoot 🐧

## About the Project

Born2beRoot is a system administration project developed as part of the 42 curriculum.

The goal is to create and secure a Linux virtual machine while learning essential concepts of operating systems, virtualization, user management, networking, and server security.

## 🖥️ System Information

| Component | Configuration |
|-----------|---------------|
| Operating System | Debian 13 (Trixie) |
| Virtualization | Oracle VirtualBox |
| Hostname | baltaleb42 |
| Main User | baltaleb |
| SSH Port | 4242 |
| Firewall | UFW |
| Partitioning | Encrypted LVM |
| Task Scheduler | Cron |

## 🔐 Security Configuration

### 1. User and Group Management

Configured the following groups:

- `sudo` — Allows authorized administrative operations.
- `user42` — Required group for the project.

The main user `baltaleb` belongs to both groups.

### 2. SSH Configuration

Installed and configured OpenSSH Server.

Security measures:

- Changed the default SSH port from 22 to 4242.
- Disabled direct root login.
- Enabled remote administration for authorized users.

Configuration file:

`/etc/ssh/sshd_config`

### 3. Firewall Configuration

Configured UFW to restrict incoming network connections.

Rules:

- Deny incoming connections by default.
- Allow outgoing connections by default.
- Allow incoming TCP connections on port 4242.

Verification:

```bash
sudo ufw status verbose
```

### 4. Password Policy

Configured password expiration rules:

- Maximum password age: 30 days.
- Minimum password age: 2 days.
- Warning before expiration: 7 days.

Configured password complexity using PAM and libpam-pwquality.

Requirements include:

- Minimum 10 characters.
- At least one uppercase letter.
- At least one lowercase letter.
- At least one digit.
- Restrictions on repeated characters.
- Restrictions on including the username.

### 5. Sudo Security

Configured sudo with additional security measures:

- Maximum of three password attempts.
- Custom incorrect-password message.
- Input/output logging.
- TTY requirement.
- Restricted executable search path.

Sudo log location:

`/var/log/sudo/sudo.log`

## 💾 Disk Partitioning

Configured encrypted disk partitioning using LVM (Logical Volume Manager).

Main partitions:

| Partition | Purpose |
|-----------|---------|
| /boot | Boot files |
| / | Root filesystem |
| /home | User files |
| /var | Variable system data |
| /tmp | Temporary files |
| swap | Swap space |

LVM provides flexible storage management, while encryption helps protect data at rest.

## 📊 System Monitoring

Created a Bash monitoring script named `monitoring.sh`.

The script collects:

- System architecture
- Physical and virtual CPU information
- RAM utilization
- Disk utilization
- CPU load
- Last boot time
- LVM status
- Active TCP connections
- Logged-in users
- IP and MAC addresses
- Number of sudo commands

The script broadcasts system information using `wall`.

### Cron Configuration

Configured Cron to execute the script every 10 minutes.

```cron
*/10 * * * * /usr/local/bin/monitoring.sh
```

## 🧪 Useful Verification Commands

```bash
# Display operating system information
cat /etc/os-release

# Display disk partitions
lsblk

# Check SSH configuration
sudo sshd -T | grep -E '^(port|permitrootlogin) '

# Check firewall
sudo ufw status

# Check user groups
groups baltaleb

# Verify sudo configuration
sudo visudo -c

# Check password expiration
sudo chage -l baltaleb

# Check Cron jobs
sudo crontab -l
```

## 🧠 Skills Developed

Through this project, I practiced:

- Linux system administration
- Virtualization with VirtualBox
- Disk encryption and LVM
- User and permission management
- SSH hardening
- Firewall configuration
- Password security policies
- Bash scripting
- System monitoring
- Task automation with Cron

## 📁 Repository Structure

```text
Born2beRoot/
├── README.md
└── signature.txt
```

The virtual machine disk is stored locally and is not included in the repository.

## 👩‍💻 Author

**Bayan Altaleb**

Networks & Cybersecurity Graduate

42 Amman

