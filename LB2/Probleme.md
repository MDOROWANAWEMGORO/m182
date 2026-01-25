# Probleme

### Telnet hat nicht funktioniert:

Das installierte Telnet unit konnte nicht gefunden werden
![](Screenshots/Telnetnotfound.png)

Telnet war aus?
![](Screenshots/TelnetOff.png)

Wir mussten den Telnet "Superserver" installieren:

```bash
sudo apt install telnetd inetutils-inetd -y
```

Danach hat Telnet funktioniert:
![](Screenshots/TelnetUp.png)

---