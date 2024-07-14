---
title: Integra [!DNL Assets]  con flusso attività
description: Descrive le funzionalità di registrazione di  [!DNL Experience Manager]  e come configurarle per registrare eventi specifici.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Integra [!DNL Assets] con il flusso di attività {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] utenti eseguono molte azioni come la creazione, il caricamento e l&#39;eliminazione di Assets. Puoi registrare queste azioni in modo da fornire una cronologia di ciò che è stato fatto da un utente. In questa sezione vengono descritte le funzionalità di registrazione di [!DNL Experience Manager] e viene descritto come configurare [!DNL Experience Manager] per registrare eventi specifici.

## Considerazioni sulle prestazioni e comportamento predefinito {#performance-considerations-and-default-behavior}

Questa integrazione potrebbe richiedere l’utilizzo di CPU e spazio su disco, ad esempio durante l’importazione in blocco. Per questi motivi, l&#39;integrazione di [!DNL Assets] con il flusso di attività è disabilitata per impostazione predefinita.

## Eventi di azione supportati {#supported-action-events}

Puoi configurare i seguenti eventi da registrare:

* Licenza accettata (ACCETTATA)
* Risorsa creata (ASSET_CREATED)
* Risorsa spostata (ASSET_MOVE)
* Risorsa rimossa (ASSET_REMOVED)
* Licenza rifiutata (RIFIUTATA)
* Risorsa scaricata (DOWNLOADED)
* Risorsa con versione (CON VERSIONE)
* Versione risorsa ripristinata (RIPRISTINATA)
* Metadati risorsa aggiornati (METADATA_UPDATED)
* Risorsa pubblicata su un sistema esterno (PUBLISHED_EXTERNAL)
* Risorsa originale aggiornata (ORIGINAL_UPDATED)
* Rappresentazione risorsa aggiornata (RENDITION_UPDATED)
* Rappresentazione risorsa rimossa (RENDITION_REMOVED)
* Risorsa secondaria aggiornata (SUBASSET_UPDATED)
* Risorsa secondaria rimossa (SUBASSET_REMOVED)

## Configura registrazione di [!DNL Assets] eventi {#configuring-aem-assets-events-recording}

La [console Web](/help/sites-deploying/configuring-osgi.md) fornisce l&#39;accesso al tuning di Assets Event Recorder. Per configurare Assets Event Recorder, procedere come segue:

1. Passa alla **[!UICONTROL console Web]**

1. Fare clic su **[!UICONTROL Configurazione]**.

1. Fare doppio clic su **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Seleziona **[!UICONTROL Abilita il servizio]**.

1. Controlla quali **[!UICONTROL Tipi di evento]** desideri registrare nel flusso dell&#39;attività utente.

1. Fai clic su **[!UICONTROL Salva]**.

## Leggi eventi registrati {#reading-recorded-events}

Gli eventi registrati vengono memorizzati come attività. È possibile leggerli a livello di programmazione utilizzando l&#39;[API ActivityManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
