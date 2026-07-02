# Command Injection

## Introduzione
La Command Injection è una vulnerabilità che permette a un attaccante di eseguire comandi arbitrari sul sistema operativo del server tramite input non controllati.

È estremamente critica perché può portare al controllo completo del sistema host.

---

## Come funziona
Quando un'applicazione passa input utente a una shell senza sanitizzazione, l'attaccante può concatenare comandi.

Esempio vulnerabile:
```bash
ping 127.0.0.1; rm -rf /
```

---

## Impatti
- Esecuzione di codice remoto (RCE)
- Compromissione completa del server
- Furto o distruzione dati
- Installazione di malware/backdoor

---

## Tecniche di attacco
- Command chaining (`;`, `&&`, `|`)
- Injection in parametri di sistema
- Exploiting wrapper script vulnerabili

---

## Prevenzione
- Evitare l'uso di shell quando possibile
- Usare API sicure per operazioni di sistema
- Sanitizzare input rigorosamente
- Whitelisting dei valori ammessi

---

## Best practices
- Separare dati e comandi
- Eseguire processi con privilegi minimi
- Logging e monitoring dei comandi eseguiti

---

## Conclusione
La Command Injection è una delle vulnerabilità più pericolose perché consente l'esecuzione diretta di comandi sul sistema operativo.