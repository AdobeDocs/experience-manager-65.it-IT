---
title: Utilizzo di Adobe Sign in un modulo adattivo
seo-title: Utilizzo di Adobe Sign in un modulo adattivo
description: Attiva i flussi di lavoro di firma elettronica (Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multipla e per firmare elettronicamente i moduli dai dispositivi mobili.
seo-description: Attiva i flussi di lavoro di firma elettronica (Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multipla e per firmare elettronicamente i moduli dai dispositivi mobili.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 0%

---


# Utilizzo di [!DNL Adobe Sign] in un modulo adattivo{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per elaborare i documenti per aree legali, di vendita, di retribuzione, di gestione delle risorse umane e per altre aree.

In uno scenario tipico [!DNL Adobe Sign] e con moduli adattivi, un utente compila un modulo adattivo da richiedere per un servizio. Ad esempio, una domanda di mutuo e di carta di credito richiede firme legali da parte di tutti i mutuatari e co-richiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, è possibile integrare [!DNL Adobe Sign] con AEM [!DNL Forms]. Altri esempi sono disponibili in [!DNL Adobe Sign] per:

* Chiudi le offerte da qualsiasi dispositivo con processi di proposta, preventivo e contratto completamente automatizzati.
* Completa più velocemente i processi delle risorse umane e dai ai tuoi dipendenti le esperienze digitali.
* Taglia i tempi del ciclo di contratto e accedi più rapidamente ai tuoi fornitori.
* Crea flussi di lavoro digitali per automatizzare i processi comuni.

[!DNL Adobe Sign] l&#39;integrazione con AEM  [!DNL Forms] supporta:

* Flussi di lavoro di firma singoli e multipli
* Flussi di lavoro di firma sequenziali e simultanei
* Esperienze di firma in-form e out-of-form
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con AEM [!DNL Forms] flusso di lavoro)
* Autenticazione tramite una knowledge base, un telefono e profili social

Scopri le [best practice per utilizzare Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) per creare esperienze di firma migliori.

## Prerequisiti {#prerequisites}

Prima di utilizzare [!DNL Adobe Sign] in un modulo adattivo:

* Assicurati che AEM servizio cloud [!DNL Forms] sia configurato per utilizzare [!DNL Adobe Sign]. Per informazioni dettagliate, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Prepara l’elenco dei firmatari. È necessario almeno un indirizzo e-mail per ogni firmatario.

## Configurare [!DNL Adobe Sign] per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Esegui i seguenti passaggi per configurare [!DNL Adobe Sign] per un modulo adattivo:

1. [Modificare le proprietà del modulo adattivo per il simbolo di Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Aggiungere campi Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Selezionare Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Aggiungere firmatari di Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Dettagli firmatario](assets/signer_details_new.png)

### Modificare le proprietà dei moduli adattivi per [!DNL Adobe Sign] {#enableadobesign}

Configura le proprietà del modulo adattivo per [!DNL Adobe Sign] per un modulo adattivo esistente o nuovo.

[Creazione di un modulo adattivo, ad Adobe ](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) Firma descrive i passaggi necessari per creare un modulo adattivo di base. Per altre opzioni disponibili durante la creazione di un modulo adattivo, consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md) .

#### Crea un modulo adattivo per [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo abilitato per i segni, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona il modello e tocca **[!UICONTROL Avanti]**.
1. Nella scheda **[!UICONTROL Base]** :

   1. Specifica il **[!UICONTROL Nome]** e il **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona il [contenitore di configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione di [!DNL Adobe Sign] con AEM [!DNL Forms].

      >[!NOTE]
      >
      >L&#39;elenco a discesa **[!UICONTROL Cloud Service Adobe Sign]** visualizza i servizi cloud configurati nel contenitore di configurazione selezionato in questo campo. L’elenco a discesa **[!UICONTROL Cloud Service Adobe Sign]** è disponibile nella sezione **[!UICONTROL Firma elettronica]** delle proprietà del modulo adattivo quando si seleziona l’opzione **[!UICONTROL Abilita Adobe Sign]** .

1. Nella scheda **[!UICONTROL Modello di modulo]**, selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello di documento]** e selezionare un modello di documento di record. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Se si utilizza un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato per la firma, che può essere utilizzato per aggiungere  [!DNL Adobe Sign] campi.

#### Modificare un modulo adattivo per [!DNL Adobe Sign] {#editafsign}

Esegui i seguenti passaggi per utilizzare [!DNL Adobe Sign] in un modulo adattivo esistente:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Seleziona il modulo adattivo e tocca **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]** , seleziona il contenitore di configurazione [creato durante la configurazione di [!DNL Adobe Sign] con AEM [!DNL Forms].](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)
1. Nella scheda **[!UICONTROL Modello di modulo]**, selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello di documento]** e selezionare un modello di documento di record. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Se si utilizza un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL Adobe Sign].

### Aggiungere campi Adobe Sign a un modulo adattivo {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] dispone di vari campi che possono essere inseriti in un modulo adattivo. Questi campi accettano vari tipi di dati, ad esempio firme, iniziali, aziendali o titoli, e consentono di raccogliere ulteriori informazioni durante la firma, insieme alle firme. È possibile utilizzare il componente [!DNL Adobe Sign] Blocco per posizionare i campi [!DNL Adobe Sign] in diverse posizioni all’interno di un modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare varie opzioni relative a tali campi, effettua le seguenti operazioni:

1. Trascina il componente **[!UICONTROL Blocco Adobe Sign]** dal browser Componenti al modulo adattivo. Il componente [!DNL Adobe Sign] Blocco dispone di tutti i campi [!DNL Adobe Sign] supportati. Per impostazione predefinita, aggiunge un campo **Signature** al modulo adattivo.

   ![Blocco dei segni](assets/sign_block_new.png)

   Per impostazione predefinita, il blocco [!DNL Adobe Sign] non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti firmati. È possibile modificare la visibilità di [!DNL Adobe Sign] Block dalle proprietà del componente [!DNL Adobe Sign] Block.

   >[!NOTE]
   >
   >    * L’utilizzo del blocco [!DNL Adobe Sign] non è obbligatorio per l’utilizzo di [!DNL Adobe Sign] in un modulo adattivo. Se non si utilizza il blocco [!DNL Adobe Sign] e si aggiungono campi per i firmatari, il campo firma predefinito viene visualizzato nella parte inferiore dei documenti di firma.
   >    * Utilizzare il blocco [!DNL Adobe Sign] solo per i moduli adattivi che generano automaticamente il documento di record. Se si utilizza un modulo XDP personalizzato per la generazione di un documento di record o un modulo adattivo basato su un modello di modulo, il blocco [!DNL Adobe Sign] non è supportato.


1. Seleziona il componente **[!UICONTROL Blocco Adobe Sign]** e tocca l&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Visualizza le opzioni per aggiungere campi e formattare l’aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi  [!DNL Adobe Sign] campi. **B.** Espandi il  [!DNL Adobe Sign] blocco alla visualizzazione a schermo intero

1. Tocca l&#39;icona **[!UICONTROL Adobe Sign] Campo** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Visualizza le opzioni per selezionare e aggiungere i campi [!DNL Adobe Sign].

   Espandi il campo a discesa **[!UICONTROL Tipo]** per selezionare un campo [!DNL Adobe Sign] e tocca l’icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per aggiungere il campo selezionato al blocco [!DNL Adobe Sign]. Il campo a discesa **[!UICONTROL Tipo]** include i tipi di campo Firma, Informazioni firmatario e Dati. [!DNL Adobe Sign] integrazione con i campi di  [!DNL Forms] supporto AEM elencati solo nella casella   a discesa Typedrop. Per informazioni dettagliate sui campi [!DNL Adobe Sign], consulta la documentazione [Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio fornire un nome univoco per un campo. È inoltre possibile selezionare l’opzione richiesta per contrassegnare un campo obbligatorio. Oltre all&#39;opzione **[!UICONTROL Nome]** e **[!UICONTROL Richiesto]**, alcuni campi [!DNL Adobe Sign] dispongono di più opzioni. Ad esempio, maschera e linea multipla. Inoltre, specifica un nome univoco per ciascun campo [!DNL Adobe Sign] se i campi si trovano in blocchi uguali o diversi [!DNL Adobe Sign].

   Se si seleziona **[!UICONTROL Firma digitale]** dall’elenco a discesa, è possibile applicare le firme digitali al modulo adattivo:

   * Online mediante l&#39;uso di firme cloud per firmare con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi trust.
   * Localmente scaricando il documento con Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilitare [!DNL Adobe Sign] per un modulo adattivo {#enableadobsignforanadaptiveform}

Preconfigurato, [!DNL Adobe Sign] non è abilitato per un modulo adattivo. Esegui i seguenti passaggi per abilitarlo:

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca l&#39;icona **[!UICONTROL Configura]** ![configura](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere il pannello a soffietto **[!UICONTROL Firma elettronica]** e selezionare l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.

### Seleziona [!DNL Adobe Sign] Cloud Service e ordine di firma {#selectadobesigncloudserviceforanadaptiveform}

Puoi configurare più servizi [!DNL Adobe Sign] per un&#39;istanza di AEM [!DNL Forms]. È consigliabile disporre di un insieme separato di servizi per ciascuna funzione (risorse umane, finanze e altro ancora). Semplifica il tracciamento e il reporting dei documenti firmati. Ad esempio, una banca ha più reparti. Puoi disporre di una configurazione separata per ogni reparto per un migliore monitoraggio dei documenti.

Un documento può anche avere più firmatari. Ad esempio, una domanda con carta di credito può avere più candidati. Una banca richiede la firma di tutti i richiedenti prima di iniziare la domanda di elaborazione. Per scenari con più firmatari, è possibile selezionare per firmare il documento in ordine sequenziale o simultaneo.

Esegui i seguenti passaggi per selezionare un servizio cloud e l’ordine di firma:

![servizio cloud](assets/cloud-service.png)

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca l&#39;icona **[!UICONTROL Configura]** ![configura](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere il pannello a soffietto **[!UICONTROL Firma elettronica]** e selezionare l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Seleziona un servizio cloud dall’elenco di Cloud Services [!DNL Adobe Sign] già configurati.

   Se l&#39;elenco **[!UICONTROL Cloud Service Adobe Sign]** è vuoto, segui l&#39;articolo [Configura Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) per configurare il servizio.

   L’elenco a discesa elenca i servizi cloud presenti nella cartella `global` in Strumenti > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Inoltre, l’elenco a discesa elenca i servizi cloud presenti nella cartella selezionata nel campo **[!UICONTROL Contenitore di configurazione]** al momento della creazione di un modulo adattivo.

1. Selezionare l&#39;ordine di firma dalla finestra di dialogo **[!UICONTROL Firma dei firmatari]**. [!DNL Adobe Sign] i cantanti possono firmare un modulo adattivo  **[!UICONTROL in modo sequenziale]** , uno dopo l’altro firmatario o  **[!UICONTROL simultaneamente]** , in qualsiasi ordine.

   In ordine sequenziale, un firmatario riceve il modulo per la firma, alla volta. Al termine della firma del documento da parte di un firmatario, il modulo viene inviato al firmatario successivo e così via.

   In ordine simultaneo, più firmatari possono firmare un modulo alla volta.

1. [Aggiungi i firmatari a un ](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) modulo adattivo e tocca l’icona Fine di  ![aem_6_3_forms_](assets/aem_6_3_forms_save.png) saveicon per salvare le modifiche.


### Aggiungere firmatari a un modulo adattivo {#addsignerstoanadaptiveform}

Per un modulo adattivo è possibile avere un solo firmatario o più firmatari. Quando aggiungi un firmatario, puoi anche configurare i dettagli di autenticazione per il firmatario. È inoltre possibile selezionare se il compilatore e il cantante sono la stessa persona. Esegui i seguenti passaggi per aggiungere e fornire vari dettagli su un firmatario:

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca l&#39;icona **[!UICONTROL Configura]** ![configura](assets/configure.png) . Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandere il pannello a soffietto **[!UICONTROL Firma elettronica]** e selezionare l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Tocca **[!UICONTROL Aggiungi firmatario]** in **[!UICONTROL Configurazione del firmatario]**. Aggiunge un firmatario al modulo adattivo. È possibile aggiungere più firmatari [!DNL Adobe Sign] a un modulo adattivo.
   ![dettagli telefonici](assets/phone-details.png)

1. Fai clic sull&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) per specificare le seguenti informazioni sul firmatario:

   * **[!UICONTROL Titolo]:** specifica un titolo per identificare in modo univoco un firmatario.

   * **[!UICONTROL Il firmatario e la persona che riempie il modulo corrispondono?]:** Selezionare  **Sì** se il compilatore e il primo firmatario sono la stessa persona. Se l’opzione è impostata su **No,**, non utilizzare il componente del passaggio firma nel modulo adattivo. Se il modulo contiene un componente Passaggio firma, il campo viene automaticamente impostato su Sì.

   * **[!UICONTROL Indirizzo e-mail del firmatario]:** specifica l’indirizzo e-mail del firmatario. Il firmatario riceve documenti/moduli firmati all’indirizzo e-mail specificato. È possibile scegliere di utilizzare un indirizzo e-mail fornito in un campo modulo, AEM profilo utente dell’utente connesso oppure immettere manualmente un indirizzo e-mail. Si tratta di un passo obbligatorio. Assicurati che l’indirizzo e-mail del primo firmatario o dell’unico firmatario (nel caso di un singolo firmatario) non sia identico all’account [!DNL Adobe Sign] utilizzato per configurare AEM Cloud Services.

   * **[!UICONTROL Metodo di autenticazione del firmatario]:** specifica il metodo per l’autenticazione di un utente prima di aprire un modulo per la firma. È possibile scegliere tra telefono, knowledge base e autenticazione basata sull&#39;identità social.
   >[!NOTE]
   >
   >    * Per impostazione predefinita, l&#39;autenticazione basata sull&#39;identità social fornisce un&#39;opzione per l&#39;autenticazione tramite Facebook, Google e LinkedIn. Puoi contattare il supporto [!DNL Adobe Sign] per abilitare altri provider di autenticazione social.


   * **[!DNL Adobe Sign]campi da compilare o firmare:** seleziona  [!DNL Adobe Sign] i campi per il firmatario. Un modulo adattivo può avere più campi [!DNL Adobe Sign]. Puoi scegliere di abilitare campi specifici per un firmatario. Nel campo vengono visualizzati tutti i blocchi [!DNL Adobe Sign] disponibili. Quando selezioni un blocco, vengono selezionati tutti i campi del blocco. Puoi usare l’icona X per deselezionare un campo.

   ![dettagli del firmatario](assets/signer-details.png)

   L&#39;immagine di cui sopra ha due esempi [!DNL Adobe Sign] Blocchi: Informazioni personali e dettagli dell&#39;ufficio

   Tocca l’icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) . Il firmatario viene aggiunto e configurato.

### Selezionare Invia azione per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo aver aggiunto i campi [!DNL Adobe Sign] a un modulo adattivo, abilitare [!DNL Adobe Sign] dal contenitore modulo, selezionare il Cloud Service [!DNL Adobe Sign] e aggiungere i firmatari [!DNL Adobe Sign], selezionare un’azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio dei moduli adattivi, vedere [Configurazione dell&#39;azione di invio](../../forms/using/configuring-submit-actions.md).

Inoltre, un modulo adattivo abilitato [!DNL Adobe Sign] viene inviato solo dopo che tutti i firmatari hanno firmato il modulo. È possibile trovare il modulo firmato parzialmente nella sezione Firma in sospeso del portale dei moduli. [!DNL Adobe Sign] Il servizio di configurazione mantiene il  [!DNL Adobe Sign] server di polling a  [intervalli ](../../forms/using/adobe-sign-integration-adaptive-forms.md) regolari per verificare lo stato delle firme. Se tutti i firmatari completano la firma del modulo, viene avviato il servizio di invio dell’azione e il modulo viene inviato. Se si utilizza un’azione di invio personalizzata e il modulo utilizza [!DNL Adobe Sign], aggiornare l’azione di invio personalizzata per utilizzare il servizio di azione di invio.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

L’esperienza di firma del modulo è pronta. È possibile visualizzare un’anteprima del modulo per verificare l’esperienza di firma. Nel modulo pubblicato, i campi [!DNL Adobe Sign] Blocca vengono visualizzati quando un firmatario riceve il modulo per l’apposizione della firma tramite e-mail. Questa esperienza è nota anche come esperienza di firma fuori forma. È inoltre possibile configurare un’esperienza di firma all’interno del modulo per il primo firmatario. Per passaggi dettagliati, consulta [Creare un’esperienza di firma all’interno del modulo](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali o le firme remote basate su cloud sono una nuova generazione di firme digitali che funzionano su desktop, dispositivi mobili e web e soddisfano i più alti livelli di conformità e garanzia per l’autenticazione dei firmatari. È possibile firmare un modulo adattivo con firme digitali basate su cloud.

Dopo aver [modificato le proprietà dei moduli adattivi per Adobe sign](../../forms/using/working-with-adobe-sign.md#enableadobesign), esegui i seguenti passaggi per aggiungere il campo firma cloud a un modulo adattivo:

1. Trascina il componente **[!UICONTROL Blocco Adobe Sign]** dal browser Componenti al modulo adattivo. Il componente [!UICONTROL Adobe Sign Block] dispone di tutti i campi [!DNL Adobe Sign] supportati. Per impostazione predefinita, aggiunge un campo **[!UICONTROL Signature]** al modulo adattivo.

   ![Blocco dei segni](assets/sign-block-new.png)

1. Seleziona il componente **[!UICONTROL Blocco Adobe Sign]** e tocca l&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Visualizza le opzioni per aggiungere campi e formattare l’aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi  [!DNL Adobe Sign] campi. **B.** Espandi il  [!DNL Adobe Sign] blocco alla visualizzazione a schermo intero

1. Tocca l’icona **[!UICONTROL Campo Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Visualizza le opzioni per selezionare e aggiungere i campi [!DNL Adobe Sign].

   Espandi il campo a discesa **[!UICONTROL Tipo]** per selezionare **[!UICONTROL Firma digitale]** e tocca l’icona **Fine** per aggiungere il campo selezionato al blocco [!DNL Adobe Sign].

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio fornire un nome univoco per un campo.

   Applicare le firme digitali al modulo adattivo utilizzando:

   * Firme cloud: Accedi con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi attendibili.
   * Adobe Acrobat o Reader: Scarica e apri il documento con Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.

   Dopo aver aggiunto il campo firma cloud al modulo adattivo, esegui i seguenti passaggi per completare il processo di configurazione:

   * [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Selezionare Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiungere firmatari di Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Creare un’esperienza di firma in-form {#create-in-form-signing-experience}

Un utente può inoltre firmare un modulo adattivo durante la compilazione del modulo. Questa esperienza è nota anche come esperienza di firma in-form. L’esperienza di firma in-form è disponibile solo per il primo firmatario in un ambiente con più firmatari. Per creare un’esperienza di firma all’interno del modulo adattivo, effettua le seguenti operazioni:

1. [Aggiungi e configura il componente](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component) Passaggio firma .
1. [Aggiungi il componente](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component) Passaggio di riepilogo .

![Esperienza di firma in-form](assets/in_form_signing_experience_new.png)

### Aggiungi e configura il componente Passaggio firma {#add-and-configure-the-signature-step-component}

Utilizzare il componente Passaggio firma per fornire un’area per firmare elettronicamente il modulo compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF segnalabile del modulo compilato. Il componente Passaggio firma occupa la larghezza completa disponibile per il modulo. Si consiglia di non avere alcun altro componente nella sezione contenente il componente Passaggio firma.

Esegui i seguenti passaggi per configurare il componente Passaggio firma:

1. Trascina il componente **[!UICONTROL Passaggio firma]** dal browser Componenti al modulo.
1. Seleziona il componente del passaggio Firma appena aggiunto e tocca l’icona **Configura** ![configura](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **[!UICONTROL Nome]**: Specifica il nome del componente.

   * **[!UICONTROL Titolo]:** specifica il titolo univoco del componente.
   * **[!UICONTROL Messaggio modello]:** specifica il messaggio da visualizzare durante il caricamento del PDF firma. [!DNL Adobe Sign] I servizi richiedono del tempo per preparare e caricare il PDF della firma.
   * **[!UICONTROL Servizio di firma]:** seleziona l’ **[!DNL Adobe Sign]** opzione .

   * **[!UICONTROL Utilizza il componente]** E-sign legacy: Se utilizzi il rispettivo modulo adattivo in  [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM  [!DNL Forms] app o il modulo adattivo sottostante ha un componente di firma elettronica legacy, seleziona l’opzione  **Usa** componente di firma elettronica legacy.

   * **[!UICONTROL Configurazione]**: Seleziona una configurazione ([!DNL Adobe Sign] Cloud Service). La casella a discesa è disponibile solo se l’opzione **Usa componente di firma elettronica legacy** è abilitata.

   * **[!UICONTROL Classe]** CSS: Specifica la classe CSS per il componente.

   Tocca l’icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   ![Passaggio firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * Quando si trascina il componente **[!UICONTROL Passaggio firma]** nel modulo, il firmatario e la persona che compila il modulo sono uguali?**** viene impostata automaticamente su  **Sì**. È necessario mantenere il funzionamento del modulo.
      >
      > 
   * Utilizza il componente Passaggio di riepilogo dopo il componente Passaggio firma per una migliore esperienza. Il passaggio Riepilogo invia automaticamente e immediatamente il modulo dopo aver completato la firma di un modulo nel componente Passaggio firma. Se non si utilizza il passaggio di riepilogo, viene attivato un invio automatico solo dopo l&#39;intervallo impostato utilizzando il [Servizio di configurazione Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
      > Alcune best practice sono:
   > * Il pannello adattivo del modulo contenente il passaggio Firma si trova sempre nell’ultimo o nel secondo pannello di un modulo adattivo. Può essere il secondo ultimo pannello solo quando l’ultimo pannello contiene il passaggio Riepilogo .
   > * Il pannello contenente il componente Passaggio firma o Riepilogo non può contenere altri componenti.
   > * I moduli adattivi contenenti il Passaggio firma non possono avere un pulsante di invio.
   > * L’invio dei moduli adattivi contenenti la fase Firma viene gestito tramite un servizio in background o la fase Riepilogo. Se un firmatario configurato sta anche compilando il modulo, il vantaggio di gestire l’invio del modulo adattivo utilizzando il passaggio Riepilogo è che valuta immediatamente che il firmatario ha firmato il modulo e richiama l’azione di invio. Un servizio in background richiede più tempo per valutare se tutti i firmatari configurati hanno firmato il modulo e ritarda l’invio del modulo adattivo.
   > * Creare un modulo per impedire all’utente di tornare da un pannello contenente il passaggio Firma o Riepilogo.



### Configura la pagina di ringraziamento o il componente del passaggio di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

Il componente **Passo di riepilogo** invia automaticamente il modulo, compila le informazioni all’interno della pagina di riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Ottiene anche le informazioni richieste nella mappa di ritorno. Il componente Passo di riepilogo occupa la larghezza completa disponibile per il modulo. Si consiglia di non avere nessun altro componente nella sezione contenente il componente Passaggio di riepilogo .

A questo punto, l’esperienza di firma in modulo è pronta. È possibile visualizzare un’anteprima del modulo per verificare l’esperienza di firma.

## Domande frequenti {#frequently-asked-questions}

**D:** È possibile incorporare un modulo adattivo in un altro modulo adattivo. È possibile abilitare il modulo adattivo incorporato [!DNL Adobe Sign]?
**Ans:** No, AEM  [!DNL Forms] non supporta l’uso di un modulo adattivo che incorpora un modulo adattivo  [!DNL Adobe Sign] abilitato per la firma

**D:** Quando creo un modulo adattivo utilizzando il modello avanzato e lo apro per la modifica, viene visualizzato un messaggio di errore &quot;Firma elettronica o Firmatari non sono configurati correttamente&quot;. appare. Come risolvere il messaggio di errore?
**Ans:** il modulo adattivo creato utilizzando il modello avanzato è configurato per l’utilizzo di  [!DNL Adobe Sign]. Per risolvere l’errore, crea e seleziona una configurazione cloud [!DNL Adobe Sign] e configura un firmatario [!DNL Adobe Sign] per il modulo adattivo.

**D:** È possibile utilizzare i tag  [!DNL Adobe Sign] di testo in un componente di testo statico di un modulo adattivo?
**Ans:** Sì, è possibile utilizzare i tag di testo in un componente di testo per aggiungere  [!DNL Adobe Sign] campi a un modulo adattivo abilitato  [Documento di record](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)  (solo opzione per il documento di record generato automaticamente). Per informazioni sulla procedura e le regole per creare un tag di testo, consulta [Documentazione Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Inoltre, i moduli adattivi hanno un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi supportati da [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**D:** AEM  [!DNL Forms] fornisce sia i componenti per il blocco  [!UICONTROL Adobe Sign ] che i passaggi firma. Possono essere utilizzati simultaneamente in un modulo adattivo?
**Ans:** è possibile utilizzare entrambi i componenti contemporaneamente in un modulo. Di seguito sono riportati alcuni consigli per l’utilizzo di questi componenti:

**Blocco Adobe Sign:** puoi utilizzare il  [!UICONTROL blocco ] Adobe Sign per aggiungere campi  [!UICONTROL Adobe ] firma in qualsiasi punto del modulo adattivo. Consente inoltre di assegnare campi specifici ai firmatari. Quando un modulo adattivo viene visualizzato in anteprima o pubblicato [!UICONTROL Adobe Sign] Block non è visibile, per impostazione predefinita. Questi blocchi sono abilitati solo nel documento di firma. Nel documento di firma sono abilitati solo i campi assegnati a un firmatario. [!UICONTROL Il ] blocco di Adobe può essere utilizzato con il primo e il successivo firmatario.

**Componente Passaggio firma:** è possibile utilizzare il componente Passaggio firma per creare un’esperienza di firma all’interno del modulo. Consente la firma solo del primo firmatario durante la compilazione del modulo. Quando si esegue il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF del modulo segnalabile. Si tratta generalmente dell’ultima o della penultima sezione seguita dal componente di riepilogo di un modulo.

## Risoluzione dei problemi {#troubleshoot}

### [!DNL Adobe Sign] guasti del contratto  {#adobe-sign-agreement-failures}

****
ProblemaQuando il  [!DNL Adobe Sign] servizio è configurato per un modulo adattivo, il servizio non riesce a creare un  [!DNL Adobe Sign] accordo per il modulo adattivo sottostante.

**Risoluzione**

* Controlla la [configurazione del servizio cloud Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilizzato nel modulo adattivo.
* Assicurati che l&#39;applicazione API sul server [!DNL Adobe Sign] utilizzato per configurare il servizio [!DNL Adobe Sign] Cloud disponga delle autorizzazioni necessarie.
* Se utilizzi più servizi cloud [!DNL Adobe Sign], indirizza l&#39; **[!UICONTROL URL di autenticazione]** di tutti i servizi allo stesso **[!UICONTROL Adobe Sign Share]**.

* Utilizza indirizzi e-mail separati per configurare l’account [!DNL Adobe Sign] e per il primo firmatario e il singolo firmatario. L’indirizzo e-mail del primo firmatario o dell’unico firmatario (nel caso del singolo firmatario) non può essere identico all’account [!DNL Adobe Sign] utilizzato per configurare AEM Cloud Services.

### AEM il flusso di lavoro [!DNL Forms] configurato per un modulo adattivo abilitato [!DNL Adobe Sign] non si avvia {#adobe-sign-aem-form-workflow-failures}

****
ProblemaQuando  [!DNL Adobe Sign] è configurato per un modulo adattivo, il flusso di lavoro configurato utilizzando l’opzione Richiama  [!DNL Forms] flusso di lavoro non si avvia.

**Risoluzione**

* Quando si utilizza [!DNL Adobe Sign] senza il passaggio Firma o il modulo richiede la firma di più persone, AEM [!DNL Forms] il server attende che lo scheduler confermi che tutte le persone hanno firmato il modulo. Lo scheduler invia il modulo adattivo solo dopo che l’utente ha completato la firma e il flusso di lavoro inizia solo dopo l’invio corretto del modulo adattivo. È possibile ridurre l&#39;intervallo della [pianificazione](adobe-sign-integration-adaptive-forms.md) per controllare lo stato della firma del modulo a intervalli rapidi e per velocizzare l&#39;invio del modulo.


## Articoli correlati {#related-articles}

* [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Procedure consigliate per l’utilizzo di Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
