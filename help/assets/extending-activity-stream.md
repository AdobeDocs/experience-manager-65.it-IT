---
title: Integrare le risorse con il flusso di attività
description: Descrive le funzionalità di registrazione di Experience Manager e come configurarle per registrare eventi specifici.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Integrare le risorse con il flusso di attività {#integrating-assets-with-activity-stream}

Gli utenti di Risorse Adobe Experience Manager eseguono numerose azioni come creazione, caricamento ed eliminazione di risorse. Queste azioni possono essere registrate in modo da fornire una cronologia delle operazioni eseguite da un utente. Questa sezione descrive le funzionalità di registrazione di Experience Manager e come configurare Experience Manager per registrare eventi specifici.

## Considerazioni sulle prestazioni e comportamento predefinito {#performance-considerations-and-default-behavior}

Questa integrazione potrebbe richiedere CPU e spazio su disco, ad esempio durante l&#39;importazione in massa. Per questi motivi l&#39;integrazione delle risorse con il Flusso attività è disabilitata per impostazione predefinita.

## Eventi azione supportati {#supported-action-events}

È possibile configurare i seguenti eventi per la registrazione:

* Licenza accettata (ACCETTATA)
* Risorsa creata (ASSET_CREATED)
* Risorsa spostata (ASSET_MOVED)
* Risorsa rimossa (ASSET_REMOVED)
* Licenza rifiutata (RIFIUTATA)
* Risorsa scaricata (SCARICATA)
* Versione risorsa (VERSIONE)
* Versione risorsa ripristinata (RIPRISTINATA)
* Metadati risorsa aggiornati (METADATA_UPDATED)
* Risorsa pubblicata nel sistema esterno (PUBLISHED_EXTERNAL)
* Aggiornamento originale della risorsa (ORIGINAL_UPDATED)
* Rendering risorsa aggiornata (RENDITION_UPDATED)
* Rendering risorsa rimosso (RENDITION_REMOVED)
* Risorsa secondaria aggiornata (SUBASSET_UPDATED)
* Risorsa secondaria rimossa (SUBASSET_REMOVED)

## Configurazione della registrazione degli eventi delle risorse {#configuring-aem-assets-events-recording}

La console [](/help/sites-deploying/configuring-osgi.md) Web consente di accedere al tuning del registratore eventi delle risorse. Per configurare il Registratore eventi risorse, effettuate le seguenti operazioni:

1. Passare alla console **[!UICONTROL Web]**

1. Fate clic su **[!UICONTROL Configurazione]**.

1. Fate doppio clic su Registratore **[!UICONTROL eventi CQ DAM]** Day.

1. Seleziona **[!UICONTROL Abilita il servizio]**.

1. Verificare i tipi **[!UICONTROL di]** evento da registrare nel flusso di attività dell&#39;utente.

1. Fai clic su **[!UICONTROL Salva]**.

## Lettura degli eventi registrati {#reading-recorded-events}

Gli eventi registrati vengono memorizzati come attività. Potete leggerli a livello di programmazione utilizzando l&#39;API [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)ActivityManager.
