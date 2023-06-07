---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova informazioni sulla versione, novità, procedure guidate di installazione e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: 2c9337af99811d7b58712e1d0def7b5af5661c11
workflow-type: tm+mt
source-wordcount: '3567'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | Giovedì 25 maggio 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] La versione 6.5.17.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati dopo la disponibilità iniziale della versione 6.5 di aprile 2019. [Installa il service pack](#install) il [!DNL Experience Manager] 6.5

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Alcune delle funzioni chiave e dei miglioramenti introdotti in questa versione sono i seguenti:

* **Miglioramenti all’esperienza di ricerca** - È ora possibile eseguire rapidamente le seguenti operazioni sulle risorse visualizzate nei risultati di ricerca:
   * Creare un flusso di lavoro
   * Crea una versione
   * Correlare o non correlare le risorse

   Per eseguire queste operazioni, non è necessario passare alla posizione della risorsa e visualizzarne le proprietà.
* **Dynamic Media _Snapshot_**- Sperimentate immagini di prova o URL Dynamic Media per vedere l&#39;output di diversi modificatori di immagini e ottimizzazioni Smart Imaging per le dimensioni dei file (con distribuzione WebP e AVIF), la larghezza di banda della rete e le proporzioni pixel del dispositivo. Consulta [Snapshot Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).
* **Streaming DASH con Dynamic Media** - È stato avviato il supporto del nuovo protocollo (DASH - Dynamic Adaptive Streaming over HTTP) per lo streaming adattivo nella distribuzione di video Dynamic Media (con CMAF abilitato). Disponibile ora per tutte le aree geografiche, [tramite un ticket di supporto](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Integrazione di Experience Manager Sites e frammenti di contenuto con Assets Dynamic Media di nuova generazione** - Gli utenti di Experience Manager Assets as a Cloud Service Next-Generation Dynamic Media possono ora utilizzare queste risorse ospitate sul cloud per la creazione e la distribuzione con istanze on-premise o Managed Services di Experience Manager Sites 6.5.
* **Integrazione di Adaptive Forms nelle pagine Experience Manager Sites**: crea esperienze di registrazione digitale utilizzando componenti Forms adattivi nell’editor di Experience Manager Sites utilizzando: - Contenitore Forms adattivo e Forms adattivo - Componenti Incorpora(v2).
* **Supporto di reCAPTCHA Enterprise in Experience Manager Forms**: è stato aggiunto il supporto per reCAPTCHA Enterprise in Experience Manager Forms, che fornisce una protezione avanzata contro le attività fraudolente e lo spam, oltre al supporto esistente per Google reCAPTCHA v2.
* **Supporto per Adobe Acrobat Sign for Government con Experience Manager Forms**: consente l’integrazione sicura e conforme di Experience Manager Forms con Adobe Sign for Government (conforme a FedRAMP).
* **Abilitare l’integrazione di Salesforce con Experience Manager Forms per lo scambio di dati**: configura l’integrazione tra Experience Manager Forms e l’applicazione Salesforce utilizzando il flusso delle credenziali del client OAuth 2.0. Questa funzionalità consente l&#39;autenticazione e l&#39;autorizzazione sicure e dirette dell&#39;applicazione e permette una comunicazione fluida senza il coinvolgimento dell&#39;utente.
* **Ottimizzazione e funzionalità migliorate del motore del flusso di lavoro**: aumenta le prestazioni dei motori del flusso di lavoro riducendo al minimo il numero di istanze del flusso di lavoro. Oltre a `COMPLETED` e `RUNNING` valori di stato, il flusso di lavoro supporta anche tre nuovi valori di stato: `ABORTED`, `SUSPENDED`, e `FAILED`.


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* Quando pubblichi più di 40 PDF contemporaneamente, [!DNL Experience Manager] smette di rispondere e diventa non disponibile per qualche tempo. (ASSETS-21789)
* Se hai effettuato l’accesso come utente di prova, quando fai clic su proprietà di una risorsa non potrai visualizzare le risorse relative a una particolare risorsa. (ASSETS-21648)
* Durante la modifica di risorse tramite `Desktop Actions`, se si tenta di archiviare più di cinque risorse contemporaneamente, `Limit Reached` viene visualizzato un errore e le risorse selezionate vengono estratte. (ASSETS-21121)
* Impossibile ordinare le risorse per nome in una raccolta. (ASSETS-20924)
* Impossibile impostare le dimensioni sulle risorse di un tipo di formato immagine. (ASSETS-20835)
* Il testo della descrizione comando e il relativo sfondo nel campo Cerca/Aggiungi indirizzo e-mail non visualizzano il rapporto di contrasto appropriato durante la condivisione di un collegamento. (ASSETS-17347)
* Quando si espande `Notifications`, il testo non viene visualizzato correttamente a causa della spaziatura tra i paragrafi. (ASSETS-17345)
* Quando copi una risorsa in una raccolta, `Public Collection` la casella di controllo non viene visualizzata in modo appropriato. (ASSETS-17343)
* Gli elementi utilizzano attributi ARIA senza un ruolo. (ASSETS-17325,ASSETS-17323)
* Il collegamento non è descrittivo quando si espande `Notifications`. (ASSETS-17283)
* Quando navighi ed espandi [!DNL Smart Crop] , il contenuto viene visualizzato come un elenco ma non è contrassegnato come elenco non ordinato. Di conseguenza, l’assistente vocale non riconosce l’elenco non ordinato e lo legge come testo normale. (ASSETS-17247)
* Il `Sort By` l’etichetta non è associata al relativo elenco a discesa. Di conseguenza, l’assistente vocale non riconosce le opzioni a discesa. (ASSETS-17239)
* Impossibile spostarsi in avanti o all&#39;indietro utilizzando i tasti Tab o Arrow quando si tenta di aggiungere un utente utilizzando `Add user` casella combinata. (ASSETS-17233)
* L’assistente vocale non trasmette correttamente le informazioni per il passaggio Flussi di lavoro (ASSETS-17285).
* Quando si passa a `Saved Searches` alla casella combinata, al nome e al ruolo non sono assegnate etichette. (ASSETS-17329)
* Quando navighi `Collection` e passa il mouse sul testo *Membri*, il testo non viene visualizzato come contrassegnato. Di conseguenza, l’assistente vocale non riconosce il testo dell’intestazione e lo legge come testo normale. (ASSETS-17245)
* Impossibile accedere `View Settings` mediante il tasto di scorrimento verso il basso o verso l&#39;alto della tastiera. (ASSETS-17257)
* Impossibile attivare un flusso di lavoro per più risorse selezionate trovate utilizzando i filtri di ricerca. (ASSETS-7689)
* Quando selezioni una risorsa (o più risorse) dai risultati della ricerca, l’opzione di correlazione o non correlazione non è visibile. Ma l&#39;opzione è disponibile, altrimenti. (ASSETS-7679)
* Il pannello Filtri di ricerca si apre una sola volta dopo l’accesso e non si apre se esci dalla pagina di ricerca ed esegui nuovamente la ricerca. (ASSETS-7671)
* Nella casella combinata e-mail non viene visualizzato il rapporto di contrasto appropriato durante la condivisione di un collegamento. (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* La connessione a Dynamic Media è interrotta quando esiste già una configurazione cloud di Dynamic Media. (ASSETS-23057)
* Migliori prestazioni durante la navigazione in cartelle con molti video Dynamic Media e risolti non riescono a caricare il problema sulla vista a schede delle cartelle. (ASSETS-23016)
* I token di anteprima vengono rimossi da `error.log` che può essere utilizzato per richiedere contenuto protetto dai server di test protetti. (ASSETS-22685)
* Rendering miniatura PDF aggiunta di un&#39;ombreggiatura. È stata aggiornata la libreria Gibson versione 4.0.1680232194 per risolvere il problema di rendering delle miniature dei PDF. (ASSETS-22585)
* La modalità ibrida di Dynamic Media è ora compatibile con New Relic Agent versione 8.0.1 (ASSETS-22578).
* Gli elenchi di controllo di accesso (ACL, Access Control List) di Experience Manager ora vengono rispettati quando si visualizzano in anteprima i file Dynamic Media su Experience Manager. (ASSETS-21628)
* Gli assistenti vocali non passano all’elemento nascosto quando l’utente tenta di spostarsi utilizzando il tasto freccia giù o il tasto TAB. (ASSETS-5617)
* Interfaccia utente del profilo immagine limitata per ritagli avanzati con lo stesso nome, la stessa dimensione o entrambi. (ASSETS-16997)
* I valori predefiniti di larghezza e altezza sono ora impostati su 50 pixel per Ritagli avanzati nell’interfaccia utente del profilo immagine. (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* I tag spostati vengono raccolti come rifiuti, ma sono ancora oggetto di riferimento dai prodotti in `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

* Dopo l’aggiornamento a AEM 6.5.15.0 Service Pack, i moduli HTML5 non funzionano o non vengono caricati correttamente nel browser Edge con modalità di compatibilità IE. (FORMS-8526, FORMS-8523)
* Quando un utente applica il Service Pack AEM 6.5.16.0, l’editor di regole non si apre. (FORMS-8290)
* Se a un componente Casella numerica viene applicato il numero massimo di cifre, la convalida non riesce. (FORMS-7938)
* Durante la creazione di istruzioni di comunicazione interattive, il componente grafico nel PDF non viene generato correttamente. (FORMS-7827, FORMS-8297)
* La funzione di Garbage Collection di Java™ non è in grado di cancellare l’heap di vecchia generazione su un server OSGi di Experience Manager Forms. (FORMS-8207)
* Quando un utente effettua l’aggiornamento a Service Pack Experience Manager 6.5.16.0, le proprietà dei metadati CRX non sono presenti dopo l’invio. (FORMS-8205)
* Quando un utente disabilita il componente Selettore data in un modulo adattivo, questo rimane modificabile. (FORMS-7804)
* Nell&#39;Experience Manager 6.5.16.0 di Forms Service Pack, quando un utente tenta di modificare i Coordinatori set di criteri, l&#39;opzione Manager Document Publisher rimane sempre deselezionata. (FORMS-7775, FORMS-8599)
* Quando un utente esegue l’aggiornamento a Service Pack di Experience Manager 6.5.16.0, il metodo &quot;GuideNode.externalize&quot; che gestisce le stringhe da tradurre non funziona più. (FORMS-7709)
* In `Assign task` passaggio: quando un utente seleziona &quot;Invia e-mail di notifica&quot; e richiama il flusso di lavoro, il testo non viene visualizzato correttamente nell’e-mail ricevuta. I punti interrogativi vengono ricevuti al posto del testo nell’e-mail ricevuta. (FORMS-7675)
* È in corso la localizzazione parziale del documento record. (FORMS-7674, FORMS-7573)
* Un utente non può modificare i set di criteri, anche se dispone di autorizzazioni specifiche. (FORMS-7665)
* Quando un utente accede a `forms-users` tenta di creare un modulo, l’istanza di Experience Manager Forms si blocca. (FORMS-7629)
* Quando l’utente fa clic sui pulsanti Reimposta, Salva o Invia in un modulo adattivo, sullo schermo non viene visualizzato alcun messaggio. (FORMS-7524)
* Per migliorare le prestazioni della conversione PDFG in un Service Pack Experience Manager 6.5.16.0, l’intervallo di sospensione è reso configurabile. (FORMS-6752)
* L’opzione di attivazione rimane invariata, ma la visibilità del campo cambia anche quando l’utente trascina leggermente il cursore. (FORMS-6728)
* Quando l’utente esegue l’aggiornamento a Service Pack di Experience Manager 6.5.15.0, il reindirizzamento non funziona più se viene eseguito il rendering di un modulo adattivo in Internet Explorer. (FORMS-6725)
* Lo strumento PAC 2021 per tutti gli oggetti di sfondo in un modulo PDF creato da un Designer di Experienci Manager restituisce un errore come `Path object not tagged`. (FORMS-6707)
* Quando un utente applica un filtro nella casella in entrata, genera un’ `NullPointerException` errore. (FORMS-6706)
* Quando un utente importa un file modello (con estensione tds) con frammenti di riferimento, si verifica un arresto anomalo di Experience Manager Designer. (FORMS-6702)
* Se l’utente crea un PDF statico utilizzando il servizio di output in una finestra di progettazione di Experience Manager Forms 6.5, si verifica un errore di tipo `OCCD (optional content configuration dictionary) contains AS key`. (FORMS-6691)
* Quando l’utente crea un flusso di lavoro semplice e aggiunge una variabile semplice, viene `set variable mapping` si verifica un errore. (FORMS-5819)
* Quando un utente tenta di generare un PDF utilizzando il servizio di output, anche se è contrassegnato come `PDF/A-1a`, un controllo di conformità utilizzando`Preflight` errore del servizio. (LC-3920837)
* Dopo aver installato un Service Pack di Experience Manager 6.5.16.0, non è possibile aprire un Designer di Experienci Manager. (LC-3921000)
* Quando un utente aggiunge una casella di controllo e un pulsante di scelta, la struttura di una struttura di tag non viene generata in base agli standard PDF. (LC-3920838)
* Nel caso in cui un utente generi un PDF statico utilizzando l’incorporamento e il subset di font tramite il servizio di output, il PDF risultante contiene solo i font incorporati. (LC-3920963)
* Il testo ebraico non viene visualizzato correttamente nel formato RTL. (LC-3919632)
* Quando un utente esegue l’aggiornamento all’Experience Manager 6.5.16.0 Service Pack su un server JBoss® Turnkey, il servizio Signature non viene richiamato. L’errore riscontrato è: `java.lang.ClassCastException: com.adobe.xfa.TextNode cannot be cast to com.adobe.xfa.Element`. (FORMS-7833)
* Dopo l’aggiornamento all’Experience Manager 6.5.14.0 Service Pack, i processi di Workbench per spostare un nodo CRX da una posizione all’altra non funzionano. L’errore si verifica come `ALC-CRX-30000-000: com.adobe.ep.crx.client.exceptions.CRCException: ALC-CRX-030-000-[Internal Server Error]`. (FORMS-7713)
* Quando un utente si aggiorna all’Experience Manager 6.5.16.0 Service Pack, il `Usage Rights` non si applica. (FORMS-7892)
* Quando un utente tenta di generare un documento PDF, la convalida PDF/A-1b ha esito negativo. (FORMS-7615)
* Quando un utente fa clic su `Configure` opzione per `Form Container` , il browser smette di rispondere. (FORMS-7605)
* Quando un utente si aggiorna a Experience Manager Forms 6.5.16.0 Service Pack e tenta di modificare il `LicenseType` a `Production`, le modifiche non vengono applicate. (FORMS-7594)
* Quando un utente tenta di richiamare un processo LCA con un PDF che include `Chinese Full Width Characters`, si verifica un problema con `ValidateForm` processo. (FORMS-7464)
* In Experience Manager Forms Designer, XMLFM genera un output ZPL con diversi formati di carta, ad esempio lettera, A4 e A5, per i modelli basati su XDP. (FORMS-7898)

## Integrazioni{#integrations-6517}

* Quando si converte una configurazione Adobe Target IMS in una credenziale utente una in configurazioni cloud legacy, la `connectedWhen` la proprietà non cambia. Questo problema fa sì che tutte le chiamate vadano come se la configurazione fosse ancora basata su IMS. (CQ-4352810)
* Aggiunta `modifyProperties` autorizzazione a `fd-cloudservice` utente di sistema per la configurazione di Adobe Sign. (FORMS-6164)
* Con Experience Manager integrato con Adobe Target, quando crei un’attività di test AB, questa non sincronizza con Target i tipi di pubblico ad essa associati. (NPR-40085)

## Oak{#oak-6517}

Da Service Pack 13 e versioni successive è stato avviato il seguente log degli errori che influisce sulla cache di persistenza:

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
    at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
    at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
    at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
    at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
    at org.h2.mvstore.db.Store.<init>(Store.java:129)
```

Oppure

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
```

Per risolvere l&#39;eccezione, eseguire le operazioni seguenti:

1. Elimina le due cartelle seguenti da `crx-quickstart/repository/`

   * `cache`
   * `diff-cache`

1. Installa il Service Pack o riavvia Experience Manager as a Cloud Service.
Nuove cartelle di `cache` e `diff-cache` vengono create automaticamente e non si verifica più un&#39;eccezione relativa a `mvstore` nel `error.log`.

## Platform{#platform-6517}

* Nell’interfaccia utente di Experience Manager Tag Management (/aem/tags/), gli spazi dei nomi e i tag vengono visualizzati nell’ordine in cui vengono creati. Tuttavia, in presenza di numerosi spazi dei nomi e tag, è difficile visualizzarli e gestirli. Questo problema è dovuto al fatto che non possono essere ordinati in altro modo. (NPR-39620)
* È stato necessario aggiornare la versione di chiusura di Google perché Minification Js non funziona per alcune librerie client. (NPR-40043)

## [!DNL Sites]{#sites-6517}

* Riduzione delle prestazioni in LinkCheckerTransformer. (SITES-11661)
* Le copie in lingua di una pagina non venivano aggiornate come previsto. (SITES-11191)
* Apertura della chiamata per pagine non relative a una campagna `targeteditor.html` inutilmente. Rimuovi il `targeteditor` chiama quando non è necessario. (SITES-12469)
* Non è possibile creare Live Copy per le pagine con annotazioni. (SITES-12154)
* Il rollout delle pagine funziona su Experience Manager 6.5.16. (SITES-12008)
* Memoria insufficiente; elevata attività di Garbage Collection a causa di `NotificationManagerImpl`. `NotificationManager` aggiornamento del bundle all’Experience Manager 6.5. (SITES-11440)
* Sono stati corretti i test IT WCM che bloccavano il service pack 17. (SITES-13089)
* Il recupero dei riferimenti a Sites non riesce nel servlet. (SITES-10901)

### [!DNL Sites] - Interfaccia utente amministratore{#sites-adminui-6517}

* Impossibile chiudere la finestra di anteprima per il selettore di immagini miniatura. (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* Configurazione per la connessione all’oggetto del servizio Polaris (URL, credenziali, callback e così via). (SITES-12149)
* Utilizzo di `SemanticDataType.REFERENCE` devono supportare &quot;Remote-Asset-IDs&quot;. (SITES-12127)
* Integra il selettore risorse Polaris nell’editor dei frammenti di contenuto. (SITES-12125)
* Per accedere all’endpoint del servizio metadati era necessaria un’intestazione http obbligatoria. (SITES-13068)
* L’implementazione di GraphQL 6.5 non era alla pari con il Cloud Service (primario); i problemi identificati sono stati risolti. (SITES-13096)
* Il paging/ordinamento GraphQL e il filtro ibrido dovrebbero essere disponibili all’Experience Manager 6.5/AMS. (SITES-9154)

### [!DNL Sites] - Componenti core{#sites-core-components-6517}

* La proprietà `cq-msm-lockable` presenta un valore di reindirizzamento errato nel componente della pagina Foundation. (SITES-10904)
* Il selettore risorse remote reindirizza sempre all’ambiente di stage IMS. (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* Se si seleziona una configurazione Externalizer in un frammento di esperienza durante l’esportazione in Adobe Target, viene inviato l’URL esternalizzato errato. (SITES-12402)
* Rimuovi i termini non inclusivi; applica le linee guida per i termini inclusivi. (SITES-11244)

### [!DNL Sites] - Editor pagina{#sites-pageeditor-6517}

* Nella barra laterale di Experience Manager content finder non viene visualizzata alcuna miniatura per un carosello impostato. (SITES-8593)

## Sling{#sling-6517}

* Sling `ResourceMerger` utilizza una quantità elevata di CPU se fornita con un percorso fittizio, causando una negazione del servizio. (NPR-40338)

## Progetti di traduzione{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* La copia per lingua non viene creata quando l’utente non configura campi non obbligatori. (NPR-40036)

## Interfaccia utente{#ui-6517}

* Il pulsante Annulla nelle proprietà della pagina non è attivo. Dovresti passare all’interfaccia utente Amministratore sito. (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## Flusso di lavoro{#workflow-6517}

* Modifiche alla console del flusso di lavoro. (NPR-40502)
* `SegmentNotfound errors` nei registri di un’istanza di authoring di produzione, causato da Resource resolver non chiuso nella classe `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* Chiuso non chiuso `ResourceResolver` è in corso la registrazione dell&#39;eccezione. (ASSETS-22495)
* L’autore di Experience Manager si blocca quando PSD/PDF con un numero enorme di `DocumentAncestors` attributi dei metadati caricati. (ASSETS-22966)
* Perdita di sessione nella classe `InboxSharingCache` con `user-reader-service`. (CQ-4352513)
* L&#39;elenco di utenti e gruppi incompleto viene visualizzato quando il passaggio &quot;Selettore partecipante iniziatore flusso di lavoro&quot; elenca gli utenti e i gruppi per il passaggio Partecipante. Questo problema si verificava quando un gruppo era anche membro di un altro gruppo. (NPR-40055)
* È stata migliorata la rimozione dei flussi di lavoro. (NPR-40459)

## Installa [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0 richiede [!DNL Experience Manager] 6.5. Cfr. [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate. <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del service pack è disponibile su Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip).
* In una distribuzione con MongoDB e più istanze, installa [!DNL Experience Manager] 6.5.17.0 in una delle istanze di authoring che utilizzano Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> L’Adobe non consiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.17.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup del `crx-repository` nel caso sia necessario riportarlo indietro. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installare il service pack in [!DNL Experience Manager] 6,5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia di riavviare se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup del file [!DNL Experience Manager] dell&#39;istanza.

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Consulta [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta si apre una finestra di dialogo sull’interfaccia utente di Gestione pacchetti durante l’installazione del service pack. L’Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle di aggiornamento prima di essere sicuri che le installazioni siano riuscite. In genere, questo problema si verifica in [!DNL Safari] ma può verificarsi in modo intermittente su qualsiasi browser.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente [!DNL Experience Manager] 6.5.17.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserisci la confezione in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza il [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` affinché i pacchetti nidificati vengano installati.

>[!NOTE]
>
>L&#39;Experience Manager 6.5.17.0 non supporta l&#39;installazione Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalidare l’installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo di questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa della versione aggiornata `Adobe Experience Manager (6.5.17.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (usa la console web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.15 o successiva (utilizzare la console Web: `/system/console/bundles`). <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installa Service Pack per [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Per istruzioni sull&#39;installazione del service pack in Experience Manager Forms, vedere [Istruzioni di installazione di Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installare il pacchetto di indice GraphQL per frammenti di contenuto Experience Manager{#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare [Frammento di contenuto di Experience Manager con pacchetto indice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

In questo modo puoi aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate.

Se non si installa questo pacchetto, è possibile che le query GraphQL risultino lente o non riuscite.

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar{#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.17.0 è disponibile nel [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come usare UberJar](/help/sites-developing/ht-projects-maven.md) e includere la seguente dipendenza nel POM del progetto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece che nell’archivio Maven pubblico di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Quindi, non c&#39;è `classifier`, con `apis` come valore, per `dependency` tag.

## Funzioni obsolete{#removed-deprecated-features}

Di seguito è riportato un elenco di funzionalità contrassegnate come obsolete con [!DNL Experience Manager] 6.5.7.0. Le funzioni sono contrassegnate come obsolete inizialmente e successivamente rimosse in una versione futura. Viene fornita un’opzione alternativa.

Controlla se utilizzi una funzione o una funzionalità in una distribuzione. Inoltre, pianifica di modificare l’implementazione per utilizzare un’opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrazioni | Schermata **[!UICONTROL Consenso Experienci Manager Cloud Services]** è obsoleto perché [!DNL Experience Manager] e [!DNL Adobe Target] L’integrazione di è stata aggiornata in [!DNL Experience Manager] 6.5. L’integrazione supporta l’API di Adobe Target Standard. L’API utilizza l’autenticazione tramite Adobe IMS e [!DNL Adobe I/O Runtime]. Sostiene il ruolo crescente del lancio Adobe nello strumento [!DNL Experience Manager] per le pagine di analytics e personalizzazione, la procedura guidata di consenso è funzionalmente irrilevante. | Configurare connessioni di sistema, autenticazione Adobe IMS e [!DNL Adobe I/O Runtime] integrazioni tramite il rispettivo [!DNL Experience Manager] servizi cloud. |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto per [!DNL Experience Manager] 6.5 | N/D |

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Aggiorna le query GraphQL che potrebbero aver utilizzato un nome API personalizzato per il modello di contenuto in base al nome predefinito del modello di contenuto.

* Una query GraphQL può utilizzare `damAssetLucene` indice invece di `fragments` indice. Questa azione potrebbe causare l’errore o richiedere molto tempo per l’esecuzione delle query GraphQL.

   Per risolvere il problema: `damAssetLucene` deve essere configurato per includere le due proprietà seguenti:

   * `contentFragment`
   * `model`

   Dopo aver modificato la definizione dell’indice, è necessaria una reindicizzazione (`reindex` = `true`).

   Dopo questi passaggi, le query GraphQL dovrebbero funzionare più rapidamente.

* As [!DNL Microsoft® Windows Server 2019] non supporta [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] non supporta le installazioni chiavi in mano per [!DNL Experience Manager Forms 6.5.10.0].

* Se aggiorni il tuo [!DNL Experience Manager] dalla versione 6.5.0 alla versione 6.5.4 al service pack più recente su Java™ 11, vedi `RRD4JReporter` eccezioni in `error.log` file. Per interrompere le eccezioni, riavvia l’istanza di [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Gli utenti possono rinominare una cartella in una gerarchia in [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] fino alla ripubblicazione della cartella principale.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata nel Browser proprietà. Per risolvere il problema, fai clic su per configurare un altro campo del modulo adattivo nello stesso editor.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando l’integrazione di Adobe Target è configurata in [!DNL Experience Manager] se utilizzi l’API di Target Standard (autenticazione IMS), e successivamente esporti frammenti di esperienza in Target, verranno creati tipi di offerta errati. Invece del tipo &quot;Frammento di esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in granite/operations/maintenance.
   * La convalida lato server di Moduli adattivi non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nessuna finestra di manutenzione trovata in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile durante l’anteprima della risorsa tramite il visualizzatore di banner Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : timeout in attesa del completamento della modifica del registro, annullamento della registrazione.

* Quando si tenta di spostare, eliminare o pubblicare frammenti di contenuto, siti o pagine, si verifica un problema quando si recuperano i riferimenti ai frammenti di contenuto, poiché la query in background non riesce. In altre parole, la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell’indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* Sulla piattaforma JBoss® 7.1.4, quando l’utente installa il service pack Experience Manager 6.5.16.0 o versione successiva, `adobe-livecycle-jboss.ear` distribuzione non riuscita.
* Le versioni JDK superiori a 1.8.0_281 non sono supportate per il server WebLogic JEE.

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.17.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Elenco dei bundle OSGi inclusi nell’Experience Manager 6.5.17.0](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi nell&#39;Experience Manager 6.5.17.0](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

