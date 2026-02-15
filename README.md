# 🎷 Zahni-Klarinetti

**Ein KI-gestützter musikalischer Begleiter für Klarinettisten.**
*Vom schnellen Töne-Check unterwegs bis zur professionellen Ansatz-Analyse zuhause.*

![Status](https://img.shields.io/badge/Status-In_Development-orange)
![Tech](https://img.shields.io/badge/Tech-Python_|_Django_|_OpenCV_|_TensorFlow-blue)
![Hardware](https://img.shields.io/badge/Hardware-NVIDIA_Jetson_Orin_|_Web-green)

## 🎵 Über das Projekt

Dieses Projekt ist mehr als nur ein Stimmgerät. Es ist ein intelligenter Übe-Partner ("Practice Companion"), entwickelt, um meiner Tochter (und mir) beim Klarinette-Lernen zu helfen. 

Anstatt nur zu sagen "falsch", analysiert **Zahni-Klarinetti** den **Klangcharakter**, den **Rhythmus** und (in der Home-Version) sogar die **Körperhaltung** und den **Ansatz**.

Wir vermeiden bewusst den Begriff "Coach". Musik ist Kunst, kein Sport. Dies hier ist ein geduldiger Zuhörer, der Feedback gibt.

---

## 🚀 Die 3 Modi (Architektur)

Dieses Repository ist ein **Monorepo**, das drei verschiedene Anwendungsfälle abdeckt:

### 1. 📱 Der Reise-Modus ("To Go")
Eine reine Web-Version, die ohne Server direkt im Browser auf dem Handy läuft. Perfekt für den Urlaub oder schnelles Einspielen.
* **Technik:** HTML5, JavaScript, `ml5.js` (TensorFlow.js), `p5.js`.
* **Features:** Tonhöhenerkennung, einfacher Notensatz, "Smartes Einzählen" (1-2-3-Atmen).
* **Demo:** [Hier klicken für die Live-Version](https://zahnilu.github.io/zahni-klarinetti) *(Link anpassen wenn aktiv)*
* **Code:** `/docs` (GitHub Pages)

### 2. 🏠 Der Studio-Modus ("Home Box")
Die volle Power für zuhause. Läuft auf einer dedizierten Hardware (NVIDIA Jetson Orin / "The Clawbox") neben dem Notenständer.
* **Technik:** Python, Django/FastAPI, Librosa (Audio), MediaPipe/OpenCV (Video), PyTorch (GPU beschleunigt).
* **Features:** * Latenzfreies Audio-Feedback.
    * **Ansatz-Check:** Kamera zoomt auf den Mund, warnt bei aufgeblasenen Wangen ("Frosch-Backen").
    * **Haltungs-Check:** Warnt bei hochgezogenen Schultern.
    * Speichern von Übe-Sessions.
* **Code:** `/src` + `/config/home`

### 3. ☁️ Der Demo-Modus ("VPS")
Eine Showcase-Version, die auf einem Cloud-Server (VPS) läuft, um die Python-Fähigkeiten unterwegs zu demonstrieren, ohne das Heimnetzwerk zu öffnen.
* **Technik:** Docker, Nginx, Django.
* **Features:** Upload von Aufnahmen zur Analyse, Streaming-Demo (ohne lokale Hardware-Zugriffe).
* **Code:** `/src` + `/config/vps`

---

## 📂 Ordnerstruktur

```text
zahni-klarinetti/
├── docs/                 # Statische Webseite (GitHub Pages / Mobile Version)
│   ├── index.html        # Der JS-Player
│   └── assets/           # Modelle für ml5.js
│
├── src/                  # Der Python-Kern (Für Home & VPS)
│   ├── analysis/         # Audio-Logik (Librosa) & Video-Logik (MediaPipe)
│   ├── web/              # Django App
│   └── manage.py
│
├── config/               # Docker & Environment Setups
│   ├── home/             # Docker Compose für Jetson (mit GPU/Cam Access)
│   └── vps/              # Docker Compose für Cloud Server
│
├── hardware/             # 3D-Druck-Dateien für die Box & Halterungen
└── requirements.txt      # Python Abhängigkeiten
