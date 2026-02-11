# M300-Services-ELF
# Dokumentation – Infrastruktur-Automatisierung mit Vagrant, Apache und Webalizer

---

## 1. Ziel der Arbeit

Ziel dieser Arbeit ist es, eine lokale Entwicklungs- und Testumgebung aufzubauen, in der virtuelle Maschinen automatisiert, konsistent und reproduzierbar erstellt werden.  
Dabei werden die theoretischen Konzepte der Infrastruktur-Automatisierung praktisch umgesetzt.

---

## 2. Voraussetzungen

- Windows-PC mit aktivierter Virtualisierung (Intel VT-x / AMD-V)

Installierte Software:

- Git (Git Bash)
- VirtualBox
- Vagrant
- Visual Studio Code
- Internetverbindung

---

## 3. Theoretische Grundlagen – Infrastruktur-Automatisierung

### 3.1 Cloud Computing

Cloud Computing bezeichnet die Bereitstellung von IT-Ressourcen wie Rechenleistung, Speicher, Netzwerke und Software ueber ein Netzwerk, ohne dass diese lokal installiert sein muessen.

Man unterscheidet folgende Servicemodelle:

- IaaS (Infrastructure as a Service): Virtuelle Maschinen und Infrastruktur  
- PaaS (Platform as a Service): Laufzeitumgebungen fuer Anwendungen  
- SaaS (Software as a Service): Fertige Anwendungen  
- CaaS (Container as a Service): Containerisierte Anwendungen  

---

### 3.2 Dynamische Infrastruktur-Plattformen

Eine dynamische Infrastruktur-Plattform stellt virtualisierte Ressourcen wie Compute, Storage und Network bereit und verwaltet diese programmgesteuert.  
Die Bereitstellung erfolgt ueber virtuelle Maschinen (VMs).

Beispiele:

- Public Cloud: AWS, Azure, Google Cloud  
- Private Cloud: OpenStack, VMware vCloud  
- Lokale Virtualisierung: VirtualBox  

Voraussetzungen fuer Automatisierung:

- programmierbar (API)  
- on-demand  
- self-service  
- portabel  
- sicher  

---

### 3.3 Infrastructure as Code (IaC)

Infrastructure as Code ist ein Paradigma, bei dem Infrastruktur wie Software behandelt wird.  
Systeme werden in Dateien definiert, versioniert und automatisiert ausgerollt.

Ziele von IaC:

- konsistente und reproduzierbare Systeme  
- schnelle Aenderungen ohne manuellen Aufwand  
- weniger Fehler durch Automatisierung  
- einfache Wiederherstellung von Systemen  
- kontinuierliche Verbesserungen  

---

### 3.4 Vagrant

Vagrant ist ein Open-Source-Tool zur Erstellung und Verwaltung von virtuellen Maschinen ueber die Kommandozeile.  
Die Konfiguration erfolgt ueber ein Vagrantfile.

---

## 4. Praktischer Teil – Einrichtung der Umgebung

### 4.1 Git konfigurieren

```bash
git config --global user.name "fikretelezi"
git config --global user.email "fikretelezi2008@gmail.com"
  
## 4. Praktischer Teil – Einrichtung der Umgebung

### 4.1 Git konfigurieren

git config --global user.name "fikretelezi"  
git config --global user.email "fikretelezi2008@gmail.com"

### 4.2 SSH-Key erstellen (GitHub)

ssh-keygen -t rsa -b 4096 -C "fikretelezi2008@gmail.com"

Der Public Key wurde zu GitHub hinzugefuegt und erfolgreich getestet:

ssh -T git@github.com

### 4.3 Projektstruktur erstellen

cd "/c/Users/Hans/OneDrive - Berufsbildungszentrum Schaffhausen/BBZ/Blockschule/300"  
mkdir -p vagrant/web  
cd vagrant/web

## 5. Apache Webserver automatisiert mit Vagrant

### 5.1 Vagrantfile erstellen

vagrant init ubuntu/jammy64

### 5.2 Vagrantfile konfigurieren

Vagrant.configure("2") do |config|  
  config.vm.box = "ubuntu/jammy64"  

  config.vm.network "forwarded_port", guest: 80, host: 8080  

  config.vm.provision "shell", inline: <<-SHELL  
    apt update  
    apt install -y apache2  
    systemctl enable apache2  
    systemctl start apache2  
  SHELL  
end

### 5.3 VM starten

vagrant up

### 5.4 Verbindung zur VM

vagrant ssh

## 6. Apache ueberpruefen

### 6.1 Service-Status

sudo systemctl status apache2

Ergebnis:

Active: active (running)

### 6.2 Test mit curl

curl http://localhost

### 6.3 Test im Browser

http://127.0.0.1:8080

Die Apache-Standardseite wird angezeigt.

## 7. HTML-Titel anpassen

sudo nano /var/www/html/index.html

Aenderung:

<title>M300 – Apache Webserver</title>  
<h1>Apache Webserver – Modul 300</h1>  
<p>Erstellt von Fikret</p>
