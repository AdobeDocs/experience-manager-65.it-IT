---
title: Migrazione al componente aggiuntivo AEM Commerce integration framework (CIF)
description: Come migrare al componente aggiuntivo AEM Commerce integration framework (CIF) da una versione precedente.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: b4056a4c1483dc8dcedc3c0f8f6b42f8dead0847
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---

# Guida alla migrazione per il componente aggiuntivo Experience Manager {#cif-migration}

Questa guida aiuta a identificare le aree da aggiornare per la migrazione del componente aggiuntivo Experience Manager.

## Componente aggiuntivo CIF

Il componente aggiuntivo CIF è disponibile per AEM 6.5 tramite il [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=commerce*&amp;2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&amp;2_group.propertyvalues.operation=equals&amp;2_group.propertyvalues.0_values=versione-destinazione%3Aaem%2F6-5&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=16). È compatibile e fornisce le stesse funzioni del componente aggiuntivo CIF per Experience Manager as a Cloud Service.

Consulta [Guida introduttiva a AEM Content e Commerce](getting-started.md).

Per supportare i progetti che utilizzano CIF, Adobe fornisce [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components).

## Catalogo prodotti

L&#39;importazione dei dati del catalogo dei prodotti non è supportata dal componente aggiuntivo CIF. Utilizzando gli utenti/gruppi/ruoli del componente aggiuntivo CIF, le richieste di prodotti e cataloghi vengono inviate su richiesta tramite chiamate in tempo reale a una soluzione di e-commerce esterna. Per ulteriori informazioni sull’integrazione di una soluzione commerce, consulta il capitolo Integrazione.

>[!TIP]
>
>Se non sono disponibili API in tempo reale, per l’integrazione deve essere utilizzata una cache di prodotto esterna con API. Esempio [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Esperienze nel catalogo dei prodotti con AEM Rendering

Se utilizzi la blueprint del catalogo con Classic CIF, devi aggiornare il flusso di lavoro del catalogo dei prodotti. Il componente aggiuntivo CIF ora esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM. Non è più richiesta la replica dei dati di prodotto o delle pagine di prodotto.

## Dati non memorizzabili in cache e interazione con la spesa

Le richieste lato client per dati e interazioni non memorizzabili in cache (ad esempio, add-to-cart, ricerca) devono passare direttamente all’endpoint commerce (soluzione commerce o livello di integrazione) tramite CDN/Dispatcher. Rimuovi eventuali chiamate in cui AEM era solo un proxy.
