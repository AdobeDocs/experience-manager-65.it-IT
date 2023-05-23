---
title: Generare l’anteprima HTML5 di un modulo XDP
seo-title: Generate HTML5 preview of an XDP form
description: È possibile utilizzare la scheda HTML anteprima in Progettazione LiveCycli per visualizzare in anteprima i moduli così come vengono visualizzati in un browser.
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
ht-degree: 0%

---

# Generare l’anteprima HTML5 di un modulo XDP{#generate-html-preview-of-an-xdp-form}

Durante la progettazione di un modulo in AEM Forms Designer, oltre a visualizzare l’anteprima della copia trasformata PDF di un modulo, è possibile anche visualizzarne una copia trasformata HTML 5. È possibile utilizzare **Anteprima HTML** per visualizzare in anteprima un modulo così come apparirebbe in un browser.

## Abilitare l’anteprima HTML per i moduli XDP in Designer {#html-preview-of-forms-in-forms-designer}

Per consentire a Designer di generare l’anteprima HTML dei moduli XDP, esegui le seguenti configurazioni:

* Configurare il servizio di autenticazione Apache Sling
* Disattiva modalità protetta
* Fornisci i dettagli del server AEM Forms

### Configurare il servizio di autenticazione Apache Sling {#configure-apache-sling-authentication-service}

1. Vai a `https://'[server]:[port]'/system/console/configMgr` su AEM Forms in esecuzione su OSGi o
   `https://'[server]:[port]'/lc/system/console/configMgr` su AEM Forms in esecuzione su JEE.
1. Individua e fai clic su **Servizio di autenticazione Apache Sling** per aprirla in modalità di modifica.

1. A seconda che AEM Forms sia in esecuzione su OSGi o JEE, aggiungi quanto segue in **Requisiti di autenticazione** campo:

   * AEM Forms su JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * AEM Forms su OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >Non copiare e incollare il valore specificato nel campo Requisiti di autenticazione in quanto potrebbe danneggiare i caratteri speciali nel valore. Digita invece il valore specificato nel campo.

1. Specificare un nome utente e una password in **[!UICONTROL Nome utente anonimo]** e **[!UICONTROL Password utente anonimo]** rispettivamente. Le credenziali specificate vengono utilizzate per gestire l&#39;autenticazione anonima e consentire l&#39;accesso agli utenti anonimi.
1. Clic **Salva** per salvare la configurazione.

### Disattiva modalità protetta {#disable-protected-mode}

Il [modalità protetta](../../forms/using/get-xdp-pdf-documents-aem.md) è attivato, per impostazione predefinita. Tienilo abilitato per gli ambienti di produzione. Puoi disabilitarlo per un ambiente di sviluppo per visualizzare in anteprima HTML5 Forms in desinger. Per disattivarla, effettua le seguenti operazioni:

1. Accedi alla console web dell’AEM come amministratore.

   * L’URL per AEM Forms su OSGi è `https://'[server]:[port]'/system/console/configMgr`
   * L’URL per AEM Forms su JEE è `https://'[server]:[port]'/lc/system/console/configMgr`

1. Apri **[!UICONTROL Configurazioni Forms per dispositivi mobili]** per la modifica.
1. Deseleziona il **[!UICONTROL Modalità protetta]** e fai clic su **[!UICONTROL Salva]**.

### Fornisci i dettagli del server AEM Forms {#provide-details-of-aem-forms-server}

1. In Designer, vai a **Strumenti** > **Opzioni**.
1. Nella finestra Opzioni, seleziona **Opzioni server** , fornire i dettagli seguenti e fare clic su **OK**.

   * **URL server**: URL del server AEM Forms.

   * **Numero porta HTTP**: porta del server AEM. Il valore predefinito è 4502.
   * **Contesto anteprima HTML:** Percorso del profilo per il rendering dei moduli XFA. Per visualizzare in anteprima il modulo in Designer vengono utilizzati i seguenti profili predefiniti. Tuttavia, puoi anche specificare il percorso di un profilo personalizzato.

      * `/content/xfaforms/profiles/default.html` (AEM Forms su OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms su JEE)
   * **Contesto Forms Manager:** Percorso contestuale in cui viene distribuita l’interfaccia utente di Forms Manager. I valori predefiniti sono:

      * `/aem/forms` (AEM Forms su OSGi)
      * `/lc/forms` (AEM Forms su JEE)

   >[!NOTE]
   >
   >Verifica che il server AEM Forms sia in esecuzione. L’anteprima HTML si connette al server CRX per *generare* un’anteprima.

   ![Opzioni di AEM Forms Designer ](assets/server_options.png)

   Opzioni di AEM Forms Designer

1. Per visualizzare l’anteprima di un modulo in HTML, fai clic su **Anteprima HTML** scheda.

   >[!NOTE]
   >
   >
   >
   >
   >    * Se la scheda Anteprima HTML è chiusa, premere F4 per aprire la scheda Anteprima HTML. Per aprire la scheda Anteprima HTML, è inoltre possibile selezionare Anteprima HTML dal menu Visualizza.
   >    * L&#39;anteprima HTML non supporta i documenti PDF, l&#39;anteprima HTML è solo per i documenti XDP.


   >[!CAUTION]
   >
   >Per testare la reale esperienza dell’utente finale, puoi anche visualizzare in anteprima i moduli in browser esterni (Google Chrome, Microsoft Edge, Mozilla Firefox e altro). Ogni browser utilizza un motore separato per il rendering di HTML, pertanto potrebbero esserci alcune differenze nel modo in cui un modulo viene visualizzato in anteprima in Designer e nel browser esterno.

## Per visualizzare in anteprima un modulo utilizzando dati di esempio {#to-preview-a-form-using-sample-data}

Designer consente di visualizzare in anteprima e verificare il modulo utilizzando dati XML di esempio. Si consiglia di verificare frequentemente il modulo con dati di esempio per verificare che venga eseguito correttamente il rendering.

Se non si dispone di dati di esempio, Designer può crearli o può crearli personalmente. (vedere [Per generare automaticamente i dati di esempio per l&#39;anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) e [Per creare dati di esempio per l&#39;anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

Il test del modulo tramite un&#39;origine dati di esempio assicura che i dati e i campi siano mappati e che le sottomaschere ripetute vengano ripetute come previsto. È possibile creare un layout di modulo bilanciato che fornisca lo spazio appropriato per ogni oggetto per visualizzare i dati uniti.

1. Seleziona **File > Proprietà modulo**.

1. Fai clic su **Anteprima** e nella casella File di dati digitare il percorso completo del file di dati di prova. È inoltre possibile utilizzare il pulsante Sfoglia per passare al file.

1. Fai clic su **OK**. Alla successiva anteprima del modulo in **Anteprima HTML** , i valori dei dati del file XML di esempio verranno visualizzati nei rispettivi oggetti.

## Anteprima dei moduli in un repository {#html-preview-of-forms-in-forms-manager}

In AEM Forms è possibile visualizzare in anteprima moduli e documenti in un repository. L’anteprima consente di conoscere esattamente l’aspetto e il comportamento dei moduli in quanto verranno utilizzati dagli utenti finali.
