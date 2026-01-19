# Dokumentation der Attacke als Plan

**Kurzfassung**
Sicheres, isoliertes Labor-Szenario: ARP-basierter Man-in-the-Middle (MITM) in einer Host-Only-VM-Umgebung zur Demonstration, wie unverschlüsselte Protokolle (Telnet, FTP, HTTP, POP3) Klartextdaten preisgeben. Nur im isolierten Labor durchführen.

# Lernziele

* Rolle von ARP und Funktionsweise eines ARP-MITM verstehen.
* Sichtbar machen von Klartext-Credentials in Telnet/FTP/HTTP.
* Analyse von PCAPs mit Wireshark; Erkennen von MITM-Indikatoren.
* Gegenmassnahmen (SSH, HTTPS/TLS) aufzeigen.

# Voraussetzungen

* VMware Workstation, Host-Only Netzwerk (keine Internetverbindung).
* VMs: Client (Windows, Telnet-Client), Server (Ubuntu, Telnet/optional FTP/HTTP/POP3), Angreifer (Kali, Wireshark).
* Snapshots vor jedem Versuch; Speicher für PCAPs/Screenshots.

# Sicherheitsregeln

* Nur in vollständig isolierter Umgebung.
* Snapshots erstellen; Aktionen protokollieren.
* Keine Tests in produktiven oder fremden Netzwerken.

# Ablauf

1. Snapshots erstellen; ARP-Tabellen dokumentieren.
2. Basiscapture (Wireshark) durchführen; Telnet-Login referenziell mitschneiden.
3. ARP-Manipulation (Angreifer leitet Verkehr um) — Capture starten.
4. Erneute Telnet/FTP/HTTP-Sessions ausführen; ARP-Tabellen vergleichen.
5. Wiederherstellen (ARP bereinigen / Snapshot zurückspielen).
6. PCAPs sichern und analysieren.

# Wireshark — Wichtige Filter & Indikatoren

* `arp` — ARP-Traffic
* `tcp.port == 23` (Telnet), `tcp.port == 21` (FTP), `http.request` (HTTP)
* TCP-Stream: Rechtsklick → *Follow* → *TCP Stream* (zeigt Klartext)
* MITM-Indikatoren: unterschiedliche MACs für dieselbe IP, ARP-Replies vom Angreifer, asymmetrische Ethernet-MACs in Paketen

# Erwartete Befunde

* Vorher: direkte Client↔Server-Kommunikation; Klartext-Credentials sichtbar.
* Während MITM: ARP-Replies mit falscher MAC; Verkehr läuft über Angreifer; Klartext bleibt sichtbar.

# Dokumentation

Für jedes Szenario: Datum, Ziel, Hosts (Name/IP/MAC), Snapshot-ID, Aktionen, Beobachtungen (ARP-Tabellen, Wireshark-Screenshots), Interpretation, Gegenmassnahmen.

# Gegenmassnahmen

* Telnet → SSH; HTTP → HTTPS/TLS; FTP → SFTP/FTPS.
* Netzwerk-Härtung: DHCP-Snooping, Dynamic ARP Inspection, 802.1X, Port-Security.
* Monitoring / IDS-Regeln für ungewöhnliche ARP-Aktivität.

# Checkliste

* Snapshots erstellt
* Baseline-PCAP gespeichert
* MITM-PCAP gespeichert
* ARP-Tabellen dokumentiert (Vor/Nach)
* Journal & Screenshots vorhanden
