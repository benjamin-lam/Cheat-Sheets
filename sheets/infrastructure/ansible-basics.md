---
title: Ansible Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Ansible Basics: Playbooks, Inventory, Roles & Idempotenz

Dieses Sheet bündelt die wichtigsten Ansible‑Konzepte für automatisierte Provisionierung, Konfigurationsmanagement und reproduzierbare Infrastruktur — ideal für Server‑Setups, CI/CD und Cloud‑Deployments.

---

## ❓ Wie funktioniert Ansible grundsätzlich?
**Lösung:** Agentlos, SSH‑basiert, deklarativ.

- Controller führt Playbooks aus  
- Targets brauchen nur SSH + Python  
- Tasks sind **idempotent** (mehrfach ausführbar ohne Seiteneffekte)  
- Inventory definiert Hosts & Gruppen  

---

## ❓ Wie sieht ein einfaches Inventory aus?
**Lösung:** INI‑Format.

```ini
[web]
web01 ansible_host=192.168.1.10
web02 ansible_host=192.168.1.11

[db]
db01 ansible_host=192.168.1.20
```

YAML‑Format:

```yaml
all:
  hosts:
    web01:
      ansible_host: 192.168.1.10
```

---

## ❓ Wie führe ich ein Playbook aus?
**Lösung:** ansible-playbook.

```bash
ansible-playbook site.yml
```

Nur bestimmte Hosts:

```bash
ansible-playbook site.yml -l web
```

---

## ❓ Wie sieht ein einfaches Playbook aus?
**Lösung:** YAML‑Struktur.

```yaml
- hosts: web
  become: true
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

---

## ❓ Wie führe ich Ad‑Hoc‑Befehle aus?
**Lösung:** ansible CLI.

```bash
ansible all -m ping
ansible web -m apt -a "name=nginx state=present" --become
```

---

## ❓ Wie funktionieren Variablen?
**Lösung:** vars, group_vars, host_vars.

Inline:

```yaml
vars:
  app_env: prod
```

group_vars/web.yml:

```yaml
app_port: 8080
```

---

## ❓ Wie verwende ich Templates?
**Lösung:** Jinja2‑Templates.

Playbook:

```yaml
- name: Render config
  template:
    src: app.conf.j2
    dest: /etc/app.conf
```

Template:

```jinja2
port = {{ app_port }}
env = {{ app_env }}
```

---

## ❓ Wie installiere ich Pakete?
**Lösung:** Module wie apt, yum, package.

```yaml
- name: Install nginx
  package:
    name: nginx
    state: present
```

---

## ❓ Wie kopiere ich Dateien?
**Lösung:** copy‑Modul.

```yaml
- name: Copy file
  copy:
    src: files/app.conf
    dest: /etc/app.conf
```

---

## ❓ Wie starte ich Services?
**Lösung:** service‑Modul.

```yaml
- name: Restart nginx
  service:
    name: nginx
    state: restarted
```

---

## ❓ Wie funktionieren Roles?
**Lösung:** Struktur für Wiederverwendung.

```text
roles/
  web/
    tasks/
    templates/
    handlers/
    vars/
    defaults/
```

Playbook:

```yaml
- hosts: web
  roles:
    - web
```

---

## ❓ Wie funktionieren Handlers?
**Lösung:** werden nur bei Änderungen ausgeführt.

Task:

```yaml
notify: restart nginx
```

Handler:

```yaml
- name: restart nginx
  service:
    name: nginx
    state: restarted
```

---

## ❓ Wie sichere ich Secrets?
**Lösung:** ansible-vault.

Datei verschlüsseln:

```bash
ansible-vault encrypt secrets.yml
```

Playbook mit Vault:

```bash
ansible-playbook site.yml --ask-vault-pass
```

---

## ❓ Wie teste ich Ansible?
**Lösung:** ansible-lint + Molecule.

Lint:

```bash
ansible-lint
```

Molecule:

```bash
molecule test
```

---

## Pro-Tipp
Nutze **Roles + group_vars + Templates**, um echte Infrastruktur‑Fabriken zu bauen — Ansible wird erst dadurch modular, reproduzierbar und teamfähig.
