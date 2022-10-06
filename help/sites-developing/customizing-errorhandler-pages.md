---
title: Personalizzazione delle pagine mostrate dal gestore errori
seo-title: Customizing Pages shown by the Error Handler
description: AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---

# Personalizzazione delle pagine mostrate dal gestore errori{#customizing-pages-shown-by-the-error-handler}

AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP; ad esempio, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Sono presenti script forniti dal sistema (in `/libs/sling/servlet/errorhandler`) per rispondere ai codici di errore, per impostazione predefinita sono disponibili le seguenti opzioni con un’istanza CQ standard:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM è basato su Apache Sling, quindi vedi [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) per informazioni dettagliate sulla gestione degli errori Sling.

>[!NOTE]
>
>Su un&#39;istanza dell&#39;autore, [Filtro di debug CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) è attivato per impostazione predefinita. Questo si traduce sempre nel codice di risposta 200. Il gestore di errori predefinito risponde scrivendo la traccia completa dello stack nella risposta.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM è *sempre* disabilitato (anche se configurato come abilitato).

## Come personalizzare le pagine visualizzate dal gestore errori {#how-to-customize-pages-shown-by-the-error-handler}

È possibile sviluppare script personalizzati per personalizzare le pagine mostrate dal gestore di errori quando si verifica un errore. Le pagine personalizzate verranno create in `/apps` e sovrapponi le pagine predefinite (che sono sotto `/libs`).

>[!NOTE]
>
>Vedi [Utilizzo delle sovrapposizioni](/help/sites-developing/overlays.md) per ulteriori dettagli.

1. Nell’archivio, copia gli script predefiniti:

   * da `/libs/sling/servlet/errorhandler/`
   * a `/apps/sling/servlet/errorhandler/`

   Poiché il percorso di destinazione non esiste per impostazione predefinita, sarà necessario crearlo durante questa operazione per la prima volta.

1. Accedi a `/apps/sling/servlet/errorhandler`. Qui puoi effettuare le seguenti operazioni:

   * modificare lo script esistente appropriato per fornire le informazioni richieste.
   * crea e modifica un nuovo script per il codice richiesto.

1. Salva le modifiche e verifica.

>[!CAUTION]
>
>I gestori 404.jsp e 403.jsp sono stati progettati specificamente per garantire l&#39;autenticazione CQ5; in particolare, per consentire l&#39;accesso al sistema in caso di questi errori.
>
>Pertanto, la sostituzione di questi due gestori dovrebbe essere fatta con grande cura.

### Personalizzazione della risposta agli errori HTTP 500 {#customizing-the-response-to-http-errors}

Gli errori HTTP 500 sono causati da eccezioni lato server.

* **[Errore server interno 500](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
Il server ha rilevato una condizione imprevista che ne ha impedito l&#39;esecuzione della richiesta.

Quando l’elaborazione della richiesta genera un’eccezione, il framework Sling Apache (AEM basato su):

* registra l&#39;eccezione
* restituisce:

   * il codice di risposta HTTP 500
   * traccia dello stack di eccezioni

   nel corpo della risposta.

Da [personalizzazione delle pagine mostrate dal gestore di errori](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` è possibile creare uno script. Tuttavia, viene utilizzato solo se `HttpServletResponse.sendError(500)` è eseguito esplicitamente; ovvero da un catcher di eccezione.

In caso contrario, il codice di risposta è impostato su 500, ma il `500.jsp` script non eseguito.

Per gestire 500 errori, il nome file dello script del gestore di errori deve essere lo stesso della classe di eccezione (o superclasse). Per gestire tutte queste eccezioni è possibile creare uno script `/apps/sling/servlet/errorhandler/Throwable.js`p o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Su un&#39;istanza dell&#39;autore, [Filtro di debug CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) è attivato per impostazione predefinita. Questo si traduce sempre nel codice di risposta 200. Il gestore di errori predefinito risponde scrivendo la traccia completa dello stack nella risposta.
>
>Per un gestore di errori personalizzato, sono necessarie le risposte con codice 500, quindi è necessario [CQ WCM Debug Filter deve essere disabilitato](/help/sites-deploying/osgi-configuration-settings.md). In questo modo viene restituito il codice di risposta 500, che a sua volta attiva il gestore di errori Sling corretto.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM è *sempre* disabilitato (anche se configurato come abilitato).
