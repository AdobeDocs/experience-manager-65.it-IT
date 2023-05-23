---
title: Configura Assets Insights per ottenere Analytics.
description: Configurare Assets Insights in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# Configurare Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti web di terze parti da [!DNL Adobe Analytics]. Per abilitare Assets Insights al recupero di tali dati e alla generazione di informazioni, configura innanzitutto la funzione da integrare con [!DNL Adobe Analytics]. Per utilizzare questa funzione in un’installazione on-premise, acquista [!DNL Adobe Analytics] licenza separatamente. Clienti il [!DNL Managed Services] ricevere [!DNL Analytics] licenza fornita con [!DNL Experience Manager]. Consulta [Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

1. In entrata [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, seleziona un centro dati e fornisci le tue credenziali, tra cui il nome dell’organizzazione, il nome utente e il segreto condiviso.

   ![Configurare Adobe Analytics per Informazioni su risorse in Experience Manager](assets/insights_config2.png)

   *Figura: Configurare [!DNL Adobe Analytics] per approfondimenti risorse in [!DNL Experience Manager].*

1. Clic **[!UICONTROL Autentica]**.
1. Dopo [!DNL Experience Manager] autentica le credenziali, dal **[!UICONTROL Suite di rapporti]** elenco, scegli un [!DNL Adobe Analytics] suite di rapporti da dove desideri che Assets Insights recuperi i dati. Clic **[!UICONTROL Aggiungi]**.
1. Dopo [!DNL Experience Manager] configura la suite di rapporti, fai clic su **[!UICONTROL Fine]**.

## Tracciamento pagina {#page-tracker}

Dopo aver configurato [!DNL Adobe Analytics] Account, il codice di tracciamento pagina viene generato automaticamente. Per abilitare Assets Insights al tracciamento [!DNL Experience Manager] le risorse utilizzate nei siti web di terze parti includono il codice di tracciamento della pagina nel codice del sito web. Utilizza il [!UICONTROL Tracciamento pagina] utilità in [!DNL Experience Manager Assets] per generare il codice di tracciamento della pagina. Per ulteriori informazioni su come includere il codice di tracciamento pagina in pagine web di terze parti, consulta [Utilizzare il tracciamento delle pagine e il codice di incorporamento nelle pagine web](/help/assets/use-page-tracker.md).

1. In entrata [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Clic **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.
