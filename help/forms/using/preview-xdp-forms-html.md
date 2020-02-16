---
title: Genera anteprima HTML5 di un modulo XDP
seo-title: Genera anteprima HTML5 di un modulo XDP
description: La scheda Anteprima HTML in LiveCycle Designer consente di visualizzare l'anteprima dei moduli così come vengono visualizzati in un browser.
seo-description: La scheda Anteprima HTML in LiveCycle Designer consente di visualizzare l'anteprima dei moduli così come vengono visualizzati in un browser.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# Genera anteprima HTML5 di un modulo XDP{#generate-html-preview-of-an-xdp-form}

Durante la progettazione di un modulo in AEM Forms Designer, oltre alla visualizzazione dell&#39;anteprima del rendering PDF di un modulo, è anche possibile visualizzarne l&#39;anteprima in HTML5. È possibile utilizzare la scheda **Anteprima HTML** per visualizzare l&#39;anteprima di un modulo così come apparirebbe in un browser.

## Abilita anteprima HTML per i moduli XDP in Designer {#html-preview-of-forms-in-forms-designer}

Per consentire a Designer di generare l&#39;anteprima HTML dei moduli XDP, eseguire le configurazioni seguenti:

* Configurare il servizio di autenticazione Apache Sling
* Disattiva modalità protetta
* Fornire i dettagli del server AEM Forms

### Configurare il servizio di autenticazione Apache Sling {#configure-apache-sling-authentication-service}

1. Accedi a `https://[server]:[port]/system/console/configMgr` AEM Forms in esecuzione su OSGi o
   `https://[server]:[port]/lc/system/console/configMgr` in AEM Forms in esecuzione su JEE.
1. Individuate e fate clic sulla configurazione **Apache Sling Authentication Service** per aprirla in modalità di modifica.

1. A seconda se AEM Forms è in esecuzione su OSGi o JEE, aggiungi quanto segue nel campo Requisiti **di** autenticazione:

   * AEM Forms su JEE

      * -/content/xfaforms
      * -/etc/clientlibals
   * AEM Forms su OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms
   >[!NOTE]
   >
   >Non copiate e incollate il valore specificato nel campo Requisiti autenticazione, in quanto potrebbe danneggiare i caratteri speciali presenti nel valore. Digitare il valore specificato nel campo.

1. Specificate rispettivamente il nome utente e la password nei campi Nome **[!UICONTROL utente]** anonimo e Password **[!UICONTROL utente]** anonima. Le credenziali specificate vengono utilizzate per gestire l&#39;autenticazione anonima e consentire l&#39;accesso agli utenti anonimi.
1. Click **Save** to save the configuration.

### Disattiva modalità protetta {#disable-protected-mode}

Per impostazione predefinita, la modalità [](../../forms/using/get-xdp-pdf-documents-aem.md) protetta è attivata. Mantenetela attivata per gli ambienti di produzione. È possibile disabilitarlo per un ambiente di sviluppo per visualizzare l’anteprima dei moduli HTML5 nel designer. Per disattivarlo, effettuate le seguenti operazioni:

1. Accedete alla console Web di AEM come amministratore.

   * L’URL per AEM Forms su OSGi è `https://[server]:[port]/system/console/configMgr`
   * L&#39;URL di AEM Forms su JEE è `https://[server]:[port]/lc/system/console/configMgr`

1. Aprire le configurazioni dei moduli **[!UICONTROL mobili]** per la modifica.
1. Deselezionare l’opzione Modalità **** protetta e fare clic su **[!UICONTROL Salva]**.

### Fornire i dettagli del server AEM Forms {#provide-details-of-aem-forms-server}

1. In Designer, passare a **Strumenti** > **Opzioni**.
1. Nella finestra Opzioni, selezionate la pagina Opzioni **** server, fornite i seguenti dettagli e fate clic su **OK**.

   * **URL** server: URL del server AEM Forms.

   * **Numero** porta HTTP: Porta server AEM. Il valore predefinito è 4502.
   * **** Contesto anteprima HTML: Percorso del profilo per il rendering dei moduli XFA. I seguenti profili predefiniti sono utilizzati per visualizzare l&#39;anteprima del modulo in Designer. Tuttavia, potete anche specificare il percorso di un profilo personalizzato.

      * `/content/xfaforms/profiles/default.html` (AEM Forms su OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms su JEE)
   * **** Contesto Forms Manager: Percorso di contesto in cui viene distribuita l&#39;interfaccia utente di Forms Manager. I valori predefiniti sono:

      * `/aem/forms` (AEM Forms su OSGi)
      * `/lc/forms` (AEM Forms su JEE)
   **** Nota: Verifica che il server AEM Forms sia attivato ed in esecuzione. The HTML preview connects to the CRX server to *generate* a preview.

   ![Opzioni di AEM Forms Designer ](assets/server_options.png)

   Opzioni di AEM Forms Designer

1. Per visualizzare l&#39;anteprima di un modulo in HTML, fare clic sulla scheda **Anteprima HTML** .

   >[!NOTE]
   >
   >
   >
   >
   >    * Se la scheda Anteprima HTML è chiusa, premere F4 per aprire la scheda Anteprima HTML. Potete anche selezionare Anteprima HTML dal menu Visualizza per aprire la scheda Anteprima HTML.
   >    * L&#39;anteprima HTML non supporta i documenti PDF, l&#39;anteprima HTML è solo per i documenti XDP.


   >[!CAUTION]
   >
   >Per testare l&#39;esperienza utente finale reale, visualizzare l&#39;anteprima dei moduli nei browser esterni (Google Chrome, Microsoft Edge, Mozilla Firefox e altro ancora). Ogni browser utilizza un motore separato per eseguire il rendering HTML, pertanto è possibile che le modalità di anteprima del modulo in Designer e nel browser esterno siano diverse.

## Visualizzazione in anteprima di un modulo con dati di esempio {#to-preview-a-form-using-sample-data}

Designer consente di visualizzare l’anteprima del modulo e di verificarne il funzionamento mediante l’uso di dati XML di esempio. È consigliabile eseguire frequentemente delle verifiche del modulo e dei dati di esempio per assicurarsi che sul modulo venga eseguito correttamente il rendering.

Se non sono disponibili dati di esempio, è possibile crearli manualmente o automaticamente tramite Designer. (Vedere [Generazione automatica di dati di esempio per la visualizzazione in anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) e [Creazione di dati di esempio per la visualizzazione in anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

La verifica del modulo mediante un’origine dati di esempio garantisce la mappatura dei dati e dei campi e la corretta ripetizione dei sottomoduli. È possibile creare un layout di modulo bilanciato che fornisce lo spazio appropriato per la visualizzazione dei dati uniti a ciascun oggetto.

1. Select **File > Form Properties**.

1. Click the **Preview** tab and, in the Data File box, type the full path to your test data file. Potete anche utilizzare il pulsante Sfoglia per individuare il file.

1. Fai clic su **OK**. The next time you preview the form in the **Preview HTML** tab, the data values from the sample XML file will appear in the respective objects.

## Anteprima dei moduli che si trovano in un archivio {#html-preview-of-forms-in-forms-manager}

In AEM Forms è possibile visualizzare in anteprima moduli e documenti in un archivio. La funzione Anteprima consente di sapere esattamente l’aspetto e il funzionamento dei moduli così come verranno utilizzati dagli utenti finali.

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
