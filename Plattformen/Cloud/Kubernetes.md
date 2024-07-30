
Vorausgesetzte Tools:
- [[kubectl]]

Optionale Tools:
- [[Kubescape]]

---

## Cluster Role Bindings und Role Binding

## RBAC

## Secrets

Alle Secrets abrufen:
`k get secrets -A`
Alle Secrets eines Namespaces abrufen:
`k get secrets -n mynamespace`
Bestimmtes Secret in Namespace abrufen:
`k get secrets -n mynamespace mysecret -o yaml`

### Pull secrets

Mit Pull secrets ist es möglich von einem Imagerepository images zu laden. Das Secret kann ich den meisten Fällen auch dazu benutzt werden, vorhandene Images im Repository zu updaten bzw zu ersetzten.

## Image Repositories

### Nexus

[How to](https://github.com/travelaudience/kubernetes-nexus/blob/master/docs/usage/using-nexus-with-docker.md)

## Pods

## Namespaces

## Tools

Kubescape 

```
kubescape scan framework AllControls --format-version=v1 --format json --output kubescape-AllControls.json
 ```

---

## ToDo's

- [ ] Informieren Lynis ➕ 2024-07-30
- [ ] Tooling Kubescape ➕ 2024-07-30 
- [ ] Informieren konstellation (RBAC) ➕ 2024-07-30 