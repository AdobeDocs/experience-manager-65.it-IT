---
title: Sviluppo AEM - Linee guida e best practice
seo-title: Sviluppo AEM - Linee guida e best practice
description: Linee guida e best practice per lo sviluppo su AEM
seo-description: Linee guida e best practice per lo sviluppo su AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sviluppo AEM - Linee guida e best practice{#aem-development-guidelines-and-best-practices}

## Linee guida per l’utilizzo di modelli e componenti {#guidelines-for-using-templates-and-components}

I componenti e i modelli di AEM formano un toolkit molto potente. Possono essere utilizzati dagli sviluppatori per fornire agli utenti aziendali dei siti Web, agli editor e agli amministratori le funzionalità necessarie per adattare i loro siti Web alle esigenze aziendali in continua evoluzione (agilità dei contenuti), mantenendo al contempo il layout uniforme dei siti (protezione del marchio).

Una tipica sfida per una persona responsabile di un sito Web, o per un insieme di siti Web (ad esempio in una succursale di un&#39;azienda globale), è quella di introdurre un nuovo tipo di presentazione dei contenuti sui propri siti Web.

Supponiamo che sia necessario aggiungere una pagina di newslist ai siti Web, in cui sono elencati estratti di altri articoli già pubblicati. La pagina deve avere la stessa struttura e struttura del sito Web.

Il modo consigliato per affrontare tale sfida sarebbe di:

* Riutilizzate un modello esistente per creare un nuovo tipo di pagina. Il modello definisce in modo approssimativo la struttura delle pagine (elementi di navigazione, pannelli e così via), ulteriormente regolata dalla sua progettazione (CSS, grafica).
* Utilizzate il sistema paragrafo (parsys/iparsys) nelle nuove pagine.
* Consente di definire l&#39;accesso alla modalità Progettazione dei sistemi paragrafo, in modo che solo gli utenti autorizzati (in genere l&#39;amministratore) possano modificarli.
* Definite i componenti consentiti nel sistema di paragrafi specificato in modo che gli editor possano quindi posizionare i componenti richiesti sulla pagina. Nel nostro caso potrebbe trattarsi di un componente elenco, che può scorrere una sottostruttura di pagine ed estrarre le informazioni in base a regole predefinite.
* Gli editor aggiungono e configurano i componenti consentiti, sulle pagine di cui sono responsabili, per fornire le funzionalità richieste (informazioni) all&#39;azienda.

Questo approccio illustra come questo approccio consente agli utenti e agli amministratori del sito Web partecipanti di rispondere rapidamente alle esigenze aziendali, senza richiedere il coinvolgimento di team di sviluppo. Metodi alternativi, come la creazione di un nuovo modello, è in genere un esercizio costoso, che richiede un processo di gestione delle modifiche e il coinvolgimento del team di sviluppo. Ciò rende l&#39;intero processo molto più lungo e costoso.

Gli sviluppatori di sistemi basati su AEM devono pertanto utilizzare:

* modelli e controllo dell&#39;accesso alla progettazione del sistema paragrafo per uniformità e protezione del marchio
* il sistema di paragrafi, comprese le opzioni di configurazione per la flessibilità.

Le seguenti regole generali per gli sviluppatori hanno senso nella maggior parte dei progetti comuni:

* Mantenete basso il numero di modelli, fino al numero di strutture di pagina fondamentalmente diverse nei siti Web.
* Offrite ai componenti personalizzati la flessibilità e le funzionalità di configurazione necessarie.
* Ottimizzate l’utilizzo della potenza e della flessibilità del sistema paragrafo AEM, ovvero dei componenti parsys e iparsys.

### Personalizzazione di componenti e altri elementi {#customizing-components-and-other-elements}

Quando create componenti personalizzati o personalizzate un componente esistente, è spesso più semplice (e sicuro) riutilizzare le definizioni esistenti. Gli stessi principi si applicano anche ad altri elementi in AEM, ad esempio il gestore di errori.

È possibile eseguire questa operazione copiando e sovrapponendo la definizione esistente. In altre parole, copiando la definizione da `/libs` a `/apps/<your-project>`. Questa nuova definizione, in `/apps`, può essere aggiornata in base alle tue esigenze.

>[!NOTE]
>
>Consultate [Utilizzo delle sovrapposizioni](/help/sites-developing/overlays.md) per ulteriori dettagli.

Esempio:

* [Personalizzazione di un componente](/help/sites-developing/components.md)

   Questo comportava la sovrapposizione di una definizione di componente:

   * Per creare una nuova cartella di componenti, copiate `/apps/<website-name>/components/<MyComponent>` un componente esistente:

      * Ad esempio, per personalizzare la copia del componente Testo:

         * from `/libs/foundation/components/text`
         * a `/apps/myProject/components/text`

* [Personalizzazione delle pagine mostrate dal gestore errori](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Questo caso comporta la sovrapposizione di un servlet:

   * Nell&#39;archivio, copiare gli script predefiniti:

      * from `/libs/sling/servlet/errorhandler/`
      * a `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>Non **devi** cambiare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Per la configurazione e altre modifiche:
>
>1. copiate l’elemento in `/libs``/apps`
>1. apportare eventuali modifiche `/apps`


## Quando utilizzare le query JCR e quando non utilizzarle {#when-to-use-jcr-queries-and-when-not-to-use-them}

Le query JCR sono uno strumento potente quando utilizzate correttamente. Sono appropriati per:

* query reali per l’utente finale, ad esempio ricerche full text sul contenuto.
* le occasioni in cui è necessario reperire contenuti strutturati in tutto il repository.

   In tali casi, accertatevi che le query vengano eseguite solo quando è assolutamente necessario, ad esempio in caso di attivazione di un componente o di annullamento della validità della cache (invece di eseguire i passaggi dei flussi di lavoro, i gestori eventi che attivano le modifiche ai contenuti, i filtri, ecc.).

Le query JCR non devono mai essere utilizzate per richieste di rendering pure. Ad esempio, le query JCR non sono adatte a

* rendering, navigazione
* creazione di una panoramica delle 10 ultime notizie
* visualizzazione del numero di elementi di contenuto

Per eseguire il rendering del contenuto, utilizzate l&#39;accesso alla struttura del contenuto invece di eseguire una query JCR.

>[!NOTE]
>
>Se utilizzate [Query Builder](/help/sites-developing/querybuilder-api.md), potete utilizzare Query JCR, poiché Query Builder genera Query JCR sotto la cappa.


## Considerazioni sulla sicurezza {#security-considerations}

>[!NOTE]
>
>È inoltre utile fare riferimento all&#39;elenco di controllo della [sicurezza](/help/sites-administering/security-checklist.md).

### Sessioni JCR (repository) {#jcr-repository-sessions}

Utilizzate la sessione utente, non quella amministrativa. Questo significa che devi usare:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protezione contro gli script tra siti (XSS) {#protect-against-cross-site-scripting-xss}

Lo scripting tra siti (XSS) consente agli aggressori di inserire codice nelle pagine Web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti Web malintenzionati per aggirare i controlli di accesso.

AEM applica il principio di filtrare tutti i contenuti forniti dall’utente al momento dell’output. La prevenzione di XSS viene data la massima priorità sia durante lo sviluppo che durante i test.

Inoltre, un firewall per applicazioni Web, come [mod_security per Apache](https://modsecurity.org), può fornire un controllo centrale affidabile sulla sicurezza dell&#39;ambiente di distribuzione e proteggere contro attacchi di script tra siti non rilevati in precedenza.

>[!CAUTION]
>
>Il codice di esempio fornito con AEM potrebbe non essere di per sé protetto da tali attacchi e in genere si basa sul filtraggio delle richieste da parte di un firewall dell’applicazione Web.

Il foglio di controllo API XSS contiene informazioni che è necessario conoscere per utilizzare l&#39;API XSS e rendere più sicura un&#39;app AEM. Potete scaricarlo qui:

Il foglio di imbroglio XSSAPI.

[Ottieni file](assets/xss_cheat_sheet_2016.pdf)

### Comunicazione sicura per informazioni riservate {#securing-communication-for-confidential-information}

Per quanto riguarda le applicazioni Internet, assicurarsi che durante il trasporto di informazioni riservate

* il traffico è protetto tramite SSL
* HTTP POST è utilizzato se applicabile

Ciò vale per le informazioni riservate al sistema (come la configurazione o l&#39;accesso amministrativo) e per quelle riservate agli utenti (come i loro dati personali)

## Attività di sviluppo distinte {#distinct-development-tasks}

### Personalizzazione delle pagine di errore {#customizing-error-pages}

Le pagine di errore possono essere personalizzate per AEM. Questo è consigliabile in modo che l&#39;istanza non riveli tracce di utilizzo in caso di errori interni del server.

Per informazioni dettagliate, consultate [Personalizzazione delle pagine di errore visualizzate dal gestore](/help/sites-developing/customizing-errorhandler-pages.md) di errori.

### Apri file nel processo Java {#open-files-in-the-java-process}

Poiché AEM può accedere a un gran numero di file, si consiglia di configurare in modo esplicito per AEM il numero di file [aperti per un processo](/help/sites-deploying/configuring.md#open-files-in-the-java-process) Java.

Per ridurre al minimo questo problema, lo sviluppo dovrebbe garantire che tutti i file aperti vengano chiusi correttamente non appena (significativo) possibile.
