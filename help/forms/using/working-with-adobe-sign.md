---
title: Utilizzo di Adobe Sign in un modulo adattivo
seo-title: Utilizzo di Adobe Sign in un modulo adattivo
description: È possibile abilitare i flussi di lavoro di firma elettronica (Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multipla e per firmare elettronicamente i moduli dai dispositivi mobili.
seo-description: È possibile abilitare i flussi di lavoro di firma elettronica (Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multipla e per firmare elettronicamente i moduli dai dispositivi mobili.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: 14975f409a0e17183b3da6bdc5a42c8073080108

---


# Utilizzo di Adobe Sign in un modulo adattivo{#using-adobe-sign-in-an-adaptive-form}

Adobe Sign consente flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per attività legali, di vendita, di retribuzione, di gestione delle risorse umane e per altre aree.

In uno scenario di moduli adattivi e Adobe Sign tipico, l&#39;utente compila un modulo adattivo da richiedere per un servizio. Ad esempio, una richiesta di mutuo e di carta di credito richiede firme legali da parte di tutti i mutuatari e co-richiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, è possibile integrare Adobe Sign con AEM Forms. Altri esempi sono:

* Chiude le offerte da qualsiasi dispositivo con procedure di proposta, preventivi e contratti completamente automatizzate.
* Completate più rapidamente i processi delle risorse umane e date ai vostri dipendenti le esperienze digitali.
* Riduzione dei tempi di gestione dei contratti e integrazione dei fornitori più rapida.
* Crea flussi di lavoro digitali per automatizzare i processi comuni.

L&#39;integrazione di Adobe Sign con AEM Forms supporta:

* Flussi di lavoro di firma singoli e multipli
* Flussi di lavoro di firma sequenziali e simultanei
* Esperienze di firma in-form e out-of-form
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con il flusso di lavoro di AEM Forms)
* Autenticazione tramite una knowledge base, telefoni e profili social

## Prerequisiti {#prerequisites}

Prima di utilizzare Adobe Sign in un modulo adattivo:

* Verifica che il servizio cloud AEM Forms sia configurato per l&#39;utilizzo di Adobe Sign. Per informazioni dettagliate, consultate [Integrazione di Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Tenete pronto l&#39;elenco dei firmatari. È necessario almeno un indirizzo e-mail per ogni firmatario.

## Configurare Adobe Sign per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Per configurare Adobe Sign per un modulo adattivo, procedere come segue:

1. [Modifica delle proprietà dei moduli adattivi per Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Aggiunta di campi Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Selezione di Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Aggiunta di firmatari di Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Dettagli firmatario](assets/signer_details_new.png)

### Modifica delle proprietà dei moduli adattivi per Adobe Sign {#enableadobesign}

Configurare le proprietà dei moduli adattivi per Adobe Sign per un modulo adattivo esistente o nuovo.

[La creazione di un modulo adattivo per Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) descrive i passaggi necessari per creare un modulo adattivo di base. Vedere [Creazione di un modulo](../../forms/using/creating-adaptive-form.md) adattivo per altre opzioni disponibili durante la creazione di un modulo adattivo.

#### Creare un modulo adattivo per Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo abilitato per i segni, effettuare le seguenti operazioni:

1. Passa ad **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Toccare **[!UICONTROL Crea]** e selezionare Modulo **** adattivo. Viene visualizzato un elenco di modelli. Selezionate il modello e toccate **[!UICONTROL Avanti]**.
1. Nella scheda **[!UICONTROL Base]** :

   1. Specificare **Nome** e **Titolo** per il modulo adattivo.

   1. Selezionare il contenitore [di](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) configurazione creato durante la configurazione di Adobe Sign con AEM Forms.

1. Nella scheda Modello **** modulo, selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello]** del documento di registrazione e selezionare un modello del documento di registrazione. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzeranno solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento record]** . Se si utilizza un modulo adattivo abilitato per l&#39;opzione Documento record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Toccate **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato per la firma, che può essere utilizzato per aggiungere campi Adobe Sign.

#### Modificare un modulo adattivo per Adobe Sign {#editafsign}

Effettuare le seguenti operazioni per utilizzare Adobe Sign in un modulo adattivo esistente:

1. Passa ad **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Selezionare il modulo adattivo e toccare **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]** , selezionare il contenitore [di](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) configurazione creato durante la configurazione di Adobe Sign con AEM Forms.
1. Nella scheda Modalità **** modulo, selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello]** del documento di registrazione e selezionare un modello del documento di registrazione. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzeranno solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento record]** . Se si utilizza un modulo adattivo abilitato per l&#39;opzione Documento record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Toccate **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per Adobe Sign.

### Aggiunta di campi Adobe Sign a un modulo adattivo {#addadobesignfieldstoanadaptiveform}

Adobe Sign dispone di diversi campi che possono essere inseriti in un modulo adattivo. Questi campi accettano vari tipi di dati quali firme, iniziali, società o titoli e consentono di raccogliere informazioni aggiuntive durante la firma, insieme alle firme. È possibile utilizzare il componente Adobe Sign Block per posizionare i campi di Adobe Sign in diverse aree del modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare le varie opzioni relative a tali campi, procedere come segue:

1. Trascinare il componente **Adobe Sign Block** dal browser Componenti al modulo adattivo. Il componente Adobe Sign Block contiene tutti i campi Adobe Sign supportati. Per impostazione predefinita, al modulo adattivo viene aggiunto un campo **Firma** .

   ![Blocco di firma](assets/sign_block_new.png)

   Per impostazione predefinita, Adobe Sign Block non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti firmati. Puoi modificare la visibilità di Adobe Sign Block dalle proprietà del componente Adobe Sign Block.

   >[!NOTE]
   >
   >    * L&#39;utilizzo del blocco Adobe Sign non è obbligatorio per utilizzare Adobe Sign in un modulo adattivo. Se non si utilizza il blocco Adobe Sign e non si aggiungono campi per i firmatari, il campo firma predefinito viene visualizzato nella parte inferiore dei documenti di firma.
   >    * Utilizzare il blocco Adobe Sign solo per i moduli adattivi che generano automaticamente il documento record. Se si utilizza un XDP personalizzato per generare un modulo adattivo basato su un documento o un modello di modulo, il blocco Adobe Sign non è richiesto.


1. Selezionare il componente **Adobe Sign Block** e toccare l&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Visualizza le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **** A. Selezionare e aggiungere campi Adobe Sign. **** B. Espandi il blocco Adobe Sign nella visualizzazione a schermo intero

1. Tocca l’icona del campo **** Adobe Sign ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Visualizza le opzioni per selezionare e aggiungere campi Adobe Sign.

   Espandi il campo a discesa **Tipo** per selezionare un campo Adobe Sign e tocca l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per aggiungere il campo selezionato al blocco Adobe Sign. Il campo a discesa **Tipo** include i tipi di campo Firma, Informazioni firmatario e Dati. Integrazione di Adobe Sign con i campi di supporto di AEM Forms elencati solo nella casella a discesa Tipo. Per informazioni dettagliate sui campi di Adobe Sign, consultare la documentazione [di](https://helpx.adobe.com/sign/help/field-types.html)Adobe Sign.

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio specificare un nome univoco per un campo. È inoltre possibile selezionare l&#39;opzione desiderata per contrassegnare un campo obbligatorio. Oltre a **Nome** e **** Requisito, alcuni campi di Adobe Sign dispongono di più opzioni. Ad esempio, maschera e linea multipla. Inoltre, specifica un nome univoco per ciascun campo Adobe Sign, a prescindere dal fatto che i campi risiedano nello stesso o in blocchi Adobe Sign diversi.

   Se si seleziona Firma **** digitale dall&#39;elenco a discesa, è possibile applicare le firme digitali al modulo adattivo:

   * Online mediante l&#39;uso di firme cloud per firmare con un ID [](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) digitale ospitato da un provider di servizi attendibili.
   * Localmente, scaricando il documento con Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilitare Adobe Sign per un modulo adattivo {#enableadobsignforanadaptiveform}

Adobe Sign non è abilitato per i moduli adattivi. Per attivarla, effettuate le seguenti operazioni:

1. Nel browser Contenuto, toccate Contenitore **** modulo e toccate l&#39;icona **Configura** ![configurazione](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere la struttura **Firma** elettronica e selezionare l&#39;opzione **Abilita Adobe Sign** . Abilita Adobe Sign per un modulo adattivo.

### Seleziona il servizio Adobe Sign Cloud e l&#39;ordine di firma {#selectadobesigncloudserviceforanadaptiveform}

È possibile configurare più servizi Adobe Sign per un&#39;istanza di AEM Forms. È consigliabile disporre di un set di servizi distinto per ciascuna funzione (Risorse umane, Finanza e altro ancora). Semplifica il tracciamento e la generazione di rapporti dei documenti firmati. Ad esempio, una banca ha più reparti. Puoi disporre di una configurazione separata per ciascun reparto per migliorare il monitoraggio dei documenti.

Un documento può anche contenere più firmatari. Ad esempio, una domanda con carta di credito può avere più candidati. Una banca richiede le firme di tutti i richiedenti prima di avviare l&#39;elaborazione della domanda. Per gli scenari con più firmatari, è possibile firmare il documento in ordine sequenziale o simultaneo.

Per selezionare un servizio cloud e l&#39;ordine di firma, effettuate le seguenti operazioni:

![servizio cloud](assets/cloud-service.png)

1. Nel browser Contenuto, toccate Contenitore **** modulo e toccate l&#39;icona **Configura** ![configurazione](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere la struttura **Firma** elettronica e selezionare l&#39;opzione **Abilita Adobe Sign** . Abilita Adobe Sign per un modulo adattivo.
1. Seleziona un servizio cloud dall&#39;elenco di servizi cloud Adobe Sign già configurato.

   Se l’elenco dei servizi **cloud** Adobe Sign è vuoto, per configurare il servizio segui l’articolo [Configura Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) .

1. Selezionare l&#39;ordine di firma dalla finestra di dialogo **Firma** dei firmatari. I cantanti Adobe Sign possono firmare un modulo adattivo in **sequenza** , uno dopo l’altro firmatario o **simultaneamente** , in qualsiasi ordine.

   In ordine sequenziale, un firmatario riceve il modulo per la firma, alla volta. Dopo che un firmatario ha completato la firma del documento, il modulo viene inviato al firmatario successivo e così via.

   In ordine simultaneo, più firmatari possono firmare un modulo alla volta.

1. [Aggiungete i firmatari a un modulo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) adattivo e toccate l&#39;icona Fine [aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.


### Aggiunta di firmatari a un modulo adattivo {#addsignerstoanadaptiveform}

Per un modulo adattivo è possibile avere uno o più firmatari. Quando aggiungi un firmatario, puoi anche configurare i dettagli di autenticazione per il firmatario. È inoltre possibile selezionare se il compilatore e il cantante sono la stessa persona. Per aggiungere e fornire diversi dettagli su un firmatario, effettuate le seguenti operazioni:

1. Nel browser Contenuto, toccate Contenitore **** modulo e toccate l&#39;icona **Configura** ![configurazione](assets/configure.png) . Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere la struttura **Firma** elettronica e selezionare l&#39;opzione **Abilita Adobe Sign** . Abilita Adobe Sign per un modulo adattivo.
1. Tocca **Aggiungi firmatario** in Configurazione **** firmatario. Aggiunge un firmatario al modulo adattivo. È possibile aggiungere più firmatari di Adobe Sign a un modulo adattivo.
1. ![dettagli telefono](assets/phone-details.png)

   Fate clic sull&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) per specificare le informazioni seguenti relative al firmatario:

   * **** Titolo: Specificate un titolo per identificare in modo univoco un firmatario.

   * **** Il firmatario e la persona che compila il modulo sono identici?: Selezionare **Sì**, se il compilatore e il primo firmatario sono la stessa persona. Se l’opzione è impostata su **No,** non utilizzare il componente passo firma nel modulo adattivo. Se il modulo contiene un componente Passaggio firma, il campo viene automaticamente impostato su Sì.

   * **** Indirizzo e-mail del firmatario: Specifica l&#39;indirizzo e-mail del firmatario. Il firmatario riceve i documenti/moduli firmati all&#39;indirizzo e-mail specificato. Potete scegliere di utilizzare un indirizzo e-mail fornito in un campo modulo, nel profilo utente AEM dell&#39;utente che ha effettuato l&#39;accesso, oppure immettere manualmente un indirizzo e-mail. Si tratta di un passo obbligatorio. Assicurati che l&#39;indirizzo e-mail del primo firmatario o dell&#39;unico firmatario (nel caso di un singolo firmatario) non sia identico all&#39;account Adobe Sign utilizzato per configurare i servizi cloud AEM.

   * **** Metodo di autenticazione del firmatario: Specificare il metodo di autenticazione dell&#39;utente prima di aprire un modulo per la firma. Potete scegliere tra l&#39;autenticazione basata su telefono, knowledge base e social identity.
   >[!NOTE]
   >
   >    * Per impostazione predefinita, l&#39;autenticazione basata sull&#39;identità social fornisce un&#39;opzione per l&#39;autenticazione tramite Facebook, Google e LinkedIn. È possibile contattare il supporto di Adobe Sign per abilitare altri provider di autenticazione social.


   * **** Campi Adobe Sign da compilare o firmare: Selezionare i campi di Adobe Sign per il firmatario. Un modulo adattivo può contenere più campi Adobe Sign. Puoi scegliere di abilitare campi specifici per un firmatario. Il campo visualizza tutti i blocchi Adobe Sign disponibili. Quando si seleziona un blocco, vengono selezionati tutti i campi del blocco. È possibile utilizzare l&#39;icona X per deselezionare un campo.
   ![signer-details](assets/signer-details.png)

   L&#39;immagine precedente include due esempi di blocchi Adobe Sign: Informazioni personali e informazioni sull&#39;ufficio

   Toccate l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) . Il firmatario viene aggiunto e configurato.

### Selezionare Invia azione per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo aver aggiunto i campi Adobe Sign a un modulo adattivo, abilitare Adobe Sign dal contenitore del modulo, selezionare Adobe Sign Cloud Service e aggiungere i firmatari Adobe Sign, selezionare un&#39;azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio dei moduli adattivi, vedere [Configurazione dell&#39;azione](../../forms/using/configuring-submit-actions.md)di invio.

Inoltre, un modulo adattivo abilitato per Adobe Sign viene inviato solo dopo che tutti i firmatari avranno firmato il modulo. È possibile trovare il modulo firmato parzialmente nella sezione Firma in sospeso del portale dei moduli. Il servizio di configurazione di Adobe Sign consente di effettuare il polling del server Adobe Sign a intervalli [](../../forms/using/adobe-sign-integration-adaptive-forms.md) regolari per verificare lo stato delle firme. Se tutti i firmatari completano la firma del modulo, viene avviato il servizio di invio e il modulo viene inviato. Se si utilizza un&#39;azione di invio personalizzata e il modulo utilizza Adobe Sign, aggiornare l&#39;azione di invio personalizzata per utilizzare il servizio di invio azioni.

>[!NOTE]
>
>I dati del modulo adattivo vengono memorizzati temporaneamente in Forms Portal. Si consiglia di utilizzare la memorizzazione [personalizzata per Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). Garantisce che i dati PII (informazioni personali) non vengano memorizzati sui server AEM.

La firma del modulo è pronta. È possibile visualizzare l&#39;anteprima del modulo per verificare l&#39;esperienza di firma. Nel modulo pubblicato, i campi Blocco di Adobe Sign vengono visualizzati quando un firmatario riceve il modulo per la firma tramite e-mail. Questa esperienza è nota anche come esperienza di firma fuori forma. È inoltre possibile configurare un&#39;esperienza di firma in-form per il primo firmatario, per i passaggi dettagliati, vedere [Creazione di un&#39;esperienza](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)di firma in-form.

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali o le firme remote basate su cloud sono una nuova generazione di firme digitali utilizzabili tra computer desktop, dispositivi mobili e Web. e soddisfare i massimi livelli di conformità e garanzia per l&#39;autenticazione dei firmatari. È possibile firmare un modulo adattivo con firme digitali basate su cloud.

Dopo aver [modificato le proprietà del modulo adattivo per Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobesign), effettuare le seguenti operazioni per aggiungere il campo firma cloud a un modulo adattivo:

1. Trascinare il componente **Adobe Sign Block** dal browser Componenti al modulo adattivo. Il componente Adobe Sign Block contiene tutti i campi Adobe Sign supportati. Per impostazione predefinita, al modulo adattivo viene aggiunto un campo **Firma** .

   ![Blocco di firma](assets/sign-block-new.png)

1. Selezionare il componente **Adobe Sign Block** e toccare l&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Visualizza le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **** A. Selezionare e aggiungere campi Adobe Sign. **** B. Espandi il blocco Adobe Sign nella visualizzazione a schermo intero

1. Tocca l’icona del campo **** Adobe Sign ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Visualizza le opzioni per selezionare e aggiungere campi Adobe Sign.

   Espandere il campo a discesa **Tipo** per selezionare Firma **** digitale e toccare l&#39;icona Fine per aggiungere il campo selezionato al blocco Adobe Sign.

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio specificare un nome univoco per un campo.

   Per applicare le firme digitali al modulo adattivo, utilizzare:

   * Firme cloud: Effettuate l&#39;accesso con un ID [](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) digitale ospitato da un provider di servizi attendibili.
   * Adobe Acrobat o Reader: Scaricate e aprite il documento con Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.
   Dopo aver aggiunto il campo firma cloud al modulo adattivo, effettuare le seguenti operazioni per completare il processo di configurazione:

   * [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Selezione di Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiunta di firmatari di Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Creazione di un&#39;esperienza di firma in-form {#create-in-form-signing-experience}

Un utente può inoltre firmare un modulo adattivo durante la compilazione del modulo. Questa esperienza è nota anche come esperienza di firma in-form. L&#39;esperienza di firma in-form è disponibile solo per il primo firmatario in un ambiente con più firmatari. Per creare un&#39;esperienza di firma all&#39;interno del modulo per un modulo adattivo, procedere come segue:

1. [Aggiungere e configurare il componente](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)Passaggio firma.
1. [Aggiungete il componente](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)Passaggio di riepilogo.

![Esperienza di firma in-form](assets/in_form_signing_experience_new.png)

### Aggiunta e configurazione del componente Passaggio firma {#add-and-configure-the-signature-step-component}

Utilizzare il componente Passaggio firma per specificare un&#39;area in cui firmare elettronicamente il modulo compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF firmabile del modulo compilato. Il componente Passaggio firma occupa la larghezza totale disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio firma.

Per configurare il componente Passaggio firma, effettuare le operazioni seguenti:

1. Trascinare il componente **Passaggio** firma dal browser Componenti al modulo.
1. Seleziona il componente Fase firma appena aggiunto e tocca l’icona **Configura** ![configurazione](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà dei passaggi firma. Configurare le seguenti proprietà:

   * **Nome** elemento: Specificate il nome del componente.

   * **** Titolo: Specificate il titolo univoco del componente.
   * **** Messaggio modello: Specificare il messaggio da visualizzare durante il caricamento del PDF della firma. I servizi Adobe Sign richiedono del tempo per preparare e caricare il PDF della firma.
   * **** Servizio di firma: Selezionare l&#39;opzione **Adobe Sign** .

   * **Utilizza componente** E-sign legacy: Se utilizzate il rispettivo modulo adattivo in [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), nell’app AEM Forms o nel modulo adattivo sottostante è presente un componente di firma elettronica legacy, selezionate l’opzione **Usa componente** di firma elettronica legacy.

   * **Configurazione**: Selezionare una configurazione (Adobe Sign Cloud Service). La casella a discesa è disponibile solo se è abilitata l&#39;opzione **Usa componente** e-sign legacy.
   Toccate l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   ![Passaggio firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   >    * Quando si trascina il componente Passaggio **** firma sul modulo, il firmatario **[!UICONTROL e la persona che compila il modulosono gli stessi?]** viene impostata automaticamente su **Sì**. È necessario mantenere il funzionamento del modulo.
      >
      >    
   * I moduli adattivi abilitati per Adobe Sign non supportano l&#39;utilizzo del pulsante Invia nella sezione o nel pannello tramite il componente Passaggio firma. È possibile aggiungere un passaggio di riepilogo dopo che il passaggio Firma per l&#39;invio manuale o dopo che l&#39;intervallo impostato è stato impostato tramite il servizio [di configurazione di](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)Adobe Sign è stato attivato.


### Configurare la pagina di ringraziamento o il componente fase di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

Il componente Passo **** riepilogo invia automaticamente il modulo, compila le informazioni all’interno della pagina Riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Ottiene anche le informazioni richieste nella mappa di ritorno. Il componente Passo di riepilogo occupa la larghezza totale disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passo di riepilogo.

Ora, l&#39;esperienza di firma del modulo in è pronta. È possibile visualizzare l&#39;anteprima del modulo per verificare l&#39;esperienza di firma.

## Frequently asked questions {#frequently-asked-questions}

**** Ans: No, AEM Forms non supporta l&#39;uso di un modulo adattivo che incorpora un modulo adattivo abilitato per Adobe Sign per la firma

**** Ans: Il modulo adattivo creato utilizzando il modello avanzato è configurato per l&#39;utilizzo di Adobe Sign. Per risolvere l&#39;errore, creare e selezionare una configurazione cloud Adobe Sign e configurare un firmatario Adobe Sign per il modulo adattivo.

**** Ans: Sì, è possibile utilizzare i tag di testo in un componente di testo per aggiungere campi Adobe Sign a un modulo adattivo abilitato per il documento [di registrazione](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (solo per il documento di registrazione generato automaticamente). Per ulteriori informazioni sulla procedura e sulle regole per creare un tag di testo, vedere Documentazione [di](https://helpx.adobe.com/sign/help/text-tags.html)Adobe Sign. Inoltre, i moduli adattivi hanno un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi supportati da [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) .

**** Ans: È possibile utilizzare entrambi i componenti contemporaneamente in un modulo. Di seguito sono riportati alcuni suggerimenti per l&#39;utilizzo di questi componenti:

**** Blocco Adobe Sign: È possibile utilizzare Adobe Sign Block per aggiungere campi Adobe Sign ovunque nel modulo adattivo. Consente inoltre di assegnare campi specifici ai firmatari. Quando un modulo adattivo viene visualizzato in anteprima o pubblicato, per impostazione predefinita Adobe Sign Block non è visibile. Questi blocchi sono abilitati solo nel documento di firma. Nel documento di firma sono abilitati solo i campi assegnati a un firmatario. Il blocco Adobe Sign può essere utilizzato con il primo e il successivo firmatario.

**** Componente fase firma: È possibile utilizzare il componente Fase firma per creare un&#39;esperienza di firma all&#39;interno del modulo. Consente di firmare solo il primo firmatario durante la compilazione del modulo. Durante il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF del modulo da firmare. Si tratta generalmente dell’ultima o penultima sezione seguita dal componente di riepilogo di un modulo.

## Risolvere i problemi {#troubleshoot}

### Errori di accordo di Adobe Sign {#adobe-sign-agreement-failures}

**Problema**: se il servizio Adobe Sign è configurato per un modulo adattivo, il servizio non riesce a creare un accordo Adobe Sign per il modulo adattivo sottostante.

**Risoluzione**

* Controlla la [configurazione del servizio](../../forms/using/adobe-sign-integration-adaptive-forms.md) cloud Adobe Sign utilizzato nel modulo adattivo.
* Verifica che l’applicazione API sul server Adobe Sign utilizzata per configurare il servizio Adobe Sign Cloud disponga delle autorizzazioni necessarie.
* Se utilizzi più servizi Adobe Sign Cloud, imposta l’URL **[!UICONTROL di]** autenticazione di tutti i servizi sullo stesso **[!UICONTROL Adobe Sign Share]**.

* Utilizza indirizzi e-mail separati per configurare l’account Adobe Sign e per il primo firmatario e il singolo firmatario. L&#39;indirizzo e-mail del primo firmatario o dell&#39;unico firmatario (nel caso del singolo firmatario) non può essere identico all&#39;account Adobe Sign utilizzato per configurare i servizi cloud AEM.

## Related Articles {#related-articles}

* [Integrazione di Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Utilizzo di Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)

* [Utilizzo di Adobe Sign con AEM Forms (video)
   ](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
