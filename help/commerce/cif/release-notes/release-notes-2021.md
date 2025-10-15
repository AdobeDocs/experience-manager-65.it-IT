---
title: Note sulla versione 2021 di Adobe Experience Manager Content and Commerce
description: Note sulla versione 2021 di Adobe Experience Manager Content and Commerce.
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 12%

---

# Panoramica sulla versione di Commerce integration framework GitHub

## Panoramica dei requisiti di sistema

Esaminare i requisiti minimi di sistema riportati nella tabella seguente per la versione dell&#39;CIF attualmente in uso o che si prevede di utilizzare in futuro.

| Componente | Requisiti di sistema |
|:-------|:-----:|
| Componente aggiuntivo CIF | Minimo: schemi Adobe Experience Manager (AEM) 6.5.7, Adobe Commerce 2.3.5 GraphQL |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archetipo progetto AEM | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data di rilascio: novembre 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.11.18.00 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| Componenti core CIF | 2.4.2. | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| Sito di riferimento CIF Venia | 2021.12.2001 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### Novità {#what-is-new-november}

* Componenti myAccount estesi basati sui componenti PEGRA estensibili di Commerce

![Componenti myAccount estesi](/help/assets/CIF/extended-myAccount-components.png)

* Gli autori possono creare consigli di prodotti Commerce ad hoc utilizzando altri tipi di consigli

* Supporto per le carte regalo in AEM Storefront

## Data di rilascio: ottobre 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.10.20.02 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| Componenti core CIF | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| Sito di riferimento CIF Venia | 2021.11.2001 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### Novità {#what-is-new-october}

* Il componente aggiuntivo CIF supporta la versione più recente di Commerce v2.4.3 con nuovi API e schemi di GraphQL

* Gli autori possono aggiungere collegamenti alle pagine di prodotti e cataloghi nei campi di testo utilizzando l’editor Rich Text. Alla barra degli strumenti dell’editor Rich Text è stata aggiunta un’icona CIF che apre i selettori per cercare e selezionare rapidamente il prodotto o la categoria senza uscire dal contesto.

* I carrelli e le pagine di pagamento pop-up esistenti sono stati sostituiti da carrelli e pagine di pagamento dedicati per l’AEM. I componenti di queste pagine vengono generati utilizzando i componenti PEGRA estensibili di Adobe Commerce

* Gli esercenti possono nascondere determinate categorie del catalogo dei prodotti nella navigazione utilizzando il backend di Commerce. Il componente core Navigazione CIF rispetta la configurazione back-end per l’e-commerce &quot;includi nel menu&quot; per mostrare/nascondere le categorie nella navigazione

* AEM Storefront Venia restituisce l’errore HTTP 404 se la pagina della categoria o del prodotto non è stata trovata

## Data di rilascio: settembre 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 27.9.2021 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| Componenti core CIF | 2.2.0. | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| Sito di riferimento CIF Venia | 23.9.2021 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Novità {#what-is-new-september}

* La nuova scheda &quot;Contenuto e-commerce associato&quot; nell’editor di Sites aumenta l’efficienza dell’autore grazie all’accesso rapido ai contenuti dei prodotti AEM pertinenti per il contesto corrente

  ![Contenuto commerce associato](/help/assets/CIF/associated-commerce-content.png)

* È stata migliorata l’interfaccia utente per la selezione dei prodotti, per una migliore esperienza utente, una maggiore efficienza e il supporto per cataloghi di prodotti complessi

  ![Nuovo selettore prodotti](/help/assets/CIF/product-picker.png)

* Rispetta la proprietà &quot;include_in_menu&quot; nel componente di navigazione

### Correzioni di bug {#bug-fixes-september}

* Lo svuotamento della cache del menu non funziona come previsto

* Errori JS durante il passaggio di distribuzione di AEM CS e quando non si utilizzano componenti lato client

* Impossibile creare la configurazione cloud CIF nelle cartelle con un nodo sling:configs

## Data di rilascio: agosto 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.09.02 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| Componenti core CIF | 2.1.0. | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Sito di riferimento CIF Venia | 27.8.2021 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Novità {#what-is-new-august}

* Nuova interfaccia utente per il selettore delle categorie per migliorare l’esperienza utente, l’efficienza e il supporto per cataloghi di prodotti complessi

  ![Selezione nuova categoria](/help/assets/CIF/category-picker.png)

* Migliore supporto A11Y per i componenti core CIF

### Correzioni di bug {#bug-fixes-august}

* Impossibile chiudere il pannello a soffietto del filtro categorie una volta aperto

* Proprietà &quot;Testo invito all’azione&quot; interrotta nel teaser del prodotto

* Errori CIF JS durante la fase di distribuzione di AEM CS

* Correggi l&#39;accesso ai prodotti non elaborati per gli elementi dell&#39;elenco di prodotti mappati

## Data di rilascio: luglio 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 21.7.2021 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Componenti core CIF | 2,0,0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Sito di riferimento CIF Venia | 22.7.2021 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Novità {#what-is-new-july}

* Componenti core CIF v2
   * Configurazioni semplificate e migliorate per URL PDP/PLP e SEO
   * Indicatore visivo per i dati di prodotto in staging in modalità di authoring per una migliore visibilità delle modifiche imminenti
   * Nuovo componente sitemap per contenuti e pagine commerce

* Supporto per [Adobe Commerce Sensei Product Recommendations, basato su Adobe Sensei](https://business.adobe.com/it/products/magento/product-recommendations.html) in AEM Storefront utilizzando consigli predefiniti o creati al volo

## Data di rilascio: giugno 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2021.06.18 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Componenti core CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Sito di riferimento CIF Venia | 2021.06.12. | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Novità {#what-is-new-june}

* Nuovi tipi di dati di riferimento per prodotti e categorie CIF per Frammenti di contenuto (incl. supporto dell’interfaccia utente per il selettore di prodotti/categorie)
* Nuovo componente core Frammento di contenuto di Commerce
* Ricerca e-commerce full-text supportata nel back-end AEM
* I componenti core Commerce supportano la raccolta dati Adobe Commerce Sensei Recs
* Sono stati migliorati gli URL SEO-friendly per le pagine delle categorie
* Supporto per intestazioni HTTP personalizzate per sito/configurazione

## Data di rilascio: maggio 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 26.5.2021 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Componenti core CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Sito di riferimento CIF Venia | 24.5.2021 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Novità {#what-is-new-may}

* Supporto dell’impaginazione per il contenuto associato nelle proprietà della console del prodotto

### Correzioni di bug {#bug-fixes-may}

* Le miniature delle risorse non vengono visualizzate nella scheda Risorsa delle proprietà del prodotto

* Breadcrumb ripristina i dati di anteprima nella console prodotto

## Data di rilascio: aprile 2021

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 22.04.2021 | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componenti core CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 22.04.2021 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità {#what-is-new-april}

* Supporto per la categoria UID: questo consente di sbloccare le integrazioni con e-commerce di terze parti per i sistemi che utilizzano Stringhe per gli ID categoria

* Estensione AEM per il PWA Studi, incl. integrazione di esempio

* Nuovo componente core di navigazione CIF che estende il componente core di navigazione WCM

### Correzioni di bug {#bug-fixes-april}

* Il campo della categoria principale non veniva visualizzato nella scheda Commerce nelle proprietà della pagina delle pagine delle categorie

## Data di rilascio: marzo 2021 {#what-is-new-march}

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 1,9,0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 1,9,0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 25.3.2021 | [Note sulla versione](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità

* Supporto per Adobe Commerce 2.4.2

### Novità

* È stata migliorata la riutilizzabilità del componente dei dettagli del prodotto per le pagine basate su contenuti

* Migliore caching e meno chiamate back-end per i PDP

* Correzioni di bug multipli.

## Data di rilascio: febbraio 2021

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 1,8,0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 1,8,0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 24.02.2021 | [Note sulla versione](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità {#what-is-new-february}

* Gestione dell’esperienza del prodotto: arricchisci le pagine dei cataloghi di prodotti singolarmente con Frammenti esperienza.

* Proprietà estese della console prodotti per mostrare Assets collegato e frammenti di esperienza, con azioni per passare rapidamente al contenuto associato.

### Novità  {#what-is-improved-february}

* Livello dati lato client migliorato con URL dell&#39;immagine del prodotto e informazioni sulla categoria.

* Correzioni di bug multipli.

## Data di rilascio: gennaio 2021

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 1,7,0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 1,7,0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Sito di riferimento CIF Venia | 2021.02.02 | [Note sulla versione](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novità {#what-is-new-january}

* Gestione dell’esperienza del prodotto: nuova scheda della proprietà &quot;Commerce&quot; per Assets e Frammenti esperienza. Questa scheda consente di collegare Assets e Frammenti di esperienza a prodotti e categorie. La scheda mostra anche i dati in tempo reale per gli oggetti commerce collegati e un collegamento per mostrare i dettagli nella console del prodotto.

### Novità  {#what-is-improved-january}

* Invia dati utente dopo l’autenticazione a Adobe Client Data Layer.

* Correzioni di bug multipli.
