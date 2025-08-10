# Cyber Security Internship – Task 4: Basic Firewall Configuration and Testing

## Objective:
Configure and test basic firewall rules to allow or block traffic, gaining hands-on understanding of network traffic filtering.

---

## Tools Used:
- **macOS Built-in Packet Filter (PF Firewall)**
- Terminal

---

## Steps Performed:

### 1. Checked Current Firewall Status
```bash
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate
```
Output: Shows whether firewall is enabled or disabled.

---

### 2. Enabled macOS Firewall
```bash
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on
```
Confirmed that firewall is now active.

---

### 3. Added a Rule to Block a Specific Port (Example: Telnet - Port 23)
- Opened **pf.conf** configuration file to add a blocking rule:
```bash
sudo nano /etc/pf.conf
```
- Added:
```
block drop in proto tcp from any to any port 23
```
- Saved and reloaded PF:
```bash
sudo pfctl -f /etc/pf.conf
sudo pfctl -e
```

---

### 4. Tested the Rule
- Tried connecting to port 23 (Telnet), connection was blocked.

---

### 5. Allowed SSH (Port 22)
- Edited **pf.conf** and added:
```
pass in proto tcp from any to any port 22
```
- Reloaded PF:
```bash
sudo pfctl -f /etc/pf.conf
```

---

### 6. Removed the Test Block Rule
- Removed the port 23 block rule from `pf.conf`.
- Reloaded firewall to restore default state.

---

## Key Observations:
- Port 23 was successfully blocked when rule applied.
- SSH port remained open after allowing explicitly.
- PF firewall applies rules in order; later rules can override earlier ones.
- Always reload PF after making changes.

---

## Security Insight:
Blocking unused ports (e.g., Telnet) helps reduce attack surface.  
Allowing only required services (e.g., SSH) strengthens system security.

---

## Outcome:
Gained practical skills in:
- Viewing and enabling firewall.
- Writing and applying custom firewall rules.
- Testing and verifying rules.
- Understanding how firewall filters inbound and outbound traffic.

---

## Files in this Repository:
| File                  | Description                              |
| --------------------- | ---------------------------------------- |
| `firewall_steps.txt`  | Commands and steps used in this task      |
| `screenshots/`        | Step-by-step screenshots of execution     |
| `README.md`           | Complete explanation of Task 4            |
