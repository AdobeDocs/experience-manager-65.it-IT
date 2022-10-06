---
title: Genera l’anteprima di un modulo XDP in HTML5
seo-title: Generate HTML5 preview of an XDP form
description: La scheda Anteprima HTML in LiveCycle Designer consente di visualizzare in anteprima i moduli visualizzati in un browser.
seo-description: Preview HTML tab in LiveCycle Designer can be used to preview forms as they appear in a browser.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
feature: Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 15%

---

# Genera l’anteprima di un modulo XDP in HTML5{#generate-html-preview-of-an-xdp-form}

Durante la progettazione di un modulo in AEM Forms Designer, oltre a visualizzare l’anteprima del rendering PDF di un modulo, è anche possibile visualizzarne l’anteprima in anteprima il rendering in HTML5. È possibile utilizzare **Anteprima HTML** per visualizzare l’anteprima di un modulo così come apparirebbe in un browser.

## Abilitare l’anteprima di HTML per i moduli XDP in Designer {#html-preview-of-forms-in-forms-designer}

Per consentire a Designer di generare un’anteprima HTML dei moduli XDP, esegui le seguenti configurazioni:

* Configurare il servizio di autenticazione Apache Sling
* Disattiva modalità protetta
* Fornire i dettagli del server AEM Forms

### Configurare il servizio di autenticazione Apache Sling {#configure-apache-sling-authentication-service}

1. Vai a `https://'[server]:[port]'/system/console/configMgr` su AEM Forms in esecuzione su OSGi o
   `https://'[server]:[port]'/lc/system/console/configMgr` su AEM Forms in esecuzione su JEE.
1. Individua e fai clic su **Servizio di autenticazione Apache Sling** per aprirla in modalità di modifica.

1. A seconda che tu esegua AEM Forms su OSGi o JEE, aggiungi quanto segue nella **Requisiti di autenticazione** campo:

   * AEM Forms su JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * AEM Forms su OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >Non copiare e incollare il valore specificato nel campo Requisiti di autenticazione in quanto potrebbe danneggiare i caratteri speciali nel valore. Digita invece il valore specificato nel campo .

1. Specifica un nome utente e una password in **[!UICONTROL Nome utente anonimo]** e **[!UICONTROL Password utente anonima]** rispettivamente. Le credenziali specificate vengono utilizzate per gestire l&#39;autenticazione anonima e consentire l&#39;accesso agli utenti anonimi.
1. Fai clic su **Salva** per salvare la configurazione.

### Disattiva modalità protetta {#disable-protected-mode}

La [modalità protetta](../../forms/using/get-xdp-pdf-documents-aem.md) è attivato, per impostazione predefinita. Mantenetela abilitata per gli ambienti di produzione. È possibile disattivarlo per un ambiente di sviluppo per visualizzare in anteprima HTML5 Forms nella progettazione. Esegui i seguenti passaggi per disattivarlo:

1. Accedi a AEM console Web come amministratore.

   * L’URL per AEM Forms su OSGi è `https://'[server]:[port]'/system/console/configMgr`
   * L’URL per AEM Forms su JEE è `https://'[server]:[port]'/lc/system/console/configMgr`

1. Apri **[!UICONTROL Configurazioni Forms per dispositivi mobili]** per la modifica.
1. Deseleziona la **[!UICONTROL Modalità protetta]** e fai clic su **[!UICONTROL Salva]**.

### Fornire i dettagli del server AEM Forms {#provide-details-of-aem-forms-server}

1. In Designer, vai a **Strumenti** > **Opzioni**.
1. Nella finestra Opzioni, seleziona **Opzioni server** fornire i seguenti dettagli e fare clic su **OK**.

   * **URL server**: URL del server AEM Forms.

   * **Numero di porta HTTP**: AEM porta server. Il valore predefinito è 4502.
   * **Contesto anteprima HTML:** Percorso del profilo per il rendering dei moduli XFA. I seguenti profili predefiniti vengono utilizzati per visualizzare l’anteprima del modulo in Designer. Tuttavia, puoi anche specificare il percorso di un profilo personalizzato.

      * `/content/xfaforms/profiles/default.html` (AEM Forms su OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms su JEE)
   * **Contesto Forms Manager:** Percorso di contesto in cui viene distribuita l’interfaccia utente di Forms Manager. I valori predefiniti sono:

      * `/aem/forms` (AEM Forms su OSGi)
      * `/lc/forms` (AEM Forms su JEE)

   >[!NOTE]
   >
   >Assicurati che il server AEM Forms sia in esecuzione. L’anteprima di HTML si connette al server CRX per *generare* un&#39;anteprima.

   ![Opzioni di AEM Forms Designer ](assets/server_options.png)

   Opzioni di AEM Forms Designer

1. Per visualizzare l’anteprima di un modulo in HTML, fai clic sul pulsante **Anteprima HTML** scheda .

   >[!NOTE]
   >
   >
   >
   >
   >    * Se la scheda Anteprima di HTML è chiusa, premere F4 per aprire la scheda Anteprima HTML. È inoltre possibile selezionare Anteprima HTML dal menu Visualizza per aprire la scheda Anteprima HTML.
   >    * L’anteprima di HTML non supporta i documenti PDF, l’anteprima di HTML è disponibile solo per i documenti XDP.


   >[!CAUTION]
   >
   >Per testare l’esperienza utente finale reale, è possibile visualizzare in anteprima i moduli nei browser esterni (Google Chrome, Microsoft Edge, Mozilla Firefox e altro ancora). Ogni browser utilizza un motore separato per il rendering di HTML, pertanto potrebbero esserci alcune differenze nel modo in cui un modulo viene visualizzato in anteprima in Designer e nel browser esterno.

## Visualizzazione in anteprima di un modulo con dati di esempio {#to-preview-a-form-using-sample-data}

Designer consente di visualizzare l’anteprima del modulo e di verificarne il funzionamento mediante l’uso di dati XML di esempio. È consigliabile eseguire frequentemente delle verifiche del modulo e dei dati di esempio per assicurarsi che sul modulo venga eseguito correttamente il rendering.

Se non sono disponibili dati di esempio, è possibile crearli manualmente o automaticamente tramite Designer. (Vedere [Generazione automatica di dati di esempio per la visualizzazione in anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) e [Creazione di dati di esempio per la visualizzazione in anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

La verifica del modulo mediante un’origine dati di esempio garantisce la mappatura dei dati e dei campi e la corretta ripetizione dei sottomoduli. È possibile creare un layout di modulo bilanciato che fornisce lo spazio appropriato per la visualizzazione dei dati uniti a ciascun oggetto.

1. Seleziona **File > Proprietà modulo**.

1. Fai clic sul pulsante **Anteprima** nella casella File dati digitare il percorso completo del file di dati di prova. È inoltre possibile utilizzare il pulsante Sfoglia per individuare il file desiderato.

1. Fai clic su **OK**. La prossima volta che si visualizza l’anteprima del modulo **Anteprima HTML** i valori dei dati del file XML di esempio verranno visualizzati nei rispettivi oggetti.

## Anteprima dei moduli presenti in un archivio {#html-preview-of-forms-in-forms-manager}

In AEM Forms è possibile visualizzare in anteprima moduli e documenti in un archivio. L’anteprima consente di sapere esattamente l’aspetto e il funzionamento dei moduli così come verranno utilizzati dagli utenti finali.
