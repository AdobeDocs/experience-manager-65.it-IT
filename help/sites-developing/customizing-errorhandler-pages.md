---
title: Personalizzazione delle pagine mostrate dal gestore errori
seo-title: Personalizzazione delle pagine mostrate dal gestore errori
description: AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP
seo-description: AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Personalizzazione delle pagine mostrate dal gestore errori{#customizing-pages-shown-by-the-error-handler}

AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP. ad esempio, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Gli script forniti dal sistema esistono (nella sezione `/libs/sling/servlet/errorhandler`) per rispondere ai codici di errore, per impostazione predefinita sono disponibili le seguenti opzioni con un&#39;istanza CQ standard:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM è basato su Apache Sling, pertanto consultate [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) per informazioni dettagliate sulla gestione degli errori Sling.

>[!NOTE]
>
>Per impostazione predefinita, in un’istanza di authoring [CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) è attivato. Questo restituisce sempre il codice di risposta 200. Il gestore errori predefinito risponde scrivendo la traccia dello stack completa nella risposta.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM viene *sempre* disabilitato (anche se configurato come attivato).

## Come personalizzare le pagine visualizzate dal gestore errori {#how-to-customize-pages-shown-by-the-error-handler}

È possibile sviluppare script personalizzati per personalizzare le pagine mostrate dal gestore errori quando si verifica un errore. Le pagine personalizzate verranno create sotto `/apps` e sovrapporranno le pagine predefinite (sotto `/libs`).

>[!NOTE]
>
>Consultate [Utilizzo delle sovrapposizioni](/help/sites-developing/overlays.md) per ulteriori dettagli.

1. Nell&#39;archivio, copiare gli script predefiniti:

   * from `/libs/sling/servlet/errorhandler/`
   * a `/apps/sling/servlet/errorhandler/`
   Poiché il percorso di destinazione non esiste per impostazione predefinita, sarà necessario crearlo al primo tentativo.

1. Accedi a `/apps/sling/servlet/errorhandler`. Potete effettuare le seguenti operazioni:

   * modificare lo script esistente appropriato per fornire le informazioni richieste.
   * creare e modificare un nuovo script per il codice richiesto.

1. Salvate le modifiche e verificate il comportamento.

>[!CAUTION]
>
>I gestori 404.jsp e 403.jsp sono stati progettati specificamente per garantire l’autenticazione CQ5; in particolare, per consentire l&#39;accesso al sistema in caso di tali errori.
>
>Pertanto, la sostituzione di questi due gestori dovrebbe essere fatta con grande cura.

### Personalizzazione della risposta agli errori HTTP 500 {#customizing-the-response-to-http-errors}

Gli errori HTTP 500 sono causati da eccezioni lato server.

* **[500 Errore](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**interno del server Il server ha rilevato una condizione imprevista che non consentiva all&#39;utente di soddisfare la richiesta.

Quando l’elaborazione delle richieste genera un’eccezione, il framework Apache Sling (sul quale è basato AEM):

* registra l&#39;eccezione
* return:

   * il codice di risposta HTTP 500
   * traccia dello stack di eccezioni
   nel corpo della risposta.

Personalizzando [le pagine visualizzate dal gestore](#how-to-customize-pages-shown-by-the-error-handler) di errori è possibile creare uno `500.jsp` script. Tuttavia, è utilizzato solo se `HttpServletResponse.sendError(500)` è eseguito esplicitamente; ovvero da un rilevatore di eccezioni.

In caso contrario, il codice di risposta è impostato su 500, ma lo `500.jsp` script non è eseguito.

Per gestire 500 errori, il nome file dello script del gestore di errori deve essere uguale alla classe di eccezione (o superclasse). Per gestire tutte queste eccezioni è possibile creare uno script `/apps/sling/servlet/errorhandler/Throwable.js`p o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Per impostazione predefinita, in un’istanza di authoring [CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) è attivato. Questo restituisce sempre il codice di risposta 200. Il gestore errori predefinito risponde scrivendo la traccia dello stack completa nella risposta.
>
>Per un gestore di errori personalizzato, sono necessarie risposte con codice 500, pertanto è necessario disattivare [il filtro di debug di](/help/sites-deploying/osgi-configuration-settings.md)CQ WCM. In questo modo viene restituito il codice di risposta 500, che a sua volta attiva il gestore errori Sling corretto.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM viene *sempre* disabilitato (anche se configurato come attivato).

