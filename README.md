# 🛂 Scanner Check-in OlasDelSur

App web statica per il **self check-in** degli ospiti di Olas del Sur. L'ospite, dal proprio
telefono, scansiona il codice **MRZ** del passaporto o del documento d'identità; i dati anagrafici
vengono letti **interamente nel browser** e, completati con indirizzo e contatti, inviati al modulo
di registrazione (fase di raccolta dati per il registro viajeros SES — RD 933/2021).

- **App live:** https://olasdelsurelpuerto-alt.github.io/mrz-scanner-proto/
- **Repo:** `olasdelsurelpuerto-alt/mrz-scanner-proto` (GitHub Pages)

## 🔒 Privacy & sicurezza
- **OCR on-device** (Tesseract.js / WebAssembly): l'immagine del documento **non viene mai caricata
  né salvata**. Verso il modulo arrivano solo i campi di testo confermati.
- **Zero terzi a runtime:** Tesseract, modello MRZ, font e grafica sono tutti **self-hosted** nel
  repo. L'app non contatta servizi esterni e **funziona offline** (prova che nulla lascia il device).
- **Nessun `localStorage`/cookie:** i dati non restano sul dispositivo dopo la sessione.
- **Nessun segreto nel front-end:** nessun ID di foglio di calcolo, nessuna chiave o credenziale.

## 🧠 Come funziona (pipeline)
Scan MRZ (camera, on-device) → parser **TD3** (passaporto) / **TD1** (carta) + validazione
check-digit **ICAO 9303** → parser DNI/NIE spagnolo (separa nº soporte e nº documento) → consenso
**multi-frame** per i campi senza check-digit (nomi) → conferma (campi verificati bloccati) →
completamento (indirizzo, provincia, telefono, email, consenso RGPD) → invio al modulo.

## 🗂️ Struttura
- `index.html` — app completa (markup, stile e logica in un unico file)
- `fonts/`, `fonts.css` — Playfair Display + DM Sans (self-hosted)
- `vendor/` — Tesseract.js + core WebAssembly
- `mrz.traineddata.gz` — modello OCR-B / MRZ
- `bg-doodles.svg` — pattern di sfondo (doodle a tema costiero)
- `logo.png` — logo nell'header
- `sample_dni.png`, `sample_passport.png`, `samples.html` — specimen e pagina di test

## ▶️ Sviluppo locale
I moduli WebAssembly richiedono un server HTTP (il protocollo `file://` non basta):

```bash
python3 -m http.server 8000
# poi apri http://localhost:8000/
```

## 🚀 Deploy
Push su `main` → **GitHub Pages** pubblica automaticamente in 1–2 minuti.

## 🌍 Lingue
Interfaccia interamente tradotta in 5 lingue: 🇪🇸 ES · 🇬🇧 EN · 🇫🇷 FR · 🇩🇪 DE · 🇮🇹 IT.

## 📓 Documentazione interna
La documentazione operativa e di progetto è mantenuta nel Second Brain privato
(riepilogo dei collegamenti nel file locale `PROJECT_NOTES.md`, non versionato).
