# Installation et Utilisation de Nikto

Nikto est un scanner de vulnérabilités open-source permettant d’analyser la sécurité des serveurs web.

## 1. Installation de Nikto

### **Sur Debian/Ubuntu**
```bash
sudo apt update && sudo apt install nikto -y
```

### **Via Git (Méthode recommandée)**
```bash
git clone https://github.com/sullo/nikto.git
cd nikto/program
```

## 2. Lancer un scan avec Nikto

### **Scan de base**
```bash
perl nikto.pl -h http://<IP_DU_SERVEUR>
```
Exemple :
```bash
perl nikto.pl -h http://172.24.10.50
```

### **Scan HTTPS**
```bash
perl nikto.pl -h https://172.24.10.50
```

### **Scan sur un port spécifique**
```bash
perl nikto.pl -h http://172.24.10.50 -p 8080
```

### **Scan avec un User-Agent spécifique**
```bash
perl nikto.pl -h http://172.24.10.50 -useragent "Mozilla/5.0"
```

### **Enregistrer les résultats dans un fichier**
```bash
perl nikto.pl -h http://172.24.10.50 -o resultats.txt
```

## 3. Interpréter les résultats (Exemple dans notre cas)

![image](https://github.com/user-attachments/assets/59755b9b-82af-410b-9c64-4e8db0d64f9e)

Nikto détecte :
- Failles XSS
- Headers HTTP mal configurés
- Versions obsolètes et vulnérables des logiciels
- Pages sensibles exposées (`/admin`, `/phpinfo.php`, etc.)

## 4. Correction des vulnérabilités

### **Mise à jour du serveur web**
**Pour Apache sur Debian/Ubuntu :**
```bash
sudo apt update && sudo apt upgrade apache2 -y
```

Redémarrer Apache :
```bash
sudo systemctl restart apache2
```
Ou
```bash
sudo systemctl restart httpd
```

### **Désactiver la fuite d’ETags**
Dans `/etc/apache2/apache2.conf` (ou `/etc/httpd/conf/httpd.conf`), ajoutez :
```apache
FileETag None
```

### **Ajouter les headers de sécurité**
Dans `/etc/apache2/apache2.conf` (ou `/etc/httpd/conf/httpd.conf`), ajoutez :
```apache
<IfModule mod_headers.c>
    # Content Security Policy
    Header always set Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; font-src 'self' data:; connect-src 'self'; frame-src 'none'; object-src 'none'; base-uri 'self'; form-action 'self'"

    # Autres en-têtes de sécurité recommandés
    Header always set X-Content-Type-Options "nosniff"
    Header always set X-Frame-Options "DENY"
    Header always set X-XSS-Protection "1; mode=block"
    Header always set Referrer-Policy "strict-origin-when-cross-origin"
    Header always set Permissions-Policy "geolocation=(), microphone=(), camera=()"
</IfModule>
