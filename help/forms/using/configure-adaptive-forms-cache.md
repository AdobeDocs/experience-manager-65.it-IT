---
title: Configurare la cache dei moduli adattivi
seo-title: Configurare la cache dei moduli adattivi
description: 'La cache dei moduli adattivi è stata progettata specificatamente per moduli e documenti adattivi. Memorizza nella cache moduli adattivi e documenti adattivi allo scopo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client. '
seo-description: 'La cache dei moduli adattivi è stata progettata specificatamente per moduli e documenti adattivi. Memorizza nella cache moduli adattivi e documenti adattivi allo scopo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Configurare la cache dei moduli adattivi{#configure-adaptive-forms-cache}

Una cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di ingresso/uscita (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare i dati precompilati. Consente di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client. È progettata specificamente per i moduli adattivi e supporta anche i documenti adattivi.

>[!NOTE]
>
>Quando si utilizza la cache dei moduli adattivi, AEM Dispatcher consente di memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo o di un documento adattivo.

>[!NOTE]
>
>Durante lo sviluppo di componenti personalizzati, sul server utilizzato per lo sviluppo, mantenere disattivata la cache dei moduli adattivi.

## Configurare la cache {#configure-the-cache}

Per configurare la cache dei moduli adattivi, effettuate le seguenti operazioni:

1. Andate al gestore di configurazione della console Web AEM all&#39;indirizzo https://[server]:[port]/system/console/configMgr.
1. Fate clic su Configurazione **canale Web per moduli** adattivi e comunicazioni interattive per modificarne i valori di configurazione.
1. Nella finestra di dialogo Modifica valori di configurazione, specificare il numero massimo di moduli o documenti che un’istanza del server AEM Forms può memorizzare nella cache nel campo **Numero di moduli** adattivi. Il valore predefinito è 100.

   >[!NOTE]
   >
   >Per disabilitare la cache, impostare il valore nel campo Numero di moduli adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

   ![Finestra di dialogo di configurazione per la cache HTML dei moduli adattivi](assets/cache-configuration-edit.png)

1. Click **Save** to save the configuration.

