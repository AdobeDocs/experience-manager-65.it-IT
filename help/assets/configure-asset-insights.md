---
title: Configura Asset Insights per ottenere l’analisi.
description: Configura Asset Insights in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Administrator
feature: Asset Insights,Asset Reports
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 8%

---


# Configurare Asset Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti web di terze parti da  [!DNL Adobe Analytics]. Per abilitare Asset Insights al recupero di questi dati e alla generazione di informazioni, configura prima la funzione di integrazione con Adobe Analytics.

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, seleziona un centro dati e fornisci le tue credenziali, tra cui il nome dell’organizzazione, il nome utente e il segreto condiviso.

   ![Configurare Adobe Analytics per Assets Insights in Experience Manager](assets/insights_config2.png)

   *Figura: Configurare  [!DNL Adobe Analytics] per Assets Insights in  [!DNL Experience Manager].*

1. Fare clic su **[!UICONTROL Autentica]**.
1. Dopo che [!DNL Experience Manager] autentica le credenziali, dall’elenco **[!UICONTROL Suite di rapporti]** scegli una suite di rapporti [!DNL Adobe Analytics] dalla quale desideri che Asset Insights recuperi i dati. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo che [!DNL Experience Manager] imposta la suite di rapporti, fai clic su **[!UICONTROL Fine]**.

## Tracciamento pagina {#page-tracker}

Dopo aver configurato l’account [!DNL Adobe Analytics], viene generato il codice di tracciamento pagina. Per abilitare Asset Insights a tenere traccia delle risorse [!DNL Experience Manager] utilizzate in siti web di terze parti, includi il codice di tracciamento della pagina nel codice del sito web. Utilizza l&#39;utility [!UICONTROL Page Tracker] in [!DNL Experience Manager Assets] per generare il codice di tracciamento della pagina. Per ulteriori informazioni su come includere il codice di tracciamento pagina nelle pagine web di terze parti, consulta [Utilizzare il tracciamento pagina e il codice di incorporamento nelle pagine web](/help/assets/use-page-tracker.md).

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fai clic su **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.
