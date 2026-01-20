# Dokumentation der Attacke – MITM-Attacke im Labor

---

## 1️ Wireshark Capture-Filter

```text
tcp port 23
```

### Erklärung:

* `tcp` → filtert nur TCP-Verkehr
* `port 23` → Telnet nutzt standardmässig Port 23

**Zweck:**
Reduziert die aufgezeichneten Pakete auf Telnet-Kommunikation, um Klartextdaten gezielt zu analysieren.

---

## 2️ IP-Weiterleitung aktivieren (Kali)

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

### Erklärung:

* `sysctl` → verändert Kernel-Parameter
* `net.ipv4.ip_forward` → erlaubt das Weiterleiten von IP-Paketen
* `=1` → aktiviert Forwarding

**Warum notwendig?**
Ohne IP-Forwarding würde Kali Pakete empfangen, aber **nicht weiterleiten** → Verbindung bricht ab.

---

## 3️ ARP-Spoofing starten (Kali)

### Befehl 1:

```bash
sudo arpspoof -i ens33 -t 192.168.56.10 192.168.56.20
```

### Erklärung:

* `arpspoof` → sendet gefälschte ARP-Antworten
* `-i ens33` → verwendetes Netzwerkinterface
* `-t 192.168.56.10` → Ziel (Windows Client)
* `192.168.56.20` → vorgetäuschte IP (Ubuntu Server)

**Wirkung:**
Der Client glaubt, der Server habe die MAC-Adresse von Kali.

---

### Befehl 2:

```bash
sudo arpspoof -i ens33 -t 192.168.56.20 192.168.56.10
```

**Wirkung:**
Der Server glaubt, der Client habe die MAC-Adresse von Kali.

**Ergebnis:**
Kali positioniert sich **zwischen Client und Server** (Man-in-the-Middle).

---

## 4️ ARP-Tabelle anzeigen

### Windows:

```cmd
arp -a
```

### Linux:

```bash
ip neigh
```

### Erklärung:

Zeigt die Zuordnung von IP- zu MAC-Adressen.

**Beobachtung im Angriff:**
Client und Server zeigen **die MAC-Adresse von Kali** für die jeweilige Gegenstelle.

---

## 5️ Wireshark Display-Filter

```text
tcp.port == 23
```

### Erklärung:

* Display-Filter → filtert bereits aufgezeichnete Pakete
* `==` → Vergleichsoperator
* `23` → Telnet-Port

**Zweck:**
Gezielte Analyse von Telnet-Datenströmen.

---

## 6️ TCP-Stream analysieren

```text
Follow → TCP Stream
```

### Erklärung:

* Rekonstruiert die komplette Sitzung
* Stellt Client- und Serverdaten übersichtlich dar

**Ergebnis:**

* Benutzername
* Passwort
* eingegebene Befehle
  → **alles im Klartext sichtbar**

---

## 7️ Telnet-Verbindung herstellen (Windows)

```cmd
telnet 192.168.56.20
```

### Erklärung:

* Baut eine unverschlüsselte Telnet-Verbindung auf
* Login-Daten werden direkt übertragen

**Relevanz:**
Demonstriert die Unsicherheit von Klartextprotokollen.

---

## 8️ Angriff beenden

```text
CTRL + C
```

### Erklärung:

Beendet den laufenden `arpspoof`-Prozess.

**Warum wichtig?**
ARP-Manipulation bleibt sonst aktiv und stört das Netzwerk.

---

## 9 ARP-Cache leeren

### Windows:

```cmd
arp -d *
```

### Linux:

```bash
sudo ip neigh flush all
```

### Erklärung:

* Entfernt manipulierte ARP-Einträge
* Erzwingt neue, korrekte ARP-Auflösung

**Zweck:**
Wiederherstellung des normalen Netzwerkbetriebs.

---

## 10 Warum Telnet schlechter als SSH ist (nach der Befehlsanalyse)

## Beobachtung aus dem Laborversuch

Während der MITM-Attacke konnten wir mit Wireshark:

* Benutzername
* Passwort
* ausgeführte Befehle
* Sitzungsinhalte

vollständig **im Klartext** aus dem Telnet-Datenstrom gelesen werden. Sowohl **ohne** als auch **mit** ARP-Spoofing.

---

## Technischer Vergleich: Telnet vs. SSH

### Telnet (Port 23)

**Eigenschaften:**

* Keine Verschlüsselung
* Keine Integritätsprüfung
* Keine Authentizität des Servers
* Jeder MITM kann Daten:

  * mitlesen
  * verändern
  * neu einspeisen

**Konsequenz im Angriff:**

> Sobald der Angreifer den Verkehr umleitet (z. B. per ARP-Spoofing), sind alle Zugangsdaten kompromittiert.

---

### SSH (Port 22)

**Eigenschaften:**

* Ende-zu-Ende-Verschlüsselung (z. B. AES)
* Integritätsprüfung (MAC/HMAC)
* Server-Authentifizierung über Host Keys
* Schutz vor Replay- und Manipulationsangriffen

**Konsequenz im Angriff:**

* ARP-Spoofing ist weiterhin möglich
* **Inhalt bleibt unlesbar**
* Manipulation wird erkannt
* Login-Daten sind geschützt

**Wireshark zeigt nur verschlüsselte Daten**

So hat in unserer Laborumgebung mit ssh ausgesehen:
![]()

---

## Warum hilft ARP-Spoofing bei SSH nicht?

ARP-Spoofing beeinflusst nur **den Transportweg**, nicht die **Inhaltssicherheit**.

| Ebene                | Telnet  | SSH     |
| -------------------- | ------- | ------- |
| ARP-Manipulation     | möglich | möglich |
| Verkehr umleiten     | Ja      | Nein      |
| Inhalt lesen         | Ja      | Nein       |
| Inhalt verändern     | Ja      | Nein       |
| Login-Daten sichtbar | Ja      | Nein       |

**Der Angriff scheitert an der Verschlüsselung**, nicht am Netzwerk.

---

## Sicherheitsbewertung

> Telnet ist aus heutiger Sicht als unsicher einzustufen, da es keinerlei Schutzmechanismen gegen Abhören oder Manipulation bietet. Selbst in lokalen Netzwerken können Anmeldedaten kompromittiert werden. SSH hingegen schützt die Kommunikation durch starke Verschlüsselung und Integritätsprüfungen und verhindert so eine erfolgreiche Auswertung des Datenverkehrs trotz Man-in-the-Middle-Angriff.

---

## Praxisrelevante Schlussfolgerung

* Unsichere Protokolle sind **nicht mehr zeitgemäss**
* Verschlüsselung ist **zwingend erforderlich**
* Netzwerkangriffe sind oft **einfacher als angenommen**
* Sicherheit muss **mehrschichtig** erfolgen

---

## Zusammenfassung

> Durch die Aktivierung der IP-Weiterleitung und gezieltes ARP-Spoofing konnte das Angreifer-System zwischen Client und Server positioniert werden. Die Analyse des Telnet-Verkehrs mittels Wireshark zeigte, dass sämtliche Zugangsdaten im Klartext übertragen wurden. Der Angriff verdeutlicht die Risiken unsicherer Protokolle sowie die fehlende Authentifizierung des ARP-Protokolls.
