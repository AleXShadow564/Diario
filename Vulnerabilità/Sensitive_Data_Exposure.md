# Sensitive Data Exposure

## Introduzione
La Sensitive Data Exposure si verifica quando un'applicazione non protegge adeguatamente dati sensibili come credenziali, informazioni personali o dati finanziari.

---

## Come si verifica
Può accadere a causa di:
- mancanza di crittografia
- uso di HTTP invece di HTTPS
- storage non sicuro delle password
- chiavi API esposte

---

## Impatti
- furto di identità
- accesso non autorizzato ad account
- violazioni GDPR
- perdita di fiducia degli utenti

---

## Tipi di dati a rischio
- password
- dati bancari
- token di sessione
- dati personali (PII)

---

## Tecniche di attacco
- intercettazione traffico (MITM)
- accesso a database non protetti
- leakage da repository pubblici

---

## Prevenzione
- crittografia TLS end-to-end
- hashing password con salt
- gestione sicura delle chiavi
- minimizzazione dei dati raccolti

---

## Best practices
- encryption at rest e in transit
- rotation delle chiavi
- secure vault per segreti

---

## Conclusione
La protezione dei dati sensibili è fondamentale non solo per la sicurezza tecnica ma anche per la conformità legale e la fiducia degli utenti.