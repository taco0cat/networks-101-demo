# 🛡️ Network Security & Routing Simulator

[![Made With HTML](https://img.shields.io/badge/Built%20With-HTML5%20%2F%20CSS3%20%2F%20Vanilla%20JS-orange?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero-brightgreen?style=for-the-badge&logo=checkmarx&logoColor=white)](.)
[![Live Demo](https://img.shields.io/badge/Status-Live%20Demo%20Deployed-blueviolet?style=for-the-badge&logo=statuspage&logoColor=white)](.)
[![PowerPoint Ready](https://img.shields.io/badge/Embed-PowerPoint%20Ready-B7472A?style=for-the-badge&logo=microsoftpowerpoint&logoColor=white)](.)
[![Canva Compatible](https://img.shields.io/badge/Embed-Canva%20Compatible-00C4CC?style=for-the-badge&logo=canva&logoColor=white)](.)
[![Canvas API](https://img.shields.io/badge/Rendering-HTML5%20Canvas%20API-informational?style=for-the-badge&logo=codepen&logoColor=white)](.)
[![Workshop](https://img.shields.io/badge/Format-Networks%20101%20Live%20Session-yellow?style=for-the-badge&logo=academia&logoColor=black)](.)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

---

> **"The moment the DDoS flood hit and the firewall node went dashed, the whole room understood why firewalls exist."**
> — Delivered live as part of a Networks 101 introductory workshop

---

## 📡 What Is This?

**Network Security & Routing Simulator** is a single-file, zero-dependency interactive demo built for teaching packet routing and firewall fundamentals to beginners. Rendered entirely via the **HTML5 Canvas API**, it simulates a live network topology — complete with animated packets travelling between nodes — and reacts in real time to four distinct user-triggered scenarios.

The visual feedback loop makes abstract concepts like firewall rules, packet routing, and DDoS floods *immediate* and *intuitive* — no terminal, no config, no prior knowledge required.

---

## 🎓 Workshop Context

This tool was **designed for and deployed in a live Networks 101 classroom session**. The goal was simple: make students *see* the network, not just hear about it. (Used for IoT club workshop presentation purposes)

- 🏫 Demonstrated **live** to a class, with the instructor triggering scenarios in real time during the lecture
- 🖥️ **Embedded directly into the workshop slide deck** via PowerPoint and Canva (see [Deployment](#-deployment--embedding) below) — no browser switching mid-presentation
- 💬 Each button triggered a new wave of student questions about firewalls, attack vectors, and AWS security groups
- 🎯 Calibrated for **non-technical audiences** — the animated topology did the explaining so the presenter didn't have to

The DDoS simulation in particular landed hardest: watching 20 red malware packets flood the firewall node simultaneously made the concept of volumetric attacks click faster than any slide ever had.

---

## 🖼️ Network Topology

The simulation models a realistic, simplified AWS-style network path:

```
[User PC]  ────────────────┐
                           ▼
                     [AWS Firewall]  ───►  [Web Server]  ───►  [Database]
                           ▲
[Attacker PC]  ────────────┘
```

Each node is rendered as a labelled, colour-coded circle on the canvas. The **Firewall node** visually switches between a solid ring (ON) and a dashed ring (OFF) to reflect its current state. If malware reaches the Web Server, **the server node turns red** — a visceral signal that the machine is compromised.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🟢 **Legitimate Packet Flow** | Simulates an HTTP GET request on Port 80 — User PC → Firewall → Web Server → Database |
| 🔴 **Malware Payload** | Attacker deploys an unauthorised payload on Port 22 — blocked at the Firewall if enabled |
| 🌊 **DDoS Simulation** | Fires 20 malware packets in rapid succession from the Attacker node, flooding the topology |
| 🔥 **Toggleable Firewall** | Firewall can be switched ON/OFF mid-simulation — disabling it lets malware reach and compromise the server |
| 💀 **Server Compromise State** | When malware bypasses a disabled firewall, the Web Server node turns red and a `CRITICAL ALERT` fires in the log |
| 📋 **Live Traffic Log** | Timestamped log panel records every packet decision — `SUCCESS`, `BLOCKED`, `WARNING`, `CRITICAL ALERT` |
| 🎨 **Canvas-Rendered Animation** | Smooth `requestAnimationFrame` loop powers all packet movement and node rendering |
| 📦 **Single HTML File** | No build step, no server, no npm — open the file and it runs |

---

## 🎮 Controls

| Button | What It Does |
|---|---|
| **Send Legitimate Request** | Spawns a green packet: `User PC → Firewall → Web Server → Database` |
| **Send Malware Payload** | Spawns a red packet: `Attacker PC → Firewall → Web Server` — blocked at Firewall if ON |
| **Toggle Firewall: ON / OFF** | Enables or disables the firewall node. Dashed ring = OFF. Toggling back ON also restores the server's colour. |
| **Simulate DDoS** | Spawns 20 malware packets at 100ms intervals, simulating a high-volume flood attack |

---

## 🗺️ Node Reference

| Node | Colour | Role |
|---|---|---|
| User PC | 🟢 Green | Source of legitimate traffic |
| Attacker PC | 🔴 Red | Source of malicious payloads and DDoS traffic |
| AWS Firewall | 🟣 Purple | Intercepts and drops malicious packets when enabled |
| Web Server | 🔵 Blue | Receives legitimate requests; turns red if compromised |
| Database | 🟡 Yellow | Final destination for successful legitimate requests |

---

## 📋 Log Output Reference

The scrolling log panel timestamps every network event:

```
[10:42:01] Simulation Initialized. Awaiting network traffic...
[10:42:05] User initiated HTTP GET request to Port 80.
[10:42:06] SUCCESS: HTTP GET request fulfilled by Database.
[10:42:09] Attacker deployed unauthorized payload to Port 22.
[10:42:10] BLOCKED: Malicious payload dropped at Firewall (IP: 10.0.0.99)
[10:42:15] System Administrator turned Firewall OFF.
[10:42:17] WARNING: Malware bypassed disabled firewall.
[10:42:18] CRITICAL ALERT: Web Server compromised by injected payload!
[10:42:22] WARNING: High-volume DDoS traffic detected from Attacker IP!
```

---

## 🚀 Deployment & Embedding

The tool was built **embed-first** — the entire simulation runs from a single `.html` file that drops into any presentation platform without modification.

### 🔴 PowerPoint (Web Viewer Add-in)

1. Host `demo.html` on any static host (GitHub Pages, Netlify, etc.)
2. In PowerPoint → **Insert → Get Add-ins → Web Viewer**
3. Paste the hosted URL into the add-in
4. Resize to fill the slide — the Canvas animation runs live inside the deck

> 💡 Used exactly this way during the live workshop. The instructor triggered DDoS floods and firewall toggles without ever leaving the slide.

### 🩵 Canva (Embed Widget — Canva Pro)

1. Host `demo.html` on a static provider
2. In Canva → **Add Element → Embed → Website**
3. Paste the URL — the interactive canvas renders as a live widget on any slide or doc

> 💡 The Canva deck was distributed to students after the session, letting them replay all four scenarios independently for self-study.

### 🌐 Standalone

```bash
# No install required — just open it directly
open demo.html

# Or serve locally if embedding into other tooling
python3 -m http.server 8080
npx serve .
```

---

## 🧱 Technical Notes

- **Pure vanilla HTML/CSS/JS** — no frameworks, no bundler, no external libraries
- Rendering engine: **HTML5 Canvas API** with a `requestAnimationFrame` animation loop
- Packets are class-based objects (`Packet`) with path arrays, speed, and active state — inactive packets are filtered from the array each frame to prevent memory growth
- Firewall state is a simple boolean toggled at runtime; packet path evaluation happens as each packet reaches the Firewall node
- Dark theme matches GitHub's `#0d1117` palette — renders cleanly on projectors and in presentation embeds
- Tested at **1080p projector resolution** — no zoom or scaling artifacts
- Tested in Chrome, Firefox, Edge, and Safari
- Total file size: **< 15KB**

---

## 📁 File Structure

```
network-sim-101/
├── index.html       # ← The entire application. This is all you need.
└── README.md       # ← You are here
```

---

*Single file. No install. Runs anywhere. Built for the classroom.*
