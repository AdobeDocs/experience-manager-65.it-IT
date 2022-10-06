---
title: Integrare [!DNL Assets] con flusso di attività
description: Descrive le funzionalità di registrazione di [!DNL Experience Manager] e come configurarlo per registrare eventi specifici.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Integrare [!DNL Assets] con flusso di attività {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] gli utenti eseguono molte azioni, come creare, caricare ed eliminare le risorse. Queste azioni possono essere registrate in modo da fornire una cronologia di ciò che è stato fatto da un utente. Questa sezione descrive le funzionalità di registrazione di [!DNL Experience Manager] e come configurare [!DNL Experience Manager] per registrare eventi specifici.

## Considerazioni sulle prestazioni e comportamento predefinito {#performance-considerations-and-default-behavior}

Questa integrazione potrebbe richiedere CPU e spazio su disco, ad esempio durante l&#39;importazione in massa. Per queste ragioni, [!DNL Assets] L’integrazione con Activity Stream è disabilitata per impostazione predefinita.

## Eventi azione supportati {#supported-action-events}

È possibile configurare i seguenti eventi per la registrazione:

* Licenza accettata (ACCETTATA)
* Risorsa creata (ASSET_CREATED)
* Risorsa spostata (ASSET_MOVED)
* Risorsa rimossa (ASSET_REMOVED)
* Licenza rifiutata (RIFIUTATA)
* Risorsa scaricata (SCARICATA)
* Versione risorsa (VERSIONED)
* Versione risorsa ripristinata (RIPRISTINATA)
* Metadati risorsa aggiornati (METADATA_UPDATED)
* Risorsa pubblicata nel sistema esterno (PUBLISHED_EXTERNAL)
* Aggiornato originale della risorsa (ORIGINAL_UPDATED)
* Rendering risorsa aggiornato (RENDITION_AGGIORNATO)
* Rendering risorsa rimosso (RENDITION_REMOVED)
* Risorsa secondaria aggiornata (SUBASSET_UPDATED)
* Risorsa secondaria rimossa (SUBASSET_REMOVED)

## Configura [!DNL Assets] registrazione eventi {#configuring-aem-assets-events-recording}

La [Console web](/help/sites-deploying/configuring-osgi.md) consente di accedere alla regolazione del Registratore eventi di Assets. Per configurare il Registratore eventi di Assets, procedi come segue:

1. Passa a **[!UICONTROL Console web]**

1. Fai clic su **[!UICONTROL Configurazione]**.

1. Doppio clic **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Controlla **[!UICONTROL Abilita questo servizio]**.

1. Controlla quali **[!UICONTROL Tipi di eventi]** vuoi essere registrato nel flusso di attività dell’utente.

1. Fai clic su **[!UICONTROL Salva]**.

## Leggi gli eventi registrati {#reading-recorded-events}

Gli eventi registrati vengono memorizzati come attività. Puoi leggerle a livello di programmazione utilizzando il [API di ActivityManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
