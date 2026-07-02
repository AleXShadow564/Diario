# Vulnerabilità Informatiche

Questo documento descrive in modo chiaro e dettagliato le principali vulnerabilità presenti nei sistemi software moderni, con esempi pratici e spiegazioni utili per comprenderle e prevenirle.

---

## 1. SQL Injection (SQLi)
La SQL Injection è una vulnerabilità che permette a un attaccante di inserire comandi SQL malevoli all'interno di input non sanitizzati.

### Esempio
Un form di login vulnerabile potrebbe permettere input come:
```
' OR 1=1 --
```
che bypassa l'autenticazione.

### Impatti
- Accesso non autorizzato ai dati
- Modifica o cancellazione del database
- Furto di informazioni sensibili

### Prevenzione
- Uso di query parametrizzate
- ORM sicuri
- Validazione input

---

## 2. Cross-Site Scripting (XSS)
Il Cross-Site Scripting permette l'inserimento di script malevoli in pagine web visualizzate da altri utenti.

### Tipi
- Stored XSS
- Reflected XSS
- DOM-based XSS

### Esempio
```html
<script>alert('XSS')</script>
```

### Impatti
- Furto di cookie/sessioni
- Manipolazione contenuti
- Reindirizzamenti malevoli

### Prevenzione
- Escape output
- Content Security Policy (CSP)
- Validazione input

---

## 3. Command Injection
Permette l'esecuzione di comandi sul sistema operativo host attraverso input non controllati.

### Esempio
```bash
; rm -rf /
```

### Impatti
- Controllo completo del sistema
- Esecuzione di malware

### Prevenzione
- Evitare chiamate dirette al sistema
- Sanitizzazione input
- Uso di API sicure

---

## 4. Broken Authentication
Vulnerabilità legata a sistemi di autenticazione deboli o mal implementati.

### Impatti
- Furto di account
- Session hijacking

### Prevenzione
- MFA (Multi-Factor Authentication)
- Hashing password con bcrypt/argon2
- Timeout sessioni

---

## 5. Security Misconfiguration
Configurazioni errate di server, framework o applicazioni.

### Esempi
- Directory listing attivo
- Credenziali default
- Debug mode in produzione

### Impatti
- Esposizione dati sensibili
- Accesso non autorizzato

### Prevenzione
- Hardening sistemi
- Configurazioni sicure di default
- Audit periodici

---

## 6. Sensitive Data Exposure
Esposizione di dati sensibili non protetti adeguatamente.

### Esempi
- Password in chiaro
- Mancato uso di HTTPS

### Prevenzione
- Crittografia (TLS, AES)
- Hashing sicuro
- Gestione sicura delle chiavi

---

## Conclusione
La sicurezza informatica richiede attenzione costante e aggiornamenti continui. La prevenzione delle vulnerabilità è fondamentale per proteggere dati e sistemi.