<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice on Apple Silicon**

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red)
![UTM](https://img.shields.io/badge/Virtualization-UTM-blue)
![Kali Linux](https://img.shields.io/badge/Kali%20Linux-ARM64-557C94?logo=kalilinux&logoColor=white)
![Skill](https://img.shields.io/badge/Skill-Linux-red)
![Network](https://img.shields.io/badge/Network-192.168.64.0%2F24-teal)
![Penetration Testing](https://img.shields.io/badge/Penetration%20Testing-Practice-red)
![Skill](https://img.shields.io/badge/Skill-Virtualization-red)
![GitHub](https://img.shields.io/badge/GitHub-Repository-black?logo=github)
![Ethical Hacking](https://img.shields.io/badge/Ethical%20Hacking-Learning-orange)

</div>

---

## 📑 Table of Contents

- [📌 Project Overview](#-project-overview)
- [🎯 Objectives](#-objectives)
- [🛡️ Purpose of the Lab](#️-purpose-of-the-lab)
- [🏗️ Lab Architecture](#️-lab-architecture)
- [⚙️ Lab Configuration](#️-lab-configuration)
- [🪜 Lab Setup Procedure](#-lab-setup-procedure)
- [🔎 Lab Verification](#-lab-verification)
- [🐞 Problems Encountered & Solutions](#-problems-encountered--solutions)
- [💡 What I Learned](#-what-i-learned)
- [🔐 Security & Ethical Use](#-security--ethical-use)
- [🔗 Tools & Resources](#-tools--resources)
- [👤 Author](#-author)
- [📌 Project Information](#-project-information)

---

## 📌 Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using **UTM** and **Kali Linux ARM64** on a MacBook Air M2.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The Kali Linux VM runs on UTM's **Shared Network** mode. Additional machines can be added later and used as targets for authorized security testing.

> **Status note:** Internet connectivity and clipboard sharing have been **verified**. Shared-folder access and VM snapshots are **still pending**.

📷 *Screenshot placeholder (upload your own image):*

![Kali Linux Desktop](screenshots/kali-desktop.png)

---

## 🎯 Objectives

The main objectives of this project are to:

- [x] Install and configure UTM on macOS.
- [x] Install/import Kali Linux ARM64 as a virtual machine.
- [x] Use UTM's Shared Network mode for the cybersecurity lab.
- [x] Configure network connectivity for Kali Linux.
- [x] Identify the IP address assigned to the Kali VM (`192.168.64.4/24`).
- [x] Verify network connectivity and DNS resolution (`ping -c 4 google.com`).
- [x] Test clipboard sharing between macOS and Kali Linux.
- [ ] Configure shared-folder access between macOS and Kali Linux *(pending – unresolved)*.
- [ ] Take a clean VM snapshot for recovery *(pending – not yet verified)*.
- [x] Document the setup process.
- [ ] Prepare the environment for future cybersecurity projects *(in progress)*.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

> ⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---

## 🏗️ Lab Architecture

```text
┌──────────────────────────────────────────────────────────────┐
│  Host: MacBook Air M2  (macOS)                               │
│                                                              │
│   ┌────────────────────────────────────────────────────┐     │
│   │  UTM (Virtualization Software)                     │     │
│   │                                                    │     │
│   │   Network Mode: Shared Network                     │     │
│   │   Subnet:       192.168.64.0/24                    │     │
│   │                                                    │     │
│   │   ┌──────────────────────────────────────┐         │     │
│   │   │  Kali Linux ARM64 (aarch64)          │         │     │
│   │   │  Adapter: virtio-net-pci             │         │     │
│   │   │  IP: 192.168.64.4/24                 │         │     │
│   │   └──────────────────────────────────────┘         │     │
│   │                                                    │     │
│   │   ┌──────────────────────────────────────┐         │     │
│   │   │  Future target VMs (optional)        │         │     │
│   │   │  IPs: not yet assigned               │         │     │
│   │   └──────────────────────────────────────┘         │     │
│   └──────────────────────────┬─────────────────────────┘     │
│                              │                               │
└──────────────────────────────┼───────────────────────────────┘
                               │  (shared / NAT-style access)
                               ▼
                           Internet
```

Additional target machines can be added to the same virtual network in future projects.

> **Note:** UTM Shared Network is **not the same** as a VirtualBox *NAT Network*. The reference project used a custom `10.0.0.0/24` NAT Network with Kali at `10.0.0.2/24`. This lab uses UTM's automatically provided `192.168.64.0/24` network, and Kali is currently at `192.168.64.4/24`.

---

## ⚙️ Lab Configuration

| 🧩 Component | ⚙️ Configuration |
|---|---|
| 💻 Host Device | MacBook Air M2 |
| 🖥️ Host OS | macOS |
| 🧰 Hypervisor | UTM |
| 🐉 Security OS | Kali Linux ARM64 |
| 🏛️ Architecture | aarch64 |
| 🌐 Virtual Network | UTM Shared Network |
| 🔌 Network Adapter | virtio-net-pci |
| 📡 Network Address | 192.168.64.0/24 *(subnet inferred from the Kali IP; the gateway was not recorded)* |
| 🐧 Kali IP Address | 192.168.64.4/24 |
| 🚪 Default Gateway | Not recorded (unverified) |
| 🌍 DNS Server | Not recorded (unverified) |
| 📋 Clipboard Sharing | Enabled and tested successfully |
| 📁 Shared-Folder Access | ⏳ Pending – troubleshooting performed, mounting not verified |
| 🔄 VM Snapshot | ⏳ Pending – not yet verified |
| 🧠 Host RAM / Kali RAM / vCPU | Not recorded (unverified) |

> **Reference comparison:** The reference lab used a static IP of `10.0.0.2/24`. **No static IP has been configured in this UTM lab.** The address `192.168.64.4/24` is the one currently in use.

---

## 🪜 Lab Setup Procedure

### Step 1. Install the required software

On macOS, **7-Zip is not strictly required**. The reference used 7-Zip to extract a `.7z` archive. UTM can import or create VMs directly, but you may need an archive tool if your Kali download is compressed (macOS can extract `.zip` natively; `.7z` needs an additional tool).

**Tools:** UTM, Kali Linux ARM64 image (installer ISO or pre-built UTM image), optional archive tool for `.7z` files.

---

### Step 2. Install and configure the virtualization software

UTM was installed on the MacBook Air M2 as the hypervisor (replacing VirtualBox in the reference).

> VirtualBox was **not** installed or used in this project.

Apple Silicon uses hardware virtualization built into macOS, so there is **no BIOS/VT-x step** as in the reference.

---

### Step 3. Create and configure the virtual network

The reference created a custom VirtualBox *NAT Network* (`10.0.0.0/24`). **This step does not directly apply to UTM.**

The UTM equivalent is to set the VM's network mode:

1. Open UTM and select the Kali VM.
2. Click **Edit** (VM settings) → **Network**.
3. Set **Network Mode** to **Shared Network**.
4. Set **Emulated Network Card** to **virtio-net-pci**.
5. Save and start the VM.

UTM automatically provides the `192.168.64.0/24` network and DHCP, so no custom subnet was created.

📷 *Screenshot placeholder (upload your own image):*

![Network Configuration](screenshots/network-configuration.png)

---

### Step 4. Create or import Kali Linux

Kali Linux ARM64 was obtained from the official Kali website and set up as a virtual machine in UTM.

The VM network adapter was configured as follows:

```text
Network Mode:         Shared Network
Emulated Network Card: virtio-net-pci
```

Other VM settings (RAM, CPU cores, disk size): **not recorded – unverified.**

#### Shared-folder access (unresolved)

A shared folder was intended for transferring files between macOS and Kali. This is **not working yet.** See [Problem 3](#problem-3-shared-folder-access-unresolved).

📷 *Screenshot placeholder (upload your own image):*

![Shared Folder Setup](screenshots/shared-folder-setup.png)

---

### Step 5. Configure the Kali Linux network

The Kali network was checked and found to be working with an automatically assigned (DHCP) address.

```text
Network Mode: Shared Network
Adapter:      virtio-net-pci
IP Address:   192.168.64.4/24
```

To view the current configuration:

```bash
ip a
```

> **Difference from reference:** The reference configured a manual static IP (`10.0.0.2`, gateway `10.0.0.1`, DNS `8.8.8.8`). **That configuration was not applied here.** Whether the `192.168.64.4` address came from DHCP or was set manually was not explicitly recorded, so treat it as **unverified**; UTM Shared Network normally assigns addresses by DHCP.

A consistent IP address makes it easier to document the lab. If a static address is wanted later, it can be set in NetworkManager and documented separately.

---

### Step 6. Create a clean VM snapshot

> ⏳ **Status: Pending – not yet verified.**

The reference created a VirtualBox snapshot. UTM handles this differently: UTM supports snapshots only for **QCOW2 disk images**, and the feature may not be available for every VM configuration. Alternatively, a **clone** of the VM can serve as a baseline backup.

Suggested snapshot/clone name once completed:

```text
Clean Kali - UTM Shared Network Setup
```

Still to be done and verified:

- [ ] Create a snapshot or clone of the clean VM.
- [ ] Make a change (for example, create a test file).
- [ ] Restore the snapshot or clone.
- [ ] Confirm the baseline configuration was restored.

---

## 🔎 Lab Verification

| ✅ Test | 📝 Command / Method | 🎯 Expected Result | 📊 Status |
|---|---|---|---|
| 🌐 Check IP address | `ip a` | Kali IP displayed | ✅ Verified (`192.168.64.4/24`) |
| 🌍 Test Internet & DNS | `ping -c 4 google.com` | Successful replies, 0% packet loss | ✅ Verified (0% packet loss) |
| 📋 Clipboard sharing | Copy and paste both directions | Text transfers macOS ↔ Kali | ✅ Verified (both directions) |
| 🚪 Test gateway | `ip route` then `ping <gateway>` | Successful replies | ⏳ Not recorded |
| 🔎 Test DNS resolution (explicit) | `nslookup google.com` | Domain resolves | ⏳ Not recorded separately *(the ping to `google.com` implies DNS worked)* |
| 🧰 Verify Nmap | `nmap --version` | Nmap version displayed | ⏳ Not recorded |
| 📁 Shared folder | Mount and copy a test file | File accessible in both systems | ❌ Not verified (pending) |
| 🔄 Verify snapshot | Restore snapshot and run `ip a` | Baseline restored | ⏳ Pending |

### Example Results

Only the results you actually obtained are listed:

```text
IP Address:
192.168.64.4/24

Internet Test:
ping -c 4 google.com
4 packets transmitted, 0% packet loss
```

> Exact `ping` output (times, packets received) was not provided, so it is summarized rather than reproduced.

📷 *Screenshot placeholders (upload your own images):*

![Internet Connectivity](screenshots/internet-connectivity.png)

![Clipboard Test](screenshots/clipboard-test.png)

---

## 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

### Problem 1. Internet Connectivity After Network Configuration

| Item | Details |
|---|---|
| **Issue** | The Kali VM needed confirmation that its network worked correctly with UTM Shared Network. |
| **Cause** | Not applicable – no failure was recorded. |
| **Action taken** | Verified the IP address with `ip a` and tested connectivity with `ping -c 4 google.com`. |
| **Current status** | ✅ **Resolved / verified** – 0% packet loss. |

> The reference lab's workaround (`nmcli ... ipv4.dad-timeout 0`) was needed after a **manual static IP** change. No static IP was configured here, so that command was **not used**.

---

### Problem 2. Virtualization or Architecture Compatibility

| Item | Details |
|---|---|
| **Issue** | The reference used an Intel `amd64` Kali image with VirtualBox. |
| **Cause** | The MacBook Air M2 uses an ARM (`aarch64`) CPU, so VirtualBox and Intel images are not the right fit. |
| **Solution** | Use UTM with a **Kali Linux ARM64** image. |
| **Current status** | ✅ **Resolved** – Kali runs on `aarch64`. |

> No BIOS/VT-x change was needed on Apple Silicon.

---

### Problem 3. Shared-Folder Access (Unresolved)

| Item | Details |
|---|---|
| **Issue** | A macOS folder could not be confirmed as mounted or accessible inside Kali. |
| **Cause** | Not identified yet. |
| **Current status** | ❌ **Unresolved** – shared-folder transfer is **not working or not verified**. |

**Troubleshooting steps attempted:**

1. Configured the **Downloads** directory as the shared folder in UTM.
2. Tried the **VirtFS** sharing mode.
3. Switched to **SPICE WebDAV**.
4. Installed `spice-vdagent`.
5. Installed `spice-webdavd`.
6. Started the `spice-webdavd` service.
7. Checked `/dev/virtio-ports/`.
8. Checked whether port **9843** was listening.

**Commands used:**

```bash
sudo apt update
sudo apt install spice-vdagent
sudo apt install spice-webdavd -y
sudo systemctl start spice-webdavd
systemctl status spice-webdavd
ls -l /dev/virtio-ports/
sudo ss -ltnp | grep 9843
```

**Findings:**

- The WebDAV service and device were detected.
- The shared directory was **not confirmed as mounted or accessible**.

**Possible next steps (not yet tried):**

- [ ] Check whether the shared folder appears in the Kali file manager.
- [ ] Re-test VirtFS and mount manually with `mount -t 9p`.
- [ ] Re-check the UTM shared-directory setting after a full VM restart.
- [ ] Use an alternative transfer method (for example, `scp`) if needed.

---

## 💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice on Apple Silicon.

The most important concepts I learned include:

### 1. Virtual Networking Concepts

UTM Shared Network and a VirtualBox NAT Network are **different** configurations. UTM automatically provides a private subnet (`192.168.64.0/24`) with internet access through the host, while VirtualBox NAT Network lets you define your own subnet.

### 2. Virtual Machine Networking

I learned how a virtual adapter (`virtio-net-pci`) connects a VM to the host's virtual network, and how the network mode affects communication and internet access.

### 3. IP Configuration

I learned how to check the VM's IP address with `ip a` and test connectivity and DNS with `ping`. Manual static IP configuration was **not** performed in this project.

### 4. VM Snapshots

I learned that a clean snapshot or clone should be created **before performing risky or experimental activities**. This is still **pending** in this lab.

### 5. Documentation

I learned that documenting commands, configuration, screenshots, problems, and *unresolved* issues honestly is an important part of a professional cybersecurity project.

---

## 🔐 Security & Ethical Use

This laboratory is intended strictly for **educational purposes only**.

- Only test systems you **own** or have **written permission** to test.
- Keep the lab isolated from production and personal systems.
- Do not scan or attack networks, devices, or services you are not authorized to test.
- Create a snapshot or clone before running risky tools.
- Follow all applicable laws and your organization's policies.

---

## 🔗 Tools & Resources

- **UTM:** https://mac.getutm.app/
- **Kali Linux:** https://www.kali.org/get-kali/
- **Kali Linux on Apple Silicon (UTM images):** https://www.kali.org/docs/virtualization/install-utm-guest-vm/
- **7-Zip (optional, for `.7z` files):** https://7-zip.org/download.html

---

## 👤 Author

**Your Name**
Cybersecurity Student / Professional

LinkedIn: https://www.linkedin.com/in/your-profile/

---

## 📌 Project Information

| Field | Details |
|---|---|
| **Program Name** | Cybersecurity at Networkwalks |
| **Week** | 01 |
| **Project** | Cybersecurity & Pentesting Lab Setup |
| **Repository** | GitHub |
| **Host** | MacBook Air M2 (macOS) |
| **Virtualization** | UTM |
| **Guest OS** | Kali Linux ARM64 (aarch64) |
| **Verified** | Internet connectivity, clipboard sharing |
| **Pending** | Shared-folder access, VM snapshot |

---

### 🗂️ Repository Structure

```text
cybersecurity-lab/
├── README.md
└── screenshots/
    ├── kali-desktop.png
    ├── network-configuration.png
    ├── internet-connectivity.png
    ├── clipboard-test.png
    └── shared-folder-setup.png
```

> 📷 **Screenshots:** The image links above are placeholders. Upload your own screenshots to the `screenshots/` folder using the exact filenames shown, or the images will not display.
