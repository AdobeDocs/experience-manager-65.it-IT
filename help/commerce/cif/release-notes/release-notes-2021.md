---
title: Note sulla versione 2021 di AEM Content and Commerce
description: Note sulla versione 2021 di AEM Content and Commerce
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: a401955e4b163a8062a498ea897d4a3d95ae0208
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 10%

---

# Panoramica sulla versione di Commerce Integration Framework GitHub

## Panoramica dei requisiti di sistema

Rivedi i requisiti minimi di sistema nella tabella seguente per la versione CIF in uso o che intendi utilizzare in futuro.

**Con la versione di aprile, abbiamo sostituito il connettore CIF da GitHub con il componente aggiuntivo CIF** disponibile nella Distribuzione di software di  [Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). Il passaggio al componente aggiuntivo offre grandi vantaggi per i progetti:

* La maggior parte delle nuove funzioni sarà immediatamente disponibile su AEM 6.5 (non più in attesa della porta laterale delle funzioni)
* Facile aggiornamento alle nuove versioni dei componenti aggiuntivi
* Pronto per il Cloud Service

Il vecchio connettore CIF sta entrando in modalità di manutenzione e non deve più essere utilizzato. Sostituisci il connettore CIF con il nuovo componente aggiuntivo CIF. Per la maggior parte dei progetti dovrebbe essere possibile una semplice sostituzione dei pacchetti.

| Componente | Requisiti di sistema |
|:-------|:-----:|
| Componente aggiuntivo CIF | Minimo: AEM 6.5.7, Magento 2.3.5 Schema GraphQL |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archetipo progetto AEM | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data di rilascio: Settembre 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.09.27 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| Componenti core CIF | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| Sito di riferimento CIF Venia | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Novità {#what-is-new-september}

* La nuova scheda &quot;contenuti commerce associati&quot; nell’editor Sites aumenta l’efficienza dell’autore grazie all’accesso rapido ai contenuti di prodotti AEM pertinenti per il contesto corrente

   ![Contenuto di e-commerce associato](/help/assets/CIF/associated-commerce-content.png)

* Interfaccia utente del selettore prodotti migliorata per una migliore esperienza utente, una maggiore efficienza e il supporto per cataloghi di prodotti complessi

   ![Nuovo selettore prodotti](/help/assets/CIF/product-picker.png)

* Rispetta la proprietà &quot;include_in_menu&quot; nel componente di navigazione

### Correzioni di bug {#bug-fixes-september}

* Lo scaricamento della cache del menu non funziona come previsto

* Errori JS durante AEM passaggio di distribuzione CS e quando non si utilizzano componenti lato client

* Impossibile creare la configurazione cloud CIF nelle cartelle con un nodo sling:configs

## Data di rilascio: Agosto 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.09.02 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| Componenti core CIF | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Sito di riferimento CIF Venia | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Novità {#what-is-new-august}

* Nuova interfaccia utente del selettore categorie per migliorare l’esperienza utente, aumentare l’efficienza e migliorare il supporto per cataloghi di prodotti complessi

   ![Selezione nuova categoria](/help/assets/CIF/category-picker.png)

* Supporto migliorato per A11Y per i componenti core CIF

### Correzioni di bug {#bug-fixes-august}

* Impossibile chiudere il pannello a soffietto del filtro di categoria una volta aperto

* Proprietà &#39;Invito all&#39;azione&#39; interrotta nel teaser prodotto

* Errori CIF JS durante AEM passaggio di distribuzione CS

* Correggere l&#39;accesso ai prodotti non elaborati per gli elementi dell&#39;elenco di prodotti mappati

## Data di rilascio: Luglio 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.07.21 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Componenti core CIF | 2,0,0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Sito di riferimento CIF Venia | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Novità {#what-is-new-july}

* Componenti core CIF v2
   * Configurazioni semplificate e migliorate per URL PDP/PLP e SEO
   * Indicatore visivo per i dati di prodotto in fase di creazione in modalità per una migliore visibilità delle imminenti modifiche
   * Nuovo componente mappa del sito per le pagine di contenuto e di e-commerce

* Supporto per [Adobe Commerce Sensei Product Recommendation, basato su Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) in AEM Storefront tramite consigli predefiniti o al momento dell’esecuzione

## Data di rilascio: Giugno 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.06.18 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Componenti core CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Sito di riferimento CIF Venia | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Novità {#what-is-new-june}

* Nuovi tipi di dati di riferimento CIF per prodotti e categorie per Frammenti di contenuto (Incl. supporto per l&#39;interfaccia utente del selettore prodotti/categorie)
* Nuovo componente core Frammento di contenuto Commerce
* Ricerca di e-commerce full-text supportata nel backend AEM
* I componenti core di Commerce supportano la raccolta dati di Adobe Commerce Sensei Recs
* URL ottimizzati per l’ottimizzazione SEO (Search Engine Optimization) per le pagine di categorie
* Supporto per intestazioni HTTP personalizzate per sito/configurazione

## Data di rilascio: Maggio 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.05.26 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Componenti core CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Sito di riferimento CIF Venia | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Novità {#what-is-new-may}

* Supporto per l’impaginazione del contenuto associato nelle proprietà della console del prodotto

### Correzioni di bug {#bug-fixes-may}

* Miniature delle risorse non visualizzate nella scheda Risorsa delle proprietà del prodotto

* Breadcrumb ripristina i dati di anteprima nella console del prodotto

## Data di rilascio: Aprile 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.04.22 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componenti core CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità {#what-is-new-april}

* Supporto per UID categoria : consente di sbloccare le integrazioni di e-commerce di terze parti per i sistemi che utilizzano stringhe per ID categoria

* Estensione AEM per PWA Studi incl. integrazione di esempio

* Nuovo componente core di navigazione CIF che estende il componente core di navigazione WCM

### Correzioni di bug {#bug-fixes-april}

* Il campo della categoria principale non veniva visualizzato nella scheda commercio nelle proprietà della pagina delle pagine delle categorie

## Data di rilascio: Marzo 2021 {#what-is-new-march}

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 1,9 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 1,9 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 2021.03.25 | [Note sulla versione](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità

* Supporto per Magento 2.4.2

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

* Proprietà estese della console prodotti per mostrare le risorse collegate e i frammenti esperienza, inclusa l’azione per passare rapidamente al contenuto associato.

### Miglioramenti  {#what-is-improved-february}

* Livello dati lato client migliorato con url immagine prodotto e informazioni sulla categoria.

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
