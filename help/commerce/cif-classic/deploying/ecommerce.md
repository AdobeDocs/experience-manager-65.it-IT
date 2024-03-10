---
title: Panoramica di eCommerce
description: L’eCommerce generico AEM è disponibile come parte dell’installazione standard e offre tutte le funzionalità del framework eCommerce.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# Panoramica di eCommerce{#ecommerce-overview}

L’eCommerce generico AEM è disponibile come parte di un’installazione standard e offre tutte le funzionalità del framework eCommerce.

L&#39;Adobe fornisce due versioni della Commerce integration framework:

|                         | CIF on-premise | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versioni di AEM supportate | AEM on-prem o AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java™ <br> - Integrazione monolitica, mappatura pre-build (modello)<br> - Archivio JCR | - ADOBE COMMERCE <br>- Java e JavaScript <br>- Nessun dato Commerce memorizzato nell’archivio JCR |
| Front-end | Pagine sottoposte a rendering lato server dell’AEM | Applicazione a pagina mista (rendering ibrido) |
| Catalogo prodotti | - Importazione prodotti, editor, caching in AEM <br>- Cataloghi regolari con pagine AEM o proxy | - Nessuna importazione di prodotti <br>- Modelli generici <br>- Dati on-demand tramite connettore |
| Scalabilità | - Può supportare fino a pochi milioni di prodotti (a seconda del caso d’uso) <br> - Memorizzazione in cache in Dispatcher | - Nessun limite di volume <br>- Memorizzazione in cache su Dispatcher o CDN |
| Modello dati standardizzato | No | Sì, schema Adobe Commerce GraphQL |
| Disponibilità | Sì:<br> - Commerce Cloud SAP (estensione aggiornata per supportare AEM 6.4 e Hybris 5 (impostazione predefinita) e mantenere la compatibilità con Hybris 4 <br>- Commerce Cloud Salesforce (connettore open source per supportare AEM 6.4) | Sì tramite open source tramite GitHub. <br> Adobe Commerce (supporta 2.3.2 (impostazione predefinita) e compatibile con 2.3.1). |
| Quando utilizzare | Casi d’uso limitati: per scenari in cui piccoli cataloghi statici vengono importati in base alle esigenze | Soluzione preferita nella maggior parte dei casi d’uso |


## Distribuzione di altre implementazioni {#deploying-other-implementations}

Per AEM e Adobe Commerce, consulta [Integrazione di AEM e Adobe Commerce](/help/commerce/cif/integrating/magento.md) utilizzando [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Per informazioni sui concetti e sull’amministrazione delle implementazioni di eCommerce, consulta [Amministrazione di eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Per informazioni sull’estensione delle funzionalità di eCommerce, consulta [Sviluppo dell’eCommerce](/help/commerce/cif-classic/developing/ecommerce.md).
