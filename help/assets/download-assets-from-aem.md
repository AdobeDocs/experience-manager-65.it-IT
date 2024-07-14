---
title: Scaricare le risorse
description: Scopri come scaricare risorse da [!DNL Adobe Experience Manager]  e abilitare o disabilitare la funzionalità di download.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 2%

---

# Scarica risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | Questo articolo |

Puoi scaricare risorse, incluse le rappresentazioni statiche e dinamiche. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate sono incluse in un file ZIP. Il file ZIP compresso ha una dimensione massima di 1 GB per il processo di esportazione. È consentito un massimo di 500 risorse totali per processo di esportazione.

>[!NOTE]
>
>Qualsiasi utente con autorizzazioni di lettura nel percorso `/var/dam/share` può accedere al collegamento di download condiviso nel messaggio e-mail.
>
>Qualsiasi utente con autorizzazioni di lettura per il percorso `/var/dam/jobs/download` può scaricare le risorse.
>
>Non è possibile scaricare i tipi di risorse: Set di immagini, Set 360 gradi, Set di file multimediali diversi e Set carosello.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Per scaricare le risorse, eseguire la procedura seguente:**

1. Nell&#39;angolo superiore sinistro fare clic sul logo. Nella barra a sinistra, fai clic su **[!UICONTROL Navigazione]**.
1. Nella pagina [!UICONTROL Navigazione], fare clic su **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Passa a una cartella contenente le risorse da scaricare.
1. Seleziona la cartella o una o più risorse all’interno della cartella.
1. Sulla barra degli strumenti fare clic su **[!UICONTROL Scarica]**.
1. Nella finestra di dialogo Scarica selezionare le opzioni di download desiderate.

   | Opzione di esportazione o download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Seleziona questa opzione per includere in una cartella sul computer locale tutte le risorse scaricate, comprese quelle in cartelle secondarie nidificate nella cartella principale della risorsa. Se questa opzione non è selezionata, per impostazione predefinita la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella nel computer locale. |
   | **[!UICONTROL E-mail]** | Viene inviata una notifica e-mail all’utente. I modelli di e-mail standard sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle posizioni seguenti: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puoi memorizzare modelli personalizzati specifici del tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorse]** | Seleziona questa opzione per scaricare la risorsa nella sua forma originale senza rappresentazioni.<br>L&#39;opzione Risorse secondarie è disponibile se la risorsa originale contiene risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Una rappresentazione è la rappresentazione binaria di una risorsa. Assets dispone di una rappresentazione principale, ovvero quella del file caricato. Possono avere un numero qualsiasi di rappresentazioni. <br> Con questa opzione è possibile selezionare le copie trasformate da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. L’opzione è disponibile se la risorsa ha delle rappresentazioni. |
   | **[!UICONTROL Ritagli avanzati]** | Seleziona questa opzione per scaricare tutte le rappresentazioni con ritaglio avanzato della risorsa selezionata dall’interno di AEM. Nel computer locale viene creato e scaricato un file zip con le rappresentazioni di Ritaglio avanzato. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Selezionare questa opzione per generare in tempo reale una serie di rappresentazioni alternative. Quando selezioni questa opzione, selezioni anche le rappresentazioni da creare in modo dinamico selezionandole dall&#39;elenco [Predefinito immagine](image-presets.md). <br>È inoltre possibile selezionare le dimensioni e l&#39;unità di misura, il formato, lo spazio colore, la risoluzione ed eventuali modificatori di immagine facoltativi, ad esempio l&#39;inversione dell&#39;immagine. L&#39;opzione è disponibile solo se è stato abilitato [!DNL Dynamic Media]. |

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]**.

Quando selezioni una cartella da scaricare, viene scaricata l’intera gerarchia di risorse sotto la cartella. Per includere ogni risorsa scaricata (comprese le risorse nelle cartelle secondarie nidificate nella cartella principale) in una singola cartella, seleziona **[!UICONTROL Crea una cartella separata per ogni risorsa]**.

## Abilita servlet di download risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di inviare richieste di download simultanee di dimensioni arbitrarie per creare file ZIP di risorse visibili che possono sovraccaricare il server e la rete. Per attenuare i potenziali rischi DoS causati da questa funzione, il componente OSGi `AssetDownloadServlet` è disabilitato per impostazione predefinita per le istanze di pubblicazione.

Per consentire il download di risorse dal DAM, ad esempio quando utilizzi qualcosa come Asset Share Commons o un’altra implementazione simile a un portale, abilita manualmente il servlet tramite una configurazione OSGi. L’Adobe consiglia di impostare la dimensione di download consentita il più bassa possibile senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Creare una cartella con una convenzione di denominazione che esegue il targeting della modalità di esecuzione di pubblicazione (`config.publish`): `/apps/<your-app-name>/config.publish`. Per definire le proprietà di configurazione per una modalità di esecuzione, vedere [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Nella cartella di configurazione creare un file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Popolare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con quanto segue. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L’esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 kb.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

Per impostazione predefinita, per `GET` richieste di download di file, [!DNL Experience Manager] applica un limite di 50 MB alle dimensioni di download dell&#39;archivio ZIP. I download avviati tramite `POST` richieste o l&#39;interfaccia utente non sono interessati da questo limite.

## Disabilita servlet di download risorse {#disable-asset-download-servlet}

È possibile disabilitare `Asset Download Servlet` in un&#39;istanza Publish [!DNL Experience Manager] aggiornando la configurazione del dispatcher per bloccare eventuali richieste di download di risorse. Il servlet può anche essere disabilitato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download di risorse tramite una configurazione di Dispatcher, modifica la configurazione `dispatcher.any` e aggiungi una regola alla [sezione filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Per disabilitare il componente OSGi in un&#39;istanza di Publish, accedi alla console OSGi all&#39;indirizzo `http://[aem_server]:[port]/system/console/components`. Individuare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e fare clic su **[!UICONTROL Disattiva]**.

>[!MORELIKETHIS]
>
>* [Scarica risorse tramite Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Scarica risorse protette DRM](drm.md).
>* [Scarica le risorse tramite l&#39;app desktop Experience Manager sul desktop Win o Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Scarica le risorse tramite Adobe Assets Link dalle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html).
