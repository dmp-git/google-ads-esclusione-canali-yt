# 📛 Google Ads Script — YouTube Channel Placement Exclusion con Cache Google Sheets

Questo script per Google Ads automatizza l’esclusione dei canali YouTube di bassa qualità dalla rete Display e YouTube. Utilizza un **sistema di caching** basato su **Google Sheets** e filtra soltanto i **posizionamenti attivi con almeno 1 clic**.

---

## ✨ Funzionalità principali

- 📊 **Esclude canali YouTube** con lingua e paese non compatibili.
- 🧠 **Utilizza una cache** in Google Sheets per evitare chiamate API ridondanti.
- 🧾 **Tiene traccia degli esclusi** marcandoli con `"YES"` anche se già presenti in Ads.
- 🕵️‍♂️ **Filtra solo canali con almeno 1 clic** per evitare esclusioni inutili.
- ⚙️ Supporta aggiornamento batch tramite **YouTube Data API v3**.
- 🌍 Filtra su base linguistica e geografica con una whitelist personalizzabile.

---

## ⚙️ Configurazione

Modifica i seguenti parametri nella sezione `// CONFIGURAZIONE` dello script:

```javascript
var EXCLUSION_LIST_NAME = 'esclusione placement';
var SPREADSHEET_URL = 'https://docs.google.com/spreadsheets/d/...';
var SHEET_NAME = 'YouTubeChannelCache';
var TTL_DAYS = 30;
var CHUNK_SIZE = 50;
var ALLOWED_COUNTRIES = ['US','GB','IT','CA','AU','NZ','MC'];
```

---

## 📄 Struttura del Google Sheet

Il foglio `YouTubeChannelCache` deve avere le seguenti colonne (intestazione in prima riga):

| ChannelID | Title | Lang | Country | LastCheck | Excluded |
|-----------|-------|------|---------|-----------|----------|

---

## 🧠 Logica di esclusione

Uno YouTube Channel viene escluso **solo se**:

- La lingua **non** è `en` o `it`; oppure
- La lingua è `en/it`, ma il **paese non è nella whitelist** `ALLOWED_COUNTRIES`; oppure
- La lingua è vuota **e** il paese non è nella whitelist.

---

## 📤 Come funziona

1. **Carica la cache** esistente dal foglio Google Sheets.
2. **Recupera la lista** di esclusione in Google Ads o la crea se non esiste.
3. **Identifica canali YouTube attivi** con almeno 1 clic negli ultimi giorni.
4. **Controlla nella cache** se i canali sono già presenti e se i dati sono aggiornati.
5. **Chiama la YouTube API** solo per i canali non in cache o con dati scaduti.
6. **Applica la logica di esclusione** su ciascun canale.
7. **Aggiunge automaticamente i placement da escludere** tramite bulk upload.
8. **Aggiorna la cache** nel Google Sheet.

---

## ✅ Requisiti

- Un account Google Ads con accesso per creare script.
- Autorizzazioni per accedere alla YouTube Data API v3.
- Accesso in scrittura a un Google Sheet per caching.
- Aggiungi `YouTube` e `Google Sheets` come servizi avanzati nello script editor di Google Ads.

---

## 🔍 Esempio di output nel log

```
Canale: [Kids Music] (ID: UCxyz), Lang: es, Country: AR => ESCLUSO
Canale: [English Tutorial] (ID: UCabc), Lang: en, Country: US => MANTENUTO
Canale: [Channel X] (ID: UCzzz), Lang: it, Country: RU => ESCLUSO
```

---

## 📌 Note aggiuntive

- **Lo script NON imposta un intervallo temporale**, ma è possibile aggiungere `AND segments.date DURING LAST_30_DAYS` alla query GAQL.
- **Funziona solo con canali che hanno generato almeno 1 clic**, per mantenere l’analisi focalizzata su traffico attivo.
- **Evita l’overlap** con canali già esclusi in Ads, aggiornando la colonna `Excluded` comunque a `YES`.

---

## 🛠️ Contribuire

Hai miglioramenti o idee per estendere lo script? Apri una pull request o crea un'issue!

---

## 📄 Licenza

MIT License. Vedi [LICENSE](./LICENSE) per dettagli.