---
title: Sviluppo AEM - Linee guida e best practice
seo-title: AEM Development - Guidelines and Best Practices
description: Linee guida e migliori pratiche per lo sviluppo di AEM
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Sviluppo AEM - Linee guida e best practice{#aem-development-guidelines-and-best-practices}

## Linee guida per l’utilizzo di modelli e componenti {#guidelines-for-using-templates-and-components}

AEM componenti e modelli costituiscono un toolkit molto potente. Possono essere utilizzati dagli sviluppatori per fornire agli utenti aziendali del sito web, agli editor e agli amministratori la funzionalità di adattare i propri siti web alle esigenze aziendali in continua evoluzione (agilità dei contenuti), mantenendo al contempo il layout uniforme dei siti (protezione del marchio).

Una tipica sfida per una persona responsabile di un sito web o di un insieme di siti web (ad esempio in una succursale di un&#39;azienda globale) è quella di introdurre un nuovo tipo di presentazione dei contenuti sui propri siti web.

Supponiamo che vi sia la necessità di aggiungere una pagina della newslist ai siti web, che elenca estratti di altri articoli già pubblicati. La pagina deve avere la stessa struttura e struttura del resto del sito web.

Il modo consigliato per affrontare tale sfida è quello di:

* Riutilizza un modello esistente per creare un nuovo tipo di pagina. Il modello definisce approssimativamente la struttura della pagina (elementi di navigazione, pannelli e così via), ulteriormente regolata dalla sua progettazione (CSS, grafica).
* Utilizza il sistema paragrafo (parsys/iparsys) nelle nuove pagine.
* Definire il diritto di accesso alla modalità Progettazione dei sistemi paragrafo, in modo che solo le persone autorizzate (in genere l’amministratore) possano modificarle.
* Definisci i componenti consentiti nel sistema di paragrafi specificato in modo che gli editor possano quindi posizionare i componenti richiesti sulla pagina. Nel nostro caso potrebbe trattarsi di un componente elenco, che può attraversare una sottostruttura di pagine ed estrarre le informazioni in base a regole predefinite.
* Gli editor aggiungono e configurano i componenti consentiti, nelle pagine di cui sono responsabili, per fornire le funzionalità richieste (informazioni) all’azienda.

Questo illustra come questo approccio consente agli utenti e agli amministratori del sito web contributori di rispondere rapidamente alle esigenze aziendali, senza richiedere il coinvolgimento dei team di sviluppo. I metodi alternativi, come la creazione di un nuovo modello, sono solitamente un esercizio costoso, che richiede un processo di gestione dei cambiamenti e il coinvolgimento del team di sviluppo. Ciò rende l&#39;intero processo molto più lungo e costoso.

Gli sviluppatori di sistemi basati su AEM dovrebbero pertanto utilizzare:

* modelli e controllo dell&#39;accesso alla progettazione del sistema di paragrafi per uniformità e protezione del marchio
* sistema paragrafo, incluse le opzioni di configurazione per la flessibilità.

Nella maggior parte dei progetti comuni, le seguenti regole generali per gli sviluppatori hanno senso:

* Mantenere basso il numero di modelli - basso come il numero di strutture di pagina fondamentalmente diverse sui siti web.
* Offri ai componenti personalizzati la flessibilità e le funzionalità di configurazione necessarie.
* Massimizza l&#39;uso della potenza e della flessibilità del sistema AEM paragrafo: i componenti parsys e iparsys.

### Personalizzazione di componenti e altri elementi {#customizing-components-and-other-elements}

Quando crei i tuoi componenti o personalizzi un componente esistente, spesso è più semplice (e più sicuro) riutilizzare le definizioni esistenti. Gli stessi principi si applicano anche ad altri elementi all’interno di AEM, ad esempio il gestore di errori.

Questo può essere fatto copiando e sovrapponendo la definizione esistente. In altre parole, copia la definizione da `/libs` a `/apps/<your-project>`. Questa nuova definizione `/apps`, può essere aggiornato in base alle tue esigenze.

>[!NOTE]
>
>Vedi [Utilizzo delle sovrapposizioni](/help/sites-developing/overlays.md) per ulteriori dettagli.

Esempio:

* [Personalizzazione di un componente](/help/sites-developing/components.md)

   Questo comportava la sovrapposizione di una definizione di componente:

   * Crea una nuova cartella di componenti in `/apps/<website-name>/components/<MyComponent>` copiando un componente esistente:

      * Ad esempio, per personalizzare la copia del componente Testo :

         * da `/libs/foundation/components/text`
         * a `/apps/myProject/components/text`

* [Personalizzazione delle pagine mostrate dal gestore errori](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Questo caso comporta la sovrapposizione di un servlet:

   * Nell’archivio, copia gli script predefiniti:

      * da `/libs/sling/servlet/errorhandler/`
      * a `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>You **non deve** cambia qualsiasi cosa nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).
>
>Per la configurazione e altre modifiche:
>
>1. copia l&#39;elemento in `/libs` a `/apps`
>1. apporta modifiche all&#39;interno di `/apps`


## Quando utilizzare le query JCR e quando non usarle {#when-to-use-jcr-queries-and-when-not-to-use-them}

Le query JCR sono uno strumento potente quando vengono utilizzate correttamente. Essi sono appropriati per:

* query utente finale reali, ad esempio ricerche a testo completo sul contenuto.
* occasioni in cui è necessario trovare contenuti strutturati in tutto l’archivio.

   In tali casi, assicurati che le query vengano eseguite solo quando è assolutamente necessario, ad esempio in caso di attivazione di un componente o di annullamento della validità della cache (a differenza, ad esempio, dei passaggi dei flussi di lavoro, dei gestori eventi che attivano modifiche al contenuto, dei filtri, ecc.).

Le query JCR non devono mai essere utilizzate per richieste di rendering pure. Ad esempio, le query JCR non sono appropriate per

* navigazione di rendering
* creazione di una panoramica dei 10 elementi più recenti
* visualizzazione del numero di elementi di contenuto

Per il rendering del contenuto, utilizza l’accesso di navigazione alla struttura del contenuto invece di eseguire una query JCR.

>[!NOTE]
>
>Se utilizzi [Query Builder](/help/sites-developing/querybuilder-api.md), utilizza le query JCR, poiché Query Builder genera le query JCR sotto il cofano.

## Considerazioni sulla sicurezza {#security-considerations}

>[!NOTE]
>
>Vale anche la pena fare riferimento al [elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md).

### Sessioni JCR (Repository) {#jcr-repository-sessions}

Utilizza la sessione utente, non quella amministrativa. Questo significa che devi utilizzare:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contro lo scripting tra siti (XSS) {#protect-against-cross-site-scripting-xss}

Lo scripting tra siti (XSS) consente agli aggressori di inserire codice nelle pagine web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti web malintenzionati per aggirare i controlli di accesso.

AEM applica il principio di filtrare tutti i contenuti forniti dall’utente al momento dell’output. La prevenzione di XSS viene data la massima priorità sia durante lo sviluppo che durante i test.

Inoltre, un firewall per applicazioni web, come [mod_security per Apache](https://modsecurity.org), può fornire un controllo centrale affidabile sulla sicurezza dell’ambiente di distribuzione e proteggere da attacchi di script tra siti non rilevati in precedenza.

>[!CAUTION]
>
>Il codice di esempio fornito con AEM potrebbe non proteggere da tali attacchi e in genere si basa sul filtraggio delle richieste da parte di un firewall per applicazioni web.

Il foglio di riferimento per le API XSS contiene informazioni che devi conoscere per utilizzare l’API XSS e rendere un’app AEM più sicura. Puoi scaricarlo qui:

Il foglio di imbroglio XSSAPI.

[Ottieni file](assets/xss_cheat_sheet_2016.pdf)

### Comunicazione sicura per informazioni riservate {#securing-communication-for-confidential-information}

Per quanto riguarda qualsiasi applicazione Internet, assicurati che durante il trasporto di informazioni riservate

* traffico protetto tramite SSL
* Se applicabile, viene utilizzato HTTP POST

Ciò vale per le informazioni riservate al sistema (come la configurazione o l&#39;accesso amministrativo) e per le informazioni riservate ai suoi utenti (come i loro dati personali)

## Attività di sviluppo distinte {#distinct-development-tasks}

### Personalizzazione delle pagine di errore {#customizing-error-pages}

Le pagine di errore possono essere personalizzate per AEM. Questo è consigliabile in modo che l’istanza non riveli tracce sling su errori del server interno.

Vedi [Personalizzazione delle pagine di errore mostrate dal gestore di errori](/help/sites-developing/customizing-errorhandler-pages.md) per informazioni complete.

### Apri file nel processo Java {#open-files-in-the-java-process}

Poiché AEM può accedere a un numero elevato di file, si consiglia di [aprire file per un processo Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process) deve essere configurato in modo esplicito per AEM.

Per ridurre al minimo questo problema, lo sviluppo deve garantire che tutti i file aperti vengano chiusi correttamente non appena (in modo significativo) possibile.
