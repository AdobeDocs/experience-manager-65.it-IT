---
title: Panoramica di eCommerce
description: L’eCommerce generico AEM è disponibile come parte dell’installazione standard e offre tutte le funzionalità del framework eCommerce.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
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
| Back-end | - AEM, Java™ <br> - Integrazione monolitica, mappatura pre-compilazione (modello)<br> - Archivio JCR | - Adobe Commerce <br>- Java e JavaScript <br>- Nessun dato Commerce archiviato nell&#39;archivio JCR |
| Front-end | Pagine sottoposte a rendering lato server dell’AEM | Applicazione a pagina mista (rendering ibrido) |
| Catalogo prodotti | - Importazione prodotti, editor, caching in AEM <br>- Cataloghi regolari con pagine AEM o proxy | - Nessuna importazione di prodotti <br>- Modelli generici <br>- Dati su richiesta tramite connettore |
| Scalabilità | - Può supportare fino ad alcuni milioni di prodotti (a seconda del caso d’uso) <br> - Memorizzazione in cache su Dispatcher | - Nessun limite di volume <br>- Memorizzazione in cache su Dispatcher o CDN |
| Modello dati standardizzato | No | Sì, schema Adobe Commerce GraphQL |
| Disponibilità | Sì:<br> - Commerce Cloud SAP (estensione aggiornata per supportare AEM 6.4 e Hybris 5 (impostazione predefinita) e mantiene la compatibilità con Hybris 4 <br>- Commerce Cloud Salesforce (connettore open source per supportare AEM 6.4) | Sì tramite open source tramite GitHub. <br> Adobe Commerce (supporta 2.3.2 (impostazione predefinita) e compatibile con 2.3.1). |
| Quando utilizzare | Casi d’uso limitati: per scenari in cui piccoli cataloghi statici vengono importati in base alle esigenze | Soluzione preferita nella maggior parte dei casi d’uso |


## Distribuzione di altre implementazioni {#deploying-other-implementations}

Per AEM e Adobe Commerce, consulta [Integrazione con AEM e Adobe Commerce](/help/commerce/cif/integrating/magento.md) utilizzando [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Per informazioni sui concetti e sull&#39;amministrazione delle implementazioni di eCommerce, vedere [Amministrazione di eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Per informazioni sull&#39;estensione delle funzionalità di eCommerce, vedere [Sviluppo di eCommerce](/help/commerce/cif-classic/developing/ecommerce.md).
