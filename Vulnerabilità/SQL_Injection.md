# SQL Injection (SQLi)

La SQL Injection è una vulnerabilità che consente a un attaccante di manipolare query SQL tramite input non sanitizzati.

## Esempio
```sql
' OR 1=1 --
```

## Impatti
- Accesso non autorizzato al database
- Furto o modifica dati
- Escalation di privilegi

## Prevenzione
- Query parametrizzate
- Uso di ORM
- Validazione e sanitizzazione input
