---
title: Digital Rights Management di risorse
description: Scopri come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in [!DNL Experience Manager].
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 7%

---

# Digital Rights Management per le risorse {#digital-rights-management-in-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=en) |
| AEM 6.5 | Questo articolo |

Le risorse digitali sono spesso associate a una licenza che specifica i termini e la durata di utilizzo. Perché [!DNL Adobe Experience Manager Assets] è completamente integrato con [!DNL Experience Manager] piattaforma, puoi gestire in modo efficiente le informazioni sulla scadenza delle risorse e gli stati delle risorse. È inoltre possibile associare le informazioni sulle licenze alle risorse.

## Scadenza risorsa {#asset-expiration}

La scadenza delle risorse è un modo efficace per applicare i requisiti di licenza per le risorse. In questo modo la risorsa pubblicata non verrà più pubblicata alla scadenza, evitando possibili violazioni della licenza. Un utente senza autorizzazioni di amministratore non può modificare, copiare, spostare, pubblicare e scaricare una risorsa scaduta.

Puoi visualizzare lo stato di scadenza di una risorsa in [!DNL Assets] sia nella vista a schede che in quella a elenco.

![scaduto_flag_list](assets/expired_flag_list.png)

*Figura: Nella vista a elenco, la [!UICONTROL Stato] nella colonna viene visualizzato [!UICONTROL Scaduto] banner.*

Puoi visualizzare lo stato di scadenza di una risorsa in [!UICONTROL Timeline] nella barra a sinistra.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>La data di scadenza di una risorsa viene visualizzata in modo diverso per gli utenti con fusi orari diversi.

Puoi anche visualizzare lo stato di scadenza delle risorse nella sezione **[!UICONTROL Riferimenti]** barra. Gestisce gli stati di scadenza delle risorse e le relazioni tra le risorse composte e le risorse secondarie, le raccolte e i progetti di riferimento.

1. Passa alla risorsa per la quale desideri visualizzare le pagine web di riferimento e le risorse composte.
1. Seleziona la risorsa e apri **[!UICONTROL Riferimenti]** nella barra a sinistra. Per le risorse scadute, la [!UICONTROL Riferimenti] la barra mostra lo stato di scadenza **[!UICONTROL Risorsa scaduta]** in alto.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Se la risorsa è scaduta, la [!UICONTROL Riferimenti] la barra mostra lo stato **[!UICONTROL La risorsa ha risorse secondarie scadute]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Cercare risorse scadute {#search-expired-assets}

Puoi cercare le risorse scadute, comprese le risorse secondarie scadute, nel pannello Ricerca.

1. In [!DNL Assets] , fai clic su **[!UICONTROL Ricerca]** nella barra degli strumenti per visualizzare la casella Omnisearch.

1. Con il cursore nella casella Omnisearch, selezionate la `Enter` per visualizzare la pagina dei risultati della ricerca.
1. Apri il pannello di ricerca nella barra a sinistra. Fai clic su **[!UICONTROL Stato scadenza]** per espanderla.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Scegli **[!UICONTROL Scaduto]**. Dopo aver filtrato i risultati della ricerca, vengono visualizzate solo le risorse scadute.

Quando scegli il **[!UICONTROL Scaduto]** , l&#39;opzione [!DNL Assets] in console vengono visualizzate solo le risorse scadute e le risorse secondarie a cui fanno riferimento le risorse composte. Le risorse composte che fanno riferimento a risorse secondarie scadute non vengono visualizzate immediatamente dopo la scadenza delle risorse secondarie. Vengono invece visualizzati dopo [!DNL Experience Manager] rileva che fanno riferimento a risorse secondarie scadute alla successiva esecuzione del modulo di pianificazione.

Se modifichi la data di scadenza di una risorsa pubblicata impostandola su una data precedente al ciclo di pianificazione corrente, la pianificazione rileva comunque la risorsa come scaduta alla successiva esecuzione e ne riflette lo stato di conseguenza.

Inoltre, se un problema o un errore impedisce al modulo di pianificazione di rilevare le risorse scadute nel ciclo corrente, il modulo di pianificazione le esamina nuovamente nel ciclo successivo e ne rileva lo stato di scadenza.

Per attivare [!DNL Assets] per visualizzare le risorse composte di riferimento insieme alle risorse secondarie scadute, configura una **[!UICONTROL Notifica di scadenza DAM Adobe CQ]** flusso di lavoro in [!DNL Experience Manager] Gestione configurazione.

1. Apri [!DNL Experience Manager] Gestione configurazione.
1. Scegli **[!UICONTROL Notifica di scadenza DAM Adobe CQ]**. Per impostazione predefinita, **[!UICONTROL Modulo di pianificazione basato su tempo]** , che programma un processo per verificare in un momento specifico se una risorsa è scaduta. Al termine del processo, le risorse con risorse secondarie scadute e le risorse di riferimento vengono visualizzate come scadute nei risultati della ricerca.

1. Per eseguire il processo periodicamente, cancella il campo **[!UICONTROL Time Based Scheduler Rule (Regola modulo di pianificazione basato sul tempo)]** e modifica il tempo in secondi nel campo **[!UICONTROL Periodic Scheduler (Modulo di pianificazione periodica)]**. Ad esempio, l’espressione di esempio `0 0 0 * * ?` attiva il processo alle ore 00.
1. Seleziona **[!UICONTROL invia e-mail]** per ricevere e-mail alla scadenza di una risorsa.

   >[!NOTE]
   >
   >Solo il creatore della risorsa (la persona che carica una particolare risorsa in [!DNL Assets]) riceve un’e-mail quando la risorsa scade. Consulta [come configurare le notifiche e-mail](/help/sites-administering/notification.md) per ulteriori dettagli sulla configurazione delle notifiche e-mail all’indirizzo [!DNL Experience Manager] livello.

1. In **[!UICONTROL Notifica preventiva in secondi]** , specifica il tempo in secondi precedente alla scadenza di una risorsa per ricevere una notifica relativa alla scadenza. I creatori delle risorse ricevono un messaggio prima della scadenza della risorsa che informa che la risorsa sta per scadere dopo il tempo specificato. Dopo la scadenza della risorsa, ricevi un’altra notifica che conferma la scadenza. Inoltre, le risorse scadute vengono disattivate.

1. Fai clic su **[!UICONTROL Salva]**.

## Stati risorse {#asset-states}

Il [!DNL Assets] la console può visualizzare vari stati delle risorse. A seconda dello stato corrente di una particolare risorsa, la relativa vista a schede mostra un’etichetta che ne descrive lo stato, ad esempio Scaduto, Pubblicato, Approvato, Rifiutato e così via.

1. In [!DNL Assets] interfaccia utente, seleziona una risorsa.
1. Clic **[!UICONTROL Pubblica]** dalla barra degli strumenti. Se non vedi **Pubblica** sulla barra degli strumenti, fai clic su **[!UICONTROL Altro]** sulla barra degli strumenti e individuare **[!UICONTROL Pubblica]** ![opzione di pubblicazione](assets/do-not-localize/publish-globe.png) opzione.
1. Scegli **[!UICONTROL Pubblica]** dal menu, quindi chiudere la finestra di dialogo di conferma.
1. Esci dalla modalità di selezione. Lo stato di pubblicazione della risorsa viene visualizzato nella parte inferiore della miniatura nella vista a schede. Nella vista a elenco, la colonna Pubblicato mostra l’ora in cui la risorsa è stata pubblicata.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Per visualizzare la pagina dei dettagli della risorsa, nella [!DNL Assets] , seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]** ![visualizza proprietà](assets/do-not-localize/info-circle-icon.png).

1. In [!UICONTROL Avanzate] , imposta una data di scadenza per la risorsa dalla scheda **[!UICONTROL Scade]** campo.

   ![impostare data e ora di scadenza risorsa nel campo Scadenza](assets/asset-properties-advanced-tab.png)

   *Figura: [!UICONTROL Avanzate] scheda nella risorsa [!UICONTROL Proprietà] per impostare la scadenza della risorsa.*

1. Clic **[!UICONTROL Salva]** e quindi fare clic su **[!UICONTROL Chiudi]** per visualizzare la console Risorse.
1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa viene visualizzato come **[!UICONTROL Scaduto]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. In [!DNL Assets] , selezionare una cartella e creare un&#39;attività di revisione sulla cartella.
1. Rivedi e approva/rifiuta le risorse nell’attività di revisione e fai clic su **[!UICONTROL Completa]**.
1. Passare alla cartella per la quale è stata creata l&#39;attività di revisione. Lo stato delle risorse approvate/rifiutate viene visualizzato nella parte inferiore della vista a schede. Nella vista a elenco, gli stati di approvazione e scadenza vengono visualizzati nelle colonne appropriate.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Per cercare le risorse in base al loro stato, fai clic su **[!UICONTROL Ricerca]** ![opzione di ricerca](assets/do-not-localize/search_icon.png) per visualizzare la barra di Omnisearch.
1. Seleziona `Return` e fai clic su [!DNL Experience Manager] per visualizzare il pannello di ricerca.
1. Nel pannello di ricerca, fai clic su **[!UICONTROL Stato pubblicazione]** e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Clic **[!UICONTROL Stato approvazione]** e fai clic sull’opzione appropriata per cercare le risorse approvate o rifiutate.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Per cercare le risorse in base al loro stato di scadenza, seleziona **[!UICONTROL Stato scadenza]** nel pannello di ricerca e scegli l’opzione appropriata.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Puoi anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, per cercare le risorse pubblicate che sono state approvate in un’attività di revisione e non sono ancora scadute, seleziona le opzioni appropriate nei facet di ricerca.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

Questa funzione impone l’accettazione del contratto di licenza prima di scaricare una risorsa concessa in licenza da [!DNL Adobe Experience Manager Assets].

Se selezioni una risorsa protetta e fai clic **[!UICONTROL Scarica]**, viene reindirizzato a una pagina di licenza per accettare il contratto di licenza. Se non si accetta il contratto di licenza, il **[!UICONTROL Scarica]** non è disponibile.

Se la selezione contiene più risorse protette, seleziona una risorsa alla volta, accetta il contratto di licenza e procedi al download della risorsa.

Un bene è considerato protetto se è soddisfatta una delle seguenti condizioni:

* La proprietà dei metadati della risorsa `xmpRights:WebStatement` punta al percorso della pagina che contiene il contratto di licenza per la risorsa.
* Valore della proprietà dei metadati della risorsa `adobe_dam:restrictions` è un HTML non elaborato che specifica il contratto di licenza.

>[!NOTE]
>
>La posizione `/etc/dam/drm/licenses` utilizzato per memorizzare le licenze nelle versioni precedenti di [!DNL Experience Manager] è obsoleto.
>
>Se si creano o si modificano pagine di licenza o si eseguono il porting da precedenti [!DNL Experience Manager] versioni di, l’Adobe consiglia di memorizzarle in `/apps/settings/dam/drm/licenses` o `/conf/&ast;/settings/dam/drm/licenses`.

### Scaricare risorse protette da DRM {#downloading-drm-assets}

1. Nella vista a schede, seleziona le risorse da scaricare e fai clic su **[!UICONTROL Scarica]**.
1. Nella pagina **[!UICONTROL Gestione copyright]**, seleziona dall’elenco la risorsa da scaricare.
1. In [!UICONTROL Licenza] , scegli **[!UICONTROL Accetto]**. Accanto alla risorsa viene visualizzato un segno di spunta. Fai clic su **[!UICONTROL Scarica]** opzione.

   >[!NOTE]
   >
   >Il **[!UICONTROL Scarica]** L’opzione è abilitata solo quando decidi di accettare il contratto di licenza per una risorsa protetta. Tuttavia, se la selezione include sia risorse protette che non protette, nel riquadro e nel riquadro vengono elencate solo le risorse protette **[!UICONTROL Scarica]** per scaricare le risorse non protette. Per accettare in contemporanea i contratti di licenza per più risorse protette, seleziona le risorse dall’elenco e fai clic su **[!UICONTROL Accetto]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]** per scaricare la risorsa o le relative rappresentazioni.
