---
title: Migrazione al componente aggiuntivo CIF (AEM Commerce Integration Framework)
description: Come migrare al componente aggiuntivo CIF di AEM Commerce Integration Framework (CIF) da una versione precedente
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Guida alla migrazione per il componente aggiuntivo Experience Manager {#cif-migration}

Questa guida aiuta a identificare le aree da aggiornare per la migrazione dei componenti aggiuntivi di Experience Manager.

## Componente aggiuntivo CIF

Il componente aggiuntivo CIF è disponibile per AEM 6.5 tramite il [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). È compatibile e fornisce le stesse funzionalità del componente aggiuntivo CIF, ad Experience Manager come Cloud Service.

Consulta [Guida introduttiva a Contenuto AEM e Commerce](getting-started.md).

Per supportare i progetti che implementano CIF, Adobe fornisce [AEM componenti core CIF](https://github.com/adobe/aem-core-cif-components).

## Catalogo dei prodotti

L’importazione dei dati del catalogo dei prodotti non è supportata dal componente aggiuntivo CIF. Utilizzando i componenti aggiuntivi CIF, le richieste di prodotti e catalogo sono on-demand tramite chiamate in tempo reale a una soluzione commerce esterna. Vai a capitolo Integrazione per ulteriori informazioni sull&#39;integrazione di una soluzione commerce.

>[!TIP]
>
>Se non sono disponibili API in tempo reale, per l’integrazione è necessario utilizzare una cache di prodotto esterna con API. Esempio [Magento open-source](https://magento.com/products/magento-open-source).

## Esperienze nel catalogo dei prodotti con il rendering AEM

Se utilizzi la blueprint del catalogo con Classic CIF, devi aggiornare il flusso di lavoro del catalogo dei prodotti. Il componente aggiuntivo CIF ora esegue il rendering immediato delle esperienze di catalogo di prodotti utilizzando AEM modelli di catalogo. Non è più necessaria alcuna replica dei dati di prodotto o delle pagine di prodotto.

## Dati non memorizzabili nella cache e interazione di acquisto

Le richieste lato client per dati e interazioni non memorizzabili nella cache (ad esempio add-to-cart, search) devono passare direttamente all’endpoint commerce (soluzione commerce o livello di integrazione) tramite CDN/Dispatcher. Rimuovi tutte le chiamate in cui AEM solo un proxy.
