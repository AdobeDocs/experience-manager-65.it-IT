---
title: Note sulla versione 2021 di AEM Content and Commerce
description: Note sulla versione 2021 di AEM Content and Commerce
translation-type: tm+mt
source-git-commit: 1a6d713e74056333b18ed68f58876c2a75d535b8
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 11%

---

# Panoramica sulla versione di Commerce Integration Framework GitHub

## Panoramica dei requisiti di sistema

Rivedi i requisiti minimi di sistema nella tabella seguente per la versione CIF in uso o che intendi utilizzare in futuro.

**Componente aggiuntivo CIF disponibile tramite  [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Il vecchio connettore CIF sta entrando in modalità di manutenzione e non deve più essere utilizzato. Esegui la migrazione al nuovo componente aggiuntivo CIF.**

| Componente | Requisiti di sistema |
|:-------|:-----:|
| Componente aggiuntivo CIF | Minimo: AEM 6.5.7, Magento 2.3.5 Schema GraphQL |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data di rilascio: Aprile 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | v021.04.22 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componenti core CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità {#what-is-new-april}

* Supporto per UID categoria : consente di sbloccare le integrazioni di e-commerce di terze parti per i sistemi che utilizzano stringhe per ID categoria

* Estensione AEM per PWA Studi incl. integrazione di esempio

* Nuovo componente core di navigazione CIF che estende il componente core di navigazione WCM

* Indicatore visivo per i dati di catalogo in fase di AEM vetrina

### Correzioni di bug {#bug-fixes-april}

* Il campo della categoria principale non veniva visualizzato nella scheda commercio nelle proprietà della pagina delle pagine delle categorie

## Data di rilascio: Marzo 2021{#what-is-new-march}

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 1,9 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 1,9 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 2021.03.25 | [Note sulla versione](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità

* Supporto per Magenti 2.4.2

### Miglioramenti

* È stata migliorata la riutilizzabilità del componente dettaglio del prodotto per le pagine basate su contenuti

* Memorizzazione in cache migliore e meno chiamate di backend per PDP

* Correzioni di bug multiple.

## Data di rilascio: Febbraio 2021

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 1.8.0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 1.8.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 2021.02.24 | [Note sulla versione](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità {#what-is-new-february}

* Gestione dell&#39;esperienza del prodotto: Arricchisci le pagine dei cataloghi di prodotti singolarmente con Frammenti esperienza.

* Proprietà estese della console prodotti per visualizzare le risorse collegate e i frammenti esperienza, con l’azione di passare rapidamente al contenuto associato.

### Miglioramenti  {#what-is-improved-february}

* Livello dati lato client migliorato con url immagine prodotto e informazioni sulla categoria

* Correzioni di bug multiple.

## Data di rilascio: Gennaio 2021

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 1.7.0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 1.7.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 2021.02.02 | [Note sulla versione](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità {#what-is-new-january}

* Gestione dell&#39;esperienza del prodotto: Nuova scheda di proprietà &quot;Commerce&quot; per Assets e Frammenti esperienza. Questa scheda ti consente di collegare risorse e frammenti esperienza a prodotti e categorie. La scheda mostra anche i dati in tempo reale per gli oggetti di e-commerce collegati e un collegamento per mostrare i dettagli nella console del prodotto.

### Miglioramenti  {#what-is-improved-january}

* Invia i dati utente dopo l’autenticazione ad Adobe Client Data Layer.

* Correzioni di bug multiple.
