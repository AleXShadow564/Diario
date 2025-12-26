# CUDA + OpenCL + Hashcat su Parrot OS (NVIDIA)

Guida completa, stabile e ripetibile per utilizzare **Hashcat con CUDA** su **Parrot OS**
con GPU **NVIDIA**, evitando problemi di driver, kernel e mancato rilevamento GPU.

---

## Sistema di riferimento

- **OS:** Parrot OS (stable)
- **Desktop:** MATE (Xorg)
- **GPU:** NVIDIA GeForce GTX 1660 SUPER
- **Driver NVIDIA:** repository ufficiali Parrot

---

## Problema iniziale

Installando CUDA su Parrot OS:
- Hashcat **non vedeva la GPU**
- oppure **non inizializzava CUDA**

Su **Parrot 7 beta** e **Kali Linux**, con GPU NVIDIA:
- schermate nere
- sistema rotto dopo aggiornamenti
- kernel e driver non allineati

---

## Scoperta chiave

**CUDA da sola NON basta.**

Hashcat usa **OpenCL per enumerare correttamente la GPU**,  
anche quando poi utilizza **CUDA come backend di calcolo**.

👉 Senza OpenCL NVIDIA:
- la GPU può non comparire
- CUDA può non inizializzarsi

---

## Installazione CUDA Toolkit 11.8

### Aggiunta keyring NVIDIA

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
```

### Abilitazione repository contrib

```bash
sudo add-apt-repository contrib
```

### Aggiornamento repository

```bash
sudo apt update
```

### Installazione CUDA Toolkit

```bash
sudo apt install cuda-toolkit-11-8
```

🔎 **Nota importante**
- Il toolkit serve soprattutto per `nvcc`
- Hashcat **NON usa nvcc**
- Hashcat usa il **CUDA runtime del driver NVIDIA**

---

## Installazione OpenCL NVIDIA (PASSAGGIO FONDAMENTALE)

```bash
sudo apt install nvidia-opencl-icd ocl-icd-libopencl1 clinfo
```

### Verifica OpenCL

```bash
clinfo | grep -i nvidia
```

Se NVIDIA compare → OpenCL è attivo correttamente.

---

## Verifiche di sistema

### Driver NVIDIA

```bash
nvidia-smi
```

La GPU deve essere visibile.

### CUDA Toolkit (opzionale)

```bash
nvcc --version
```

Se `nvcc` non è nel PATH **non è un problema** per Hashcat.

---

## Verifica Hashcat

### Backend disponibili

```bash
hashcat -I
```

Output corretto:
- CUDA API visibile (es. CUDA 12.x dal driver)
- GPU NVIDIA rilevata
- OpenCL NVIDIA presente
- PoCL CPU opzionale

### Benchmark CUDA

```bash
hashcat -b -D 2
```

`-D 2` forza l'uso di CUDA.

Prestazioni corrette per GTX 1660 SUPER:
- **MD5:** ~19–20 GH/s
- **SHA1:** ~6 GH/s

---

## Funzionamento reale

- Wordlist come `rockyou.txt` → meno di 1 secondo
- CUDA attivo
- GPU realmente utilizzata

### Algoritmi lenti (comportamento normale)

- WinZip
- bcrypt
- WPA

Velocità basse (kH/s o MH/s) e tempi lunghi **sono normali**.

Esempio WinZip:
- Hash.Mode: 13600
- Speed: ~2 MH/s
- GPU Util: ~98%

La GPU lavora correttamente.

---

## Spiegazione chiave

> OpenCL NON traduce CUDA.  
> OpenCL serve a far vedere la GPU a Hashcat.  
> Una volta enumerata, Hashcat usa CUDA direttamente.

**Metafora:**

- CUDA = motore  
- Driver NVIDIA = auto  
- Hashcat = pilota  
- OpenCL = chiave  

---

## Conclusioni

- Parrot OS + MATE + Xorg è stabile con NVIDIA
- CUDA Toolkit 11.8 è sufficiente
- OpenCL NVIDIA è ESSENZIALE
- Hashcat usa realmente CUDA
- Kali / Parrot beta possono rompersi dopo update kernel
- Se funziona → **non aggiornare kernel e driver insieme**

---

## Stato finale

✅ **Setup funzionante**  
✅ **Stabile**  
✅ **Ripetibile**
