# Fix audio Intel Tiger Lake (SST / SOF) su Parrot OS (HP)

Questa guida risolve il problema “nessun audio” su molti laptop **HP** con controller audio:

- **Intel Tiger Lake-LP Smart Sound Technology Audio Controller (SST)**
- Audio gestito via **SOF (Sound Open Firmware)**

Il punto chiave è: **installare il firmware SOF** e **forzare il kernel a usare SOF** tramite un parametro in **GRUB**.

---

## 0) Prerequisiti

- Accesso con utente con permessi `sudo`
- Connessione Internet per installare i pacchetti
- Un editor testuale (qui uso `nano`)

---

## 1) Verifica dell’hardware (opzionale, ma utile)

Controlla che il controller audio sia quello Intel Tiger Lake SST:

```bash
lspci | grep -i audio
```

Esempio tipico:

```text
0000:00:1f.3 Multimedia audio controller: Intel Corporation Tiger Lake-LP Smart Sound Technology Audio Controller (rev 20)
```

---

## 2) Installa firmware e componenti audio necessari (PASSAGGIO CHIAVE)

Installa il firmware SOF e gli strumenti base. Questo è spesso ciò che “manca” su installazioni fresh.

```bash
sudo apt update
sudo apt install firmware-sof-signed alsa-utils pipewire wireplumber
```

### Verifica che il firmware SOF sia presente

```bash
ls /lib/firmware/intel/sof
```

Dovresti vedere file/carte come `sof-tgl.ri` / `sof-tgl.ldc` (Tiger Lake) e cartelle come `community` o `intel-signed`.

---

## 3) Forza l’uso di SOF tramite GRUB (PASSAGGIO RISOLUTIVO)

Su molti HP con Tiger Lake l’auto-detect del kernel può scegliere il driver sbagliato.
Per evitare questo, forziamo SOF con il parametro:

- `snd_intel_dspcfg.dsp_driver=1`

### 3.1 Modifica GRUB

Apri il file di configurazione di GRUB:

```bash
sudo nano /etc/default/grub
```

Trova la riga (può essere identica o molto simile):

```text
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

Sostituiscila con:

```text
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash snd_intel_dspcfg.dsp_driver=1"
```

> Se nella tua riga ci sono già altri parametri oltre a `quiet splash`, **non eliminarli**:
> aggiungi semplicemente `snd_intel_dspcfg.dsp_driver=1` in fondo, separato da uno spazio.

#### Salva ed esci da nano

- `CTRL + O` → Invio (salva)
- `CTRL + X` (esci)

### 3.2 Rigenera la configurazione di GRUB

```bash
sudo update-grub
```

Se non ci sono errori, sei a posto.

### 3.3 Riavvia

```bash
reboot
```

---

## 4) Verifica che l’audio sia tornato

### 4.1 Controlla che ALSA veda la scheda

```bash
aplay -l
```

Un risultato “buono” spesso contiene qualcosa di simile a:

```text
card 0: sofhdadsp [sof-hda-dsp]
```

### 4.2 Controlla mixer/volume (molto importante)

Apri il mixer ALSA:

```bash
alsamixer
```

- Premi `F6` e seleziona `sof-hda-dsp` (se presente)
- Assicurati che **Master / Speaker** non siano in mute (`MM`)
  - per togliere il mute: tasto `M`
- Alza il volume con le frecce (`↑`)

### 4.3 Controlla i log (opzionale)

```bash
dmesg | grep -i sof
```

Dovresti vedere riferimenti a moduli/driver SOF (es. `sof-audio-pci-intel-tgl`).

---

## 5) Cosa fare se dopo update torna a non funzionare

1. Verifica che il parametro sia ancora presente in `/etc/default/grub`
2. Esegui di nuovo:

```bash
sudo update-grub
reboot
```

3. Ricontrolla:

```bash
aplay -l
```

---

## 6) Ripristino / annullare la modifica (se vuoi tornare indietro)

1. Apri:

```bash
sudo nano /etc/default/grub
```

2. Rimuovi `snd_intel_dspcfg.dsp_driver=1` dalla riga `GRUB_CMDLINE_LINUX_DEFAULT`
3. Poi:

```bash
sudo update-grub
reboot
```

---

## Nota tecnica (per capire “perché GRUB”)

GRUB non “installa driver”: **passa parametri al kernel** all’avvio.
Il parametro `snd_intel_dspcfg.dsp_driver=1` dice al kernel: **usa SOF** (driver corretto su Tiger Lake SST),
evitando che il sistema scelga un fallback incompatibile (o non inizializzi l’audio).

---

Buon divertimento 🐧
