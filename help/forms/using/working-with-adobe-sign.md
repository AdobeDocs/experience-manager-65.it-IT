---
title: Utilizzo di Adobe Sign in un modulo adattivo
seo-title: Using Adobe Sign in an adaptive form
description: Abilita i flussi di lavoro di firma elettronica (Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi a firma singola e multipla e firmare elettronicamente i moduli da dispositivi mobili.
seo-description: Enable e-signature (Adobe Sign) workflows for an adaptive form to automate signing workflows, simplify single and multi-signature processes, and to electronically sign forms from mobile devices.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: 4714554609a10e58b1c7141696d694fac46887a6
workflow-type: tm+mt
source-wordcount: '3826'
ht-degree: 0%

---

# Utilizzo di [!DNL Adobe Sign] in un modulo adattivo{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per questioni legali, vendite, retribuzioni, gestione delle risorse umane e altre aree.

In un tipico [!DNL Adobe Sign] e nello scenario dei moduli adattivi, un utente compila un modulo adattivo da applicare a un servizio. Ad esempio, una richiesta di mutuo e carta di credito richiede la firma legale da parte di tutti i mutuatari e i corichiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, è possibile integrare [!DNL Adobe Sign] con AEM [!DNL Forms]. Altri esempi sono: puoi utilizzare [!DNL Adobe Sign] a:

* Chiudere le offerte da qualsiasi dispositivo con procedure di proposta, preventivo e contratto completamente automatizzate.
* Completa i processi relativi alle risorse umane più rapidamente e offri ai tuoi dipendenti le esperienze digitali.
* Ridurre i tempi di ciclo del contratto e integrare i fornitori più rapidamente.
* Crea flussi di lavoro digitali che automatizzano i processi più comuni.

[!DNL Adobe Sign] Integrazione con l’AEM [!DNL Forms] supporta:

* Flussi di lavoro di firma per utente singolo e multiplo
* Flussi di lavoro di firma sequenziali e simultanei
* Esperienze di firma in-form e out-of-form
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con AEM) [!DNL Forms] workflow)
* Autenticazione tramite una knowledge base, un telefono e profili social

Scopri [best practice per l’utilizzo di Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) per creare esperienze di firma migliori.

## Prerequisiti {#prerequisites}

Prima di utilizzare [!DNL Adobe Sign] in un modulo adattivo:

* Garantire AEM [!DNL Forms] il servizio cloud è configurato per l’utilizzo [!DNL Adobe Sign]. Per ulteriori informazioni, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Tieni pronto l’elenco dei firmatari. È necessario almeno un indirizzo e-mail per ogni firmatario.

## Configura [!DNL Adobe Sign] per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Per configurare, effettua le seguenti operazioni [!DNL Adobe Sign] per un modulo adattivo:

1. [Modifica le proprietà del modulo adattivo per il segno di Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Aggiungere campi Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Seleziona Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Aggiungere firmatari Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Seleziona Azione di invio per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Dettagli firmatario](assets/signer_details_new.png)

### Modifica proprietà modulo adattivo per [!DNL Adobe Sign] {#enableadobesign}

Configurare le proprietà dei moduli adattivi per [!DNL Adobe Sign] per un modulo adattivo esistente o nuovo.

[Creazione di un modulo adattivo per Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) descrive i passaggi per creare un modulo adattivo di base. Consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md) per altre opzioni disponibili durante la creazione di un modulo adattivo.

#### Creare un modulo adattivo per [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo con firma, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona il modello e tocca **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Base]** scheda:

   1. Specifica la **[!UICONTROL Nome]** e **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona la [Contenitore configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione [!DNL Adobe Sign] con AEM [!DNL Forms].

      >[!NOTE]
      >
      >Il **[!UICONTROL Adobe Sign Cloud Service]** nell’elenco a discesa vengono visualizzati i servizi cloud configurati nel contenitore di configurazione selezionato in questo campo. Il **[!UICONTROL Adobe Sign Cloud Service]** è disponibile nella sezione **[!UICONTROL Firma elettronica]** nelle proprietà del modulo adattivo quando selezioni la **[!UICONTROL Abilita Adobe Sign]** opzione.

1. In **[!UICONTROL Modello modulo]** , selezionare una delle opzioni seguenti:

   * Seleziona la **[!UICONTROL Associa modello modulo come modello del documento record]** e selezionare un modello di documento record. Se utilizzi un modulo adattivo basato su modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Seleziona la **[!UICONTROL Genera documento di record]** opzione. Se utilizzi un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato alla firma che può essere utilizzato per aggiungere [!DNL Adobe Sign] campi.

#### Modificare un modulo adattivo per [!DNL Adobe Sign] {#editafsign}

Effettua le seguenti operazioni per utilizzare [!DNL Adobe Sign] in un modulo adattivo esistente:

1. Accedi a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Base]** , seleziona la scheda [Contenitore configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione [!DNL Adobe Sign] con AEM [!DNL Forms].
1. In **[!UICONTROL Modello modulo]** , selezionare una delle opzioni seguenti:

   * Seleziona la **[!UICONTROL Associa modello modulo come modello del documento record]** e selezionare un modello di documento record. Se utilizzi un modulo adattivo basato su modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Seleziona la **[!UICONTROL Genera documento di record]** opzione. Se utilizzi un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL Adobe Sign].

### Aggiungere campi Adobe Sign a un modulo adattivo {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] dispone di vari campi che possono essere inseriti in un modulo adattivo. Questi campi accettano diversi tipi di dati, ad esempio firme, iniziali, società o titoli, e consentono di raccogliere ulteriori informazioni durante la firma, insieme alle firme. È possibile utilizzare [!DNL Adobe Sign] Blocca componente da posizionare [!DNL Adobe Sign] campi in varie posizioni in un modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare varie opzioni relative a tali campi, effettua le seguenti operazioni:

1. Trascinamento della selezione **[!UICONTROL Blocco Adobe Sign]** dal browser componenti al modulo adattivo. Il [!DNL Adobe Sign] Il componente di blocco ha tutti i [!DNL Adobe Sign] campi. Per impostazione predefinita, aggiunge **Firma** al modulo adattivo.

   ![Blocco di firma](assets/sign_block_new.png)

   Per impostazione predefinita, il [!DNL Adobe Sign] Il blocco non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti di firma. È possibile modificare la visibilità di [!DNL Adobe Sign] Blocca dalle proprietà del [!DNL Adobe Sign] Blocca componente.

   >[!NOTE]
   >
   >    * Utilizzo di [!DNL Adobe Sign] il blocco non è obbligatorio [!DNL Adobe Sign] in un modulo adattivo. Se non usa [!DNL Adobe Sign] blocca e aggiungi i campi per i firmatari, quindi il campo firma predefinito viene visualizzato nella parte inferiore dei documenti di firma.
   >    * Utilizzare [!DNL Adobe Sign] solo per i moduli adattivi che generano automaticamente documenti di record. Se utilizzi un XDP personalizzato per generare un documento di record o un modulo adattivo basato su modello di modulo, [!DNL Adobe Sign] blocco non supportato.


1. Seleziona la **[!UICONTROL Blocco Adobe Sign]** e tocca il pulsante **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) icona. Vengono visualizzate le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **R.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandi [!DNL Adobe Sign] blocco alla visualizzazione a schermo intero

1. Tocca il **[!UICONTROL Adobe Sign] Campo** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) icona. Vengono visualizzate le opzioni per selezionare e aggiungere [!DNL Adobe Sign] campi.

   Espandi **[!UICONTROL Tipo]** campo a discesa per selezionare un [!DNL Adobe Sign] e tocca il pulsante Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) icona per aggiungere il campo selezionato a [!DNL Adobe Sign] blocco. Il **[!UICONTROL Tipo]** Il campo a discesa include i tipi di campo Firma, Informazioni firmatario e Dati. [!DNL Adobe Sign] Integrazione con l’AEM [!DNL Forms] campi di supporto elencati nella [!UICONTROL Tipo] solo casella a discesa. Per informazioni dettagliate su [!DNL Adobe Sign] campi, vedi [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio fornire un nome univoco per un campo. Puoi anche selezionare l’opzione richiesta per contrassegnare un campo come obbligatorio. Oltre al **[!UICONTROL Nome]** e **[!UICONTROL Obbligatorio]** opzione, alcuni [!DNL Adobe Sign] hanno più opzioni. Ad esempio, maschera e su più righe. Inoltre, specifica un nome univoco per ogni [!DNL Adobe Sign] se i campi si trovano nello stesso campo o in un campo diverso [!DNL Adobe Sign] blocchi.

   Se si seleziona **[!UICONTROL Firma digitale]** dall’elenco a discesa, puoi applicare le firme digitali al modulo adattivo:

   * Online utilizzando le firme cloud per firmare con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi di trust.
   * In locale, scaricando il documento con Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilita [!DNL Adobe Sign] per un modulo adattivo {#enableadobsignforanadaptiveform}

Pronti all’uso, [!DNL Adobe Sign] non è abilitato per un modulo adattivo. Per abilitarlo, effettua le seguenti operazioni:

1. Nel browser Contenuti, tocca **[!UICONTROL Contenitore modulo]**, e tocca il **[!UICONTROL Configura]** ![configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la sezione **[!UICONTROL Firma elettronica]** Pannello a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione. Abilita [!DNL Adobe Sign] per un modulo adattivo.

### Seleziona [!DNL Adobe Sign] Cloud Service e ordine di firma {#selectadobesigncloudserviceforanadaptiveform}

È possibile configurare più [!DNL Adobe Sign] servizi per un&#39;istanza dell&#39;AEM [!DNL Forms]. È consigliabile disporre di un insieme separato di servizi per ciascuna funzione (risorse umane, finanze e altro ancora). Semplifica il tracciamento e il reporting dei documenti firmati. Ad esempio, una banca dispone di più reparti. È possibile disporre di una configurazione separata per ciascun reparto per un migliore tracciamento dei documenti.

Un documento può anche avere più firmatari. Ad esempio, un&#39;applicazione con carta di credito può avere più richiedenti. Una banca richiede le firme di tutti i richiedenti prima di iniziare l&#39;elaborazione della domanda. Per scenari con più firmatari, è possibile scegliere di firmare il documento in ordine sequenziale o simultaneo.

Per selezionare un servizio cloud e impostare l’ordine di firma, effettua le seguenti operazioni:

![servizio cloud](assets/cloud-service.png)

1. Nel browser Contenuti, tocca **[!UICONTROL Contenitore modulo]**, e tocca il **[!UICONTROL Configura]** ![configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la sezione **[!UICONTROL Firma elettronica]** Pannello a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Seleziona un servizio cloud dall’elenco già configurato di [!DNL Adobe Sign] Cloud Services.

   Se il **[!UICONTROL Adobe Sign Cloud Service]** è vuoto, segui la [Configurare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) articolo per configurare il servizio.

   Il menu a discesa elenca i servizi cloud esistenti nel `global` cartella in Strumenti > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Inoltre, il menu a discesa elenca anche i servizi cloud presenti nella cartella selezionata nel **[!UICONTROL Contenitore configurazione]** quando crei un modulo adattivo.

1. Selezionare l&#39;ordine di firma dalla **[!UICONTROL I firmatari possono firmare]** . [!DNL Adobe Sign] i cantanti possono firmare un modulo adattivo **[!UICONTROL In sequenza]** - uno dopo l&#39;altro firmatario, oppure **[!UICONTROL Contemporaneamente]** - in qualsiasi ordine.

   In ordine sequenziale, un firmatario riceve il modulo per la firma, alla volta. Dopo che un firmatario ha completato la firma del documento, il modulo viene inviato al firmatario successivo e così via.

   In ordine simultaneo, più firmatari possono firmare un modulo alla volta.

1. [Aggiungere firmatari a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) e tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.


### Aggiungere firmatari a un modulo adattivo {#addsignerstoanadaptiveform}

Per un modulo adattivo puoi avere un solo firmatario o più firmatari. Quando aggiungi un firmatario, puoi anche configurare i dettagli di autenticazione per il firmatario. Puoi anche selezionare se la persona che compila il modulo e il cantante sono la stessa. Per aggiungere e fornire vari dettagli su un firmatario, effettua le seguenti operazioni:

1. Nel browser Contenuti, tocca **[!UICONTROL Contenitore modulo]**, e tocca il **[!UICONTROL Configura]** ![configura](assets/configure.png) icona. Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la sezione **[!UICONTROL Firma elettronica]** Pannello a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Tocca **[!UICONTROL Aggiungi firmatario]** in **[!UICONTROL Configurazione firmatario]**. Aggiunge un firmatario al modulo adattivo. È possibile aggiungere più [!DNL Adobe Sign] da firmatari a un modulo adattivo.
   ![phone-details](assets/phone-details.png)

1. Fai clic su **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) per specificare le seguenti informazioni sul firmatario:

   * **[!UICONTROL Titolo]:** Specifica un titolo per identificare in modo univoco un firmatario.

   * **[!UICONTROL Il firmatario e la persona che riempie il modulo corrispondono?]:** Seleziona **Sì**, se il compilatore del modulo e il primo firmatario sono la stessa persona. Se l’opzione è impostata su **No,** quindi non utilizzare il componente del passaggio di firma nel modulo adattivo. Se il modulo contiene un componente Passaggio firma, il campo viene automaticamente impostato su Sì.

   * **[!UICONTROL Indirizzo e-mail del firmatario]:** Specifica l’indirizzo e-mail del firmatario. Il firmatario riceve i documenti/moduli da firmare all&#39;indirizzo e-mail specificato. Puoi scegliere di utilizzare un indirizzo e-mail fornito in un campo del modulo, nel profilo utente AEM dell’utente connesso o immettere manualmente un indirizzo e-mail. È un passaggio obbligatorio. Assicurati che l’indirizzo e-mail del primo firmatario o dell’unico firmatario (in caso di firmatario singolo) non sia identico a [!DNL Adobe Sign] account utilizzato per configurare AEM Cloud Services.

   * **[!UICONTROL Metodo di autenticazione del firmatario]:** Specifica il metodo per autenticare un utente prima di aprire un modulo per la firma. Puoi scegliere tra l’autenticazione basata su telefono, knowledge base e social identity.
   >[!NOTE]
   >
   >    * Per impostazione predefinita, l’autenticazione basata su identità social fornisce un’opzione per eseguire l’autenticazione utilizzando Facebook, Google e LinkedIn. Puoi contattare [!DNL Adobe Sign] supporto per abilitare altri provider di autenticazione social.


   * **[!DNL Adobe Sign]campi da compilare o firmare:** Seleziona [!DNL Adobe Sign] campi per il firmatario. Un modulo adattivo può avere più [!DNL Adobe Sign] campi. Puoi scegliere di abilitare campi specifici per un firmatario. Nel campo vengono visualizzati tutti i [!DNL Adobe Sign] Blocchi. Quando selezioni un blocco, vengono selezionati tutti i campi del blocco. Puoi utilizzare l’icona X per deselezionare un campo.

   ![dettagli-firmatario](assets/signer-details.png)

   L’immagine precedente presenta due esempi [!DNL Adobe Sign] Blocchi: Informazioni personali e dettagli dell’ufficio

   Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) icona. Il firmatario viene aggiunto e configurato.

### Seleziona Azione di invio per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo, aggiungi [!DNL Adobe Sign] campi in un modulo adattivo, abilita [!DNL Adobe Sign] dal contenitore modulo, seleziona [!DNL Adobe Sign] Cloud Service e aggiungi [!DNL Adobe Sign] Firmatari, seleziona un’azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio dei moduli adattivi, consulta [Configurazione dell’azione Invia](../../forms/using/configuring-submit-actions.md).

Inoltre, un’ [!DNL Adobe Sign] il modulo adattivo abilitato viene inviato solo dopo che tutti i firmatari hanno firmato il modulo. Puoi trovare un modulo parzialmente firmato nella sezione Firma in sospeso del portale dei moduli. [!DNL Adobe Sign] Il servizio di configurazione mantiene il polling [!DNL Adobe Sign] server in [intervalli regolari](../../forms/using/adobe-sign-integration-adaptive-forms.md) per verificare lo stato delle firme. Se tutti i firmatari completano la firma del modulo, viene avviato il servizio azione di invio e il modulo viene inviato. Se utilizzi un’azione di invio personalizzata e il modulo utilizza [!DNL Adobe Sign], aggiorna l’azione di invio personalizzata per utilizzare il servizio azione di invio.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

L’esperienza di firma del modulo è pronta. Puoi visualizzare in anteprima il modulo per verificare l’esperienza di firma. Nel modulo pubblicato: [!DNL Adobe Sign] I campi di blocco vengono visualizzati quando un firmatario riceve il modulo per la firma tramite un messaggio e-mail. Questa esperienza è anche nota come esperienza di firma out-of-form. Puoi anche configurare un’esperienza di firma interna ai moduli per il primo firmatario. Per i passaggi dettagliati, vedi [Creare un’esperienza di firma interna ai moduli](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali basate sul cloud o firme remote sono una nuova generazione di firme digitali che funzionano su desktop, dispositivi mobili e Web e soddisfano i massimi livelli di conformità e garanzia per l&#39;autenticazione dei firmatari. Puoi firmare un modulo adattivo con firme digitali basate su cloud.

Dopo [modifica delle proprietà di un modulo adattivo per il segno di Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), per aggiungere un campo firma cloud a un modulo adattivo, effettua le seguenti operazioni:

1. Trascinamento della selezione **[!UICONTROL Blocco Adobe Sign]** dal browser componenti al modulo adattivo. Il [!UICONTROL Blocco Adobe Sign] il componente dispone di tutti i [!DNL Adobe Sign] campi. Per impostazione predefinita, aggiunge **[!UICONTROL Firma]** al modulo adattivo.

   ![Blocco di firma](assets/sign-block-new.png)

1. Seleziona la **[!UICONTROL Blocco Adobe Sign]** e tocca il pulsante **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) icona. Vengono visualizzate le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **R.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandi [!DNL Adobe Sign] blocco alla visualizzazione a schermo intero

1. Tocca il **[!UICONTROL Campo Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) icona. Vengono visualizzate le opzioni per selezionare e aggiungere [!DNL Adobe Sign] campi.

   Espandi **[!UICONTROL Tipo]** campo a discesa da selezionare **[!UICONTROL Firma digitale]** e tocca il **Fine** icona per aggiungere il campo selezionato a [!DNL Adobe Sign] blocco.

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio fornire un nome univoco per un campo.

   Applica firme digitali al modulo adattivo utilizzando:

   * Firme cloud: firma con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi di trust.
   * Adobe Acrobat o Reader: scarica e apri il documento con Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.

   Dopo aver aggiunto il campo firma cloud al modulo adattivo, esegui i seguenti passaggi per completare il processo di configurazione:

   * [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Seleziona Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiungere firmatari Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Seleziona Azione di invio per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Creare un’esperienza di firma interna ai moduli {#create-in-form-signing-experience}

Un utente può anche firmare un modulo adattivo durante la compilazione dello stesso. Questa esperienza è nota anche come esperienza di firma interna ai moduli. L’esperienza di firma interna ai moduli è disponibile solo per il primo cantante in un ambiente con più firmatari. Per creare un’esperienza di firma interna ai moduli per un modulo adattivo, effettua le seguenti operazioni:

1. [Aggiungere e configurare il componente Passaggio firma](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [Aggiungere il componente Passaggio di riepilogo](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![Esperienza di firma nei moduli](assets/in_form_signing_experience_new.png)

### Aggiungere e configurare il componente Passaggio firma {#add-and-configure-the-signature-step-component}

Utilizza il componente Passaggio di firma per fornire un’area in cui firmare elettronicamente il modulo compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio di firma, viene visualizzata una versione PDF firmabile del modulo compilato. Il componente Passaggio di firma occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di firma.

Per configurare il componente Passaggio firma, effettua le seguenti operazioni:

1. Trascina la selezione **[!UICONTROL Passaggio di firma]** dal browser Componenti al modulo.
1. Seleziona il componente del passaggio Firma appena aggiunto e tocca il **Configura** ![configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **[!UICONTROL Nome]**: specifica il nome del componente.

   * **[!UICONTROL Titolo]:** Specifica il titolo univoco del componente.
   * **[!UICONTROL Messaggio modello]:** Specificare il messaggio da visualizzare durante il caricamento del PDF della firma. [!DNL Adobe Sign] I servizi richiedono un po’ di tempo per preparare e caricare signature PDF.
   * **[!UICONTROL Servizio di firma]:** Seleziona la **[!DNL Adobe Sign]** opzione.

   * **[!UICONTROL Usa componente E-sign legacy]**: se utilizzi il rispettivo modulo adattivo in [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM [!DNL Forms] o il modulo adattivo sottostante contiene un componente e-sign legacy, seleziona la **Usa componente E-sign legacy** opzione.

   * **[!UICONTROL Configurazione]**: seleziona una configurazione ([!DNL Adobe Sign] Cloud Service). La casella a discesa è disponibile solo se **Usa componente E-sign legacy** l&#39;opzione è abilitata.

   * **[!UICONTROL Classe CSS]**: specifica la classe CSS per il componente.

   Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   ![Passaggio di firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* Quando si trascina **[!UICONTROL Passaggio di firma]** componente del modulo, il **[!UICONTROL Il firmatario e la persona che compila il modulo corrispondono?]** l&#39;opzione è impostata automaticamente su **Sì**. È necessario per il corretto funzionamento del modulo.
   >* Utilizza il componente Passaggio di riepilogo dopo il componente Passaggio di firma per una migliore esperienza. Il passaggio Riepilogo invia automaticamente e immediatamente il modulo dopo aver completato la firma nel componente Passaggio firma. Se non utilizzi il passaggio di riepilogo, l’invio automatico viene attivato solo dopo l’intervallo impostato utilizzando [Servizio di configurazione Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).

   >
   >Alcune best practice sono:
   >
   >* Il pannello dei moduli adattivi contenente il passaggio Firma si trova sempre nell’ultimo o nel secondo ultimo pannello di un modulo adattivo. Può essere il secondo ultimo pannello solo quando l’ultimo pannello contiene il passaggio Riepilogo.
   >* Il pannello contenente il componente del passaggio Firma o Riepilogo non può contenere altri componenti.
   >* I moduli adattivi contenenti il passaggio di firma non possono avere un pulsante di invio.
   >* L’invio dei moduli adattivi contenenti la fase Firma viene gestito tramite un servizio in background o la fase Riepilogo. Se esiste un firmatario configurato che compila anche il modulo, il vantaggio di gestire l’invio del modulo adattivo utilizzando il passaggio di riepilogo è che valuta immediatamente che il firmatario ha firmato il modulo e richiama l’azione di invio. Un servizio in background impiega più tempo per valutare se tutti i firmatari configurati hanno firmato il modulo e ritarda l’invio del modulo adattivo.
   >* Progettare il modulo in modo da non consentire a un utente di tornare da un pannello contenente il passaggio Firma o Riepilogo.



### Configurare il componente per la pagina di ringraziamento o il passaggio di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

Il **Passaggio di riepilogo** Il componente invia automaticamente il modulo, compila le informazioni all&#39;interno della pagina di riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Ottiene anche le informazioni richieste nella mappa di ritorno. Il componente Passaggio di riepilogo occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di riepilogo.

Ora l’esperienza di firma dei moduli in è pronta. Puoi visualizzare in anteprima il modulo per verificare l’esperienza di firma.

## Domande frequenti {#frequently-asked-questions}

**D:** È possibile incorporare un modulo adattivo in un altro modulo adattivo. Il modulo adattivo incorporato può essere [!DNL Adobe Sign] abilitato?
**Ans:** No, AEM [!DNL Forms] non supporta l’utilizzo di un modulo adattivo che incorpora un [!DNL Adobe Sign] modulo adattivo abilitato per la firma

**D:** Quando creo un modulo adattivo utilizzando il modello avanzato e lo apro per la modifica, viene visualizzato un messaggio di errore di tipo &quot;La firma o i firmatari elettronici non sono configurati correttamente&quot;. viene visualizzato. Come si risolve il messaggio di errore?
**Ans:** Il modulo adattivo creato utilizzando il modello avanzato è configurato per l’utilizzo [!DNL Adobe Sign]. Per risolvere l’errore, crea e seleziona una [!DNL Adobe Sign] configurazione cloud e configurazione di un [!DNL Adobe Sign] firmatario del modulo adattivo.

**D:** Posso utilizzare [!DNL Adobe Sign] tag di testo in un componente testo statico di un modulo adattivo?
**Ans:** Sì, puoi utilizzare i tag di testo in un componente testo per aggiungere [!DNL Adobe Sign] campi in una [Documento record](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (Solo per documento di record generato automaticamente) modulo adattivo abilitato. Per informazioni sulla procedura e sulle regole per creare un tag di testo, consulta [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Inoltre, i moduli adattivi hanno un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi che [Blocco Adobe Sign](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) supporta.

**D:** AEM [!DNL Forms] fornisce entrambi [!UICONTROL Blocco Adobe Sign] e i componenti del passaggio Firma. Possono essere utilizzate simultaneamente in un modulo adattivo?
**Ans:** È possibile utilizzare entrambi i componenti contemporaneamente in un modulo. Di seguito sono riportati alcuni consigli per l’utilizzo di questi componenti:

**Blocco Adobe Sign:** È possibile utilizzare [!UICONTROL Blocco Adobe Sign] da aggiungere [!UICONTROL Adobe Sign] in qualsiasi punto del modulo adattivo. Consente inoltre di assegnare campi specifici ai firmatari. Quando un modulo adattivo viene visualizzato in anteprima o pubblicato [!UICONTROL Adobe Sign] Per impostazione predefinita, il blocco non è visibile. Questi blocchi sono attivati solo nel documento di firma. Nel documento di firma vengono abilitati solo i campi assegnati a un firmatario. [!UICONTROL Adobe Sign] Il blocco può essere utilizzato con il primo firmatario e i firmatari successivi.

**Componente passaggio di firma:** Puoi utilizzare il componente del passaggio di firma per creare un’esperienza di firma interna ai moduli. Consente solo al primo firmatario di firmare mentre il modulo viene compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio di firma, viene visualizzata una versione del modulo firmata da PDF. In genere si tratta dell’ultima o penultima sezione seguita dal componente di riepilogo di un modulo.

## Risoluzione dei problemi {#troubleshoot}

### [!DNL Adobe Sign] errori di contratto {#adobe-sign-agreement-failures}

**Problema**
Quando [!DNL Adobe Sign] è configurato per un modulo adattivo, il servizio non riesce a creare un [!DNL Adobe Sign] accordo per il modulo adattivo sottostante.

**Risoluzione**

* Controlla la [configurazione di Adobe Sign cloud service](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilizzato nel modulo adattivo.
* Assicurati che l’applicazione API su [!DNL Adobe Sign] server utilizzato per configurare [!DNL Adobe Sign] Il servizio cloud dispone delle autorizzazioni necessarie.
* Se utilizzi più [!DNL Adobe Sign] Servizi cloud, punta il **[!UICONTROL URL OAuth]** di tutti i servizi allo stesso **[!UICONTROL Condivisione Adobe Sign]**.

* Utilizza indirizzi e-mail separati per configurare [!DNL Adobe Sign] e per il primo firmatario e il firmatario singolo. L’indirizzo e-mail del primo firmatario o dell’unico firmatario (nel caso del firmatario singolo) non può essere identico a [!DNL Adobe Sign] account utilizzato per configurare AEM Cloud Services.

### AEM [!DNL Forms] workflow configurato per un [!DNL Adobe Sign] il modulo adattivo abilitato non si avvia {#adobe-sign-aem-form-workflow-failures}

**Problema**
Quando [!DNL Adobe Sign] è configurato per un modulo adattivo, il flusso di lavoro è configurato utilizzando l’opzione Richiama [!DNL Forms] L’opzione Flusso di lavoro non si avvia.

**Risoluzione**

* Quando si utilizza [!DNL Adobe Sign] senza la fase di firma o il modulo richieda la firma di più persone, AEM [!DNL Forms] il server attende che l&#39;utilità di pianificazione confermi che tutte le persone hanno firmato il modulo. Il modulo adattivo viene inviato dal modulo di pianificazione solo dopo che tutte le persone hanno completato la firma e il flusso di lavoro inizia solo dopo l’invio corretto del modulo adattivo. È possibile ridurre l&#39;intervallo [modulo di pianificazione](adobe-sign-integration-adaptive-forms.md) per verificare lo stato della firma dei moduli a intervalli rapidi e velocizzare l&#39;invio dei moduli.


## Articoli correlati {#related-articles}

* [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Best practice per l’utilizzo di Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
