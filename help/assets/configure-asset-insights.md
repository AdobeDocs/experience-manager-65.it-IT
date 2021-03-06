---
title: Configura Asset Insights per ottenere l’analisi.
description: Configurare Assets Insights in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Informazioni sulla risorsa, rapporti sulle risorse
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---

# Configurare Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti web di terze parti da  [!DNL Adobe Analytics]. Per abilitare Assets Insights al recupero di questi dati e alla generazione di informazioni, configura prima la funzionalità da integrare con [!DNL Adobe Analytics]. Per utilizzare questa funzione in un’installazione on-premise, acquista la licenza [!DNL Adobe Analytics] separatamente. I clienti su [!DNL Managed Services] ricevono la licenza [!DNL Analytics] inclusa in [!DNL Experience Manager]. Consulta [Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

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
1. Dopo che [!DNL Experience Manager] autentica le credenziali, dall’elenco **[!UICONTROL Suite di rapporti]** scegli una suite di rapporti [!DNL Adobe Analytics] dalla quale desideri che Assets Insights recuperi dati. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo che [!DNL Experience Manager] imposta la suite di rapporti, fai clic su **[!UICONTROL Fine]**.

## Tracciamento pagina {#page-tracker}

Dopo aver configurato l’account [!DNL Adobe Analytics], viene generato il codice di tracciamento pagina. Per abilitare Asset Insights a tenere traccia delle risorse [!DNL Experience Manager] utilizzate in siti web di terze parti, includi il codice di tracciamento della pagina nel codice del sito web. Utilizza l&#39;utility [!UICONTROL Page Tracker] in [!DNL Experience Manager Assets] per generare il codice di tracciamento della pagina. Per ulteriori informazioni su come includere il codice di tracciamento pagina nelle pagine web di terze parti, consulta [Utilizzare il tracciamento pagina e il codice di incorporamento nelle pagine web](/help/assets/use-page-tracker.md).

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fai clic su **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.
