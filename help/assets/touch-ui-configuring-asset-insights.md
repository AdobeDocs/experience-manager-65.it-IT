---
title: Configurare approfondimenti risorse
description: Configurare approfondimenti risorse in AEM Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Configurare approfondimenti risorse {#configure-asset-insights}

Risorse Adobe Experience Manager (AEM) recupera i dati di utilizzo relativi alle risorse AEM utilizzate da siti Web di terze parti da Adobe Analytics. Per abilitare Asset Insights per recuperare questi dati e generare approfondimenti, configura prima la funzione da integrare con Adobe Analytics.

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

1. In AEM, fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, selezionate un centro dati e fornite le credenziali, incluso il nome dell&#39;organizzazione, il nome utente e il segreto condiviso.

   ![Configurare Adobe Analytics per Assets Insights in AEM](assets/insights_config2.png)

   *Figura:Configurare Adobe Analytics per Assets Insights in AEM*

1. Tocca o fai clic su **[!UICONTROL Autentica]**.
1. Dopo l’autenticazione delle credenziali da parte di AEM, dall’elenco Suite **[!UICONTROL di]** rapporti, scegliete una suite di rapporti di Adobe Analytics da cui recuperare i dati da Asset Insights. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo aver impostato la suite di rapporti in AEM, tocca o fai clic su **[!UICONTROL Fine]**.

## Tracciatore pagina {#page-tracker}

Dopo aver configurato l’account Adobe Analytics, viene generato il codice Page Tracker. Per abilitare Assets Insights per tenere traccia delle risorse AEM utilizzate in siti Web di terze parti, includi il codice di tracciamento delle pagine nel codice del sito Web. Utilizzate l&#39;utilità Tracker pagina in Risorse AEM per generare il codice tracciatore pagina. Per ulteriori informazioni su come includere il codice Tracciatore pagina nelle pagine Web di terze parti, consultate [Utilizzare il tracciatore di pagina e il codice da incorporare nelle pagine](/help/assets/touch-ui-using-page-tracker.md)Web.

1. In AEM, fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fate clic su **[!UICONTROL Scarica]** per scaricare il codice tracciatore pagina.
