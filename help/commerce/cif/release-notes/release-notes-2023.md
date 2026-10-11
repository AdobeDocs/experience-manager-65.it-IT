---
title: Note sulla versione 2023 di AEM Content and Commerce
description: Note sulla versione 2023 di Adobe Experience Manager Content and Commerce.
exl-id: 00349400-6860-4e3c-ba56-fa12afc5db1d
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 20%
---
# Panoramica sulla versione di Commerce integration framework GitHub

## Panoramica dei requisiti di sistema

Esaminare i requisiti minimi di sistema nella tabella seguente per la versione di CIF in uso o che si prevede di utilizzare in futuro.

| Componente | Requisiti di sistema |
|:-------|:-----------------------------------------------------------------------------------------------:|
| Componente aggiuntivo CIF | Minimo: schemi AEM 6.5.8, Adobe Commerce 2.3.5 GraphQL |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archetipo di progetto AEM | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data di rilascio: dicembre 2023

| Componente | Versione | Dettagli |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componenti core CIF | 2.12.4 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.4) |

### Correzioni di bug {#bug-fixes-december}

* Servlet di reindirizzamento di prodotti e categorie registrati per il tipo di risorsa Pagina v3
* Correggere gli eventi di ricerca live dell’estensione CIF AEP

## Data di rilascio: novembre 2023

| Componente | Versione | Dettagli |
|:-------|:-------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Componente aggiuntivo CIF | 2023.11.23.00 | [Distribuzione del software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2023.11.23.00.zip) |
| Sito di riferimento CIF Venia | 2023.11.08 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2023.11.08) |

### Correzioni di bug {#bug-fixes-november}

* Visualizzazione di più di 40 configurazioni nella console Configurazioni CIF

## Data di rilascio: luglio 2023

| Componente | Versione | Dettagli |
|:-------|:-------:|--------------------------------------------------------------------------------------------------------------:|
| Componenti core CIF | 2.12.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.2) |

### Novità {#what-is-new-july}

* Gli hook del filtro prodotti nel componente `ProductList`
