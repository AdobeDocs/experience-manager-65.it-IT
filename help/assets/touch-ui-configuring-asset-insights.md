---
title: Configurare Asset Insights per ottenere l'analisi.
description: Configura approfondimenti risorse in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 8%

---


# Configurare approfondimenti risorse {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti Web di terze parti da [!DNL Adobe Analytics]. Per abilitare Asset Insights per recuperare questi dati e generare approfondimenti, configura innanzitutto la funzione da integrare con  Adobe Analytics.

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, selezionate un centro dati e fornite le credenziali, incluso il nome dell&#39;organizzazione, il nome utente e il segreto condiviso.

   ![Configurare  Adobe Analytics per Assets Insights in  Experience Manager](assets/insights_config2.png)

   *Figura: Configura[!DNL Adobe Analytics]per informazioni approfondite sulle risorse in[!DNL Experience Manager].*

1. Fate clic su **[!UICONTROL Autenticazione]**.
1. Dopo aver [!DNL Experience Manager] autenticato le credenziali, dall’elenco Suite **[!UICONTROL di]** rapporti, scegliete una suite di [!DNL Adobe Analytics] rapporti da cui recuperare i dati mediante approfondimenti delle risorse. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo aver [!DNL Experience Manager] impostato la suite di rapporti, fate clic su **[!UICONTROL Fine]**.

## Tracciatore pagina {#page-tracker}

Dopo aver configurato l’ [!DNL Adobe Analytics] account, viene generato il codice Tracciatore pagina. Per abilitare Assets Insights per tenere traccia delle [!DNL Experience Manager] risorse utilizzate in siti Web di terze parti, includi il codice di tracciamento delle pagine nel codice del sito Web. Utilizzate l&#39;utility [!UICONTROL Page Tracker] in [!DNL Experience Manager Assets] per generare il codice di tracciamento pagina. Per ulteriori informazioni su come includere il codice Tracciatore pagina nelle pagine Web di terze parti, consultate [Utilizzare il tracciatore di pagina e il codice da incorporare nelle pagine](/help/assets/touch-ui-using-page-tracker.md)Web.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fate clic su **[!UICONTROL Scarica]** per scaricare il codice tracciatore pagina.
