# Cross-Site Scripting (XSS)

## Introduzione
Il Cross-Site Scripting (XSS) è una vulnerabilità che consente a un attaccante di inserire script malevoli all'interno di pagine web visualizzate da altri utenti.

Rientra tra le vulnerabilità più comuni delle applicazioni web moderne.

---

## Come funziona
XSS si verifica quando un'applicazione inserisce input utente non sanitizzato direttamente nell'HTML della pagina.

Esempio:
```html
<div>Benvenuto, USER_INPUT</div>
```
Se USER_INPUT contiene:
```html
<script>alert('XSS')</script>
```
lo script viene eseguito nel browser della vittima.

---

## Tipologie di XSS

### 1. Stored XSS
Il payload viene salvato nel database e mostrato ad altri utenti.

### 2. Reflected XSS
Il payload viene riflesso immediatamente nella risposta HTTP.

### 3. DOM-based XSS
La vulnerabilità si trova nel codice JavaScript lato client.

---

## Impatti
- Furto di cookie e sessioni
- Account takeover
- Defacement del sito
- Phishing tramite pagine fidate

---

## Tecniche di attacco
- Inserimento di script inline
- Manipolazione DOM
- Caricamento script esterni malevoli

---

## Prevenzione
- Escape output HTML/JS
- Content Security Policy (CSP)
- Framework sicuri (React, Angular con escaping automatico)
- Validazione input lato server

---

## Conclusione
XSS è pericoloso perché viene eseguito nel browser della vittima, quindi nel contesto di fiducia del sito stesso.