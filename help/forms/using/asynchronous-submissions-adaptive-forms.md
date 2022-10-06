---
title: Invio asincrono di moduli adattivi
seo-title: Asynchronous submission of adaptive forms
description: Scopri come configurare l’invio asincrono per i moduli adattivi.
seo-description: Learn to configure asynchronous submission for adaptive forms.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
feature: Adaptive Forms
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Invio asincrono di moduli adattivi{#asynchronous-submission-of-adaptive-forms}

In genere, i moduli web sono configurati per l’invio in modo sincrono. Nell’invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento o in caso di errore di invio, a una pagina di errore. Tuttavia, le moderne esperienze web come le applicazioni a pagina singola stanno guadagnando popolarità laddove la pagina web rimane statica mentre l&#39;interazione client-server avviene in background. È ora possibile fornire questa esperienza con i moduli adattivi configurando l’invio asincrono.

Nell’invio asincrono, quando un utente invia un modulo, lo sviluppatore del modulo inserisce un’esperienza separata, come il reindirizzamento ad un altro modulo o a una sezione separata del sito web. L’autore può anche collegare servizi separati come l’invio di dati a un archivio dati diverso o aggiungere un motore di analisi personalizzato. In caso di invio asincrono, un modulo adattivo si comporta come un’applicazione a pagina singola, in quanto il modulo non viene ricaricato o il relativo URL non cambia quando i dati del modulo inviati vengono convalidati sul server.

Continua a leggere per i dettagli sull’invio asincrono nei moduli adattivi.

## Configurare l’invio asincrono {#configure}

Per configurare l’invio asincrono per un modulo adattivo:

1. In modalità di creazione dei moduli adattivi, seleziona l’oggetto Contenitore modulo e tocca ![cmppr1](assets/cmppr1.png) per aprire le relative proprietà.
1. In **[!UICONTROL Invio]** sezione proprietà, abilita **[!UICONTROL Utilizzare l’invio asincrono]**.
1. In **[!UICONTROL Al momento dell’invio]** selezionare una delle opzioni seguenti da eseguire in caso di invio corretto del modulo.

   * **[!UICONTROL Reindirizzare a URL]**: Reindirizza all’URL o alla pagina specificati all’invio del modulo. Puoi specificare un URL o sfogliare per scegliere il percorso di una pagina nel **[!UICONTROL URL/percorso di reindirizzamento]** campo .
   * **[!UICONTROL Mostra messaggio]**: Visualizza un messaggio all’invio del modulo. Puoi scrivere un messaggio nel campo di testo sotto l’opzione Mostra messaggio . Il campo di testo supporta la formattazione RTF.

1. Tocca ![pulsante di spunta1](assets/check-button1.png) per salvare le proprietà.

## Funzionamento dell’invio asincrono {#how-asynchronous-submission-works}

AEM Forms fornisce gestori di errori e di successo preconfigurati per l’invio dei moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento riuscito o di errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione .

Inoltre, gli autori e gli sviluppatori dei moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. Per ulteriori informazioni, consulta [Ignora gestori predefiniti utilizzando le regole](#custom).

Esaminiamo innanzitutto la risposta del server per gli eventi di successo ed errore.

### Risposta del server per l&#39;invio dell&#39;evento di successo {#server-response-for-submission-success-event}

La struttura della risposta del server per l’evento di successo dell’invio è la seguente:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

La risposta del server in caso di invio corretto del modulo include:

* Tipo di formato dei dati del modulo: XML o JSON
* Dati modulo in formato XML o JSON
* Opzione selezionata per reindirizzare a una pagina o visualizzare un messaggio come configurato nel modulo
* URL della pagina o contenuto del messaggio configurato nel modulo

Il gestore di successo legge la risposta del server e quindi reindirizza all’URL della pagina configurato o visualizza un messaggio.

### Risposta del server all’evento di errore di invio {#server-response-for-submission-error-event}

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

La risposta del server in caso di errore nell’invio del modulo include:

* Motivo dell’errore, convalida CAPTCHA non riuscita o convalida lato server
* Elenco degli oggetti errore, che include l&#39;espressione SOM del campo che non ha superato la convalida e il messaggio di errore corrispondente

Il gestore errori legge la risposta del server e visualizza di conseguenza il messaggio di errore sul modulo.

## Ignora gestori predefiniti utilizzando le regole {#custom}

Gli sviluppatori e gli autori di moduli possono scrivere regole a livello di modulo nell’editor di codice per ignorare i gestori predefiniti. La risposta del server per gli eventi di successo ed errore è esposta a livello di modulo, a cui gli sviluppatori possono accedere utilizzando `$event.data` nelle regole.

Esegui i seguenti passaggi per scrivere regole nell&#39;editor di codice per gestire eventi di successo ed errore.

1. Apri il modulo adattivo in modalità di creazione, seleziona un oggetto modulo qualsiasi e tocca ![edit-rules1](assets/edit-rules1.png) per aprire l’editor di regole.
1. Seleziona **[!UICONTROL Modulo]** nell’albero Oggetti modulo e toccare **[!UICONTROL Crea]**.
1. Seleziona **[!UICONTROL Editor di codice]** dal menu a discesa selezione modalità.
1. Nell’editor di codice, tocca **[!UICONTROL Modifica codice]**. Tocca **[!UICONTROL Modifica]** nella finestra di dialogo di conferma.
1. Scegli **[!UICONTROL Invio riuscito]** o **[!UICONTROL Errore nell&#39;invio]** dal **[!UICONTROL Evento]** a discesa.
1. Scrivere una regola per l’evento selezionato e toccare **[!UICONTROL Fine]** per salvare la regola.
