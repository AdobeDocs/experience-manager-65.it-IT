---
title: Note sulla versione 2022 di AEM Content and Commerce
description: Note sulla versione 2022 di AEM Content and Commerce
source-git-commit: 84ac40a5cd18b1a5c8bb7a93af4106be6bda7631
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 45%

---

# Panoramica sulla versione di Commerce Integration Framework GitHub

## Panoramica dei requisiti di sistema

Rivedi i requisiti minimi di sistema nella tabella seguente per la versione CIF in uso o che intendi utilizzare in futuro.

| Componente | Requisiti di sistema |
|:-------|:-----:|
| Componente aggiuntivo CIF | Minimo: AEM 6.5.7, Magento 2.3.5 Schema GraphQL |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archetipo progetto AEM | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

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

