# Verificatore di Sitemap XML e Struttura di Protocollo

[![Verificatore Sitemap](https://img.shields.io/badge/TAVARDT-Sitemap%20XML-5b3cf5.svg)](https://tools.tavardt.com/it/verificatore-sitemap-xml/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Il **TAVARDT Verificatore di Sitemap XML** fornisce verifica automatizzata della sintassi, convalida degli schemi di protocollo, controllo del volume di URL e rilevamento di contenuti misti in Italia.

***

## Architettura del Protocollo e Matrice Diagnostica

I motori di ricerca utilizzano sitemap XML strutturate per individuare nuovi contenuti e pianificare la frequenza di scansione. Errori sintattici, file sovradimensionati o URL insicuri sprecano il budget di scansione e rallentano l'indicizzazione.

Questo strumento diagnostico analizza l'integrità dell'XML, convalida gli schemi urlset e sitemapindex, controlla il limite di 50.000 URL e isola link non sicuri partendo da 100 punti base senza dipendenze esterne.

Il motore di scansione esamina i file sitemap secondo le specifiche ufficiali Sitemaps.org e i requisiti di ingestione dei bot:

<table>
  <thead>
    <tr>
      <th>Controllo di Protocollo</th><th>Criterio di Validazione</th><th>Deduzione</th><th>Impatto su Scansione e SEO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Integrità Sintattica XML</strong></td><td>Parsing completo via ElementTree. Rileva caratteri riservati (&amp;) non scappati, tag aperti ed errori di codifica.</td><td>Punteggio azzerato a 0</td><td>Errore fatale; i crawler di ricerca rifiutano integralmente il documento.</td>
    </tr>
    <tr>
      <td><strong>Validazione dello Schema Radice</strong></td><td>Richiede conformità con gli schemi standard: il tag radice deve essere <code>&lt;urlset&gt;</code> o <code>&lt;sitemapindex&gt;</code>.</td><td>-40 pts</td><td>Struttura non riconosciuta che blocca l'analisi automatizzata delle URL.</td>
    </tr>
    <tr>
      <td><strong>Soglia di Volume Entrate</strong></td><td>Verifica il limite di 50.000 elementi. Penalizza sitemap vuote (-30 pts) e file sovradimensionati (&gt;50.000 URL, -20 pts).</td><td>Fino a -30 pts</td><td>Scansione troncata, sovraccarico di memoria del crawler o invio di file privi di valore.</td>
    </tr>
    <tr>
      <td><strong>URL HTTP Non Sicure</strong></td><td>Individua link non protetti <code>http://</code> inseriti in sitemap di siti che operano interamente sotto HTTPS.</td><td>-15 pts</td><td>Spreco di crawl budget in catene di reindirizzamento non necessarie.</td>
    </tr>
    <tr>
      <td><strong>Disponibilità di Rete</strong></td><td>Verifica codice HTTP 200 e tempi di risposta durante l'handshake TLS.</td><td>Punteggio azzerato a 0</td><td>Host non raggiungibile che impedisce l'ingestione automatica del file XML.</td>
    </tr>
  </tbody>
</table>

### Scala di Qualità e Livelli di Stato

Il sistema calcola un punteggio complessivo di conformità classificando lo stato della sitemap:

* <strong>85 a 100 (OPTIMAL)</strong>: Conformità completa; sintassi XML corretta, URL sicure HTTPS e volume di entrate conforme.
* <strong>65 a 84 (WARNING)</strong>: File funzionale con lievi avvisi su protocollo misto o volume elevato.
* <strong>0 a 64 (CRITICAL)</strong>: Gravi anomalie sintattiche, schemi non riconosciuti o sitemap vuota che richiedono bonifica immediata.

***

## Installazione ed Esecuzione

Sviluppato unicamente con moduli standard di Python 3.8+, senza dipendenze esterne.

```bash
git clone https://github.com/TAVARDT-Italia/xml-sitemap-validator-it.git
cd xml-sitemap-validator-it
```

### Esecuzione Standard CLI

```bash
python sitemap_validator.py https://esempio.it/sitemap.xml
```

### Output Strutturato per Pipeline in JSON

```bash
python sitemap_validator.py https://esempio.it/sitemap.xml -j
```

### Configurazione di Timeout Personalizzato

```bash
python sitemap_validator.py https://esempio.it/sitemap.xml -j -t 15
```

***

## Linee Guida Nazionali e Integrità Web in Italia

Il mantenimento di sitemap corrette e crittografate rispetta i criteri di affidabilità e trasparenza digitale raccomandati in ambito nazionale. Rimuovere link non protetti difende l'integrità del traffico e consolida la reputazione aziendale.

Si raccomanda l'inserimento di audit automatici delle sitemap nelle pipeline continue di rilascio applicativo per garantire una scansione efficiente.

***

## Domande Frequenti Tecniche

### Qual è la soglia massima di entrate per singolo file sitemap?

Lo standard Sitemaps.org limita ciascun file a 50.000 URL e 50MB non compressi. I file che superano le 50.000 voci subiscono una detrazione di 20 punti e devono essere suddivisi tramite un indice di sitemap.

### Perché le URL HTTP non sicure vengono penalizzate?

Inserire link HTTP in una sitemap di un sito HTTPS genera confusione per i bot, spreca budget di scansione nei reindirizzamenti e indebolisce la postura di sicurezza. Il tool detrae 15 punti alla presenza di link HTTP.

### Come viene gestita la differenza tra sitemapindex e urlset?

Il motore esamina l'elemento XML radice, instradando la verifica tra <code>&lt;sitemapindex&gt;</code> per sitemap subordinate e <code>&lt;urlset&gt;</code> per documenti individuali. Tag radice non riconosciuti comportano la perdita di 40 punti.

### Cosa accade in presenza di un errore di sintassi XML?

Caratteri speciali non convertiti (&amp;) o tag aperti impediscono ai bot di interpretare il file. L'analizzatore azzera il punteggio a 0 e assegna lo stato CRITICAL.

### Cosa indicano i livelli di punteggio e le classi di stato?

Un punteggio tra 85 e 100 corrisponde allo stato OPTIMAL. Da 65 a 84 punti indica WARNING con lievi correzioni suggerite, mentre sotto i 65 punti lo stato è CRITICAL, imponendo un intervento tempestivo.

***

## Supporto Tecnico e Consulenza Digitale

Per verifiche approfondite di SEO tecnica, ottimizzazione delle sitemap e standard di conformità web, contattare gli esperti di **TAVARDT**.

***

## Link Utili

* **Portale Aziendale:** https://ag.tavardt.com/it/
* **Suite di Diagnostica:** https://tools.tavardt.com/it/
* **Contatto Tecnico:** https://ag.tavardt.com/it/contatto/

***

### Licenza
Rilasciato sotto licenza MIT.

***

© 2026 TAVARDT. Tutti i diritti riservati.
