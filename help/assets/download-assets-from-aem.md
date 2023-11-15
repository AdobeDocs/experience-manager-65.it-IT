---
title: Scaricare le risorse
description: Scopri come scaricare le risorse da [!DNL Adobe Experience Manager] e abilitare o disabilitare la funzionalità di download.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
hide: true
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 4%

---

# Scaricare risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | Questo articolo |

Puoi scaricare risorse, incluse le rappresentazioni statiche e dinamiche. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate sono incluse in un file ZIP. Il file ZIP compresso ha una dimensione massima di 1 GB per il processo di esportazione. È consentito un massimo di 500 risorse totali per processo di esportazione.

>[!NOTE]
>
>Qualsiasi utente con autorizzazioni di lettura in `/var/dam/share` la posizione può accedere al collegamento di download condiviso nel messaggio e-mail.
>
>Qualsiasi utente con autorizzazioni di lettura per `/var/dam/jobs/download` la posizione può scaricare le risorse.
>
>Non è possibile scaricare i tipi di risorse: Set di immagini, Set 360 gradi, Set di file multimediali diversi e Set carosello.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Per scaricare le risorse, effettua le seguenti operazioni:**

1. Nell&#39;angolo superiore sinistro fare clic sul logo. Nella barra a sinistra, fai clic su **[!UICONTROL Navigazione]**.
1. Il giorno [!UICONTROL Navigazione] pagina, fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa a una cartella contenente le risorse da scaricare.
1. Seleziona la cartella o una o più risorse all’interno della cartella.
1. Sulla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.
1. Nella finestra di dialogo Scarica selezionare le opzioni di download desiderate.

   | Opzione di esportazione o download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Seleziona questa opzione per includere in una cartella sul computer locale tutte le risorse scaricate, comprese quelle in cartelle secondarie nidificate nella cartella principale della risorsa. Se questa opzione non è selezionata, per impostazione predefinita la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella nel computer locale. |
   | **[!UICONTROL E-mail]** | Viene inviata una notifica e-mail all’utente. I modelli di e-mail standard sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle posizioni seguenti: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puoi memorizzare modelli personalizzati specifici del tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Seleziona questa opzione per scaricare la risorsa nella sua forma originale senza rappresentazioni.<br>L’opzione Risorse secondarie è disponibile se la risorsa originale dispone di risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Una rappresentazione è la rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione primaria, quella del file caricato. Possono avere un numero qualsiasi di rappresentazioni. <br> Con questa opzione, puoi selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. L’opzione è disponibile se la risorsa ha delle rappresentazioni. |
   | **[!UICONTROL Ritagli avanzati]** | Seleziona questa opzione per scaricare tutte le rappresentazioni con ritaglio avanzato della risorsa selezionata dall’interno di AEM. Nel computer locale viene creato e scaricato un file zip con le rappresentazioni di Ritaglio avanzato. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Selezionare questa opzione per generare in tempo reale una serie di rappresentazioni alternative. Quando si seleziona questa opzione, si selezionano anche le copie trasformate che si desidera creare in modo dinamico selezionandole dalla [Predefinito immagine](image-presets.md) elenco. <br>Inoltre, è possibile selezionare le dimensioni e l&#39;unità di misura, il formato, lo spazio colore, la risoluzione ed eventuali modificatori di immagine opzionali, ad esempio l&#39;inversione dell&#39;immagine. L’opzione è disponibile solo se [!DNL Dynamic Media] abilitato. |

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]**.

Quando selezioni una cartella da scaricare, viene scaricata l’intera gerarchia di risorse sotto la cartella. Per includere in una singola cartella tutte le risorse scaricate (comprese le risorse nelle cartelle secondarie nidificate nella cartella principale), seleziona **[!UICONTROL Crea una cartella separata per ogni risorsa]**.

## Abilita servlet di download risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di inviare richieste di download simultanee di dimensioni arbitrarie per la creazione di file ZIP di risorse visibili che possono sovraccaricare il server e la rete. Per attenuare i potenziali rischi DoS causati da questa funzione, `AssetDownloadServlet` Per impostazione predefinita, il componente OSGi è disabilitato per le istanze di pubblicazione.

Per consentire il download di risorse dal DAM, ad esempio quando utilizzi qualcosa come Asset Share Commons o un’altra implementazione simile a un portale, abilita manualmente il servlet tramite una configurazione OSGi. L’Adobe consiglia di impostare la dimensione di download consentita il più bassa possibile senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Creare una cartella con una convenzione di denominazione che esegue il targeting della modalità di esecuzione di pubblicazione (`config.publish`): `/apps/<your-app-name>/config.publish`. Per definire le proprietà di configurazione per una modalità di esecuzione, vedi [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Nella cartella di configurazione, crea un file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Popolare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con quanto segue. Imposta una dimensione massima (in byte) per il download come valore `asset.download.prezip.maxcontentsize`. L’esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 kb.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

Per impostazione predefinita, per `GET` richieste di download di file, [!DNL Experience Manager] applica un limite di 50 MB alla dimensione di download dell’archivio ZIP. Download avviati tramite `POST` Le richieste o l’interfaccia utente non sono interessate da questo limite.

## Disabilita servlet di download risorse {#disable-asset-download-servlet}

Il `Asset Download Servlet` può essere disabilitato su un [!DNL Experience Manager] Pubblica le istanze aggiornando la configurazione del dispatcher per bloccare eventuali richieste di download di risorse. Il servlet può anche essere disabilitato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download di risorse tramite una configurazione di Dispatcher, modifica `dispatcher.any` e aggiungere una regola al [sezione filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Per disabilitare il componente OSGi in un’istanza Publish, accedi alla console OSGi all’indirizzo `http://[aem_server]:[port]/system/console/components`. Individua `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e fai clic su **[!UICONTROL Disattiva]**.

>[!MORELIKETHIS]
>
>* [Scaricare le risorse tramite Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Scaricare risorse protette DRM](drm.md).
>* [Scaricare risorse utilizzando l’app desktop Experience Manager su desktop Win o Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Scaricare risorse tramite Adobe Assets Link dalle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html).
