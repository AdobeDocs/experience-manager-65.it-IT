---
title: Note sulla versione 2022 di AEM Content and Commerce
description: Note sulla versione 2022 di AEM Content and Commerce
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 0fdff88695646603cec120d25f156f8c918686df
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 46%

---

# Panoramica sulla versione GitHub di Commerce Integration Framework

## Panoramica dei requisiti di sistema

Esaminare i requisiti di sistema minimi nella tabella seguente per la versione CIF in uso o che si prevede di utilizzare in futuro.

| Componente | Requisiti di sistema |
|:-------|:-----:|
| Componente aggiuntivo CIF | Minimo: schemi GraphQL del Magento 2.3.5 per AEM 6.5.7 |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archetipo progetto AEM | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data di rilascio: settembre 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.09.20.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| Componenti core CIF | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| Sito di riferimento CIF Venia | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### Novità {#what-is-new-september}

* Gli autori possono arricchire dinamicamente gli elenchi di prodotti con Frammenti di esperienza (ad esempio, inserendo un banner tra le voci dei prodotti elencati)
* Il componente Elenco supporta le pagine di prodotti/categorie associate per mostrare in modo dinamico le pagine correlate
* Supporto per componenti Peregrine 12.5
* Supporto per il caricamento dei prezzi lato client nel teaser e nel carosello dei prodotti

## Data di rilascio: luglio 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.08.02.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Novità {#what-is-new-july}

* Associazione di pagine AEM a prodotti e categorie tramite le proprietà della pagina AEM e panoramica nella cabina di comando del prodotto
   ![associazione pagina pannello di comando del prodotto](/help/assets/CIF/product_cockpit_page_association.png)

## Data di rilascio: giugno 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.07.05.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Componenti core CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Sito di riferimento CIF Venia | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Novità {#what-is-new-june}

* L’arricchimento del catalogo dei prodotti ora supporta le pagine AEM. Questo consente agli autori di gestire l’associazione pagina - prodotto.

* Vari miglioramenti dei componenti core CIF

### Correzioni di bug {#bug-fixes-june}

* Aggiungere token di accesso al recupero prezzi lato client

* Componente pagina errato in Data Layer

## Data di rilascio: maggio 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.05.31.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| Componenti core CIF | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| Sito di riferimento CIF Venia | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Novità {#what-is-new-may}

* Nuova pagina delle proprietà del pannello di comando del prodotto, per una panoramica migliore e semplificata

![panoramica delle proprietà del pannello di comando del prodotto](/help/assets/CIF/product_cockpit_properties_overview.png)

* Compatibilità e robustezza migliorate per i connettori di terze parti su I/O Runtime

* Migliora il supporto per le sovrascritture della configurazione client GQL (ad esempio, imposta il comportamento di caching personalizzato)

### Correzioni di bug {#bug-fixes-may}

* Il campo del selettore prodotti con più valori mostra il secondo e gli ulteriori prodotti come non validi

* Il selettore prodotti viene talvolta nascosto dietro i componenti

## Data di rilascio: aprile 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.04.28.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| Componenti core CIF | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| Sito di riferimento CIF Venia | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Novità {#what-is-new-april}

* Accesso rapido alla cabina di comando del prodotto: accesso semplice e dettagliato alle informazioni di prodotto con un solo clic nell’editor di Sites

   ![Abilitare la lista dei desideri](/help/assets/CIF/enable-wishlist.png)

* Supporto per componenti di marketing commerce aggiuntivi: i componenti possono essere configurati per mostrare un’invito all’azione di aggiunta al carrello e aggiunta alla lista dei desideri

   ![Collegamento all’editor di Sites per la cabina di comando del prodotto](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Data di rilascio: febbraio 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.02.24.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Componenti core CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Sito di riferimento CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Novità {#what-is-new-march}

* Beta: supporto per i componenti core di ricerca CIF di AEM Commerce LiveSearch
* SEO migliorata per scenari multi-store: ora puoi configurare i formati URL per PDP/PLP a livello di store tramite le proprietà CIF Cloud Config
* Il selettore prodotti supporta i prodotti in staging tramite la nuova opzione di filtro nell’interfaccia utente.  In questo modo i professionisti dei contenuti possono preparare la gestione contenuti di prodotto per i prossimi lanci
* Gestione semplificata della configurazione CIF e della gestione degli errori utilizzando il nome della configurazione cloud CIF anziché l’URL proxy
* Selezione manuale della categoria per l’elenco dei prodotti e i componenti Carosello. Questo consente agli utenti del contenuto di utilizzare questi componenti sulle pagine di contenuto, al di fuori dell’esperienza del catalogo

## Data di rilascio: gennaio 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.01.20.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| Componenti core CIF | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| Sito di riferimento CIF Venia | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Novità {#what-is-new-january}

* Componenti myAccount migliorati
* Il componente Consiglio di prodotto supporta ulteriori tipi di pagina (pagina home, carrello acquisti, conferma ordine)
* **Lista dei desideri**
   * I visitatori registrati possono aggiungere prodotti a una lista dei desideri
   * È possibile gestire la lista dei desideri e i prodotti contenuti tramite myAccount
   * Il pulsante “Aggiungi alla lista dei desideri” può essere abilitato/disabilitato a livello di componente tramite i criteri (ad esempio, teaser di prodotto, dettaglio di prodotto)
   * Disponibile come componente core e in AEM Venia Storefront

![Lista dei desideri](/help/assets/CIF/wishlist.png)
