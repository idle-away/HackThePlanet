Eine Knowledge Base rund um Pentesting und IT-Sicherheit

## Install

Auf die Version aufpassen beim installieren (lol)

```
wget -P ~/Downloads https://github.com/obsidianmd/obsidian-releases/releases/download/v1.6.7/obsidian_1.6.7_amd64.deb
sudo dpkg -i ~/Downloads/obsidian_1.6.7_amd64.deb
rm ~/Downloads/obsidian_1.6.7_amd64.deb
```

## Obsidian Hilfe

[Offizielle Hilfe Seite](https://help.obsidian.md/Home)
[Hilfe zu Tasks und Filtering](https://publish.obsidian.md/tasks/Introduction)

### Shortcuts

| Combination | Command Palette     |
| ----------- | ------------------- |
| CTRL+P      | Commando Palette    |
| CTRL+O      | Find or create Node |

## Standards

**TAGS**
 - Tags werden klein geschrieben (sind eh case insensitive)
 - Tags werden mit `/` genested
 
**Bilder und oder andere Dateien**
- Werden im Unterordner `res` des momentanen Ordners abgelegt.

**Tools**
- Tools sollen zu Writeups verlinken in denen diese benutzt werden um als weitere Hilfe zur Tool Nutzung zu dienen.

**Writeups**
- Writeups sollen zu benutzten Tools sowie Exploits verlinken
- Writeups zu aktiven Maschinen werden auf die `.gitignore` Liste gesetzt bis diese archiviert werden.

**Exploits**

## Templates

- [x] Template Writeup ➕ 2024-07-27 ✅ 2024-07-27
	- [x] Template Writeup Box tag ➕ 2024-07-27 ✅ 2024-07-27
	- [x] Template Writeup Box Header mit Datum und Autor ➕ 2024-07-27 ✅ 2024-07-27
	- [x] Template Writeup  Box Info für Provider, Typ und Schwierigkeit ➕ 2024-07-27 ✅ 2024-07-27
	- [x] Template Writeup Generelle Struktur Enum -> Foothold -> Privesc ➕ 2024-07-27 ✅ 2024-07-27
	- [x] Todo's für User/Root Flag und Veröffentlichung ➕ 2024-07-27 ✅ 2024-07-27
- [ ] Template Tool ➕ 2024-07-27
## Aufgaben

### In Arbeit
```tasks
filter by function task.status.type === "IN_PROGRESS"
```

### Offene Aufgaben
```tasks
not done
path does not include Templates
path does not include Writeups
```

### Erledigte Aufgaben
```tasks
done
```


## Writeups

## Publish me

```tasks
```

### Pwnd

```tasks
done
path includes Writeups
```