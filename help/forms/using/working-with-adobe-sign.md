---
title: Utilizzo di  Adobe Sign in un modulo adattivo
seo-title: Utilizzo di  Adobe Sign in un modulo adattivo
description: È possibile abilitare i flussi di lavoro di firma elettronica ( Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multi-firma e firmare elettronicamente i moduli dai dispositivi mobili.
seo-description: È possibile abilitare i flussi di lavoro di firma elettronica ( Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multi-firma e firmare elettronicamente i moduli dai dispositivi mobili.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: 4abfda568fc15f225510c79635387142aefddc72
workflow-type: tm+mt
source-wordcount: '3949'
ht-degree: 0%

---


# Utilizzo  Adobe Sign in un modulo adattivo{#using-adobe-sign-in-an-adaptive-form}

 Adobe Sign consente flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per attività legali, di vendita, di retribuzione, di gestione delle risorse umane e per altre aree.

In uno scenario di moduli  Adobe Sign e adattivi tipico, un utente compila un modulo adattivo da richiedere per un servizio. Ad esempio, una richiesta di mutuo e di carta di credito richiede firme legali da parte di tutti i mutuatari e co-richiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, puoi integrare  Adobe Sign con  AEM Forms. Altri esempi sono: potete utilizzare  Adobe Sign per:

* Chiude le offerte da qualsiasi dispositivo con procedure di proposta, preventivi e contratti completamente automatizzate.
* Completate più rapidamente i processi delle risorse umane e date ai vostri dipendenti le esperienze digitali.
* Riduzione dei tempi di gestione dei contratti e integrazione dei fornitori più rapida.
* Crea flussi di lavoro digitali per automatizzare i processi comuni.

 integrazione Adobe Sign con  AEM Forms supporta:

* Flussi di lavoro di firma singoli e multipli
* Flussi di lavoro di firma sequenziali e simultanei
* Esperienze di firma in-form e out-of-form
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con  flusso di lavoro AEM Forms)
* Autenticazione tramite una knowledge base, telefoni e profili social

## Prerequisiti {#prerequisites}

Prima di utilizzare  Adobe Sign in un modulo adattivo:

* Assicurati  che il servizio cloud AEM Forms sia configurato per l&#39;utilizzo  Adobe Sign. Per informazioni dettagliate, vedere [Integrare  Adobe Sign con  AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Tenete a portata di mano l&#39;elenco dei firmatari. È necessario almeno un indirizzo e-mail per ogni firmatario.

## Configurare  Adobe Sign per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Per configurare  Adobe Sign per un modulo adattivo, effettuate le seguenti operazioni:

1. [Modificare le proprietà dei moduli adattivi per  Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Aggiunta  campi Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Abilitare  Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Selezionare  Cloud Service Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Aggiunta  firmatari Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Dettagli firmatario](assets/signer_details_new.png)

### Modificare le proprietà dei moduli adattivi per  Adobe Sign {#enableadobesign}

Configurare le proprietà del modulo adattivo per  Adobe Sign per un modulo adattivo esistente o nuovo.

[Creare un modulo adattivo per  ](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) Firma Adobe descrive i passaggi necessari per creare un modulo adattivo di base. Per le altre opzioni disponibili durante la creazione di un modulo adattivo, vedere [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).

#### Creare un modulo adattivo per  Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo abilitato per i segni, effettuare le seguenti operazioni:

1. Andate su **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toccate **[!UICONTROL Crea]** e selezionate **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Selezionate il modello e toccate **[!UICONTROL Next]**.
1. Nella scheda **[!UICONTROL Base]**:

   1. Specificare **Name** e **Title** per il modulo adattivo.

   1. Selezionare il [contenitore di configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione  Adobe Sign con  AEM Forms.

      >[!NOTE]
      >
      >Nell&#39;elenco a discesa **[!UICONTROL Cloud Service Adobe Sign]** vengono visualizzati i servizi cloud configurati nel contenitore di configurazione selezionato in questo campo. L&#39;elenco a discesa **[!UICONTROL Cloud Service Adobe Sign]** è disponibile nella sezione **[!UICONTROL Firma elettronica]** delle proprietà del modulo adattivo quando si seleziona l&#39;opzione **[!UICONTROL Abilita  Adobe Sign]**.

1. Nella scheda **[!UICONTROL Modello modulo]**, selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello del documento record]** e selezionare un modello del documento di registrazione. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzeranno solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento record]**. Se si utilizza un modulo adattivo abilitato per l&#39;opzione Documento record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Toccate **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato per la firma, che può essere utilizzato per aggiungere  campi Adobe Sign.

#### Modificare un modulo adattivo per  Adobe Sign {#editafsign}

Effettuate le seguenti operazioni per utilizzare  Adobe Sign in un modulo adattivo esistente:

1. Andate su **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Selezionare il modulo adattivo e toccare **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]**, selezionare il contenitore di configurazione [creato durante la configurazione  Adobe Sign con  AEM Forms.](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)
1. Nella scheda **[!UICONTROL Modalità modulo]**, selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello del documento record]** e selezionare un modello del documento di registrazione. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzeranno solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento record]**. Se si utilizza un modulo adattivo abilitato per l&#39;opzione Documento record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Toccate **[!UICONTROL Save and Close]** (Salva e chiudi). Il modulo adattivo è abilitato per  Adobe Sign.

### Aggiungere  campi Adobe Sign a un modulo adattivo {#addadobesignfieldstoanadaptiveform}

 Adobe Sign dispone di diversi campi che possono essere inseriti in un modulo adattivo. Questi campi accettano vari tipi di dati quali firme, iniziali, società o titoli e consentono di raccogliere informazioni aggiuntive durante la firma, insieme alle firme. È possibile utilizzare il componente  Blocco Adobe Sign per posizionare  campi Adobe Sign in diverse aree di un modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare le varie opzioni relative a tali campi, procedere come segue:

1. Trascinare il componente **Adobe Sign Block** dal browser Componenti al modulo adattivo. Il  componente Adobe Sign Block dispone di tutti i campi Adobe Sign  supportati. Per impostazione predefinita, aggiunge al modulo adattivo un campo **Signature**.

   ![Blocco di firma](assets/sign_block_new.png)

   Per impostazione predefinita, il  blocco Adobe Sign non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti firmati. È possibile modificare la visibilità di  blocco Adobe Sign dalle proprietà del componente  blocco Adobe Sign.

   >[!NOTE]
   >
   >    * L&#39;utilizzo  blocco Adobe Sign non è obbligatorio per utilizzare  Adobe Sign in un modulo adattivo. Se non si utilizza  blocco Adobe Sign e non si aggiungono campi per i firmatari, il campo firma predefinito viene visualizzato nella parte inferiore dei documenti di firma.
   >    * Utilizzare  blocco Adobe Sign solo per i moduli adattivi che generano automaticamente Document of Record. Se si utilizza un XDP personalizzato per la generazione di un modulo adattivo basato su un documento o un modello di modulo,  blocco Adobe Sign non è richiesto.


1. Selezionare il componente **blocco Adobe Sign** e toccare l&#39;icona **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png). Visualizza le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Selezionare e aggiungere  campi Adobe Sign. **B.** Espandere il blocco Adobe Sign  a schermo intero

1. Toccate l&#39;icona **Adobe Sign Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Visualizza le opzioni per selezionare e aggiungere  campi Adobe Sign.

   Espandere il campo a discesa **Tipo** per selezionare un campo Adobe Sign  e toccare l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per aggiungere il campo selezionato  blocco Adobe Sign. Il campo a discesa **Type** include i tipi di campo Firma, Informazioni sul firmatario e Dati.  integrazione Adobe Sign con  campi di supporto AEM Forms elencati solo nella casella a discesa Tipo. Per informazioni dettagliate  campi Adobe Sign, consultare la [ documentazione Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio specificare un nome univoco per un campo. È inoltre possibile selezionare l&#39;opzione desiderata per contrassegnare un campo obbligatorio. Oltre all&#39;opzione **Name** e **Required**, alcuni  campo Adobe Sign dispongono di più opzioni. Ad esempio, maschera e linea multipla. Inoltre, specificate un nome univoco per ciascun campo Adobe Sign  se i campi risiedono in blocchi Adobe Sign  uguali o diversi.

   Se si seleziona **Firma digitale** dall&#39;elenco a discesa, è possibile applicare firme digitali al modulo adattivo:

   * Online mediante l&#39;uso di firme cloud per firmare con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi di trust.
   * Localmente, scaricando il documento con  Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilitare  Adobe Sign per un modulo adattivo {#enableadobsignforanadaptiveform}

In questo caso,  Adobe Sign non è abilitato per un modulo adattivo. Per attivarla, effettuate le seguenti operazioni:

1. Nel browser Contenuto, toccate **Contenitore modulo**, quindi toccate l&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere l&#39;opzione **Firma elettronica** e selezionare l&#39;opzione **Abilita  Adobe Sign**. Abilita  Adobe Sign per un modulo adattivo.

### Selezionare  Cloud Service Adobe Sign e ordine di firma {#selectadobesigncloudserviceforanadaptiveform}

Potete configurare più servizi Adobe Sign  per un’istanza di  AEM Forms. È consigliabile disporre di un set di servizi distinto per ciascuna funzione (Risorse umane, Finanza e altro ancora). Semplifica il tracciamento e la generazione di rapporti dei documenti firmati. Ad esempio, una banca ha più reparti. Puoi disporre di una configurazione separata per ciascun reparto per migliorare il tracciamento dei documenti.

Un documento può anche contenere più firmatari. Ad esempio, una domanda con carta di credito può avere più candidati. Una banca richiede le firme di tutti i richiedenti prima di avviare l&#39;elaborazione della domanda. Per gli scenari con più firmatari, è possibile firmare il documento in ordine sequenziale o simultaneo.

Per selezionare un servizio cloud e l&#39;ordine di firma, effettuate le seguenti operazioni:

![servizio cloud](assets/cloud-service.png)

1. Nel browser Contenuto, toccate **Contenitore modulo**, quindi toccate l&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere l&#39;opzione **Firma elettronica** e selezionare l&#39;opzione **Abilita  Adobe Sign**. Abilita  Adobe Sign per un modulo adattivo.
1. Selezionate un servizio cloud dall&#39;elenco di Cloud Services Adobe Sign già configurati.

   Se l&#39;elenco **Cloud Service Adobe Sign** è vuoto, seguire l&#39;articolo [Configura  Adobe Sign con  AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) per configurare il servizio.

   Il menu a discesa elenca i servizi cloud presenti nella cartella `global` in Strumenti > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Inoltre, nel menu a discesa sono elencati anche i servizi cloud presenti nella cartella selezionata nel campo **[!UICONTROL Contenitore di configurazione]** quando si crea un modulo adattivo.

1. Selezionare l&#39;ordine di firma dalla finestra di dialogo **I firmatari possono firmare**.  cantanti Adobe Sign possono firmare un modulo adattivo **in sequenza**, uno dopo l&#39;altro firmatario o **Simultaneamente**, in qualsiasi ordine.

   In ordine sequenziale, un firmatario riceve il modulo per la firma, alla volta. Dopo che un firmatario ha completato la firma del documento, il modulo viene inviato al firmatario successivo e così via.

   In ordine simultaneo, più firmatari possono firmare un modulo alla volta.

1. [Aggiungete i firmatari a un ](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) modulo adattivo e toccate l&#39;icona Fine  [aem_6_3_forms_](assets/aem_6_3_forms_save.png) saveicon per salvare le modifiche.


### Aggiunta di firmatari a un modulo adattivo {#addsignerstoanadaptiveform}

Per un modulo adattivo è possibile avere un solo firmatario o più firmatari. Quando aggiungi un firmatario, puoi anche configurare i dettagli di autenticazione per il firmatario. È inoltre possibile selezionare se il compilatore e il cantante sono la stessa persona. Per aggiungere e fornire diversi dettagli su un firmatario, effettuate le seguenti operazioni:

1. Nel browser Contenuto, toccate **Contenitore modulo**, quindi toccate l&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere l&#39;opzione **Firma elettronica** e selezionare l&#39;opzione **Abilita  Adobe Sign**. Abilita  Adobe Sign per un modulo adattivo.
1. Toccare **Aggiungi firmatario** in **Configurazione del firmatario**. Aggiunge un firmatario al modulo adattivo. È possibile aggiungere più  firmatari Adobe Sign a un modulo adattivo.
1. ![dettagli telefonici](assets/phone-details.png)

   Fare clic sull&#39;icona **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png) per specificare le informazioni seguenti relative al firmatario:

   * **Titolo:** specificate un titolo per identificare in modo univoco un firmatario.

   * **Il firmatario e la persona che compila il modulo sono identici?:** Selezionare  **Sì**, se il compilatore e il primo firmatario sono la stessa persona. Se l&#39;opzione è impostata su **No,**, non utilizzare il componente per il passaggio della firma nel modulo adattivo. Se il modulo contiene un componente Passaggio firma, il campo viene automaticamente impostato su Sì.

   * **Indirizzo e-mail del firmatario:** specifica l’indirizzo e-mail del firmatario. Il firmatario riceve i documenti/moduli firmati all&#39;indirizzo e-mail specificato. È possibile scegliere di utilizzare un indirizzo e-mail fornito in un campo modulo, AEM profilo utente dell&#39;utente che ha effettuato l&#39;accesso o immettere manualmente un indirizzo e-mail. Si tratta di un passo obbligatorio. Assicurati che l&#39;indirizzo e-mail del primo firmatario o dell&#39;unico firmatario (nel caso di un singolo firmatario) non sia identico a  account Adobe Sign utilizzato per configurare i servizi cloud AEM.

   * **Metodo di autenticazione del firmatario:** specificare il metodo per l&#39;autenticazione di un utente prima di aprire un modulo per la firma. Potete scegliere tra l&#39;autenticazione basata su telefono, knowledge base e social identity.
   >[!NOTE]
   >
   >    * Per impostazione predefinita, l&#39;autenticazione basata sull&#39;identità social fornisce un&#39;opzione per l&#39;autenticazione tramite Facebook, Google e LinkedIn. Potete contattare  supporto Adobe Sign per abilitare altri provider di autenticazione social.


   * **campi Adobe Sign da compilare o firmare:** Selezionare  campi Adobe Sign per il firmatario. Un modulo adattivo può contenere più campi  Adobe Sign. Puoi scegliere di abilitare campi specifici per un firmatario. Nel campo vengono visualizzati tutti i blocchi  Adobe Sign disponibili. Quando si seleziona un blocco, vengono selezionati tutti i campi del blocco. È possibile utilizzare l&#39;icona X per deselezionare un campo.

   ![signer-details](assets/signer-details.png)

   L&#39;immagine precedente ha due esempi  blocchi Adobe Sign: Informazioni personali e informazioni sull&#39;ufficio

   Toccate l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Il firmatario viene aggiunto e configurato.

### Selezionare Invia azione per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo aver aggiunto  campi Adobe Sign a un modulo adattivo, abilitare  Adobe Sign dal contenitore del modulo, selezionare  Cloud Service Adobe Sign e aggiungere  firmatari Adobe Sign, selezionare un&#39;azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio dei moduli adattivi, vedere [Configurazione dell&#39;azione di invio](../../forms/using/configuring-submit-actions.md).

Inoltre, un  modulo adattivo abilitato per Adobe Sign viene inviato solo dopo che tutti i firmatari avranno firmato il modulo. È possibile trovare il modulo firmato parzialmente nella sezione Firma in sospeso del portale dei moduli.  Adobe Sign Configuration Service esegue il polling  server Adobe Sign a [intervalli regolari](../../forms/using/adobe-sign-integration-adaptive-forms.md) per verificare lo stato delle firme. Se tutti i firmatari completano la firma del modulo, viene avviato il servizio di invio e il modulo viene inviato. Se si utilizza un&#39;azione di invio personalizzata e il modulo utilizza  Adobe Sign, aggiornare l&#39;azione di invio personalizzata per utilizzare il servizio di invio dell&#39;azione.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

L&#39;esperienza di firma del modulo è pronta. È possibile visualizzare l&#39;anteprima del modulo per verificare l&#39;esperienza di firma. Nel modulo pubblicato,  campi blocco Adobe Sign vengono visualizzati quando un firmatario riceve il modulo per la firma tramite e-mail. Questa esperienza è nota anche come esperienza di firma fuori forma. È inoltre possibile configurare un&#39;esperienza di firma all&#39;interno del modulo per il primo firmatario. Per ulteriori informazioni, vedere [Creare un&#39;esperienza di firma all&#39;interno del modulo](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali o le firme remote basate su cloud sono una nuova generazione di firme digitali utilizzabili tra computer desktop, dispositivi mobili e Web. e soddisfare i massimi livelli di conformità e garanzia per l&#39;autenticazione dei firmatari. È possibile firmare un modulo adattivo con firme digitali basate su cloud.

Dopo la [modifica delle proprietà del modulo adattivo per  Adobe sign](../../forms/using/working-with-adobe-sign.md#enableadobesign), effettuare le seguenti operazioni per aggiungere il campo firma cloud a un modulo adattivo:

1. Trascinare il componente **Adobe Sign Block** dal browser Componenti al modulo adattivo. Il  componente Adobe Sign Block dispone di tutti i campi Adobe Sign  supportati. Per impostazione predefinita, aggiunge al modulo adattivo un campo **Signature**.

   ![Blocco di firma](assets/sign-block-new.png)

1. Selezionare il componente **blocco Adobe Sign** e toccare l&#39;icona **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png). Visualizza le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Selezionare e aggiungere  campi Adobe Sign. **B.** Espandere il blocco Adobe Sign  a schermo intero

1. Toccate l&#39;icona **Adobe Sign Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Visualizza le opzioni per selezionare e aggiungere  campi Adobe Sign.

   Espandere il campo a discesa **Tipo** per selezionare **Firma digitale** e toccare l&#39;icona Fine per aggiungere il campo selezionato  blocco Adobe Sign.

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio specificare un nome univoco per un campo.

   Per applicare le firme digitali al modulo adattivo, utilizzare:

   * Firme cloud: Effettuare l&#39;accesso con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi attendibili.
   *  Adobe Acrobat o Reader: Scaricate e aprite il documento con  Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.

   Dopo aver aggiunto il campo firma cloud al modulo adattivo, effettuare le seguenti operazioni per completare il processo di configurazione:

   * [Abilitare  Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Selezionare  Cloud Service Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiunta  firmatari Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Creazione di un&#39;esperienza di firma in-form {#create-in-form-signing-experience}

Un utente può inoltre firmare un modulo adattivo durante la compilazione del modulo. Questa esperienza è nota anche come esperienza di firma in-form. L&#39;esperienza di firma in-form è disponibile solo per il primo firmatario in un ambiente con più firmatari. Per creare un&#39;esperienza di firma all&#39;interno del modulo per un modulo adattivo, procedere come segue:

1. [Aggiungere e configurare il componente](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component) Passaggio firma.
1. [Aggiungete il componente](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component) Passaggio di riepilogo.

![Esperienza di firma in-form](assets/in_form_signing_experience_new.png)

### Aggiungere e configurare il componente Passaggio firma {#add-and-configure-the-signature-step-component}

Utilizzare il componente Passaggio firma per specificare un&#39;area in cui firmare elettronicamente il modulo compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF firmabile del modulo compilato. Il componente Passaggio firma occupa la larghezza totale disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio firma.

Per configurare il componente Passaggio firma, effettuare le operazioni seguenti:

1. Trascinare il componente **Passaggio firma** dal browser Componenti al modulo.
1. Selezionare il componente Fase firma appena aggiunto e toccare l&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà dei passaggi firma. Configurare le seguenti proprietà:

   * **Nome** elemento: Specificate il nome del componente.

   * **Titolo:** specificate il titolo univoco del componente.
   * **Messaggio modello:** specificare il messaggio da visualizzare durante il caricamento del PDF della firma.  i servizi Adobe Sign richiedono del tempo per preparare e caricare il PDF della firma.
   * **Servizio di firma:** selezionare la  **** firma Adobe.

   * **Utilizza componente** E-sign legacy: Se si utilizza il rispettivo modulo adattivo in  [ AEM Forms Workspace](../../forms/using/introduction-html-workspace.md),  app AEM Forms o se il modulo adattivo sottostante presenta un componente di firma elettronica legacy, selezionare l&#39;opzione  **Usa** componente di firma elettronica precedente.

   * **Configurazione**: Selezionate una configurazione ( Cloud Service Adobe Sign). La casella a discesa è disponibile solo se è abilitata l&#39;opzione **Usa componente di firma elettronica legacy**.

   Toccate l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   ![Passaggio firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * Quando si trascina il componente **[!UICONTROL Passaggio firma]** nel modulo, il firmatario e la persona che compila il modulo sono gli stessi?**** viene impostata automaticamente su  **Sì**. È necessario mantenere il funzionamento del modulo.
      >
      > 
   * Per una migliore esperienza, utilizza il componente Passo di riepilogo dopo il componente Passaggio firma. Il passaggio Riepilogo invia il modulo automaticamente e immediatamente dopo aver completato la firma di un modulo nel componente Passaggio firma. Se non si utilizza il passaggio di riepilogo, l&#39;invio automatico viene attivato solo dopo l&#39;intervallo impostato utilizzando il [ Adobe Sign Configuration Service](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
   > * Alcune best practice:
   > * Il pannello dei moduli adattivi contenente il passaggio Firma si trova sempre nell&#39;ultimo o secondo pannello di un modulo adattivo. Può essere il secondo ultimo pannello solo quando l’ultimo pannello contiene il passaggio Riepilogo.
   > * Il pannello contenente il componente Passaggio firma o Riepilogo non può contenere altri componenti.
   > * Per i moduli adattivi contenenti il Passaggio firma non è possibile utilizzare il pulsante di invio. L&#39;invio viene gestito tramite un servizio in background o il passaggio Riepilogo.
   > * Creare un modulo che non consenta all&#39;utente di tornare indietro da un pannello contenente il passaggio Firma o Riepilogo.



### Configurare la pagina di ringraziamento o il componente fase di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

Il componente **Passaggio di riepilogo** invia automaticamente il modulo, compila le informazioni all&#39;interno della pagina di riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Ottiene anche le informazioni richieste nella mappa di ritorno. Il componente Passo di riepilogo occupa la larghezza totale disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passo di riepilogo.

Ora, l&#39;esperienza di firma del modulo in è pronta. È possibile visualizzare l&#39;anteprima del modulo per verificare l&#39;esperienza di firma.

## Domande frequenti {#frequently-asked-questions}

**D:** È possibile incorporare un modulo adattivo in un altro modulo adattivo. È possibile abilitare il modulo adattivo incorporato  Adobe Sign?
**Ans:** No,  AEM Forms non supporta l&#39;uso di un modulo adattivo che incorpora un modulo adattivo abilitato per Adobe Sign  per la firma

**D:** Quando si crea un modulo adattivo utilizzando il modello avanzato e lo si apre per la modifica, viene visualizzato il messaggio di errore &quot;Firma elettronica o Firma elettronica non sono configurati correttamente&quot;. viene visualizzato. Come risolvere il messaggio di errore?
**Ans:Modulo** adattivo creato utilizzando il modello avanzato è configurato per l&#39;utilizzo  Adobe Sign. Per risolvere l&#39;errore, creare e selezionare una configurazione cloud Adobe Sign  e configurare un firmatario Adobe Sign  per il modulo adattivo.

**D:** È possibile utilizzare  tag di testo Adobe Sign in un componente di testo statico di un modulo adattivo?
**Ans:** Sì, è possibile utilizzare i tag di testo in un componente di testo per aggiungere  campi Adobe Sign a un modulo adattivo abilitato per il  [documento di registrazione](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)  (solo opzione per il documento di record generato automaticamente). Per informazioni sulla procedura e sulle regole per creare un tag di testo, vedere [ Documentazione Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Inoltre, i moduli adattivi hanno un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi supportati da [ Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**D:**  AEM Forms fornisce sia  componenti blocco Adobe Sign sia componenti passo firma. Possono essere utilizzati simultaneamente in un modulo adattivo?
**Ans:** È possibile utilizzare entrambi i componenti contemporaneamente in un modulo. Di seguito sono riportati alcuni suggerimenti per l&#39;utilizzo di questi componenti:

**blocco Adobe Sign:** è possibile utilizzare  blocco Adobe Sign per aggiungere  campi Adobe Sign ovunque nel modulo adattivo. Consente inoltre di assegnare campi specifici ai firmatari. Quando un modulo adattivo viene visualizzato in anteprima o pubblicato  blocco Adobe Sign non è visibile, per impostazione predefinita. Questi blocchi sono abilitati solo nel documento di firma. Nel documento di firma sono abilitati solo i campi assegnati a un firmatario.  blocco Adobe Sign può essere utilizzato con il primo e il successivo firmatario.

**Componente passo firma:** È possibile utilizzare il componente passo firma per creare un&#39;esperienza di firma all&#39;interno del modulo. Consente di firmare solo il primo firmatario durante la compilazione del modulo. Durante il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF del modulo da firmare. Si tratta in genere dell’ultima o penultima sezione seguita dal componente di riepilogo di un modulo.

## Risoluzione dei problemi {#troubleshoot}

###  accordi Adobe Sign non riusciti {#adobe-sign-agreement-failures}

****
Problema servizio Adobe Sign configurato per un modulo adattivo, il servizio non riesce a creare un contratto Adobe Sign  per il modulo adattivo sottostante.

**Risoluzione**

* Controllare la [configurazione di  servizio cloud Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilizzato nel modulo adattivo.
* Assicurati che l&#39;applicazione API  server Adobe Sign utilizzata per configurare  servizio Adobe Sign Cloud disponga delle autorizzazioni necessarie.
* Se utilizzate più servizi  Adobe Sign Cloud, indicate l&#39; **[!UICONTROL URL di autenticazione]** di tutti i servizi allo stesso **[!UICONTROL Adobe Sign Share]**.

* Utilizza indirizzi e-mail separati per configurare  account Adobe Sign e per il primo firmatario e il singolo firmatario. L&#39;indirizzo e-mail del primo firmatario o dell&#39;unico firmatario (nel caso del singolo firmatario) non può essere identico a  account Adobe Sign utilizzato per configurare i servizi cloud AEM.

###  flusso di lavoro AEM Forms configurato per  modulo adattivo abilitato per Adobe Sign non viene avviato {#adobe-sign-aem-form-workflow-failures}

****
Problema Adobe Sign è configurato per un modulo adattivo, il flusso di lavoro configurato utilizzando l&#39;opzione Richiama Forms Workflow non viene avviato.

**Risoluzione**

* Se si utilizza  Adobe Sign senza il passaggio Firma o se il modulo richiede la firma di più persone,  server AEM Forms attende che il pianificatore confermi che tutte le persone hanno firmato il modulo. L&#39;utilità di pianificazione invia il modulo adattivo solo dopo che l&#39;utente ha completato la firma e il flusso di lavoro inizia solo dopo l&#39;invio corretto del modulo adattivo. È possibile abbreviare l&#39;intervallo di [scheduler](adobe-sign-integration-adaptive-forms.md) per controllare lo stato della firma del modulo a intervalli rapidi e per velocizzare l&#39;invio.


## Articoli correlati {#related-articles}

* [Integrare  Adobe Sign con  AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Utilizzo di  Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Utilizzo  Adobe Sign con  AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
