# Security Misconfiguration

## Introduzione
La Security Misconfiguration è una delle vulnerabilità più comuni e deriva da configurazioni errate o incomplete di applicazioni, server o servizi cloud.

---

## Come si verifica
Può accadere quando:
- vengono lasciate credenziali di default
- il debug mode è attivo in produzione
- directory listing è abilitato
- permessi sono troppo permissivi
- servizi non necessari sono esposti

---

## Impatti
- accesso non autorizzato ai sistemi
- esposizione di dati sensibili
- esecuzione di attacchi successivi
- compromissione completa dell'infrastruttura

---

## Esempi reali
- pannelli admin esposti su internet
- database senza autenticazione
- bucket cloud pubblici

---

## Tecniche di attacco
- scanning di configurazioni deboli
- exploit di servizi esposti
- enumerazione directory

---

## Prevenzione
- hardening dei sistemi
- configurazioni secure-by-default
- disabilitare servizi inutili
- patch management costante
- audit di sicurezza regolari

---

## Best practices
- Infrastructure as Code con security review
- principle of least privilege
- security headers (CSP, HSTS, etc.)

---

## Conclusione
La Security Misconfiguration è pericolosa perché spesso nasce da errori umani e dimenticanze, rendendo sistemi altrimenti sicuri facilmente attaccabili.