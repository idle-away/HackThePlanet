
## Powershell Benutzer erstellen

```powershell
New-ADUser -Name "pwn" -SamAccountName "pwn" -AccountPassword (ConvertTo-SecureString "<pass>" -AsPlainText -Force) -Enabled $true -Description "pwnage"
```

[[#Powershell Benutzer zu Gruppe hinzufügen]]

## Powershell Benutzerliste erstellen

```powershell
get-domainuser | select samaccountname | out-file -encoding utf8 user_list.txt
```

## Powershell Benutzer zu Gruppe hinzufügen

[[#Powershell Benutzer erstellen]]

```powershell
Add-LocalGroupMember -Group Administrators -Member "pwn"
```

## Powershell Credentials

### Credential Objekt erstellen

```powershell
$SecPassword = ConvertTo-SecureString 'Password' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential('DOMAIN\USER', $SecPassword)
```

### One-Liner Ersatz für $cred

```powershell
(New-Object System.Management.Automation.PSCredential ("USER", (ConvertTo-SecureString "PASS" -AsPlainText -Force)))
```

## Powershell Domain Shares

Vorraussetzungen:
- [[#Credential Objekt erstellen]]

```powershell
Find-DomainShare -Domain testlab.local -CheckShareAccess -Credential $Cred
```

## Powershell Kerberos

### Kerberos Tickets anzeigen

```powershell
klist
```

## Powershell Remoting

Vorraussetzungen:
- [[#Powershell Credentials]]

Ein anderes Feature von WinRM ist Powershell remoting. Wie der Name sagt eine Powershell Session auf einem anderen System.

```powershell
# Session initiieren
New-PSSession -ComputerName IPADDRESS -Credential $Cred

# Zum interagieren mit der Session muss diese betreten werden
Enter-PSSession SESSID
```


## Powershell Routen

```powershell
route add ZIELNETZ mask ZIELMASK GATEWAY
```

