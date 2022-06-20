---
title: Scaricare le risorse
description: Scopri come scaricare risorse da [!DNL Adobe Experience Manager] e abilitare o disabilitare la funzionalità di download.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 5%

---

# Scaricare le risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | Questo articolo |
| AEM 6.4 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/download-assets-from-aem.html?lang=en) |

Puoi scaricare le risorse, compresi i rendering statici e dinamici. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate sono raggruppate in un file ZIP. Il file ZIP compresso ha una dimensione massima del file di 1 GB per il processo di esportazione. È consentito un massimo di 500 risorse totali per processo di esportazione.

>[!NOTE]
>
>Qualsiasi utente con autorizzazioni di lettura in `/var/dam/share` la posizione può accedere al collegamento di download condiviso nel messaggio e-mail.
>
>Qualsiasi utente con autorizzazioni di lettura per `/var/dam/jobs/download` la posizione può scaricare le risorse.
>
>Non è possibile scaricare i tipi di risorse Set immagini, Set 360 gradi, Set di file multimediali diversi e Set carosello.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Per scaricare le risorse, effettua le seguenti operazioni:**

1. Nell’angolo in alto a sinistra, fai clic sul logo. Nella barra a sinistra, fai clic su **[!UICONTROL Navigazione]**.
1. Sulla [!UICONTROL Navigazione] pagina, fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa a una cartella contenente le risorse da scaricare.
1. Seleziona la cartella o seleziona una o più risorse all’interno della cartella.
1. Sulla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.
1. Nella finestra di dialogo Scarica selezionare le opzioni di download desiderate.

   | Opzione di esportazione o download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Seleziona questa opzione per includere ogni risorsa scaricata, incluse le risorse in cartelle secondarie nidificate sotto la cartella padre della risorsa, in un’unica cartella sul computer locale. Quando questa opzione non è selezionata, per impostazione predefinita la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in un&#39;unica cartella nel computer locale. |
   | **[!UICONTROL E-mail]** | Viene inviata all’utente una notifica e-mail. I modelli e-mail standard sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle seguenti posizioni: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>È possibile archiviare modelli personalizzati specifici per il tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Seleziona questa opzione per scaricare la risorsa nel modulo originale senza rendering.<br>L’opzione Risorse secondarie è disponibile se la risorsa originale include risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere diverse rappresentazioni. <br> Con questa opzione, puoi selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. L’opzione è disponibile se la risorsa dispone di rendering. |
   | **[!UICONTROL Ritagli avanzati]** | Seleziona questa opzione per scaricare dal AEM tutte le rappresentazioni di ritaglio avanzato della risorsa selezionata. Viene creato e scaricato nel computer locale un file zip con le rappresentazioni di ritaglio avanzato. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Seleziona questa opzione per generare una serie di rappresentazioni alternative in tempo reale. Quando selezioni questa opzione, selezioni anche le rappresentazioni che desideri creare in modo dinamico selezionando dalla [Predefinito immagine](image-presets.md) elenco. <br>È inoltre possibile selezionare le dimensioni e l&#39;unità di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine opzionale, ad esempio l&#39;inversione dell&#39;immagine. L’opzione è disponibile solo se è disponibile [!DNL Dynamic Media] abilitato. |

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]**.

Quando selezioni una cartella da scaricare, viene scaricata l’intera gerarchia delle risorse sotto la cartella. Per includere ogni risorsa scaricata (incluse le risorse nelle cartelle secondarie nidificate sotto la cartella principale) in una singola cartella, seleziona **[!UICONTROL Crea una cartella separata per ogni risorsa]**.

## Abilita il servlet di download delle risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di emettere richieste di download simultanee di grandi dimensioni per la creazione di file ZIP di risorse visibili che possono sovraccaricare il server e la rete. Per attenuare i potenziali rischi DoS causati da questa funzione, `AssetDownloadServlet` Il componente OSGi è disabilitato per impostazione predefinita per le istanze di pubblicazione.

Per consentire il download delle risorse dal tuo DAM, ad esempio quando utilizzi qualcosa come Asset Share Commons o un’altra implementazione simile a un portale, abilita manualmente il servlet tramite una configurazione OSGi. L’Adobe consiglia di impostare la dimensione del download consentito il più possibile bassa senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Crea una cartella con una convenzione di denominazione per la modalità di esecuzione di pubblicazione (`config.publish`): `/apps/<your-app-name>/config.publish`. Per definire le proprietà di configurazione per una modalità di esecuzione, vedi [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Nella cartella di configurazione, crea un file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Popolare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con le seguenti caratteristiche. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP in modo che non superi 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

Per impostazione predefinita, per `GET` richieste di download di file, [!DNL Experience Manager] applica un limite di 50 MB alla dimensione di download dell&#39;archivio ZIP. Download avviati tramite `POST` le richieste o l’interfaccia utente non sono influenzate da questo limite.

## Disattiva il servlet di download delle risorse {#disable-asset-download-servlet}

La `Asset Download Servlet` può essere disabilitato su un [!DNL Experience Manager] Pubblica le istanze aggiornando la configurazione del dispatcher per bloccare eventuali richieste di download delle risorse. Il servlet può anche essere disabilitato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione del dispatcher, modifica la `dispatcher.any` e aggiungi una regola al [sezione filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Per disabilitare il componente OSGi in un’istanza Publish, accedi alla console OSGi all’indirizzo `http://[aem_server]:[port]/system/console/components`. Individua `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e fai clic su **[!UICONTROL Disattiva]**.

>[!MORELIKETHIS]
>
>* [Scaricare risorse con Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Scaricare risorse protette DRM](drm.md).
>* [Scaricare risorse utilizzando l’app desktop Experience Manager su desktop Win o Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Scaricare le risorse utilizzando il collegamento Risorse di Adobe dalle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html).

