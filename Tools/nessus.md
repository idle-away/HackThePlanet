#nessus
#tool/nessus

## Lizenz erneuern

Nessus stoppen

```bash
sudo systemctl stop nessusd.service
```

Neue Lizenz aktivieren:

```bash
/opt/nessus/sbin/nessuscli fetch --register ACTIVATIONCODE
```