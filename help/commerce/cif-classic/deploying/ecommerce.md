---
title: Panoramica di eCommerce
seo-title: eCommerce Overview
description: AEM eCommerce generico è disponibile come parte dell’installazione standard e offre tutte le funzionalità del framework eCommerce.
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# Panoramica di eCommerce{#ecommerce-overview}

AEM eCommerce generico è disponibile come parte di un’installazione standard e offre tutte le funzionalità del framework eCommerce.

In Adobe sono disponibili due versioni di Commerce Integration Framework:

|  | CIF on-prem | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versioni di AEM supportate | AEM on-premise o AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java <br> - Integrazione monolitica, mappatura pre-compilazione (modello)<br> - Archivio JCR | - Adobe Commerce <br>- Java e JavaScript <br>- Nessun dato Commerce memorizzato nell&#39;archivio JCR |
| Front-end | AEM pagine di rendering lato server | Applicazione a pagina mista (rendering ibrido) |
| Catalogo dei prodotti | - Importazione prodotti, editor, memorizzazione in cache in AEM <br>- Cataloghi regolari con pagine AEM o proxy | - Nessuna importazione di prodotti <br>- Modelli generici <br>- Dati on-demand tramite connettore |
| Scalabilità | - Può supportare fino a pochi milioni di prodotti (dipende dal caso d&#39;uso) <br> - Memorizzazione in cache su Dispatcher | - Nessuna limitazione del volume <br>- Memorizzazione in cache su Dispatcher o CDN |
| Modello dati standardizzato | No | Sì, schema GraphQL di Adobe Commerce |
| Disponibilità | Sì:<br> - Commerce Cloud SAP (estensione aggiornata per supportare AEM 6.4 e Hybris 5 (impostazione predefinita) e mantenere la compatibilità con Hybris 4 <br>- Commerce Cloud Salesforce (connettore open source per supportare AEM 6.4) | Sì tramite open source tramite GitHub. <br> Adobe Commerce (Supporta 2.3.2 (predefinito) e compatibile con 2.3.1). |
| Quando utilizzare | Casi d’uso limitati: Per gli scenari in cui possono essere necessari l’importazione di cataloghi statici di piccole dimensioni | Soluzione preferita nella maggior parte dei casi d&#39;uso |


## Distribuzione di altre implementazioni {#deploying-other-implementations}

Per AEM e Adobe Commerce, consulta [Integrazione AEM e Adobe Commerce](/help/commerce/cif/integrating/magento.md) utilizzando [Commerce Integration Framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Per informazioni sui concetti e sull’amministrazione delle implementazioni di eCommerce, consulta [Amministrazione di eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Per informazioni sull’estensione delle funzionalità di eCommerce, consulta [Sviluppo di eCommerce](/help/commerce/cif-classic/developing/ecommerce.md).
