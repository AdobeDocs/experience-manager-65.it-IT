---
title: Utilizzo di Adobe Sign in un modulo adattivo
description: Abilita i flussi di lavoro di firma elettronica (Adobe Sign) per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi a firma singola e multipla e firmare elettronicamente i moduli da dispositivi mobili.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components,Acrobat Sign
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3875'
ht-degree: 0%

---

# Utilizzo di [!DNL Adobe Sign] in un modulo adattivo{#using-adobe-sign-in-an-adaptive-form}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html?lang=it) |
| AEM 6.5 | Questo articolo |


[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per questioni legali, vendite, retribuzioni, gestione delle risorse umane e altre aree.

In uno scenario tipico di [!DNL Adobe Sign] e moduli adattivi, un utente compila un modulo adattivo da applicare a un servizio. Ad esempio, una richiesta di mutuo e carta di credito richiede la firma legale da parte di tutti i mutuatari e i corichiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, è possibile integrare [!DNL Adobe Sign] con AEM [!DNL Forms]. Altri esempi: puoi utilizzare [!DNL Adobe Sign] per:

* Chiudere le offerte da qualsiasi dispositivo con procedure di proposta, preventivo e contratto completamente automatizzate.
* Completa i processi relativi alle risorse umane più rapidamente e offri ai tuoi dipendenti le esperienze digitali.
* Ridurre i tempi di ciclo del contratto e integrare i fornitori più rapidamente.
* Crea flussi di lavoro digitali che automatizzano i processi più comuni.

L&#39;integrazione di [!DNL Adobe Sign] con AEM [!DNL Forms] supporta:

* Flussi di lavoro di firma per utente singolo e multiplo
* Flussi di lavoro di firma sequenziali e simultanei
* Esperienze di firma in-form e out-of-form
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con flusso di lavoro AEM [!DNL Forms])
* Autenticazione tramite una knowledge base, un telefono e profili social

Scopri le [best practice per utilizzare Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) per creare esperienze di firma migliori.

## Prerequisiti {#prerequisites}

Prima di utilizzare [!DNL Adobe Sign] in un modulo adattivo:

* Verificare che il servizio cloud AEM [!DNL Forms] sia configurato per l&#39;utilizzo di [!DNL Adobe Sign]. Per ulteriori dettagli, vedere [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Tieni pronto l’elenco dei firmatari. È necessario almeno un indirizzo e-mail per ogni firmatario.

## Configura [!DNL Adobe Sign] per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Per configurare [!DNL Adobe Sign] per un modulo adattivo, effettua le seguenti operazioni:

1. [Modifica le proprietà del modulo adattivo per il segno di Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Aggiungere campi Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Seleziona Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Aggiungere firmatari Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Seleziona Azione di invio per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Dettagli firmatario](assets/signer_details_new.png)

### Modifica proprietà modulo adattivo per [!DNL Adobe Sign] {#enableadobesign}

Configura le proprietà del modulo adattivo per [!DNL Adobe Sign] per un modulo adattivo esistente o nuovo.

[Creare un modulo adattivo per Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) descrive i passaggi per la creazione di un modulo adattivo di base. Consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md) per altre opzioni disponibili durante la creazione di un modulo adattivo.

#### Crea un modulo adattivo per [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo con firma, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **[!UICONTROL Crea]** e **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Selezionare il modello e selezionare **[!UICONTROL Avanti]**.
1. Nella scheda **[!UICONTROL Base]**:

   1. Specifica il **[!UICONTROL Nome]** e il **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Selezionare il [contenitore di configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione di [!DNL Adobe Sign] con AEM [!DNL Forms].

      >[!NOTE]
      >
      >Nell&#39;elenco a discesa **[!UICONTROL Adobe Sign Cloud Service]** sono visualizzati i servizi cloud configurati nel contenitore di configurazione selezionato in questo campo. L&#39;elenco a discesa **[!UICONTROL Adobe Sign Cloud Service]** è disponibile nella sezione **[!UICONTROL Firma elettronica]** delle proprietà del modulo adattivo quando si seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**.

1. Nella scheda **[!UICONTROL Modello modulo]** selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello modulo come modello del documento record]** e selezionare un modello del documento record. Se utilizzi un modulo adattivo basato su modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Se utilizzi un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Selezionare **[!UICONTROL Crea.]** È stato creato un modulo adattivo abilitato alla firma che può essere utilizzato per aggiungere [!DNL Adobe Sign] campi.

#### Modifica un modulo adattivo per [!DNL Adobe Sign] {#editafsign}

Per utilizzare [!DNL Adobe Sign] in un modulo adattivo esistente, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e seleziona **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]**, seleziona il [contenitore di configurazione](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante la configurazione di [!DNL Adobe Sign] con AEM [!DNL Forms].
1. Nella scheda **[!UICONTROL Modello modulo]** selezionare una delle opzioni seguenti:

   * Selezionare l&#39;opzione **[!UICONTROL Associa modello modulo come modello del documento record]** e selezionare un modello del documento record. Se utilizzi un modulo adattivo basato su modello di modulo, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Se utilizzi un modulo adattivo abilitato per l’opzione Documento di record, il documento inviato per la firma visualizza tutti i campi del modulo adattivo.

1. Seleziona **[!UICONTROL Salva e chiudi]**. Modulo adattivo abilitato per [!DNL Adobe Sign].

### Aggiungere campi Adobe Sign a un modulo adattivo {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] contiene vari campi che possono essere inseriti in un modulo adattivo. Questi campi accettano diversi tipi di dati, ad esempio firme, iniziali, società o titoli, e consentono di raccogliere ulteriori informazioni durante la firma, insieme alle firme. È possibile utilizzare il componente di blocco [!DNL Adobe Sign] per inserire [!DNL Adobe Sign] campi in varie posizioni in un modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare varie opzioni relative a tali campi, effettua le seguenti operazioni:

1. Trascina il componente **[!UICONTROL Adobe Sign Block]** dal browser dei componenti al modulo adattivo. Il componente di blocco [!DNL Adobe Sign] contiene tutti i campi [!DNL Adobe Sign] supportati. Per impostazione predefinita, aggiunge un campo **Firma** al modulo adattivo.

   ![Blocco firma](assets/sign_block_new.png)

   Per impostazione predefinita, il blocco [!DNL Adobe Sign] non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti di firma. È possibile modificare la visibilità del blocco [!DNL Adobe Sign] dalle proprietà del componente di blocco [!DNL Adobe Sign].

   >[!NOTE]
   >
   >    * L&#39;utilizzo del blocco [!DNL Adobe Sign] non è obbligatorio per l&#39;utilizzo di [!DNL Adobe Sign] in un modulo adattivo. Se non si utilizza il blocco [!DNL Adobe Sign] e non si aggiungono campi per i firmatari, il campo firma predefinito viene visualizzato nella parte inferiore dei documenti di firma.
   >    * Utilizza il blocco [!DNL Adobe Sign] solo per i moduli adattivi che generano automaticamente documenti di record. Se utilizzi un XDP personalizzato per generare un documento di record o un modulo adattivo basato su modello di modulo, il blocco [!DNL Adobe Sign] non è supportato.
   >
   >

1. Seleziona il componente **[!UICONTROL Adobe Sign Block]** e l&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png). Vengono visualizzate le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandere il blocco [!DNL Adobe Sign] in visualizzazione a schermo intero

1. Seleziona l&#39;icona **[!UICONTROL Adobe Sign] Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Vengono visualizzate le opzioni per selezionare e aggiungere i campi [!DNL Adobe Sign].

   Espandi il campo a discesa **[!UICONTROL Tipo]** per selezionare un campo [!DNL Adobe Sign] e seleziona l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per aggiungere il campo selezionato al blocco [!DNL Adobe Sign]. Il campo a discesa **[!UICONTROL Tipo]** include i tipi di campi Firma, Informazioni firmatario e Dati. L&#39;integrazione di [!DNL Adobe Sign] con AEM [!DNL Forms] supporta solo i campi elencati nella casella a discesa [!UICONTROL Tipo]. Per informazioni dettagliate sui campi [!DNL Adobe Sign], consulta la [documentazione di Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio fornire un nome univoco per un campo. Puoi anche selezionare l’opzione richiesta per contrassegnare un campo come obbligatorio. Oltre all&#39;opzione **[!UICONTROL Name]** e **[!UICONTROL Required]**, alcuni campi [!DNL Adobe Sign] contengono altre opzioni. Ad esempio, maschera e su più righe. Inoltre, specificare un nome univoco per ogni campo [!DNL Adobe Sign], indipendentemente dal fatto che i campi si trovino nello stesso blocco [!DNL Adobe Sign] o in blocchi diversi.

   Se si seleziona **[!UICONTROL Firma digitale]** dall&#39;elenco a discesa, è possibile applicare le firme digitali al modulo adattivo:

   * Online utilizzando le firme cloud per la firma con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi di attendibilità.
   * In locale, scaricando il documento con Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilita [!DNL Adobe Sign] per un modulo adattivo {#enableadobsignforanadaptiveform}

Per un modulo adattivo, [!DNL Adobe Sign] non è abilitato come impostazione predefinita. Per abilitarlo, effettua le seguenti operazioni:

1. Nel browser Contenuto, selezionare **[!UICONTROL Contenitore modulo]** e l&#39;icona **[!UICONTROL Configura]** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi il pannello a soffietto **[!UICONTROL Firma elettronica]** e seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.

### Seleziona il Cloud Service [!DNL Adobe Sign] e l&#39;ordine di firma {#selectadobesigncloudserviceforanadaptiveform}

È possibile configurare più servizi [!DNL Adobe Sign] per un&#39;istanza di AEM [!DNL Forms]. È consigliabile disporre di un insieme separato di servizi per ciascuna funzione (risorse umane, finanze e altro ancora). Semplifica il tracciamento e il reporting dei documenti firmati. Ad esempio, una banca dispone di più reparti. È possibile disporre di una configurazione separata per ciascun reparto per un migliore tracciamento dei documenti.

Un documento può anche avere più firmatari. Ad esempio, un&#39;applicazione con carta di credito può avere più richiedenti. Una banca richiede le firme di tutti i richiedenti prima di iniziare l&#39;elaborazione della domanda. Per scenari con più firmatari, è possibile scegliere di firmare il documento in ordine sequenziale o simultaneo.

Per selezionare un servizio cloud e impostare l’ordine di firma, effettua le seguenti operazioni:

![servizio cloud](assets/cloud-service.png)

1. Nel browser Contenuto, selezionare **[!UICONTROL Contenitore modulo]** e l&#39;icona **[!UICONTROL Configura]** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi il pannello a soffietto **[!UICONTROL Firma elettronica]** e seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Selezionare un servizio cloud dall&#39;elenco già configurato di [!DNL Adobe Sign] Cloud Service.

   Se l&#39;elenco **[!UICONTROL Adobe Sign Cloud Service]** è vuoto, seguire l&#39;articolo [Configurare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) per configurare il servizio.

   Nel menu a discesa sono elencati i servizi cloud esistenti nella cartella `global` in Strumenti > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. Nel menu a discesa sono inoltre elencati i servizi cloud presenti nella cartella selezionata nel campo **[!UICONTROL Contenitore configurazione]** al momento della creazione di un modulo adattivo.

1. Selezionare l&#39;ordine di firma dalla finestra di dialogo **[!UICONTROL I firmatari possono firmare]**. [!DNL Adobe Sign] firmatari possono firmare un modulo adattivo **[!UICONTROL In sequenza]** - uno dopo l&#39;altro firmatario o **[!UICONTROL Contemporaneamente]** - in qualsiasi ordine.

   In ordine sequenziale, un firmatario riceve il modulo per la firma, alla volta. Dopo che un firmatario ha completato la firma del documento, il modulo viene inviato al firmatario successivo e così via.

   In ordine simultaneo, più firmatari possono firmare un modulo alla volta.

1. [Aggiungi firmatari a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) e seleziona l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.


### Aggiungere firmatari a un modulo adattivo {#addsignerstoanadaptiveform}

Per un modulo adattivo puoi avere un solo firmatario o più firmatari. Quando aggiungi un firmatario, puoi anche configurare i dettagli di autenticazione per il firmatario. Puoi anche selezionare se la persona che compila il modulo e il cantante sono la stessa. Per aggiungere e fornire vari dettagli su un firmatario, effettua le seguenti operazioni:

1. Nel browser Contenuto, selezionare **[!UICONTROL Contenitore modulo]** e l&#39;icona **[!UICONTROL Configura]** ![configura](assets/configure.png). Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi il pannello a soffietto **[!UICONTROL Firma elettronica]** e seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Selezionare **[!UICONTROL Aggiungi firmatario]** in **[!UICONTROL Configurazione firmatario]**. Aggiunge un firmatario al modulo adattivo. È possibile aggiungere più [!DNL Adobe Sign] firmatari a un modulo adattivo.
   ![dettagli telefono](assets/phone-details.png)

1. Fai clic sull&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png) per specificare le seguenti informazioni sul firmatario:

   * **[!UICONTROL Titolo]:** Specificare un titolo per identificare in modo univoco un firmatario.

   * **[!UICONTROL Il firmatario e la persona che compila il modulo sono gli stessi?]:** Seleziona **Sì**, se il compilatore del modulo e il primo firmatario sono la stessa persona. Se l&#39;opzione è impostata su **No,** non utilizzare il componente del passaggio della firma nel modulo adattivo. Se il modulo contiene un componente Passaggio firma, il campo viene automaticamente impostato su Sì.

   * **[!UICONTROL Indirizzo e-mail firmatario]:** Specifica l&#39;indirizzo e-mail del firmatario. Il firmatario riceve i documenti/moduli da firmare all&#39;indirizzo e-mail specificato. Puoi scegliere di utilizzare un indirizzo e-mail fornito in un campo del modulo, nel profilo utente AEM dell’utente connesso o immettere manualmente un indirizzo e-mail. È un passaggio obbligatorio. Verificare che l&#39;indirizzo di posta elettronica del primo firmatario o dell&#39;unico firmatario (se esiste un solo firmatario) non sia identico all&#39;account [!DNL Adobe Sign] utilizzato per configurare i servizi cloud AEM.

   * **[!UICONTROL Metodo di autenticazione del firmatario]:** Specificare il metodo di autenticazione di un utente prima di aprire un modulo per la firma. Puoi scegliere tra l’autenticazione basata su telefono, knowledge base e social identity. Per Adobe Acrobat Sign Solutions for Government sono disponibili solo opzioni di autenticazione tramite telefono e knowledge-based.

   >[!NOTE]
   >
   >    * Per impostazione predefinita, l’autenticazione basata su identità social fornisce un’opzione per eseguire l’autenticazione utilizzando Facebook, Google e LinkedIn. È possibile contattare il supporto di [!DNL Adobe Sign] per abilitare altri provider di autenticazione social network.
   >
   >

   * **[!DNL Adobe Sign]campi da compilare o firmare:** Seleziona [!DNL Adobe Sign] campi per il firmatario. Un modulo adattivo può avere più campi [!DNL Adobe Sign]. Puoi scegliere di abilitare campi specifici per un firmatario. Nel campo vengono visualizzati tutti i [!DNL Adobe Sign] blocchi disponibili. Quando selezioni un blocco, vengono selezionati tutti i campi del blocco. Puoi utilizzare l’icona X per deselezionare un campo.

   ![dettagli-firmatario](assets/signer-details.png)

   L&#39;immagine precedente contiene due blocchi di esempio [!DNL Adobe Sign]: Personal-Information e Office-details

   Seleziona l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Il firmatario viene aggiunto e configurato.

### Seleziona Azione di invio per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo aver aggiunto [!DNL Adobe Sign] campi a un modulo adattivo, abilitato [!DNL Adobe Sign] dal contenitore del modulo, selezionato [!DNL Adobe Sign] Cloud Service e aggiunto [!DNL Adobe Sign] firmatari, seleziona un&#39;azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio dei moduli adattivi, consulta [Configurazione dell&#39;azione di invio](../../forms/using/configuring-submit-actions.md).

Inoltre, un modulo adattivo abilitato per [!DNL Adobe Sign] viene inviato solo dopo che tutti i firmatari hanno firmato il modulo. Puoi trovare un modulo parzialmente firmato nella sezione Firma in sospeso del portale dei moduli. Il servizio di configurazione [!DNL Adobe Sign] mantiene il polling del server [!DNL Adobe Sign] a [intervalli regolari](../../forms/using/adobe-sign-integration-adaptive-forms.md) per verificare lo stato delle firme. Se tutti i firmatari completano la firma del modulo, viene avviato il servizio azione di invio e il modulo viene inviato. Se si utilizza un&#39;azione di invio personalizzata e il modulo utilizza [!DNL Adobe Sign], aggiornare l&#39;azione di invio personalizzata per utilizzare il servizio Azione di invio.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. Use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

L’esperienza di firma del modulo è pronta. Puoi visualizzare in anteprima il modulo per verificare l’esperienza di firma. Nel modulo pubblicato, i campi di blocco [!DNL Adobe Sign] vengono visualizzati quando un firmatario riceve il modulo per la firma tramite un messaggio e-mail. Questa esperienza è anche nota come esperienza di firma out-of-form. È inoltre possibile configurare un&#39;esperienza di firma interna ai moduli per il primo firmatario. Per i passaggi dettagliati, vedere [Creare un&#39;esperienza di firma interna ai moduli](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali basate sul cloud o firme remote sono una nuova generazione di firme digitali che funzionano su desktop, dispositivi mobili e Web e soddisfano i massimi livelli di conformità e garanzia per l&#39;autenticazione dei firmatari. Puoi firmare un modulo adattivo con firme digitali basate su cloud.

Dopo [aver modificato le proprietà del modulo adattivo per il segno di Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), effettua le seguenti operazioni per aggiungere il campo della firma cloud a un modulo adattivo:

1. Trascina il componente **[!UICONTROL Adobe Sign Block]** dal browser dei componenti al modulo adattivo. Il componente [!UICONTROL Blocco Adobe Sign] include tutti i campi [!DNL Adobe Sign] supportati. Per impostazione predefinita, aggiunge un campo **[!UICONTROL Firma]** al modulo adattivo.

   ![Blocco firma](assets/sign-block-new.png)

1. Seleziona il componente **[!UICONTROL Adobe Sign Block]** e l&#39;icona **Modifica** ![aem_6_3_edit](assets/aem_6_3_edit.png). Vengono visualizzate le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandere il blocco [!DNL Adobe Sign] in visualizzazione a schermo intero

1. Seleziona l&#39;icona **[!UICONTROL Campo Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Vengono visualizzate le opzioni per selezionare e aggiungere i campi [!DNL Adobe Sign].

   Espandere il campo a discesa **[!UICONTROL Tipo]** per selezionare **[!UICONTROL Firma digitale]** e selezionare l&#39;icona **Fine** per aggiungere il campo selezionato al blocco [!DNL Adobe Sign].

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio fornire un nome univoco per un campo.

   Applica firme digitali al modulo adattivo utilizzando:

   * Firme cloud: accedi con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider del servizio di trust. L’opzione Firma cloud non è disponibile per Adobe Acrobat Sign Solutions for Government.

   * Adobe Acrobat o Reader: scarica e apri il documento con Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.

   Dopo aver aggiunto il campo firma cloud al modulo adattivo, esegui i seguenti passaggi per completare il processo di configurazione:

   * [Abilitare Adobe Sign per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Seleziona Adobe Sign Cloud Service per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiungere firmatari Adobe Sign a un modulo adattivo](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Seleziona Azione di invio per un modulo adattivo](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

## Creare un’esperienza di firma interna ai moduli {#create-in-form-signing-experience}

Un utente può anche firmare un modulo adattivo durante la compilazione dello stesso. Questa esperienza è nota anche come esperienza di firma interna ai moduli. L’esperienza di firma interna ai moduli è disponibile solo per il primo cantante in un ambiente con più firmatari. Per creare un’esperienza di firma interna ai moduli per un modulo adattivo, effettua le seguenti operazioni:

1. [Aggiungere e configurare il componente del passaggio di firma](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [Aggiungere il componente Passaggio di riepilogo](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![Esperienza di firma interna al modulo](assets/in_form_signing_experience_new.png)

### Aggiungere e configurare il componente Passaggio firma {#add-and-configure-the-signature-step-component}

Utilizza il componente Passaggio di firma per fornire un’area in cui firmare elettronicamente il modulo compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio di firma, viene visualizzata una versione PDF firmabile del modulo compilato. Il componente Passaggio di firma occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di firma.

Per configurare il componente Passaggio firma, effettua le seguenti operazioni:

1. Trascina il componente **[!UICONTROL Passaggio firma]** dal browser Componenti al modulo.
1. Seleziona il componente del passaggio di firma appena aggiunto e fai clic sull&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **[!UICONTROL Nome]**: specificare il nome del componente.

   * **[!UICONTROL Titolo]:** Specificare il titolo univoco del componente.
   * **[!UICONTROL Messaggio modello]:** Specificare il messaggio da visualizzare durante il caricamento del PDF della firma. I servizi [!DNL Adobe Sign] richiedono un po&#39; di tempo per preparare e caricare signature PDF.
   * **[!UICONTROL Servizio di firma]:** Selezionare l&#39;opzione **[!DNL Adobe Sign]**.

   * **[!UICONTROL Usa componente E-sign legacy]**: se utilizzi il rispettivo modulo adattivo nell&#39;app [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM [!DNL Forms] o se il modulo adattivo sottostante include un componente e-sign legacy, seleziona l&#39;opzione **Usa componente E-sign legacy**.

   * **[!UICONTROL Configurazione]**: selezionare una configurazione ([!DNL Adobe Sign] Cloud Service). La casella a discesa è disponibile solo se è abilitata l&#39;opzione **Usa componente E-sign legacy**.

   * **[!UICONTROL Classe CSS]**: specificare la classe CSS per il componente.

   Seleziona l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   ![Passaggio firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* Quando si trascina il componente **[!UICONTROL Passaggio firma]** nel modulo, **[!UICONTROL Il firmatario e la persona che compila il modulo sono la stessa persona?L&#39;opzione]** è impostata automaticamente su **Sì**. È necessario per il corretto funzionamento del modulo.
   >* Utilizza il componente Passaggio di riepilogo dopo il componente Passaggio di firma per una migliore esperienza. Il passaggio Riepilogo invia automaticamente e immediatamente il modulo dopo aver completato la firma nel componente Passaggio firma. Se non utilizzi il passaggio di riepilogo, l&#39;invio automatico viene attivato solo dopo l&#39;intervallo impostato utilizzando il [Servizio di configurazione Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
   >
   >Alcune best practice sono:
   >
   >* Il pannello dei moduli adattivi contenente il passaggio Firma si trova sempre nell’ultimo o nel secondo ultimo pannello di un modulo adattivo. Può essere il secondo ultimo pannello solo quando l’ultimo pannello contiene il passaggio Riepilogo.
   >* Il pannello contenente il componente del passaggio Firma o Riepilogo non può contenere altri componenti.
   >* I moduli adattivi contenenti il passaggio di firma non possono avere un pulsante di invio.
   >* L’invio dei moduli adattivi contenenti la fase Firma viene gestito tramite un servizio in background o la fase Riepilogo. Se esiste un firmatario configurato che compila anche il modulo, il vantaggio di gestire l’invio del modulo adattivo utilizzando il passaggio di riepilogo è che valuta immediatamente che il firmatario ha firmato il modulo e richiama l’azione di invio. Un servizio in background impiega più tempo per valutare se tutti i firmatari configurati hanno firmato il modulo e ritarda l’invio del modulo adattivo.
   >* Progettare il modulo in modo da non consentire a un utente di tornare da un pannello contenente il passaggio Firma o Riepilogo.


### Configurare il componente per la pagina di ringraziamento o il passaggio di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

Il componente **Passaggio di riepilogo** invia automaticamente il modulo, compila le informazioni all&#39;interno della pagina di riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Ottiene anche le informazioni richieste nella mappa di ritorno. Il componente Passaggio di riepilogo occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di riepilogo.

Ora l’esperienza di firma dei moduli in è pronta. Puoi visualizzare in anteprima il modulo per verificare l’esperienza di firma.

## Domande frequenti {#frequently-asked-questions}

**Q:** È possibile incorporare un modulo adattivo in un altro modulo adattivo. Il modulo adattivo incorporato può essere abilitato per [!DNL Adobe Sign]?
**Ans:** No, AEM [!DNL Forms] non supporta l&#39;utilizzo di un modulo adattivo che incorpora un modulo adattivo abilitato per [!DNL Adobe Sign] per la firma

**Q:** Quando creo un modulo adattivo utilizzando il modello avanzato e lo apro per la modifica, viene visualizzato un messaggio di errore di tipo &quot;Firmatario o firma elettronica non configurata correttamente&quot;. viene visualizzato. Come si risolve il messaggio di errore?
**Ans:** Il modulo adattivo creato utilizzando il modello avanzato è configurato per l&#39;utilizzo di [!DNL Adobe Sign]. Per risolvere l&#39;errore, creare e selezionare una configurazione cloud [!DNL Adobe Sign] e configurare un firmatario [!DNL Adobe Sign] per il modulo adattivo.

**Q:** posso utilizzare [!DNL Adobe Sign] tag di testo in un componente di testo statico di un modulo adattivo?
**Ans:** Sì, puoi utilizzare i tag di testo in un componente di testo per aggiungere [!DNL Adobe Sign] campi a un [documento di record](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (solo opzione per documento di record generato automaticamente) modulo adattivo abilitato. Per informazioni sulla procedura e sulle regole per la creazione di un tag di testo, consulta la [documentazione di Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Inoltre, i moduli adattivi hanno un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi supportati da [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**Q:** L&#39;AEM [!DNL Forms] fornisce sia [!UICONTROL il blocco Adobe Sign] che i componenti del passaggio di firma. Possono essere utilizzate simultaneamente in un modulo adattivo?
**Ans:** È possibile utilizzare entrambi i componenti contemporaneamente in un modulo. Di seguito sono riportati alcuni consigli per l’utilizzo di questi componenti:

**Blocco Adobe Sign:** Puoi utilizzare il [!UICONTROL Blocco Adobe Sign] per aggiungere [!UICONTROL Campi Adobe Sign] in qualsiasi punto del modulo adattivo. Consente inoltre di assegnare campi specifici ai firmatari. Per impostazione predefinita, quando un modulo adattivo viene visualizzato in anteprima o pubblicato, il blocco [!UICONTROL Adobe Sign] non è visibile. Questi blocchi sono attivati solo nel documento di firma. Nel documento di firma vengono abilitati solo i campi assegnati a un firmatario. Il blocco [!UICONTROL Adobe Sign] può essere utilizzato con il primo e i successivi firmatari.

**Componente passaggio firma:** È possibile utilizzare il componente passaggio firma per creare un&#39;esperienza di firma interna ai moduli. Consente solo al primo firmatario di firmare mentre il modulo viene compilato. Quando viene eseguito il rendering della sezione contenente il componente Passaggio di firma, viene visualizzata una versione del modulo firmata da PDF. In genere si tratta dell’ultima o penultima sezione seguita dal componente di riepilogo di un modulo.

## Risoluzione dei problemi {#troubleshoot}

### [!DNL Adobe Sign] errori contratto {#adobe-sign-agreement-failures}

**Problema**
Quando il servizio [!DNL Adobe Sign] è configurato per un modulo adattivo, non riesce a creare un contratto [!DNL Adobe Sign] per il modulo adattivo sottostante.

**Risoluzione**

* Controlla la [configurazione di Adobe Sign Cloud Service](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilizzata nel modulo adattivo.
* Verificare che l&#39;applicazione API nel server [!DNL Adobe Sign] utilizzata per configurare il servizio cloud [!DNL Adobe Sign] disponga delle autorizzazioni necessarie.
* Se utilizzi più servizi cloud [!DNL Adobe Sign], punta l&#39;**[!UICONTROL URL oAuth]** di tutti i servizi allo stesso **[!UICONTROL Adobe Sign Shard]**.

* Utilizzare indirizzi di posta elettronica separati per configurare l&#39;account [!DNL Adobe Sign] e per il primo firmatario e il singolo firmatario. L&#39;indirizzo di posta elettronica del primo firmatario o dell&#39;unico firmatario (se è presente il firmatario singolo) non può essere identico all&#39;account [!DNL Adobe Sign] utilizzato per configurare i servizi cloud AEM.

### Il flusso di lavoro AEM [!DNL Forms] configurato per un modulo adattivo abilitato per [!DNL Adobe Sign] non si avvia {#adobe-sign-aem-form-workflow-failures}

**Problema**
Quando [!DNL Adobe Sign] è configurato per un modulo adattivo, il flusso di lavoro configurato utilizzando l&#39;opzione Richiama flusso di lavoro [!DNL Forms] non si avvia.

**Risoluzione**

* Quando si utilizza [!DNL Adobe Sign] senza il passaggio di firma o il modulo richiede la firma di più persone, il server AEM [!DNL Forms] attende che l&#39;utilità di pianificazione confermi che tutte le persone hanno firmato il modulo. Il modulo adattivo viene inviato dal modulo di pianificazione solo dopo che tutte le persone hanno completato la firma e il flusso di lavoro inizia solo dopo l’invio corretto del modulo adattivo. È possibile abbreviare l&#39;intervallo della [pianificazione](adobe-sign-integration-adaptive-forms.md) per controllare lo stato della firma del modulo a intervalli rapidi e velocizzare l&#39;invio del modulo.


## Articoli correlati {#related-articles}

* [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Best practice per l&#39;utilizzo di Adobe Sign con moduli adattivi](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
