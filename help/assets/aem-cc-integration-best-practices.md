---
title: Best practice per l'integrazione con AEM e Creative Cloud
description: Best practice per integrare AEM con Adobe Creative Cloud per semplificare i flussi di lavoro di trasferimento delle risorse e ottenere la massima efficienza.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Best practice per l&#39;integrazione con AEM e Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.4 article that's behind this article in terms of content streamlining and structuring.
-->

Risorse Adobe Experience Manager è una soluzione di gestione delle risorse digitali (DAM) che può essere integrata con Adobe Creative Cloud per aiutare gli utenti DAM a collaborare con i team creativi, semplificando la collaborazione nel processo di creazione dei contenuti.

Adobe Creative Cloud offre ai team creativi un ecosistema di soluzioni e servizi per aiutarli a creare risorse digitali. Include applicazioni desktop e mobili, servizi cloud come l’archiviazione con sincronizzazione desktop o esperienza Web, nonché marketplace come Adobe Stock.

Continua a leggere per scoprire quali integrazioni scegliere tra desktop e DAM di livello Enterprise in base al tuo caso di utilizzo e quali sono le best practice associate ai flussi di lavoro di collegamento.

>[!NOTE]
>
>La condivisione delle cartelle da AEM a Creative Cloud è obsoleta e non è più inclusa in questa guida. Adobe consiglia di utilizzare funzionalità più recenti, quali [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) o l’app [desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) AEM, per fornire agli utenti creativi l’accesso alle risorse gestite in AEM.

## Esigenze di collaborazione tra creativi, esperti di marketing e utenti DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisiti | Caso di utilizzo | Superfici interessate |
|---|---|---|
| Esperienza semplificata per i creativi su desktop | Semplificate l&#39;accesso alle risorse da DAM (AEM Assets) per i creativi professionisti o, più in generale, per gli utenti desktop che lavorano nelle applicazioni native per la creazione di risorse. Hanno bisogno di un modo semplice e semplice per scoprire, usare (aprire), modificare e salvare le modifiche in AEM, nonché caricare nuovi file. | desktop Win o Mac; App Creative Cloud |
| Fornire risorse pronte all’uso di alta qualità da Adobe Stock | Gli esperti di marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l&#39;origine e l&#39;individuazione delle risorse. I creativi professionisti usano le risorse approvate direttamente dai loro strumenti creativi. | Risorse AEM; mercato Adobe Stock; campi di metadati |
| Distribuire e condividere le risorse per organizzazioni | I dipartimenti interni/le filiali locali e i partner esterni, i distributori e le agenzie utilizzano le risorse approvate condivise dall&#39;organizzazione madre. L’organizzazione intende condividere in modo sicuro e senza soluzione di continuità le risorse create per un riutilizzo più ampio. | Portale marchio, Contenuti di condivisione risorse |

## Offerte Adobe a supporto delle esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per le persone coinvolte | Offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti creativi scoprono le risorse da AEM, le aprono e le utilizzano, le modificano e caricano in AEM, nonché caricano nuovi file in AEM, senza uscire dalle app Creative Cloud. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign |
| Gli utenti aziendali semplificano l’apertura e l’utilizzo delle risorse, la modifica e il caricamento delle modifiche in AEM e il caricamento di nuovi file in AEM dall’ambiente desktop. Utilizzano un&#39;integrazione generica per aprire qualsiasi tipo di risorsa nell&#39;applicazione desktop nativa, inclusi quelli non Adobe. | [App desktop AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | App desktop AEM su Windows e Mac |
| Gli esperti di marketing e gli utenti aziendali possono scoprire, visualizzare in anteprima, concedere in licenza e salvare e gestire le risorse Adobe Stock dall’interno di AEM. Le risorse concesse in licenza e salvate forniscono metadati Adobe Stock selezionati per una migliore governance. | [Integrazione con Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | Interfaccia Web AEM |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala è brevemente indicata come caso d’uso. Per tali esigenze, prendete in considerazione Adobe Brand Portal o Asset Share Commons. Le soluzioni alternative come [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html), che possono essere create in base ai componenti di [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) , [Link Share](/help/assets/link-sharing.md), che utilizzano Risorse [](/help/assets/managing-assets-touch-ui.md) Experience Manager devono essere riviste in base a requisiti specifici.

![Connessioni Creative Cloud per AEM: Definizione di quale funzionalità utilizzare](assets/creative-connections-aem.png)

### Mappatura dei casi di utilizzo e delle soluzioni Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso d’uso | Adobe Asset Link | App desktop AEM | Note / Altre soluzioni |
|---|---|---|---|
| Scopri - Sfoglia cartelle AEM | Sì | AEM Web UI + azioni desktop | Quando sfogliate la condivisione di rete, disattivate le miniature per evitare di scaricare file binari di risorse. |
| Scopri - Accesso alle raccolte AEM | Sì | AEM Web UI + azioni desktop |  |
| Scopri - cercare risorse da AEM | Sì | AEM Web UI + azioni desktop |  |
| Usa - apri risorsa | Sì | Sì - per qualsiasi app | [Apri dall&#39;interfaccia](managing-assets-touch-ui.md#previewing-assets) Web o dal Finder |
| Utilizzo: inserire una risorsa da AEM in un documento | Sì - incorporamento | Sì - collegamento o incorporazione | L’app desktop AEM consente di accedere alle risorse come file nel file system locale. Tali collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica - aprire per la modifica | Sì - Azione di check-out | Sì - Azione aperta (nella condivisione di rete) | [Il check-out in AAL](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) salva la risorsa nell’account di archiviazione Creative Cloud dell’utente (sincronizzato dall’app Creative Cloud) per impostazione predefinita. |
| Modifica - lavoro in corso all’esterno di AEM | Sì - Risorsa disponibile nell’account di archiviazione Creative Cloud dell’utente sincronizzato con il desktop. | Sì |  |
| Modifica - modifiche di caricamento | Sì - [Check-in azione](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento facoltativo | Sì |  |
| Carica - file singolo | Sì - carica il documento attivo corrente | Sì | [Caricamento tramite interfaccia Web](managing-assets-touch-ui.md#uploading-assets) |
| Caricamento: più file/strutture di cartelle gerarchiche | No | Sì | [Caricamento tramite interfaccia](managing-assets-touch-ui.md#uploading-assets)Web;script o strumento<br>personalizzato |
| Varie - utente e login | L&#39;utente Creative Cloud che ha effettuato l&#39;accesso all&#39;app desktop Creative Cloud viene riconosciuto (SSO) | Accesso utente/accesso AEM | Gli utenti di entrambe le soluzioni contano sulla quota di utenti di AEM. |
| Varie - rete e accesso | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione AEM in rete | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione AEM in rete | Adobe Asset Link non condivide l’ambiente proxy di rete. |
| Varie - Migrazione di un numero elevato di risorse | No | No | [Guida alla migrazione](assets-migration-guide.md) |

Per supportare i casi di utilizzo della distribuzione delle risorse, è necessario considerare altre soluzioni:

* [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) per un componente aggiuntivo SaaS configurabile per Risorse AEM per pubblicare risorse.
* Le soluzioni personalizzate vengono create in base al codice [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* Condivisione [dei](/help/assets/link-sharing.md) collegamenti AEM per condividere risorse ad hoc tramite i collegamenti.
* [Interfaccia](/help/assets/managing-assets-touch-ui.md) Web di AEM Assets con aree per soggetti esterni protetti dalla configurazione di AEM Access Control e con le necessarie regolazioni di configurazione IT/rete, per consentire a questi utenti esterni di accedere ad AEM.

## Concetti chiave e casi di utilizzo {#key-concepts-and-use-cases}

### Glossario dei termini comuni {#glossary-of-common-terms}

* **** Lavoro in corso o lavorazione creativa in corso (WIP): Una fase del ciclo di vita delle risorse in cui una risorsa subisce più modifiche e in genere non è ancora pronta per essere condivisa con team più grandi.
* **** Risorse pronte per la creazione: Risorse pronte per essere condivise con un team più ampio o selezionate o approvate dal team creativo per la condivisione con i team di marketing o LOB.
* **** Approvazioni risorse: Il processo di approvazione che viene eseguito per le risorse già caricate in DAM, che in genere include approvazioni del marchio, approvazioni legali e così via.
* **** Risorsa finale: Una risorsa che ha superato tutte le approvazioni/i tag dei metadati ed è pronta per essere utilizzata dal team più ampio. Tale risorsa viene memorizzata in DAM e resa disponibile a tutti gli utenti (o a tutti gli utenti interessati). Può essere utilizzato nei canali di marketing o dai team creativi per creare progetti.
* **** Aggiornamento/modifica risorsa secondaria: Una modifica rapida e piccola a una risorsa digitale. Spesso viene effettuata in risposta a una richiesta di ritocco o di modifica minore, a una revisione delle risorse o all’approvazione (ad esempio, riposizionate, modificate le dimensioni del testo, regolate la saturazione/luminosità, il colore e così via).
* **** Aggiornamento/modifica risorsa principale: Un passaggio a una risorsa digitale che richiede un lavoro considerevole e che a volte deve essere effettuato in un periodo di tempo più lungo. Generalmente include più modifiche. La risorsa deve essere salvata più volte durante l’aggiornamento. Gli aggiornamenti principali delle risorse in genere fanno sì che la risorsa entri in una fase WIP.
* **** DAM: Gestione delle risorse digitali. In questo documento, è sinonimo di Risorse AEM Experience Manager, a meno che non venga espressamente indicato diversamente.
* **** Utente creativo: Un professionista creativo, che crea risorse digitali utilizzando le app e i servizi Creative Cloud. In alcuni casi, un utente creativo può essere membro di un team creativo che può utilizzare Creative Cloud, ma non crea risorse digitali (come un direttore creativo o un manager del team creativo).
* **** Utente DAM: Utente tipico di un sistema DAM. A seconda dell’organizzazione, un utente DAM può essere un utente di marketing o non di marketing, ad esempio un utente Line-of-Business (LOB), un venditore, un venditore e così via.

### Considerazioni sull’utilizzo dell’integrazione AEM e Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

* Consultate Best practice per le app [desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Consultate Integrazione [con Adobe Stock](aem-assets-adobe-stock.md)
* Consultate Collegamento risorse [Adobe](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Questo è un breve riepilogo delle best practice per l&#39;integrazione di Experience Manager e Creative Cloud. Leggi il resto del documento per avere una comprensione dettagliata di questi.

* **** Per gli utenti creativi che lavorano in Photoshop, InDesign o Illustrator: Adobe Asset Link offre la migliore esperienza utente, inclusa la gestione del lavoro in corso sulle risorse estratte da AEM
* **** Per semplificare l’accesso alle risorse dal desktop per qualsiasi formato di file o applicazione generico: app desktop AEM
* **** Scopri perché e quando archiviare le risorse in DAM: Aggiornamenti da rendere disponibili al team più ampio della tua organizzazione
* **** Considerate il volume di risorse condivise: Se il caso d’uso è la distribuzione delle risorse, governance e sicurezza potrebbero essere gli aspetti più importanti. Considerate l’utilizzo di strumenti creati per farlo in scala, come Brand Portal.
* **** Comprendere il ciclo di vita delle risorse: Scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **** Gestite con attenzione i salvataggi frequenti sulle risorse: Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire attività in corso in cartelle condivise o mappate a meno che non siano necessarie tutte le modifiche in DAM

### Accesso alle risorse Adobe Stock da Risorse AEM {#access-to-adobe-stock-assets-from-aem-assets}

[L’integrazione](/help/assets/aem-assets-adobe-stock.md) di AEM e Adobe Stock consente agli utenti AEM di cercare, visualizzare in anteprima, concedere in licenza e salvare risorse da Adobe Stock in AEM. Le risorse Adobe Stock concesse in licenza e salvate hanno selezionato i metadati Stock, che possono essere utilizzati per la ricerca con altri filtri.

Alcuni punti importanti su questa integrazione:

* Quando le risorse di Adobe stock vengono salvate in AEM, diventano normali risorse AEM, con file binari salvati nell’archivio AEM. Alcuni metadati relativi ad Adobe Stock vengono salvati per la risorsa in AEM, altrimenti il processo di assimilazione sarà simile a quello di qualsiasi altro file. Ad esempio, se i tag avanzati sono attivi, al momento del salvataggio vengono aggiunti a tali risorse.
* La risorsa salvata in AEM è una copia, non un collegamento in Adobe Stock.

**Utilizzo delle risorse salvate da Adobe Stock in AEM in Creative Cloud**. Questa integrazione è indipendente da Adobe Asset Link, ma Adobe Asset Link riconosce le risorse salvate da Stock in questo modo e visualizza metadati aggiuntivi e l’icona Stock su queste risorse nell’interfaccia utente dell’estensione Adobe Asset Link in Photoshop, Illustrator o InDesign. I file sono disponibili per la navigazione, l’apertura e così via, perché sono normali risorse AEM se salvate in AEM.
Gli utenti Creative Cloud che lavorano nelle app Creative Cloud con l’estensione Adobe Asset Link presente, oltre a poter accedere a risorse già concesse in licenza da Adobe Stock in AEM, possono anche utilizzare il pannello Creative Cloud Libraries per cercare, visualizzare in anteprima e concedere in licenza risorse Adobe Stock.
Le risorse da Adobe Stock con licenza e salvate in AEM diventano disponibili per i team più grandi che accedono alla distribuzione di Risorse AEM, mentre le risorse per la licenza di Adobe Stock mediante il pannello Creative Cloud Libraries le rendono disponibili per se stesse solo per impostazione predefinita nel loro account Creative Cloud.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## Memorizzazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra i team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante comprendere quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse sono memorizzate in DAM {#why-assets-are-stored-in-dam}

La memorizzazione delle risorse in DAM le rende facilmente accessibili e accessibili. Garantisce che le risorse possano essere sfruttate da numerosi utenti in tutta l&#39;organizzazione o l&#39;ecosistema, compresi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di archiviare solo le risorse rilevanti per i processi di marketing/LOB a valle (la pubblicazione su canali come il canale Web tramite AEM Sites o altri canali serviti da Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e misurati da Analytics Cloud, fornendo a utenti/partner e così via). Inoltre, le organizzazioni memorizzano le risorse che possono essere sottoposte a un processo di revisione/approvazione in DAM. In questo modo, DAM memorizza principalmente le risorse che hanno alte probabilità di essere sfruttate ed evita di archiviare le risorse inutilizzate.

La memorizzazione delle risorse è inoltre soggetta a considerazioni tecniche e di utilizzo delle risorse. DAM offre servizi aggiuntivi sulle risorse memorizzate, come l’estrazione di metadati, il controllo delle versioni, la generazione di anteprime/transcodifica, la gestione dei riferimenti e l’aggiunta di informazioni sul controllo degli accessi. Questi servizi richiedono tempo e risorse aggiuntive per l&#39;infrastruttura.

Spesso, non è consigliabile memorizzare tutte le risorse e gli aggiornamenti. Ad esempio, se gli aggiornamenti a risorse specifiche sono di scarsa qualità e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team creativi (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del ciclo di vita delle risorse. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Risorse che devono ancora essere completate o che devono essere sperimentate
* Risorse che non superano il ciclo di revisione del team creativo/interno
* Rispetto alla risorsa in questione, la squadra ha candidati migliori per rappresentare il proprio lavoro a squadre esterne

In genere, le risorse delle classi seguenti vengono memorizzate in DAM:

* Attività che hanno raggiunto una certa scadenza e sono considerate pronte per essere condivise
* Risorse preselezionate dal team creativo
* Formati di risorse specifici utilizzabili o richiesti dal marketing, a seconda di un contratto o contratto specifico (ad esempio, file JPG convertiti da file RAW, TIFF/immagini da originali PSD)

#### Quando vengono memorizzati gli aggiornamenti delle risorse in DAM {#when-updates-to-assets-are-stored-in-dam}

Di regola, solo gli aggiornamenti alle risorse rilevanti per il più ampio set di utenti DAM devono essere memorizzati in DAM. Essa garantisce che gli utenti (funzioni di marketing e simili) vedano solo le versioni rilevanti nella timeline delle risorse DAM.

In genere, le modifiche sono correlate alle tappe principali del ciclo di vita delle risorse. Ad esempio, la risorsa iniziale pronta per il marketing o un aggiornamento ufficiale basato su richiesta/revisione fornita dal team creativo devono essere memorizzati e dotati di versione in DAM.

L&#39;aggiornamento del team creativo per la revisione da parte del team marketing dopo una richiesta di modifica della risorsa esistente in DAM è un esempio di aggiornamento rilevante. Deve essere memorizzato e conservato in DAM per ulteriori riferimenti o per ripristinare la versione precedente.

Di seguito sono riportati alcuni esempi di aggiornamenti generalmente non rilevanti:

* Versioni precedenti delle risorse caricate prima che siano pronte per la revisione del marketing
* Frequenti modifiche creative alla risorsa nella fase di lavoro in corso prima che i team creativi e di marketing decidano che la risorsa è pronta

### Accesso utente a DAM {#user-access-to-dam}

Risorse AEM supporta due tipi di utenti in base al loro accesso alla distribuzione di Risorse AEM. In genere, gli utenti all&#39;interno della rete aziendale (firewall) hanno accesso diretto a DAM. Gli altri utenti esterni alla rete aziendale non avrebbero accesso diretto. Il tipo di utente determina le integrazioni utilizzabili dal punto di vista tecnico.

#### Utenti creativi con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/i professionisti creativi caricati sulla rete interna hanno accesso all’istanza DAM, incluso l’accesso AEM. AEM e l’infrastruttura di rete possono essere configurate per consentire l’accesso diretto alle parti esterne, in genere organizzazioni affidabili come le agenzie che lavorano per un cliente, per accedere ad AEM tramite rete (ad esempio tramite VPN o whitelist IP).

In tali casi, Adobe Asset Link o l’app desktop AEM consente di accedere facilmente alle risorse finali/approvate e di salvare le risorse pronte per la creazione in DAM.

#### Utenti creativi senza accesso a DAM {#creative-users-without-access-to-dam}

Le agenzie esterne e i freelance senza accesso diretto all’istanza DAM possono richiedere l’accesso alle risorse approvate o desiderano aggiungere nuove progettazioni al DAM.

Utilizzate le seguenti strategie per fornire l&#39;accesso alle risorse finali/approvate:

* Utilizzate l’app desktop se il collegamento risorsa non funziona.
* Utilizzare [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) per distribuire le risorse in modo sicuro ai partner esterni
* Utilizzare un&#39;implementazione personalizzata di un portale di distribuzione e determinazione origine basato su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizza il controllo degli accessi impostato in AEM e l’infrastruttura di rete necessaria (ad esempio, la whitelist VPN e IP) per consentire alle parti esterne di accedere a un’area dedicata di contenuto nel tuo DAM. Possono utilizzare l’interfaccia utente Web di AEM per ottenere risorse e caricare nuovi contenuti in DAM.

#### Lavoro in corso sulle risorse da AEM {#work-in-progress-on-assets-from-aem}

Come discusso in questo documento, si consiglia di eseguire importanti aggiornamenti sulle risorse, talvolta denominati lavoro in corso, senza che tutte le modifiche salvate nel file locale siano caricate anche su AEM come modifiche. Questo consente di velocizzare il lavoro di un utente desktop, limitare la larghezza di banda utilizzata e mantenere la timeline delle risorse pulita e focalizzata sugli aggiornamenti principali e controllati.

Adobe Asset Link offre un buon supporto per questo caso di utilizzo:

* Quando gli utenti in Photoshop, InDesign o Illustrator intendono modificare un file, eseguono un’operazione di estrazione sulla risorsa specificata
* La risorsa viene scaricata in background, inserita nell’account Creative Cloud sincronizzato su disco dall’app desktop Creative Cloud e il flag di estrazione è attivato in AEM sulla risorsa per ridurre al minimo i conflitti di modifica
* Da qui in poi, l&#39;utente lavora in un file memorizzato localmente nella posizione sincronizzata, e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account Creative Cloud, è disponibile anche su altri dispositivi che l’utente potrebbe avere (ad esempio, può essere aperta o modificata in un’app mobile Creative Cloud dedicata) e può essere condivisa con altri utenti Creative Cloud a scopo di collaborazione.
* Al termine delle modifiche, l’utente creativo può eseguire un’operazione di check-in sul file nell’applicazione Creative Cloud, con un commento facoltativo. La risorsa corrispondente in AEM dispone di una versione e viene aggiornata con il nuovo binario. Gli utenti AEM, come gli esperti di marketing o gli utenti LOB, possono accedere alle modifiche o alle pietre miliari principali delle risorse tramite l’interfaccia utente della timeline delle risorse AEM.

L&#39;app desktop AEM fornisce una condivisione di rete per le risorse aperte nell&#39;app nativa. Per impostazione predefinita, tutte le modifiche effettuate localmente vengono caricate automaticamente in AEM dopo un breve periodo di tempo. Grazie a questa configurazione, i frequenti risparmi durante la fase di lavoro in corso vengono caricati in AEM e versioni, creando un sacco di traffico di rete e potenziali problemi di scalabilità, per non parlare delle versioni non necessarie in AEM.

L’approccio consigliato consiste nell’utilizzare un’opzione nell’app desktop AEM per disattivare gli aggiornamenti automatizzati e caricare manualmente le modifiche alle risorse in AEM, sfruttando l’azione di caricamento delle modifiche nell’interfaccia utente Stato risorsa dell’app.

#### Caricamento in blocco su DAM {#bulk-upload-to-dam}

In alcuni scenari potrebbe essere necessario caricare simultaneamente un numero maggiore di file in DAM, ad esempio:

* Caricamento dei risultati di fotoscatti o di progetti più grandi
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento delle risorse selezionate da un set più grande se la selezione viene effettuata al di fuori di DAM

La descrizione fa riferimento al caricamento di file operativamente (ad esempio, ogni settimana o con ogni singola foto), come parte normale del flusso di lavoro dell’utente desktop. Le migrazioni di risorse di grandi dimensioni non sono incluse in questa sezione.

Potete sfruttare le seguenti funzionalità di caricamento:

* Per caricare cartelle grandi o gerarchiche in massa, utilizzate l&#39;app desktop AEM che fornisce funzionalità di caricamento [delle](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) cartelle. Potete anche caricare strutture di cartelle gerarchiche. Le risorse vengono caricate in background e, di conseguenza, non sono collegate a una sessione del browser Web
* Per caricare alcuni file da una singola cartella, trascinateli direttamente nell’interfaccia Web o utilizzate l’opzione Crea nell’interfaccia Web di Risorse AEM.
* A seconda delle esigenze aziendali, potete anche utilizzare il caricatore personalizzato.

#### Gestione delle risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se utilizzate Condivisione file di rete per gestire le risorse digitali, l&#39;utilizzo della condivisione di rete mappata dall&#39;app desktop AEM potrebbe essere considerato un comodo sostituto. Quando si passa da condivisioni di file di rete, l’interfaccia Web di AEM fornisce un set completo di funzionalità di gestione delle risorse digitali che vanno ben oltre quanto possibile su una condivisione di rete (ricerca, raccolte, metadati, collaborazione, anteprime e così via), e l’app desktop AEM fornisce un collegamento pratico per connettere l’archivio DAM lato server al lavoro sul desktop.

Evitate di utilizzare l&#39;app desktop AEM per gestire le risorse direttamente nella condivisione di rete di Risorse AEM. Ad esempio, evitate di utilizzare l&#39;app desktop AEM per spostare/copiare più file. Utilizzate invece l&#39;interfaccia utente Web di Risorse AEM per trascinare le cartelle dal Finder/Esplora risorse alla condivisione di rete o utilizzate la funzione di caricamento delle cartelle di Risorse AEM.

#### Migrazione delle risorse {#asset-migration}

Per pianificare ed eseguire la migrazione delle risorse dal sistema esistente a un nuovo sistema o per migrare un grande volume di risorse memorizzate sui server, consulta la Guida alla [migrazione](/help/assets/assets-migration-guide.md). L&#39;app desktop AEM e le integrazioni AEM con Creative Cloud non supportano tali migrazioni. A causa dell’elevato volume di risorse da assimilare e dei requisiti aggiuntivi relativi alla mappatura dei metadati, alla trasformazione e all’assimilazione, le migrazioni devono essere gestite mediante strumenti e approcci diversi.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [Best practice per le app desktop AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [AEM Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integrazione di AEM e Adobe Stock](aem-assets-adobe-stock.md)

