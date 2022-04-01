---
title: Note sulla versione 2022 di AEM Content and Commerce
description: Note sulla versione 2022 di AEM Content and Commerce
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 27%

---

# Panoramica sulla versione di Commerce Integration Framework GitHub

## Panoramica dei requisiti di sistema

Rivedi i requisiti minimi di sistema nella tabella seguente per la versione CIF in uso o che intendi utilizzare in futuro.

| Componente | Requisiti di sistema |
|:-------|:-----:|
| Componente aggiuntivo CIF | Minimo: AEM 6.5.7, Magento 2.3.5 Schema GraphQL |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archetipo progetto AEM | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data di rilascio: Marzo 2022

| Componente | Versione | Dettagli |
|:-------|:-----:|---------------------:|
| Componente aggiuntivo CIF | 2022.02.24.00 | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Componenti core CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Sito di riferimento CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Novità {#what-is-new-march}

* Beta: Supporto per i componenti core di ricerca CIF di AEM Commerce LiveSearch
* SEO migliorato per scenari multi-store: È ora possibile configurare i formati URL per PDP/PLP a livello di archivio tramite le proprietà CIF Cloud Config
* Il selettore prodotti supporta i prodotti in staging tramite la nuova opzione di filtro nell’interfaccia utente.  In questo modo i professionisti dei contenuti possono preparare la gestione dei contenuti dei prodotti per i prossimi lanci
* Gestione semplificata della configurazione CIF e degli errori utilizzando il nome della configurazione cloud CIF anziché l’URL proxy
* Selezione manuale della categoria per l’elenco dei prodotti e i componenti Carosello. Questo consente agli utenti del contenuto di utilizzare questi componenti sulle pagine di contenuto, al di fuori dell’esperienza del catalogo

## Data di rilascio: Gennaio 2022

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
