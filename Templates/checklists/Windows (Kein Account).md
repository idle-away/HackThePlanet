
## Test Setup

Solange Konfigurationen nicht permanent angewandt werden, müssen diese nach **jedem Neustart** neu gesetzt werden.

### Scope definieren:

- [ ] Setup: scope.list erstellen ➕ {{date}}

```bash
echo "scopeip,\nscopeip2" > scope.list
```

### Traffic an nicht in Scope Adressen blocken:

- [ ] Setup: exclude.list erstellen ➕ {{date}}

```bash
echo "excludeip,\nexcludeip1" > exclude.list
```

**Blocken der Adressen**

```bash
for HOST in `cat exclude.list` do; sudo iptables -A OUTPUT -d $HOST -j DROP && echo "$HOST is now ignored" done; sudo iptables -L OUTPUT
```

### DNS

Eintragen des DNS-Servers

```bash
echo "dns-ip" >> /etc/respf.conf
```

---
## Todo's

### Zu Erledigen

```tasks
path includes {{query.file.path}}
limit 10
```

### Funde

```tasks
done
path includes {{query.file.path}}
limit 10
```

### Abgearbeitet
```tasks
canceled
path includes {{query.file.path}}
limit 10
```
---
### Nessus

### Dienste

#### Datenbanken

#### FTP

Liste aller FTP Server erstellen:

#### SMB

#### Webserver
