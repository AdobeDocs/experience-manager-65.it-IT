---
title: Personalizzazione delle pagine visualizzate dal gestore degli errori
description: Adobe Experience Manager viene fornito con un gestore degli errori standard per la gestione degli errori HTTP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Personalizzazione delle pagine visualizzate dal gestore degli errori{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager (AEM) viene fornito con un gestore degli errori standard per la gestione degli errori HTTP, ad esempio mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Gli script forniti dal sistema esistono (in `/libs/sling/servlet/errorhandler`) per rispondere ai codici di errore. Per impostazione predefinita, con un&#39;istanza CQ standard sono disponibili i seguenti script:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>L’AEM si basa su Apache Sling. Per informazioni dettagliate sulla gestione degli errori Sling, consulta [Gestione errori](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html).

>[!NOTE]
>
>In un&#39;istanza Autore, il filtro di debug [CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) è abilitato per impostazione predefinita. Questo determina sempre il codice di risposta 200. Il gestore degli errori predefinito risponde scrivendo la traccia full stack nella risposta.
>
>In un&#39;istanza di pubblicazione, il filtro di debug WCM CQ è disabilitato *sempre* (anche se configurato come abilitato).

## Personalizzare le pagine visualizzate dal gestore degli errori {#how-to-customize-pages-shown-by-the-error-handler}

Puoi sviluppare script personalizzati per personalizzare le pagine visualizzate dal gestore degli errori quando viene rilevato un errore. Le pagine personalizzate vengono create in `/apps` e si sovrappongono alle pagine predefinite (che si trovano in `/libs`).

>[!NOTE]
>
>Per ulteriori dettagli, vedi [Utilizzo delle sovrapposizioni](/help/sites-developing/overlays.md).

1. Nell’archivio, copia gli script predefiniti:

   * da `/libs/sling/servlet/errorhandler/`
   * a `/apps/sling/servlet/errorhandler/`

   Poiché il percorso di destinazione non esiste per impostazione predefinita, è necessario crearlo quando si esegue questa operazione per la prima volta.

1. Passare a `/apps/sling/servlet/errorhandler` ed effettuare una delle seguenti operazioni:

   * modificare lo script esistente appropriato in modo da poter fornire le informazioni richieste.
   * crea e modifica un nuovo script per il codice richiesto.

1. Salva le modifiche e verifica.

>[!CAUTION]
>
>I gestori 404.jsp e 403.jsp sono stati progettati per soddisfare l’autenticazione CQ5; in particolare, per consentire l’accesso al sistema in caso di errori.
>
>Pertanto, la sostituzione di questi due gestori deve essere effettuata con molta attenzione.

### Personalizzazione della risposta agli errori HTTP 500 {#customizing-the-response-to-http-errors}

Gli errori HTTP 500 sono causati da eccezioni sul lato server.

* **[Errore interno del server ](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
Il server ha rilevato una condizione imprevista che ha impedito il completamento della richiesta.

Quando l’elaborazione delle richieste genera un’eccezione, il framework Sling Apache (su cui si basa l’AEM):

* registra l’eccezione
* restituisce:

   * il codice di risposta HTTP 500
   * traccia dello stack di eccezioni

  nel corpo della risposta.

È possibile creare uno script `500.jsp` personalizzando le pagine visualizzate dal gestore degli errori[&#128279;](#how-to-customize-pages-shown-by-the-error-handler).  Tuttavia, viene utilizzato solo se `HttpServletResponse.sendError(500)` viene eseguito in modo esplicito, ovvero da un servizio di raccolta eccezioni.

In caso contrario, il codice di risposta è impostato su 500, ma lo script `500.jsp` non viene eseguito.

Per gestire gli errori 500, il nome file dello script del gestore degli errori deve essere uguale a quello della classe di eccezione (o superclasse). Per gestire tutte queste eccezioni, è possibile creare uno script `/apps/sling/servlet/errorhandler/Throwable.js`p o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>In un&#39;istanza Autore, il filtro di debug [CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) è abilitato per impostazione predefinita. Questo determina sempre il codice di risposta 200. Il gestore degli errori predefinito risponde scrivendo la traccia full stack nella risposta.
>
>Per un gestore degli errori personalizzato, sono necessarie risposte con codice 500, pertanto il filtro di debug WCM [CQ deve essere disabilitato](/help/sites-deploying/osgi-configuration-settings.md). In questo modo viene restituito il codice di risposta 500, che a sua volta attiva il gestore di errori Sling corretto.
>
>In un&#39;istanza di pubblicazione, il filtro di debug WCM CQ è disabilitato *sempre* (anche se configurato come abilitato).
