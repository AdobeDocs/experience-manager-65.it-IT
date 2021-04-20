---
title: Configurazione dell’azione Invia
seo-title: Configurazione dell’azione Invia
description: Forms consente di configurare un’azione di invio per definire la modalità di elaborazione di un modulo adattivo dopo l’invio. È possibile utilizzare azioni di invio integrate o creare azioni personalizzate da zero.
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 1%

---


# Configurazione dell’azione Invia{#configuring-the-submit-action}

## Introduzione all’invio di azioni {#introduction-to-submit-actions}

Un’azione di invio viene attivata quando l’utente fa clic sul pulsante Invia su un modulo adattivo. Puoi configurare l’azione di invio sul modulo adattivo. I moduli adattivi forniscono alcune azioni predefinite per l’invio di . È possibile copiare ed estendere le azioni di invio predefinite per creare una propria azione di invio. Tuttavia, in base alle tue esigenze, puoi scrivere e registrare una tua azione di invio per elaborare i dati nel modulo inviato. L&#39;azione di invio può utilizzare [invio sincrono o asincrono](../../forms/using/asynchronous-submissions-adaptive-forms.md).

Puoi configurare un’azione di invio nella sezione **Invio** delle proprietà del contenitore di modulo adattivo, nella barra laterale.

![Configurare l’azione Invia](assets/thank-you-setting.png)

Configurare l’azione Invia

Le azioni di invio predefinite disponibili con i moduli adattivi sono le seguenti:

* Invia all’endpoint REST
* Invia e-mail
* Invia PDF via e-mail
* Richiamare un Forms Workflow
* Invia usando il modello dati modulo
* Azione di invio Forms Portal
* Richiamare un flusso di lavoro AEM

>[!NOTE]
>
>L’azione Invia PDF tramite e-mail è applicabile solo ai moduli adattivi che utilizzano il modello XFA come modello di modulo.

>[!NOTE]
>
>Assicurati che [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>esiste. La directory è necessaria per memorizzare temporaneamente gli allegati. Se la directory non esiste, creala.

>[!CAUTION]
>
>Se si [precompila](../../forms/using/prepopulate-adaptive-form-fields.md) un modello di modulo, un modello di dati modulo o un modulo adattivo basato su schema con tag XML o JSON, si desidera segnalare a uno schema (schema XML, schema JSON, modello di modulo o modello di dati modulo) i cui dati non contengono tag &lt;afData>, &lt;afBoundData> e &lt;/afUnboundData>, i dati dei campi non associati (campi non delimitati) i campi modulo adattivo sono persi senza la proprietà [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) del modulo adattivo.

Puoi scrivere un’azione di invio personalizzata per i moduli adattivi per soddisfare il tuo caso d’uso. Per ulteriori informazioni, vedere [Scrittura di azioni di invio personalizzate per i moduli adattivi](../../forms/using/custom-submit-action-form.md).

## Invia all’endpoint REST {#submit-to-rest-endpoint}

L’opzione di invio **Invia a endpoint REST** trasmette i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Puoi aggiungere il nome dei campi da richiedere. Il formato della richiesta è:

`{fieldName}={request parameter name}`

Come mostrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con valori copiati dai campi **textbox** e **numeric box** per l&#39;azione successiva.

È inoltre possibile **Abilitare la richiesta di POST** e fornire un URL per inviare la richiesta. Per inviare dati al server Experience Manager che ospita il modulo, utilizzare un percorso relativo corrispondente al percorso principale del server Experience Manager. Ad esempio, /content/forms/af/SampleForm.html. Per inviare dati a qualsiasi altro server, utilizzare un percorso assoluto.

![Configurazione dell&#39;azione di invio dell&#39;endpoint rimanente](assets/action-config.png)

Configurazione dell&#39;azione di invio dell&#39;endpoint rimanente

>[!NOTE]
Per trasmettere i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi.

### Invia i dati a una risorsa o a un punto finale di riposo esterno  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Utilizza l&#39;azione **Invia a REST Endpoint** per inviare i dati inviati a un URL rimanente. L’URL può essere di un server interno (il server su cui viene eseguito il rendering del modulo) o di un server esterno.

Per inviare dati a un server interno, fornisci il percorso della risorsa. I dati vengono inviati nel percorso della risorsa. Ad esempio, /content/restEndPoint. Per tali richieste post, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

Per inviare dati a un server esterno, specifica un URL. Il formato dell’URL è https://host:port/path_to_rest_end_point. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

![Mappatura dei valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

Nell’esempio precedente, le informazioni immesse dall’utente in `textbox` vengono acquisite utilizzando il parametro `param1`. La sintassi per la pubblicazione dei dati acquisiti utilizzando `param1` è la seguente:

`String data=request.getParameter("param1");`

Analogamente, i parametri utilizzati per la registrazione di dati XML e allegati sono `dataXml` e `attachments`.

Ad esempio, è possibile utilizzare questi due parametri nello script per analizzare i dati in un punto finale residuo. Utilizza la sintassi seguente per memorizzare e analizzare i dati:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

In questo esempio, `data` memorizza i dati XML e `att` memorizza i dati allegati.

## Invia e-mail {#send-email}

L’azione di invio **Invia e-mail** invia un messaggio e-mail a uno o più destinatari dopo l’invio del modulo. L’e-mail generata può contenere dati del modulo in un formato predefinito.

>[!NOTE]
Per includere i dati del modulo in un messaggio e-mail, tutti i campi del modulo devono avere nomi di elementi diversi, anche se si trovano in pannelli diversi).

## Invia PDF tramite e-mail {#send-pdf-via-email}

L’azione **Invia PDF tramite e-mail** invia un’e-mail con un PDF contenente dati del modulo a uno o più destinatari dopo l’invio corretto del modulo.

>[!NOTE]
Questa azione di invio è disponibile per i moduli adattivi basati su XFA e per i moduli di adattamento basati su XSD che dispongono del modello Document of Record.

## Richiamare un Forms Workflow {#invoke-a-forms-workflow}

L&#39;opzione **Invia a Forms Workflow** invia un file xml di dati e allegati (se presenti) a un LiveCycle di Adobe esistente o ad AEM Forms su un processo JEE.

Per informazioni su come configurare l’azione Invia al Forms Workflow, vedere [Invio ed elaborazione dei dati del modulo tramite flussi di lavoro per moduli](../../forms/using/submit-form-data-livecycle-process.md).

## Invia usando il modello dati modulo {#submit-using-form-data-model}

L’azione di invio **Invia utilizzando Form Data Model** scrive i dati del modulo adattivo inviati per l’oggetto modello dati specificato in un modello dati modulo alla relativa origine dati. Durante la configurazione dell’azione di invio, è possibile scegliere un oggetto modello dati di cui si desidera riscrivere i dati inviati nella relativa origine dati.

È inoltre possibile inviare un allegato del modulo utilizzando un modello dati del modulo e un documento di record all’origine dati.

Per informazioni sul modello di dati del modulo, vedere [Integrazione dei dati di AEM Forms](../../forms/using/data-integration.md).

## Azione di invio del portale Forms {#forms-portal-submit-action}

L’opzione **Forms Portal Submit Action** rende i dati del modulo disponibili tramite un portale AEM Forms.

Per ulteriori informazioni sul portale Forms e sull&#39;azione di invio, consulta [Componente Bozze e invii](../../forms/using/draft-submission-component.md).

## Richiamare un flusso di lavoro AEM {#invoke-an-aem-workflow}

L&#39;azione **Richiama un flusso di lavoro AEM** invia associa un modulo adattivo a un flusso di lavoro AEM. Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente sul nodo di elaborazione. Inoltre, inserisce file di dati, allegati e documenti di record, se applicabile, nel percorso di payload del flusso di lavoro.

Prima di utilizzare l&#39;azione di invio **Richiama un flusso di lavoro AEM**, [configura le impostazioni di DS di Experience Manager](../../forms/using/configuring-the-processing-server-url-.md). Per informazioni sulla creazione di un flusso di lavoro AEM, consulta [Flussi di lavoro incentrati sui moduli su OSGi](../../forms/using/aem-forms-workflow.md).

## Rivalutazione lato server in forma adattiva {#server-side-revalidation-in-adaptive-form}

In genere, in qualsiasi sistema di acquisizione dati online, gli sviluppatori inseriscono alcune convalide JavaScript sul lato client per applicare alcune regole business. Ma nei browser moderni, gli utenti finali hanno modo di bypassare tali convalide e fare manualmente gli invii utilizzando varie tecniche, come ad esempio Web Browser DevTools Console. Tali tecniche sono valide anche per i moduli adattivi. Uno sviluppatore di moduli può creare diversi logici di convalida, ma tecnicamente, gli utenti finali possono ignorare tali logici di convalida e inviare dati non validi al server. Dati non validi potrebbero interrompere le regole business applicate da un autore di moduli.

La funzione di riconvalida lato server consente di eseguire anche le convalide fornite da un autore di moduli adattivi durante la progettazione di un modulo adattivo sul server. Impedisce qualsiasi possibile compromesso tra l’invio dei dati e le violazioni delle regole aziendali rappresentate in termini di convalida dei moduli.

### Cosa convalidare sul server? {#what-to-validate-on-server-br}

Tutte le convalide predefinite (OOTB) di un modulo adattivo che vengono ripetute sul server sono:

* Obbligatorio
* Clausola di convalida dell&#39;immagine
* Espressione di convalida

### Abilitazione della convalida lato server {#enabling-server-side-validation-br}

Per abilitare o disabilitare la convalida lato server per il modulo corrente, utilizza la funzione **Rivalida sul server** in Contenitore modulo adattivo nella barra laterale.

![Abilitazione della convalida lato server](assets/revalidate-on-server.png)

Abilitazione della convalida lato server

Se l’utente finale bypassa tali convalide e invia i moduli, il server esegue nuovamente la convalida. Se la convalida ha esito negativo al server, la transazione di invio viene arrestata. All’utente finale viene presentato nuovamente il modulo originale. I dati acquisiti e inviati vengono presentati all’utente come un errore.

>[!NOTE]
La convalida lato server convalida il modello di modulo. È consigliabile creare una libreria client separata per le convalide e non combinarla con altri elementi come lo stile HTML e la manipolazione DOM nella stessa libreria client.

### Supporto di funzioni personalizzate nelle espressioni di convalida {#supporting-custom-functions-in-validation-expressions-br}

In alcuni casi, in presenza di regole di convalida complesse, lo script di convalida esatto risiede in funzioni personalizzate e l’autore chiama queste funzioni personalizzate dall’espressione di convalida dei campi. Per rendere questa libreria di funzioni personalizzate nota e disponibile durante l’esecuzione delle convalide lato server, l’autore del modulo può configurare il nome AEM libreria client nella scheda **Base** delle proprietà Contenitore di moduli adattivi , come illustrato di seguito.

![Supporto di funzioni personalizzate nelle espressioni di convalida](assets/clientlib-cat.png)

Supporto di funzioni personalizzate nelle espressioni di convalida

L’autore può configurare una libreria JavaScript personalizzata per ciascun modulo adattivo. Nella libreria , mantieni solo le funzioni riutilizzabili, che dipendono dalle librerie di terze parti jquery e underscore.js.

## Gestione degli errori nell’azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida per la sicurezza e l’indurimento di Experience Manager, configura pagine di errore personalizzate come 404.jsp e 500.jsp. Quando si invia un modulo 404 o 500 vengono visualizzati errori, questi gestori vengono chiamati. I gestori vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Publish .

Per ulteriori informazioni, consulta [Personalizzazione delle pagine mostrate dal gestore errori](/help/sites-developing/customizing-errorhandler-pages.md).
