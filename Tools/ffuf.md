
#ffuf 

Fuzz faster you fool ist ein fuzzing/webenumeration tool.

-------
## Quelle

Link zum [ffuf github repo](https://github.com/ffuf/ffuf)

## Installation

Binaries zum direkten ausführen sind auf der Releasepage im Git.
Binary nach `/usr/bin` verschieben und die Rechte anpassen.

---------
## TLDR Usage

Webdir fuzzing:
```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://blazorized.htb/FUZZ -c
```

Subdomain fuzzing  (bei zu vielen false positives auf einen gleichbleibenden parameter filtern):
```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.blazorized.htb" -u http://blazorized.htb/  -c

# Filter auf Größe 153
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.blazorized.htb" -u http://blazorized.htb/  -c -fs 153
```

Outputfile schreiben:
```bash
-o web/PORT-WORDLIST
```

Outputfile filtern und neuschreiben:
```bash
cat ffuf/PORT-LISTE | jq -c '.results[] | {status: .status, url: .url}' | jq -s 'sort_by(.status)' | jq -r '.[] | "\(.status),\(.url)"' | tee ffuf/PORT-LISTE
```

## Cheatsheet
#cheatsheet-toolname

| **Command** | **Description** |
| --------------|-------------------|
| `ffuf -h` | ffuf help |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ` | Directory Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/indexFUZZ` | Extension Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/blog/FUZZ.php` | Page Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v` | Recursive Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u https://FUZZ.hackthebox.eu/` | Sub-domain Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb' -fs xxx` | VHost Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx` | Parameter Fuzzing - GET |
| `ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx` | Parameter Fuzzing - POST |
| `ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx` | Value Fuzzing |

## Wordlists

| **Command** | **Description** |
| --------------|-------------------|
| `/opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt` | Directory/Page Wordlist |
| `/opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt` | Extensions Wordlist |
| `/opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt` | Domain Wordlist |
| `/opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt` | Parameters Wordlist |

## Misc

| **Command** | **Description** |
| --------------|-------------------|
| `sudo sh -c 'echo "SERVER_IP academy.htb" >> /etc/hosts'` | Add DNS entry |
| `for i in $(seq 1 1000); do echo $i >> ids.txt; done` | Create Sequence Wordlist |
| `curl http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=key' -H 'Content-Type: application/x-www-form-urlencoded'` | curl w/ POST |

## Todos

- [x] ffuf-tool page
- [x] Installation
- [x] Cheatsheets übertragen
- [x] TLDR Usage