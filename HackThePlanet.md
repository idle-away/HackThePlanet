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

**Shortcuts**

| Combination | Command Palette     |
| ----------- | ------------------- |
| CTRL+P      | Commando Pallete    |
| CTRL+O      | Find or create Node |

## Standards

**TAGS**
 - Tags werden klein geschrieben (sind eh case insensitive)
 - Tags werden mit `/` genested
 
## Aufgaben

### In Arbeit
```tasks
filter by function task.status.type === "IN_PROGRESS"
```

### Offene Aufgaben
```tasks
not done
```

### Erledigte Aufgaben
```tasks
done
```

- [ ] Templates entwerfen
	- [ ] Exploit
	- [ ] Tool
	- [ ] Writeup
- [ ] Cheatsheets
- [ ] Techniken und Verfahren
- [ ] Systemsetup
