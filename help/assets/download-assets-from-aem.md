---
title: Scarica risorse digitali da [!DNL Adobe Experience Manager].
description: Scoprite come scaricare risorse da [!DNL Adobe Experience Manager] e abilitare o disabilitare la funzionalità di download.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d292059a865d150f7de5664eca164c542f965fcb

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Potete scaricare le risorse incluse le rappresentazioni statiche e dinamiche. In alternativa, potete inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate vengono raggruppate in un file ZIP. Il file ZIP compresso ha una dimensione massima di 1 GB per il processo di esportazione. È consentito un massimo di 500 risorse totali per processo di esportazione.

>[!NOTE]
>
>I destinatari delle e-mail devono essere membri del `dam-users` gruppo per accedere al collegamento di download ZIP nel messaggio e-mail. Per poter scaricare le risorse, i membri devono disporre delle autorizzazioni necessarie per avviare flussi di lavoro che attivano il download delle risorse.

Per scaricare le risorse, individuate una risorsa, selezionatela e toccate **[!UICONTROL Scarica]** dalla barra degli strumenti. Nella finestra di dialogo risultante, specificate le opzioni di download.

Impossibile scaricare i tipi di risorse Set immagini, Set 360 gradi, Set file multimediali diversi e Set caroselli.

![Opzioni disponibili durante il download delle risorse da Experience Manager Assets](assets/asset_download_dialog.png)

*Figura: Opzioni disponibili durante il download delle risorse da[!DNL Experience Manager Assets].*

Di seguito sono riportate le opzioni di esportazione o di download disponibili. Le rappresentazioni dinamiche sono esclusive dell&#39; [!DNL Dynamic Media] offerta. Questa opzione consente di generare nuove rappresentazioni in tempo reale, oltre alla risorsa selezionata. L’opzione è disponibile solo se è stata [!DNL Dynamic Media] attivata.

| Opzioni di esportazione o download | Descrizioni |
|---|---|
| [!UICONTROL Assets] | Selezionate l’opzione per scaricare la risorsa nel modulo originale senza alcuna rappresentazione. |
| [!UICONTROL Rappresentazioni] | Rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere un numero qualsiasi di rappresentazioni. <br> Con questa opzione, potete selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. |
| [!UICONTROL Rendering dinamici] | Una rappresentazione dinamica genera altre rappresentazioni in tempo reale. Quando selezionate questa opzione, potete anche selezionare le rappresentazioni da creare in modo dinamico selezionandole dall’elenco Predefinito [](image-presets.md) immagine. <br>Potete inoltre selezionare le dimensioni e l’unità di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine (ad esempio per invertire l’immagine) |
| [!UICONTROL E-mail] | All’utente viene inviata una notifica e-mail. I modelli standard per le e-mail sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione devono essere presenti nelle seguenti posizioni: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Potete memorizzare i modelli personalizzati specifici per il tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
| [!UICONTROL Crea una cartella separata per ogni risorsa] | Selezionate l’opzione per mantenere la gerarchia delle cartelle durante il download delle risorse. Per impostazione predefinita, la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella del file system locale. |

L&#39;opzione delle rappresentazioni è disponibile se la risorsa dispone di rappresentazioni. L’opzione Risorse secondarie è disponibile se la risorsa originale contiene risorse secondarie.

Quando selezionate una cartella da scaricare, viene scaricata l’intera gerarchia di risorse sotto la cartella. Per includere ciascuna risorsa scaricata (incluse le risorse nelle cartelle figlie nidificate sotto la cartella principale) in una singola cartella, selezionate **[!UICONTROL Crea cartella separata per ciascuna risorsa]**.

## Abilita servlet download risorse {#enable-asset-download-servlet}

Il servlet predefinito [!DNL Experience Manager] consente agli utenti autenticati di emettere richieste di download simultanee di grandi dimensioni per la creazione di file ZIP di risorse visibili agli utenti che possono sovraccaricare il server e la rete. Per attenuare i potenziali rischi DoS causati da questa funzione, il componente `AssetDownloadServlet` OSGi è disabilitato per impostazione predefinita per le istanze di pubblicazione.

Per consentire il download delle risorse da DAM, ad esempio quando si utilizza un sistema simile a Asset Share Commons o ad altre implementazioni di tipo portale, è necessario abilitare manualmente il servlet tramite una configurazione OSGi. Adobe consiglia di impostare la dimensione di download consentita il più bassa possibile senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Create una cartella con una convenzione di denominazione per la modalità di esecuzione della pubblicazione (`config.publish`): `/apps/<your-app-name>/config.publish`. Per definire le proprietà di configurazione per una modalità di esecuzione, vedere Modalità di [esecuzione](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).

1. Nella cartella di configurazione, create un file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Compilate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con le seguenti opzioni. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disattivazione del servlet di download delle risorse {#disable-asset-download-servlet}

È `Asset Download Servlet` possibile disattivare le istanze di [!DNL Experience Manager] pubblicazione aggiornando la configurazione del dispatcher per bloccare qualsiasi richiesta di download di risorse. Il servlet può anche essere disattivato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione dispatcher, modifica la `dispatcher.any` configurazione e aggiungi una regola alla sezione [](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)filtro.

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Disattivate il componente OSGi in un’istanza di pubblicazione accedendo alla console OSGi all’indirizzo `http://[aem_server]:[port]/system/console/components`. Individuate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e fate clic su **[!UICONTROL Disattiva]**.

>[!MORELIKETHIS]
>
>* [Scaricate le risorse](drm.md)protette da DRM.
>* [Scaricate le risorse tramite l’app desktop Experience Manager su Windows o Mac desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html).
>* [Scaricate le risorse tramite Adobe Assets Link dall&#39;interno delle app](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)Adobe Creative Cloud supportate.

