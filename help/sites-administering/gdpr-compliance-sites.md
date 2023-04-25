---
title: AEM Sites - Preparazione all’RGPD
seo-title: AEM Sites - GDPR Readiness
description: Scopri i dettagli sulla preparazione all’RGPD per AEM Sites.
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 54%

---

# AEM Sites - Preparazione all’RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come RGPD, CCPA, ecc.

Il Regolamento generale sulla protezione dei dati dell&#39;Unione europea sui diritti relativi alla privacy dei dati entra in vigore a maggio 2018.

AEM Sites è pronto ad aiutare i clienti ad adempiere ai loro obblighi di conformità ai requisiti RGPD. Questa pagina guida i clienti attraverso le procedure per gestire le richieste RGPD in AEM Sites. Descrive la posizione dei dati privati memorizzati e come rimuoverli manualmente o con codice.

Per ulteriori informazioni, consulta [Pagina RGPD nell’Adobe Privacy Center](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Vedi [Preparazione AEM RGPD](/help/managing/data-protection-and-privacy.md) per ulteriori dettagli.

## Author Server {#author-server}

Gli account utente e i contenuti UGC sul server di authoring sono trattati nella sezione [Documentazione di Platform RGPD](/help/managing/data-protection-and-privacy.md).

## Server di pubblicazione {#publish-server}

Gli account utente utilizzati per autenticare i visitatori sul sito e i contenuti UGC sul server di pubblicazione sono trattati nella sezione [Documentazione di Platform RGPD](/help/managing/data-protection-and-privacy.md).

Per impostazione predefinita, i componenti AEM Sites non memorizzano i dati dei moduli immessi dai visitatori sul server di pubblicazione. Si consiglia di inoltrare i dati a un sistema di terze parti o ad Adobe Campaign per un’ulteriore elaborazione.

## Consenso/rinuncia {#opt-in-opt-out}

AEM [servizio di rinuncia ai cookie](/help/sites-developing/cookie-optout.md) che può essere utilizzato per gestire l’opt-in/opt-out per gli utenti.

## Approfondimenti migliorati di Analytics {#enhanced-insights-by-analytics}

AEM Sites include un’integrazione opzionale con gli approfondimenti migliorati di Analytics che utilizza funzionalità all’interno del servizio Adobe Analytics On-demand.

Per ulteriori informazioni sulla gestione delle richieste relative alle persone interessate al RGPD in relazione ad Adobe Analytics, consulta [Adobe Analytics e RGPD](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html).

## Personalizzazione migliorata da Target {#enhanced-personalization-by-target}

AEM Sites include un’integrazione opzionale con la personalizzazione avanzata di Target che utilizza funzionalità all’interno del servizio Adobe Target On-demand.

Per ulteriori informazioni sulla gestione delle richieste relative alle persone interessate al RGPD in relazione ad Adobe Target, consulta [Adobe Target - Privacy e Regolamento generale sulla protezione dei dati (RGPD)](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

AEM fornisce un livello di dati facoltativo con [ContextHub](/help/sites-developing/contexthub.md). In questo modo i dati specifici del visitatore vengono mantenuti nel browser e utilizzati per la personalizzazione basata su regole.

Per impostazione predefinita, i dati visitatore non sono memorizzati in AEM. AEM invia regole al livello dati per prendere decisioni sulla personalizzazione nel browser.

>[!NOTE]
>
>Prima di Adobe CQ 5.6, il ClientContext (una versione precedente di ContextHub) inviava i dati al server, ma non li memorizzava.
>
>Adobe CQ 5.5 e versioni precedenti sono ora EOL e non sono coperti da questa documentazione.

### Implementazione di consenso/rinuncia {#implementing-opt-in-opt-out}

Il proprietario del sito deve implementare un componente di rinuncia in base alle seguenti linee guida.

In queste linee guida il consenso è implementato per impostazione predefinita. Pertanto, un visitatore del sito web deve essere chiaramente d’accordo, prima che qualsiasi Dati Personali sia memorizzato nella persistenza del browser (lato client).

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

      * ContextHub.Utils.Persistence.Modes.LOCAL (predefinito)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      L’archivio ContextHub definisce il livello di persistenza da utilizzare, in modo da visualizzare lo stato attuale della persistenza in tutti i livelli che devono essere controllati.


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

      * ContextHub.Utils.Persistence.Modes.LOCAL (predefinito)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      L’archivio ContextHub definisce il livello di persistenza da utilizzare, in modo da visualizzare lo stato attuale della persistenza in tutti i livelli che devono essere controllati.


Ad esempio, per visualizzare i dati memorizzati in localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Cancellazione della persistenza di ContextHub {#clearing-persistence-of-contexthub}

Per cancellare la persistenza di ContextHub:

* Per cancellare la persistenza degli archivi attualmente caricati:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
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

   * ContextHub.Utils.Persistence.Modes.LOCAL (predefinito)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
