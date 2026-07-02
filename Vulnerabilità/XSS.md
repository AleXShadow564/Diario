# Cross-Site Scripting (XSS)

Il Cross-Site Scripting (XSS) permette l'iniezione di script malevoli nelle pagine web visualizzate dagli utenti.

## Tipi
- Stored XSS
- Reflected XSS
- DOM-based XSS

## Esempio
```html
<script>alert('XSS')</script>
```

## Impatti
- Furto di cookie e sessioni
- Manipolazione della pagina web
- Reindirizzamenti malevoli

## Prevenzione
- Escape output
- Content Security Policy (CSP)
- Validazione input
