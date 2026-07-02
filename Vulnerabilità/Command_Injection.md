# Command Injection

La Command Injection consente l'esecuzione di comandi arbitrari sul sistema operativo tramite input non controllati.

## Esempio
```bash
; rm -rf /
```

## Impatti
- Controllo completo del sistema
- Esecuzione di malware

## Prevenzione
- Evitare chiamate dirette alla shell
- Sanitizzazione input
- Uso di API sicure
