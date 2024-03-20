---
title: Invio asincrono di moduli adattivi
description: Scopri come configurare l’invio asincrono per i moduli adattivi.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Invio asincrono di moduli adattivi{#asynchronous-submission-of-adaptive-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html) |
| AEM 6.5 | Questo articolo |

In genere, i moduli web sono configurati per l’invio sincrono. Nell’invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento oppure, se l’invio non riesce, a una pagina di errore. Tuttavia, le moderne esperienze web come le applicazioni a pagina singola stanno guadagnando popolarità, dove la pagina web rimane statica mentre l’interazione client-server avviene in background. Ora puoi fornire questa esperienza con i moduli adattivi configurando l’invio asincrono.

Nell’invio asincrono, quando un utente invia un modulo, lo sviluppatore del modulo inserisce un’esperienza separata, ad esempio il reindirizzamento verso un altro modulo o una sezione separata del sito web. L’autore può anche inserire servizi separati come l’invio di dati a un altro archivio dati o aggiungere un motore di analisi personalizzato. In caso di invio asincrono, un modulo adattivo si comporta come un’applicazione a pagina singola poiché il modulo non viene ricaricato o il suo URL non cambia quando i dati del modulo inviati vengono convalidati sul server.

Continua a leggere per informazioni dettagliate sull’invio asincrono nei moduli adattivi.

## Configurare l’invio asincrono {#configure}

Per configurare l’invio asincrono per un modulo adattivo:

1. In modalità di authoring di moduli adattivi, seleziona l’oggetto Contenitore modulo e fai clic su ![cmppr1](assets/cmppr1.png) per aprirne le proprietà.
1. In **[!UICONTROL Invio]** proprietà, abilita **[!UICONTROL Utilizzare l’invio asincrono]**.
1. In **[!UICONTROL All’invio]** , selezionare una delle opzioni seguenti da eseguire in caso di invio corretto del modulo.

   * **[!UICONTROL Reindirizza a URL]**: reindirizza all’URL o alla pagina specificata al momento dell’invio del modulo. Puoi specificare un URL o sfogliare per scegliere il percorso di una pagina in **[!UICONTROL URL/percorso di reindirizzamento]** campo.
   * **[!UICONTROL Mostra messaggio]**: visualizza un messaggio all’invio del modulo. Puoi scrivere un messaggio nel campo di testo sotto l’opzione Mostra messaggio. Il campo di testo supporta la formattazione RTF.

1. Seleziona ![check-button1](assets/check-button1.png) per salvare le proprietà.

## Funzionamento dell’invio asincrono {#how-asynchronous-submission-works}

AEM Forms fornisce gestori predefiniti di successo e di errori per l’invio di moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento di successo o errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione.

Inoltre, gli autori e gli sviluppatori di moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. Per ulteriori informazioni, consulta [Ignora gestori predefiniti tramite regole](#custom).

Esaminiamo innanzitutto la risposta del server per gli eventi di successo e di errore.

### Risposta del server per l’evento di successo dell’invio {#server-response-for-submission-success-event}

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

* Tipo di formato dati modulo: XML o JSON
* Dati modulo in formato XML o JSON
* Opzione selezionata per reindirizzare a una pagina o visualizzare un messaggio come configurato nel modulo
* Contenuto dell’URL della pagina o del messaggio configurato nel modulo

Il gestore dei processi riusciti legge la risposta del server e di conseguenza reindirizza all’URL della pagina configurato o visualizza un messaggio.

### Risposta del server per l’evento di errore di invio {#server-response-for-submission-error-event}

La struttura della risposta del server per l’evento di errore di invio è la seguente:

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

* Motivo dell’errore, convalida CAPTCHA o lato server non riuscita
* Elenco di oggetti errore, che include l&#39;espressione SOM del campo che non ha superato la convalida e il messaggio di errore corrispondente

Il gestore degli errori legge la risposta del server e visualizza di conseguenza il messaggio di errore nel modulo.

## Ignora gestori predefiniti tramite regole {#custom}

Gli sviluppatori e gli autori di moduli possono scrivere regole, a livello di modulo, nell’editor di codice per ignorare i gestori predefiniti. La risposta del server per eventi di successo ed errore viene esposta a livello di modulo, a cui gli sviluppatori possono accedere utilizzando `$event.data` nelle regole.

Per scrivere regole nell’editor di codice per gestire gli eventi di successo e di errore, effettua le seguenti operazioni.

1. Apri il modulo adattivo in modalità di authoring, seleziona un oggetto modulo e fai clic su ![edit-rules1](assets/edit-rules1.png) per aprire l’editor di regole.
1. Seleziona **[!UICONTROL Modulo]** nella struttura Oggetti modulo e selezionare **[!UICONTROL Crea]**.
1. Seleziona **[!UICONTROL Editor di codice]** dal menu a discesa di selezione della modalità.
1. Nell’editor di codice, seleziona **[!UICONTROL Modifica codice]**. Seleziona **[!UICONTROL Modifica]** nella finestra di conferma.
1. Scegli **[!UICONTROL Invio corretto]** o **[!UICONTROL Errore nell’invio]** dal **[!UICONTROL Evento]** a discesa.
1. Scrivi una regola per l’evento selezionato e seleziona **[!UICONTROL Fine]** per salvare la regola.
