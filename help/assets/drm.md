---
title: Digital Rights Management di attività
description: Scopri come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in [!DNL Experience Manager].
contentOwner: AG
role: User, Admin
feature: DRM,Gestione risorse
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 6%

---

# Digital Rights Management per le risorse {#digital-rights-management-in-assets}

Le risorse digitali sono spesso associate a una licenza che specifica i termini e la durata dell’utilizzo. Poiché [!DNL Adobe Experience Manager Assets] è completamente integrato con la piattaforma [!DNL Experience Manager], puoi gestire in modo efficiente le informazioni sulla scadenza delle risorse e gli stati delle risorse. È inoltre possibile associare le informazioni sulle licenze alle risorse.

## Scadenza risorse {#asset-expiration}

La scadenza delle risorse è un modo efficace per applicare i requisiti di licenza per le risorse. In questo modo la risorsa pubblicata viene annullata quando scade, evitando così la possibilità di eventuali violazioni della licenza. Un utente senza autorizzazioni di amministratore non può modificare, copiare, spostare, pubblicare e scaricare una risorsa scaduta.

Puoi visualizzare lo stato di scadenza di una risorsa nella console [!DNL Assets] sia nella vista a schede che in quella a elenco.

![expiration_flag_list](assets/expired_flag_list.png)

*Figura: Nella vista a elenco, nella colonna   Statusbanner viene visualizzato   Expiredbanner.*

Puoi visualizzare lo stato di scadenza di una risorsa nella barra a sinistra di [!UICONTROL Timeline].

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>La data di scadenza di una risorsa viene visualizzata in modo diverso per gli utenti con diversi valori orari.

Puoi anche visualizzare lo stato di scadenza delle risorse nella barra **[!UICONTROL Riferimenti]** . Gestisce gli stati di scadenza delle risorse e le relazioni tra le risorse composte e le risorse secondarie, le raccolte e i progetti a cui si fa riferimento.

1. Passa alla risorsa per la quale desideri visualizzare i riferimenti alle pagine web e alle risorse composte.
1. Seleziona la risorsa e apri **[!UICONTROL Riferimenti]** nella barra a sinistra. Per le risorse scadute, la barra [!UICONTROL Riferimenti] visualizza lo stato di scadenza **[!UICONTROL La risorsa è scaduta]** nella parte superiore.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Se la risorsa è scaduta, nella barra [!UICONTROL Riferimenti] viene visualizzato lo stato **[!UICONTROL Risorse secondarie scadute]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Cercare risorse scadute {#search-expired-assets}

Puoi cercare le risorse scadute, incluse le risorse secondarie scadute, nel pannello Ricerca.

1. Nella console [!DNL Assets], fai clic su **[!UICONTROL Cerca]** nella barra degli strumenti per visualizzare la casella di ricerca Omnisearch.

1. Con il cursore nella casella Omnisearch, selezionare il tasto `Enter` per visualizzare la pagina dei risultati della ricerca.
1. Apri il pannello di ricerca nella barra a sinistra. Fai clic sull&#39;opzione **[!UICONTROL Stato scadenza]** per espanderla.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Scegli **[!UICONTROL Scaduto]**. Dopo aver filtrato i risultati della ricerca vengono visualizzate solo le risorse scadute.

Quando scegli l’opzione **[!UICONTROL Expired]** , nella console [!DNL Assets] vengono visualizzate solo le risorse e le risorse secondarie scadute a cui fanno riferimento le risorse composte. Le risorse composte che fanno riferimento a risorse secondarie scadute non vengono visualizzate immediatamente dopo la scadenza delle risorse secondarie. Vengono invece visualizzati dopo che [!DNL Experience Manager] rileva che fanno riferimento a risorse secondarie scadute al successivo avvio della pianificazione.

Se modifichi la data di scadenza di una risorsa pubblicata a una data precedente al ciclo di pianificazione corrente, la pianificazione rileva comunque questa risorsa come una risorsa scaduta la prossima volta che viene eseguita e ne riflette lo stato di conseguenza.

Inoltre, se un errore o un errore impedisce al programmatore di rilevare le risorse scadute nel ciclo corrente, lo scheduler riesamina tali risorse nel ciclo successivo e ne rileva lo stato scaduto.

Per abilitare la console [!DNL Assets] affinché visualizzi le risorse composte di riferimento insieme alle risorse secondarie scadute, configura un flusso di lavoro **[!UICONTROL Adobe CQ DAM Expiry Notification]** in [!DNL Experience Manager] Configuration Manager.

1. Apri [!DNL Experience Manager] Configuration Manager.
1. Scegli **[!UICONTROL Notifica di scadenza Adobe CQ DAM]**. Per impostazione predefinita, è selezionata l&#39;opzione **[!UICONTROL Utilità di pianificazione basata sul tempo]**, che consente di pianificare un processo per verificare in un momento specifico se una risorsa è scaduta per le risorse secondarie. Al termine del processo, le risorse con risorse secondarie scadute e risorse di riferimento vengono visualizzate come scadute nei risultati della ricerca.

1. Per eseguire il processo periodicamente, cancella il campo **[!UICONTROL Time Based Scheduler Rule (Regola modulo di pianificazione basato sul tempo)]** e modifica il tempo in secondi nel campo **[!UICONTROL Periodic Scheduler (Modulo di pianificazione periodica)]**. Ad esempio, l’espressione di esempio `0 0 0 &ast; &ast; ?` attiva il processo a 00 ore.
1. Seleziona **[!UICONTROL Invia e-mail]** per ricevere e-mail alla scadenza di una risorsa.

   >[!NOTE]
   >
   >Solo il creatore di risorse (la persona che carica una particolare risorsa in [!DNL Assets]) riceve un’e-mail alla scadenza della risorsa. Per ulteriori informazioni sulla configurazione delle notifiche e-mail a livello globale [!DNL Experience Manager], consulta [come configurare la notifica e-mail](/help/sites-administering/notification.md) .

1. Nel campo **[!UICONTROL Notifica preventiva in secondi]** , specifica il tempo in secondi prima della scadenza di una risorsa quando desideri ricevere una notifica relativa alla scadenza. I creatori di risorse ricevono un messaggio prima della scadenza della risorsa che ti informa che la risorsa sta per scadere dopo il tempo specificato. Dopo la scadenza della risorsa, riceverai un’altra notifica che conferma la scadenza. Inoltre, le risorse scadute vengono disattivate.

1. Fai clic su **[!UICONTROL Salva]**.

## Stati delle risorse {#asset-states}

La console [!DNL Assets] può visualizzare vari stati delle risorse. A seconda dello stato corrente di una particolare risorsa, nella relativa vista a schede viene visualizzata un’etichetta che ne descrive lo stato, ad esempio Scaduto, Pubblicato, Approvato, Rifiutato e così via.

1. Nell’interfaccia utente di [!DNL Assets] , seleziona una risorsa.
1. Fai clic su **[!UICONTROL Pubblica]** nella barra degli strumenti. Se non trovi **Pubblica** sulla barra degli strumenti, fai clic su **[!UICONTROL Altro]** sulla barra degli strumenti e individua l&#39;opzione **[!UICONTROL Pubblica]** ![Pubblica](assets/do-not-localize/publish-globe.png) .
1. Scegli **[!UICONTROL Pubblica]** dal menu, quindi chiudi la finestra di dialogo di conferma.
1. Esci dalla modalità di selezione. Lo stato di pubblicazione della risorsa viene visualizzato nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, la colonna Pubblicato visualizza l’ora in cui è stata pubblicata la risorsa.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Per visualizzare la pagina dei dettagli della risorsa, nell’interfaccia [!DNL Assets] seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]** ![visualizza proprietà](assets/do-not-localize/info-circle-icon.png).

1. Nella scheda [!UICONTROL Avanzate] , imposta una data di scadenza per la risorsa dal campo **[!UICONTROL Scade]** .

   ![imposta la data e l’ora di scadenza del cespite nel campo Scadenza](assets/asset-properties-advanced-tab.png)

   *Figura:   Scheda Avanzate nella pagina   Proprietà delle risorse per impostare la scadenza delle risorse.*

1. Fai clic su **[!UICONTROL Salva]**, quindi fai clic su **[!UICONTROL Chiudi]** per visualizzare la console delle risorse.
1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa viene visualizzato come **[!UICONTROL Scaduto]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. Nella console [!DNL Assets], seleziona una cartella e crea un’attività di revisione sulla cartella.
1. Rivedi e approva/rifiuta le risorse nell’attività di revisione e fai clic su **[!UICONTROL Completa]**.
1. Passare alla cartella per la quale è stata creata l&#39;attività di revisione. Lo stato delle risorse approvate o rifiutate viene visualizzato nella parte inferiore della vista a schede. Nella vista a elenco, gli stati di approvazione e scadenza vengono visualizzati nelle colonne appropriate.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Per cercare le risorse in base al loro stato, fai clic su **[!UICONTROL Cerca]** ![opzione di ricerca](assets/do-not-localize/search_icon.png) per visualizzare la barra di ricerca Omnisearch.
1. Seleziona `Return` e fai clic su [!DNL Experience Manager] per visualizzare il pannello di ricerca.
1. Nel pannello di ricerca, fai clic su **[!UICONTROL Stato pubblicazione]** e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Fai clic su **[!UICONTROL Stato approvazione]** e fai clic sull&#39;opzione appropriata per cercare le risorse approvate o rifiutate.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Per cercare le risorse in base al loro stato di scadenza, seleziona **[!UICONTROL Stato scadenza]** nel pannello di ricerca e scegli l’opzione appropriata.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Puoi anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, puoi cercare le risorse pubblicate che sono state approvate in un’attività di revisione e che non sono ancora scadute selezionando le opzioni appropriate nei facet di ricerca.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

Questa funzione impone l’accettazione del contratto di licenza prima di poter scaricare una risorsa con licenza da [!DNL Adobe Experience Manager Assets].

Se selezioni una risorsa protetta e fai clic su **[!UICONTROL Scarica]**, vieni reindirizzato a una pagina di licenza per accettare il contratto di licenza. Se non accetti il contratto di licenza, l&#39;opzione **[!UICONTROL Scarica]** non è disponibile.

Se la selezione contiene più risorse protette, seleziona una risorsa alla volta, accetta il contratto di licenza e procedi con il download.

Un’attività è considerata protetta se una di queste condizioni è soddisfatta:

* La proprietà metadati della risorsa `xmpRights:WebStatement` punta al percorso della pagina che contiene il contratto di licenza per la risorsa.
* Il valore della proprietà metadati risorsa `adobe_dam:restrictions` è un codice HTML non elaborato che specifica il contratto di licenza.

>[!NOTE]
>
>La posizione `/etc/dam/drm/licenses` utilizzata per memorizzare le licenze nelle versioni precedenti di [!DNL Experience Manager] è obsoleta.
>
>Se crei o modifichi pagine di licenza o le porti dalle versioni precedenti di [!DNL Experience Manager], Adobe consiglia di memorizzarle in `/apps/settings/dam/drm/licenses` o `/conf/&ast;/settings/dam/drm/licenses`.

### Scaricare risorse protette da DRM {#downloading-drm-assets}

1. Nella vista a schede, seleziona le risorse da scaricare e fai clic su **[!UICONTROL Scarica]**.
1. Nella pagina **[!UICONTROL Gestione copyright]**, seleziona dall’elenco la risorsa da scaricare.
1. Nel riquadro [!UICONTROL Licenza], scegli **[!UICONTROL Accetto]**. Accanto alla risorsa viene visualizzato un segno di spunta. Fai clic sull&#39;opzione **[!UICONTROL Scarica]** .

   >[!NOTE]
   >
   >L’opzione **[!UICONTROL Scarica]** è abilitata solo quando scegli di accettare il contratto di licenza per una risorsa protetta. Tuttavia, se la selezione include sia risorse protette che non protette, solo le risorse protette sono elencate nel riquadro e l’opzione **[!UICONTROL Scarica]** è abilitata per scaricare le risorse non protette. Per accettare in contemporanea i contratti di licenza per più risorse protette, seleziona le risorse dall’elenco e fai clic su **[!UICONTROL Accetto]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]** per scaricare la risorsa o le relative rappresentazioni.
