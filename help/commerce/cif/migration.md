---
title: Migrazione al componente aggiuntivo Commerce integration framework AEM (CIF)
description: Come migrare al componente aggiuntivo AEM Commerce integration framework (CIF) da una versione precedente.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Guida alla migrazione per il componente aggiuntivo Experience Manager {#cif-migration}

Questa guida aiuta a identificare le aree da aggiornare per la migrazione del componente aggiuntivo Experience Manager.

## Componente aggiuntivo CIF

Il componente aggiuntivo CIF è disponibile per AEM 6.5 tramite il [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). È compatibile e offre le stesse caratteristiche del componente aggiuntivo CIF, ad Experience Manager as a Cloud Service.

Consulta [Guida introduttiva a AEM Content and Commerce](getting-started.md).

Per supportare i progetti che utilizzano l’CIF, Adobe fornisce [Componenti core dell’CIF dell’AEM](https://github.com/adobe/aem-core-cif-components).

## Catalogo prodotti

L’importazione dei dati del catalogo dei prodotti non è supportata dal componente aggiuntivo CIF. Utilizzando i principal del componente aggiuntivo CIF, le richieste di prodotti e cataloghi vengono effettuate on-demand tramite chiamate in tempo reale a una soluzione di e-commerce esterna. Per ulteriori informazioni sull’integrazione di una soluzione commerce, consulta il capitolo Integrazione.

>[!TIP]
>
>Se non sono disponibili API in tempo reale, per l’integrazione deve essere utilizzata una cache di prodotto esterna con API. Esempio [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Esperienze nel catalogo dei prodotti con rendering AEM

Se utilizzi la blueprint del catalogo con CIF classico, devi aggiornare il flusso di lavoro del catalogo dei prodotti. Il componente aggiuntivo CIF ora esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM. Non è più richiesta la replica dei dati di prodotto o delle pagine di prodotto.

## Dati non memorizzabili in cache e interazione con la spesa

Le richieste lato client per dati e interazioni non memorizzabili in cache (ad esempio, add-to-cart, ricerca) devono passare direttamente all’endpoint commerce (soluzione commerce o livello di integrazione) tramite CDN/Dispatcher. Rimuovi eventuali chiamate in cui AEM era solo un proxy.
