---
title: ' AEM Sites - Preparazione GDPR'
seo-title: ' AEM Sites - Preparazione GDPR'
description: Scopri i dettagli di GDPR Readiness per  AEM Sites.
seo-description: Scopri i dettagli di GDPR Readiness per  AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---


#  AEM Sites - GDPR: prontezza{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>Il GDPR è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come GDPR, CCPA ecc.

Il regolamento generale dell&#39;Unione europea sulla protezione dei dati in materia di diritti sulla privacy ha effetto a maggio 2018.

 AEM Sites è pronta ad aiutare i clienti a rispettare gli obblighi di conformità ai requisiti GDPR. Questa pagina illustra ai clienti le procedure per gestire le richieste GDPR in  AEM Sites. Descrive la posizione dei dati privati memorizzati e come rimuoverli manualmente o con il codice.

Per ulteriori informazioni, vedere la pagina [GDPR all&#39; Centro per la privacy del Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Per ulteriori informazioni, vedere [AEM GDPR Readiness](/help/managing/data-protection-and-privacy.md).

## Author Server {#author-server}

Gli account utente e i contenuti UGC sul server di creazione sono trattati nella [Documentazione GDPR della piattaforma](/help/managing/data-protection-and-privacy.md).

## Server di pubblicazione {#publish-server}

Gli account utente utilizzati per autenticare i visitatori del sito e i contenuti UGC sul server di pubblicazione sono descritti nella documentazione [Platform GDPR](/help/managing/data-protection-and-privacy.md).

Per impostazione predefinita,  componenti AEM Sites non memorizzano i dati dei moduli immessi dai visitatori sul server di pubblicazione. Si consiglia di inoltrare i dati a un sistema di terze parti o  Adobe Campaign per un&#39;ulteriore elaborazione.

## Opt-In/Opt-Out {#opt-in-opt-out}

AEM dispone di un [servizio di rinuncia ai cookie](/help/sites-developing/cookie-optout.md) che può essere utilizzato per gestire il consenso o il rifiuto per gli utenti.

## Approfondimenti migliorati di Analytics {#enhanced-insights-by-analytics}

 AEM Sites include un&#39;integrazione opzionale con Enhanced Insights di Analytics che utilizza funzionalità all&#39;interno  Adobe Analytics On-demand Service.

Per ulteriori informazioni sulla gestione delle richieste di dati GDPR relative a  Adobe Analytics, vedere [ Adobe Analytics e GDPR](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html).

## Personalizzazione avanzata per Target {#enhanced-personalization-by-target}

 AEM Sites include un&#39;integrazione opzionale con Enhanced Personalization by Target, che utilizza funzionalità all&#39;interno  Adobe Target On-demand Service.

Per ulteriori informazioni sulla gestione delle richieste di dati GDPR relative a  Adobe Target, vedere [ Adobe Target - Privacy e Regolamento generale sulla protezione dei dati](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

AEM fornisce un livello dati opzionale con [ContextHub](/help/sites-developing/contexthub.md). In questo modo i dati specifici del visitatore vengono conservati nel browser e utilizzati per la personalizzazione basata su regole.

Per impostazione predefinita, questi dati visitatore non sono memorizzati in AEM; AEM invia regole al livello dati per prendere decisioni di personalizzazione nel browser.

>[!NOTE]
>
>Prima di  Adobe CQ 5.6, l&#39;ClientContext (una versione precedente di ContextHub) inviava i dati al server, ma non li memorizzava.
>
> Adobe CQ 5.5 e versioni precedenti sono ora EOL e non sono coperti da questa documentazione.

### Implementazione consenso/rifiuto {#implementing-opt-in-opt-out}

Il proprietario del sito deve implementare un componente di rinuncia in base alle seguenti linee guida.

Queste linee guida implementano il consenso come impostazione predefinita. Pertanto, un visitatore del sito Web deve essere chiaramente d&#39;accordo, prima che i Dati Personali siano memorizzati nella persistenza (lato client) del browser.

* Il componente di rinuncia deve essere incluso ogni volta che viene incluso il componente ContextHub.
* I termini e le condizioni relativi al GDPR per il sito Web devono essere visualizzati al visitatore del sito Web, consentendo loro di:

   * accetto
   * rifiutare
   * modifica la scelta precedente

* Se un visitatore accetta i termini e le condizioni del sito, il cookie di rinuncia ContextHub deve essere rimosso:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Se un visitatore del sito non accetta i termini e le condizioni del sito, il cookie di rinuncia ContextHub deve essere impostato:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Per verificare se ContextHub è in esecuzione in modalità di rifiuto, nella console del browser deve essere effettuata la seguente chiamata:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Anteprima della persistenza di ContextHub {#previewing-persistence-of-contexthub}

Per visualizzare in anteprima la persistenza utilizzata ContextHub, un utente può:

* Utilizzare la console del browser; ad esempio:

   * Effetto cromatura:

      * Apri Strumenti Sviluppatore > Applicazione > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistenza
         * Archiviazione sessione > (sito Web) > ContextHubPersistenza
         * Cookie > (sito Web) > SessionPersistenza
   * Firefox:

      * Apri Strumenti Sviluppatore > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistenza
         * Archiviazione sessione > (sito Web) > ContextHubPersistenza
         * Cookie > (sito Web) > SessionPersistenza
   * Safari:

      * Apri Preferenze > Avanzate > Mostra menu Sviluppo nella barra dei menu
      * Apri Sviluppo > Mostra console JavaScript

         * Console > Storage > Archiviazione locale > (sito Web) > ContextHubPersistenza
         * Console > Storage > Archiviazione sessione > (sito Web) > ContextHubPersistenza
         * Console > Storage > Cookie > (sito Web) > ContextHubPersistenza
   * Internet Explorer:

      * Apri strumenti per sviluppatori > Console

         * localStorage.getItem(&#39;ContextHubPersistenza&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistenza&#39;)
         * document.cookie




* Utilizzate l&#39;API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * ContextHub.Utils.Persistenza.Modes.LOCAL (predefinito)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      L&#39;archivio ContextHub definisce il livello di persistenza da utilizzare, pertanto per visualizzare lo stato corrente della persistenza tutti i livelli devono essere controllati.


Ad esempio, per visualizzare i dati memorizzati in localStorage:

Per visualizzare in anteprima la persistenza utilizzata ContextHub, un utente può:

* Utilizzate la console del browser:

   * Chrome - aprire Strumenti per sviluppatori > Applicazione > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistenza
      * Archiviazione sessione > (sito Web) > ContextHubPersistenza
      * Cookie > (sito Web) > SessionPersistenza
   * Firefox - aprire Strumenti per sviluppatori > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistenza
      * Archiviazione sessione > (sito Web) > ContextHubPersistenza
      * Cookie > (sito Web) > SessionPersistenza


* Utilizzate l&#39;API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * ContextHub.Utils.Persistenza.Modes.LOCAL (predefinito)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      L&#39;archivio ContextHub definisce il livello di persistenza da utilizzare, pertanto per visualizzare lo stato corrente della persistenza tutti i livelli devono essere controllati.


Ad esempio, per visualizzare i dati memorizzati in localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Cancellazione della persistenza di ContextHub {#clearing-persistence-of-contexthub}

Per cancellare la persistenza ContextHub:

* Per eliminare la persistenza degli store attualmente caricati:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Cancellazione di un livello di persistenza specifico; ad esempio, sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Per cancellare tutti i livelli di persistenza ContextHub, è necessario chiamare il codice appropriato per tutti i livelli:

   * ContextHub.Utils.Persistenza.Modes.LOCAL (predefinito)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

