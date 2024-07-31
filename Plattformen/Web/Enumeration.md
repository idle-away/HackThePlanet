#web/enum 

---
## Well known Ports

#well-known/ports

| Port | Protokoll   | Dienst            |
| ---- | ----------- | ----------------- |
| 21   | TCP/UDP     | FTP               |
| 22   | TCP/UDP     | SSH               |
| 23   | TCP         | Telnet            |
| 25   | TCP         | SMTP              |
| 53   | TCP/**UDP** | DNS               |
| 80   | TCP/UDP     | HTTP              |
| 88   | TCP/UDP     | Kerberos          |
| 143  | TCP/UDP     | IMAP              |
| 161  | TCP/UDP     | SNMP              |
| 389  | TCP/UDP     | LDAP              |
| 443  | TCP/UDP     | HTTPS             |
| 445  | TCP         | SMB               |
| 3306 | TCP/UDP     | MySQL DB System   |
| 3389 | TCP/UDP     | Windows RDP       |
| 8080 | TCP/UDP     | Alternative HTTP  |
| 8443 | TCP/UDP     | Alternative HTTPS |

---
## Dienste identifizieren

Schneller scan erreichbarer Dienste mit Versions Erkennung:
```bash
nmap -sCV --min-rate 1500 -v 10 10.10.11.12 -oA nmap/script1k
```

Gleicher Scan über alle Ports:
```bash
nmap -sCV --min-rate 1500 -v -p- 10 10.10.11.12 -oA nmap/script1k
```

### FTP

| **Kommando**                                                             | **Beschreibung**                                |
| ------------------------------------------------------------------------ | ----------------------------------------------- |
| `ftp 192.168.2.142`                                                      | Verbindung zum FTP Server mit dem `ftp` Client. |
| `nc -v 192.168.2.142 21`                                                 | Verbindung zum Ftp Server mit `netcat`.         |
| `hydra -l user1 -P /usr/share/wordlists/rockyou.txt ftp://192.168.2.142` | FTP Server Zugang erraten mit `hydra`.          |

---

## Webdienst Analyse

Es ist hilfreich zu wissen mit welchen Technologien man konfrontiert wird. Um einen Einblick zu bekommen kann zum Beispiel das Firefox Browser Addon [wappalyzer](https://www.wappalyzer.com/) benutzt werden. Alternativ können per Kommandozeilen Tool `whatweb` ähnliche Informationen angezeigt werden.

Erfahrenswerte Informationen sind:
- Verwendete Software in Version
- Verwendeter Webserver in Version

Mit diesen Vorinformationen wird "aufdecken" der Website einfacher. Angenommen Wappalyzer zeigt uns die Verwendung von Wordpress an, daraus können wir ableiten, dass einen Login zur WP-Adminseite geben sollte sowie dass PHP im Einsatz ist.

---
## Virtual Hosts/Subdomains

Oft kommt es vor, dass ein Webserver mehrere VHosts bzw. Subdomains bereitstellt. Entweder laufen auf den VHosts eigenständige Webdienste oder irgendwo anders eingebundene Webdienste. Ein Indiz für eingebundene Dienste sind zum Beispiel fehlgeschlagene API Aufrufe und dem entsprechend fehlender Inhalt auf der Webseite oder Links in denen die Ressource mit Namen definiert ist z.B. `api.example.com`.

Eine andere Möglichkeit VHosts bzw. Subdomains zu erraten ist Fuzzing. [[ffuf]] ist ein Kommandozeilen Tool mit dem dies umgesetzt werden kann.

```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.blazorized.htb" -u http://blazorized.htb/
```

Wenn die Liste zu viel False/Positive Einträge enthält kann die Ausgabe mit Filter Optionen angepasst werden.

```bash
-fc     # Filter HTTP status codes from response. 200,204,301
-fl     # Filter by amount of lines in response. 0,2,16
-fmode  # Filter set operator. Either of: and, or (default: or)
-fr     # Filter regexp
-fs     # Filter HTTP response size.  
-ft     # Filter by number of milliseconds to the first response byte, either greater or less than. EG: >100 or <100
-fw     # Filter by amount of words in response.
```

Wenn die `subdomains-top1million-110000` nichts ausspuckt, sollte noch eine andere Liste probiert werden.

---
## Endpunkte und Dateien

Webdienste können verschieden aufgebaut sein, je mehr Informationen vorliegen vereinfacht es das weitere Vorgehen indem spezifischere Listen zum Fuzzing verwendet werden können.

Mit [[ffuf]] ist ein suchen nach Endpunkte möglich

```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/quickhits.txt -u targeturl/FUZZ
```

Interessante Listen sind:
```
/usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
/usr/share/wordlists/seclists/Discovery/Web-Content/quickhits.txt
/usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```

Um nach Dateien zu suchen müssen die gewünschten Endungen angegeben werden. Entweder entwirft man dafür eine extra Liste, die gewünschte Dateinamen mit Endungen enthält oder die gibt Flag `-e` und die gewünschte Dateiendung als Komma separierte Liste

```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/quickhits.txt -u targeturl/FUZZ -e .pdf,.docx
```

---
## Quick wins

### Tomcat manager

#### Versions Identifikation

```bash
curl -s http://tomcat-site.local:8080/docs/ | grep Tomcat 
```

#### Manager plugin lokalisieren

Default läuft das Manager Plugin unter `/manager` oder `/host-manager`. Der Pfad kann aber auch angepasst werden. In dem Fall muss danach gefuzzed werden.

#### Credentials

Der Zugriff zur Seite ist in der Regel mit Basic Auth geschützt kann also simpel geraten werden.

[[hydra]] ist ein Bruteforce tool das Basic Auth unterstützt
```bash
hydra -L users.txt -P /usr/share/seclists/Passwords/darkweb2017-top1000.txt -f 10.10.10.64 http-get /manager/html
```

Alternativ kann dies auch über [[MSF]] überprüft werden. Das entsprechende Modul ist `auxiliary/scanner/http/tomcat_mgr_login`.

---

## Todo's

- [x] Web Enumeration Seite erstellt ➕ 2024-07-27 ✅ 2024-07-27
- [x] Web Enumeration Quick Wins Tomcat Manager ➕ 2024-07-27 ✅ 2024-07-27
- [x] Web Enum VHost/Sudomain Enumeration ➕ 2024-07-27 ✅ 2024-07-27
- [x] Web Enum Endpunkte, Ordner und Dateien ➕ 2024-07-27 ✅ 2024-07-27
- [x] Web Enum Dienste identifizieren ➕ 2024-07-27 ✅ 2024-07-27
- [x] Web Enum Well Known Ports ➕ 2024-07-27 ✅ 2024-07-27
- [x] Web Enum Webdienst Analyse ➕ 2024-07-27 ✅ 2024-07-27
- [ ] Web Enum Quick Wins Tomcat Manager RCE ➕ 2024-07-27
- [ ] Web Enum Client Side Applications ➕ 2024-07-27
- [ ] Web Enum Nmap lInk und Nmap Tool Page ➕ 2024-07-27