---
title: Note generali sulla versione per [!DNL Adobe Experience Manager] 6.5
description: '[!DNL Adobe Experience Manager]Le note per 6.5 contengono informazioni sulla versione, novità, modalità di installazione ed elenchi dettagliati delle modifiche.'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: f8fcfa9e09167cd4dbaafe938bcbe3ee6ece270f
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 65%

---

# Note generali sulla versione per [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] |
|---|---|
| Versione | 6.5 |
| Tipo | Versione principale |
| Data di disponibilità generale | 8 aprile 2019 |
| Aggiornamenti consigliati | Consulta [AEM aggiornamenti recenti](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it). |

### Informazioni varie {#trivia}

Il ciclo di rilascio di questa versione di [!DNL Adobe Experience Manager] è iniziato il 4 aprile 2018 ed è terminato il 28 marzo 2019 passando attraverso 23 fasi di controllo della qualità e risoluzione dei bug. Il numero complessivo di errori relativi ai clienti risolti in questa versione con miglioramenti e aggiunta di nuove funzioni è pari a 1345. 

[!DNL Adobe Experience Manager] La versione 6.5 è generalmente disponibile dall’8 aprile 2019.

![Schermata di accesso di AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novità {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 è una versione di aggiornamento della codebase  [!DNL Adobe Experience Manager] 6.4. Fornisce funzionalità nuove e migliorate, importanti correzioni di casi segnalati dai clienti, miglioramenti con priorità alta e correzioni di bug generali per migliorare la stabilità del prodotto. Include inoltre [!DNL Adobe Experience Manager] 6.4 Service Pack fino a SP4.

L’elenco seguente fornisce una panoramica, mentre nelle pagine successive sono riportati tutti i dettagli.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

Elenco completo delle modifiche apportate in [AEM Foundation](/help/release-notes/wcm-platform.md).

La piattaforma di [!DNL Adobe Experience Manager] 6.5 si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e del Java Content Repository: Apache Jackrabbit Oak 1.10.2.

Quickstart utilizza Eclipse Jetty 9.4.15 come motore servlet.

#### Supporto per Java  {#java-support}

* Nuovo supporto per Java 11, che si aggiunge alla versione già supportata di Java 8.
* Per prestazioni ottimali, sovrascrivi i valori GC predefiniti con altri valori. Per ulteriori informazioni, consulta la sezione [installare e aggiornare](/help/sites-deploying/custom-standalone-install.md) .
* Gli aggiornamenti di manutenzione per Java 11 e Java 8 sono distribuiti per Adobe per l’utilizzo da parte dei clienti nei progetti relativi AEM, quando non sono disponibili al pubblico in Oracle.

#### Sviluppo per Java {#java-development}

* Sono ora disponibili [due versioni di Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), una versione consigliata con interfacce pubbliche non contrassegnate per elementi obsoleti e una versione che include le interfacce contrassegnate per elementi obsoleti.

#### Interfaccia utente {#user-interface}

Sono stati apportati vari miglioramenti all’interfaccia utente per renderla più produttiva e facile da usare.

* Nuova interfaccia utente per la gestione delle autorizzazioni per utenti e gruppi.
* La vista a colonne ora carica solo le voci che sono visibili sullo schermo e ne carica altre solo quando l’utente inizia a scorrere. Questa funzione era già disponibile nelle viste a elenco e a schede dalla versione 6.0 (migliorata in 6.4).
* La vista a colonna ora include lo stato del flusso di lavoro per le pagine/risorse, se applicabile.
* L’azione [Seleziona tutto](/help/sites-authoring/basic-handling.md#select-all) permette di eseguire rapidamente un’azione su tutte le pagine/risorse nella stessa cartella.
* L’azione [Seleziona tutto](/help/sites-authoring/basic-handling.md#select-all) tenta di eseguire l’azione su tutte le pagine/risorse, non solo sugli elementi caricati. Se l’azione non viene aggiornata per gestire le azioni collettive, viene visualizzata una finestra di dialogo di avviso.

>[!CAUTION]
>
>Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia utente classica. In AEM 6.5 è già inclusa l’interfaccia utente classica e i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a usarla normalmente. L’interfaccia classica rimane completamente supportata anche se obsoleta. [Ulteriori informazioni](/help/sites-deploying/ui-recommendations.md).

#### Ricerca e indicizzazione {#indexing-and-search}

* La ricerca in Oak supporta ora i facet dinamici. Ad esempio, la barra del filtro nella ricerca delle risorse mostra la quantità stimata di risultati.
* QueryBuilder è stato esteso per fornire risultati con facet dinamici.

#### Aggiornamento {#upgrade}

* L’aggiornamento diretto locale ad AEM 6.5 è supportato per i clienti che eseguono AEM 6.2, 6.3 e 6.4. I clienti che eseguono 5.x o 6.0/6.1 e che desiderano utilizzare l’aggiornamento locale devono prima eseguire l’aggiornamento a 6.4 e successivamente a 6.5 oppure effettuare l’aggiornamento tramite il trasferimento del contenuto tra le istanze direttamente ad AEM 6.5.

#### Progetti e flussi di lavoro {#projects-and-workflows}

* Il nuovo editor per modelli di flusso di lavoro introdotto nella versione 6.4 è stato migliorato per includere più operazioni come copia e pubblicazione, supporto delle variabili nei passaggi del flusso di lavoro e miglioramento delle suddivisioni OR e AND.

### [!DNL Experience Manager] Sites {#experience-manager-sites}

Elenco completo delle modifiche in [AEM Sites e componenti aggiuntivi](/help/release-notes/sites.md).

#### Applicazioni a pagina singola gestite {#managed-single-page-apps}

L’Editor pagina aggiunge la possibilità di modificare contestualmente i contenuti e di comporre/impostare il layout all’interno di esperienze di rendering lato client (noto anche come [Editor SPA](/help/sites-developing/spa-architecture.md)). Le applicazioni a pagina singola esistenti create con framework JavaScript React o Angular possono essere estese con l’SDK di AEM SJ per essere rese modificabili dai professionisti.

Fornito inizialmente come componente di AEM 6.4 SP2, con AEM 6.5 il supporto SPA offre le seguenti funzionalità:

* Utilizzo dell’Editor modelli per modificare e configurare le parti modificabili AEM di SPA
* Utilizzo della gestione multisito per creare esperienze SPA regionali, in franchising o con rebranding

#### Gestione dei contenuti headless {#headless-content-management}

AEM consente di gestire i contenuti in vari formati e da diversi livelli dello stack. Alcuni sono in giro dal 2008 con [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) e [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([Sling Model Exporter](https://docs.adobe.com/content/help/it-IT/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)) è stato introdotto in AEM 6.3 ed è il metodo utilizzato dall’SDK AEM SJ per idratare applicazioni a pagina singola. Le [API HTTP per Assets](/help/assets/mac-api-assets.md) sono API CRUD, estese ad AEM 6.5.

Nuove funzionalità API HTTP:

* È stato aggiunto il [supporto dei frammenti di contenuto alle API HTTP per Assets](/help/assets/assets-api-content-fragments.md) per creare, aggiornare, leggere ed eliminare i frammenti.
* È possibile esporre elenchi di frammenti di contenuto tramite Content Services con il [componente core per elenco dei frammenti di contenuto](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Libreria di componenti core](https://opensource.adobe.com/aem-core-wcm-components/library.html), che mostra l’output JSON di default di Content Services per ogni componente

#### Add-on Screens {#screens-add-on}

Consente di progettare, fornire e ottimizzare in modo efficiente le esperienze su tutti i display digitali, dai chioschi interattivi alla segnaletica digitale.

**Design**

* Unione di esperienze e contenuti per canali digitali e in-store con un migliore riutilizzo dei contenuti
* Flussi di lavoro ottimizzati per l’authoring e l’approvazione/pubblicazione con supporto per i lanci
* Possibilità di modificare e fornire esperienze interattive avanzate utilizzando l’Editor SPA

**Consegna**

* Supporto esteso per lettori multimediali con prestazioni online e offline affidabili (sincronizzazione avanzata) in grado di adattarsi alle reti di segnaletica più grandi.

**Ottimizzazione**

* Personalizzazione in base alla posizione o alla configurazione dei dati generati dai contenuti utilizzando segnaposto dinamici.
* Informazioni unificate in base all’integrazione di Adobe Analytics in AEM Screens Player

Per ulteriori dettagli sulle modifiche ad AEM Screens, consulta le Note sulla versione nella [Guida utente di AEM Screens](https://docs.adobe.com/content/help/it/experience-manager-screens/user-guide/aem-screens-introduction.html).

### [!DNL Experience Manager Assets] {#experience-manager-assets}

Elenco completo delle modifiche nelle [AEM note sulla versione 6.5 Assets](/help/release-notes/assets.md).

AEM 6.5 introduce le seguenti funzionalità e miglioramenti per incrementare la produttività degli utenti AEM, dei ruoli DAM e dei ruoli creativi e di marketing associati.

#### Integrazione in Adobe Creative Cloud {#integration-with-adobe-creative-cloud}

Introduzione ad [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html), un’esperienza in-app per gli utenti creativi che lavorano su applicazioni Adobe Creative Cloud, tra cui Photoshop, Illustrator e InDesign, per semplificare la collaborazione tra creativi e addetti al marketing nel processo di creazione dei contenuti. AEM’app desktop continua a supportare le esigenze degli utenti che utilizzano risorse da AEM sul desktop, utilizzando qualsiasi tipo di file e qualsiasi applicazione desktop.

Inoltre, AEM si integra con Adobe Stock per trovare, visualizzare in anteprima, concedere in licenza e salvare le risorse Adobe Stock direttamente dall’interfaccia utente di AEM Web.

![Pannello Collegamento risorsa in Photoshop](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Risorse collegate {#connected-assets}

La funzionalità Risorse collegate è destinata a implementazioni più grandi con una serie di implementazioni AEM Sites che devono sfruttare le risorse da una distribuzione AEM Assets DAM centrale. Consente di migliorare la governance intorno alle risorse gestite a livello centrale, consentendo al tempo stesso un’elevata efficienza nella fornitura di risorse alle varie implementazioni di Sites.

### Dynamic Media {#dynamic-media}

Dynamic Media fornisce funzionalità avanzate per l’authoring e la distribuzione di contenuti multimediali in AEM Assets per offrire esperienze all’avanguardia, coinvolgenti e personalizzate. Con un’unica risorsa principale di alta qualità, è possibile sfruttare le funzionalità avanzate di rendering cloud, Ritaglio avanzato, e i migliori visualizzatori del settore per offrire le esperienze più coinvolgenti con prestazioni leader del settore.

Le nuove funzioni includono:

* Supporto per video a 360° e visore VR
* Miniature video personalizzate
* Supporto migliorato per l’accessibilità
* Protezione hot-linking

#### Esperienza utente e ricerca {#user-experience-and-search}

I miglioramenti chiave consentono di trovare più rapidamente le risorse giuste grazie alla possibilità di eseguire ricerche dinamiche e di gestire più risorse in modo più efficiente grazie alla possibilità di selezionare tutte le risorse da qualsiasi cartella o risultato di ricerca.

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms offre diverse nuove funzioni e miglioramenti. Le caratteristiche principali sono:

* Rapporti delle transazioni per tenere traccia del numero di moduli inviati, documenti elaborati e documenti di cui è stato eseguito il rendering
* Miglioramenti a livello di usabilità per le comunicazioni interattive
* Firme digitali basate su cloud nei moduli adattivi
* Incorporazione dei moduli adattivi e comunicazioni interattive nelle applicazioni a pagina singola (SPA) di AEM Sites.
* Supporto delle variabili nei flussi di lavoro AEM
* Supporto dei pattern di visualizzazione dei dati nelle comunicazioni interattive
* Ordinamento di moduli adattivi e tabelle di comunicazione interattive
* Convalida automatica dei dati di input nei modelli di dati per moduli

Per informazioni sulle funzioni nuove e migliorate e sulle risorse della documentazione, consulta il [Riepilogo delle nuove funzioni e dei miglioramenti in AEM 6.5 Forms](/help/forms/using/whats-new.md) .

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

AEM 6.5 aggiunge nuove funzioni e miglioramenti a Communities. Le caratteristiche principali di questa versione sono:

* Menzione dei membri registrati (@menzione) supportata durante l’authoring di contenuti generati dagli utenti.
* Supporto della messaggistica in blocco diretta a gruppi di membri.
* Filtri personalizzati sviluppati e aggiunti all’interfaccia utente di moderazione di gruppo. Un [progetto di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) che dimostra che il filtraggio per tag può essere utilizzato come base per sviluppare filtri personalizzati analoghi.
* Nuova vista a elenco con interfaccia utente migliorata per la moderazione di gruppo.
* È possibile assegnare amministratori separati ai diversi siti della community e gruppi nidificati, invece di un singolo amministratore della comunità.
* La funzionalità di abilitazione di AEM 6.5 Communities supporta il motore [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .
* Supporto per la navigazione da tastiera su componenti di abilitazione per una migliore accessibilità.
* Apache Solr 7.0 supportato durante la configurazione di MSRP e DSRP.

Per un elenco dettagliato delle modifiche, consulta le [AEM note sulla versione 6.5 Communities](/help/release-notes/communities-release-notes.md).

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Puoi integrare Livefyre con l’istanza di AEM 6.5. Scopri [come integrare Livefyre con AEM](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html).

### Sfruttare lo sviluppo mirato ai clienti {#leverage-customer-focused-development}

Adobe utilizza un modello di sviluppo incentrato sul cliente che consente ai clienti di contribuire a tutte le fasi del processo di sviluppo, per le specifiche, lo sviluppo e il testing. Il nostro ringraziamento va a tutti i clienti e partner che hanno contribuito a questo processo.

Adobe dispone delle procedure e dei processi necessari a consentire la raccolta, la definizione delle priorità e il monitoraggio della risoluzione dei bug incentrati sul cliente e dello sviluppo delle richieste di miglioramento. Il [portale di supporto Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) è integrato con il sistema di monitoraggio dei miglioramenti e dei difetti di Adobe. Le domande dei clienti vengono identificate e risolte dal team di assistenza clienti, ove possibile. Quando è necessario passarle al reparto R&amp;D, tutte le informazioni sui clienti vengono acquisite e utilizzate per stabilire le priorità e a scopo di reportistica. Nello sviluppo viene data la priorità al supporto a pagamento, ai problemi di garanzia e ai miglioramenti pagati dal cliente.

Grazie a questo processo di prioritizzazione, in AEM 6.5 sono stati risolti oltre 750 cambiamenti incentrati sul cliente.

## Elenco dei file che fanno parte della versione {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Quickstart indipendente: `cq-quickstart-6.5.0.jar`.
* Avvio rapido server applicazioni: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 o versioni successive per i vari server web e piattaforme. Vedi [collegamento per il download](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plug-in per Eclipse IDE ([informazioni e download](/help/sites-developing/aem-eclipse.md))

* Estensione per l’Editor di codice con parentesi ([informazioni e download](/help/sites-developing/aem-brackets.md))
* Dipendenze Maven/Gradle ([collegamento di download](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componenti core ([progetto GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementazione di riferimento We.Retail ([informazioni](/help/sites-developing/we-retail.md))
* Archetipi di progetto Maven:

   * per siti full-stack: [progetto GitHub](https://github.com/adobe/aem-project-archetype)
   * per applicazioni a pagina singola con React/Angular: [progetto GitHub](https://github.com/adobe/aem-spa-project-archetype)

* Lettori AEM Screens per varie piattaforme di destinazione ([download](https://download.macromedia.com/screens/))

* Modelli lingua per contenuti avanzati. L’inglese è preinstallato, è possibile scaricare altre lingue

   * [Tedesco](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Spagnolo](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francese](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernize Tools Suite, ad esempio lo strumento di conversione delle finestre di dialogo. ([Progetto GitHub](https://github.com/adobe/aem-modernize-tools))

**Assets**

* Pacchetto per aggiungere PDF Rasterizer migliorato ([ulteriori informazioni](/help/assets/aem-pdf-rasterizer.md))
* Pacchetto per aggiungere il supporto esteso per le immagini RAW ([ulteriori informazioni](/help/assets/camera-raw.md))

**Forms**

* [Pacchetti per le funzionalità di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [SDK client OSGi di AEM Forms](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

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

[!DNL Experience Manager] 6.5 è stato certificato per GB18030-2005 CITS per l’utilizzo dello standard di codifica cinese.

## Installazione e aggiornamento {#install-update}

Per i requisiti di configurazione, consulta [istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

Per istruzioni dettagliate, consulta la [documentazione di aggiornamento](/help/sites-deploying/upgrade.md).

## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto, su [AEM 6.5 requisiti tecnici](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle è stato spostato in un modello di supporto a lungo termine (LTS) per i prodotti Java SE di Oracle. Java 9 e 10 sono versioni non LTS per Oracle. Consulta la [roadmap del supporto Java SE di Oracle](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe fornisce il supporto per le versioni LTS di Java per l’esecuzione di AEM solo in produzione. Java 11 è la versione consigliata da utilizzare con AEM 6.5.

## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità del prodotto e, nel tempo, pianifica di sostituire le funzionalità con versioni più potenti, oppure decide di reimplementare specifiche parti per una migliore preparazione a eventuali estensioni future.

Per [!DNL Adobe Experience Manager] 6.5, [leggi l&#39;elenco delle funzionalità obsolete e rimosse](/help/release-notes/deprecated-removed-features.md). La pagina contiene anche il preannuncio di modifiche che verranno implementate prossimamente e un avviso importante per i clienti che eseguono l’aggiornamento da versioni precedenti.

## Problemi noti {#known-issues}

[Elenco dei problemi noti](/help/release-notes/known-issues.md)

### Download e supporto del prodotto (siti con limitazioni) {#product-download-and-support-restricted-sites}

I seguenti siti sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/).

* Aggiornamenti dei prodotti, patch e pacchetti per funzionalità aggiuntive su [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).

* [Assistenza clienti tramite Admin Console](https://adminconsole.adobe.com/). Per ulteriori informazioni, consulta [Nuovo Adobe sull’esperienza di accesso all’Assistenza clienti](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
