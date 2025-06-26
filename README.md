# week5

# Infrastructure as Code – Week 5

## Inhoud

Deze repository bevat de opdracht voor week 5 van het vak *Infrastructure as Code*. De focus ligt op het opzetten van een CI/CD-pipeline via GitHub Actions voor zowel Terraform- als Ansible-scripts.

---

## Bestanden & Structuur

| Bestand/folder              | Beschrijving                                                |
|-----------------------------|-------------------------------------------------------------|
| `main.tf`                   | Terraform-configuratie voor Azure resource deployment       |
| `inventory.ini`             | Ansible-inventory met IP’s en hostgroepen                   |
| `install_apache.yml`        | Eenvoudig Ansible-playbook voor Apache-installatie          |
| `opdracht1.yml`             | Ansible-playbook met conditionele logica en output testing  |
| `.github/workflows/*.yml`   | GitHub Actions workflows voor CI/CD                         |
| `ci.yml`                    | Alternatief CI-configuratiebestand (niet actief gebruikt)   |
| `Schermafbeeldingen *.png` | Bewijs van succesvolle CI/CD-runs                           |

---

## CI/CD Workflows

De folder `.github/workflows/` bevat de volgende pipelines:

| Workflow-bestand            | Functie                                                     |
|-----------------------------|-------------------------------------------------------------|
| `terraform.yml`             | Voert automatisch `terraform plan` en `apply` uit bij push |
| `terraform-destroy.yml`     | Handmatige workflow om infrastructuur te vernietigen       |
| `ansible-ci.yml`            | Test Ansible-playbooks bij elke push naar main             |
| `ansible-runner.yml`        | Draait effectief Ansible-configuraties op remote servers    |

De workflows worden automatisch geactiveerd bij een `push` of via handmatige triggers in GitHub Actions.

---

## Terraform Deployment

Terraform wordt gebruikt voor het deployen van een infrastructuurcomponent in Azure (zoals een VM of netwerkresource).

### Uitvoeren lokaal:

terraform init
terraform plan
terraform apply -auto-approve

Ansible Playbooks
install_apache.yml
Installeert Apache op de opgegeven webserver(s).

ansible-playbook -i inventory.ini install_apache.yml
opdracht1.yml
Complexer playbook dat conditioneel uitvoert en feedback geeft via statusmeldingen (changed, failed).

ansible-playbook -i inventory.ini opdracht1.yml

Inventory
Voorbeeld uit inventory.ini:

[webservers]
192.168.1.101

[dbservers]
192.168.1.102
Zorg ervoor dat de juiste SSH-sleutels zijn toegevoegd aan je lokale machine of GitHub Runner.

Resultaten
- CI/CD via GitHub Actions werkt automatisch en handmatig
- Zowel Terraform als Ansible workflows zijn actief getest
- Screenshots als bewijs toegevoegd
- Roles en playbooks gestructureerd
- README bevat uitvoerbare instructies en volledige uitleg

Extra Tips
- Gebruik terraform destroy alleen via de veilige workflow terraform-destroy.yml
- Ansible-playbooks kunnen worden uitgebreid met roles en vars
- Let op permissies van je SSH key bij self-hosted runners

