---
title: Scaricare le risorse
description: Scoprite come scaricare le risorse da  [!DNL Adobe Experience Manager] e attivare o disattivare la funzionalità di download.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 3%

---


# Scaricare risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Potete scaricare le risorse incluse le rappresentazioni statiche e dinamiche. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate vengono raggruppate in un file ZIP. Il file ZIP compresso ha una dimensione massima di 1 GB per il processo di esportazione. È consentito un massimo di 500 risorse totali per processo di esportazione.

>[!NOTE]
>
>I destinatari delle e-mail devono essere membri del gruppo `dam-users` per accedere al collegamento di download ZIP nel messaggio e-mail. Per poter scaricare le risorse, i membri devono disporre delle autorizzazioni necessarie per avviare flussi di lavoro che attivano il download delle risorse.

Impossibile scaricare i tipi di risorse Set immagini, Set 360 gradi, Set file multimediali diversi e Set caroselli.

Per scaricare le risorse, effettuate le seguenti operazioni:

1. Nell’angolo in alto a sinistra, fate clic sul logo. Nella barra a sinistra, fare clic su **[!UICONTROL Navigazione]**.
1. Nella pagina [!UICONTROL Navigazione] fare clic su **[!UICONTROL Risorse]** > **[!UICONTROL File.]**
1. Individuate una cartella contenente le risorse da scaricare.
1. Selezionate la cartella o selezionate una o più risorse all’interno della cartella.
1. Sulla barra degli strumenti, fare clic su **[!UICONTROL Scarica.]**

   ![Opzioni disponibili durante il download delle risorse da  risorse Experience Manager](/help/assets/assets/asset-download1.png)

   *Figura: Opzioni disponibili nella finestra di dialogo di download.*

1. Nella finestra di dialogo Download, selezionate le opzioni di download desiderate.

   | Opzione di esportazione o download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Selezionate questa opzione per includere in un’unica cartella del computer locale tutte le risorse che avete scaricato, comprese quelle presenti in cartelle figlie nidificate sotto la cartella padre della risorsa. Se questa opzione non è selezionata, per impostazione predefinita la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella del computer locale. |
   | **[!UICONTROL E-mail]** | All’utente viene inviata una notifica e-mail. I modelli standard per le e-mail sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle seguenti posizioni: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Potete memorizzare i modelli personalizzati specifici per il tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Selezionate questa opzione per scaricare la risorsa nel modulo originale senza alcuna rappresentazione.<br>L’opzione Risorse secondarie è disponibile se la risorsa originale contiene risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere un numero qualsiasi di rappresentazioni. <br> Con questa opzione, potete selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. L’opzione è disponibile se la risorsa dispone di rappresentazioni. |
   | **[!UICONTROL Ritagli avanzati]** | Selezionate questa opzione per scaricare tutte le rappresentazioni di ritaglio avanzato della risorsa selezionata dall’interno AEM. Viene creato e scaricato nel computer locale un file zip con le rappresentazioni SmartCrop. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Selezionate questa opzione per generare una serie di rappresentazioni alternative in tempo reale. Quando selezionate questa opzione, potete anche selezionare le rappresentazioni che desiderate creare in modo dinamico selezionando dall&#39;elenco [Image Preset](image-presets.md). <br>Potete inoltre selezionare le dimensioni e l’unità di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine opzionale, ad esempio l’inversione dell’immagine. L&#39;opzione è disponibile solo se [!DNL Dynamic Media] è stata attivata. |

1. Nella finestra di dialogo, fare clic su **[!UICONTROL Scarica.]**.

Quando selezionate una cartella da scaricare, viene scaricata l’intera gerarchia di risorse sotto la cartella. Per includere ciascuna risorsa scaricata (comprese le risorse nelle cartelle figlie nidificate sotto la cartella principale) in una singola cartella, selezionate **[!UICONTROL Crea una cartella separata per ciascuna risorsa]**.

## Abilita servlet download risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di emettere richieste di download simultanei di grandi dimensioni per la creazione di file ZIP di risorse visibili agli utenti che possono sovraccaricare il server e la rete. Per attenuare i potenziali rischi DoS causati da questa funzione, il componente `AssetDownloadServlet` OSGi è disabilitato per impostazione predefinita per le istanze di pubblicazione.

Per consentire il download delle risorse da DAM, ad esempio quando si utilizza un sistema simile a Asset Share Commons o ad altre implementazioni di tipo portale, è necessario abilitare manualmente il servlet tramite una configurazione OSGi.  Adobe consiglia di impostare la dimensione di download consentita il più bassa possibile senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Create una cartella con una convenzione di denominazione per la modalità di esecuzione della pubblicazione (`config.publish`): `/apps/<your-app-name>/config.publish`. Per definire le proprietà di configurazione per una modalità di esecuzione, vedere [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Nella cartella di configurazione, create un file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Compilare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con i seguenti elementi. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disattivazione del servlet di download delle risorse {#disable-asset-download-servlet}

È possibile disabilitare `Asset Download Servlet` su [!DNL Experience Manager] istanze di pubblicazione aggiornando la configurazione del dispatcher per bloccare qualsiasi richiesta di download di risorse. Il servlet può anche essere disattivato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione dispatcher, modificare la configurazione `dispatcher.any` e aggiungere una regola alla sezione [filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Per disabilitare il componente OSGi in un’istanza Pubblica, accedete alla console OSGi all’indirizzo `http://[aem_server]:[port]/system/console/components`. Individuare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e fare clic su **[!UICONTROL Disattiva]**.

>[!MORELIKETHIS]
>
>* [Scaricare le risorse tramite Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Scaricate le risorse](drm.md) protette da DRM.
>* [Scaricate le risorse tramite &#39;app desktop Experience Manager su Windows o Mac desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Scaricate le risorse tramite  collegamento Risorse Adobe dalle app](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) Adobe Creative Cloud supportate.

