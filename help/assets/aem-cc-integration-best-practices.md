---
title: Integrazione con le best practice di Adobe Creative Cloud
description: Best practice per integrare [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] per semplificare i flussi di lavoro di trasferimento delle risorse e ottenere un’elevata velocità dei contenuti.
contentOwner: AG
role: Business Practices, amministratore
feature: Collaborazione,Adobe Asset Link,App desktop Experience Manager
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '3259'
ht-degree: 16%

---


# [!DNL Adobe Experience Manager] e le best practice  [!DNL Creative Cloud] di integrazione  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] è una soluzione di gestione delle risorse digitali (DAM) che può integrarsi con  [!DNL Adobe Creative Cloud] per aiutare gli utenti DAM a lavorare insieme con i team creativi, semplificando la collaborazione nel processo di creazione dei contenuti.

[!DNL Adobe Creative Cloud] fornisce ai team creativi un ecosistema di soluzioni e servizi per aiutarli a creare risorse digitali. Include applicazioni desktop e mobili, servizi cloud come l’archiviazione con sincronizzazione desktop o esperienza web, nonché marketplace come [!DNL Adobe Stock].

Continua a leggere per scoprire quali integrazioni scegliere tra desktop e DAM di livello enterprise in base al tuo caso d’uso e quali sono le best practice associate per i flussi di lavoro di connessione.

>[!NOTE]
>
>[!DNL Experience Manager] la condivisione delle  [!DNL Creative Cloud] cartelle su è obsoleta e non è più inclusa in questa guida. Adobe consiglia di utilizzare funzionalità più recenti, come [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) o [app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) per fornire all’utente creativo l’accesso alle risorse gestite in [!DNL Experience Manager].

## Necessità di collaborazione di creativi, esperti marketing e utenti DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisiti | Caso d’uso | Superfici interessate |
|---|---|---|
| Semplificare l&#39;esperienza per i creativi sul desktop | Semplifica l’accesso alle risorse da un DAM ([!DNL Experience Manager Assets]) per i creativi o, più in generale, per gli utenti desktop che lavorano in applicazioni di creazione di risorse native. Hanno bisogno di un modo semplice e semplice per scoprire, utilizzare (aprire), modificare e salvare le modifiche a [!DNL Experience Manager], nonché caricare nuovi file. | desktop Win o Mac; [!DNL Creative Cloud] app |
| Fornire risorse pronte all’uso di alta qualità da [!DNL Adobe Stock] | Gli addetti al marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l’origine e l’individuazione delle risorse. I professionisti creativi utilizzano le risorse approvate direttamente dai propri strumenti creativi. | [!DNL Experience Manager Assets];  [!DNL Adobe Stock] mercato; campi metadati |
| Distribuire e condividere le risorse per organizzazioni | I dipartimenti interni/le filiali locali e i partner esterni, i distributori e le agenzie utilizzano le risorse approvate condivise dall&#39;organizzazione madre. L&#39;organizzazione desidera condividere in modo sicuro e senza soluzione di continuità le risorse create per un riutilizzo più ampio. | Brand Portal, Asset Share Commons |

## Offerte di Adobe per supportare le esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per i soggetti coinvolti | offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti creativi individuano le risorse da [!DNL Experience Manager], le aprono e le utilizzano, le modificano e caricano le modifiche in [!DNL Experience Manager], nonché caricano nuovi file in [!DNL Experience Manager], senza uscire dalle app [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator] e  [!DNL Adobe InDesign]. |
| Gli utenti aziendali semplificano l’apertura e l’utilizzo delle risorse, la modifica e il caricamento delle modifiche a [!DNL Experience Manager] e il caricamento di nuovi file in [!DNL Experience Manager] dall’ambiente desktop. Utilizzano un’integrazione generica per aprire qualsiasi tipo di risorsa nell’applicazione desktop nativa, inclusi quelli non Adobi. | [app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] app desktop su desktop Win e Mac |
| Gli addetti al marketing e gli utenti aziendali possono individuare, visualizzare in anteprima, concedere in licenza e salvare le risorse [!DNL Adobe Stock] all’interno di [!DNL Experience Manager] e gestirle. Le risorse concesse in licenza e salvate forniscono metadati selezionati [!DNL Adobe Stock] per una migliore governance. | [Integrazione di Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interfaccia web |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala viene brevemente citata come caso d’uso. Per tali esigenze, valuta prodotti come Adobe Brand Portal o Asset Share Commons. Le soluzioni alternative come [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), che possono essere create in base ai componenti [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Condivisione collegamenti](/help/assets/link-sharing.md), che utilizzano [Risorse di Experience Manager](/help/assets/manage-assets.md) devono essere esaminate in base a requisiti specifici.

![Creative Cloud connessioni, ad Experience Manager, decidere quale funzionalità utilizzare](assets/creative-connections-aem.png)

### Mappatura dei casi d’uso e delle soluzioni di Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso d’uso  | [!DNL Adobe Asset Link] | App desktop [!DNL Experience Manager]  | Osservazioni / Altre soluzioni |
|---|---|---|---|
| Scopri - sfogliare le cartelle DAM | Sì | [!DNL Experience Manager] Azioni per l’interfaccia web e il desktop |  |
| Scopri - accedere alle raccolte DAM | Sì | [!DNL Experience Manager] Azioni per l’interfaccia web e il desktop |  |
| Scopri - cercare risorse da DAM | Sì | [!DNL Experience Manager] Azioni per l’interfaccia web e il desktop |  |
| Utilizzo - Apri risorsa | Sì | Sì | [Apri dall&#39;](manage-assets.md#previewing-assets) interfaccia Web o dal Finder |
| Utilizzare: posizionare una risorsa da DAM in un documento | Sì - incorporazione | Sì: collegamento o incorporamento | [!DNL Experience Manager] l’app desktop consente l’accesso alle risorse come file nel file system locale. Questi collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica : aperto per la modifica | Sì - Azione di ritiro | Sì - Azione aperta (nella condivisione di rete) | [Il check-out in ](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) AAL salva la risorsa nell’account di archiviazione creative cloud dell’utente (sincronizzato dall’app Creative Cloud) per impostazione predefinita. |
| Modifica : lavoro in corso al di fuori di DAM | Sì: risorsa disponibile nell’account di archiviazione Creative Cloud dell’utente sincronizzato con il desktop. | Sì |  |
| Modifica - Carica modifiche | Sì - [Azione di archiviazione](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento facoltativo | Sì |  |
| Carica - file singolo | Sì - carica il documento attivo corrente | Sì | [Caricare tramite interfaccia web](manage-assets.md#uploading-assets) |
| Caricamento: più file / strutture di cartelle gerarchiche | No | Sì | [Carica tramite ](manage-assets.md#uploading-assets) interfaccia web o tramite script o strumenti personalizzati. |
| Varie - utente e accesso | Viene riconosciuto l’accesso dell’utente Creative Cloud all’app desktop Creative Cloud (SSO) | [!DNL Experience Manager] utente e credenziali | Gli utenti di entrambe le soluzioni contano per la quota utente [!DNL Experience Manager]. |
| Varie - rete e accesso | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione [!DNL Experience Manager] in rete | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione [!DNL Experience Manager] in rete | [!DNL Adobe Asset Link] non condivide l&#39;ambiente proxy di rete. |
| Varie - Migrazione di un numero elevato di risorse | No | No | [Guida alla migrazione delle risorse](assets-migration-guide.md) |

Per supportare i casi di utilizzo della distribuzione delle risorse, è necessario considerare altre soluzioni:

* [Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portal è un componente aggiuntivo SaaS configurabile  [!DNL Experience Manager Assets] per la pubblicazione delle risorse.
* Le soluzioni personalizzate vengono create in base al codice [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager] [collegare ](/help/assets/link-sharing.md) shareto condividere risorse ad hoc utilizzando i collegamenti.
* [Interfaccia web di Experience Manager Assets ](/help/assets/manage-assets.md) con aree per soggetti esterni protette dalla configurazione del controllo di  [!DNL Experience Manager] accesso e con le necessarie regolazioni di configurazione IT/rete, che consentono a tali utenti esterni di accedere a  [!DNL Experience Manager].

## Concetti chiave e casi d’uso {#key-concepts-and-use-cases}

### Glossario dei termini comuni {#glossary-of-common-terms}

* **Work-in-progress o creative work-in-progress (WIP):** una fase del ciclo di vita delle risorse in cui una risorsa subisce più modifiche e, in genere, non è ancora pronta per essere condivisa con team più grandi.
* **Creative-ready assets (Risorse pronte per i creativi):** [!DNL Assets]  sono pronti per essere condivisi con un team più ampio oppure sono stati selezionati o approvati dal team creativo per la condivisione con i team di marketing o LOB.
* **Asset approvals (Approvazioni risorse):** il processo di approvazione che viene eseguito per le risorse già caricate in DAM, che, in genere, include approvazioni del marchio, approvazioni legali e così via.
* **Final asset (Risorsa finale):** una risorsa che ha superato tutte le approvazioni/assegnazione tag dei metadati ed è pronta per essere utilizzata dal team più ampio. Tale risorsa viene memorizzata in DAM, per poi essere resa disponibile a tutti gli utenti (o a tutti gli interessati). Può essere utilizzata nei canali di marketing o dai team creativi per la creazione di design.
* **Minor asset update/change (Aggiornamento/modifica risorsa secondaria):** una modifica rapida e piccola a una risorsa digitale. Spesso viene effettuata in risposta a una richiesta di ritocco o di modifica minore, a una revisione delle risorse o all’approvazione (ad esempio: riposizionamento, modifica dimensioni del testo, regolazione di saturazione/luminosità, colore e così via).
* **Major asset update/change (Aggiornamento/modifica risorsa principale):** un passaggio a una risorsa digitale che richiede un lavoro considerevole e che a volte deve essere effettuato in un periodo di tempo più lungo. Generalmente include più modifiche. La risorsa deve essere salvata più volte durante l’aggiornamento. In genere, gli aggiornamenti principali delle risorse fanno sì che la risorsa entri in una fase WIP.
* **DAM:** gestione delle risorse digitali. In questo documento, è sinonimo di [!DNL Experience Manager Assets], salvo specificazione contraria.
* **Creative user (Utente creativo):** un professionista che crea risorse digitali utilizzando le app e i servizi Creative Cloud. In alcuni casi, è possibile che un utente creativo sia membro di un team creativo che utilizza Creative Cloud, ma che non crea risorse digitali, ad esempio un direttore creativo o un manager del team creativo.
* **DAM user (Utente DAM)**: utente tipico di un sistema DAM. A seconda dell’organizzazione, un utente DAM può essere di marketing o non, come un utente Line-of-Business (LOB), un bibliotecario, un venditore e così via.

### Considerazioni sull&#39;utilizzo dell&#39;integrazione [!DNL Experience Manager] e [!DNL Creative Cloud] {#considerations-when-using-aem-and-creative-cloud-integration}

* Consulta [best practice per le app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)
* Vedi [Integrazione Adobe Stock](aem-assets-adobe-stock.md)
* Consulta [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Questo è un breve riepilogo delle best practice per l’integrazione [!DNL Experience Manager] e [!DNL Creative Cloud] . Leggi il resto di questo documento per ottenere la comprensione dettagliata di questi.

* **For creative users, working in Photoshop, InDesign, or Illustrator (Per gli utenti creativi che lavorano in Photoshop, InDesign o Illustrator)**: Adobe Asset Link offre la migliore esperienza utente possibile, inclusa la gestione del Work-in-progress sulle risorse estratte da [!DNL Experience Manager].
* **Per semplificare l’accesso alle risorse dal desktop per qualsiasi formato di file o applicazione generico:** utilizza l’app  [!DNL Experience Manager] desktop.
* **Understand why and when to store assets in DAM (Scopri perché e quando archiviare le risorse in DAM)**: aggiornamenti da rendere disponibili al team più ampio della tua organizzazione.
* **Mind the volume of assets shared (Considera il volume di risorse condivise):** se il caso d’uso è la distribuzione delle risorse, la governance e la sicurezza potrebbero diventare gli aspetti più importanti. Valuta l’utilizzo di strumenti creati per il lavoro in scala, come Brand Portal.
* **Understand asset lifecycle (Informazioni sul ciclo di vita delle risorse):** scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **Handle frequent saves to assets with care (Gestisci con attenzione i salvataggi frequenti nelle risorse):** Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire le attività WIP in cartelle condivise o mappate, a meno che non ti servano tutte le modifiche all’interno di DAM

### Accesso alle risorse [!DNL Adobe Stock] da [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[L’](/help/assets/aem-assets-adobe-stock.md) integrazione di Experience Manager e Adobe Stock offre  [!DNL Experience Manager] agli utenti la possibilità di cercare, visualizzare in anteprima, concedere in licenza e salvare le risorse da  [!DNL Adobe Stock] a  [!DNL Experience Manager]. Le risorse [!DNL Stock] concesse in licenza e salvate hanno selezionato i metadati [!DNL Stock], che possono essere utilizzati per cercarli con filtri aggiuntivi.

Alcuni punti importanti su questa integrazione:

* Quando le risorse da stock di Adobe vengono salvate in [!DNL Experience Manager], diventano una [!DNL Assets] normale, con file binari salvati nell&#39;archivio [!DNL Experience Manager]. Alcuni metadati relativi a [!DNL Adobe Stock] vengono salvati per la risorsa in [!DNL Experience Manager], altrimenti il processo di acquisizione sarà lo stesso di qualsiasi altro file. Ad esempio, se Tag avanzati sono attivi, al momento del salvataggio questi tag vengono aggiunti a tali risorse.
* La risorsa salvata in [!DNL Experience Manager] è una copia, non un collegamento in [!DNL Adobe Stock].

**Utilizzo delle risorse salvate da  [!DNL Adobe Stock] in  [!DNL Experience Manager] in[!DNL Creative Cloud]**. Questa integrazione è indipendente da [!DNL Adobe Asset Link], ma [!DNL Adobe Asset Link] riconosce tali risorse salvate da [!DNL Stock] e visualizza metadati aggiuntivi e un logo [!DNL Adobe Stock] su queste risorse nell&#39;interfaccia utente dell&#39;estensione [!DNL Adobe Asset Link] in [!DNL Photoshop], [!DNL Illustrator] o [!DNL InDesign]. I file sono disponibili per la navigazione, l’apertura e così via, perché sono risorse normali quando vengono salvati in [!DNL Experience Manager].
I creativi che lavorano in [!DNL Creative Cloud] app con estensione [!DNL Adobe Asset Link] presenti, oltre ad avere accesso a risorse già concesse in licenza da [!DNL Adobe Stock] in [!DNL Experience Manager], possono utilizzare il pannello [!DNL Creative Cloud] Librerie per cercare, visualizzare in anteprima e concedere in licenza le risorse [!DNL Adobe Stock].
[!DNL Assets] da  [!DNL Adobe Stock] concesso in licenza e salvato in  [!DNL Experience Manager] diventano disponibili per i team più grandi che accedono alla  [!DNL Experience Manager Assets] distribuzione, mentre i creativi che rilasciano risorse  [!DNL Adobe Stock] tramite il pannello  [!DNL Creative Cloud] Librerie le rendono disponibili solo per impostazione predefinita nel loro  [!DNL Creative Cloud] account.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Informazioni sull’archiviazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante comprendere quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse vengono memorizzate in DAM {#why-assets-are-stored-in-dam}

L’archiviazione delle risorse in DAM le rende facilmente accessibili e accessibili. Garantisce che le risorse possano essere sfruttate da numerosi utenti nell’organizzazione o nell’ecosistema, inclusi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di archiviare solo le risorse rilevanti per i processi di marketing/LOB a valle (pubblicazione su canali come il canale web tramite [!DNL Experience Manager Sites] o altri canali serviti da Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e misurati da Analytics Cloud, fornendo a utenti/partner e così via). Inoltre, le organizzazioni memorizzano risorse che possono essere soggette a un processo di revisione/approvazione in DAM. In questo modo, DAM memorizza principalmente risorse che hanno alte probabilità di essere sfruttate ed evita di archiviare le risorse inattive.

La memorizzazione delle risorse è inoltre soggetta a considerazioni tecniche e relative all’utilizzo delle risorse. DAM fornisce servizi aggiuntivi sulle risorse memorizzate, tra cui l’estrazione dei metadati, il controllo delle versioni, la generazione di anteprime/transcodifica, la gestione dei riferimenti e l’aggiunta di informazioni sul controllo degli accessi. Questi servizi richiedono tempo e risorse aggiuntive per l&#39;infrastruttura.

Spesso, l’archiviazione di tutte le risorse e gli aggiornamenti non è auspicabile. Ad esempio, se gli aggiornamenti a risorse specifiche sono di scarsa qualità e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team creativi (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del ciclo di vita delle risorse. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Risorse che devono ancora essere completate o soggette a sperimentazione.
* Risorse che non superano il ciclo di revisione creativo/interno del team.
* Rispetto alla risorsa in questione, il team ha candidati migliori per rappresentare il proprio lavoro a team esterni.

Di solito, le risorse delle classi seguenti vengono memorizzate in DAM:

* Attività che hanno raggiunto una certa scadenza e sono considerate pronte per essere condivise.
* Risorse preselezionate dal team creativo.
* Formati di risorse specifici utilizzabili o richiesti dal marketing, a seconda di un contratto o di un contratto specifico (ad esempio, file JPG convertiti da file RAW, TIFF/immagini da originali PSD).

#### Quando gli aggiornamenti alle risorse vengono memorizzati in DAM {#when-updates-to-assets-are-stored-in-dam}

Di regola, solo gli aggiornamenti alle risorse rilevanti per il set più ampio di utenti DAM devono essere archiviati in DAM. Assicura che gli utenti (marketing e funzioni simili) vedano solo le versioni rilevanti nella timeline delle risorse DAM.

In genere, le modifiche sono correlate alle fasi principali del ciclo di vita delle risorse. Ad esempio, la risorsa iniziale pronta per il marketing o un aggiornamento ufficiale basato su richiesta/revisione fornita dal team creativo devono essere memorizzati e controllati in versione in DAM.

L’aggiornamento del team creativo per la revisione da parte del team marketing dopo una richiesta di modifica della risorsa esistente in DAM è un esempio di aggiornamento rilevante. Deve essere memorizzato e modificato in DAM per ulteriori riferimenti o per ripristinare la versione precedente.

Di seguito sono riportati alcuni esempi di aggiornamenti che in genere non sono rilevanti:

* Versioni precedenti delle risorse caricate prima che sia pronto per la revisione del marketing
* Frequenti modifiche creative alla risorsa nella fase in corso di lavorazione prima che i team creativi e di marketing decidano che la risorsa è pronta

### Accesso utente a DAM {#user-access-to-dam}

[!DNL Assets] supporta due tipi di utenti in base al loro accesso alla  [!DNL Assets] distribuzione. In genere, gli utenti all’interno della rete aziendale (firewall) hanno accesso diretto a DAM. Altri utenti esterni alla rete aziendale non avrebbero accesso diretto. Il tipo di utente determina quali integrazioni possono essere utilizzate dal punto di vista tecnico.

#### Utenti creativi con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/i professionisti creativi caricati nella rete interna hanno accesso alla distribuzione DAM, incluso l’accesso [!DNL Experience Manager]. [!DNL Experience Manager] e l&#39;infrastruttura di rete può essere impostata per consentire l&#39;accesso diretto a soggetti esterni - di solito organizzazioni fidate come agenzie che lavorano per un cliente - per avere accesso a  [!DNL Experience Manager] attraverso la rete, ad esempio tramite VPN o elenco Consentiti IP.

In questi casi, Adobe Asset Link o l’ app desktop [!DNL Experience Manager] consente di accedere facilmente alle risorse finali/approvate e di salvare le risorse pronte per la creazione in DAM.

#### Utenti creativi senza accesso a DAM {#creative-users-without-access-to-dam}

Le agenzie esterne e i freelance senza accesso diretto all’implementazione DAM possono richiedere l’accesso alle risorse approvate o desiderano aggiungere le loro nuove progettazioni al DAM.

Utilizza le seguenti strategie per fornire accesso alle risorse finali/approvate:

* Utilizza l’app desktop se Asset Link non funziona.
* Utilizza [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per distribuire le risorse in modo sicuro ai partner esterni
* Utilizza un&#39;implementazione personalizzata di un portale di distribuzione e determinazione origine basata su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizza il Controllo accessi configurato in [!DNL Experience Manager] e l&#39;infrastruttura di rete necessaria (ad esempio, VPN e elenco Consentiti IP) per consentire a parti esterne di accedere a un&#39;area dedicata di contenuto nel tuo DAM. Possono utilizzare l’ [!DNL Experience Manager] interfaccia utente web per ottenere risorse e caricare nuovi contenuti nel DAM.

#### Lavoro in corso sulle risorse da [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Come discusso in questo documento, si consiglia di eseguire aggiornamenti importanti sulle risorse, talvolta denominati work in progress, senza che tutte le modifiche salvate nel file locale siano caricate anche in [!DNL Experience Manager] come modifiche. Questo consente di velocizzare il lavoro dell’utente desktop, limitare l’ampiezza di banda utilizzata e mantenere pulita la timeline delle risorse e concentrarsi su aggiornamenti principali controllati.

Adobe Asset Link offre un buon supporto per questo caso d’uso:

* Quando gli utenti in [!DNL Photoshop], [!DNL InDesign] o [!DNL Illustrator] intendono modificare un file, eseguono un’operazione di estrazione sulla risorsa specificata
* La risorsa viene scaricata in background, inserita nell’account di Creative Cloud degli utenti sincronizzato su disco dall’app desktop Creative Cloud e il flag di estrazione è attivato in [!DNL Experience Manager] sulla risorsa per ridurre al minimo i conflitti di modifica
* Da lì in poi, l&#39;utente lavora in un file memorizzato localmente nella posizione sincronizzata, e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account Creative Cloud, è disponibile anche su altri dispositivi di cui l’utente potrebbe disporre (ad esempio, possono essere aperti o modificati in un’app mobile Creative Cloud dedicata) e può essere condivisa con altri utenti di Creative Cloud a scopo di collaborazione.
* Al termine delle modifiche, l’utente creativo può eseguire un’operazione di Check-in sul file nella propria applicazione Creative Cloud, con un commento facoltativo. Le versioni della risorsa corrispondente in [!DNL Experience Manager] vengono impostate e aggiornate in con il nuovo binario. [!DNL Experience Manager] gli utenti come gli addetti al marketing o gli utenti LOB possono accedere a modifiche importanti delle risorse o a fasi cardine tramite l’interfaccia utente della timeline delle  [!DNL Experience Manager] risorse.

[!DNL Experience Manager] l’app desktop fornisce una condivisione di rete per le risorse aperte nell’app nativa. Per impostazione predefinita, tutte le modifiche eseguite localmente vengono caricate in [!DNL Experience Manager] automaticamente dopo un breve periodo di tempo. Con tale configurazione, durante la fase di lavorazione in corso verranno caricati tutti in [!DNL Experience Manager] e versioni, creando un sacco di traffico di rete e potenziali problemi di scalabilità - per non parlare delle versioni non necessarie in [!DNL Experience Manager].

L’approccio consigliato consiste nell’utilizzare un’opzione nell’ [!DNL Experience Manager] app desktop per disattivare gli aggiornamenti automatizzati e caricare manualmente le modifiche alle risorse in [!DNL Experience Manager] , sfruttando l’azione di caricamento delle modifiche nell’interfaccia utente dell’app Stato risorsa.

#### Caricamento in serie in DAM {#bulk-upload-to-dam}

Potrebbe essere necessario caricare contemporaneamente un numero maggiore di file in DAM in alcuni scenari, ad esempio:

* Caricamento dei risultati di fotografie o progetti più grandi
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento di risorse selezionate da un set più grande se la selezione viene eseguita all’esterno di DAM

La descrizione fa riferimento al caricamento dei file operazionale (ad esempio, ogni settimana o con ogni servizio fotografico), come parte normale del flusso di lavoro dell’utente desktop. Le migrazioni di risorse di grandi dimensioni non sono coperte qui.

Puoi sfruttare le seguenti funzionalità di caricamento:

* Per caricare in massa cartelle grandi/gerarchiche, utilizza l’ app desktop [!DNL Experience Manager] che fornisce la funzionalità [caricamento cartelle](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem). Puoi anche caricare strutture di cartelle gerarchiche. [!DNL Assets] sono caricati in background e, pertanto, non è legato a una sessione del browser web
* Per caricare alcuni file da una singola cartella, trascina i file direttamente nell’interfaccia Web o utilizza l’opzione Crea nell’ interfaccia Web [!DNL Assets] .
* A seconda delle esigenze aziendali, puoi anche utilizzare caricatori personalizzati.

#### Gestire le risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se utilizzi Condivisione file di rete per gestire le risorse digitali, puoi considerare come un comodo sostituto solo l’utilizzo della condivisione di rete mappata dall’ [!DNL Experience Manager] app desktop. Durante la transizione da condivisioni di file di rete, l’ [!DNL Experience Manager] interfaccia web offre un set completo di funzionalità di Digital Asset Management che vanno ben oltre quanto possibile su una condivisione di rete (ricerca, raccolte, metadati, collaborazione, anteprime e così via) e l’ [!DNL Experience Manager] app desktop fornisce un comodo collegamento per collegare l’archivio DAM lato server con il lavoro sul desktop.

Evita di usare l’ [!DNL Experience Manager] app desktop per gestire le risorse direttamente nella condivisione di rete di [!DNL Assets]. Ad esempio, evita di utilizzare l’ [!DNL Experience Manager] app desktop per spostare/copiare più file. Utilizza invece l&#39;interfaccia [!DNL Assets] per trascinare le cartelle da Finder/Explorer alla condivisione di rete o utilizza la funzione [!DNL Assets] Caricamento cartelle .

#### Migrazione delle risorse {#asset-migration}

Per pianificare ed eseguire le migrazioni delle risorse dal sistema esistente a un nuovo sistema o per la migrazione di un grande volume di risorse memorizzate sui server, consulta la [Guida alla migrazione](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] l’app desktop e  [!DNL Experience Manager] alle  [!DNL Creative Cloud] integrazioni non supportano tali migrazioni. A causa dei grandi volumi di risorse da acquisire e dei requisiti aggiuntivi relativi alla mappatura, alla trasformazione e all’acquisizione dei metadati, le migrazioni devono essere gestite utilizzando strumenti e approcci diversi.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Manager - Best practice per le app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integrazione di Experience Manager e Adobe Stock](aem-assets-adobe-stock.md)

