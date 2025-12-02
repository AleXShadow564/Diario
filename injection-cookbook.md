# COOKBOOK PER TESTARE LE INJECTION

## Comprendere Shell, Template e Parser

Questo ricettario pratico aiuta ad analizzare come un'applicazione interpreta input controllato dall’utente. L'obiettivo è individuare potenziali punti di injection **senza** usare exploit, ma solo caratteri diagnostici.

Utile per CTF, pentest e write‑up tecnici.

---

## 1. Perché i caratteri speciali causano problemi

La maggior parte delle vulnerabilità di injection si verifica quando:

1. L’applicazione accetta input dall’utente.
2. Inserisce quell’input all’interno di:

   * comandi di shell,
   * template,
   * percorsi di file,
   * file di configurazione.
3. **Non** applica sanitizzazione o escaping adeguati.

Lo scopo dei test è capire **come** il backend interpreta l’input.

---

## 2. Caratteri diagnostici principali

Questi caratteri **non** sono exploit: servono solo a testare il comportamento del parser.

### 1. Virgolette doppie — `"`

Rompono stringhe in JSON, shell e template.

### 2. Virgolette singole — `'`

Rompono parametri di shell o file di configurazione.

### 3. Punto e virgola — `;`

Separatore di comandi nella shell. Funziona solo fuori dalle virgolette.

### 4. Pipe — `|`

Indica possibile uso della shell. Può rompere concatenazioni di comandi.

### 5. Sostituzione di comando — `$( )`

Valutata **sempre** dalla shell prima dell’esecuzione, anche dentro virgolette doppie.

**Esempio:**

```bash
echo "ciao $(whoami)"
```

Output:

```text
ciao www-data
```

Se il sistema interpreta costrutti come `$( )`, allora l’input passa alla shell.

### 6. Traversal di directory — `../`

Indica possibili problemi nel trattamento di percorsi.

---

## 3. Come testare un endpoint sospetto

Endpoint come:

```
/generate
/build
/export
/convert
/vpn/generate
```

devono far sospettare l’esecuzione di processi esterni.

### Procedura standard

**Step 1 — Test di base**

```
test
user1
prova123
```

Serve per capire dove finisce l’input.

**Step 2 — Test di rottura stringhe**

```
test"
test'
```

Errori → string parsing debole.

**Step 3 — Test metacaratteri shell**

```
test;
test|
```

Errori → possibile uso di `system()`, `exec()`, `subprocess(shell=True)`.

**Step 4 — Test di sostituzione (diagnostico)**

```
test$(aaa)
```

Serve solo per verificare se l’input passa alla shell.

---

## 4. Come interpretare i risultati

Se l’applicazione:

* riflette `test` in un file → template;
* si rompe con `"` → parsing debole;
* si rompe con `;` o `|` → probabile command injection;
* interpreta `$( )` → input passato alla shell;
* reagisce a `../` → possibile path traversal.

---

## 5. Tabella rapida per riconoscere il parser

| Comportamento            | Parser                         |                |
| ------------------------ | ------------------------------ | -------------- |
| `"` rompe                | JSON / shell / template        |                |
| `'` rompe                | shell / config / SQL-like      |                |
| `;` rompe                | system() / exec()              |                |
| `                        | ` rompe                        | shell / piping |
| `$( )` valutato          | Shell command substitution     |                |
| `{{ }}` valutato         | Template engine (Jinja, Twig…) |                |
| `../` influenza percorsi | File path manipulation         |                |
| Input in .conf/.ovpn     | Template o script esterno      |                |

---

## 6. Regole d’oro del pentesting

* Non iniziare mai con payload complessi.
* Prima studia il parser usando caratteri diagnostici.
* Solo dopo identifica la vulnerabilità reale.
* Un exploit va costruito solo conoscendo:

  * contesto,
  * quoting,
  * sanitizzazione,
  * percorso del dato.

---

## 7. Termini utili da cercare

* bash command substitution injection
* shell metacharacters injection
* iniezione di comandi system()
* unsanitized shell arguments
* CWE-78 OS Command Injection
* template injection basics
* path traversal vulnerability

---

## 8. Conclusione

Test come `$( )`, `;`, `"`, `'`, `../` non sono exploit.
Sono la tecnica standard per riconoscere:

* contesti shell,
* template engine,
* manipolazione di file path,
* configurazioni vulnerabili.

Comprendere il parser è il primo passo per individuare qualsiasi injection.
