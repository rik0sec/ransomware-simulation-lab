# 🔒 Wannabe Ransomware — Educational Ransomware Simulation

> **A controlled, educational simulation of ransomware behavior and a C2 (Command & Control) panel, built to understand attacker TTPs and strengthen defensive thinking.**

---

## ⚠️ Disclaimer

This project was built **strictly for educational and research purposes** as part of a cybersecurity learning exercise/presentation. It was executed in an **isolated lab environment** (no real network, no real victims, dummy files only).

- No actual malicious payload is included in this repository.
- This project must **not** be used against any system without explicit authorization.
- Publishing this is meant to demonstrate understanding of ransomware mechanics for learning, awareness, and defensive (blue team) purposes — not to provide a ready-to-use attack tool.
- If you fork or reference this project, you are responsible for using it ethically and legally.

---

## 📌 Project Overview

This lab simulates the end-to-end flow of a typical crypto-ransomware attack:

1. A **victim machine (Windows)** executes the simulated ransomware.
2. The program "locks" the system by encrypting a set of dummy files and displaying a ransom note with a countdown timer.
3. A **C2 (Command & Control) dashboard**, controlled by the "attacker," tracks infected victims and can issue the decryption key to unlock files remotely.
4. The victim can attempt to unlock files using a key — the simulation distinguishes between **invalid** and **valid** keys before fully restoring access.

The goal was to understand, hands-on, how ransomware operators structure an attack chain — from initial execution to extortion to remote "customer support"-style decryption — so the behavior can be better recognized and defended against.

---

## 🧩 Architecture (High-Level)

```
┌─────────────────────┐        reports status        ┌──────────────────────┐
│   Victim Machine     │ ───────────────────────────▶ │     C2 Dashboard      │
│  (Windows, isolated) │                               │  (Attacker Console)   │
│                      │ ◀─────────────────────────── │                        │
│  - Lock screen UI    │        sends unlock key       │  - Victim ID list      │
│  - File "encryption" │                               │  - Status (Locked/   │
│  - Ransom note       │                               │    Unlocked)          │
│  - Key verification  │                               │  - Key per victim     │
└─────────────────────┘                               │  - Unlock action       │
                                                        └──────────────────────┘
```

No real exfiltration, lateral movement, or network propagation is implemented — this simulation is scoped to **single-host file locking + remote key-based unlock**, which is enough to demonstrate the core ransomware concept.

---

## ✨ Features Demonstrated

- 🔐 Simulated file encryption (dummy files renamed with `.locked` extension)
- 🧾 Ransom note generation (`README.txt`) dropped automatically after "encryption"
- ⏱️ Countdown timer + lock-screen UI to simulate psychological pressure tactics used by real ransomware
- 🔑 Key verification flow — rejects invalid keys, accepts the correct key issued from C2
- 🖥️ C2 dashboard to track victim ID, lock status, and assigned decryption key
- 🔓 Remote "unlock" action triggered from the attacker's dashboard

---

## 🖼️ Screenshots

### 1. Victim's files before the simulation
![Before Simulation](assets/before-simulation.png)

### 2. Ransomware active — system locked
![Ransomware Active](assets/ransomeware-aktif.png)

### 3. Ransom note (attacker's message) delivered to the victim
![Ransom Note](assets/menampilkanpesan_dari_si_attaker.png)

### 4. Invalid key attempt rejected
![Invalid Key](assets/Invalid-Key.png)

### 5. Attacker's C2 control panel
![C2 Dashboard](assets/c2-dashboard.png)

### 6. Victim's files after the simulation (locked state)
![After Simulation](assets/after-simulation.png)

---

## 🎓 Key Concepts & Lessons Learned

- **Attack lifecycle**: execution → impact (encryption) → extortion (ransom note) → C2 communication → resolution (decryption)
- **Why backups matter**: offline/immutable backups are the single most effective mitigation against ransomware impact
- **Indicators of Compromise (IOCs)**: mass file renaming, sudden extension changes (`.locked`), ransom note drops, unusual outbound connections to a C2 endpoint
- **Defense-in-depth ideas**: endpoint detection (EDR) for abnormal file I/O patterns, network segmentation to limit C2 reachability, application allow-listing, user awareness training
- **Why visibility into C2 behavior matters**: understanding how attackers track and manage victims helps blue teams build better detection logic (e.g., anomalous panel traffic patterns, beaconing)

---

## 🛠️ Tech Stack

> _(Isi sesuai yang kamu pakai — contoh di bawah, silakan sesuaikan)_

- **Victim-side UI**: Python / Tkinter (atau sebutkan bahasa/framework yang kamu pakai)
- **C2 Dashboard**: Flask / Python (web-based control panel)
- **Environment**: Isolated VM (Windows target), local-only network (127.0.0.1)

---

## 📂 Repository Structure (suggested)

```
.
├── README.md
├── assets/                  # screenshots used in this README
│   ├── before-simulation.png
│   ├── ransomeware-aktif.png
│   ├── menampilkanpesan_dari_si_attaker.png
│   ├── Invalid-Key.png
│   ├── c2-dashboard.png
│   └── after-simulation.png
├── docs/
│   └── report.pdf           # laporan/presentasi lengkap (optional)
└── LICENSE
```

> **Catatan keamanan:** Sengaja *tidak* menyertakan folder source code payload/C2 secara penuh dan dapat dieksekusi langsung di repo publik ini. Kalau kamu tetap ingin menyertakan kode, pertimbangkan: (1) hanya source yang sudah dijelaskan konsepnya di laporan, (2) tambahkan `.gitignore` untuk file hasil build (`.exe`), (3) jangan sertakan key/credential asli, dan (4) cantumkan disclaimer ini juga di bagian atas setiap file kode.

---

## 📄 Full Report

A detailed write-up/presentation of this project (methodology, tools used, and conclusions) is available in [`docs/report.pdf`](docs/report.pdf).

---

## 📬 Contact

Feel free to reach out if you'd like to discuss this project or cybersecurity topics in general.

---

*Built as part of a cybersecurity learning project. Shared for educational purposes only.*
