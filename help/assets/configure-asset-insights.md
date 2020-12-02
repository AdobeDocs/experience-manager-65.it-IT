---
title: Configurare Asset Insights per ottenere l'analisi.
description: Configura approfondimenti risorse in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 8%

---


# Configurare approfondimenti risorse {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti Web di terze parti da  [!DNL Adobe Analytics]. Per abilitare Asset Insights per recuperare questi dati e generare approfondimenti, configura innanzitutto la funzione da integrare con  Adobe Analytics.

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, selezionate un centro dati e fornite le credenziali, incluso il nome dell&#39;organizzazione, il nome utente e il segreto condiviso.

   ![Configurare  Adobe Analytics per Assets Insights in  Experience Manager](assets/insights_config2.png)

   *Figura: Configura  [!DNL Adobe Analytics] per informazioni approfondite sulle risorse in  [!DNL Experience Manager].*

1. Fare clic su **[!UICONTROL Autenticazione]**.
1. Dopo che [!DNL Experience Manager] esegue l&#39;autenticazione delle credenziali, dall&#39;elenco **[!UICONTROL Suite di rapporti]**, scegliete una suite di rapporti [!DNL Adobe Analytics] da cui recuperare i dati mediante Asset Insights. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo che [!DNL Experience Manager] ha impostato la suite di rapporti, fare clic su **[!UICONTROL Fine]**.

## Tracciatore pagina {#page-tracker}

Dopo aver configurato l&#39;account [!DNL Adobe Analytics], viene generato il codice Page Tracker. Per abilitare Assets Insights a tenere traccia delle risorse [!DNL Experience Manager] utilizzate in siti Web di terze parti, includi il codice di tracciamento delle pagine nel codice del sito Web. Utilizzare l&#39;utility [!UICONTROL Page Tracker] in [!DNL Experience Manager Assets] per generare il codice di tracciamento pagina. Per ulteriori informazioni su come includere il codice Page Tracker nelle pagine Web di terze parti, vedere [Utilizzare il tracciatore di pagina e il codice da incorporare nelle pagine Web](/help/assets/use-page-tracker.md).

1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fate clic su **[!UICONTROL Scarica]** per scaricare il codice tracciatore pagina.
