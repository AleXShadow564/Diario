# SQL Injection (SQLi)

## Introduzione
La SQL Injection è una delle vulnerabilità più critiche nelle applicazioni web e rientra stabilmente nella OWASP Top 10. Si verifica quando un'applicazione costruisce query SQL concatenando input dell'utente senza un'adeguata validazione o parametrizzazione.

Un attaccante può manipolare la struttura della query per alterarne il comportamento originale.

---

## Come funziona
Quando un'applicazione inserisce direttamente input utente in una query SQL, il database non distingue tra codice e dati.

Esempio vulnerabile:
```sql
SELECT * FROM users WHERE username = '" + user + "' AND password = '" + pass + "';
```

Se l'input è:
```
' OR '1'='1
```
la query diventa sempre vera.

---

## Tipologie di SQL Injection
- In-band SQLi (error-based, union-based)
- Blind SQLi (boolean-based, time-based)
- Out-of-band SQLi

---

## Impatti
- Accesso non autorizzato ai sistemi
- Furto di database completi
- Alterazione o cancellazione dati
- Escalation di privilegi

In scenari reali può portare al completo compromesso dell'applicazione.

---

## Tecniche di attacco
- Union-based injection per estrarre dati
- Blind injection basata su risposte true/false
- Time-based injection usando ritardi SQL

---

## Prevenzione
- Uso di query parametrizzate (prepared statements)
- ORM moderni (Hibernate, Sequelize, SQLAlchemy)
- Validazione rigorosa degli input
- Principio del privilegio minimo sul database

---

## Best practices
- Mai concatenare stringhe SQL
- Logging delle query sospette
- Web Application Firewall (WAF)

---

## Conclusione
La SQL Injection rimane una delle vulnerabilità più pericolose perché sfrutta un errore logico di base: confondere dati e codice. La prevenzione è semplice ma deve essere applicata sistematicamente.