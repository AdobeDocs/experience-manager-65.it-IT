---
title: Configurazione dell’azione Invia
description: Forms consente di configurare un’azione di invio per definire come viene elaborato un modulo adattivo dopo l’invio. Puoi utilizzare azioni di invio incorporate o scriverne una da zero.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2593'
ht-degree: 3%

---

# Configurazione dell’azione Invia {#configuring-the-submit-action}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html) |
| AEM 6.5 | Questo articolo |


## Introduzione all’invio di azioni {#introduction-to-submit-actions}

Un’azione di invio viene attivata quando un utente fa clic sul pulsante Invia in un modulo adattivo. Puoi configurare l’azione di invio per il modulo adattivo. I moduli adattivi forniscono alcune azioni di invio pronte all’uso. Puoi copiare ed estendere le azioni di invio predefinite per creare un’azione di invio personalizzata. Tuttavia, in base alle tue esigenze, puoi scrivere e registrare la tua azione di invio per elaborare i dati nel modulo inviato. L&#39;azione di invio può utilizzare [invio sincrono o asincrono](../../forms/using/asynchronous-submissions-adaptive-forms.md).

Puoi configurare un’azione di invio nella sezione **Invio** delle proprietà Contenitore modulo adattivo nella barra laterale.

![Configura azione di invio](assets/thank-you-setting.png)

Configura azione di invio

Le azioni di invio predefinite disponibili con i moduli adattivi sono:

* Invia all’endpoint REST
* Invia e-mail
* Invia PDF tramite e-mail
* Richiama un Forms Workflow
* Invia usando il modello dati modulo
* Azione di invio Forms Portal
* Richiama un flusso di lavoro AEM
* Invia a Power Automate

>[!NOTE]
>
>L’azione Invia PDF tramite e-mail è applicabile solo ai moduli adattivi che utilizzano il modello XFA come modello di modulo.

>[!NOTE]
>
>Assicurati che la cartella [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM
>esiste. La directory è necessaria per archiviare temporaneamente gli allegati. Se la directory non esiste, creala.

>[!CAUTION]
>
>Se si [precompila](../../forms/using/prepopulate-adaptive-form-fields.md) un modello di modulo, un modello di dati modulo o un modulo adattivo basato su schema con dati XML o JSON in un reclamo a uno schema (schema XML, schema JSON, modello di modulo o modello di dati del modulo) contenente dati che non contengono tag &lt;afData>, &lt;afBoundData> e &lt;/afUnboundData>, i dati dei campi non associati (i campi non associati sono campi di modulo adattivo senza la proprietà [bindref](../../forms/using/prepopulate-adaptive-form-fields.md)) del modulo adattivo andranno persi.

Per soddisfare il tuo caso d’uso, puoi scrivere un’azione di invio personalizzata per i moduli adattivi. Per ulteriori informazioni, vedere [Scrittura di un&#39;azione di invio personalizzata per i moduli adattivi](../../forms/using/custom-submit-action-form.md).

## Invia all’endpoint REST {#submit-to-rest-endpoint}

L&#39;opzione di invio **Invia all&#39;endpoint REST** trasmette i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Puoi aggiungere il nome dei campi da richiedere. Il formato della richiesta è:

`{fieldName}={request parameter name}`

Come mostrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con valori copiati dai campi **textbox** e **numeric box** per l&#39;azione successiva.

Puoi anche **abilitare la richiesta di POST** e fornire un URL per pubblicare la richiesta. Per inviare i dati al server Experience Manager che ospita il modulo, utilizzare un percorso relativo corrispondente al percorso principale del server Experience Manager. Ad esempio, /content/forms/af/SampleForm.html. Per inviare dati a qualsiasi altro server, utilizzare il percorso assoluto.

![Configurazione dell&#39;azione di invio dell&#39;endpoint REST](assets/action-config.png)

Configurazione dell’azione di invio endpoint REST

>[!NOTE]
>
Per passare i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi.

### Post ha inviato dati a una risorsa o a un endpoint di riposo esterno  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Utilizzare l&#39;azione **Invia all&#39;endpoint REST** per inviare i dati inviati a un URL rest. L’URL può essere interno (il server sul quale viene eseguito il rendering del modulo) o esterno.

Per pubblicare i dati su un server interno, specifica il percorso della risorsa. I dati vengono inseriti nel percorso della risorsa. Ad esempio, /content/restEndPoint. Per tali richieste successive, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

Per pubblicare dati su un server esterno, fornisci un URL. Il formato dell’URL è https://host:port/path_to_rest_end_point. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

![Mappatura dei valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

Nell&#39;esempio precedente, le informazioni immesse dall&#39;utente in `textbox` vengono acquisite tramite il parametro `param1`. La sintassi per pubblicare i dati acquisiti tramite `param1` è:

`String data=request.getParameter("param1");`

Analogamente, i parametri utilizzati per la registrazione di dati e allegati XML sono `dataXml` e `attachments`.

Ad esempio, questi due parametri vengono utilizzati nello script per analizzare i dati in un punto finale rest. Utilizza la sintassi seguente per archiviare e analizzare i dati:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

In questo esempio, `data` memorizza i dati XML e `att` i dati dell&#39;allegato.

## Invia e-mail {#send-email}

L&#39;azione di invio **Invia e-mail** invia un&#39;e-mail a uno o più destinatari quando il modulo viene inviato correttamente. L’e-mail generata può contenere dati del modulo in un formato predefinito.

>[!NOTE]
>
Tutti i campi modulo devono avere nomi di elementi diversi, anche se sono inseriti in pannelli diversi), ad esempio per includere i dati del modulo in un messaggio e-mail.

## Invia PDF tramite e-mail {#send-pdf-via-email}

L&#39;azione di invio **Invia PDF tramite e-mail** invia un messaggio e-mail con un PDF contenente i dati del modulo a uno o più destinatari non appena il modulo viene inviato correttamente.

>[!NOTE]
>
Questa azione di invio è disponibile per i moduli adattivi basati su XFA e per i moduli di adattamento basati su XSD che dispongono del modello del documento di record.

## Richiama un Forms Workflow {#invoke-a-forms-workflow}

L&#39;opzione di invio **Invia al Forms Workflow** invia un file XML dati e gli eventuali allegati a un LiveCycle di Adobi o AEM Forms esistente in JEE.

Per informazioni su come configurare l&#39;azione Invia al Forms Workflow, vedere [Invio ed elaborazione dei dati del modulo tramite flussi di lavoro moduli](../../forms/using/submit-form-data-livecycle-process.md).

## Invia usando il modello dati modulo {#submit-using-form-data-model}

L&#39;azione di invio **Invia tramite modello dati modulo** scrive i dati del modulo adattivo inviati per l&#39;oggetto modello dati specificato in un modello dati modulo nella relativa origine dati. Durante la configurazione dell’azione di invio, puoi scegliere un oggetto modello dati di cui desideri riscrivere i dati inviati nella relativa origine dati.

Inoltre, è possibile inviare un allegato del modulo utilizzando un modello di dati del modulo e un documento di record (DoR) all’origine dati.

Per informazioni sul modello dati modulo, vedere [Integrazione dati AEM Forms](../../forms/using/data-integration.md).

## Azione di invio Forms Portal {#forms-portal-submit-action}

L&#39;opzione **Azione invio portale Forms** rende disponibili i dati del modulo tramite un portale AEM Forms.

Per ulteriori informazioni sul portale Forms e sull&#39;azione di invio, vedere [Componente bozze e invii](../../forms/using/draft-submission-component.md).

## Richiama un flusso di lavoro AEM {#invoke-an-aem-workflow}

L&#39;azione di invio **[!UICONTROL Richiama un flusso di lavoro AEM]** associa un modulo adattivo a un [flusso di lavoro AEM](/help/sites-developing/workflows-models.md). Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente nell’istanza Autore. Puoi salvare il file di dati, gli allegati e il documento di record nella cartella relativa o sotto il payload del flusso di lavoro o in una variabile. Se il flusso di lavoro è contrassegnato per l’archiviazione dati esterna, l’opzione della variabile è disponibile e non l’opzione payload. Puoi effettuare una selezione dall’elenco di variabili disponibili per il modello di flusso di lavoro. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni in una fase successiva e non al momento della creazione del flusso di lavoro, assicurati che siano presenti le configurazioni di variabili richieste.

Prima di utilizzare l&#39;azione di invio **Richiama un flusso di lavoro AEM**, [configura le impostazioni di Experience Manager DS](../../forms/using/configuring-the-processing-server-url.md). Per informazioni sulla creazione di un flusso di lavoro AEM, consulta [Flussi di lavoro incentrati sui moduli in OSGi](../../forms/using/aem-forms-workflow.md).

L’azione Invia inserisce quanto segue nella posizione del payload del flusso di lavoro. Tuttavia, se il modello di flusso di lavoro è contrassegnato per l’archiviazione dei dati esterni e non per l’opzione payload, viene visualizzata solo l’opzione Variabile.

* **File di dati**: contiene i dati inviati al modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso file dati]** per specificare il nome del file e il percorso del file relativo al payload. Il percorso `/addresschange/data.xml`, ad esempio, crea una cartella denominata `addresschange` e la inserisce in relazione al payload. È inoltre possibile specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle. Utilizza l’opzione variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

>[!NOTE]
>
Le variabili possono essere utilizzate indipendentemente dal fatto che il modello di flusso di lavoro sia contrassegnato o meno per l’archiviazione dati esterna.

* **Allegati**: è possibile utilizzare l&#39;opzione **[!UICONTROL Percorso allegato]** per specificare il nome della cartella in cui archiviare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

* **Documento record**: contiene il documento record generato per il modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso del documento record]** per specificare il nome del file del documento record e il percorso del file relativo al payload. Ad esempio, il percorso `/addresschange/DoR.pdf` crea una cartella denominata `addresschange` relativa al payload e inserisce `DoR.pdf` relativa al payload. È inoltre possibile specificare solo `DoR.pdf` per salvare solo il documento di record senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

## Invia a Power Automate {#microsoft-power-automate}

È possibile configurare un modulo adattivo per eseguire un flusso cloud di Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record al flusso cloud Power Automate per l’elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche di business basate sui dati acquisiti e automatizzare i flussi di lavoro dei clienti. Di seguito sono riportati alcuni esempi di cosa è possibile fare dopo l’integrazione di un modulo adattivo con Microsoft® Power Automate:

* Utilizzare dati Forms adattivi in processi aziendali Power Automate
* Utilizza Power Automate per inviare i dati acquisiti a più di 500 origini dati o a qualsiasi API disponibile pubblicamente
* Eseguire calcoli complessi sui dati acquisiti
* Salvataggio dei dati Adaptive Forms sui sistemi di storage secondo una pianificazione predefinita

L&#39;editor di Forms adattivo fornisce l&#39;azione di invio **Richiama un flusso Microsoft® Power Automate** per inviare dati di moduli adattivi, allegati e documenti di record al flusso cloud di Power Automate. Per utilizzare l&#39;azione Invia per inviare i dati acquisiti a Microsoft® Power Automate, [Connetti l&#39;istanza AEM Forms con Microsoft® Power Automate](/help/forms/using/forms-microsoft-power-automate-integration.md)

Dopo una configurazione corretta, utilizzare l&#39;azione di invio [Richiama un flusso Microsoft® Power Automate](/help/forms/using/forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) per inviare dati a un flusso Power Automate.

## Invia a Microsoft® SharePoint List{#submit-to-sharedrive}

>[!NOTE]
>
La funzione Submit to Microsoft® SharePoint List è stata introdotta con AEM 6.5 Forms Service Pack 19 (6.5.19.0).

L&#39;azione di invio **[!UICONTROL Invia a SharePoint]** collega un modulo adattivo a un archivio Microsoft® SharePoint. È possibile inviare il file di dati del modulo, gli allegati o il documento di record all&#39;archivio di Microsoft® Sharepoint connesso.

### Collegare un modulo adattivo all’elenco di Microsoft® SharePoint {#connect-af-sharepoint-list}

Per collegare un modulo adattivo a Microsoft® SharePoint List:

1. [Crea una configurazione elenco SharePoint](#create-sharepoint-list-configuration): connette AEM Forms all&#39;archiviazione elenco Microsoft® Sharepoint.
1. [Utilizza l&#39;azione di invio **Invia utilizzando il modello dati del modulo** in un modulo adattivo](#use-submit-using-fdm): invia i dati del modulo adattivo a Microsoft® SharePoint configurato.

#### Creare una configurazione dell’elenco SharePoint {#create-sharepoint-list-configuration}

Per collegare AEM Forms all’elenco di Microsoft® Sharepoint:

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Seleziona un **contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Elenco SharePoint]** dall&#39;elenco a discesa. Viene visualizzata la procedura guidata di configurazione di SharePoint.
1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l&#39;ID client, il segreto client e l&#39;ID tenant per l&#39;URL OAuth, consulta la [documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Puoi recuperare `Client ID` e `Client Secret` dell&#39;app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungere l&#39;URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l&#39;URL dell&#39;istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Sites.Manage.All` nella scheda **Microsoft® Graph** per fornire le autorizzazioni di lettura/scrittura. Aggiungere l&#39;autorizzazione `AllSites.Manage` nella scheda **Sharepoint** per interagire in remoto con i dati di SharePoint.
   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell&#39;app dal portale di Microsoft® Azure.

     >[!NOTE]
     >
     Il campo **segreto client** è obbligatorio oppure facoltativo in base alla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Fai clic su **[!UICONTROL Connetti]**. Se la connessione ha esito positivo, viene visualizzato il messaggio `Connection Successful`.
1. Selezionare **[!UICONTROL Sito SharePoint]** e **[!UICONTROL Elenco SharePoint]** dall&#39;elenco a discesa.
1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per Microsoft® SharePointList.

#### Utilizzare l’invio utilizzando il modello dati del modulo in un modulo adattivo {#use-submit-using-fdm}

È possibile utilizzare la configurazione dell’elenco SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in un elenco SharePoint. Per utilizzare una configurazione di archiviazione Elenco SharePoint in un modulo adattivo, effettua le seguenti operazioni:

1. [Creare un modello di dati modulo con Microsoft](/help/forms/using/create-form-data-model.md)
1. [Configurare il modello dati modulo per recuperare e inviare dati](/help/forms/using/work-with-form-data-model.md#configure-services)
1. [Crea un modulo adattivo](/help/forms/using/create-adaptive-form.md).
1. [Configurare l’azione di invio utilizzando un modello dati modulo](/help/forms/using/configuring-submit-actions.md#submit-using-form-data-model-submit)

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio elenco di Microsoft® Sharepoint specificato.

>[!NOTE]
>
In Microsoft® SharePoint List non sono supportati i seguenti tipi di colonna:
* colonna immagine
* colonna metadati
* colonna persona
* colonna di dati esterni


>[!NOTE]
>
Per impostare i valori di una configurazione, [Genera configurazioni OSGi utilizzando l&#39;SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [distribuisci la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) nell&#39;istanza di Cloud Service.

## Riconvalida lato server in modulo adattivo {#server-side-revalidation-in-adaptive-form}

In genere, in qualsiasi sistema di acquisizione dati online, gli sviluppatori inseriscono alcune convalide JavaScript sul lato client per applicare alcune regole di business. Tuttavia, nei browser moderni, gli utenti finali possono ignorare tali convalide ed effettuare manualmente gli invii utilizzando varie tecniche, ad esempio la Console per la creazione di strumenti di browser Web. Tali tecniche sono valide anche per i moduli adattivi. Uno sviluppatore di moduli può creare diverse logiche di convalida, ma tecnicamente gli utenti finali possono ignorarle e inviare dati non validi al server. I dati non validi violano le regole business applicate da un autore di moduli.

La funzione di riconvalida lato server consente inoltre di eseguire le convalide fornite da un autore di moduli adattivi durante la progettazione di un modulo adattivo sul server. Impedisce qualsiasi possibile compromissione dell’invio dei dati e delle violazioni delle regole aziendali rappresentate in termini di convalide dei moduli.

### Cosa convalidare su Server? {#what-to-validate-on-server-br}

Tutte le convalide predefinite dei campi di un modulo adattivo rieseguite sul server sono:

* Obbligatorio
* Clausola di convalida immagine
* Espressione di convalida

### Abilitazione della convalida lato server {#enabling-server-side-validation-br}

Utilizza **Riconvalida sul server** in Contenitore modulo adattivo nella barra laterale per abilitare o disabilitare la convalida lato server per il modulo corrente.

![Abilitazione della convalida lato server](assets/revalidate-on-server.png)

Abilitazione della convalida lato server

Se l&#39;utente finale ignora tali convalide e invia i moduli, il server esegue nuovamente la convalida. Se la convalida non riesce alla fine del server, la transazione di invio viene interrotta. All’utente finale viene nuovamente presentato il modulo originale. I dati acquisiti e inviati vengono presentati all’utente come un errore.

>[!NOTE]
>
La convalida lato server convalida il modello del modulo. Si consiglia di creare una libreria client separata per le convalide e non combinarla con altri elementi come lo stile HTML e la manipolazione DOM nella stessa libreria client.

### Supporto di funzioni personalizzate nelle espressioni di convalida {#supporting-custom-functions-in-validation-expressions-br}

Talvolta, in presenza di regole di convalida complesse, lo script di convalida esatto risiede in funzioni personalizzate e l’autore chiama tali funzioni personalizzate dall’espressione di convalida del campo. Per rendere nota e disponibile questa libreria di funzioni personalizzata durante l&#39;esecuzione delle convalide lato server, l&#39;autore del modulo può configurare il nome della libreria client AEM nella scheda **Base** delle proprietà del contenitore di moduli adattivi, come illustrato di seguito.

![Supporto di funzioni personalizzate nelle espressioni di convalida](assets/clientlib-cat.png)

Supporto di funzioni personalizzate nelle espressioni di convalida

L’autore può configurare una libreria JavaScript personalizzata per modulo adattivo. Si consiglia di mantenere solo le funzioni riutilizzabili nella libreria, che dipendono dalle librerie di terze parti jquery e underscore.js.

## Gestione degli errori durante l’azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida sulla sicurezza e l’irrigidimento di Experience Manager, configura pagine di errore personalizzate come 404.jsp e 500.jsp. Questi gestori vengono chiamati quando all’invio di un modulo vengono visualizzati errori 404 o 500. I gestori vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Publish.

Per ulteriori informazioni, vedere [Personalizzazione delle pagine visualizzate dal gestore degli errori](/help/sites-developing/customizing-errorhandler-pages.md).
