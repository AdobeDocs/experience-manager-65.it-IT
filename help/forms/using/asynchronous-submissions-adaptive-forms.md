---
title: Invio asincrono di moduli adattivi
seo-title: Invio asincrono di moduli adattivi
description: Informazioni su come configurare l'invio asincrono per i moduli adattivi.
seo-description: Informazioni su come configurare l'invio asincrono per i moduli adattivi.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# Invio asincrono di moduli adattivi{#asynchronous-submission-of-adaptive-forms}

Tradizionalmente, i moduli Web sono configurati per l&#39;invio sincrono. Nell&#39;invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento o, in caso di invio non riuscito, a una pagina di errore. Tuttavia, esperienze Web moderne come applicazioni a pagina singola stanno acquisendo sempre maggiore popolarità, dove la pagina Web rimane statica mentre l&#39;interazione client-server avviene in background. È ora possibile fornire questa esperienza con i moduli adattivi configurando l&#39;invio asincrono.

Nell&#39;invio asincrono, quando un utente invia un modulo, lo sviluppatore del modulo inserisce un&#39;esperienza separata, come il reindirizzamento ad un altro modulo o a una sezione separata del sito Web. L&#39;autore può inoltre collegare servizi separati come l&#39;invio di dati a un archivio dati diverso o l&#39;aggiunta di un motore di analisi personalizzato. In caso di invio asincrono, un modulo adattivo si comporta come un&#39;applicazione a pagina singola, in quanto il modulo non viene ricaricato o il relativo URL non viene modificato quando i dati del modulo inviato vengono convalidati sul server.

Per ulteriori informazioni sull&#39;invio asincrono nei moduli adattivi, consultare il documento.

## Configurare l&#39;invio asincrono {#configure}

Per configurare l&#39;invio asincrono per un modulo adattivo:

1. In modalità di creazione moduli adattivi, selezionare l&#39;oggetto Contenitore modulo e toccare ![cmppr1](assets/cmppr1.png) per aprirne le proprietà.
1. Nella sezione Proprietà **[!UICONTROL invio]** , abilitare **[!UICONTROL Usa invio]** asincrono.
1. Nella sezione **[!UICONTROL Al momento dell&#39;invio]** , selezionare una delle opzioni seguenti da eseguire in caso di invio corretto del modulo.

   * **[!UICONTROL Reindirizza a URL]**: Reindirizza all&#39;URL o alla pagina specificati all&#39;invio del modulo. Potete specificare un URL o individuare il percorso di una pagina nel campo URL/percorso **[!UICONTROL di]** reindirizzamento.
   * **[!UICONTROL Mostra messaggio]**: Visualizza un messaggio all&#39;invio del modulo. È possibile scrivere un messaggio nel campo di testo sotto l&#39;opzione Mostra messaggio. Il campo di testo supporta la formattazione RTF.

1. Toccate ![check-button1](assets/check-button1.png) per salvare le proprietà.

## Funzionamento dell&#39;invio asincrono {#how-asynchronous-submission-works}

I AEM Forms forniscono gestori di errori e di successo out-of-the-box per l&#39;invio dei moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull&#39;evento success o error per l&#39;invio. Le informazioni vengono trasmesse come parametri al gestore interessato per eseguire la funzione.

Inoltre, autori e sviluppatori di moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. Per ulteriori informazioni, vedere [Ignorare i gestori predefiniti utilizzando le regole](#custom).

Esaminiamo innanzitutto la risposta del server per gli eventi di successo e di errore.

### Risposta del server per l&#39;evento di successo invio {#server-response-for-submission-success-event}

La struttura per la risposta del server per l&#39;evento di successo dell&#39;invio è la seguente:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

La risposta del server in caso di invio corretto del modulo include:

* Tipo formato dati modulo: XML o JSON
* Dati del modulo in formato XML o JSON
* Opzione selezionata per reindirizzare a una pagina o visualizzare un messaggio come configurato nel modulo
* URL pagina o contenuto del messaggio come configurato nel modulo

Il gestore di eventi di successo legge la risposta del server e reindirizza quindi all&#39;URL di pagina configurato o visualizza un messaggio.

### Risposta del server all&#39;evento di errore di invio {#server-response-for-submission-error-event}

La struttura per la risposta del server all&#39;evento di errore di invio è la seguente:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

La risposta del server in caso di errore nell&#39;invio del modulo include:

* Motivo dell’errore, convalida CAPTCHA non riuscita o convalida lato server
* Elenco di oggetti errore, che include l&#39;espressione SOM del campo con errore di convalida e il messaggio di errore corrispondente

Il gestore errori legge la risposta del server e visualizza di conseguenza il messaggio di errore sul modulo.

## Ignorare i gestori predefiniti utilizzando le regole {#custom}

Gli sviluppatori di moduli e gli autori possono scrivere regole, a livello di modulo, nell&#39;editor di codice per ignorare i gestori predefiniti. La risposta del server per gli eventi di successo e di errore è esposta a livello di modulo, a cui gli sviluppatori possono accedere utilizzando `$event.data` nelle regole.

Effettuate le seguenti operazioni per scrivere le regole nell&#39;editor di codice per gestire gli eventi di successo e di errore.

1. Aprite il modulo adattivo in modalità di creazione, selezionate un oggetto modulo qualsiasi e toccate ![edit-rules1](assets/edit-rules1.png) per aprire l&#39;editor di regole.
1. Selezionare **[!UICONTROL Modulo]** nella struttura Oggetti modulo e toccare **[!UICONTROL Crea]**.
1. Selezionate Editor **[!UICONTROL di]** codice dal menu a discesa di selezione della modalità.
1. Nell&#39;editor di codice, tocca **[!UICONTROL Modifica codice]**. Toccate **[!UICONTROL Modifica]** nella finestra di dialogo di conferma.
1. Scegliete **[!UICONTROL Invio]** o **[!UICONTROL Errore nell&#39;invio]** dall&#39;elenco a discesa **[!UICONTROL Evento]** .
1. Scrivete una regola per l&#39;evento selezionato e toccate **[!UICONTROL Fine]** per salvare la regola.

