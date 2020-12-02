---
title: Sviluppo AEM - Linee guida e migliori prassi
seo-title: Sviluppo AEM - Linee guida e migliori prassi
description: Linee guida e migliori prassi per lo sviluppo di AEM
seo-description: Linee guida e migliori prassi per lo sviluppo di AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---


# Sviluppo AEM - Linee guida e best practice{#aem-development-guidelines-and-best-practices}

## Linee guida per l&#39;utilizzo di modelli e componenti {#guidelines-for-using-templates-and-components}

AEM componenti e modelli formano un potente toolkit. Possono essere utilizzati dagli sviluppatori per fornire agli utenti aziendali dei siti Web, agli editor e agli amministratori le funzionalità necessarie per adattare i loro siti Web alle esigenze aziendali in continua evoluzione (agilità dei contenuti), mantenendo al contempo il layout uniforme dei siti (protezione del marchio).

Una tipica sfida per una persona responsabile di un sito Web, o per un insieme di siti Web (ad esempio in una succursale di un&#39;azienda globale), è quella di introdurre un nuovo tipo di presentazione dei contenuti sui propri siti Web.

Supponiamo che sia necessario aggiungere una pagina di newslist ai siti Web, in cui sono elencati estratti di altri articoli già pubblicati. La pagina deve avere la stessa struttura e struttura del sito Web.

Il modo consigliato per affrontare tale sfida sarebbe di:

* Riutilizzate un modello esistente per creare un nuovo tipo di pagina. Il modello definisce in modo approssimativo la struttura delle pagine (elementi di navigazione, pannelli e così via), ulteriormente regolata dalla sua progettazione (CSS, grafica).
* Utilizzate il sistema paragrafo (parsys/iparsys) nelle nuove pagine.
* Consente di definire l&#39;accesso alla modalità Progettazione dei sistemi di paragrafi, in modo che solo gli utenti autorizzati (in genere l&#39;amministratore) possano modificarli.
* Definite i componenti consentiti nel sistema di paragrafi specificato in modo che gli editor possano quindi posizionare i componenti richiesti sulla pagina. Nel nostro caso potrebbe trattarsi di un componente elenco, che può scorrere una sottostruttura di pagine ed estrarre le informazioni in base a regole predefinite.
* Gli editor aggiungono e configurano i componenti consentiti, sulle pagine di cui sono responsabili, per fornire le funzionalità richieste (informazioni) all&#39;azienda.

Questo approccio illustra come questo approccio consente agli utenti e agli amministratori del sito Web partecipanti di rispondere rapidamente alle esigenze aziendali, senza richiedere il coinvolgimento di team di sviluppo. Metodi alternativi, come la creazione di un nuovo modello, è in genere un esercizio costoso, che richiede un processo di gestione delle modifiche e il coinvolgimento del team di sviluppo. Ciò rende l&#39;intero processo molto più lungo e costoso.

Gli sviluppatori di sistemi AEM dovrebbero pertanto utilizzare:

* modelli e controllo dell&#39;accesso alla progettazione del sistema paragrafo per uniformità e protezione del marchio
* il sistema di paragrafi, comprese le opzioni di configurazione per la flessibilità.

Le seguenti regole generali per gli sviluppatori hanno senso nella maggior parte dei progetti comuni:

* Mantenete basso il numero di modelli, fino al numero di strutture di pagina fondamentalmente diverse nei siti Web.
* Offrite ai componenti personalizzati la flessibilità e le funzionalità di configurazione necessarie.
* Ottimizzate l&#39;utilizzo della potenza e della flessibilità del sistema AEM paragrafi, ovvero i componenti parsys e iparsys.

### Personalizzazione di componenti e altri elementi {#customizing-components-and-other-elements}

Quando create componenti personalizzati o personalizzate un componente esistente, è spesso più semplice (e sicuro) riutilizzare le definizioni esistenti. Gli stessi principi si applicano anche ad altri elementi all&#39;interno di AEM, ad esempio il gestore di errori.

È possibile eseguire questa operazione copiando e sovrapponendo la definizione esistente. In altre parole, copiando la definizione da `/libs` a `/apps/<your-project>`. Questa nuova definizione, in `/apps`, può essere aggiornata in base alle tue esigenze.

>[!NOTE]
>
>Per ulteriori informazioni, consultate [Utilizzo delle sovrapposizioni](/help/sites-developing/overlays.md).

Esempio:

* [Personalizzazione di un componente](/help/sites-developing/components.md)

   Questo comportava la sovrapposizione di una definizione di componente:

   * Crea una nuova cartella di componenti in `/apps/<website-name>/components/<MyComponent>` copiando un componente esistente:

      * Ad esempio, per personalizzare la copia del componente Testo:

         * da `/libs/foundation/components/text`
         * a `/apps/myProject/components/text`

* [Personalizzazione delle pagine mostrate dal gestore errori](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Questo caso comporta la sovrapposizione di un servlet:

   * Nell&#39;archivio, copiare gli script predefiniti:

      * da `/libs/sling/servlet/errorhandler/`
      * a `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**non è necessario modificare alcun elemento nel percorso `/libs`.**
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Per la configurazione e altre modifiche:
>
>1. copiare l&#39;elemento in `/libs` in `/apps`
>1. apportare modifiche entro `/apps`


## Quando utilizzare le query JCR e quando non usarle {#when-to-use-jcr-queries-and-when-not-to-use-them}

Le query JCR sono uno strumento potente quando utilizzate correttamente. Sono appropriati per:

* query reali per l’utente finale, ad esempio ricerche full-text sul contenuto.
* le occasioni in cui è necessario reperire contenuti strutturati in tutto il repository.

   In tali casi, accertatevi che le query vengano eseguite solo quando è assolutamente necessario, ad esempio in caso di attivazione di un componente o di annullamento della validità della cache (invece di eseguire i passaggi dei flussi di lavoro, i gestori eventi che attivano le modifiche ai contenuti, i filtri, ecc.).

Le query JCR non devono mai essere utilizzate per richieste di rendering pure. Ad esempio, le query JCR non sono adatte a

* rendering, navigazione
* creazione di una panoramica delle 10 ultime notizie
* visualizzazione del numero di elementi di contenuto

Per eseguire il rendering del contenuto, utilizzate l&#39;accesso alla struttura del contenuto invece di eseguire una query JCR.

>[!NOTE]
>
>Se utilizzate il [Generatore di query](/help/sites-developing/querybuilder-api.md), utilizzate le query JCR, poiché Query Builder genera le query JCR sotto il cofano.


## Considerazioni sulla sicurezza {#security-considerations}

>[!NOTE]
>
>Vale anche la pena fare riferimento alla [lista di controllo di sicurezza](/help/sites-administering/security-checklist.md).

### Sessioni JCR (repository) {#jcr-repository-sessions}

Utilizzate la sessione utente, non quella amministrativa. Questo significa che devi usare:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect per lo scripting tra siti (XSS) {#protect-against-cross-site-scripting-xss}

Lo scripting tra siti (XSS) consente agli aggressori di inserire codice nelle pagine Web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti Web malintenzionati per aggirare i controlli di accesso.

AEM applica il principio di filtraggio di tutti i contenuti forniti dall’utente al momento dell’output. La prevenzione di XSS viene data la massima priorità sia durante lo sviluppo che durante i test.

Inoltre, un firewall per applicazioni Web, come [mod_security for Apache](https://modsecurity.org), può fornire un controllo centrale affidabile sulla sicurezza dell&#39;ambiente di distribuzione e proteggere contro attacchi di script tra siti non rilevati in precedenza.

>[!CAUTION]
>
>Il codice di esempio fornito con AEM potrebbe non essere di per sé protetto da tali attacchi e in genere si basa sul filtraggio delle richieste da parte di un firewall dell&#39;applicazione Web.

Il foglio di controllo API XSS contiene informazioni che è necessario conoscere per utilizzare l&#39;API XSS e rendere un&#39;app AEM più sicura. Potete scaricarlo qui:

Il foglio di imbroglio XSSAPI.

[Ottieni file](assets/xss_cheat_sheet_2016.pdf)

### Protezione della comunicazione per informazioni riservate {#securing-communication-for-confidential-information}

Per quanto riguarda le applicazioni Internet, assicurarsi che durante il trasporto di informazioni riservate

* il traffico è protetto tramite SSL
* POST HTTP, se applicabile

Ciò vale per le informazioni riservate al sistema (come la configurazione o l&#39;accesso amministrativo) e per quelle riservate agli utenti (come i loro dati personali)

## Attività di sviluppo distinte {#distinct-development-tasks}

### Personalizzazione delle pagine di errore {#customizing-error-pages}

Le pagine di errore possono essere personalizzate per AEM. Questo è consigliabile in modo che l&#39;istanza non riveli tracce di utilizzo in caso di errori interni del server.

Per informazioni dettagliate, vedere [Personalizzazione delle pagine di errore visualizzate dal gestore di errori](/help/sites-developing/customizing-errorhandler-pages.md).

### Apri i file nel processo Java {#open-files-in-the-java-process}

Poiché AEM può accedere a un gran numero di file, si consiglia di configurare in modo esplicito per AEM il numero di [file aperti per un processo Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process).

Per ridurre al minimo questo problema, lo sviluppo dovrebbe garantire che tutti i file aperti vengano chiusi correttamente non appena (significativo) possibile.
