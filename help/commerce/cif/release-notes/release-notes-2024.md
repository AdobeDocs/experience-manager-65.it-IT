---
title: Contenuto dell’AEM e note sulla versione 2024 di Commerce
description: Note sulla versione 2024 di Adobe Experience Manager Content and Commerce.
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 26%

---

# Panoramica sulla versione di Commerce integration framework GitHub

## Panoramica dei requisiti di sistema

Esaminare i requisiti minimi di sistema riportati nella tabella seguente per la versione dell&#39;CIF attualmente in uso o che si prevede di utilizzare in futuro.

| Componente | Requisiti di sistema |
|:-------|:-----------------------------------------------------------------------------------------------:|
| Componente aggiuntivo CIF | Minimo: AEM 6.5.18, schemi Adobe Commerce 2.3.5 GraphQL |
| Componenti core CIF | [Requisiti di sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archetipo progetto AEM | [Requisiti di sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data di rilascio: ottobre 2024

| Componente | Versione | Dettagli |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componenti core CIF | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### Correzioni di bug {#bug-fixes-October}

* Sono stati corretti i test dell’interfaccia utente per il corretto funzionamento con i componenti core CIF.
* È stato risolto un problema a causa del quale il formato dell’URL della categoria non funzionava come previsto nell’istanza cloud.

## Data di rilascio: settembre 2024

| Componente | Versione | Dettagli |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componenti core CIF | 2.14.2. | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### Miglioramenti {#improvements-September}

* Rendere personalizzabile il limite delle categorie.

### Correzioni di bug {#bug-fixes-September}

* I campi di Commerce non sono correttamente integrati nell’editor schema metadati di Assets.
* Problema con più campi dei prodotti carosello per il trascinamento.
* Problema con il multicampo della categoria Carosello per il trascinamento
* Il clic non funziona per i menu nella pagina Informazioni pagina nell’editor categoria e prodotto.
* Il campo Numero ordine non è visibile nella pagina di conferma dell’ordine.

## Data di rilascio: gennaio 2024

| Componente | Versione | Dettagli |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componenti core CIF | 2.12.6. | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### Correzioni di bug {#bug-fixes-january}

* È stato corretto il pulsante Aggiungi al carrello ed Aggiungi alla lista dei desideri nel componente per la raccolta di prodotti
