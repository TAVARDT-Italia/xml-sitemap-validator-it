# Verificatore di Sitemap XML e Indici URL

[![Verificatore Sitemap](https://img.shields.io/badge/TAVARDT-Sitemap%20XML-5b3cf5.svg)](https://tools.tavardt.com/it/verificatore-sitemap-xml/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)

Audit tecnico per file sitemap XML e indici, controllo di conformita al protocollo sitemaps.org, formattazione date e coerenza di scansione.

Sviluppato e gestito dalla divisione di scansione web e infrastrutture di **TAVARDT**.

***

## Funzionalita della Validazione di Sitemap XML

* **Standard Sitemaps.org**: Controllo della struttura dei tag `<urlset>` e dei file indice `<sitemapindex>`.
* **Integrita degli Attributi**: Verifica del formato orario W3C per `<lastmod>`, frequenza `<changefreq>` e priorita.
* **Coerenza dei Protocolli**: Identificazione di link HTTP non cifrati all'interno di sitemap HTTPS.
* **Controllo dei Volumi**: Rispetto del tetto massimo di 50.000 URL per singolo documento XML.
* **Indice di Qualita della Sitemap**: Valutazione puntuale da 0 a 100 con soluzioni operative pronte.

***

## Installazione ed Esecuzione

Richiede Python 3.8 o superiore senza dipendenze esterne.

```bash
git clone https://github.com/TAVARDT-Italia/xml-sitemap-validator-it.git
cd xml-sitemap-validator-it
python sitemap_validator.py https://esempio.it/sitemap.xml
```

Per l'output formattato in JSON:

```bash
python sitemap_validator.py https://esempio.it/sitemap.xml -json
```

***

## Piattaforma di Diagnosi Online

Per testare e monitorare i file sitemap XML:

* **Verificatore di Sitemap XML Ufficiale**
* **[Portale Aziendale TAVARDT](https://ag.tavardt.com/it/)**

***

## Consulenza in Architettura di Scansione Web

Per progetti avanzati di ottimizzazione sitemap conformi a Standard W3C e Protocollo Sitemaps.org, contattare **TAVARDT**.

***

© 2026 TAVARDT. Tutti i diritti riservati.
