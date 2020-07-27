---
title: Configurazione dell’azione Invia
seo-title: Configurazione dell’azione Invia
description: I AEM Forms consentono di configurare un'azione di invio per definire il modo in cui un modulo adattivo viene elaborato dopo l'invio. È possibile utilizzare azioni di invio integrate o scrivere azioni personalizzate da zero.
seo-description: I AEM Forms consentono di configurare un'azione di invio per definire il modo in cui un modulo adattivo viene elaborato dopo l'invio. È possibile utilizzare azioni di invio integrate o scrivere azioni personalizzate da zero.
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 1%

---


# Configurazione dell’azione Invia{#configuring-the-submit-action}

## Introduzione all&#39;invio di azioni {#introduction-to-submit-actions}

Un&#39;azione di invio viene attivata quando l&#39;utente fa clic sul pulsante Invia di un modulo adattivo. È possibile configurare l&#39;azione di invio sul modulo adattivo. I moduli adattivi forniscono alcune delle azioni di invio previste. È possibile copiare ed estendere le azioni di invio predefinite per creare una propria azione di invio. Tuttavia, in base alle esigenze dell&#39;utente, è possibile scrivere e registrare una propria azione di invio per elaborare i dati nel modulo inviato. L&#39;azione di invio può utilizzare l&#39;invio [](../../forms/using/asynchronous-submissions-adaptive-forms.md)sincrono o asincrono.

È possibile configurare un&#39;azione di invio nella sezione **Invio** delle proprietà Contenitore modulo adattivo, nella barra laterale.

![Configura azione di invio](assets/thank-you-setting.png)

Configura azione di invio

Le azioni di invio predefinite disponibili con i moduli adattivi sono:

* Invia a endpoint REST
* Invia e-mail
* Invia PDF tramite e-mail
* Richiama un flusso di lavoro moduli
* Invia usando il modello dati modulo
* Azione di invio del portale Forms
* Richiamo di un flusso di lavoro AEM

>[!NOTE]
>
>L&#39;azione Invia PDF tramite e-mail è applicabile solo ai moduli adattivi che utilizzano il modello XFA come modello di modulo.

>[!NOTE]
>
>Accertatevi che [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>esiste. La directory è necessaria per memorizzare temporaneamente gli allegati. Se la directory non esiste, createla.

>[!CAUTION]
>
>Se si [precompila](../../forms/using/prepopulate-adaptive-form-fields.md) un modello di modulo, un modello di dati o un modulo adattivo basato su schema con un reclamo di dati XML o JSON a uno schema (schema XML, schema JSON, modello di modulo o modello di dati di modulo) che non contiene i tag &lt;afData>, &lt;afBoundData> e &lt;/afUnboundData>, i dati dei campi non associati (campi non associati sono campi adattivi) senza campi modulo. proprietà [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) ) del modulo adattivo viene perso.

È possibile scrivere un&#39;azione di invio personalizzata per i moduli adattivi per soddisfare le esigenze d&#39;uso. Per ulteriori informazioni, vedere [Scrittura di un&#39;azione di invio personalizzata per i moduli](../../forms/using/custom-submit-action-form.md)adattivi.

## Invia a endpoint REST {#submit-to-rest-endpoint}

L&#39;opzione di invio **Invia a endpoint** REST passa i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Potete aggiungere il nome dei campi da richiedere. Il formato della richiesta è:

`{fieldName}={request parameter name}`

Come illustrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con valori copiati dai campi **textbox** e **numericbox** per l&#39;azione successiva.

Potete anche **abilitare la richiesta** POST e fornire un URL per inviare la richiesta. Per inviare dati al server AEM che ospita il modulo, usa un percorso relativo corrispondente al percorso principale del server AEM. Ad esempio, /content/forms/af/SampleForm.html. Per inviare dati a qualsiasi altro server, utilizzare il percorso assoluto.

![Configurazione dell&#39;azione di invio dell&#39;endpoint rimanente](assets/action-config.png)

Configurazione dell&#39;azione di invio dell&#39;endpoint rimanente

>[!NOTE]
Per trasmettere i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati in pannelli diversi.

### Invia i dati inviati a una risorsa o a un punto finale di riposo esterno  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Utilizzare l&#39;azione **Invia a endpoint** REST per inviare i dati inviati a un URL rimanente. L&#39;URL può essere di un server interno (il server su cui viene eseguito il rendering del modulo) o di un server esterno.

Per inviare i dati a un server interno, fornire il percorso della risorsa. I dati vengono inviati nel percorso della risorsa. Ad esempio, /content/restEndPoint. Per tali richieste di post, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

Per inviare dati a un server esterno, immetti un URL. Il formato dell’URL è https://host:port/path_to_rest_end_point. Accertatevi di configurare il percorso per gestire la richiesta POST in modo anonimo.

![Mapping dei valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

Nell&#39;esempio precedente, le informazioni immesse dall&#39;utente in `textbox` vengono acquisite utilizzando il parametro `param1`. Sintassi per registrare i dati acquisiti tramite `param1` è:

`String data=request.getParameter("param1");`

Analogamente, i membri utilizzati per inviare dati e allegati XML sono `dataXml` e `attachments`.

Ad esempio, è possibile utilizzare questi due parametri nello script per analizzare i dati in un punto finale rimanente. È possibile utilizzare la sintassi seguente per memorizzare e analizzare i dati:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

In questo esempio `data` vengono memorizzati i dati XML e `att` i dati degli allegati.

## Invia e-mail {#send-email}

L&#39;azione **Invia e-mail** invia un messaggio e-mail a uno o più destinatari dopo l&#39;invio corretto del modulo. L&#39;e-mail generata può contenere dati del modulo in un formato predefinito.

>[!NOTE]
Tutti i campi modulo devono avere nomi di elementi diversi, anche se si trovano in pannelli diversi), per l’inclusione dei dati del modulo in un messaggio e-mail.

## Send PDF via Email {#send-pdf-via-email}

L&#39;azione **Invia PDF tramite e-mail** invia un messaggio e-mail contenente i dati del modulo a uno o più destinatari dopo l&#39;invio corretto del modulo.

>[!NOTE]
Questa azione di invio è disponibile per i moduli adattivi basati su XFA e per i moduli di adattamento basati su XSD con modello Documento di record.

## Invoke a forms workflow {#invoke-a-forms-workflow}

L&#39;opzione di invio del flusso di lavoro **** Invia a Forms invia un file xml di dati ed eventuali allegati a un eventuale processo Adobe LiveCycle o a AEM Forms esistenti in un processo JEE.

Per informazioni su come configurare l&#39;azione di invio del flusso di lavoro Invia ai moduli, vedere [Invio ed elaborazione dei dati del modulo mediante i flussi di lavoro](../../forms/using/submit-form-data-livecycle-process.md)dei moduli.

## Invia usando il modello dati modulo {#submit-using-form-data-model}

L&#39;azione di invio **Invia utilizzando il modello** dati del modulo scrive i dati del modulo adattivo inviati per l&#39;oggetto modello dati specificato in un modello dati del modulo alla relativa origine dati. Durante la configurazione dell&#39;azione di invio, è possibile scegliere un oggetto modello dati di cui si desidera riscrivere i dati inviati nell&#39;origine dati.

È inoltre possibile inviare all&#39;origine dati un allegato del modulo utilizzando un modello dati del modulo e un documento record (DoR).

Per informazioni sul modello dati del modulo, vedere Integrazione dei dati [AEM Forms](../../forms/using/data-integration.md).

## Azione di invio del portale Forms {#forms-portal-submit-action}

L&#39;opzione Invia azione **per** Forms Portal rende i dati del modulo disponibili tramite un portale AEM Forms.

Per ulteriori informazioni sul portale dei moduli e sull&#39;azione di invio, vedere [Bozze e componenti](../../forms/using/draft-submission-component.md)di invio.

## Invoke an AEM Workflow {#invoke-an-aem-workflow}

L’azione **Richiama un flusso di lavoro** AEM consente di associare un modulo adattivo a un flusso di lavoro AEM. Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente sul nodo di elaborazione. Inoltre, posiziona il file di dati, gli allegati e il documento di registrazione, se applicabile, nel percorso di payload del flusso di lavoro.

Prima di usare l’azione di invio **Richiama un flusso di lavoro** AEM, [configura le impostazioni](../../forms/using/configuring-the-processing-server-url-.md)di AEM DS. Per informazioni sulla creazione di un flusso di lavoro AEM, consultate Flussi di lavoro incentrati sui [moduli in OSGi](../../forms/using/aem-forms-workflow.md).

## Ripristino lato server nel modulo adattivo {#server-side-revalidation-in-adaptive-form}

In genere, in qualsiasi sistema di acquisizione dei dati online, gli sviluppatori inseriscono alcune convalide JavaScript sul lato client per applicare alcune regole aziendali. Tuttavia, nei browser più recenti, gli utenti finali hanno modo di bypassare tali convalide e di effettuare manualmente gli invii utilizzando varie tecniche, come ad esempio Web Browser DevTools Console. Tali tecniche sono valida anche per i moduli adattivi. Gli sviluppatori di moduli possono creare diversi logici di convalida, ma tecnicamente gli utenti finali possono ignorare tali logici di convalida e inviare al server dati non validi. Dati non validi potrebbero interrompere le regole aziendali applicate dall&#39;autore di un modulo.

La funzione di ripristino lato server consente inoltre di eseguire le convalide fornite da un autore di moduli adattivi durante la progettazione di un modulo adattivo sul server. Impedisce qualsiasi compromesso nell&#39;invio di dati e nelle violazioni delle regole aziendali rappresentate in termini di convalida dei moduli.

### Cosa convalidare sul server? {#what-to-validate-on-server-br}

Tutte le convalide dei campi (OOTB) di un modulo adattivo eseguite nuovamente sul server sono:

* Obbligatorio
* Convalida dell&#39;immagine
* Espressione di convalida

### Abilitazione della convalida lato server {#enabling-server-side-validation-br}

Per attivare o disattivare la convalida lato server per il modulo corrente, utilizzare **Revoca sul server** in Contenitore modulo adattivo nella barra laterale.

![Abilitazione della convalida lato server](assets/revalidate-on-server.png)

Abilitazione della convalida lato server

Se l&#39;utente finale bypassa tali convalide e invia i moduli, il server esegue di nuovo la convalida. Se la convalida ha esito negativo alla fine del server, la transazione di invio viene arrestata. All&#39;utente finale viene nuovamente presentato il modulo originale. I dati acquisiti e inviati vengono presentati all&#39;utente come un errore.

### Supporto delle funzioni personalizzate nelle espressioni di convalida {#supporting-custom-functions-in-validation-expressions-br}

In alcuni casi, in caso di regole **di convalida** complesse, lo script di convalida esatto risiede in funzioni personalizzate e l&#39;autore chiama queste funzioni personalizzate dall&#39;espressione di convalida del campo. Per rendere questa libreria di funzioni personalizzata nota e disponibile durante l&#39;esecuzione di convalide sul lato server, l&#39;autore del modulo può configurare il nome della libreria client AEM nella scheda **Base** delle proprietà Contenitore di moduli adattivi, come illustrato di seguito.

![Supporto delle funzioni personalizzate nelle espressioni di convalida](assets/clientlib-cat.png)

Supporto delle funzioni personalizzate nelle espressioni di convalida

L&#39;autore può configurare la libreria JavaScript personalizzata per ciascun modulo adattivo. Nella libreria, mantenere solo le funzioni riutilizzabili, che dipendono dalle librerie di terze parti jquery e underscore.js.

## Gestione degli errori durante l&#39;azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida sulla protezione e l’indurimento di AEM, configura pagine di errore personalizzate come 404.jsp e 500.jsp. Questi gestori vengono chiamati quando si invia un modulo 404 o 500 errori. I gestori vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Pubblica.

Per ulteriori informazioni, vedere [Personalizzazione delle pagine mostrate dal gestore](/help/sites-developing/customizing-errorhandler-pages.md)errori.
