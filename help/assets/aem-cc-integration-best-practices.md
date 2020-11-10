---
title: Integrazione con le best practice Adobe Creative Cloud
description: Procedure ottimali per l’ [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] integrazione, per semplificare i flussi di lavoro di trasferimento delle risorse e ottenere un’elevata velocità dei contenuti.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '3248'
ht-degree: 16%

---


# [!DNL Adobe Experience Manager] e procedure ottimali per [!DNL Creative Cloud] l&#39;integrazione {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] è una soluzione di gestione delle risorse digitali (DAM) che può essere integrata con [!DNL Adobe Creative Cloud] per aiutare gli utenti DAM a collaborare con i team creativi, semplificando la collaborazione nel processo di creazione dei contenuti.

[!DNL Adobe Creative Cloud] fornisce ai team creativi un ecosistema di soluzioni e servizi per aiutarli a creare risorse digitali. Include applicazioni desktop e mobili, servizi cloud come l&#39;archiviazione con sincronizzazione desktop o esperienza Web, nonché marketplace come [!DNL Adobe Stock].

Continua a leggere per scoprire quali integrazioni scegliere tra desktop e DAM di livello Enterprise in base al tuo caso di utilizzo e quali sono le best practice associate ai flussi di lavoro di collegamento.

>[!NOTE]
>
>[!DNL Experience Manager] la condivisione delle [!DNL Creative Cloud] cartelle è obsoleta e non è più inclusa in questa guida.  Adobe consiglia di utilizzare funzionalità più recenti, come [collegamento](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) risorse Adobe o l’app [desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html)  per fornire agli utenti creativi l’accesso alle risorse gestite in [!DNL Experience Manager].

## Esigenze di collaborazione tra creativi, esperti di marketing e utenti DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisiti | Caso di utilizzo | Superfici interessate |
|---|---|---|
| Esperienza semplificata per i creativi su desktop | Semplificate l&#39;accesso alle risorse da un DAM ([!DNL Experience Manager Assets]) per i creativi professionisti o, più in generale, per gli utenti desktop che lavorano nelle applicazioni native per la creazione di risorse. Hanno bisogno di un modo semplice e semplice per scoprire, usare (aprire), modificare e salvare le modifiche in [!DNL Experience Manager]e caricare nuovi file. | desktop Win o Mac; [!DNL Creative Cloud] apps |
| Fornire risorse pronte all’uso di alta qualità da [!DNL Adobe Stock] | Gli esperti di marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l&#39;origine e l&#39;individuazione delle risorse. I creativi professionisti usano le risorse approvate direttamente dai loro strumenti creativi. | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] mercato; campi di metadati |
| Distribuire e condividere le risorse per organizzazioni | I dipartimenti interni/le filiali locali e i partner esterni, i distributori e le agenzie utilizzano le risorse approvate condivise dall&#39;organizzazione madre. L&#39;organizzazione intende condividere in modo sicuro e senza soluzione di continuità le risorse create per un riutilizzo più ampio. | Portale del marchio, Contenuti di condivisione delle risorse |

## Offerte  Adobe per supportare le esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per le persone coinvolte |  offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti creativi scoprono le risorse da [!DNL Experience Manager], le aprono e le utilizzano, le modifiche e il caricamento di [!DNL Experience Manager]modifiche, nonché il caricamento di nuovi file in [!DNL Experience Manager], senza uscire dalle [!DNL Creative Cloud] app. | [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign]. |
| Gli utenti aziendali semplificano l’apertura e l’utilizzo delle risorse, la modifica e il caricamento delle modifiche [!DNL Experience Manager]e il caricamento di nuovi file [!DNL Experience Manager] dall’ambiente desktop. Utilizzano un&#39;integrazione generica per aprire qualsiasi tipo di risorsa nell&#39;applicazione desktop nativa, inclusi quelli non  Adobe. | [app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] app desktop su Windows e Mac desktop |
| Gli esperti di marketing e gli utenti aziendali possono scoprire, visualizzare in anteprima, concedere in licenza e salvare le [!DNL Adobe Stock] risorse e gestirle dall&#39;interno [!DNL Experience Manager]. Le risorse concesse in licenza e salvate forniscono [!DNL Adobe Stock] metadati specifici per una migliore governance. | [Integrazione  Experience Manager e  Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interfaccia web |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala viene brevemente citata come caso d’uso. Per tali esigenze, valuta prodotti come Adobe Brand Portal o Asset Share Commons. Alternate solutions such as [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), solutions that can be built based on [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) components, [Link Share](/help/assets/link-sharing.md), using [Experience Manager Assets](/help/assets/manage-assets.md) should be reviewed based on specific requirement.

![Creative Cloud connessioni per  Experience Manager, decidere quale funzionalità utilizzare](assets/creative-connections-aem.png)

### Mappatura di casi di utilizzo e soluzioni  Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso d’uso  | [!DNL Adobe Asset Link] | [!DNL Experience Manager] app desktop | Note / Altre soluzioni |
|---|---|---|---|
| Scopri - sfogliare le cartelle DAM | Sì | [!DNL Experience Manager] Azioni interfaccia Web e desktop |  |
| Scopri - Accesso alle raccolte DAM | Sì | [!DNL Experience Manager] Azioni interfaccia Web e desktop |  |
| Scopri - cercare risorse da DAM | Sì | [!DNL Experience Manager] Azioni interfaccia Web e desktop |  |
| Usa - apri risorsa | Sì | Sì | [Apri dall&#39;interfaccia](manage-assets.md#previewing-assets) Web o dal Finder |
| Utilizzo: posizionamento di risorse da DAM in un documento | Sì - incorporamento | Sì - collegamento o incorporazione | [!DNL Experience Manager] l’app desktop consente di accedere alle risorse come file nel file system locale. Tali collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica - aprire per la modifica | Sì - Azione di check-out | Sì - Azione di apertura (nella condivisione di rete) | [Il check-out in AAL](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) salva la risorsa nell’account di archiviazione Creative Cloud dell’utente (sincronizzato dall’app di Creative Cloud) per impostazione predefinita. |
| Modifica - lavoro in corso al di fuori di DAM | Sì - Risorsa disponibile nell’account di archiviazione di Creative Cloud dell’utente sincronizzato con il desktop. | Sì |  |
| Modifica - modifiche di caricamento | Sì - [Check-in azione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento facoltativo | Sì |  |
| Carica - file singolo | Sì - carica il documento attivo corrente | Sì | [Caricamento tramite interfaccia Web](manage-assets.md#uploading-assets) |
| Caricamento: più file/strutture di cartelle gerarchiche | No | Sì | [Caricate tramite interfaccia](manage-assets.md#uploading-assets) Web o tramite script o strumenti personalizzati. |
| Varie - utente e login | Creative Cloud utente che ha eseguito l&#39;accesso all&#39;app desktop di Creative Cloud viene riconosciuto (SSO) | [!DNL Experience Manager] utente e credenziali | Gli utenti di entrambe le soluzioni contano sulla quota [!DNL Experience Manager] di utenti. |
| Varie - rete e accesso | Richiede l&#39;accesso dal desktop dell&#39;utente alla [!DNL Experience Manager] distribuzione in rete | Richiede l&#39;accesso dal desktop dell&#39;utente alla [!DNL Experience Manager] distribuzione in rete | [!DNL Adobe Asset Link] non condivide l&#39;ambiente proxy di rete. |
| Varie - Migrazione di un numero elevato di risorse | No | No | [Guida alla migrazione delle risorse](assets-migration-guide.md) |

Per supportare i casi di utilizzo della distribuzione delle risorse, è necessario considerare altre soluzioni:

* [Portale](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) marchio per un componente aggiuntivo SaaS configurabile per [!DNL Experience Manager Assets] pubblicare le risorse.
* Le soluzioni personalizzate vengono create in base al codice di base di [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* [!DNL Experience Manager] [condivisione](/help/assets/link-sharing.md) di collegamenti per condividere risorse ad hoc tramite i collegamenti.
* [Experience Manager Interfaccia](/help/assets/manage-assets.md) Web Assets con aree per soggetti esterni protette dalla configurazione del controllo di [!DNL Experience Manager] accesso e con le necessarie regolazioni di configurazione IT/di rete, per consentire a questi utenti esterni di accedere a [!DNL Experience Manager].

## Concetti chiave e casi di utilizzo {#key-concepts-and-use-cases}

### Glossario dei termini comuni {#glossary-of-common-terms}

* **Work-in-progress o creative work-in-progress (WIP):** una fase del ciclo di vita delle risorse in cui una risorsa subisce più modifiche e, in genere, non è ancora pronta per essere condivisa con team più grandi.
* **Risorse pronte per la creazione:** [!DNL Assets] pronti per essere condivisi con un team più ampio, oppure selezionati o approvati dal team creativo per la condivisione con i team di marketing o LOB.
* **Asset approvals (Approvazioni risorse):** il processo di approvazione che viene eseguito per le risorse già caricate in DAM, che, in genere, include approvazioni del marchio, approvazioni legali e così via.
* **Final asset (Risorsa finale):** una risorsa che ha superato tutte le approvazioni/assegnazione tag dei metadati ed è pronta per essere utilizzata dal team più ampio. Tale risorsa viene memorizzata in DAM, per poi essere resa disponibile a tutti gli utenti (o a tutti gli interessati). Può essere utilizzata nei canali di marketing o dai team creativi per la creazione di design.
* **Minor asset update/change (Aggiornamento/modifica risorsa secondaria):** una modifica rapida e piccola a una risorsa digitale. Spesso viene effettuata in risposta a una richiesta di ritocco o di modifica minore, a una revisione delle risorse o all’approvazione (ad esempio: riposizionamento, modifica dimensioni del testo, regolazione di saturazione/luminosità, colore e così via).
* **Major asset update/change (Aggiornamento/modifica risorsa principale):** un passaggio a una risorsa digitale che richiede un lavoro considerevole e che a volte deve essere effettuato in un periodo di tempo più lungo. Generalmente include più modifiche. La risorsa deve essere salvata più volte durante l’aggiornamento. In genere, gli aggiornamenti principali delle risorse fanno sì che la risorsa entri in una fase WIP.
* **DAM:** gestione delle risorse digitali. In this document, it is synonymous with [!DNL Experience Manager Assets], unless specifically mentioned otherwise.
* **Creative user (Utente creativo):** un professionista che crea risorse digitali utilizzando le app e i servizi Creative Cloud. In alcuni casi, è possibile che un utente creativo sia membro di un team creativo che utilizza Creative Cloud, ma che non crea risorse digitali, ad esempio un direttore creativo o un manager del team creativo.
* **DAM user (Utente DAM)**: utente tipico di un sistema DAM. A seconda dell’organizzazione, un utente DAM può essere di marketing o non, come un utente Line-of-Business (LOB), un bibliotecario, un venditore e così via.

### Considerazioni sull&#39;utilizzo [!DNL Experience Manager] e l&#39; [!DNL Creative Cloud] integrazione {#considerations-when-using-aem-and-creative-cloud-integration}

* Consultate Best practice per le app [desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)
* Consultate Integrazione [Adobe Stock](aem-assets-adobe-stock.md)
* Consultate [collegamento Adobe risorse](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)

Questo è un breve riepilogo delle best practice per [!DNL Experience Manager] e [!DNL Creative Cloud] integrazione. Leggi il resto del documento per avere una comprensione dettagliata di questi.

* **For creative users, working in Photoshop, InDesign, or Illustrator (Per gli utenti creativi che lavorano in Photoshop, InDesign o Illustrator)**: Adobe Asset Link offre la migliore esperienza utente possibile, inclusa la gestione del Work-in-progress sulle risorse estratte da [!DNL Experience Manager].
* **Per semplificare l’accesso alle risorse dal desktop per qualsiasi formato di file o applicazione generico:** utilizzate l&#39;app [!DNL Experience Manager] desktop.
* **Understand why and when to store assets in DAM (Scopri perché e quando archiviare le risorse in DAM)**: aggiornamenti da rendere disponibili al team più ampio della tua organizzazione.
* **Mind the volume of assets shared (Considera il volume di risorse condivise):** se il caso d’uso è la distribuzione delle risorse, la governance e la sicurezza potrebbero diventare gli aspetti più importanti. Valuta l’utilizzo di strumenti creati per il lavoro in scala, come Brand Portal.
* **Understand asset lifecycle (Informazioni sul ciclo di vita delle risorse):** scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **Handle frequent saves to assets with care (Gestisci con attenzione i salvataggi frequenti nelle risorse):** Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire le attività WIP in cartelle condivise o mappate, a meno che non ti servano tutte le modifiche all’interno di DAM

### Accesso alle [!DNL Adobe Stock] risorse da [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[&#39;integrazione](/help/assets/aem-assets-adobe-stock.md) di Adobe Stock e Experience Manager  offre agli [!DNL Experience Manager] utenti la possibilità di cercare, visualizzare in anteprima, concedere in licenza e salvare le risorse [!DNL Adobe Stock] in [!DNL Experience Manager]. Le [!DNL Stock] risorse concesse in licenza e salvate hanno selezionato [!DNL Stock] i metadati, che possono essere utilizzati per la ricerca con altri filtri.

Alcuni punti importanti su questa integrazione:

* Quando vengono salvate le risorse da  stock di Adobe in [!DNL Experience Manager], queste diventano regolari [!DNL Assets]e il file binario viene salvato nella [!DNL Experience Manager] directory archivio. Alcuni metadati relativi a [!DNL Adobe Stock] [!DNL Experience Manager]vengono salvati per la risorsa in, in caso contrario il processo di assimilazione sarà simile a quello di qualsiasi altro file. Ad esempio, se i tag avanzati sono attivi, al momento del salvataggio vengono aggiunti a tali risorse.
* La risorsa salvata in [!DNL Experience Manager] è una copia, non un collegamento in [!DNL Adobe Stock].

**Utilizzo delle risorse salvate da [!DNL Adobe Stock] in [!DNL Experience Manager] in[!DNL Creative Cloud]**. Questa integrazione è indipendente da [!DNL Adobe Asset Link], ma [!DNL Adobe Asset Link] riconosce le risorse salvate in [!DNL Stock] quel modo e visualizza metadati aggiuntivi e un [!DNL Adobe Stock] logo su tali risorse nell’interfaccia utente delle [!DNL Adobe Asset Link] estensioni in [!DNL Photoshop], [!DNL Illustrator]o [!DNL InDesign]. I file sono disponibili per la navigazione, l’apertura e così via, poiché sono risorse normali al momento del salvataggio in [!DNL Experience Manager].
Gli utenti creativi che lavorano nelle [!DNL Creative Cloud] app con [!DNL Adobe Asset Link] estensione presente, oltre ad avere accesso alle risorse già concesse in licenza da [!DNL Adobe Stock] a [!DNL Experience Manager], possono anche utilizzare il pannello [!DNL Creative Cloud] Librerie per cercare, visualizzare in anteprima e concedere in licenza [!DNL Adobe Stock] le risorse.
[!DNL Assets] da [!DNL Adobe Stock] concesso in licenza e salvato in [!DNL Experience Manager] diventano disponibili per i team più grandi che accedono alla [!DNL Experience Manager Assets] distribuzione, mentre i creativi che dispongono di licenze per le risorse [!DNL Adobe Stock] tramite il pannello [!DNL Creative Cloud] Librerie le rendono disponibili a se stessi solo per impostazione predefinita nel loro [!DNL Creative Cloud] account.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Memorizzazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra i team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante comprendere quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse sono memorizzate in DAM {#why-assets-are-stored-in-dam}

La memorizzazione delle risorse in DAM le rende facilmente accessibili e accessibili. Garantisce che le risorse possano essere sfruttate da numerosi utenti in tutta l&#39;organizzazione o l&#39;ecosistema, compresi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di archiviare solo le risorse rilevanti per i processi di marketing/LOB a valle (la pubblicazione su canali come canali Web tramite [!DNL Experience Manager Sites] o altri canali serviti da Adobe Experience Cloud - Marketing Cloud,  Advertising Cloud, e misurati da  Analytics Cloud, fornendo a utenti/partner e così via). Inoltre, le organizzazioni memorizzano le risorse che possono essere sottoposte a un processo di revisione/approvazione in DAM. In questo modo, DAM memorizza principalmente le risorse che hanno alte probabilità di essere sfruttate ed evita di archiviare le risorse inutilizzate.

La memorizzazione delle risorse è inoltre soggetta a considerazioni tecniche e di utilizzo delle risorse. DAM offre servizi aggiuntivi sulle risorse memorizzate, come l’estrazione di metadati, il controllo delle versioni, la generazione di anteprime/transcodifica, la gestione dei riferimenti e l’aggiunta di informazioni sul controllo degli accessi. Questi servizi richiedono tempo e risorse aggiuntive per l&#39;infrastruttura.

Spesso, non è consigliabile memorizzare tutte le risorse e gli aggiornamenti. Ad esempio, se gli aggiornamenti a risorse specifiche sono di scarsa qualità e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team creativi (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del ciclo di vita delle risorse. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Risorse che devono ancora essere completate o che devono essere sperimentate.
* Risorse che non superano il ciclo di revisione creativo/interno del team.
* Rispetto alla risorsa in questione, la squadra ha candidati migliori per rappresentare il proprio lavoro a squadre esterne.

In genere, le risorse delle classi seguenti vengono memorizzate in DAM:

* Attività che hanno raggiunto una certa scadenza e sono considerate pronte per essere condivise.
* Risorse preselezionate dal team creativo.
* Formati di risorse specifici utilizzabili o richiesti dal marketing, a seconda di un contratto o di un contratto specifico (ad esempio, file JPG convertiti da file RAW, TIFF/immagini da originali PSD).

#### Quando vengono memorizzati gli aggiornamenti delle risorse in DAM {#when-updates-to-assets-are-stored-in-dam}

Di regola, solo gli aggiornamenti alle risorse rilevanti per il più ampio set di utenti DAM devono essere memorizzati in DAM. Essa garantisce che gli utenti (funzioni di marketing e simili) vedano solo le versioni rilevanti nella timeline delle risorse DAM.

In genere, le modifiche sono correlate alle tappe principali del ciclo di vita delle risorse. Ad esempio, la risorsa iniziale pronta per il marketing o un aggiornamento ufficiale basato su richiesta/revisione fornita dal team creativo devono essere memorizzati e dotati di versione in DAM.

L&#39;aggiornamento del team creativo per la revisione da parte del team marketing dopo una richiesta di modifica della risorsa esistente in DAM è un esempio di aggiornamento rilevante. Deve essere memorizzato e conservato in DAM per ulteriori riferimenti o per ripristinare la versione precedente.

Di seguito sono riportati alcuni esempi di aggiornamenti generalmente non rilevanti:

* Versioni precedenti delle risorse caricate prima che siano pronte per la revisione del marketing
* Frequenti modifiche creative alla risorsa nella fase di lavoro in corso prima che i team creativi e di marketing decidano che la risorsa è pronta

### Accesso utente a DAM {#user-access-to-dam}

[!DNL Assets] supporta due tipi di utenti in base al loro accesso alla [!DNL Assets] distribuzione. In genere, gli utenti all&#39;interno della rete aziendale (firewall) hanno accesso diretto a DAM. Gli altri utenti esterni alla rete aziendale non avrebbero accesso diretto. Il tipo di utente determina quali integrazioni possono essere utilizzate dal punto di vista tecnico.

#### Utenti creativi con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/i professionisti creativi caricati sulla rete interna hanno accesso alla distribuzione DAM, incluso il [!DNL Experience Manager] login. [!DNL Experience Manager] e l&#39;infrastruttura di rete può essere impostata per consentire l&#39;accesso diretto alle parti esterne - solitamente organizzazioni affidabili come le agenzie che lavorano per un cliente - per avere accesso a [!DNL Experience Manager] una rete, ad esempio tramite VPN o elenco Consentiti di  IP.

In tali casi,  collegamento risorse di Adobe o l’app [!DNL Experience Manager] desktop consente di accedere facilmente alle risorse finali/approvate e consente di salvare le risorse pronte per la creazione in DAM.

#### Utenti creativi senza accesso a DAM {#creative-users-without-access-to-dam}

Agenzie esterne e freelance senza accesso diretto alla distribuzione DAM possono richiedere l&#39;accesso alle risorse approvate o desiderano aggiungere le loro nuove progettazioni al DAM.

Utilizzate le seguenti strategie per fornire l&#39;accesso alle risorse finali/approvate:

* Utilizzate l’app desktop se il collegamento risorsa non funziona.
* Utilizzare [Portale](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) del marchio Assets per distribuire le risorse in modo sicuro ai partner esterni
* Utilizzare un&#39;implementazione personalizzata di un portale di distribuzione e determinazione origine basato su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizza il controllo degli accessi impostato nell&#39;infrastruttura di rete [!DNL Experience Manager] e nell&#39;infrastruttura necessaria (ad esempio, VPN e elenco Consentiti di  IP) per consentire alle parti esterne di accedere a un&#39;area dedicata di contenuto nel tuo DAM. Possono utilizzare l&#39;interfaccia [!DNL Experience Manager] Web per ottenere risorse e caricare nuovi contenuti in DAM.

#### Lavoro in corso sulle risorse da [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Come discusso in questo documento, si consiglia di eseguire importanti aggiornamenti sulle risorse, talvolta denominati lavoro in corso, senza che tutte le modifiche salvate nel file locale siano caricate anche [!DNL Experience Manager] come modifiche. Questo consente di velocizzare il lavoro di un utente desktop, limitare la larghezza di banda utilizzata e mantenere la timeline delle risorse pulita e focalizzata sugli aggiornamenti principali e controllati.

 collegamento risorse Adobe offre un valido supporto per questo caso di utilizzo:

* Quando gli utenti accedono [!DNL Photoshop]o [!DNL InDesign]intendono [!DNL Illustrator] modificare un file, eseguono un’operazione di estrazione sulla risorsa specificata
* La risorsa viene scaricata in background, inserita nell’account di Creative Cloud degli utenti sincronizzato su disco dall’app desktop Creative Cloud e il flag di estrazione viene attivato [!DNL Experience Manager] sulla risorsa per ridurre al minimo i conflitti di modifica
* Da qui in poi, l&#39;utente lavora in un file memorizzato localmente nella posizione sincronizzata, e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account di Creative Cloud, è disponibile anche su altri dispositivi che l’utente potrebbe avere (ad esempio, può essere aperta o modificata in un’app mobile di Creative Cloud dedicata) e può essere condivisa con altri utenti di Creative Cloud a scopo di collaborazione.
* Quando l’utente creativo ha completato le modifiche, può eseguire un’operazione di check-in su tale file nell’applicazione di Creative Cloud, con un commento facoltativo. La risorsa corrispondente in [!DNL Experience Manager] viene creata con versione e aggiornata con il nuovo binario. [!DNL Experience Manager] gli utenti come Marketing o LOB possono accedere alle modifiche principali alle risorse, o alle pietre miliari, tramite l’interfaccia utente della cronologia delle [!DNL Experience Manager] risorse.

[!DNL Experience Manager] l&#39;app desktop fornisce una condivisione di rete per le risorse aperte nell&#39;app nativa. Per impostazione predefinita, tutte le modifiche effettuate localmente vengono caricate [!DNL Experience Manager] automaticamente dopo un breve periodo di tempo. Grazie a questa configurazione, i risparmi frequenti durante la fase di lavoro in corso vengono caricati [!DNL Experience Manager] e controllati, creando un sacco di traffico di rete e potenziali problemi di scalabilità - per non parlare delle versioni non necessarie in [!DNL Experience Manager].

L&#39;approccio consigliato consiste nell&#39;utilizzare un&#39;opzione nell&#39;app [!DNL Experience Manager] desktop per disattivare gli aggiornamenti automatici e caricare [!DNL Experience Manager] manualmente le modifiche alle risorse, sfruttando l&#39;azione di caricamento delle modifiche nell&#39;interfaccia utente Stato risorsa dell&#39;app.

#### Caricamento in blocco su DAM {#bulk-upload-to-dam}

In alcuni scenari potrebbe essere necessario caricare simultaneamente un numero maggiore di file in DAM, ad esempio:

* Caricamento dei risultati di fotoscatti o di progetti più grandi
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento delle risorse selezionate da un set più grande se la selezione viene effettuata al di fuori di DAM

La descrizione fa riferimento al caricamento di file operativamente (ad esempio, ogni settimana o con ogni singola foto), come parte normale del flusso di lavoro dell’utente desktop. Le migrazioni di risorse di grandi dimensioni non sono incluse in questa sezione.

Potete sfruttare le seguenti funzionalità di caricamento:

* Per caricare cartelle grandi o gerarchiche in massa, utilizzate l&#39;app [!DNL Experience Manager] desktop che fornisce la funzionalità di caricamento [delle](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem) cartelle. Potete anche caricare strutture di cartelle gerarchiche. [!DNL Assets] vengono caricati in background e, di conseguenza, non sono collegati a una sessione del browser Web
* Per caricare alcuni file da una singola cartella, trascinateli direttamente nell’interfaccia Web o usate l’opzione Crea nell’interfaccia [!DNL Assets] Web.
* A seconda delle esigenze aziendali, potete anche utilizzare il caricatore personalizzato.

#### Gestione delle risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se utilizzate Condivisione file di rete per gestire le risorse digitali, l&#39;utilizzo della condivisione di rete mappata dall&#39;app [!DNL Experience Manager] desktop potrebbe essere considerato un comodo sostituto. Quando si passa da condivisioni di file di rete, [!DNL Experience Manager] l&#39;interfaccia Web fornisce un set completo di funzionalità di Digital Asset Management che vanno ben oltre quanto possibile su una condivisione di rete (ricerca, raccolte, metadati, collaborazione, anteprime e così via), e l&#39;app [!DNL Experience Manager] desktop fornisce un collegamento pratico per collegare l&#39;archivio DAM lato server al lavoro sul desktop.

Evitate di utilizzare l&#39;app [!DNL Experience Manager] desktop per gestire le risorse direttamente nella condivisione di rete di [!DNL Assets]. Ad esempio, evitate di utilizzare l&#39;app [!DNL Experience Manager] desktop per spostare/copiare più file. Utilizzate invece l&#39; [!DNL Assets] interfaccia per trascinare le cartelle dal Finder/Esplora risorse alla condivisione di rete o utilizzate la funzione di caricamento [!DNL Assets] delle cartelle.

#### Asset migration {#asset-migration}

Per pianificare ed eseguire la migrazione delle risorse dal sistema esistente a un nuovo sistema o per migrare un grande volume di risorse memorizzate sui server, consulta la Guida alla [migrazione](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] l&#39;app desktop e [!DNL Experience Manager] le [!DNL Creative Cloud] integrazioni non supportano tali migrazioni. A causa dell’elevato volume di risorse da assimilare e dei requisiti aggiuntivi relativi alla mappatura dei metadati, alla trasformazione e all’assimilazione, le migrazioni devono essere gestite mediante strumenti e approcci diversi.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Best practice per le app desktop  Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Portale marchio Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integrazione  Experience Manager e  Adobe Stock](aem-assets-adobe-stock.md)

