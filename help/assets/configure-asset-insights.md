---
title: Configura Assets Insights per ottenere Analytics.
description: Configura Assets Insights in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a4e1c1f5-18fc-592e-bfc7-453ce6ae0030
    internal-label: Asset Insights
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 7%
---
# Configurare Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti Web di terze parti da [!DNL Adobe Analytics]. Per consentire ad Assets Insights di recuperare questi dati e generare approfondimenti, configura innanzitutto la funzione da integrare con [!DNL Adobe Analytics]. Per utilizzare questa funzionalità in un&#39;installazione locale, acquistare separatamente la licenza [!DNL Adobe Analytics]. I clienti su [!DNL Managed Services] ricevono [!DNL Analytics] licenza in bundle con [!DNL Experience Manager]. Vedi [descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, seleziona un centro dati e fornisci le tue credenziali, tra cui il nome dell’organizzazione, il nome utente e il segreto condiviso.

   ![Configurazione di Adobe Analytics per approfondimenti su Assets in Experience Manager](assets/insights_config2.png)

   *Figura: configurare [!DNL Adobe Analytics] per Assets Insights in [!DNL Experience Manager].*

1. Fare clic su **[!UICONTROL Autentica]**.
1. Dopo che [!DNL Experience Manager] ha autenticato le credenziali, dall&#39;elenco **[!UICONTROL Suite di rapporti]**, scegli una suite di rapporti [!DNL Adobe Analytics] da cui desideri che Assets Insights recuperi i dati. Fai clic su **[!UICONTROL Aggiungi]**.
1. Dopo che [!DNL Experience Manager] ha configurato la tua suite di rapporti, fai clic su **[!UICONTROL Fine]**.

## Tracciamento pagina {#page-tracker}

Dopo aver configurato l&#39;account [!DNL Adobe Analytics], il codice di tracciamento pagina viene generato automaticamente. Per consentire ad Assets Insights di tenere traccia delle risorse [!DNL Experience Manager] utilizzate in siti Web di terze parti, includi il codice di tracciamento della pagina nel codice del sito Web. Utilizzare l&#39;utilità [!UICONTROL Page Tracker] in [!DNL Experience Manager Assets] per generare il codice di tracciamento della pagina. Per ulteriori informazioni su come includere il codice di tracciamento delle pagine in pagine Web di terze parti, vedere [Utilizzare il tracciamento delle pagine e incorporare il codice nelle pagine Web](/help/assets/use-page-tracker.md).

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fai clic su **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.
