---
title: Terraform Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Terraform Basics: Provider, State, Modules & Workspaces

Dieses Sheet bündelt die wichtigsten Terraform‑Konzepte für Infrastructure‑as‑Code, reproduzierbare Deployments und modulare Cloud‑Architekturen.

---

## ❓ Wie initialisiere ich ein Terraform‑Projekt?
**Lösung:** init lädt Provider & Module.

```bash
terraform init
```

---

## ❓ Wie plane und applye ich Änderungen?
**Lösung:** plan → apply.

```bash
terraform plan
terraform apply
```

Automatisch bestätigen:

```bash
terraform apply -auto-approve
```

---

## ❓ Wie definiere ich Provider?
**Lösung:** provider‑Block.

```hcl
provider "aws" {
  region = "eu-central-1"
}
```

---

## ❓ Wie definiere ich Ressourcen?
**Lösung:** resource‑Block.

```hcl
resource "aws_s3_bucket" "assets" {
  bucket = "my-assets"
}
```

---

## ❓ Wie nutze ich Variablen?
**Lösung:** variables + terraform.tfvars.

```hcl
variable "env" {
  type = string
}

output "env" {
  value = var.env
}
```

terraform.tfvars:

```hcl
env = "prod"
```

---

## ❓ Wie nutze ich Outputs?
**Lösung:** output‑Block.

```hcl
output "bucket_name" {
  value = aws_s3_bucket.assets.bucket
}
```

---

## ❓ Wie funktionieren Module?
**Lösung:** module‑Block.

```hcl
module "network" {
  source = "./modules/network"
  cidr   = "10.0.0.0/16"
}
```

Remote Module:

```hcl
source = "git::https://github.com/org/repo.git//vpc"
```

---

## ❓ Wie funktioniert der Terraform State?
**Lösung:** state hält den Ist‑Zustand.

Wichtige Befehle:

```bash
terraform state list
terraform state show <resource>
```

Remote Backend (Beispiel S3):

```hcl
backend "s3" {
  bucket = "tf-state"
  key    = "prod/terraform.tfstate"
  region = "eu-central-1"
}
```

---

## ❓ Wie mache ich Destroy?
**Lösung:** Infrastruktur löschen.

```bash
terraform destroy
```

---

## ❓ Wie arbeite ich mit Workspaces?
**Lösung:** mehrere Umgebungen.

```bash
terraform workspace new staging
terraform workspace select staging
terraform workspace list
```

---

## ❓ Wie verhindere ich Drift?
**Lösung:** refresh & plan.

```bash
terraform plan -refresh=true
```

---

## ❓ Wie formatiere ich Code?
**Lösung:** fmt.

```bash
terraform fmt
```

---

## ❓ Wie prüfe ich Codequalität?
**Lösung:** validate.

```bash
terraform validate
```

---

## ❓ Wie nutze ich Data Sources?
**Lösung:** externe Ressourcen lesen.

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]
  filter {
    name   = "name"
    values = ["ubuntu/images/*"]
  }
}
```

---

## ❓ Wie setze ich Lifecycle‑Regeln?
**Lösung:** create_before_destroy, prevent_destroy.

```hcl
lifecycle {
  create_before_destroy = true
}
```

---

## ❓ Wie verhindere ich versehentliches Löschen?
**Lösung:** prevent_destroy.

```hcl
lifecycle {
  prevent_destroy = true
}
```

---

## Pro-Tipp
Nutze **Module + Remote State + Workspaces**, um reproduzierbare, teamfähige IaC‑Pipelines zu bauen — Terraform wird erst dadurch wirklich skalierbar.
