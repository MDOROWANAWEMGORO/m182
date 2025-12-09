# Projektantrag – Analyse von Netzwerksicherheitsrisiken in virtuellen Testumgebungen

## 1. Projekttitel
**Analyse unsicherer Netzwerkprotokolle und Man-in-the-Middle-Szenarien mit Wireshark“**

---

## 2. Ausgangslage
In vielen Netzwerkumgebungen finden sich weiterhin ältere Dienste wie Telnet, FTP oder unverschlüsseltes HTTP. Diese Protokolle übertragen Daten ohne jegliche Schutzmechanismen. Dadurch können Zugangsdaten, Befehle oder persönliche Informationen leicht abgefangen und manipuliert werden.

Um diese Risiken realistisch, aber gefahrlos demonstrieren zu können, wird eine vollständig isolierte Laborumgebung mit mehreren virtuellen Maschinen aufgebaut.

---

## 3. Motivation
Das Projekt dient dazu, ein Bewusstsein für veraltete und unsichere Netzwerkprotokolle zu schaffen.  
Durch praktische Analyse mit Wireshark und ergänzenden Tools sollen typische Schwachstellen nachvollziehbar gemacht werden.

Zudem soll gezeigt werden, wie moderne Sicherheitsmechanismen solche Risiken reduzieren.

---

## 4. Projektziel
Erstellung eines Screencasts mit begleitender Dokumentation, das:

- den Aufbau einer Testumgebung erklärt  
- die Analyse unverschlüsselter Netzwerkkommunikation demonstriert  
- zeigt, wie Login-Daten und Nutzlasten in Klartextprotokollen sichtbar werden  
- ein Man-in-the-Middle-Szenario (ARP-Manipulation) erkennt und auswertet  
- Vergleiche zu sicheren Alternativen liefert (SSH, HTTPS, TLS)  

---

## 5. Umfang und Inhalte

### 5.1 Grundlagenmodul
- Erklärung der Funktionsweise von Netzwerkprotokollen  
- Rolle von ARP
- Einführung in Wireshark  

### 5.2 Praktisches Anwendermodul
- Aufbau eines Client Server Angreifer Netzwerks  
- Analyse eines regulären Telnet-Logins  
- Untersuchung der ARP-Tabelle und Vergleich vor/nach Manipulation  
- Identifikation sensibler Daten im Mitschnitt  
- Darstellung der Verkehrsumleitung im MITM-Fall

### 5.3 Vertiefungsmodul
- Erkennen von MITM-Angriffsmustern im Netzwerkverkehr  
- Vergleich verschiedener unsicherer Protokolle (Telnet, FTP, POP3, HTTP)  

---

## 6. Vorgehensmethodik

### 6.1 Konzeption
- Definition der Lern- und Demonstrationsziele  
- Erstellen eines Storyboards für das Tutorial  
- Planung des Laboraufbaus  

### 6.2 Umsetzung
- Konfiguration der VMs  
- Durchführung der Netzwerkcaptures  
- Dokumentation der Analyseszenarien  
- Aufnahme und Strukturierung des Screencasts  

### 6.3 Dokumentation
- Journal mit täglichem Fortschritt  
- Screenshots
- Reflexion zum Umgang mit komplexen Netzwerksituationen  
- Quellenverzeichnis  

---

## 7. Erwartete Ergebnisse
- Video im vorgegebenen Zeitrahmen  
- Vollständige technische Dokumentation  
- Vergleich von unsicheren und sicheren Netzwerkprotokollen  
- Analyse von Klartextdaten und protokollspezifischen Schwachstellen  
- Empfehlungen zur Absicherung der gezeigten Dienste  

---

## 8. Mehrwert & Bewertungskriterien

### Fachliche Tiefe
Kombination aus Grundlagenwissen, Praxisanalyse und MITM-Demonstration.

### Mediale Qualität
Klar strukturierter Screencast mit nachvollziehbaren Erklärungen.

### Dokumentation
Vollständig, mit Journal, Fehleranalyse, Screenshots und Quellen.

### Engagement
Erweiterte Betrachtung mehrerer Protokolle, realistische Angriffsszenarien

---


