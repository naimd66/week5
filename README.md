# week5

# Week 5 – Infrastructure as Code: CI/CD

**Student:** naimd66  
**Datum:** 2025-05-29  
**Onderwerp:** Gebruik van AI tijdens practicumweek 5

---

## 📌 Instructie
In deze markdown worden alle AI-prompts en bijbehorende antwoorden opgenomen die gebruikt zijn bij de uitvoering van de opdrachten uit **week 5** van het vak Infrastructure as Code. Dit dient als bewijs voor het gebruik van AI volgens de beoordelingscriteria.

---

## 🔧 Opdracht 1: Ansible zonder apt-module

**Prompt:**
> Maak een playbook waarbij het pakket apache2 wordt geinstalleerd, maar niet via de apt module. En er moet een ‘Changed’ melding komen als het installeren gelukt is. Zorg er ook voor dat het in een andere taak fout gaat en Ansible netjes laat zien dat het fout gegaan is.

**AI-antwoord (samenvatting):**
Er werd een Ansible-playbook gemaakt met de `command` module om Apache te installeren:
```yaml
- name: Install Apache without using apt module
  command: "apt install -y apache2"
  register: apache_output
  changed_when: "'is already the newest version' not in apache_output.stdout"
```
Daarna werd een foutieve taak toegevoegd met een `fail` module:
```yaml
- name: Force failure for testing
  fail:
    msg: "Dit is een opzettelijke fout voor demonstratie."
```

---

## 🤖 Opdracht 2: GitHub Runner & Ansible CI/CD

**Prompt:**
> Installeer een lokale GitHub Runner en voeg deze toe aan je repository...

**AI-antwoord (samenvatting):**
Stap-voor-stap werd uitgelegd hoe een GitHub self-hosted runner wordt toegevoegd:
1. `mkdir actions-runner && cd actions-runner`
2. Download + extract runner tarball
3. Configureren met `./config.sh --url https://github.com/naimd66/week5 --token <TOKEN>`
4. Start met `./run.sh`

Daarna werd een workflow bestand aangemaakt:
```yaml
# .github/workflows/ansible-ci.yml
name: Run Ansible playbook on push

on:
  push:
    branches: [main]

jobs:
  run-ansible:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v3
      - name: Run Ansible Playbook
        run: ansible-playbook -i inventory.ini opdracht1.yml
```

---

## 🌍 Opdracht 3: Terraform + CI/CD

**Prompt:**
> Maak een terraform manifest waarbij je een simpele vm deployed...

**AI-antwoord (samenvatting):**
Een `main.tf` werd gemaakt met:
- `provider "azurerm"` config
- Een `azurerm_linux_virtual_machine` resource
- SSH-key en image configuratie
- `terraform.tfvars` en `variables.tf` toegevoegd

CI/CD workflow:
```yaml
# .github/workflows/terraform.yml
name: Terraform Plan & Apply

on:
  push:
    paths:
      - 'terraform/**.tf'

jobs:
  terraform:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v3
      - name: Init
        run: terraform init
      - name: Validate
        run: terraform validate
      - name: Plan
        run: terraform plan -var-file="terraform.tfvars"
```

---

## ✅ Beoordelingsdoel: Bewijs AI-gebruik

Alle opdrachten zijn ondersteund door AI-prompts. Taken zijn uitgevoerd via eigen Ubuntu VM met een lokale GitHub runner en automatische workflow-executie via GitHub Actions.

Logs, commits en actie-uitvoeringen zijn zichtbaar in de Actions-tab van:  
🔗 https://github.com/naimd66/week5/actions

---

**Einde verslag.**  
