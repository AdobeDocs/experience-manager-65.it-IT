---
title: Integrazione con le best practice di Adobe Creative Cloud
description: Best practice per l'integrazione di  [!DNL Adobe Experience Manager] con [!DNL Adobe Creative Cloud] per semplificare i flussi di lavoro di trasferimento delle risorse e velocizzare la realizzazione dei contenuti.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: a144f7cc75b1a5cdb45d2aaf90e87013ac68a431
workflow-type: tm+mt
source-wordcount: '3173'
ht-degree: 11%

---

# Best practice per l&#39;integrazione di [!DNL Adobe Experience Manager] e [!DNL Creative Cloud] {#aem-and-creative-cloud-integration-best-practices}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] è una soluzione DAM (Digital Asset Management) che può essere integrata con [!DNL Adobe Creative Cloud] per aiutare gli utenti DAM a collaborare con i team creativi, semplificando la collaborazione nel processo di creazione dei contenuti.

[!DNL Adobe Creative Cloud] offre ai team creativi un ecosistema di soluzioni e servizi per aiutarli a creare risorse digitali. Include applicazioni desktop e mobili, servizi cloud come l&#39;archiviazione con sincronizzazione desktop o esperienza Web e marketplace come [!DNL Adobe Stock].

Continua a leggere per scoprire quali integrazioni scegliere tra desktop e DAM di livello Enterprise in base al tuo caso d’uso e quali sono le best practice associate per i flussi di lavoro di connessione.

>[!NOTE]
>
>La condivisione di cartelle da [!DNL Experience Manager] a [!DNL Creative Cloud] è obsoleta e non è più trattata in questa guida. L&#39;Adobe consiglia di utilizzare funzionalità più recenti, ad esempio [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) o [Experience Manager Desktop App](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=it), per consentire ai creativi di accedere alle risorse gestite in [!DNL Experience Manager].

## Esigenze di Collaboration per creativi, addetti al marketing e utenti DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisiti | Caso d’uso | Superfici interessate |
|---|---|---|
| Esperienza semplificata per i creativi sul desktop | Accesso semplificato alle risorse da un DAM ([!DNL Experience Manager Assets]) per i creativi o più in generale per gli utenti desktop che lavorano in applicazioni di creazione di risorse native. Hanno bisogno di un modo semplice per individuare, utilizzare (aprire), modificare e salvare le modifiche in [!DNL Experience Manager] e caricare nuovi file. | Windows o Mac desktop; [!DNL Creative Cloud] app |
| Fornisci risorse pronte all&#39;uso di alta qualità da [!DNL Adobe Stock] | Gli addetti al marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l’origine e il rilevamento delle risorse. I creativi utilizzano le risorse approvate direttamente nei loro strumenti creativi. | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] marketplace; campi metadati |
| Distribuire e condividere le risorse per organizzazioni | Reparti interni/filiali locali e partner esterni, distributori e agenzie utilizzano le risorse approvate condivise dall’organizzazione principale. L’organizzazione desidera condividere in modo sicuro e fluido le risorse create per un riutilizzo più ampio. | Brand Portal, Asset Share Commons |

## Adobi di offerte per supportare le esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per gli utenti tipo interessati | offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti creativi individuano le risorse da [!DNL Experience Manager], le aprono e le utilizzano, modificano e caricano le modifiche in [!DNL Experience Manager] e caricano nuovi file in [!DNL Experience Manager], senza uscire da [!DNL Creative Cloud] app. | [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) | .[!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign]. |
| Gli utenti aziendali semplificano l&#39;apertura e l&#39;utilizzo delle risorse, la modifica e il caricamento delle modifiche in [!DNL Experience Manager] e il caricamento di nuovi file in [!DNL Experience Manager] dall&#39;ambiente desktop. Utilizzano un’integrazione generica per aprire qualsiasi tipo di risorsa nell’applicazione desktop nativa, incluse quelle non di Adobe. | [app desktop di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it) | App desktop [!DNL Experience Manager] su desktop Win e Mac |
| Gli addetti al marketing e gli utenti aziendali possono individuare, visualizzare in anteprima, concedere in licenza e salvare le risorse [!DNL Adobe Stock] e gestirle da [!DNL Experience Manager]. Le risorse concesse in licenza e salvate forniscono alcuni metadati [!DNL Adobe Stock] per una migliore governance. | [Integrazione di Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | Interfaccia Web [!DNL Experience Manager] |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala viene brevemente citata come caso d’uso. Per tali esigenze, valuta prodotti come Adobe Brand Portal o Asset Share Commons. Le soluzioni alternative, come [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=it), che possono essere create in base ai componenti [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](/help/assets/link-sharing.md), utilizzando [Experience Manager Assets](/help/assets/manage-assets.md), devono essere esaminate in base a requisiti specifici.

![Creative Cloud connessioni per Experience Manager, decidere quale funzionalità utilizzare](assets/creative-connections-aem.png)

### Mappatura dei casi d’uso e soluzioni di Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso d’uso | [!DNL Adobe Asset Link] | App desktop [!DNL Experience Manager] | Osservazioni / Altre soluzioni |
|---|---|---|---|
| Individuare: sfogliare le cartelle DAM | Sì | [!DNL Experience Manager] Interfaccia Web e azioni desktop | |
| Individuare: accedere alle raccolte DAM | Sì | [!DNL Experience Manager] Interfaccia Web e azioni desktop | |
| Individuazione: ricerca di risorse da DAM | Sì | [!DNL Experience Manager] Interfaccia Web e azioni desktop | |
| Usa: apri risorsa | Sì | Sì | [Apri dall&#39;interfaccia Web](manage-assets.md#previewing-assets) o dal Finder |
| Utilizza: inserisci risorsa da DAM in un documento | Sì - incorporamento | Sì - Collegamento o incorporamento | L&#39;app desktop [!DNL Experience Manager] consente di accedere alle risorse come file nel file system locale. Questi collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica: apri per la modifica | Sì - Estrai | Sì - Azione aperta nella condivisione di rete | [Il Check-Out in AAL](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) salva la risorsa nell&#39;account di archiviazione di Creative Cloud dell&#39;utente (sincronizzato dall&#39;app Creative Cloud) per impostazione predefinita. |
| Modifica: lavoro in corso al di fuori di DAM | Sì - Risorsa disponibile nell’account di archiviazione Creative Cloud dell’utente sincronizzato con il desktop. | Sì | |
| Modifica - Carica modifiche | Sì - [Azione di archiviazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento facoltativo | Sì | |
| Caricamento - file singolo | Sì - carica il documento attivo corrente | Sì | [Carica tramite interfaccia Web](manage-assets.md#uploading-assets) |
| Caricamento: più file/strutture di cartelle gerarchiche | No | Sì | [Carica tramite l&#39;interfaccia Web](manage-assets.md#uploading-assets) o tramite script o strumento personalizzato. |
| Varie - utente e accesso | Riconoscimento SSO (Creative Cloud User logged in Creative Cloud Desktop app) | [!DNL Experience Manager] utente e credenziali | Gli utenti di entrambe le soluzioni vengono conteggiati nella quota utente [!DNL Experience Manager]. |
| Varie - Rete e accesso | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione [!DNL Experience Manager] in rete | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione [!DNL Experience Manager] in rete | [!DNL Adobe Asset Link] non condivide l&#39;ambiente proxy di rete. |
| Varie - Migrazione di un numero elevato di risorse | No | No | [Guida alla migrazione di Assets](assets-migration-guide.md) |

Per supportare i casi di utilizzo della distribuzione delle risorse, è necessario prendere in considerazione altre soluzioni:

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=it) per un componente aggiuntivo SaaS configurabile in [!DNL Experience Manager Assets] per la pubblicazione delle risorse.
* Le soluzioni personalizzate vengono create in base alla base di codice di [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager] [condivisione collegamenti](/help/assets/link-sharing.md) per condividere risorse su richiesta tramite collegamenti.
* [Interfaccia Web di Experience Manager Assets](/help/assets/manage-assets.md) con aree per le parti esterne protette dalla configurazione del controllo di accesso di [!DNL Experience Manager] e con le necessarie regolazioni della configurazione IT/di rete, consentendo a tali utenti esterni di accedere a [!DNL Experience Manager].

## Concetti chiave e casi d’uso {#key-concepts-and-use-cases}

### Glossario dei termini più comuni {#glossary-of-common-terms}

* **Work-in-progress o creative work-in-progress (WIP):** una fase del ciclo di vita delle risorse in cui una risorsa subisce più modifiche e, in genere, non è ancora pronta per essere condivisa con team più grandi.
* **Risorse pronte per i creativi:** [!DNL Assets] pronte per essere condivise con un team più ampio oppure che sono state selezionate o approvate dal team creativo per la condivisione con i team di marketing o LOB.
* **Asset approvals (Approvazioni risorse):** il processo di approvazione che viene eseguito per le risorse già caricate in DAM, che, in genere, include approvazioni del marchio, approvazioni legali e così via.
* **Risorsa finale:** una risorsa che ha superato tutte le approvazioni/assegnazione tag dei metadati ed è pronta per essere utilizzata dal team più ampio. Tale risorsa viene memorizzata in DAM, per poi essere resa disponibile a tutti gli utenti (o a tutti gli interessati). Può essere utilizzata nei canali di marketing o dai team creativi per la creazione di design.
* **Aggiornamento/modifica risorsa secondaria:** Una modifica rapida e piccola a una risorsa digitale. Spesso viene effettuata in risposta a una richiesta di ritocco o di modifica minore, a una revisione delle risorse o all’approvazione (ad esempio: riposizionamento, modifica dimensioni del testo, regolazione di saturazione/luminosità, colore e così via).
* **Aggiornamento/modifica risorsa principale:** una modifica a una risorsa digitale che richiede un lavoro considerevole e che a volte deve essere eseguita in un periodo di tempo più lungo. Generalmente include più modifiche. La risorsa deve essere salvata più volte durante l’aggiornamento. In genere, gli aggiornamenti principali delle risorse fanno sì che la risorsa entri in una fase WIP.
* **DAM:** gestione delle risorse digitali. In questo documento, è sinonimo di [!DNL Experience Manager Assets], a meno che non venga espressamente indicato altrimenti.
* **Creative user (Utente creativo):** un professionista che crea risorse digitali utilizzando le app e i servizi Creative Cloud. In alcuni casi, è possibile che un utente creativo sia membro di un team creativo che utilizza Creative Cloud, ma che non crea risorse digitali, ad esempio un direttore creativo o un manager del team creativo.
* **DAM user (Utente DAM)**: utente tipico di un sistema DAM. A seconda dell’organizzazione, un utente DAM può essere di marketing o non, ad esempio un utente Line-of-Business (LOB), un bibliotecario, un venditore e così via.

### Considerazioni durante l&#39;utilizzo dell&#39;integrazione di [!DNL Experience Manager] e [!DNL Creative Cloud] {#considerations-when-using-aem-and-creative-cloud-integration}

* Vedi [best practice per le app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=it#best-practices-to-prevent-troubles)
* Vedi [Integrazione Adobe Stock](aem-assets-adobe-stock.md)
* Vedi [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)

Questo è un breve riepilogo delle best practice per l&#39;integrazione di [!DNL Experience Manager] e [!DNL Creative Cloud]. Leggi il resto del documento per informazioni dettagliate su questi.

* **Per gli utenti creativi che lavorano in Photoshop, InDesign o Illustrator:** Adobe Asset Link offre la migliore esperienza utente, inclusa la gestione del Work-in-progress sulle risorse estratte da [!DNL Experience Manager].
* **Per semplificare l&#39;accesso alle risorse dal desktop per qualsiasi formato di file o applicazione generica:** utilizzare l&#39;app desktop [!DNL Experience Manager].
* **Scopri perché e quando archiviare le risorse in DAM:** Aggiornamenti da rendere disponibili al team più ampio della tua organizzazione.
* **Mind the volume of assets shared (Considera il volume di risorse condivise):** se il caso d’uso è la distribuzione delle risorse, la governance e la sicurezza potrebbero diventare gli aspetti più importanti. Valuta l’utilizzo di strumenti creati per il lavoro in scala, come Brand Portal.
* **Understand asset lifecycle (Informazioni sul ciclo di vita delle risorse):** scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **Handle frequent saves to assets with care (Gestisci con attenzione i salvataggi frequenti nelle risorse):** Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire le attività WIP in una cartella condivisa/mappata a meno che non siano necessarie tutte le modifiche in DAM

### Accesso a [!DNL Adobe Stock] risorse da [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

L&#39;integrazione di [Experience Manager e Adobe Stock](/help/assets/aem-assets-adobe-stock.md) consente a [!DNL Experience Manager] utenti di eseguire ricerche, visualizzare in anteprima, concedere in licenza e salvare risorse da [!DNL Adobe Stock] in [!DNL Experience Manager]. [!DNL Stock] risorse concesse in licenza e salvate hanno selezionato [!DNL Stock] metadati che possono essere utilizzati per cercarli con filtri aggiuntivi.

Alcuni punti importanti su questa integrazione:

* Quando le risorse da Adobe Stock vengono salvate in [!DNL Experience Manager], diventano un [!DNL Assets] regolare, con file binari salvati nell&#39;archivio [!DNL Experience Manager]. Alcuni metadati relativi a [!DNL Adobe Stock] sono stati salvati per la risorsa in [!DNL Experience Manager]. In caso contrario, il processo di acquisizione avrà lo stesso aspetto di qualsiasi altro file. Ad esempio, se sono attivi i tag avanzati, questi vengono aggiunti a queste risorse al momento del salvataggio.
* La risorsa salvata in [!DNL Experience Manager] è una copia, non un collegamento in [!DNL Adobe Stock].

**Utilizzo delle risorse salvate da [!DNL Adobe Stock] in [!DNL Experience Manager] in[!DNL Creative Cloud]**. Questa integrazione è indipendente da [!DNL Adobe Asset Link], ma [!DNL Adobe Asset Link] riconosce queste risorse salvate da [!DNL Stock] in questo modo e visualizza metadati aggiuntivi e un logo [!DNL Adobe Stock] su queste risorse nell&#39;interfaccia utente dell&#39;estensione [!DNL Adobe Asset Link] in [!DNL Photoshop], [!DNL Illustrator] o [!DNL InDesign]. I file sono disponibili per l&#39;esplorazione, l&#39;apertura e così via, in quanto si tratta di risorse normali quando vengono salvate in [!DNL Experience Manager].
Gli utenti creativi che lavorano in app [!DNL Creative Cloud] con estensione [!DNL Adobe Asset Link] presenti, oltre ad avere accesso a risorse con licenza da [!DNL Adobe Stock] in [!DNL Experience Manager], possono utilizzare anche il pannello Librerie [!DNL Creative Cloud] per cercare, visualizzare in anteprima e concedere in licenza [!DNL Adobe Stock] risorse.
[!DNL Assets] da [!DNL Adobe Stock] concesso in licenza e salvato in [!DNL Experience Manager] diventa disponibile ai team più grandi che accedono alla distribuzione di [!DNL Experience Manager Assets], mentre le risorse create con licenza da [!DNL Adobe Stock] tramite il pannello Librerie [!DNL Creative Cloud] le rendono disponibili solo per impostazione predefinita nel loro account [!DNL Creative Cloud].

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Informazioni sulla memorizzazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra i team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante capire quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse vengono memorizzate in DAM {#why-assets-are-stored-in-dam}

L’archiviazione delle risorse in DAM ne semplifica l’accesso e la ricerca. In questo modo le risorse possono essere utilizzate da numerosi utenti nell’organizzazione o nell’ecosistema, inclusi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di memorizzare solo le risorse rilevanti per i processi di marketing/LOB a valle (pubblicazione su canali come il canale web tramite [!DNL Experience Manager Sites] o altri canali gestiti da Adobe Experience Cloud, come Marketing Cloud, Advertising Cloud e misurati da Analytics Cloud, fornendo informazioni a utenti/partner e così via). Inoltre, le organizzazioni memorizzano in DAM le risorse che possono essere soggette a un processo di revisione/approvazione. In questo modo, DAM archivia principalmente le risorse che hanno elevate probabilità di essere utilizzate ed evita di archiviare le risorse inattive.

L’archiviazione delle risorse è inoltre soggetta a considerazioni tecniche e sull’utilizzo delle risorse. DAM offre servizi aggiuntivi sulle risorse memorizzate, tra cui estrazione di metadati, controllo delle versioni, generazione di anteprime/transcodifica, gestione dei riferimenti e aggiunta di informazioni di controllo degli accessi. Questi servizi richiedono più tempo e risorse infrastrutturali.

Spesso non è consigliabile archiviare tutte le risorse e gli aggiornamenti. Ad esempio, se gli aggiornamenti a risorse specifiche sono di qualità scadente e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team creativi (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del loro ciclo di vita. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Assets non ancora finalizzati o soggetti a sperimentazione.
* Assets che non superano il ciclo di revisione del team creativo/interno.
* Rispetto alla risorsa in questione, il team ha candidati migliori per rappresentare il proprio lavoro in team esterni.

In genere, le risorse delle classi seguenti sono memorizzate in DAM:

* Assets che hanno raggiunto una certa maturità e sono considerati pronti per essere condivisi.
* Assets preselezionati dal team creativo.
* Formati di risorse specifici utilizzabili o richiesti dal marketing, a seconda di un contratto o accordo specifico (ad esempio, file JPG TIFF convertiti da file RAW,/immagini da originali PSD).

#### Quando gli aggiornamenti alle risorse vengono memorizzati in DAM {#when-updates-to-assets-are-stored-in-dam}

Di regola, in DAM devono essere memorizzati solo gli aggiornamenti delle risorse rilevanti per il set più ampio di utenti DAM. In questo modo gli utenti (funzioni di marketing e simili) potranno visualizzare solo le versioni rilevanti nella timeline delle risorse DAM.

In genere, le modifiche sono correlate alle principali attività cardine del ciclo di vita delle risorse. Ad esempio, la risorsa pronta per il marketing iniziale o un aggiornamento ufficiale basato su richiesta/revisione fornito dal team creativo deve essere archiviato e la versione deve essere in DAM.

L’aggiornamento del team creativo, che dovrà essere rivisto dal team marketing dopo una richiesta di modifica della risorsa esistente in DAM, è un esempio di aggiornamento rilevante. Deve essere archiviato e sottoposto a controllo delle versioni in DAM per ulteriore riferimento o per il ripristino della versione precedente.

Di seguito sono riportati alcuni esempi di aggiornamenti che in genere non sono rilevanti:

* Versioni precedenti delle risorse caricate prima che sia pronto per la revisione marketing
* Frequenti modifiche creative alla risorsa nella fase work-in-progress prima che i team creativi e di marketing decidano che la risorsa è pronta

### Accesso utente a DAM {#user-access-to-dam}

[!DNL Assets] supporta due tipi di utenti in base al loro accesso alla distribuzione di [!DNL Assets]. In genere, gli utenti all’interno della rete aziendale (firewall) hanno accesso diretto a DAM. Gli altri utenti esterni alla rete aziendale non avrebbero accesso diretto. Il tipo di utente determina quali integrazioni possono essere utilizzate dal punto di vista tecnico.

#### Utenti creativi con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/i professionisti creativi integrati nella rete interna hanno accesso all’implementazione DAM, incluso l’accesso [!DNL Experience Manager]. È possibile configurare [!DNL Experience Manager] e l&#39;infrastruttura di rete per consentire l&#39;accesso diretto a parti esterne, in genere organizzazioni attendibili come le agenzie che lavorano per un client, per accedere a [!DNL Experience Manager] in rete, ad esempio tramite elenchi Consentiti VPN o IP.

In questi casi, Adobe Asset Link o l&#39;app desktop [!DNL Experience Manager] facilita l&#39;accesso alle risorse finali/approvate e consente di salvare le risorse pronte per la creazione in DAM.

#### Utenti creativi senza accesso a DAM {#creative-users-without-access-to-dam}

Le agenzie esterne e i freelance che non dispongono di un accesso diretto all’implementazione DAM potrebbero richiedere l’accesso alle risorse approvate o voler aggiungere le nuove progettazioni al DAM.

Utilizza le seguenti strategie per fornire accesso alle risorse finali/approvate:

* Se Asset Link non funziona, utilizza l’app desktop.
* Utilizza [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=it) per distribuire le risorse in modo sicuro ai partner esterni
* Utilizza un&#39;implementazione personalizzata di un portale di distribuzione e sourcing basato su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizzare il controllo degli accessi configurato in [!DNL Experience Manager] e l&#39;infrastruttura di rete necessaria (ad esempio, VPN e elenco Consentiti IP) per consentire alle parti esterne di accedere a un&#39;area dedicata di contenuto nel DAM. Possono utilizzare l&#39;interfaccia utente Web di [!DNL Experience Manager] per ottenere risorse e caricare nuovi contenuti in DAM.

#### Lavori in corso sulle risorse da [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Come descritto in questo documento, si consiglia di eseguire importanti aggiornamenti sulle risorse, talvolta denominati work in progress, senza dover caricare tutte le modifiche nel file locale anche in [!DNL Experience Manager] come modifiche. Ciò consente di velocizzare il lavoro di un utente desktop, limitare la larghezza di banda della rete utilizzata, mantenere pulita la timeline delle risorse e concentrarsi su aggiornamenti controllati e importanti.

Adobe Asset Link offre un buon supporto per questo caso d’uso:

* Quando gli utenti in [!DNL Photoshop], [!DNL InDesign] o [!DNL Illustrator] intendono modificare un file, eseguono un&#39;operazione di Check-Out sulla risorsa specificata
* La risorsa viene scaricata in background, inserita nell&#39;account di Creative Cloud degli utenti sincronizzato su disco dall&#39;app desktop Creative Cloud e il contrassegno di estrazione viene attivato in [!DNL Experience Manager] sulla risorsa per ridurre al minimo i conflitti di modifica
* Da lì in poi, l’utente lavora in un file memorizzato localmente nella posizione sincronizzata e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account di Creative Cloud, è disponibile anche su altri dispositivi di cui l’utente potrebbe disporre (ad esempio, può essere aperta o modificata in un’app mobile Creative Cloud dedicata) e può essere condivisa con altri utenti Creative Cloud a scopo di collaborazione.
* Una volta apportate le modifiche, l&#39;utente creativo può eseguire un&#39;operazione di check-in su tale file nell&#39;applicazione Creative Cloud, con un commento facoltativo. La risorsa corrispondente in [!DNL Experience Manager] è stata sottoposta a controllo delle versioni e aggiornata a con il nuovo binario. [!DNL Experience Manager] utenti come gli addetti al marketing o gli utenti LOB hanno accesso alle principali modifiche alle risorse o alle milestone tramite l&#39;interfaccia utente della timeline di [!DNL Experience Manager] risorse.

L&#39;app desktop [!DNL Experience Manager] fornisce una condivisione di rete per le risorse aperte nell&#39;app nativa. Per impostazione predefinita, tutte le modifiche eseguite localmente vengono caricate in [!DNL Experience Manager] automaticamente dopo un breve periodo di tempo. Con questa configurazione, i salvataggi frequenti durante la fase di work-in-progress verrebbero tutti caricati in [!DNL Experience Manager] e sottoposti a gestione delle versioni, creando numerosi problemi di traffico di rete e scalabilità, per non parlare delle versioni non necessarie in [!DNL Experience Manager].

L&#39;approccio consigliato è quello di utilizzare un&#39;opzione nell&#39;app desktop [!DNL Experience Manager] per disattivare gli aggiornamenti automatici e caricare manualmente le modifiche alle risorse in [!DNL Experience Manager], utilizzando l&#39;azione carica modifiche nell&#39;interfaccia utente dello stato delle risorse dell&#39;app.

#### Caricamento in blocco in DAM {#bulk-upload-to-dam}

In alcuni casi potrebbe essere necessario caricare simultaneamente un numero maggiore di file in DAM, ad esempio:

* Caricamento dei risultati di servizio fotografico o di progetti più grandi
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento delle risorse selezionate da un set più grande se la selezione viene eseguita al di fuori di DAM

La descrizione si riferisce al caricamento operativo dei file (ad esempio, ogni settimana o con ogni servizio fotografico), come parte normale del flusso di lavoro dell’utente desktop. Le migrazioni di risorse di grandi dimensioni non sono trattate qui.

Puoi utilizzare le seguenti funzionalità di caricamento:

* Per caricare in blocco cartelle di grandi dimensioni o gerarchiche, utilizzare l&#39;app desktop [!DNL Experience Manager] che fornisce la funzionalità di [caricamento cartelle](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it#upload-and-add-new-assets-to-aem). Puoi anche caricare strutture di cartelle gerarchiche. [!DNL Assets] sono caricati in background e, pertanto, non sono associati a una sessione del browser Web
* Per caricare alcuni file da una singola cartella, trascinarli direttamente nell&#39;interfaccia Web o utilizzare l&#39;opzione Crea nell&#39;interfaccia Web [!DNL Assets].
* A seconda dei requisiti aziendali, puoi anche utilizzare un caricatore personalizzato.

#### Gestire le risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se si utilizzano le condivisioni file di rete per gestire le risorse digitali, l&#39;utilizzo della condivisione di rete mappata dall&#39;app desktop [!DNL Experience Manager] potrebbe essere considerato un comodo sostituto. Durante la transizione da condivisioni di file di rete, l&#39;interfaccia Web [!DNL Experience Manager] offre un set completo di funzionalità di gestione delle risorse digitali che vanno ben oltre quanto possibile in una condivisione di rete (ricerca, raccolte, metadati, collaborazione, anteprime e così via) e l&#39;app desktop [!DNL Experience Manager] fornisce un comodo collegamento per collegare l&#39;archivio DAM lato server con il lavoro sul desktop.

Evitare di utilizzare l&#39;app desktop [!DNL Experience Manager] per gestire le risorse direttamente nella condivisione di rete di [!DNL Assets]. Ad esempio, evitare di utilizzare l&#39;app desktop [!DNL Experience Manager] per spostare/copiare più file. Utilizzare invece l&#39;interfaccia [!DNL Assets] per trascinare le cartelle da Finder/Explorer alla condivisione di rete o utilizzare la funzionalità Caricamento cartella [!DNL Assets].

#### Migrazione risorse {#asset-migration}

Per pianificare ed eseguire le migrazioni delle risorse dal sistema esistente a un nuovo sistema o la migrazione di grandi volumi di risorse archiviate nei server, consulta la [Guida alla migrazione](/help/assets/assets-migration-guide.md). L&#39;app desktop [!DNL Experience Manager] e le integrazioni da [!DNL Experience Manager] a [!DNL Creative Cloud] non supportano tali migrazioni. A causa dei grandi volumi di risorse da acquisire e dei requisiti aggiuntivi relativi alla mappatura, alla trasformazione e all’acquisizione dei metadati, le migrazioni devono essere gestite utilizzando strumenti e approcci diversi.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Experienci Manager di best practice per le app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html?lang=it)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=it)
>* [Integrazione di Experience Manager e Adobe Stock](aem-assets-adobe-stock.md)
