# Broken Authentication

## Introduzione
Broken Authentication riguarda debolezze nei sistemi di autenticazione e gestione sessioni che permettono ad un attaccante di impersonare altri utenti.

---

## Come funziona
Le vulnerabilità possono emergere da:
- password deboli o prevedibili
- sessioni non protette
- token non sicuri
- mancanza di controlli MFA

---

## Impatti
- Account takeover (ATO)
- Furto di identità digitale
- Accesso a dati sensibili
- Escalation di privilegi

---

## Attacchi comuni
- Brute force
- Credential stuffing
- Session hijacking
- Token theft

---

## Prevenzione
- MFA (Multi-Factor Authentication)
- Hashing password con algoritmi robusti (Argon2, bcrypt)
- Rate limiting login
- Session timeout e rotation
- Secure cookies (HttpOnly, Secure, SameSite)

---

## Best practices
- Monitoraggio accessi sospetti
- Blocchi temporanei dopo tentativi falliti
- Uso di identity provider sicuri (OAuth2, OpenID Connect)

---

## Conclusione
Broken Authentication è critica perché permette di bypassare completamente il sistema di identità, uno dei pilastri della sicurezza applicativa.