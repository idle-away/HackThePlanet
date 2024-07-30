#kubectl 
#tool/kubectl

Kommandozeilen Tool zur integration von Kunbernetes

-------
## Quelle


Link zum [tool](https://kubernetes.io/de/docs/tasks/tools/install-kubectl/)

## Installation
#kubectl/install
#tool/kubectl/install

### Via Curl

```bash
curl -LS https://dl.k8s.io/release/stable.txt
curl -LO https://dl.k8s.io/release/$(curl -LS https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

### Alias and Autocompletion

```bash
echo 'alias k="kubectl"'
echo 'source <(kubectl completion zsh)' >> ~/.zshrc
```

### Default config

Die Konfigurationsdatei für Kubectl ist im Verzeichnis `.kube` des Benutzers `~/.kube/config`

#### Interessante config file flags

Wenn ein Jumphost zur Kommunikation benutzt wird, kann der entsprechende Proxy zum Cluster gesetzt werden. Der Key ist `proxy-url` und sollte dann auf den selbst geöffneten socks proxy zeigen.

### Plugins

Um Plugins für kubectl zu benutzen muss [krew](https://krew.sigs.k8s.io/docs/user-guide/setup/install/) installiert werden.

**Bash or Zsh**

```sh
(
  set -x; cd "$(mktemp -d)" &&
  OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
  KREW="krew-${OS}_${ARCH}" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
  tar zxvf "${KREW}.tar.gz" &&
  ./"${KREW}" install krew
)
```

```sh
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
```

Mit `kubectl krew version` überprüfen ob die Installation gelungen ist.

Plugins werden dann wie folgt installiert:

`kubectl krew install PLUGINNAME`

---------

## TLDR Usage


## Cheatsheet
#kubectl/cheatsheet
#cheatsheet/kubectl


### Kubernetes Quick Reference

[Kubernetes Quick Reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

## Todo's
- [x] Tool kubectl erstellt ➕ 2024-07-27 ✅ 2024-07-30