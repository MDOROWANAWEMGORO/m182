# IT-Infrastruktur-Dokumentation

## 1. Virtualisierungsplattform

Zur Umsetzung des Projekts wird eine Virtualisierungssoftware eingesetzt, um eine vollständig isolierte Testumgebung zu erstellen.

**Eingesetzte Plattformen:**
- VMware Workstation

**Netzwerkkonfiguration:**
- Host-Only Network 

Diese Netzwerkmodi stellen sicher, dass:
- kein Zugriff auf externe Netzwerke besteht
- alle Tests in einem abgeschlossenen Labor durchgeführt werden

---

## 2. Virtuelle Maschinen (Laboraufbau)

### 2.1 Client-System

**Betriebssystem:**
- Windows 10 / Windows 11  
 

**Zweck:**
- Aufbau einer Telnet-Verbindung zum Server
- Simulation eines regulären Benutzers im Netzwerk

**Installierte Software:**
- Telnet-Client  
  - z. B. PuTTY (Windows)


---

### 2.2 Server-System

**Betriebssystem:**
- Linux Ubuntu Server

**Zweck:**
- Bereitstellung unsicherer Netzwerkdienste

**Dienste:**
- Telnet-Server  
- Optional:
  - FTP
  - HTTP
  - POP3

**Rolle im Netzwerk:**
- Zielsystem der Netzwerkkommunikation
- Bereitstellung der zu analysierenden Dienste

---

### 2.3 Analyse- / Angreifer-System

**Betriebssystem:**
- Kali Linux

**Zweck:**
- Mitschnitt und Analyse des Netzwerkverkehrs
- Untersuchung von Man-in-the-Middle-Szenarien

**Installierte Software:**
- Wireshark
- Weitere Netzwerkanalyse-Tools

**Rolle im Netzwerk:**
- Beobachtung des Datenverkehrs
- Auswertung der aufgezeichneten Kommunikationsdaten

---

## 3. Netzwerkinfrastruktur

- Virtuelles lokales Netzwerk innerhalb der Virtualisierungssoftware
- Alle virtuellen Maschinen befinden sich im gleichen Subnetz
- Keine Internetverbindung erforderlich
- Kommunikation ausschließlich innerhalb des Labor-Netzwerks

---

## 4. Analyse- und Dokumentationssoftware

**Analysewerkzeuge:**
- Wireshark
  - Live-Capture von Netzwerkverkehr
  - Filterung und Protokollanalyse
  - TCP-Stream-Auswertung

**Dokumentation:**
- Screenshot-Tool 
- Textverarbeitung:
  - Markdown
  - Word
  - PDF-Export

---

## 5. Datenspeicherung

Lokaler Speicherplatz für:
- Netzwerkaufzeichnungen (PCAP-Dateien)
- Screenshots
- Projektbezogene Dokumentation

---

## 6. Sicherheits- und Rahmenbedingungen

- Vollständig isolierte Laborumgebung
- Keine produktiven oder realen Systeme beteiligt
- Keine Verbindung zu fremden Netzwerken
- Alle Analysen erfolgen ausschließlich zu Lern- und Demonstrationszwecken

---
