---
title: Note generali sulla versione per  [!DNL Adobe Experience Manager] 6.5
description: '[!DNL Adobe Experience Manager] 6.5 note che descrivono le informazioni sulla versione, le novità, le modalità di installazione e gli elenchi dettagliati delle modifiche.'
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '4477'
ht-degree: 5%

---

# Note generali sulla versione per [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] |
|---|---|
| Versione | 6,5 |
| Tipo | Versione principale |
| Data di disponibilità generale | 8 aprile 2019 |
| Aggiornamenti consigliati | Vedi [Aggiornamenti recenti di AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it). |

### Bizzarra {#trivia}

Il ciclo di rilascio di questa versione di [!DNL Adobe Experience Manager] è iniziato il 4 aprile 2018 ed è terminato il 28 marzo 2019, dopo 23 iterazioni di controllo qualità e correzione di bug. Il numero totale di problemi relativi al cliente, inclusi miglioramenti e nuove funzioni, risolti in questa versione è 1345.

[!DNL Adobe Experience Manager] 6.5 è generalmente disponibile dall&#39;8 aprile 2019.

![Schermata di accesso ad AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novità {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 è una versione di aggiornamento della base di codice di [!DNL Adobe Experience Manager] 6.4. Fornisce funzionalità nuove e migliorate, correzioni chiave per i clienti, miglioramenti per i clienti ad alta priorità e correzioni generali di bug orientate al consolidamento del prodotto. Include anche [!DNL Adobe Experience Manager] versioni di Service Pack 6.4 fino a SP4.

L’elenco seguente fornisce una panoramica, mentre le pagine successive elencano tutti i dettagli.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e del repository dei contenuti Java™: Apache Jackrabbit Oak 1.10.2.

Quickstart utilizza Eclipse Jetty 9.4.15 come servlet engine.

#### Supporto Java™  {#java-support}

* Nuovo supporto per Java™ 11 e Java™ 8 già supportato.
* Per ottenere prestazioni ottimali, sostituire i valori GC predefiniti con altri valori. Per ulteriori informazioni, consulta la sezione [Installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Gli aggiornamenti di manutenzione di Java™ 11 e Java™ 8 vengono distribuiti da Adobe per l’utilizzo da parte dei clienti nei progetti correlati ad AEM, quando non sono disponibili al pubblico da Oracle.

#### Sviluppo Java™ {#java-development}

* Sono ora disponibili [due versioni di Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), una versione consigliata con interfacce pubbliche non contrassegnate per l&#39;obsolescenza e una versione che include interfacce contrassegnate per l&#39;obsolescenza.

#### Interfaccia utente {#user-interface}

Sono stati apportati diversi miglioramenti all’interfaccia utente per renderla più produttiva e facile da utilizzare.

* Nuova interfaccia utente per la gestione delle autorizzazioni per utenti e gruppi.
* Le viste a colonne ora caricano solo le voci visibili sullo schermo e ne caricano di più solo quando l’utente inizia a scorrere. La vista a elenco e a schede lo faceva già dalla versione 6.0 (migliorata nella versione 6.4).
* Le visualizzazioni a colonne ora includono lo stato del flusso di lavoro per le pagine o le risorse, se applicabile.
* L&#39;azione [Seleziona tutto](/help/sites-authoring/basic-handling.md#select-all) è un modo rapido per eseguire un&#39;azione con tutte le pagine/risorse nella stessa cartella.
* L&#39;azione [Seleziona tutto](/help/sites-authoring/basic-handling.md#select-all) tenta di eseguire l&#39;azione su tutte le pagine/risorse, non solo su ciò che è stato caricato. Se l&#39;azione non viene aggiornata per gestire le azioni in blocco, viene visualizzata una finestra di dialogo di avviso.

>[!CAUTION]
>
>Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia classica. AEM 6.5 include l’interfaccia classica; i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a utilizzarla così com’è. L’interfaccia classica rimane completamente supportata anche se è obsoleta. [Ulteriori informazioni](/help/sites-deploying/ui-recommendations.md).

#### Ricerca e indicizzazione {#indexing-and-search}

* La funzione Ricerca in Oak ora supporta i facet dinamici. Ad esempio, la barra dei filtri nella ricerca di risorse mostra il numero stimato di risultati.
* QueryBuilder è stato esteso per fornire risultati con facet dinamici.

#### Aggiornamento {#upgrade}

* L’aggiornamento diretto a AEM 6.5 è supportato per i clienti che eseguono AEM 6.2, 6.3 e 6.4. I clienti che utilizzano 5.x o 6.0/6.1 e desiderano utilizzare l’aggiornamento sul posto devono prima eseguire l’aggiornamento alla versione 6.4. Quindi, effettua l’aggiornamento a 6.5 oppure tramite il trasferimento dei contenuti tra le istanze direttamente in AEM 6.5.
* La procedura di aggiornamento rimane in gran parte la stessa della versione 6.5.
* Continuiamo a supportare le funzioni di Compatibilità con le versioni precedenti, Valutazione della complessità dell’aggiornamento e Aggiornamenti sostenibili introdotte nella versione 6.4. Sono stati apportati aggiornamenti specifici alle versioni in queste aree, ove necessario.
* Il pacchetto del rilevatore pattern è ora semplificato. Esiste un pacchetto che valuta gli aggiornamenti alla versione 6.5 per le versioni di origine disponibili.
* Per informazioni dettagliate sulla procedura di aggiornamento, vedere la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md).

#### Progetti e flussi di lavoro {#projects-and-workflows}

* Il nuovo editor modello di flusso di lavoro introdotto in 6.4 è stato migliorato per includere più operazioni come Copia e Pubblica, Supporto delle variabili nei passaggi del flusso di lavoro e `OR` e `AND` divisioni migliorate.

#### Archivio {#repository}

* Le basi di Adobe Experience Manager 6.5 si basano sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e del Content Repository Java™: Apache Jackrabbit Oak 1.10.2.
* Per una panoramica dei problemi risolti, vedere [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) e [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nuova versione del Tar del segmento di Oak, presente a partire da AEM 6.3, richiede una migrazione dell’archivio. Questo passaggio è obbligatorio se si esegue l’aggiornamento da una versione precedente di TarMK o si desidera cambiare il nuovo Tar segmento da un altro tipo di persistenza. Per ulteriori informazioni sui vantaggi del nuovo Tar segmento, consulta le [Domande frequenti sulla migrazione al Tar segmento di Oak](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Sono state aggiunte le librerie dell’utilità OSGi Promises e Converter.

#### Protezione {#security}

* È stata aggiunta la scadenza della password per l’utente amministratore.

#### Server web {#web-server}

* La distribuzione Quickstart utilizza Eclipse Jetty 9.4.15 come servlet engine (AEM 6.4 fornito con 9.3.22).

### [!DNL Experience Manager] siti {#experience-manager-sites}

#### App a pagina singola gestite {#managed-single-page-apps}

L&#39;Editor pagina aggiunge la possibilità di modificare il contenuto nel contesto e di comporre/layout all&#39;interno di esperienze sottoposte a rendering lato client (noto anche come [Editor SPA](/help/sites-developing/spa-architecture.md)). Le app a pagina singola esistenti create con il framework JavaScript React o Angular possono essere estese con AEM SJ SDK per essere rese modificabili dagli utenti.

Viene fornito per la prima volta come parte di AEM 6.4 SP2, con AEM 6.5 il supporto SPA offre le seguenti funzionalità:

* Utilizza Editor modelli per modificare e configurare le parti modificabili di AEM nell’applicazione a pagina singola
* Utilizzare la gestione multisito per creare esperienze SPA in base al paese, al franchising o al bianco

#### Gestione dei contenuti headless {#headless-content-management}

AEM può distribuire il contenuto in vari formati e da vari livelli dello stack. Alcuni sono disponibili dal 2008 con [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) e [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([Sling Model Exporter](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=it)) è stato introdotto in AEM 6.3 ed è il metodo utilizzato da AEM SJ SDK per idratare le app a pagina singola. L&#39;API [HTTP per Assets](/help/assets/mac-api-assets.md) è un&#39;API CRUD, estesa per AEM 6.5.

Nuove funzionalità API HTTP:

* Aggiunta del supporto per [Frammenti di contenuto all&#39;API HTTP per Assets](/help/assets/assets-api-content-fragments.md) per creare, aggiornare, leggere ed eliminare frammenti.
* Esposizione di elenchi di frammenti di contenuto tramite Content Services con il [componente core Elenco frammenti di contenuto](https://www.aemcomponents.dev).
* [Libreria dei componenti core](https://www.aemcomponents.dev) che mostra l&#39;output JSON predefinito di Content Services per ogni componente

#### Componente aggiuntivo Screens {#screens-add-on}

Progetta, distribuisci e ottimizza in modo efficiente le esperienze su tutti i display digitali, dai chioschi interattivi al digital signage.

* Unificare esperienze e contenuti tra contenuti digitali e in-store con un migliore riutilizzo dei contenuti
* Flussi di lavoro semplificati per l’authoring e l’approvazione/pubblicazione con supporto per Launches
* Modifica e fornisci esperienze interattive utilizzando l’Editor SPA
* Utilizzo di Launches per pianificare modifiche future al contenuto per la segnaletica
* Riproduzione controllata in un canale di sequenza
* Creazione automatica di una struttura di progetto utilizzando un file di origine, ad esempio un foglio di Excel
* Supporto esteso del lettore multimediale con un funzionamento affidabile on-line e offline (Smart Sync) in grado di scalare anche alle reti di segnaletica più grandi.
* Personalizza in base alla posizione o alla configurazione del contenuto attivato dai dati utilizzando segnaposto dinamici.
* Informazioni unificate basate sull’integrazione di Adobe Analytics in AEM Screens Player

Per ulteriori dettagli sulle modifiche apportate ad AEM Screens, consulta le Note sulla versione nella [Guida utente di AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=it).

#### Sviluppo di componenti e modelli {#component-amp-template-development}

* Archetipo progetto Maven 18+ per i nuovi progetti, consulta [GitHub per le note sulla versione](https://github.com/adobe/aem-project-archetype/releases).
* Archetipo progetto Maven app a pagina singola 1.0.6+ per i nuovi progetti, consulta [GitHub per le note sulla versione](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versione 1.4, consulta [GitHub per le note sulla versione](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * Operatore &quot;in&quot; per stringhe, array e oggetti:

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * Dichiarazioni di variabili con data-sly-set :
     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Elenca e ripeti parametri di controllo: begin, step, end:
     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificatori per data-sly-unwrap:

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * Supporto per numeri negativi

* Componenti core 2.3.2+, consulta [GitHub per le note sulla versione](https://github.com/adobe/aem-core-wcm-components/releases).
* Grid System per il contenitore di layout. Vedere [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: ha impostato Google Closure Compiler come predefinito per la minimizzazione delle clientlibs di JavaScript (il vecchio predefinito era Yahoo YUI) e ha aggiornato Google Closure Compiler alla versione v20190121
* Editor modelli e criteri

   * Creare e modificare modelli per le app a pagina singola che utilizzano JS SDK (noto anche come editor SPA)

* Sito di riferimento We.Retail 4.0, consulta [GitHub per le note sulla versione](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Toolkit per aggiornare i siti esistenti in modo da utilizzare le funzionalità dell&#39;editor più recenti. Vedere [Archivio GitHub](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM include la versione 1.12.4 della libreria jQuery per fornire la massima compatibilità con il codice personalizzato esistente. Adobe ha apportato modifiche per risolvere problemi di sicurezza noti.

#### Amministrazione sito {#site-administration}

* La barra [Riferimento](/help/sites-authoring/author-environment-tools.md#references) include una nuova sezione in cui sono elencati i collegamenti interni che puntano alla pagina selezionata. Questa funzione è utile quando si prevede di mettere una pagina offline o eliminarla, per vedere quali pagine devono essere regolate prima di metterle offline.
* La [visualizzazione elenco](/help/sites-authoring/basic-handling.md#list-view) include una nuova colonna del flusso di lavoro che mostra lo stato quando la pagina si trova in un flusso di lavoro.
* Nelle [proprietà pagina](/help/sites-authoring/editing-page-properties.md) è ora possibile cercare le risorse esistenti quando si assegna una miniatura alla pagina (scheda Miniatura).

#### Editor di pagine {#page-editor}

* Consentire la modifica e la composizione nel contesto di esperienze di app a pagina singola build con componenti lato client React e Angular che utilizzano JS SDK (noto anche come editor SPA)
* La modalità scaffolding viene visualizzata solo se la pagina presenta una pagina di scaffolding configurata.

#### Frammenti di contenuto ed editor {#content-fragments-amp-editor}

* Nuova barra [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) nell&#39;Editor frammenti di contenuto per aggiungere commenti generali e visualizzare i commenti all&#39;interno del testo (viene visualizzata anche nella barra Timeline)
* Possibilità di impostare il tipo di contenuto predefinito di un elemento di testo su più righe in un [Modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) su testo semplice, testo RTF o markdown
* Aggiungi [commento/annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) selezionando il testo nell&#39;editor Rich Text (visualizzazione a schermo intero)
* [Confrontare le versioni](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) di un frammento di contenuto affiancate tramite la barra dei riferimenti
* Il rapporto Download risorse ora mostra di conseguenza i frammenti di contenuto
* Aggiungi il supporto per [Frammenti di contenuto all&#39;API HTTP di Assets](/help/assets/assets-api-content-fragments.md) tramite /api.json. Esistono API per creare, aggiornare, leggere ed eliminare frammenti di contenuto.

#### Frammenti di esperienza {#experience-fragments}

* È stata migliorata l&#39;indicizzazione di [Frammenti esperienza](/help/sites-authoring/experience-fragments.md), in modo che il loro contenuto venga trovato nella ricerca di pagine in cui vengono utilizzati.
* L&#39;opzione [Esporta in Target](/help/sites-administering/experience-fragments-target.md) ora consente di inviare il frammento di esperienza come JSON (l&#39;impostazione predefinita è HTML) o entrambi.

#### Traduzione {#translation}

* Semplifica la creazione di progetti di traduzione utilizzando i progetti principali.
* Per impostazione predefinita, semplifica l’esecuzione dei progetti di traduzione impostando i processi di traduzione sullo stato approvato.
* Consenti l’aggiornamento delle pagine tradotte con modifiche nella memoria di traduzione di terze parti.
* Consenti l’esportazione di processi di traduzione in formato JSON.
* Aggiornare l’integrazione di Microsoft® Translation per utilizzare l’API V3.

#### Gestione multisito (MSM) {#multi-site-management-msm}

* Per le configurazioni di rollout che utilizzano PushOnModify, è necessario gestire meglio le operazioni di spostamento della pagina per evitare stati incoerenti.
* La creazione di una pagina all’interno della struttura Live Copy crea una pagina indipendente per impostazione predefinita.
* Utilizzare le funzioni MSM nelle app a pagina singola che utilizzano JS SDK (detto anche editor SPA)

#### Lanci {#launches}

* Nuovo flusso di lavoro di revisione e approvazione per i lanci e possibilità di promuovere solo le pagine di lancio approvate
* È stata aggiunta l&#39;opzione [ nell&#39;interfaccia utente per scegliere di eliminare il lancio subito dopo il passaggio di promozione](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Targeting e simulazione dei contenuti {#content-targeting-simulation}

* Il livello dati ContextHub e il motore di regole lato client JavaScript è stato aggiornato per utilizzare jQuery 3 per impostazione predefinita.

#### AEM e ADOBE TARGET {#aem-amp-adobe-target}

>[!CAUTION]
>
>Attualmente:
>
>* Se utilizzi Adobe Target come motore di targeting all&#39;interno della console Attività di AEM, è supportato solo `at.js 1.x`.
>
>* Sia `at.js. 1.x` che `at.js 2.x` sono supportati se si utilizza l&#39;esportazione di frammenti di esperienza in Target e si eseguono attività all&#39;interno della console di Target.

* L’integrazione di Adobe Target ora utilizza l’API Target Standard. Le versioni precedenti di AEM utilizzano l’API HTTP di Target Classic, che ora è obsoleta.
* Adobe Target `mbox.js` versione 63 inclusa. Adobe consiglia vivamente di passare all&#39;implementazione `at.js` v1.x.
* `at.js` versione 1.5.0 è ora inclusa. Adobe consiglia di utilizzare [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) per eseguire il provisioning di `at.js` v1.x nel sito.

#### AEM e ADOBE ANALYTICS {#aem-amp-adobe-analytics}

* È incluso `s_code.js` H.27.5. Adobe consiglia di passare all&#39;implementazione in `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 è incluso. Adobe consiglia di utilizzare [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) per eseguire il provisioning di AppMeasurement.js nel sito.

#### AEM e COMMERCE {#aem-commerce}

I miglioramenti apportati a Commerce integration framework sono soggetti a un ciclo di rilascio più rapido da AEM 6.4. Ulteriori informazioni dall&#39;integrazione di [AEM e Adobe Commerce tramite Commerce integration framework](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html).

#### Componente aggiuntivo per community {#communities-add-on}

Per ottenere la versione più recente, consulta la sezione [Distribuzione delle community](/help/communities/deploy-communities.md) della documentazione.

##### Miglioramenti al coinvolgimento della community {#enhancements-to-community-engagement}

Supporto di **@Mentions**
AEM Communities ora consente agli utenti registrati di assegnare tag (menzioni) ad altri membri registrati per attirare la loro attenzione, nei Contenuti generati dagli utenti. I membri taggati (menzionati) vengono quindi notificati, con un collegamento diretto al corrispondente Contenuto generato dall&#39;utente. Tuttavia, gli utenti possono scegliere di disabilitare/abilitare le notifiche web ed e-mail.

![Al supporto menzioni](/help/release-notes/assets/at-mentions.png)

Gli utenti della community non devono cercare il proprio nome, cognome o nome utente per vedere se qualcuno ha contattato loro o ha bisogno della loro attenzione. Inoltre, consente agli autori UGC di richiedere una risposta a specifici utenti registrati che possono affrontare al meglio il problema e aggiungere input.

Gli amministratori della community devono **abilitare la menzione** sui componenti della community per consentire agli utenti registrati di utilizzare la funzionalità su tali componenti.

**Messaggistica di gruppo**

I membri della community registrati possono ora inviare messaggi diretti in blocco ai gruppi tramite una singola composizione e-mail, anziché inviare lo stesso messaggio singolarmente ai membri del gruppo. Per consentire la [messaggistica di gruppo](/help/communities/configure-messaging.md), abilitare entrambe le istanze di [Messaging Operations Service](/help/communities/messaging.md#group-messaging).

![Messaggio gruppo](/help/release-notes/assets/group-messaging.png)

##### Miglioramenti alla moderazione in blocco {#enhancements-to-bulk-moderation}

Filtri personalizzati nella moderazione in blocco

È ora possibile sviluppare e aggiungere [filtri personalizzati](/help/communities/moderation.md#custom-filters) all&#39;interfaccia utente per la moderazione in blocco.

Un [progetto di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) che dimostra il filtraggio tramite tag è disponibile in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Questo progetto può essere utilizzato come base per sviluppare filtri personalizzati analoghi.

![Filtri personalizzati](/help/release-notes/assets/custom-tag-filter.png)

**Visualizzazione elenco in moderazione collettiva**

È stata fornita una nuova vista a elenco con interfaccia utente migliorata in modalità di moderazione collettiva per visualizzare le voci di contenuto generato dagli utenti.

![Moderazione in blocco nella vista a elenco](/help/release-notes/assets/list-view-moderation.png)

##### Miglioramenti alla gestione di siti e gruppi {#enhancements-to-site-and-group-management}

**Amministratori di siti e gruppi lato autore**

Communities, AEM 6.5 e versioni successive, consente l’amministrazione decentrata (e la gestione) di diversi siti e gruppi della community/gruppi nidificati. Le organizzazioni che ospitano più siti community e gruppi nidificati possono ora selezionare i membri per i ruoli di amministratore sul lato Autore al momento della creazione del sito (e del gruppo).

![Amministratore sito](/help/release-notes/assets/site-admin.png)

Gli amministratori del sito possono creare un gruppo a qualsiasi livello gerarchico e diventare gli amministratori predefiniti. Questi amministratori possono essere successivamente rimossi da altri amministratori di gruppi. Gli amministratori di gruppi possono gestire il proprio gruppo G1 e creare un sottogruppo nidificato in G1.

##### Miglioramenti all’abilitazione {#enhancements-to-enablement}

Supporto di **SCORM 2017.1**

La funzionalità di abilitazione di AEM 6.5 Communities supporta il motore SCORM (Shared Content Object Reference Model) 2017.1[.](https://rusticisoftware.com/blog/scorm-engine-2017-released/)

* Supporto della navigazione tramite tastiera nei componenti di attivazione
* I componenti di abilitazione (ad esempio, Riproduzione di cataloghi e corsi, Assegnazioni, Libreria file) in AEM Communities supportano la navigazione da tastiera per migliorare l’accessibilità.

##### Altri miglioramenti {#other-enhancements}

* Supporto Solr 7
* Le community AEM 6.5 supportano la versione 7.0 di Apache Solr della piattaforma di ricerca durante la configurazione di MSRP e DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 introduce le seguenti funzionalità e miglioramenti per aumentare la produttività degli utenti AEM, i ruoli DAM e i ruoli creativi e di marketing associati.

#### Integrazione con [!DNL Adobe Creative Cloud] e flussi di lavoro creativi {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] offre diversi modi per integrarsi con [!DNL Adobe Creative Cloud] e condividere le risorse da utilizzare nei flussi di lavoro in cui i team creativi e di marketing o i team aziendali collaborano strettamente. [!DNL Experience Manager] 6.5 continua a migliorare l&#39;integrazione e la semplifica ulteriormente per esporre più opportunità e semplificare i metodi esistenti.

Continua a leggere per scoprire le funzionalità e le integrazioni specifiche di [!DNL Experience Manager] 6.5 che puoi utilizzare per supportare al meglio i tuoi casi di utilizzo di velocità dei contenuti.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] rafforza la collaborazione tra creativi e addetti al marketing nel processo di creazione dei contenuti. I creativi possono accedere ai contenuti archiviati in [!DNL Experience Manager Assets] senza uscire dalle app che hanno più familiarità con. I creativi possono sfogliare, cercare, estrarre e archiviare senza problemi le risorse tramite il pannello in-app nelle app [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign].

[!DNL Adobe Asset Link] fa parte dell&#39;offerta [Creative Cloud for enterprise](https://www.adobe.com/it/creativecloud/business/enterprise.html). Per ulteriori informazioni, inclusa la configurazione necessaria della distribuzione di [!DNL Experience Manager], vedi [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html).

![Cerca risorse in Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### Integrazione di [!DNL Adobe Stock] {#stock}

La tua organizzazione può utilizzare il piano aziendale [!DNL Adobe Stock] in [!DNL Experience Manager Assets] per garantire che le risorse concesse in licenza siano ampiamente disponibili per i progetti creativi e di marketing. Puoi trovare, visualizzare in anteprima e concedere in licenza [!DNL Adobe Stock] risorse salvate in Experience Manager utilizzando le potenti funzionalità DAM di [!DNL Experience Manager].

Il servizio [!DNL Adobe Stock] consente ai designer e alle aziende di accedere a milioni di foto, vettori, illustrazioni, video, modelli e risorse 3D di alta qualità e curate, senza royalty, per tutti i progetti creativi.

Per ulteriori informazioni, consulta [Utilizzare risorse Adobe Stock in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Anteprima immagine Adobe Stock e licenza da Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figura: Anteprima dell&#39;immagine [!DNL Adobe Stock] e licenza da [!DNL Experience Manager Assets].*

![Cerca e filtra le immagini Adobe Stock con licenza in Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Figura: cercare e filtrare le immagini [!DNL Adobe Stock] concesse in licenza in [!DNL Experience Manager].*

##### Riferimenti dinamici in [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] utilizzati in [!DNL Adobe InDesign] file sono dinamici. I riferimenti vengono aggiornati automaticamente se le risorse di riferimento si spostano nell’archivio. Per ulteriori informazioni, consulta [come gestire le risorse composte](/help/assets/managing-linked-subassets.md).

#### Funzionalità di Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] consente di acquisire, controllare e distribuire in modo semplice e sicuro le risorse approvate a fornitori/agenzie esterni e utenti aziendali interni su dispositivi diversi. Consente di migliorare l’efficienza della condivisione delle risorse, accelera il time-to-market delle risorse ed elimina il rischio di utilizzo non conforme e di accesso non autorizzato.

Per ulteriori informazioni, vedere [Novità di Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=it).

#### Risorse collegate {#connectedassets}

Nelle grandi aziende è possibile distribuire l&#39;infrastruttura necessaria per la creazione di siti Web. A volte, le funzionalità di creazione del sito web e le risorse digitali richieste risiedono in silos diversi.

[!DNL Experience Manager Sites] offre funzionalità per la creazione di pagine Web e [!DNL Experience Manager Assets] è il sistema di gestione delle risorse digitali (DAM) che fornisce le risorse necessarie per i siti Web. [!DNL Experience Manager] ora supporta il caso d&#39;uso precedente integrando [!DNL Sites] e [!DNL Assets]. Consulta [come configurare e utilizzare la funzionalità Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

![Trascina una risorsa da una distribuzione [!DNL Experience Manager] in una pagina [!DNL Sites] di una distribuzione [!DNL Experience Manager] diversa](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Figura: trascinare una risorsa da una distribuzione [!DNL Experience Manager] in una pagina [!DNL Sites] in una distribuzione [!DNL Experience Manager] diversa.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] offre funzioni avanzate di authoring e distribuzione di contenuti rich media in [!DNL Experience Manager Assets] per promuovere esperienze all&#39;avanguardia, coinvolgenti e personalizzate. Caricando una singola risorsa principale di alta qualità e utilizzando il rendering e i visualizzatori cloud avanzati di Adobe, puoi fornire al volo qualsiasi combinazione di rendering per supportare la strategia multimediale della tua organizzazione.

Per ulteriori dettagli sulle nuove funzionalità di [!DNL Dynamic Media], consulta [Note sulla versione di Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Supporto video 360 {#video-support}

Gestisci i tuoi file video 360 direttamente in [!DNL Experience Manager] utilizzando i visualizzatori all&#39;avanguardia per offrire esperienze VR a desktop, dispositivi mobili e cuffie VR. Per ulteriori informazioni, vedere [Utilizzo di video 360](/help/assets/360-video.md).

##### Miniature video personalizzate {#custom-video-thumbnails}

Ora puoi personalizzare le miniature delle risorse video utilizzando fotogrammi provenienti dal video stesso o altro contenuto memorizzato in DAM. Per ulteriori istruzioni, vedere [Informazioni sulle miniature video](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Miglioramenti all’accessibilità {#accessibility-enhancements}

[!DNL Dynamic Media] visualizzatori ora supportano funzioni di accessibilità avanzate come Aria-support, screen-reader e Alt-text. Per ulteriori dettagli, vedere [Guida di riferimento visualizzatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Miglioramento dell’esperienza di ricerca {#experience-enhancement-for-searching}

A partire da [!DNL Experience Manager] 6.5, gli addetti al marketing possono individuare più rapidamente le risorse desiderate dalla pagina dei risultati della ricerca. I facet di ricerca vengono aggiornati con il numero di risorse anche prima di applicare il filtro di ricerca. Visualizzare il conteggio previsto rispetto al filtro consente agli utenti di navigare tra i risultati della ricerca in modo efficiente. Per ulteriori informazioni, consulta [Cercare risorse in Experience Manager](/help/assets/search-assets.md).

![Visualizza il numero di risorse senza filtrare i risultati di ricerca nei facet di ricerca](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: visualizzare il numero di risorse senza filtrare i risultati della ricerca nei facet di ricerca.*

#### Miglioramento dell’usabilità {#usability-enhancement}

Ora puoi selezionare tutte le risorse caricate all’interno di una cartella o da un risultato di ricerca in un’unica operazione. Consente di gestire rapidamente più risorse. La casella di controllo seleziona tutte le risorse che rientrano nello scenario, ad esempio un risultato di ricerca, e non solo le risorse visibili nell&#39;interfaccia [!DNL Experience Manager].

![Utilizzare l&#39;opzione Seleziona tutto per selezionare tutte le risorse caricate con un solo clic.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Figura: utilizzare l&#39;opzione Seleziona tutto per selezionare tutte le risorse caricate con un solo clic.*

#### Miglioramenti ai metadati {#metadata-enhancements}

[!DNL Assets] consente di creare schemi di metadati per le cartelle di risorse, che definiscono il layout e i metadati visualizzati nelle pagine delle proprietà delle cartelle. Ora puoi assegnare uno schema di metadati di cartella a una cartella esistente o durante la creazione di una cartella. Per ulteriori informazioni, vedere [Schema metadati cartelle](/help/assets/metadata-config.md#folder-metadata-schema).

Quando si specificano i metadati a catena, le scelte possono essere caricate da un file JSON in fase di esecuzione, ad esempio invece di digitare manualmente nel modulo. Per ulteriori informazioni, vedere [metadati a catena](/help/assets/metadata-schemas.md#cascading-metadata).

#### Miglioramenti al reporting {#reporting-enhancements}

I frammenti di contenuto e le condivisioni di collegamenti sono ora inclusi nel rapporto scaricato. Per ulteriori informazioni, consulta [Rapporti di Assets](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms introduce diverse nuove funzioni e miglioramenti. Gli elementi di rilievo includono:

* Rapporti sulle transazioni per tenere traccia del numero di moduli inviati, documenti elaborati e documenti sottoposti a rendering
* Miglioramenti a livello di usabilità per le comunicazioni interattive
* Firme digitali basate su cloud nei moduli adattivi
* Incorpora moduli adattivi e comunicazioni interattive in un’applicazione a pagina singola (SPA) di AEM Sites.
* Supporto per le variabili nei flussi di lavoro di AEM
* Supporto dei pattern di visualizzazione dei dati nelle comunicazioni interattive
* Ordinamento dei moduli adattivi e delle tabelle di comunicazione interattive
* Convalida automatizzata dei dati di input nei modelli di dati dei moduli

Per informazioni sulle funzioni nuove e migliorate e sulle risorse della documentazione, consulta il [Riepilogo delle funzioni e dei miglioramenti introdotti in AEM 6.5 Forms](/help/forms/using/whats-new.md).

### Utilizzare lo sviluppo incentrato sul cliente {#use-customer-focused-development}

Adobe utilizza un modello di sviluppo incentrato sul cliente che consente ai clienti di contribuire a tutte le fasi del processo di sviluppo, durante le fasi di specifica, sviluppo e test. I nostri ringraziamenti vanno a tutti i clienti e partner che hanno contribuito a questo processo.

Adobe dispone delle procedure e dei processi necessari per abilitare la raccolta, la definizione delle priorità e il tracciamento della risoluzione dei bug incentrata sul cliente e lo sviluppo delle richieste di miglioramento. Il [portale di supporto Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&lang=it#support) è integrato con Adobe Enhancement and Defect Tracking System. Le domande dei clienti vengono identificate e risolte dal team di assistenza clienti, ove possibile. Quando vengono trasferiti a R&amp;D, tutte le informazioni sui clienti vengono acquisite e utilizzate a scopo di definizione delle priorità e reporting. La priorità è data nello sviluppo al supporto a pagamento, alle questioni di garanzia e ai miglioramenti pagati dal cliente.

Questo processo di definizione delle priorità ha prodotto più di 750 modifiche incentrate sui clienti, risolte in AEM 6.5.

## Elenco dei file che fanno parte della versione {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Quickstart autonomo: `cq-quickstart-6.5.0.jar`.
* Avvio rapido server applicazioni: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 o versione successiva per i vari server web e piattaforme. Vedi [collegamento download](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plug-in per Eclipse IDE ([ulteriori informazioni e download](/help/sites-developing/aem-eclipse.md))

* Estensione per l&#39;editor di codice Brackets ([leggi tutto e scarica](/help/sites-developing/aem-brackets.md))
* Dipendenze Maven/Gradle ([collegamento di download](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componenti core ([Progetto GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementazione del riferimento We.Retail ([ulteriori informazioni](/help/sites-developing/we-retail.md))
* Archetipi progetto Maven:

   * per siti full stack: [Progetto GitHub](https://github.com/adobe/aem-project-archetype)
   * per le app a pagina singola con React/Angular: [Progetto GitHub](https://github.com/adobe/aem-spa-project-archetype)

* Lettori AEM Screens per varie piattaforme di destinazione ([download](https://download.macromedia.com/screens/))

* Modelli linguistici per contenuti avanzati. L&#39;inglese è preinstallato - è possibile scaricare più lingue

   * [Tedesco](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Spagnolo](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francese](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* Suite di strumenti di modernizzazione AEM, ad esempio Strumento di conversione delle finestre di dialogo. ([Progetto GitHub](https://github.com/adobe/aem-modernize-tools))

**Risorse**

* Pacchetto per l&#39;aggiunta di PDF Rasterizer avanzato ([ulteriori informazioni](/help/assets/aem-pdf-rasterizer.md))
* Pacchetto per aggiungere il supporto esteso per le immagini RAW ([ulteriori informazioni](/help/assets/camera-raw.md))

**Moduli**

* [Pacchetti per funzionalità AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [SDK client AEM Forms OSGi](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Lingue {#languages}

L’interfaccia utente è disponibile nelle seguenti lingue:

* Inglese
* Tedesco
* Francese
* Spagnolo
* Italiano
* Portoghese brasiliano
* Giapponese
* Cinese semplificato
* Cinese tradizionale (supporto limitato)
* Coreano

[!DNL Experience Manager] 6.5 è stato certificato per GB18030-2005 CITS per l&#39;utilizzo dello standard di codifica cinese.

## Installare e aggiornare {#install-update}

Per i requisiti di configurazione, consulta [Istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

Per istruzioni dettagliate, consulta [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md).

## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto, sui [requisiti tecnici di AEM 6.5](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle è passato a un modello LTS (Long Term Support) per i prodotti Oracle Java™ SE. Java™ 9 e 10 non sono versioni LTS di Oracle. Consulta la roadmap del supporto di [Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe supporta le versioni LTS di Java™ per eseguire AEM solo in produzione. Java™ 11 è la versione consigliata per AEM 6.5.

## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità del prodotto e nel tempo pianifica la sostituzione delle funzionalità con versioni più potenti, oppure decide di reimplementare parti selezionate per prepararsi meglio ad aspettative o estensioni future.

Per [!DNL Adobe Experience Manager] 6.5, [leggere l&#39;elenco delle funzionalità obsolete e rimosse](/help/release-notes/deprecated-removed-features.md). La pagina contiene anche un preannuncio delle modifiche in arrivo in futuro e un avviso importante per i clienti che eseguono un aggiornamento dalle versioni precedenti.

## Problemi noti {#known-issues}

### Platform {#platform}

* Viene segnalato un problema che comporta l’eliminazione di CRX-Quickstart e del relativo contenuto.

  In ognuna di queste azioni, verificare che la proprietà `htmllibmanager.fileSystemOutputCacheLocation` non sia una stringa vuota:

   1. Chiamata di `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Aggiornamento ad AEM 6.5.
   3. Esecuzione della &quot;migrazione lenta dei contenuti&quot; su AEM 6.5.

* Se utilizzi JDK 11 con l’istanza AEM 6.5, alcune pagine potrebbero risultare vuote dopo la distribuzione di alcuni pacchetti. Nel file di registro viene visualizzato il seguente messaggio di errore:

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

Per risolvere l&#39;errore:

1. Arresta l’istanza di AEM. Vai a `<aem_server_path_on_server>crx-quickstart\conf` e apri il file `sling.properties`. Adobe consiglia di eseguire un backup del file.

1. Cerca `org.osgi.framework.bootdelegation=`. Aggiungi `jdk.internal.reflect,jdk.internal.reflect.*` proprietà per visualizzare il risultato come.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Salva il file e riavvia l’istanza di AEM.

### Sites {#sites}

* **Utilizzo delle versioni delle pagine**: [Se una pagina è stata spostata, non è più possibile eseguire un&#39;anteprima sulle versioni create prima dello spostamento](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Risorse {#assets}

* **Ricerca:** La ricerca non restituisce alcun risultato se la stringa di ricerca contiene spazi iniziali ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schema metadati cartelle**: dopo aver aggiunto un pulsante di scelta, i campi ID e Valore non vengono visualizzati come previsto e la funzionalità di eliminazione non funziona. (CQ-4261144)
* Quando si rinomina una risorsa, non è possibile usare uno spazio vuoto nel nome della risorsa. (CQ-4266403)

### Forms {#forms}

* Quando AEM Forms è installato su un sistema operativo Linux®, il modulo di protezione Firma digitale con hardware non funziona. (CQ-4266721)
* (Solo AEM Forms su WebSphere®) L&#39;opzione **Forms Workflow** > **Ricerca attività** non restituisce alcun risultato se si cerca un **Amministratore** con **Nome utente** come criterio di ricerca. (CQ-4266457)

* AEM Forms non riesce a convertire i file TIF e TIFF con compressione JPEG in documenti PDF. (CQ-4265972)
* Le opzioni **AEM Forms Assets Scanner** e **Letter to Interactive Communication Migration** non funzionano nella pagina **AEM Forms Migration**. (CQ-4266572)

* (Solo JBoss® 7) Quando si esegue l’aggiornamento da una versione precedente a AEM 6.5 Forms e la versione precedente disponeva di processi (.lca) che creavano e utilizzavano una copia del processo di invio o di rendering predefinito, HTML5 Forms che utilizzava tali processi (.lca) non riesce a eseguire le azioni richieste. (CQ-4243928)
* In un modulo adattivo da, quando un servizio del modello dati modulo viene richiamato dall’editor di regole per aggiornare dinamicamente i valori del componente di scelta immagine, i valori del componente di scelta immagine non vengono aggiornati. (CQ-4254754)
* Il programma di installazione di AEM Forms Designer richiede la versione a 32 bit di [pacchetti runtime ridistribuibili Visual C++ 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) e [pacchetti runtime ridistribuibili Visual C++ 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). Prima di avviare l’installazione, assicurati che siano installati i pacchetti runtime ridistribuibili precedentemente menzionati. (CQ-4265668)

* PDF Generator non supporta l&#39;autenticazione basata su smart card. Quando un amministratore abilita i Criteri di gruppo `Interactive Logon: Require Smart card` in un server Windows, tutti gli utenti PDF Generator esistenti vengono invalidati.

* Quando un modulo adattivo è configurato per aggiornare dinamicamente i valori di un componente e l’istanza Publish che ospita il modulo è accessibile tramite Dispatcher, la funzionalità per aggiornare dinamicamente i valori di un campo smette di funzionare. Per risolvere il problema, nell&#39;istanza di pubblicazione aprire CRXDE, passare a `/libs/fd/af/runtime/clientlibs/guideChartReducer` e creare la proprietà elencata di seguito.

   * Nome: allowProxy
   * Tipo: booleano
   * Valore: true
   * Protetto: False
   * Obbligatorio: False
   * Multiplo: False
   * Creazione automatica: False

  La proprietà consente alle librerie client nella cartella runtime di accedere ai proxy. (CQ-4268679)

* All&#39;avvio di AEM Forms viene visualizzato l&#39;avviso `SAX Security Manager could not be setup`.
* Quando apri un PDF protetto con AEM Forms Document Security su un Apple iOS o iPadOS con versione 20.10.00 di Adobe Acrobat Reader
* Quando invii un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file da 0 byte. Apple iOS 15.1 fornisce una correzione per il problema.

## Download e supporto dei prodotti (siti con restrizioni) {#product-download-and-support-restricted-sites}

I seguenti siti sono disponibili solo per i clienti. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Download del prodotto in licensing.adobe.com](https://licensing.adobe.com/).

* Aggiornamenti dei prodotti, patch e pacchetti per funzionalità aggiuntive in [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).

* [Assistenza clienti tramite Admin Console](https://adminconsole.adobe.com/). Per ulteriori informazioni, consulta [Nuova esperienza di assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).
