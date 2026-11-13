<div align="center">

# 🔎 FOOTPRINTING, RECONNAISSANCE & LAN SCANNING

### 🛡️ Practical Cybersecurity Lab Report

![Maltego](https://img.shields.io/badge/Tool-Maltego-6f42c1?style=for-the-badge)
![Zenmap](https://img.shields.io/badge/Tool-Zenmap%20%2F%20Nmap-0d6efd?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-00b4d8?style=for-the-badge)
![Type](https://img.shields.io/badge/Type-Passive%20Recon-2ea44f?style=for-the-badge)
![Exploitation](https://img.shields.io/badge/Exploitation-None-lightgrey?style=for-the-badge)

</div>

> 📌 **Exercise overview:** This report documents the reconnaissance performed against `networkwalks.com` using **Maltego** and the host-discovery scan performed on the local area network using **Zenmap**.

---

## 📋 1. Exercise Overview

The practical exercise consisted of two activities:

| # | Activity | Tool | Goal |
|:-:|----------|:----:|------|
| 1️⃣ | **Footprinting & reconnaissance** | 🟣 Maltego | Gather publicly discoverable information and visualize relationships between entities associated with `networkwalks.com` |
| 2️⃣ | **Local network discovery** | 🔵 Zenmap | Identify live hosts on the local LAN |

> 💡 **Purpose of Maltego:** to gather publicly available information and visualize relationships between entities associated with the target domain.

---

## 🕵️ 2. Footprinting & Reconnaissance: Maltego

🎯 **Target domain:** `networkwalks.com`

Reconnaissance was performed against the domain using **Maltego**, an OSINT tool available on Kali Linux. The objective was to identify publicly available information associated with the domain and discover relationships between its **email addresses, online accounts, websites and contact information**.

### 🔧 2.1 Transforms Performed and Results

#### 📧 A. To Email @ Domain
Applied to `networkwalks.com` to identify email addresses associated with the domain. This established a connection between the domain and publicly discoverable email information.

#### 🌐 B. Search Web
Applied to the discovered email address. The transform returned **24 entities**, including **23 links** to websites and social media accounts. These results provided additional information about the online presence associated with the email address.

#### 📘 C. Transform on the Facebook Entity
A further transform was run on the Facebook entity among the discovered results. The result included a **phone number** associated with the Facebook entity, revealing another piece of publicly discoverable contact information.

### 📊 2.2 Maltego Findings Summary

| 🧩 Transform | 🔍 Observation |
|--------------|----------------|
| 📧 **To Email @ Domain** | Identified an email address associated with `networkwalks.com` |
| 🌐 **Search Web** | Returned **24 entities**, including **23 links** to websites and social media accounts |
| 📘 **Further transform on Facebook entity** | Returned a **phone number** associated with the Facebook entity |

---

## 📡 3. Local Network Scanning: Zenmap

After the Maltego reconnaissance, **Zenmap** was used to perform host discovery on the local area network. The scan was intended to identify active hosts within the local subnet.

### 🖧 3.1 Network Details

| 📌 Item | ✅ Result |
|---------|-----------|
| 💻 Local IP address | `10.40.36.221` |
| 🌍 LAN subnet | `10.40.36.0/24` |
| 🟢 Live hosts identified | **2** |
| 🔬 Host discovery method | sS with sV |

### 🖥️ 3.2 Live Hosts Identified

| 🌐 Host IP address | 🏷️ MAC address |
|--------------------|----------------|
| `10.40.36.191` | `3A:59:DA:79:75:0F` |
| `10.40.36.221` | _Not recorded in the information available for this report_ |

The scan identified **two live hosts** on the local subnet. The MAC address recorded above was associated with `10.40.36.191`.

### ⌨️ Command Used

```bash
sudo nmap -sS -sV 10.40.36.0/24
```

| 🚩 Flag | 📖 Meaning |
|:-------:|-----------|
| `-sS` | TCP port scan |
| `-sV` | service version  |

---

## 🚨 4. Identified Risks and Findings

Based on the information collected during the footprinting and network scanning activities, the following potential risks and observations were identified.

| # | 🏷️ Risk / Finding | 🔎 Evidence / Observation | 💥 Potential Impact | 🚦 Risk Level |
|:-:|-------------------|---------------------------|---------------------|:-------------:|
| 1 | **Email address associated with the target domain identified** | Maltego's **To Email @ Domain** transform identified an email address associated with `networkwalks.com` | Discovered email addresses could be used for targeted phishing or social engineering attempts | 🟢 **Low** |
| 2 | **Multiple online accounts and websites associated with the email address** | Maltego's **Search Web** transform returned 24 entities, including 23 links to websites and social media accounts | Could help an attacker build a profile of the target's online presence and identify potential avenues for social engineering | 🟡 **Medium** |
| 3 | **Phone number associated with a Facebook entity discovered** | A further Maltego transform on the Facebook entity returned an associated phone number | Contact information could potentially be misused for targeted phishing, impersonation or unwanted contact | 🟡 **Medium** |
| 4 | **Multiple live hosts identified on the local network** | Zenmap host discovery identified 2 live hosts on the `10.40.36.0/24` subnet: `10.40.36.191` and `10.40.36.221` | Identifying active devices provides information about the network environment and could assist an attacker in planning further network reconnaissance | 🟡 **Medium** |
| 5 | **MAC address information identified during LAN scanning** | The scan identified MAC address `3A:59:DA:79:75:0F` associated with host `10.40.36.191` | MAC address information can assist in identifying devices on the local network, although it does not independently establish a vulnerability | 🟢 **Low** |

### 🎨 Risk Level Key

| Level | Meaning |
|:-----:|---------|
| 🔴 | **Critical** |
| 🟡 | **Medium** |
| 🟢 | **Low** |

> ℹ️ The findings above represent observations from the footprinting and network scanning exercises and **do not necessarily indicate confirmed security vulnerabilities**.

### 🧠 Interpretation

- 🟣 The **Maltego** exercise focused on **passive reconnaissance** and gathering publicly discoverable information associated with `networkwalks.com`.
- 🔵 The **Zenmap** exercise focused on discovering **active hosts** within the local network.
- 🔬 The Zenmap scan used host discovery (`-sn -PR`), which identifies live hosts using ARP discovery on the local network. It did **not** perform port scanning or vulnerability assessment.

> ⚖️ Therefore, identifying email addresses, social media accounts, phone numbers, IP addresses or MAC addresses does **not** automatically mean that the target domain or local network is vulnerable. Further **authorized** security testing would be required to establish whether any actual vulnerabilities exist.

---

## ✅ 5. Security Recommendations

Based on the observations from the footprinting and network scanning activities, the following security improvements are recommended:

| # | 🛠️ Recommendation | 📖 Description |
|:-:|-------------------|----------------|
| 1 | 📧 **Protect publicly discoverable email addresses** | Monitor the exposure of official email addresses and implement appropriate email security measures to reduce phishing and email-based attacks |
| 2 | 🌐 **Monitor the organization's online presence** | Regularly review websites, social media accounts and other online platforms associated with the domain to identify unauthorized or outdated information |
| 3 | 📞 **Protect publicly available contact information** | Carefully manage the exposure of phone numbers and other contact details to reduce the risk of social engineering, impersonation and unwanted contact |
| 4 | 🔐 **Strengthen social media account security** | Use strong passwords, multi-factor authentication and appropriate privacy settings to prevent unauthorized access |
| 5 | 🔄 **Perform regular internal network discovery** | Periodically scan your own networks using tools such as Zenmap to identify active devices and maintain awareness of the network environment |
| 6 | 🕵️ **Investigate unknown or unauthorized devices** | Investigate any unexpected device to determine its owner, purpose and authorization to connect to the network |
| 7 | 🗂️ **Maintain accurate network documentation** | Document and regularly update IP addresses, MAC addresses, connected devices and network topology to support monitoring and administration |
| 8 | 📈 **Monitor network activity** | Implement network monitoring to identify unusual connections, suspicious devices and potentially unauthorized network access |
| 9 | 📜 **Perform security testing with authorization** | Only perform reconnaissance and network scanning against systems and networks where appropriate authorization has been provided |

---

## 🏁 6. Conclusion

The practical exercise demonstrated how **OSINT** and **network-discovery** tools can be used to collect information about a domain and identify active devices on a local network.

- 🟣 **Maltego** helped reveal relationships between `networkwalks.com`, an associated email address, websites, social media accounts and a phone number returned by a further transform on a Facebook entity.
- 🔵 **Zenmap** identified two live hosts on the local `10.40.36.0/24` subnet.

These activities provided experience in **information gathering**, **entity relationship analysis** and **local network host discovery**.


<div align="center">

---

🔐 _Practical Cybersecurity Lab Report: Footprinting, Reconnaissance & LAN Scanning_ 🔐

</div>
