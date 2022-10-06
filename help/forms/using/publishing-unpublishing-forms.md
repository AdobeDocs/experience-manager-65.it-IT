---
title: Pubblicazione e annullamento della pubblicazione di moduli e documenti
seo-title: Publishing and unpublishing forms and documents
description: È possibile pianificare la pubblicazione e l’annullamento della pubblicazione dei moduli. I moduli pubblicati vengono replicati nell’istanza di pubblicazione.
seo-description: You can schedule publishing and unpublishing of forms. Published forms are replicated on the publish instance.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Pubblicazione e annullamento della pubblicazione di moduli e documenti{#publishing-and-unpublishing-forms-and-documents}

AEM Forms consente di creare, pubblicare e annullare facilmente la pubblicazione dei moduli. Per ulteriori informazioni su AEM Forms, vedi [Introduzione alla gestione dei moduli](../../forms/using/introduction-managing-forms.md).

Il server AEM Forms fornisce due istanze: Creazione e pubblicazione. L’istanza di authoring consente di creare e gestire le risorse e le risorse del modulo. L’istanza di pubblicazione serve a mantenere le risorse e le risorse correlate disponibili per gli utenti finali. È possibile importare XDP e PDF forms nella modalità Autore. Per ulteriori informazioni, consulta [Ottenimento di documenti XDP e PDF in AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md).

## Risorse supportate   {#supported-assets-nbsp}

AEM Forms supporta i seguenti tipi di risorse:

* Moduli adattivi
* Documenti adattivi
* Frammenti di moduli adattivi
* Temi
* Modelli di modulo (moduli XFA)
* PDF forms
* Documento (documenti Flat PDF)
* Set di moduli
* Risorsa (immagini, schemi e fogli di stile)

Inizialmente, tutte le risorse sono disponibili solo nell’istanza di authoring. Un amministratore o un autore di moduli può pubblicare tutte le risorse, tranne le risorse.

Quando si seleziona un modulo e lo si pubblica, vengono pubblicate anche le relative risorse e risorse. Tuttavia, le risorse dipendenti non vengono pubblicate. In questo contesto, le risorse e le risorse correlate sono risorse utilizzate o a cui si riferisce una risorsa pubblicata. Le risorse dipendenti sono risorse che fanno riferimento a una risorsa pubblicata.

Il tuo Adaptive Forms può utilizzare alcune configurazioni, impostazioni e personalizzazioni che non vengono pubblicate automaticamente. È consigliabile pubblicare o attivare queste risorse prima di pubblicare un modulo adattivo.

* Modelli di modulo adattivo modificabili
* Configurazioni di Cloud Service per Adobe Sign, Typekit, reCAPTCHA e modelli di dati per moduli
* Altre configurazioni di Cloud Services vengono attivate solo se l’utente dispone di autorizzazioni di amministrazione.
* Personalizzazioni. Questi includono, tra l&#39;altro:

   * Layout personalizzati
   * Aspetto personalizzato
   * File CSS - da inserire nella finestra di dialogo delle proprietà del contenitore Modulo adattivo
   * Categoria libreria client: da inserire nella finestra di dialogo delle proprietà del contenitore Modulo adattivo
   * Qualsiasi altra libreria client che può essere inclusa come parte del modello di modulo adattivo.
   * Percorsi di progettazione

## Stati delle risorse {#asset-states}

Una risorsa può avere i seguenti stati:

* **Non pubblicato:** Una risorsa che non è mai stata pubblicata (lo stato di pubblicazione non è valido solo per le risorse Forms). Le risorse di Gestione Corrispondenza non dispongono di uno stato Non pubblicato.)
* **Pubblicato**: Una risorsa pubblicata ed disponibile nell’istanza Pubblica
* **Modificato**: Una risorsa che viene modificata dopo la pubblicazione

## Pubblicare una risorsa {#publish-an-asset}

1. Accedi al server AEM Forms.
1. Utilizza una delle seguenti opzioni per selezionare e pubblicare una risorsa.

   1. Sposta il puntatore su una risorsa e tocca **[!UICONTROL Pubblica]** ![aem6forms_globbe](assets/aem6forms_globe.pngasset.png).
   1. Effettua una delle seguenti operazioni, quindi tocca Pubblica:

      * Se ti trovi nella vista a schede, tocca **[!UICONTROL Inserisci selezione]** ![aem6forms_check-cerchio](assets/aem6forms_check-circle.png), quindi tocca la risorsa. La risorsa viene selezionata.
      * Se ti trovi nella vista a elenco, seleziona la casella di controllo di una risorsa. La risorsa viene selezionata.
      * Toccate una risorsa per visualizzarne i dettagli.
      * Visualizzare le proprietà di una risorsa toccando Visualizza proprietà ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >Non selezionare più risorse. La pubblicazione di più risorse contemporaneamente non è supportata.


1. All’avvio del processo di pubblicazione viene visualizzata una finestra di dialogo di conferma in cui sono elencate tutte le risorse e le risorse correlate. Nella finestra di dialogo che contiene le risorse correlate, tocca **[!UICONTROL Pubblica]**. La risorsa viene pubblicata e viene visualizzata la finestra di dialogo Pubblica risorse completata.

   >[!NOTE]
   >
   >Per i moduli adattivi, insieme alle relative risorse, viene visualizzato anche il nome della pagina Modulo adattivo .

   ![Una finestra di dialogo di conferma con tutte le risorse e le risorse correlate](assets/p4.png)

   Una finestra di dialogo di conferma con tutte le risorse e le risorse correlate.

   >[!NOTE]
   >
   >Per Forms Manager, se l’utente non dispone dell’autorizzazione per pubblicare le risorse elencate, l’azione Pubblica è disabilitata. Una risorsa che richiede autorizzazioni aggiuntive viene visualizzata in rosso.

   Dopo la pubblicazione di una risorsa, le proprietà dei metadati della risorsa vengono copiate nell’istanza Pubblica e lo stato della risorsa viene modificato in Pubblicato. Anche lo stato delle risorse dipendenti pubblicate viene modificato in Pubblicato .

   Dopo aver pubblicato una risorsa, puoi utilizzare il portale Forms per visualizzare tutte le risorse su una pagina web. Per ulteriori informazioni, consulta [Introduzione alla pubblicazione di moduli su un portale](../../forms/using/introduction-publishing-forms.md).

## Pubblicare tutte le risorse di Gestione Corrispondenza {#publish-all-the-correspondence-management-assets}

AEM Forms consente di pubblicare tutte le risorse di Gestione Corrispondenza su un server contemporaneamente. Le risorse pubblicate includono tutte le risorse di Gestione Corrispondenza e le relative dipendenze.

Completa i seguenti passaggi per pubblicare su un server tutte le risorse di Gestione Corrispondenza :

1. Accedi al server AEM Forms.
1. Tocca **Adobe Experience Manager** nella barra di navigazione globale.
1. Tocca ![strumenti](assets/tools.png), quindi tocca **Forms**.
1. Tocca **Pubblicare le risorse di gestione della corrispondenza**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   Viene visualizzata la pagina Pubblica tutte le risorse di gestione della corrispondenza, con le informazioni relative all’ultima volta che è stato effettuato un tentativo di pubblicazione del processo Risorse di gestione della corrispondenza.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Tocca **Pubblica** e, nel messaggio di conferma, tocca **OK**.

   Al termine di un processo batch, puoi visualizzare i dettagli dell&#39;ultima esecuzione. Ciò include informazioni quali l&#39;accesso Amministratore e se il batch viene eseguito correttamente o non è riuscito.

   >[!NOTE]
   >
   >Il processo di pubblicazione non può essere annullato una volta avviato. Inoltre, mentre l’operazione di pubblicazione è in corso, non creare, eliminare, modificare o pubblicare risorse o avviare l’operazione Esporta tutte le risorse di gestione della corrispondenza.

## Pubblicazione automatica e annullamento della pubblicazione per Forms e documenti {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms consente di pianificare la pubblicazione e l’annullamento della pubblicazione delle risorse per Forms e documenti. È possibile specificare la pianificazione nell’Editor metadati. Per ulteriori informazioni sulla gestione dei metadati del modulo, consulta [Gestione dei metadati del modulo.](../../forms/using/manage-form-metadata.md)

Segui questi passaggi per pianificare la data e l’ora di pubblicazione e annullamento della pubblicazione delle risorse Forms &amp; Documents:

1. Seleziona una risorsa e tocca **[!UICONTROL Visualizza proprietà]**. Viene visualizzata la pagina Proprietà metadati .
1. Nella pagina Proprietà metadati , tocca **[!UICONTROL Avanzate]**, quindi tocca **[!UICONTROL Modifica]** ![illustratorcc_penciltool_agreement_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. In **[!UICONTROL Pubblica in tempo]** e **[!UICONTROL Ora di disattivazione pubblicazione]** selezionare la data e l&#39;ora.\
   Tocca **[!UICONTROL Fine]** ![aem6forms_check](assets/aem6forms_check.png).

## Annullare la pubblicazione di una risorsa {#unpublish-an-asset}

1. Seleziona una risorsa pubblicata e tocca **[!UICONTROL Annulla pubblicazione]** ![annullare](assets/unpublish.png).
1. Utilizza una delle seguenti opzioni per selezionare e annullare la pubblicazione di una risorsa.

   1. Sposta il puntatore su una risorsa e tocca **[!UICONTROL Annulla pubblicazione]** ![annullare](assets/unpublish.png).
   1. Effettua una delle seguenti operazioni, quindi tocca Annulla pubblicazione:

      * Se ti trovi nella vista a schede, tocca **[!UICONTROL Inserisci selezione]** ![aem6forms_check-cerchio](assets/aem6forms_check-circle.png), quindi tocca la risorsa. La risorsa viene selezionata.

      * Se ti trovi nella vista a elenco, passa il puntatore del mouse su una risorsa e tocca ![segno di spunta](assets/selectassetcheckmark.png) . La risorsa viene selezionata.

      * Toccate una risorsa per visualizzarne i dettagli.
      * Visualizzare le proprietà di una risorsa toccando Visualizza proprietà ![viewproperties](assets/viewproperties.png).

1. All&#39;avvio del processo di annullamento pubblicazione viene visualizzata una finestra di dialogo di conferma. Tocca **[!UICONTROL Annulla pubblicazione]**.

   >[!NOTE]
   >
   >Solo la risorsa selezionata viene annullata e le relative risorse figlie e di riferimento, se presenti, non vengono annullate la pubblicazione.

## Ripristino di una risorsa o di una lettera alla versione pubblicata in precedenza {#revert-an-asset-or-letter-to-the-previously-published-version}

Ogni volta che pubblichi una risorsa o una lettera dopo averla modificata, viene creata una versione della risorsa o della lettera. Puoi ripristinare una risorsa o una lettera a una versione pubblicata in precedenza. Potrebbe essere necessario eseguire questa operazione se qualcosa non funziona correttamente nella versione corrente della risorsa o del documento.

>[!NOTE]
>
>Non ripristinare una lettera a un ultimo stato pubblicato se una risorsa dipendente utilizzata in tale lettera pubblicata viene eliminata dal sistema.

1. Seleziona una risorsa e tocca **[!UICONTROL Ripristina versione pubblicata in precedenza]** ![reverttopreview publishedversion](assets/reverttopreviouslypublishedversion.png).
1. Prima che la risorsa venga ripristinata, viene visualizzata una finestra di dialogo di conferma. Tocca **[!UICONTROL Ripristina]**.

   Viene eseguito il rollback della risorsa o della lettera alla versione pubblicata in precedenza.

## Eliminare una risorsa {#delete-an-asset}

>[!NOTE]
>
>L’eliminazione di una risorsa la rimuove dall’istanza di pubblicazione. L’eliminazione di una risorsa comporta anche la rimozione della cronologia delle versioni, ad eccezione della versione di base.

1. Seleziona una risorsa e tocca **[!UICONTROL Elimina]** ![delete](assets/delete.png).

   >[!NOTE]
   >
   >L’opzione Elimina è disponibile anche quando visualizzi i dettagli della risorsa toccando una risorsa o visualizzando le proprietà di una risorsa toccando Visualizza proprietà ![viewproperties](assets/viewproperties.png).

1. Prima di eliminare la risorsa, viene visualizzata una finestra di dialogo di conferma. Tocca **[!UICONTROL Elimina]**.

   >[!NOTE]
   >
   >Solo la risorsa selezionata viene eliminata, le risorse dipendenti e non vengono eliminate. Per controllare i riferimenti di una risorsa, tocca ![riferimenti](assets/references.png) quindi seleziona una risorsa.
   >
   >
   >Se la risorsa che si sta tentando di eliminare è una risorsa figlia di un’altra risorsa, non viene eliminata. Per eliminare una risorsa di questo tipo, rimuovi i riferimenti di questa risorsa da altre risorse e riprova.

## Moduli adattivi protetti {#protected-adaptive-forms}

È possibile abilitare l’autenticazione per i moduli a cui gli utenti selezionati devono accedere. Quando si abilita l’autenticazione per i moduli, gli utenti visualizzano una schermata di accesso prima di accedervi. Solo gli utenti con credenziali autorizzate possono accedere ai moduli.

Per abilitare l’autenticazione per i moduli:

1. Nel browser, apri configMgr nell&#39;istanza di pubblicazione.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Nella configurazione della console Web di Adobe Experience Manager, fai clic su **Servizio di autenticazione Apache Sling** per configurarlo.
1. Nella finestra di dialogo Apache Sling Authentication Service visualizzata, utilizza il **+** per aggiungere percorsi.\
   Quando si aggiunge un percorso, il servizio di autenticazione è abilitato per i moduli presenti in tale percorso.
