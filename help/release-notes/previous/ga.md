---
title: Note generali sulla versione di [!DNL Adobe Experience Manager] 6,5
description: "[!DNL Adobe Experience Manager] Note 6.5 che descrivono le informazioni sulla versione, le novità, le modalità di installazione e gli elenchi dettagliati delle modifiche."
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '4675'
ht-degree: 5%

---

# Note generali sulla versione di [!DNL Adobe Experience Manager] 6,5{#general-release-notes-for-adobe-experience-manager}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] |
|---|---|
| Versione | 6.5 |
| Tipo | Versione principale |
| Data di disponibilità generale | 8 aprile 2019 |
| Aggiornamenti consigliati | Vedi [Aggiornamenti AEM recenti](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=en). |

### Trivia {#trivia}

Ciclo di rilascio per questa versione di [!DNL Adobe Experience Manager] iniziato il 4 aprile 2018, ha superato 23 fasi di controllo della qualità e correzione di bug, ed è terminato il 28 marzo 2019. Il numero totale di problemi relativi ai clienti risolti in questa versione con miglioramenti e nuove funzioni è pari a 1345.

[!DNL Adobe Experience Manager] La versione 6.5 è generalmente disponibile dall’8 aprile 2019.

![Schermata di accesso di AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novità {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 è una versione di aggiornamento di [!DNL Adobe Experience Manager] 6.4 codice base. Fornisce funzionalità nuove e migliorate, correzioni di problemi fondamentali per i clienti, miglioramenti dei clienti ad alta priorità e correzioni di bug generali orientati alla stabilizzazione del prodotto. Include inoltre [!DNL Adobe Experience Manager] 6.4 Service Pack rilascia fino a SP4.

L’elenco seguente fornisce una panoramica, mentre nelle pagine successive sono riportati tutti i dettagli.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 versione aggiornata del framework basato su OSGi (Apache Sling e Apache Felix) e del Java™ Content Repository: Apache Jackrabbit Oak 1.10.2.

Quickstart utilizza Eclipse Jetty 9.4.15 come motore servlet.

#### Supporto Java™  {#java-support}

* Nuovo supporto per Java™ 11 e Java™ 8 già supportato.
* Per prestazioni ottimali, sovrascrivi i valori GC predefiniti con altri valori. Per ulteriori informazioni, consulta la sezione [installare e aggiornare](/help/sites-deploying/custom-standalone-install.md) sezione .
* Gli aggiornamenti di manutenzione per Java™ 11 e Java™ 8 sono distribuiti per Adobe per l&#39;utilizzo da parte del cliente nei progetti relativi alla AEM, quando non sono disponibili pubblicamente dall&#39;Oracle.

#### Sviluppo Java™ {#java-development}

* Ci sono ora [due versioni di Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), una versione consigliata con interfacce pubbliche non contrassegnate per elementi obsoleti e una versione che include interfacce contrassegnate per elementi obsoleti.

#### Interfaccia utente {#user-interface}

Sono stati apportati diversi miglioramenti all’interfaccia utente per renderla più produttiva e facile da usare.

* Nuova interfaccia utente per la gestione delle autorizzazioni per utenti e gruppi.
* Le visualizzazioni a colonne ora caricano solo le voci visibili sullo schermo e ne caricano altre solo quando l’utente inizia a scorrere. La vista a elenco e a schede lo ha già fatto a partire dalla versione 6.0 (migliorata in 6.4).
* Le visualizzazioni a colonne ora includono lo stato del flusso di lavoro per le pagine/risorse, se applicabile.
* La [Seleziona tutto](/help/sites-authoring/basic-handling.md#select-all) è un modo rapido per eseguire un’azione con tutte le pagine/risorse presenti nella stessa cartella.
* La [Seleziona tutto](/help/sites-authoring/basic-handling.md#select-all) tenta di eseguire l’azione su tutte le pagine/risorse, non solo su ciò che è stato caricato. Se l’azione non viene aggiornata per gestire le azioni collettive, viene visualizzata una finestra di dialogo di avviso.

>[!CAUTION]
>
>Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia utente classica. AEM 6.5 include l’interfaccia classica e i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a usarla così com’è. L’interfaccia classica rimane completamente supportata anche se obsoleta. [Leggi tutto](/help/sites-deploying/ui-recommendations.md).

#### Ricerca e indicizzazione {#indexing-and-search}

* La ricerca in Oak ora supporta i facet dinamici. Ad esempio, la barra del filtro nella ricerca delle risorse mostra il numero stimato di risultati.
* QueryBuilder è stato esteso per fornire risultati con facet dinamici.

#### Aggiornamento {#upgrade}

* L’aggiornamento diretto in-place a AEM 6.5 è supportato per i clienti che eseguono AEM 6.2, 6.3 e 6.4. I clienti che utilizzano 5.x o 6.0/6.1 e desiderano utilizzare l’aggiornamento locale devono prima effettuare l’aggiornamento a 6.4. Quindi, effettua l’aggiornamento alla versione 6.5 o effettua l’aggiornamento tramite il trasferimento del contenuto tra le istanze direttamente a AEM 6.5.
* La procedura di aggiornamento rimane sostanzialmente la stessa nella versione 6.5.
* Continuiamo a supportare le funzioni di Compatibilità con le versioni precedenti , Valutazione della complessità dell’aggiornamento e Aggiornamenti sostenibili introdotte nella versione 6.4. Sono stati apportati aggiornamenti specifici alle versioni, se necessario.
* Il pacchetto del rilevatore pattern è ora semplificato. Esiste un pacchetto che valuta gli aggiornamenti a 6.5 per le versioni sorgente disponibili.
* Per informazioni dettagliate sulla procedura di aggiornamento, consulta la sezione [documentazione di aggiornamento](/help/sites-deploying/upgrade.md).

#### Progetti e flussi di lavoro {#projects-and-workflows}

* Il nuovo editor per modelli di flusso di lavoro introdotto nella versione 6.4 è stato migliorato per includere più operazioni come copia e pubblicazione, supporto delle variabili nei passaggi del flusso di lavoro e migliorato `OR` e `AND` spaccature.

#### Archivio {#repository}

* Le basi di Adobe Experience Manager 6.5 si basano sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e del Java™ Content Repository: Apache Jackrabbit Oak 1.10.2.
* Per una panoramica dei problemi risolti, vedi [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) e [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nuova versione di Oak Segment Tar, presente dal AEM 6.3, richiede una migrazione dell&#39;archivio. Questo passaggio è obbligatorio se effettui l’aggiornamento da una versione precedente di TarMK o desideri cambiare il nuovo Segment Tar da un altro tipo di persistenza. Per ulteriori informazioni sui vantaggi del nuovo Segment Tar, consulta la sezione [Domande frequenti sulla migrazione a Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Sono state aggiunte le librerie di utility OSGi Promises e Converter.

#### Sicurezza {#security}

* È stata aggiunta la scadenza della password per l’utente amministratore.

#### Server web {#web-server}

* La distribuzione Quickstart utilizza Eclipse Jetty 9.4.15 come motore servlet (AEM 6.4 fornito con 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### App gestite a pagina singola {#managed-single-page-apps}

L’Editor pagina aggiunge la possibilità di modificare contenuti contestuali e comporre/impostare il layout all’interno di esperienze di rendering lato client (anche noto [come editor SPA](/help/sites-developing/spa-architecture.md)). Le app a pagina singola esistenti create con framework JavaScript React o Angular possono essere estese con l&#39;SDK SJ AEM per essere rese modificabili dai professionisti.

Fornito inizialmente come parte di AEM 6.4 SP2, con AEM 6.5 il supporto SPA offre le seguenti funzionalità:

* Utilizza l’Editor modelli per modificare e configurare le AEM parti modificabili del SPA
* Utilizza la gestione multisito per creare esperienze SPA con etichetta nazionale, franchising o bianca

#### Gestione dei contenuti headless {#headless-content-management}

AEM il contenuto può essere distribuito in vari formati e da vari livelli dello stack. Alcuni sono in giro dal 2008 con [GET Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) e [Servlet POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([Esportatore di modelli Sling](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en)) è stato introdotto in AEM 6.3 ed è il metodo utilizzato dall’SDK SJ AEM per idratare le app a pagina singola. La [API HTTP per Assets](/help/assets/mac-api-assets.md) è un’API CRUD, che è stata estesa per AEM 6.5.

Nuove funzionalità API HTTP:

* Aggiunto [Supporto dei frammenti di contenuto per le API HTTP per le risorse](/help/assets/assets-api-content-fragments.md) per creare, aggiornare, leggere ed eliminare frammenti.
* Esporre elenchi di frammenti di contenuto tramite Content Services con [Componente core dell’elenco dei frammenti di contenuto](https://www.aemcomponents.dev).
* [Libreria dei componenti core](https://www.aemcomponents.dev) che mostra l’output JSON predefinito di Content Services per ogni componente

#### Add-on Screens {#screens-add-on}

Progettare, distribuire e ottimizzare in modo efficiente le esperienze su tutti i display digitali, dai chioschi interattivi al digital signage.

* Unificare esperienze e contenuti digitali e in-store con un migliore riutilizzo dei contenuti
* Flussi di lavoro ottimizzati per l’authoring e l’approvazione/pubblicazione con supporto per i lanci
* Modificare e fornire esperienze interattive avanzate utilizzando l’editor SPA
* Utilizzo di Lanci per pianificare future modifiche ai contenuti di segnaletica
* Riproduzione controllata in un canale sequenziale
* Creazione automatica della struttura del progetto utilizzando un file di origine, ad esempio un foglio Excel
* Supporto esteso del lettore multimediale con funzioni on-line e offline affidabili (sincronizzazione avanzata) in grado di adattarsi anche alle reti di segnaletica più grandi.
* Personalizzazione in base alla posizione o alla configurazione dei dati generati dai contenuti utilizzando segnaposti dinamici.
* Informazioni unificate in base all’integrazione di Adobe Analytics in AEM Screens Player

Per ulteriori dettagli sulle modifiche ad AEM Screens, consulta le Note sulla versione nella sezione [Guida utente di AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=en).

#### Sviluppo di componenti e modelli {#component-amp-template-development}

* Archetipo di progetto Maven 18+ per nuovi progetti, vedi [Note sulla versione di GitHub](https://github.com/adobe/aem-project-archetype/releases).
* Archetipo di progetto Maven 1.0.6+ per app a pagina singola per nuovi progetti, consulta [Note sulla versione di GitHub](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versione 1.4, vedi [Note sulla versione di GitHub](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * operatore &quot;in&quot; per stringhe, array e oggetti:

      ```html
      ${'a' in 'abc'}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Dichiarazioni di variabili con data-sly-set :
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Elencare e ripetere i parametri di controllo: inizio, passo, fine:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificatori per data-sly-unwrapping:

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Supporto per numeri negativi

* Componenti core 2.3.2+, vedi [Note sulla versione di GitHub](https://github.com/adobe/aem-core-wcm-components/releases).
* Sistema a griglia per contenitore di layout, vedi [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: Google Closure Compiler è stato impostato come predefinito per la minimizzazione delle clientlibs JavaScript (il vecchio predefinito era Yahoo YUI) e aggiornato Google Closure Compiler alla versione v20190121
* Editor modelli e criteri

   * Creare e modificare modelli per le app a pagina singola che utilizzano l&#39;SDK JS (chiamato anche Editor SPA)

* Sito di riferimento We.Retail 4.0, vedi [Note sulla versione di GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Toolkit per aggiornare i siti esistenti per utilizzare le funzionalità più recenti dell’editor, vedi [Archivio GitHub](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM include la versione 1.12.4 della libreria jQuery per fornire la massima compatibilità con il codice personalizzato esistente. Sono state apportate modifiche per Adobe per risolvere problemi di sicurezza noti.

#### Amministrazione del sito {#site-administration}

* La [Riferimento](/help/sites-authoring/author-environment-tools.md#references) La barra laterale presenta una nuova sezione per elencare i collegamenti interni che puntano alla pagina selezionata. Questa funzione è utile quando si pianifica di portare una pagina offline o di eliminarla, per vedere quali pagine devono essere regolate prima di portarle offline.
* La [vista a elenco](/help/sites-authoring/basic-handling.md#list-view) dispone di una nuova colonna del flusso di lavoro che mostra lo stato quando la pagina si trova in un flusso di lavoro.
* In [proprietà pagina](/help/sites-authoring/editing-page-properties.md), è ora possibile cercare le risorse esistenti quando si assegna una miniatura alla pagina (scheda Miniature ).

#### Editor pagina {#page-editor}

* Consente la modifica e la composizione contestuale delle esperienze di app a pagina singola create con React e componenti lato client Angular che utilizzano l’SDK JS (chiamato anche Editor SPA)
* La modalità Scaffolding viene visualizzata solo se la pagina dispone di una pagina di scaffolding configurata.

#### Editor e frammenti di contenuto {#content-fragments-amp-editor}

* Nuovo [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) nell’Editor frammento di contenuto per fare commenti generali e visualizzare i commenti all’interno del testo (anche nella barra Timeline)
* Possibilità di impostare il tipo di contenuto predefinito di un elemento di testo su più righe in un [Modello a frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) per testo semplice, RTF o markdown
* Aggiungi [commento/annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) selezionando il testo nell’editor Rich Text (visualizzazione a schermo intero)
* [Confronto delle versioni](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) di un frammento di contenuto affiancato tramite la barra Riferimento
* Il rapporto di download delle risorse ora mostra i frammenti di contenuto di conseguenza
* Aggiungi [Supporto dei frammenti di contenuto per l’API HTTP Assets](/help/assets/assets-api-content-fragments.md) via /api.json. Sono disponibili API per creare, aggiornare, leggere ed eliminare frammenti di contenuto.

#### Frammenti di esperienza {#experience-fragments}

* È stata migliorata l&#39;indicizzazione di [Frammenti esperienza](/help/sites-authoring/experience-fragments.md)Il loro contenuto si trova quindi nella ricerca di pagine in cui vengono utilizzate.
* La [Esportazione in Target](/help/sites-administering/experience-fragments-target.md) ora consente di inviare il frammento esperienza come JSON (il valore predefinito è HTML) o entrambi.

#### Traduzione {#translation}

* Semplifica la creazione di progetti di traduzione utilizzando i master del progetto.
* Semplifica l’esecuzione dei progetti di traduzione impostando i lavori di traduzione sullo stato approvato per impostazione predefinita.
* Consenti l’aggiornamento delle pagine tradotte con modifiche nella memoria di traduzione di terze parti.
* Consenti esportazione di processi di traduzione in formato JSON.
* Aggiorna l&#39;integrazione di Microsoft® Translation per utilizzare l&#39;API V3.

#### Gestione multisito (MSM) {#multi-site-management-msm}

* Per le configurazioni di rollout che utilizzano PushOnModify, è stata migliorata la gestione delle operazioni di spostamento delle pagine per evitare uno stato incoerente.
* Per impostazione predefinita, la creazione di una pagina all’interno della struttura della Live Copy crea una pagina autonoma.
* Utilizzare le funzionalità MSM nelle app a pagina singola che utilizzano l&#39;SDK JS (chiamato anche Editor SPA)

#### Lanci {#launches}

* Nuovo flusso di lavoro di revisione e approvazione per i lanci e possibilità di promuovere solo le pagine di lancio approvate
* Aggiunto [nell’interfaccia utente per scegliere di eliminare Launch subito dopo la fase di promozione](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Targeting e simulazione dei contenuti {#content-targeting-simulation}

* JavaScript per il livello dati ContextHub e il motore regole lato client è stato aggiornato per utilizzare jQuery 3 per impostazione predefinita.

#### AEM e Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Attualmente:
>
>* Solo `at.js 1.x` è supportato se utilizzi Adobe Target come motore di destinazione in AEM console Attività .
>
>* Entrambi `at.js. 1.x` e `at.js 2.x` sono supportati se utilizzi l’esportazione di Frammenti esperienza in Target ed esegui attività nella console di Target.


* L’integrazione di Adobe Target ora utilizza l’API di Target Standard. Le versioni precedenti di AEM utilizzano l’API HTTP di Target Classic, che ora è obsoleta.
* Adobe Target `mbox.js` è inclusa la versione 63. L’Adobe consiglia vivamente di cambiare l’implementazione in `at.js` v1.x
* `at.js` È ora inclusa la versione 1.5.0. Adobe consiglia di utilizzare [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) disposizione `at.js` v1.x nel sito.

#### AEM e Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 è incluso. Adobe consiglia di passare all’implementazione in `AppMeasurement.js`
* `AppMeasurement.js` È inclusa la versione 1.8.0. Adobe consiglia di utilizzare [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) per eseguire il provisioning di AppMeasurement.js nel sito.

#### AEM e commercio {#aem-commerce}

I miglioramenti apportati a Commerce Integration Framework si trovano a un ciclo di rilascio più rapido a partire da AEM 6.4. [Ulteriori informazioni qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html).

#### Componente aggiuntivo per community {#communities-add-on}

Per ottenere la versione più recente, vedi [Distribuzione di Communities](/help/communities/deploy-communities.md) sezione della documentazione.

##### Miglioramenti all&#39;impegno della community {#enhancements-to-community-engagement}

**Supporto di @Mentions**
AEM Communities consente ora agli utenti registrati di assegnare tag (menzione) ad altri membri registrati per attirare la loro attenzione, in Contenuto generato dagli utenti. I membri con tag (menzionati) vengono quindi informati, con collegamento profondo al contenuto generato dall’utente corrispondente. Gli utenti possono, tuttavia, disattivare/abilitare le notifiche web ed e-mail.

![Supporto delle menzioni](/help/release-notes/assets/at-mentions.png)

Gli utenti della community non devono cercare il loro nome, cognome o nome utente per vedere se qualcuno ha contattato l’utente o ha bisogno della loro attenzione. Inoltre, consente agli autori UGC di cercare risposte da specifici utenti registrati che possono risolvere al meglio il problema e aggiungere input.

Gli amministratori della community devono **Abilita menzione** sui componenti della community per consentire agli utenti registrati di utilizzare la funzionalità su tali componenti.

**Messaggistica di gruppo**

I membri registrati della community ora possono inviare messaggi diretti in blocco ai gruppi tramite una singola composizione e-mail, invece di inviare lo stesso messaggio singolarmente ai membri del gruppo. Consentire [messaggistica di gruppo](/help/communities/configure-messaging.md), attiva entrambe le istanze di [Servizio operazioni di messaggistica](/help/communities/messaging.md#group-messaging).

![Messaggio del gruppo](/help/release-notes/assets/group-messaging.png)

##### Miglioramenti alla moderazione di gruppo {#enhancements-to-bulk-moderation}

Filtri personalizzati nella moderazione di gruppo

[Filtri personalizzati](/help/communities/moderation.md#custom-filters) possono ora essere sviluppati e aggiunti all’interfaccia utente di moderazione di gruppo.

A [progetto di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) che illustra come filtrare tramite tag è disponibile in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Questo progetto può essere utilizzato come base per sviluppare filtri personalizzati analoghi.

![Filtri personalizzati](/help/release-notes/assets/custom-tag-filter.png)

**Visualizzazione a elenco nella moderazione di gruppo**

È stata fornita una nuova visualizzazione a elenco con interfaccia utente migliorata con moderazione di gruppo per visualizzare le voci di contenuto generato dall’utente.

![Moderazione in blocco nella vista a elenco](/help/release-notes/assets/list-view-moderation.png)

##### Miglioramenti alla gestione del sito e dei gruppi {#enhancements-to-site-and-group-management}

**Sito lato autore e amministratori di gruppo**

Le comunità, AEM 6.5 a partire, consentono l&#39;amministrazione decentrata (e la gestione) di diversi siti e gruppi di comunità/gruppi nidificati. Le organizzazioni che ospitano più siti della community e gruppi nidificati ora possono selezionare i membri per i ruoli di amministratore sul lato autore al momento della creazione del sito (e del gruppo).

![Amministratore del sito](/help/release-notes/assets/site-admin.png)

Gli amministratori del sito possono creare un gruppo a qualsiasi livello gerarchico e diventare gli amministratori predefiniti. Gli amministratori di gruppo possono essere rimossi in seguito da altri amministratori di gruppo. Gli amministratori del gruppo possono gestire il proprio gruppo G1 e creare un sottogruppo nidificato sotto G1.

##### Miglioramenti all’abilitazione {#enhancements-to-enablement}

**Supporto SCORM 2017.1**

La funzionalità di abilitazione di AEM 6.5 Communities supporta il modello di riferimento per oggetti di contenuto condivisibile [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) motore.

* Supporto per la navigazione da tastiera su componenti di abilitazione
* I componenti di abilitazione (ad esempio Riproduzione catalogo e corso, Assegnazioni, Libreria file) in AEM Communities supportano la navigazione da tastiera per una migliore accessibilità.

##### Altri miglioramenti {#other-enhancements}

* Supporto Solr 7
* AEM 6.5 Communities supportano la versione Apache Solr 7.0 della piattaforma di ricerca durante la configurazione di MSRP e DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 introduce le seguenti funzionalità e miglioramenti per incrementare la produttività degli utenti AEM, dei ruoli DAM e dei ruoli creativi e di marketing associati.

#### Integrazione con [!DNL Adobe Creative Cloud] e i flussi di lavoro creativi {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] offre diversi modi per integrare con [!DNL Adobe Creative Cloud] e condividere risorse da utilizzare nei flussi di lavoro in cui i team creativi e di marketing o aziendali collaborano strettamente. [!DNL Experience Manager] 6.5 continua a migliorare l&#39;integrazione e a semplificarla ulteriormente per esporre maggiori opportunità e snellire i metodi esistenti.

Continua a leggere per conoscere le funzionalità specifiche e le integrazioni di [!DNL Experience Manager] 6.5 che è possibile utilizzare per supportare al meglio i casi d’uso di velocità dei contenuti.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] rafforza la collaborazione tra creativi e addetti al marketing nel processo di creazione dei contenuti. I creativi possono accedere ai contenuti memorizzati in [!DNL Experience Manager Assets], senza lasciare le app che hanno più familiarità con. I creativi possono sfogliare, cercare, estrarre e archiviare facilmente le risorse utilizzando il pannello in-app in [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] app.

[!DNL Adobe Asset Link] fa parte di [Creative Cloud aziendale](https://www.adobe.com/it/creativecloud/business/enterprise.html) offerta. Per ulteriori informazioni, inclusa la configurazione necessaria del [!DNL Experience Manager] implementazione, vedi [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html).

![Cercare risorse in Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] integrazione {#stock}

La tua organizzazione può utilizzare i propri [!DNL Adobe Stock] piano aziendale entro [!DNL Experience Manager Assets] per garantire che le risorse concesse in licenza siano ampiamente disponibili per i progetti creativi e di marketing. Puoi trovare rapidamente, visualizzare in anteprima e concedere licenze [!DNL Adobe Stock] risorse salvate in Experience Manager, utilizzando le potenti funzionalità DAM di [!DNL Experience Manager].

[!DNL Adobe Stock] Il servizio consente a designer e aziende di accedere a milioni di foto, vettoriali, illustrazioni, video, modelli e risorse 3D di alta qualità, curate e prive di royalty, per tutti i loro progetti creativi.

Per ulteriori informazioni, consulta [Utilizzare le risorse Adobe Stock in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Anteprima immagine e licenza di Adobe Stock da Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figura: Anteprima [!DNL Adobe Stock] immagine e licenza da [!DNL Experience Manager Assets].*

![Cerca e filtra le immagini Adobe Stock concesse in licenza in Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Figura: Cerca e filtra la licenza [!DNL Adobe Stock] immagini in [!DNL Experience Manager].*

##### Riferimenti dinamici in [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] utilizzato in [!DNL Adobe InDesign] i file sono dinamici. I riferimenti vengono aggiornati automaticamente se le risorse a cui si fa riferimento si spostano nella directory archivio. Per ulteriori informazioni, consulta [come gestire le risorse composte](/help/assets/managing-linked-subassets.md).

#### Funzionalità Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] consente di acquisire, controllare efficacemente e distribuire in modo sicuro le risorse approvate a fornitori/agenzie esterni e utenti aziendali interni su diversi dispositivi. Consente di migliorare l’efficienza della condivisione delle risorse, di accelerare il time-to-market delle risorse ed elimina il rischio di utilizzo non conforme e di accesso non autorizzato.

Per ulteriori informazioni, consulta [Novità di Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=it).

#### Risorse collegate {#connectedassets}

Nelle grandi aziende l&#39;infrastruttura necessaria per la creazione di siti web può essere distribuita. A volte, le funzionalità di creazione dei siti web e le risorse digitali richieste risiedono in silos diversi.

[!DNL Experience Manager Sites] offerte per la creazione di pagine web e [!DNL Experience Manager Assets] è il sistema Digital Asset Management (DAM) che fornisce le risorse necessarie per i siti web. [!DNL Experience Manager] ora supporta il caso d’uso precedente integrando [!DNL Sites] e [!DNL Assets]. Vedi [come configurare e utilizzare la funzione Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

![Trascina una risorsa da un [!DNL Experience Manager] implementazione su un [!DNL Sites] di una pagina diversa [!DNL Experience Manager] distribuzione](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Figura: Trascina una risorsa da un [!DNL Experience Manager] implementazione su un [!DNL Sites] in una pagina diversa [!DNL Experience Manager] distribuzione.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] fornisce funzionalità avanzate di authoring e distribuzione di contenuti rich media in [!DNL Experience Manager Assets] per offrire esperienze all’avanguardia coinvolgenti e personalizzate. Caricando un’unica risorsa primaria di alta qualità e utilizzando il rendering cloud avanzato di Adobe e i visualizzatori, puoi fornire in tempo reale qualsiasi combinazione di rappresentazioni per supportare la strategia multimediale della tua organizzazione.

Per maggiori dettagli sulle nuove [!DNL Dynamic Media] funzioni, vedi [Note sulla versione di Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Supporto video a 360° {#video-support}

Gestisci i tuoi file video a 360° direttamente in [!DNL Experience Manager] utilizzando i visualizzatori all&#39;avanguardia per offrire esperienze VR a desktop, dispositivi mobili e visore VR. Per ulteriori informazioni, consulta [Utilizzo di video 360](/help/assets/360-video.md).

##### Miniature video personalizzate {#custom-video-thumbnails}

È ora possibile personalizzare le miniature delle risorse video utilizzando i fotogrammi del video stesso o di altro contenuto memorizzato in DAM. Per ulteriori istruzioni, consulta [Informazioni sulle miniature video](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Miglioramenti dell’accessibilità {#accessibility-enhancements}

[!DNL Dynamic Media] i visualizzatori ora supportano funzioni di accessibilità avanzate come supporto Aria, assistenti vocali e testo Alt. Per ulteriori dettagli, consulta [Guida di riferimento visualizzatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Miglioramento dell’esperienza di ricerca {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partire dalla versione 6.5, gli addetti al marketing possono individuare più rapidamente le risorse desiderate dalla pagina dei risultati di ricerca. I facet di ricerca vengono aggiornati con il numero di risorse anche prima di applicare il filtro di ricerca. La visualizzazione del conteggio previsto per il filtro consente agli utenti di navigare nei risultati della ricerca in modo efficiente. Per ulteriori informazioni, consulta [Cercare risorse in Experience Manager](/help/assets/search-assets.md).

![Visualizzare il numero di risorse senza filtrare i risultati di ricerca nei facet di ricerca](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Vedi il numero di risorse senza filtrare i risultati di ricerca nei facet di ricerca.*

#### Miglioramento dell’usabilità {#usability-enhancement}

Ora puoi selezionare tutte le risorse caricate all’interno di una cartella o da un risultato di ricerca con una sola operazione. Consente di gestire rapidamente più risorse. La casella di controllo seleziona tutte le risorse che rientrano nello scenario, ad esempio un risultato di ricerca, e non solo le risorse visibili nel [!DNL Experience Manager] interfaccia.

![Utilizza l’opzione Seleziona tutto per selezionare tutte le risorse caricate con un solo clic.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Figura: Utilizza l’opzione Seleziona tutto per selezionare tutte le risorse caricate con un solo clic.*

#### Miglioramenti ai metadati {#metadata-enhancements}

[!DNL Assets] consente di creare schemi di metadati per le cartelle di risorse, che definiscono il layout e i metadati visualizzati nelle pagine delle proprietà della cartella. È ora possibile assegnare uno schema di metadati della cartella a una cartella esistente o durante la creazione di una cartella. Per ulteriori informazioni, consulta [Schema metadati cartelle](/help/assets/metadata-config.md#folder-metadata-schema).

Quando si specificano i metadati a cascata, le scelte possono essere caricate da un file JSON in fase di esecuzione, ad esempio anziché digitare manualmente nel modulo. Per ulteriori informazioni, consulta [metadati a cascata](/help/assets/metadata-schemas.md#cascading-metadata).

#### Miglioramenti al reporting {#reporting-enhancements}

I frammenti di contenuto e le condivisioni di collegamenti sono ora inclusi nel rapporto scaricato. Per ulteriori informazioni, consulta [Rapporti sulle risorse](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms introduce diverse nuove funzioni e miglioramenti. Gli elementi di rilievo includono:

* Rapporti delle transazioni per tenere traccia del numero di moduli inviati, documenti elaborati e documenti sottoposti a rendering
* Miglioramenti a livello di usabilità delle comunicazioni interattive
* Firme digitali basate su cloud nei moduli adattivi
* Incorporare moduli adattivi e comunicazioni interattive in un’applicazione a pagina singola (SPA) AEM Sites.
* Supporto delle variabili nei flussi di lavoro AEM
* Supporto dei pattern di visualizzazione dei dati nelle comunicazioni interattive
* Ordinamento di moduli adattivi e tabelle di comunicazione interattive
* Convalida automatizzata dei dati di input nei modelli di dati per moduli

Consulta la sezione [Riepilogo delle nuove funzioni e dei miglioramenti in Forms 6.5 AEM](/help/forms/using/whats-new.md) per informazioni sulle funzioni nuove e migliorate e sulle risorse di documentazione.

### Utilizzare lo sviluppo incentrato sul cliente {#leverage-customer-focused-development}

Adobe utilizza un modello di sviluppo incentrato sul cliente che consente ai clienti di contribuire a tutte le fasi del processo di sviluppo, durante specifiche, sviluppo e test. I nostri ringraziamenti vanno a tutti i clienti e partner che hanno contribuito a questo processo.

Adobe dispone delle procedure e dei processi necessari per abilitare la raccolta, la definizione delle priorità e il tracciamento della risoluzione dei bug incentrata sul cliente e lo sviluppo delle richieste di miglioramento. La [Portale di supporto Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=it#support) è integrato con il sistema di monitoraggio Adobe e difetti. Le domande dei clienti vengono identificate e risolte dal team di assistenza clienti, ove possibile. Quando si passa a R&amp;S, tutte le informazioni dei clienti vengono acquisite e utilizzate a scopo di definizione delle priorità e reporting. Nello sviluppo viene data la priorità al supporto a pagamento, ai problemi di garanzia e ai miglioramenti pagati dal cliente.

Questo processo di prioritizzazione ha portato a più di 750 cambiamenti incentrati sul cliente risolti nella AEM 6.5.

## Elenco dei file che fanno parte della versione {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Quickstart indipendente: `cq-quickstart-6.5.0.jar`.
* Avvio rapido server applicazioni: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 o versioni successive per i vari server web e piattaforme. Vedi [collegamento di download](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plug-in per Eclipse IDE ([ulteriori informazioni e download](/help/sites-developing/aem-eclipse.md))

* Estensione per l’editor di codice di Brackets ([ulteriori informazioni e download](/help/sites-developing/aem-brackets.md))
* Dipendenze Maven/Gradle ([collegamento di download](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componenti core ([Progetto GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementazione di riferimento We.Retail ([leggi tutto](/help/sites-developing/we-retail.md))
* Archetipi di progetto Maven:

   * per siti con stack completo: [Progetto GitHub](https://github.com/adobe/aem-project-archetype)
   * per le app a pagina singola con React/Angular: [Progetto GitHub](https://github.com/adobe/aem-spa-project-archetype)

* Lettori AEM Screens per varie piattaforme target ([scaricare](https://download.macromedia.com/screens/))

* Modelli per lingue con contenuti avanzati. L&#39;inglese è preinstallato - è possibile scaricare altre lingue

   * [Tedesco](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Spagnolo](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francese](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernizza la suite di strumenti, ad esempio lo strumento di conversione finestra di dialogo. ([Progetto GitHub](https://github.com/adobe/aem-modernize-tools))

**Risorse**

* Pacchetto per aggiungere un PDF Rasterizer migliorato ([leggi tutto](/help/assets/aem-pdf-rasterizer.md))
* Pacchetto per aggiungere supporto esteso per immagini RAW ([leggi tutto](/help/assets/camera-raw.md))

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

Per istruzioni dettagliate, vedi [documentazione di aggiornamento](/help/sites-deploying/upgrade.md).

## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto su [AEM 6.5 requisiti tecnici](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle è passato a un modello di supporto a lungo termine (LTS) per i prodotti Java™ SE di Oracle. Java™ 9 e 10 sono versioni non LTS per Oracle. Vedi [Roadmap del supporto Java™ SE di Oracle](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe supporta le versioni LTS di Java™ per eseguire AEM solo in produzione. Java™ 11 è la versione consigliata da utilizzare con AEM 6.5.

## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità del prodotto e nel tempo pianifica di sostituire le funzionalità con versioni più potenti, oppure decide di reimplementare parti selezionate per essere meglio preparate per aspettative o estensioni future.

Per [!DNL Adobe Experience Manager] 6.5 [leggi l’elenco delle funzionalità obsolete e rimosse](/help/release-notes/deprecated-removed-features.md). La pagina contiene anche un preannuncio delle modifiche in arrivo in futuro e un avviso importante per i clienti che eseguono l’aggiornamento da versioni precedenti.

## Problemi noti {#known-issues}

### Platform {#platform}

* Viene segnalato un problema in cui il CRX-Quickstart e il relativo contenuto vengono eliminati.

   Per ciascuna di queste azioni, assicurati che la proprietà `htmllibmanager.fileSystemOutputCacheLocation` non è una stringa vuota:

   1. Chiamata `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Aggiornamento a AEM 6.5.
   3. Esecuzione della &quot;migrazione pigra dei contenuti&quot; in AEM 6.5.

   A [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) questo articolo è disponibile con ulteriori dettagli e la soluzione a questo problema.

* Se utilizzi JDK 11 con AEM istanza 6.5, alcune pagine potrebbero essere visualizzate come vuote dopo la distribuzione di alcuni pacchetti. Nel file di registro viene visualizzato il seguente messaggio di errore:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Per risolvere questo errore:

1. Interrompi l&#39;istanza AEM. Vai a `<aem_server_path_on_server>crx-quickstart\conf` e aprire `sling.properties` file. L&#39;Adobe consiglia di eseguire un backup del file.

1. Cerca `org.osgi.framework.bootdelegation=`. Aggiungi `jdk.internal.reflect,jdk.internal.reflect.*` proprietà per visualizzare il risultato come.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Salva il file e riavvia l&#39;istanza AEM.

### Sites {#sites}

* **Utilizzo delle versioni di una pagina**: [Se una pagina è stata spostata, non è più possibile eseguire un’anteprima su nessuna versione effettuata prima dello spostamento](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Risorse {#assets}

* **Ricerca:** La ricerca non restituisce alcun risultato se la stringa di ricerca contiene spazi iniziali ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schema metadati cartelle**: Dopo aver aggiunto un pulsante di scelta, i campi ID e Valore non vengono visualizzati come previsto e la funzionalità di eliminazione non funziona. (CQ-4261144)
* Quando si rinomina una risorsa, non è possibile utilizzare uno spazio vuoto nel nome della risorsa. (CQ-4266403)

### Forms {#forms}

* Quando AEM Forms è installato sul sistema operativo Linux®, la firma digitale con modulo di sicurezza hardware non funziona. (CQ-4266721)
* (AEM Forms solo su WebSphere®) Il **Forms Workflow** > **Ricerca attività** l&#39;opzione non restituisce alcun risultato se si cerca un **Amministratore** con **Nome utente** come criteri di ricerca. (CQ-4266457)

* AEM Forms non riesce a convertire i file TIF e TIFF con compressione JPEG in documenti PDF. (CQ-4265972)
* La **Scanner risorse AEM Forms** e **Migrazione dalla comunicazione interattiva** le opzioni non funzionano **Migrazione AEM Forms** pagina. (CQ-4266572)

* (Solo JBoss® 7) Quando si esegue l’aggiornamento da una versione precedente a AEM 6.5 Forms e la versione precedente disponeva di processi (.lca) che hanno creato e utilizzato una copia del processo di invio o di rendering predefinito, HTML5 Forms che utilizza tali processi (.lca) non riesce a eseguire le azioni richieste. (CQ-4243928)
* In un modulo adattivo, quando un servizio del modello dati modulo viene richiamato dall’editor di regole per aggiornare dinamicamente i valori del componente di scelta dell’immagine, i valori del componente di scelta dell’immagine non vengono aggiornati. (CQ-4254754)
* Il programma di installazione di AEM Forms Designer richiede la versione a 32 bit di [Pacchetto runtime ridistribuibile di Visual C++ 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) e [Pacchetti runtime ridistribuibili di Visual C++ 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). Prima di avviare l&#39;installazione, verificare che i pacchetti di runtime ridistribuibili di cui sopra siano installati. (CQ-4265668)

* PDF Generator non supporta l&#39;autenticazione basata su smart card. Quando un amministratore abilita Criteri di gruppo `Interactive Logon: Require Smart card` su un server Windows, tutti gli utenti esistenti di PDF Generator vengono invalidati.

* Quando un modulo adattivo è configurato per aggiornare dinamicamente i valori di un componente e l’istanza di pubblicazione che ospita il modulo è accessibile tramite Dispatcher, la funzionalità di aggiornamento dinamico dei valori di un campo smette di funzionare. Per risolvere il problema, nell&#39;istanza di pubblicazione, apri CRXDE, accedi a `/libs/fd/af/runtime/clientlibs/guideChartReducer`, e crea la proprietà elencata di seguito.

   * Nome: allowProxy
   * Tipo: Booleano
   * Valore: true
   * Protetto: False
   * Obbligatorio: False
   * Multipli: False
   * Creazione automatica: False

   La proprietà consente alle librerie client nella cartella di runtime di accedere ai proxy. (CQ-4268679)

* Quando AEM Forms viene avviato, la `SAX Security Manager could not be setup` viene visualizzato un avviso.
* Quando si apre un PDF protetto con AEM Forms Document Security su un Apple iOS o iPadOS con versione 20.10.00 di Adobe Acrobat Reader
* Quando si invia un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file a 0 byte dall’altro lato. Apple iOS 15.1 fornisce una correzione al problema.

## Download e supporto del prodotto (siti con restrizioni) {#product-download-and-support-restricted-sites}

I seguenti siti sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il tuo responsabile commerciale di Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/).

* Aggiornamenti dei prodotti, patch e pacchetti per funzionalità aggiuntive su [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).

* [Assistenza clienti tramite Admin Console](https://adminconsole.adobe.com/). Per ulteriori informazioni, consulta [Nuova esperienza di accesso all’Assistenza clienti di Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en).
