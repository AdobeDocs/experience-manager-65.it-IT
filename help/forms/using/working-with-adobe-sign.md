---
title: Utilizzo di Adobe Sign in un modulo adattivo
seo-title: Using Adobe Sign in an adaptive form
description: Attiva i flussi di lavoro di firma elettronica (Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multipla e per firmare elettronicamente i moduli dai dispositivi mobili.
seo-description: Enable e-signature (Adobe Sign) workflows for an adaptive form to automate signing workflows, simplify single and multi-signature processes, and to electronically sign forms from mobile devices.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '3826'
ht-degree: 0%

---

# Utilizzo [!DNL Adobe Sign] in un modulo adattivo{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per elaborare i documenti per aree legali, di vendita, di retribuzione, di gestione delle risorse umane e per altre aree.

In un tipico [!DNL Adobe Sign] e nello scenario relativo ai moduli adattivi, un utente compila un modulo adattivo da richiedere per un servizio. Ad esempio, una domanda di mutuo e di carta di credito richiede firme legali da parte di tutti i mutuatari e co-richiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, è possibile integrare [!DNL Adobe Sign] con AEM [!DNL Forms]. Alcuni altri esempi sono disponibili, è possibile utilizzare [!DNL Adobe Sign] a:

* Chiudi le offerte da qualsiasi dispositivo con processi di proposta, preventivo e contratto completamente automatizzati.
* Completa più velocemente i processi delle risorse umane e dai ai tuoi dipendenti le esperienze digitali.
* Taglia i tempi del ciclo di contratto e accedi più rapidamente ai tuoi fornitori.
* Crea flussi di lavoro digitali per automatizzare i processi comuni.

[!DNL Adobe Sign] integrazione con AEM [!DNL Forms] supporta:

* Flussi di lavoro di firma singoli e multipli
* Flussi di lavoro di firma sequenziali e simultanei
* Esperienze di firma in-form e out-of-form
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con AEM [!DNL Forms] workflow)
* Autenticazione tramite una knowledge base, un telefono e profili social

Scopri le [best practice per l’utilizzo di Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) per creare esperienze di firma migliori.

## Prerequisiti {#prerequisites}

Prima di utilizzare [!DNL Adobe Sign] in un modulo adattivo:

* Assicurati AEM [!DNL Forms] il servizio cloud è configurato per l&#39;utilizzo [!DNL Adobe Sign]. Per maggiori dettagli, vedi [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Prepara l’elenco dei firmatari. È necessario almeno un indirizzo e-mail per ogni firmatario.

## Configura [!DNL Adobe Sign] per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Esegui i seguenti passaggi per configurare [!DNL Adobe Sign] per un modulo adattivo:

1. [Modificare le proprietà del modulo adattivo per il simbolo di Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Aggiungere campi Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Selezionare Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Aggiungere firmatari di Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Dettagli firmatario](assets/signer_details_new.png)

### Modificare le proprietà dei moduli adattivi per [!DNL Adobe Sign] {#enableadobesign}

Configurare le proprietà dei moduli adattivi per [!DNL Adobe Sign] per un modulo adattivo esistente o nuovo.

[Creare un modulo adattivo per Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) descrive i passaggi necessari per creare un modulo adattivo di base. Vedi [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md) per altre opzioni disponibili durante la creazione di un modulo adattivo.

#### Creare un modulo adattivo per [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo abilitato per i segni, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona il modello e tocca **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Base]** scheda:

   1. Specifica la **[!UICONTROL Nome]** e **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona la [contenitore di configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione [!DNL Adobe Sign] con AEM [!DNL Forms].

      >[!NOTE]
      >
      >La **[!UICONTROL Adobe Sign Cloud Service]** nell’elenco a discesa vengono visualizzati i servizi cloud configurati nel contenitore di configurazione selezionato in questo campo. La **[!UICONTROL Adobe Sign Cloud Service]** l’elenco a discesa è disponibile nella **[!UICONTROL Firma elettronica]** della sezione delle proprietà del modulo adattivo quando si seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione .

1. In **[!UICONTROL Modello Modulo]** seleziona una delle opzioni seguenti:

   * Seleziona la **[!UICONTROL Associa modello di modulo come modello del documento di record]** e selezionare un modello Documento di record. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   * Seleziona la **[!UICONTROL Genera documento di registrazione]** opzione . Se si utilizza un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato per la firma, che può essere utilizzato per aggiungere [!DNL Adobe Sign] campi.

#### Modificare un modulo adattivo per [!DNL Adobe Sign] {#editafsign}

Esegui i seguenti passaggi per utilizzare [!DNL Adobe Sign] in un modulo adattivo esistente:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Base]** seleziona la scheda [contenitore di configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione [!DNL Adobe Sign] con AEM [!DNL Forms].
1. In **[!UICONTROL Modello Modulo]** seleziona una delle opzioni seguenti:

   * Seleziona la **[!UICONTROL Associa modello di modulo come modello del documento di record]** e selezionare un modello Documento di record. Se si utilizza un modulo adattivo basato su un modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   * Seleziona la **[!UICONTROL Genera documento di registrazione]** opzione . Se si utilizza un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL Adobe Sign].

### Aggiungere campi Adobe Sign a un modulo adattivo {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] dispone di vari campi che possono essere inseriti in un modulo adattivo. Questi campi accettano vari tipi di dati, ad esempio firme, iniziali, aziendali o titoli, e consentono di raccogliere ulteriori informazioni durante la firma, insieme alle firme. È possibile utilizzare [!DNL Adobe Sign] Blocco del componente da posizionare [!DNL Adobe Sign] in vari punti di un modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare varie opzioni relative a tali campi, effettua le seguenti operazioni:

1. Trascinamento della selezione **[!UICONTROL Blocco Adobe Sign]** dal browser Componenti al modulo adattivo. La [!DNL Adobe Sign] Il componente Blocco dispone di tutti i [!DNL Adobe Sign] campi. Per impostazione predefinita, aggiunge un **Firma** al modulo adattivo.

   ![Blocco dei segni](assets/sign_block_new.png)

   Per impostazione predefinita, la [!DNL Adobe Sign] Il blocco non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti firmati. È possibile modificare la visibilità di [!DNL Adobe Sign] Blocca le proprietà del [!DNL Adobe Sign] Componente blocco.

   >[!NOTE]
   >
   >    * Utilizzo [!DNL Adobe Sign] blocco non obbligatorio da utilizzare [!DNL Adobe Sign] in un modulo adattivo. Se non utilizzi [!DNL Adobe Sign] bloccare e aggiungere campi per i firmatari, quindi il campo firma predefinito viene visualizzato nella parte inferiore dei documenti di firma.
   >    * Utilizzo [!DNL Adobe Sign] bloccare solo i moduli adattivi che generano automaticamente il documento di record. Se si utilizza un XDP personalizzato per la generazione di un modulo adattivo basato su un documento di record o su un modello di modulo, [!DNL Adobe Sign] blocco non supportato.


1. Seleziona la **[!UICONTROL Blocco Adobe Sign]** e tocca **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) icona. Visualizza le opzioni per aggiungere campi e formattare l’aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandi la [!DNL Adobe Sign] blocca a schermo intero

1. Tocca **[!UICONTROL Adobe Sign] Campo** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) icona. Visualizza le opzioni di selezione e aggiunta [!DNL Adobe Sign] campi.

   Espandi la **[!UICONTROL Tipo]** campo a discesa per selezionare un [!DNL Adobe Sign] e tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) icona per aggiungere il campo selezionato a [!DNL Adobe Sign] blocco. La **[!UICONTROL Tipo]** Il campo a discesa include i tipi di campo Firma, Informazioni firmatario e Dati. [!DNL Adobe Sign] integrazione con AEM [!DNL Forms] campi di supporto elencati in [!UICONTROL Tipo] solo casella a discesa. Per informazioni dettagliate su [!DNL Adobe Sign] campi, vedi [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio fornire un nome univoco per un campo. È inoltre possibile selezionare l’opzione richiesta per contrassegnare un campo obbligatorio. Oltre al **[!UICONTROL Nome]** e **[!UICONTROL Obbligatorio]** opzione, alcuni [!DNL Adobe Sign] Il campo dispone di più opzioni. Ad esempio, maschera e linea multipla. Inoltre, specifica un nome univoco per ogni [!DNL Adobe Sign] se i campi si trovano nello stesso o in un altro [!DNL Adobe Sign] blocchi.

   Se si seleziona **[!UICONTROL Firma digitale]** dall’elenco a discesa è possibile applicare le firme digitali al modulo adattivo:

   * Online tramite firme cloud per firmare con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi attendibili.
   * Localmente scaricando il documento con Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilita [!DNL Adobe Sign] per un modulo adattivo {#enableadobsignforanadaptiveform}

Fuori dalla scatola, [!DNL Adobe Sign] non è abilitato per un modulo adattivo. Esegui i seguenti passaggi per abilitarlo:

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca **[!UICONTROL Configura]** ![configurare](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la **[!UICONTROL Firma elettronica]** a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione . Attiva [!DNL Adobe Sign] per un modulo adattivo.

### Seleziona [!DNL Adobe Sign] Cloud Service e ordine di firma {#selectadobesigncloudserviceforanadaptiveform}

È possibile configurare più [!DNL Adobe Sign] servizi per un esempio di AEM [!DNL Forms]. È consigliabile disporre di un insieme separato di servizi per ciascuna funzione (risorse umane, finanze e altro ancora). Semplifica il tracciamento e il reporting dei documenti firmati. Ad esempio, una banca ha più reparti. Puoi disporre di una configurazione separata per ogni reparto per un migliore monitoraggio dei documenti.

Un documento può anche avere più firmatari. Ad esempio, una domanda con carta di credito può avere più candidati. Una banca richiede la firma di tutti i richiedenti prima di iniziare la domanda di elaborazione. Per scenari con più firmatari, è possibile selezionare per firmare il documento in ordine sequenziale o simultaneo.

Esegui i seguenti passaggi per selezionare un servizio cloud e l’ordine di firma:

![servizio cloud](assets/cloud-service.png)

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca **[!UICONTROL Configura]** ![configurare](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la **[!UICONTROL Firma elettronica]** a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione . Attiva [!DNL Adobe Sign] per un modulo adattivo.
1. Seleziona un servizio cloud dall’elenco già configurato di [!DNL Adobe Sign] Cloud Services.

   Se la **[!UICONTROL Adobe Sign Cloud Service]** elenco vuoto, seguire [Configurare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) per configurare il servizio.

   L’elenco a discesa elenca i servizi cloud presenti nel `global` cartella in Strumenti > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Inoltre, il menu a discesa elenca anche i servizi cloud presenti nella cartella selezionata nella **[!UICONTROL Contenitore di configurazione]** quando si crea un modulo adattivo.

1. Seleziona l’ordine di firma dal **[!UICONTROL Firma dei firmatari]** finestra di dialogo. [!DNL Adobe Sign] i cantanti possono firmare un modulo adattivo **[!UICONTROL Sequenziale]** - uno dopo l&#39;altro firmatario, oppure **[!UICONTROL Simultaneamente]** - in qualsiasi ordine.

   In ordine sequenziale, un firmatario riceve il modulo per la firma, alla volta. Al termine della firma del documento da parte di un firmatario, il modulo viene inviato al firmatario successivo e così via.

   In ordine simultaneo, più firmatari possono firmare un modulo alla volta.

1. [Aggiungere firmatari a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) e tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.


### Aggiungere firmatari a un modulo adattivo {#addsignerstoanadaptiveform}

Per un modulo adattivo è possibile avere un solo firmatario o più firmatari. Quando aggiungi un firmatario, puoi anche configurare i dettagli di autenticazione per il firmatario. È inoltre possibile selezionare se il compilatore e il cantante sono la stessa persona. Esegui i seguenti passaggi per aggiungere e fornire vari dettagli su un firmatario:

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca **[!UICONTROL Configura]** ![configurare](assets/configure.png) icona. Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la **[!UICONTROL Firma elettronica]** a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione . Attiva [!DNL Adobe Sign] per un modulo adattivo.
1. Tocca **[!UICONTROL Aggiungi firmatario]** sotto **[!UICONTROL Configurazione del firmatario]**. Aggiunge un firmatario al modulo adattivo. È possibile aggiungere più [!DNL Adobe Sign] effettua la firma su un modulo adattivo.
   ![dettagli telefonici](assets/phone-details.png)

1. Fai clic sul pulsante **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) per specificare le seguenti informazioni sul firmatario:

   * **[!UICONTROL Titolo]:** Specifica un titolo per identificare in modo univoco un firmatario.

   * **[!UICONTROL Il firmatario e la persona che riempie il modulo corrispondono?]:** Seleziona **Sì**, se il compilatore e il primo firmatario sono la stessa persona. Se l’opzione è impostata su **No,** quindi non utilizzare il componente del passaggio firma nel modulo adattivo. Se il modulo contiene un componente Passaggio firma, il campo viene automaticamente impostato su Sì.

   * **[!UICONTROL Indirizzo e-mail del firmatario]:** Specifica l’indirizzo e-mail del firmatario. Il firmatario riceve documenti/moduli firmati all’indirizzo e-mail specificato. È possibile scegliere di utilizzare un indirizzo e-mail fornito in un campo modulo, AEM profilo utente dell’utente connesso oppure immettere manualmente un indirizzo e-mail. Si tratta di un passo obbligatorio. Assicurati che l&#39;indirizzo e-mail del primo firmatario o dell&#39;unico firmatario (nel caso di un singolo firmatario) non sia identico a [!DNL Adobe Sign] account utilizzato per configurare AEM Cloud Services.

   * **[!UICONTROL Metodo di autenticazione del firmatario]:** Specificare il metodo di autenticazione di un utente prima di aprire un modulo per la firma. È possibile scegliere tra telefono, knowledge base e autenticazione basata sull&#39;identità social.
   >[!NOTE]
   >
   >    * Per impostazione predefinita, l’autenticazione basata sull’identità social fornisce un’opzione per l’autenticazione tramite Facebook, Google e LinkedIn. È possibile contattare [!DNL Adobe Sign] supporto per abilitare altri provider di autenticazione social.


   * **[!DNL Adobe Sign]campi da compilare o firmare:** Seleziona [!DNL Adobe Sign] campi per il firmatario. Un modulo adattivo può avere più [!DNL Adobe Sign] campi. Puoi scegliere di abilitare campi specifici per un firmatario. Nel campo vengono visualizzate tutte le opzioni disponibili [!DNL Adobe Sign] Blocchi. Quando selezioni un blocco, vengono selezionati tutti i campi del blocco. Puoi usare l’icona X per deselezionare un campo.

   ![dettagli del firmatario](assets/signer-details.png)

   L&#39;immagine precedente ha due esempi [!DNL Adobe Sign] Blocchi: Informazioni personali e dettagli dell&#39;ufficio

   Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) icona. Il firmatario viene aggiunto e configurato.

### Selezionare Invia azione per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo di te, aggiungi [!DNL Adobe Sign] campi di un modulo adattivo, abilita [!DNL Adobe Sign] dal contenitore modulo, seleziona [!DNL Adobe Sign] Cloud Service e aggiungi [!DNL Adobe Sign] Firmatari, seleziona un’azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio dei moduli adattivi, consulta [Configurazione dell’azione Invia](../../forms/using/configuring-submit-actions.md).

Inoltre, un [!DNL Adobe Sign] il modulo adattivo abilitato viene inviato solo dopo che tutti i firmatari hanno firmato il modulo. È possibile trovare il modulo firmato parzialmente nella sezione Firma in sospeso del portale dei moduli. [!DNL Adobe Sign] Il servizio di configurazione continua il polling [!DNL Adobe Sign] server a [intervalli regolari](../../forms/using/adobe-sign-integration-adaptive-forms.md) per verificare lo stato delle firme. Se tutti i firmatari completano la firma del modulo, viene avviato il servizio di invio dell’azione e il modulo viene inviato. Se si utilizza un’azione di invio personalizzata e il modulo utilizza [!DNL Adobe Sign], aggiorna l’azione di invio personalizzata per utilizzare il servizio di azione di invio.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

L’esperienza di firma del modulo è pronta. È possibile visualizzare un’anteprima del modulo per verificare l’esperienza di firma. Sul modulo pubblicato, [!DNL Adobe Sign] I campi blocco vengono visualizzati quando un firmatario riceve il modulo per la firma tramite e-mail. Questa esperienza è nota anche come esperienza di firma fuori forma. Puoi anche configurare un’esperienza di firma in-form per il primo firmatario, per i passaggi dettagliati vedi [Creare un’esperienza di firma in-form](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali o le firme remote basate su cloud sono una nuova generazione di firme digitali che funzionano su desktop, dispositivi mobili e web e soddisfano i più alti livelli di conformità e garanzia per l’autenticazione dei firmatari. È possibile firmare un modulo adattivo con firme digitali basate su cloud.

Dopo [modifica delle proprietà dei moduli adattivi per Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), effettua le seguenti operazioni per aggiungere il campo firma cloud a un modulo adattivo:

1. Trascinamento della selezione **[!UICONTROL Blocco Adobe Sign]** dal browser Componenti al modulo adattivo. La [!UICONTROL Blocco Adobe Sign] il componente ha tutti i [!DNL Adobe Sign] campi. Per impostazione predefinita, aggiunge un **[!UICONTROL Firma]** al modulo adattivo.

   ![Blocco dei segni](assets/sign-block-new.png)

1. Seleziona la **[!UICONTROL Blocco Adobe Sign]** e tocca **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) icona. Visualizza le opzioni per aggiungere campi e formattare l’aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandi la [!DNL Adobe Sign] blocca a schermo intero

1. Tocca **[!UICONTROL Campo Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) icona. Visualizza le opzioni di selezione e aggiunta [!DNL Adobe Sign] campi.

   Espandi la **[!UICONTROL Tipo]** campo a discesa da selezionare **[!UICONTROL Firma digitale]** e tocca **Fine** icona per aggiungere il campo selezionato a [!DNL Adobe Sign] blocco.

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio fornire un nome univoco per un campo.

   Applicare le firme digitali al modulo adattivo utilizzando:

   * Firme cloud: Firma con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi attendibili.
   * Adobe Acrobat o Reader: Scarica e apri il documento con Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.

   Dopo aver aggiunto il campo firma cloud al modulo adattivo, esegui i seguenti passaggi per completare il processo di configurazione:

   * [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Selezionare Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiungere firmatari di Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Selezionare Invia azione per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Creare un’esperienza di firma in-form {#create-in-form-signing-experience}

Un utente può inoltre firmare un modulo adattivo durante la compilazione del modulo. Questa esperienza è nota anche come esperienza di firma in-form. L’esperienza di firma in-form è disponibile solo per il primo firmatario in un ambiente con più firmatari. Per creare un’esperienza di firma all’interno del modulo adattivo, effettua le seguenti operazioni:

1. [Aggiungere e configurare il componente Passaggio firma](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [Aggiungi il componente Passaggio di riepilogo](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![Esperienza di firma in-form](assets/in_form_signing_experience_new.png)

### Aggiungere e configurare il componente Passaggio firma {#add-and-configure-the-signature-step-component}

Utilizzare il componente Passaggio firma per fornire un’area per firmare elettronicamente il modulo compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF segnalabile del modulo compilato. Il componente Passaggio firma occupa la larghezza completa disponibile per il modulo. Si consiglia di non avere alcun altro componente nella sezione contenente il componente Passaggio firma.

Esegui i seguenti passaggi per configurare il componente Passaggio firma:

1. Trascina e rilascia la **[!UICONTROL Passaggio firma]** dal browser Componenti al modulo.
1. Seleziona il componente del passaggio Firma appena aggiunto e tocca il **Configura** ![configurare](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **[!UICONTROL Nome]**: Specifica il nome del componente.

   * **[!UICONTROL Titolo]:** Specifica il titolo univoco del componente.
   * **[!UICONTROL Messaggio del modello]:** Specificare il messaggio da visualizzare durante il caricamento del PDF firma. [!DNL Adobe Sign] I servizi richiedono del tempo per preparare e caricare signature PDF.
   * **[!UICONTROL Servizio di firma]:** Seleziona la **[!DNL Adobe Sign]** opzione .

   * **[!UICONTROL Usa componente e-sign legacy]**: Se utilizzi il rispettivo modulo adattivo in [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM [!DNL Forms] oppure nel modulo adattivo sottostante è presente un componente di firma elettronica legacy, seleziona la **Usa componente e-sign legacy** opzione .

   * **[!UICONTROL Configurazione]**: Seleziona una configurazione ([!DNL Adobe Sign] Cloud Service). La casella a discesa è disponibile solo se **Usa componente e-sign legacy** è abilitata.

   * **[!UICONTROL Classe CSS]**: Specifica la classe CSS per il componente.

   Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   ![Passaggio firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * Quando trascini e rilascia la **[!UICONTROL Passaggio firma]** al modulo, la **[!UICONTROL Il firmatario e la persona che compila il modulo sono uguali?]** è automaticamente impostato su **Sì**. È necessario mantenere il funzionamento del modulo.
   >
   > * Utilizza il componente Passaggio di riepilogo dopo il componente Passaggio firma per una migliore esperienza. Il passaggio Riepilogo invia automaticamente e immediatamente il modulo dopo aver completato la firma di un modulo nel componente Passaggio firma. Se non si utilizza il passaggio di riepilogo, viene attivato un invio automatico solo dopo l&#39;intervallo impostato utilizzando [Servizio di configurazione di Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
      > Alcune best practice sono:
   > * Il pannello adattivo del modulo contenente il passaggio Firma si trova sempre nell’ultimo o nel secondo pannello di un modulo adattivo. Può essere il secondo ultimo pannello solo quando l’ultimo pannello contiene il passaggio Riepilogo .
   > * Il pannello contenente il componente Passaggio firma o Riepilogo non può contenere altri componenti.
   > * I moduli adattivi contenenti il Passaggio firma non possono avere un pulsante di invio.
   > * L’invio dei moduli adattivi contenenti la fase Firma viene gestito tramite un servizio in background o la fase Riepilogo. Se un firmatario configurato sta anche compilando il modulo, il vantaggio di gestire l’invio del modulo adattivo utilizzando il passaggio Riepilogo è che valuta immediatamente che il firmatario ha firmato il modulo e richiama l’azione di invio. Un servizio in background richiede più tempo per valutare se tutti i firmatari configurati hanno firmato il modulo e ritarda l’invio del modulo adattivo.
   > * Creare un modulo per impedire all’utente di tornare da un pannello contenente il passaggio Firma o Riepilogo.



### Configura la pagina di ringraziamento o il componente del passaggio di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

La **Passaggio di riepilogo** il componente invia automaticamente il modulo, compila le informazioni all’interno della pagina di riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Ottiene anche le informazioni richieste nella mappa di ritorno. Il componente Passo di riepilogo occupa la larghezza completa disponibile per il modulo. Si consiglia di non avere nessun altro componente nella sezione contenente il componente Passaggio di riepilogo .

A questo punto, l’esperienza di firma in modulo è pronta. È possibile visualizzare un’anteprima del modulo per verificare l’esperienza di firma.

## Domande frequenti {#frequently-asked-questions}

**D:** È possibile incorporare un modulo adattivo in un altro modulo adattivo. È possibile che il modulo adattivo incorporato sia [!DNL Adobe Sign] abilitato?
**Ans:** No, AEM [!DNL Forms] non supporta l’uso di un modulo adattivo che incorpora un [!DNL Adobe Sign] modulo adattivo abilitato per la firma

**D:** Quando creo un modulo adattivo utilizzando il modello avanzato e lo apro per la modifica, viene visualizzato un messaggio di errore &quot;Firma elettronica o Firmatari non sono configurati correttamente&quot;. appare. Come risolvere il messaggio di errore?
**Ans:** Il modulo adattivo creato utilizzando il modello avanzato è configurato per l’utilizzo [!DNL Adobe Sign]. Per risolvere l’errore, crea e seleziona un [!DNL Adobe Sign] configurazione cloud e configurazione di un [!DNL Adobe Sign] firma per il modulo adattivo.

**D:** Posso usare [!DNL Adobe Sign] tag di testo in un componente di testo statico di un modulo adattivo?
**Ans:** Sì, è possibile utilizzare i tag di testo in un componente di testo per aggiungere [!DNL Adobe Sign] campi a un [Documento di registrazione](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) Il modulo adattivo abilitato (solo opzione per il documento generato automaticamente). Per informazioni sulla procedura e le regole per creare un tag di testo, consulta [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Inoltre, i moduli adattivi hanno un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi che [Blocco Adobe Sign](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) supporta.

**D:** AEM [!DNL Forms] fornisce entrambi [!UICONTROL Blocco Adobe Sign] e i componenti del passaggio Firma. Possono essere utilizzati simultaneamente in un modulo adattivo?
**Ans:** È possibile utilizzare entrambi i componenti contemporaneamente in un modulo. Di seguito sono riportati alcuni consigli per l’utilizzo di questi componenti:

**Blocco Adobe Sign:** È possibile utilizzare [!UICONTROL Blocco Adobe Sign] per aggiungere [!UICONTROL Adobe Sign] in qualsiasi punto del modulo adattivo. Consente inoltre di assegnare campi specifici ai firmatari. Visualizzazione in anteprima o pubblicazione di un modulo adattivo [!UICONTROL Adobe Sign] Blocco non visibile, per impostazione predefinita. Questi blocchi sono abilitati solo nel documento di firma. Nel documento di firma sono abilitati solo i campi assegnati a un firmatario. [!UICONTROL Adobe Sign] può essere utilizzato con il primo e il successivo firmatario.

**Componente del passaggio firma:** È possibile utilizzare il componente del passaggio firma per creare un’esperienza di firma all’interno del modulo. Consente la firma solo del primo firmatario durante la compilazione del modulo. Quando si esegue il rendering della sezione contenente il componente Passaggio firma, viene visualizzata una versione PDF del modulo segnalabile. Si tratta generalmente dell’ultima o della penultima sezione seguita dal componente di riepilogo di un modulo.

## Risoluzione dei problemi {#troubleshoot}

### [!DNL Adobe Sign] guasti del contratto {#adobe-sign-agreement-failures}

**Problema**
Quando [!DNL Adobe Sign] il servizio è configurato per un modulo adattivo, il servizio non riesce a creare un [!DNL Adobe Sign] accordo per il modulo adattivo sottostante.

**Risoluzione**

* Controlla la [configurazione del servizio cloud Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilizzato nel modulo adattivo.
* Assicurati che l’applicazione API sia attiva su [!DNL Adobe Sign] server utilizzato per configurare [!DNL Adobe Sign] Il servizio Cloud dispone delle autorizzazioni necessarie.
* Se utilizzi più [!DNL Adobe Sign] Servizi cloud, **[!UICONTROL URL di autenticazione]** di tutti i servizi **[!UICONTROL Adobe Sign Shard]**.

* Utilizzare indirizzi e-mail separati per la configurazione [!DNL Adobe Sign] e per il primo firmatario e il singolo firmatario. L’indirizzo e-mail del primo firmatario o dell’unico firmatario (nel caso del singolo firmatario) non può essere identico a [!DNL Adobe Sign] account utilizzato per configurare AEM Cloud Services.

### AEM [!DNL Forms] flusso di lavoro configurato per un [!DNL Adobe Sign] il modulo adattivo abilitato non si avvia {#adobe-sign-aem-form-workflow-failures}

**Problema**
Quando [!DNL Adobe Sign] è configurato per un modulo adattivo, il flusso di lavoro configurato utilizzando la funzione Invoke [!DNL Forms] L&#39;opzione Flusso di lavoro non si avvia.

**Risoluzione**

* Quando utilizzi [!DNL Adobe Sign] senza la fase Firma o il modulo richiede la firma di più persone, AEM [!DNL Forms] server attende che lo scheduler confermi che tutte le persone hanno firmato il modulo. Lo scheduler invia il modulo adattivo solo dopo che l’utente ha completato la firma e il flusso di lavoro inizia solo dopo l’invio corretto del modulo adattivo. È possibile ridurre l&#39;intervallo di [schedulatore](adobe-sign-integration-adaptive-forms.md) per controllare lo stato della firma del modulo a intervalli rapidi e per velocizzare l’invio del modulo.


## Articoli correlati {#related-articles}

* [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Procedure consigliate per l’utilizzo di Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
