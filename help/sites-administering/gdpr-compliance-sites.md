---
title: AEM Sites - Preparazione al RGPD
description: Scopri le procedure per gestire le richieste RGPD in AEM Sites e come utilizzarle.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 54%

---

# AEM Sites - Preparazione al RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli coperti sono applicabili a tutte le normative su privacy e protezione dei dati, come RGPD, CCPA e così via.

Il Regolamento generale sulla protezione dei dati dell&#39;Unione Europea sui diritti relativi alla privacy dei dati entra in vigore a maggio 2018.

AEM Sites è pronta ad aiutare i clienti a rispettare gli obblighi di conformità ai requisiti RGPD. Questa pagina guida i clienti attraverso le procedure per gestire le richieste RGPD in AEM Sites. Descrive la posizione dei dati privati memorizzati e come rimuoverli manualmente o con codice.

Per ulteriori informazioni, consulta [Pagina RGPD nel Centro per la privacy di Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulta [Preparazione all’AEM per il RGPD](/help/managing/data-protection-and-privacy.md) per ulteriori dettagli.

## Author Server {#author-server}

Gli account utente e i contenuti UGC sul server di authoring sono trattati in [Documentazione di Platform RGPD](/help/managing/data-protection-and-privacy.md).

## Server di pubblicazione {#publish-server}

Gli account utente utilizzati per autenticare i visitatori sul sito e i contenuti UGC sul server di pubblicazione sono trattati in [Documentazione di Platform RGPD](/help/managing/data-protection-and-privacy.md).

Per impostazione predefinita, i componenti AEM Sites non memorizzano i dati dei moduli immessi dai visitatori sul server di pubblicazione. Si consiglia di inoltrare i dati a un sistema di terze parti o ad Adobe Campaign per un’ulteriore elaborazione.

## Consenso/rinuncia {#opt-in-opt-out}

L&#39;AEM ha un [servizio di rinuncia ai cookie](/help/sites-developing/cookie-optout.md) che può essere utilizzato per gestire il consenso/diniego per gli utenti.

## Approfondimenti migliorati da Analytics {#enhanced-insights-by-analytics}

AEM Sites include un’integrazione opzionale con Enhanced Insights by Analytics che utilizza funzionalità interne al servizio Adobe Analytics On-demand.

Per ulteriori informazioni sulla gestione delle richieste dei soggetti interessati ai sensi del RGPD in relazione ad Adobe Analytics, consulta [ADOBE ANALYTICS e RGPD](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html).

## Personalizzazione avanzata per Target {#enhanced-personalization-by-target}

AEM Sites include un’integrazione opzionale con la Personalizzazione avanzata di Target che utilizza funzionalità interne al servizio Adobe Target On-demand.

Per ulteriori informazioni sulla gestione delle richieste dei soggetti interessati ai sensi del RGPD in relazione ad Adobe Target, consulta [Adobe Target - Privacy e Regolamento generale sulla protezione dei dati (RGPD)](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

L’AEM fornisce un livello di dati opzionale con [ContextHub](/help/sites-developing/contexthub.md). In questo modo i dati specifici del visitatore vengono mantenuti nel browser e utilizzati per la personalizzazione basata su regole.

Per impostazione predefinita, i dati visitatore non sono memorizzati in AEM. AEM invia regole al livello dati per prendere decisioni sulla personalizzazione nel browser.

>[!NOTE]
>
>Prima di Adobe CQ 5.6, il ClientContext (una versione precedente di ContextHub) ha inviato i dati al server, ma non li ha memorizzati.
>
>Adobe CQ 5.5 e versioni precedenti sono ora fine del ciclo di vita e non sono coperte da questa documentazione.

### Implementazione di consenso/rinuncia {#implementing-opt-in-opt-out}

Il proprietario del sito deve implementare un componente di rinuncia in base alle seguenti linee guida.

In queste linee guida il consenso è implementato per impostazione predefinita. Pertanto, un visitatore del sito web deve dare il suo consenso esplicito prima che qualsiasi dato personale venga memorizzato nella persistenza del browser (lato client).

* Il componente di rinuncia deve essere incluso ogni volta che il componente ContextHub è incluso.
* I termini e le condizioni relativi al RGPD per il sito web devono essere visualizzati al visitatore del sito web, consentendo loro di:

   * accetta
   * rifiuta
   * cambia la scelta precedente

* Se un visitatore del sito accetta i termini e le condizioni del sito, il cookie di rinuncia di ContextHub deve essere rimosso:

  ```
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* Se un visitatore del sito non accetta i termini e le condizioni del sito, il cookie di rinuncia di ContextHub deve essere impostato:

  ```
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* Per verificare se ContextHub è in esecuzione in modalità di rinuncia, è necessario effettuare la seguente chiamata nella console del browser:

  ```
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### Anteprima della persistenza di ContextHub {#previewing-persistence-of-contexthub}

Per visualizzare in anteprima la persistenza utilizzata in ContextHub, un utente può:

* Utilizzare la console del browser, ad esempio:

   * Chrome:

      * Apri Strumenti per sviluppatori > Applicazione > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistence
         * Archiviazione sessione > (sito Web) > ContextHubPersistence
         * Cookie > (sito Web) > SessionPersistence

   * Firefox:

      * Apri Strumenti di sviluppo web > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistence
         * Archiviazione sessione > (sito Web) > ContextHubPersistence
         * Cookie > (sito Web) > SessionPersistence

   * Safari:

      * Apri Preferenze > Avanzate > Mostra menu Sviluppo nella barra dei menu
      * Apri Sviluppo > Mostra console JavaScript

         * Console > Archiviazione > Archiviazione locale > (sito Web) > ContextHubPersistence
         * Console > Archiviazione > Archiviazione sessione > (sito Web) > ContextHubPersistence
         * Console > Archiviazione > Cookie > (sito Web) > ContextHubPersistence

   * Internet Explorer:

      * Apri Strumenti di sviluppo > Console

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie

* Utilizza l’API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * ContextHub.Utils.Persistence.Modes.LOCAL (impostazione predefinita)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     L’archivio ContextHub definisce il livello di persistenza utilizzato, in modo da visualizzare lo stato attuale della persistenza in tutti i livelli che devono essere controllati.

Ad esempio, per visualizzare i dati memorizzati in localStorage:

Per visualizzare in anteprima la persistenza utilizzata in ContextHub, un utente può:

* Usa la console del browser:

   * Chrome - apri Strumenti per sviluppatori > Applicazione > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistence
      * Archiviazione sessione > (sito Web) > ContextHubPersistence
      * Cookie > (sito Web) > SessionPersistence

   * Firefox - apri Strumenti di sviluppo web > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistence
      * Archiviazione sessione > (sito Web) > ContextHubPersistence
      * Cookie > (sito Web) > SessionPersistence

* Utilizza l’API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * ContextHub.Utils.Persistence.Modes.LOCAL (impostazione predefinita)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     L’archivio ContextHub definisce il livello di persistenza utilizzato, in modo da visualizzare lo stato attuale della persistenza in tutti i livelli che devono essere controllati.

Ad esempio, per visualizzare i dati memorizzati in localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Cancellazione della persistenza di ContextHub {#clearing-persistence-of-contexthub}

Per cancellare la persistenza di ContextHub:

* Per cancellare la persistenza degli archivi attualmente caricati:

  ```
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* Per cancellare un livello di persistenza specifico, ad esempio, sessionStorage:

  ```
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* Per cancellare tutti i livelli di persistenza ContextHub, è necessario chiamare il codice appropriato per tutti i livelli:

   * ContextHub.Utils.Persistence.Modes.LOCAL (impostazione predefinita)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
