---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova informazioni sulla versione, novità, procedure guidate di installazione e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5
mini-toc-levels: 4
source-git-commit: 19fe527ce44d8ec5be50ebd32b46f13df96c52cc
workflow-type: tm+mt
source-wordcount: '2928'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | giovedì 22 febbraio 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] La versione 6.5.20.0 include nuove funzioni, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la disponibilità iniziale della versione 6.5 di aprile 2019. [Installa il service pack](#install) il [!DNL Experience Manager] 6.5

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funzioni principali e miglioramenti

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Alcune delle funzioni e dei miglioramenti principali di questa versione includono:

* Dynamic Medie ora supporta il formato immagine HEIC senza perdita di dati per Apple iOS/iPadOS. Consulta [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) nell’API di server e rendering immagini di Dynamic Medie.

* Multisite Manager (MSM) ora supporta le strutture dei frammenti di esperienza, incluse cartelle e sottocartelle, per un rollout in blocco efficiente dei frammenti di esperienza in Live Copy.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problemi risolti in Service Pack 20 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### Interfaccia utente amministratore{#sites-adminui-6520}

* Il `Workflow Title` il campo è contrassegnato con `*` come richiesto, ma non esiste alcuna convalida. (SITES-16491) NORMALE

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* Le cartelle di configurazione nidificate non erano più supportate e le cartelle dei modelli per frammenti di contenuto non erano più visibili dopo l’aggiornamento a AEM 6.5.18 o a AEM 6.5.19. (SITES-18110) PRINCIPALE
* Alcune sottocartelle non sono in grado di scegliere da modelli di frammenti di contenuto ereditati. Deve supportare le cartelle senza `jcr:content` , anche se le cartelle DAM create tramite l’interfaccia utente dispongono di tale nodo. (SITES-17943) NORMALE

#### [!DNL Content Fragments] - API GRAPHQL {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* Durante l’esecuzione di una query GraphQL in [risultati filtro](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) utilizzando variabili facoltative, se un valore specifico è **non** fornito per la variabile facoltativa, la variabile viene ignorata nella valutazione del filtro. (SITES-17051) NORMALE

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - API REST{#sites-restapi-6520}

* Con l&#39;aggiornamento del `org.json` libreria, si è verificata una modifica nel modo in cui i numeri decimali sono stati deserializzati. Prima venivano convertiti &quot;per impostazione predefinita&quot; in doppi e ora in BigDecimals. Al contrario, i valori delle proprietà dei metadati, memorizzati tramite l’API REST, devono essere convertiti in Double da BigDecimal. (SITES-16857) NORMALE

#### Back-end core{#sites-core-backend-6520}

* Quando si utilizza la pubblicazione rapida di un frammento di contenuto, questo continua a essere caricato e non viene pubblicato. In altre parole, la pubblicazione rapida non funziona per i frammenti di contenuto dopo un aggiornamento del service pack da AEM 6.5.7 a AEM 6.5.17. Quando l’utente tentava di eseguire una pubblicazione gestita, questa funzionava. Tuttavia, quando hanno provato la pubblicazione rapida, non veniva pubblicata. In particolare, `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` ha causato il malfunzionamento del sistema. (SITES-17311) PRINCIPALE
* I frammenti di contenuto non possono essere serializzati con l’esportatore Jackson: il caricamento della pagina si interrompe quando in una pagina viene fatto riferimento a un frammento di contenuto (viene utilizzato il codice di esportazione Jackson) ed eventuali tag aggiunti a un frammento di contenuto. (SITES-18096) NORMALE

#### Componenti core{#sites-core-components-6520}

* L’installazione del pacchetto dei componenti core CIF sull’AEM causa `:type` valore dei componenti esistenti da modificare. In seguito alla modifica, non verranno più riprodotte sulle pagine a cui sono state aggiunte. (SITES-17601) PRINCIPALE

#### Integrazione di Campaign{#sites-campaign-integration-6520}

* L’AEM utilizzava un elenco Consentiti di, noto anche come `whitelist`-a causa di un rapporto di vulnerabilità. Il inserisco nell&#39;elenco Consentiti di impediva ai clienti di utilizzare le funzionalità necessarie. (SITES-16822) CRITICO

#### Frammenti di esperienza{#sites-experiencefragments-6520}

* MSM per frammenti di esperienza ora supporta il rollout in blocco nelle strutture di contenuto dei frammenti di esperienza, incluse cartelle e sottocartelle. (SITES-16004) PRINCIPALE

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - Live Copy{#sites-msm-live-copies-6520}

* Un &quot;`Is not modifiable`&quot;viene generata un’eccezione durante il rollout del componente. In particolare, un `org.apache.sling.servlets.post.impl.operations.ModifyOperation` si verifica un’eccezione durante l’elaborazione della risposta. (SITES-18809) PRINCIPALE
* Impossibile eseguire il rollout delle modifiche a specifiche Live Copy di frammenti esperienza. (SITES-17930) PRINCIPALE
* Quando un utente aggiunge un’annotazione a un componente in una pagina blueprint e poi la esegue su rollout, il conteggio delle annotazioni in Live Copy non viene visualizzato correttamente. (SITES-17099) PRINCIPALE
* Il pulsante Rollout MSM dalla pagina padre alla pagina figlio è interrotto nell’interfaccia utente grafica touch; se selezionata, viene visualizzato il seguente errore: `Uncaught TypeError: _g.shared is undefined`. (SITES-16991) PRINCIPALE

#### Editor pagina{#sites-pageeditor-6520}

* L’anteprima dell’Editor temi di Forms è interrotta. Quando si seleziona Anteprima, è visibile solo un&#39;icona di caricamento. (SITES-17164) BLOCCANTE

### [!DNL Assets]{#assets-6520}

* Impossibile convalidare i campi basati su regole nell’helper dell’editor di metadati e visualizza un messaggio di errore &quot;Campi obbligatori mancanti&quot;. (ASSETS-31396) PRINCIPALE
* Quando un PDF viene spostato in un&#39;altra posizione, **[!UICONTROL Visualizza pagina]** scompare. (ASSETS-30538) PRINCIPALE
* Impossibile selezionare un&#39;immagine con autorizzazioni di lettura. (ASSETS-32199) NORMALE
* Impossibile modificare le dimensioni della scheda nelle impostazioni di visualizzazione. (ASSETS-31667) NORMALE
* Il caricamento non riesce durante il caricamento del tipo di file .oft. (ASSETS-30109) NORMALE
* Quando tenti di aggiungere al rapporto un campo di metadati personalizzato come colonna aggiuntiva, le caselle di controllo non sono selezionate. (ASSETS-31671) NON GRAVE
* L’operazione di spostamento delle risorse non funziona correttamente in Experience Manager Service Pack 16. (ASSETS-30598) NON GRAVE

#### [!DNL Dynamic Media]{#assets-dm-6520}

* Quando una risorsa viene caricata nell’AEM, il `Update_asset` viene attivato il flusso di lavoro. Tuttavia, il flusso di lavoro non viene mai completato. Il flusso di lavoro viene completato solo fino al passaggio di caricamento del prodotto. Il passaggio successivo è il caricamento batch di Scene7, ma tale processo non viene inserito nell’AEM. (ASSETS-30443) CRITICO
* Hai bisogno di un modo migliore per gestire correttamente i video non Dynamic Medie nel componente Dynamic Medie. Questo problema causava un’istanza di eccezione `dynamicmedia_sly.js`. (ASSETS-31301) PRINCIPALE
* L’anteprima funziona per tutte le risorse, i set di video adattivi e i video. Tuttavia, genera un errore 403 per `.m3u8` file (che, tra l&#39;altro, funzionano ancora tramite collegamenti pubblici). (ASSETS-31882) PRINCIPALE
* Il `scene7SmartCropProcessingStatus` stato corretto. Metadati video di ritaglio avanzato utilizzati per mostrare l’errore anche in caso di esito positivo. (ASSETS-31255) NON GRAVE

### [!DNL Forms]{#forms-6520}

Correzioni in [!DNL Experience Manager] Forms vengono forniti tramite un pacchetto aggiuntivo separato una settimana dopo il [!DNL Experience Manager] Data di rilascio del Service Pack. In questo caso, il rilascio del pacchetto aggiuntivo Forms AEM 6.5.20.0 è pianificato per giovedì 29 febbraio 2024. Dopo la versione di, a questa sezione viene aggiunto un elenco di correzioni e miglioramenti di Forms.

<!-- #### [!DNL Adaptive Forms] -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6520}

* text -->

#### [!DNL Forms Designer]{#forms-designer-6520}

* text

<!-- ### Foundation{#foundation-6520}

* text -->

#### Communities {#communities-6520}

* Diagnostica sincronizzazione utenti non riuscita dopo la configurazione della sincronizzazione utenti. (NPR-41693) NORMALE

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### Integrazioni{#integrations-6520}

* Rimuovi tutto il codice e le dipendenze di Adobe Search&amp;Promote da AEM 6.5. (NPR-40856) NORMALE

#### Localizzazione{#localization-6520}

* Aria-label &quot;close&quot; non è localizzato in **[!UICONTROL Risorse]** > **[!UICONTROL File]**, seleziona una cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]** > **[!UICONTROL Autorizzazioni]** scheda > nome membro. (NPR-41705) PRINCIPALE
* La descrizione del comando per il **[!UICONTROL Password archivio chiavi]** nella pagina SSL Setup (Impostazione SSL) per le impostazioni internazionali ENG, FRA, KOR, DEU e PTB. (NPR-41367) NORMALE

<!-- #### Oak{#oak-6520}

* text -->

#### Platform{#foundation-platform-6520}

* Problema durante l’integrazione di Campaign con AEM causato dal fatto che il servlet /api non restituisce lo schema corretto nel json href. Il motivo era che l’AEM non stava ricevendo l’intestazione X-Forward-Proto che costrinse la richiesta a rispondere con uno schema HTTP invece che HTTPS. Pertanto, è necessario aggiungere la possibilità di attivare/disattivare la selezione dello schema in base a una configurazione OSGI. (GRANITE-48454) PRINCIPALE

<!-- #### Replication{#foundation-replication-6520}

* text -->

#### Sling{#foundation-sling-6520}

* Il `org.apache.sling.resourceMerger` il bundle 1.4.2 genera un’eccezione da AEM 6.5, Service Pack 17 e versioni successive. La fusione di risorse Sling 1.4.4 deve essere inclusa in Service Pack 20. (NPR-41630) NORMALE

#### Traduzione{#foundation-translation-6520}

* In seguito alla distribuzione di AEM 6.5 Service Pack 18, si è verificato un problema con la scheda Filtri nell’Editor delle regole di traduzione. Quando si seleziona un contesto, facendo clic su Modifica > Salva, alla successiva apertura dello stesso contesto viene visualizzata una virgoletta doppia come carattere HTML. In sostanza, le regole di traduzione non venivano salvate correttamente. (NPR-41624) PRINCIPALE
* Problemi relativi alle traduzioni di frammenti di contenuto, in cui le stringhe tradotte vengono rimandate dal provider di traduzione all’AEM, ma rimangono bloccate nel `/content/projects` senza aggiornare i frammenti di contenuto. (NPR-41516) PRINCIPALE
* Durante la creazione di una copia per lingua viene visualizzato un messaggio di errore. Si verifica in una pagina in cui è presente un frammento di contenuto a cui si fa riferimento in una proprietà della pagina, utilizzando modelli per frammenti di contenuto. (NPR-41441) PRINCIPALE
* I collegamenti nei frammenti esperienza non vengono regolati nella lingua corretta durante la copia in lingua. Il frammento di esperienza punta invece alla lingua principale. (NPR-41343) NORMALE

#### Interfaccia utente{#foundation-ui-6520}

* Si verifica un errore della console dopo un aggiornamento a AEM 6.5, Service Pack 18. L’errore si trova in `coralUI3.js` e si verifica quando si seleziona un elenco a discesa in AEM. Nello specifico, si verifica con un `onOverlayToggle` evento. L’errore `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` viene visualizzato. (NPR-41467) PRINCIPALE
* Nell&#39;AEM, **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Assegnazione tag]** > **[!UICONTROL Crea]** > **[!UICONTROL Crea tag]**, immissione di caratteri non latini nel **Titolo** causa la **Nome** campo da compilare con il solo trattino ( `-` ). (NPR-41623) NORMALE
* L&#39;anno di copyright non è corretto in `About Adobe Experience Manager` . (NPR-41526) NORMALE
* Non tradotti **[!UICONTROL Proprietà profilo]** durante la modifica delle impostazioni utente. Si verifica in tutte le lingue. (NPR-41365) NORMALE

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## Installa [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0 richiede [!DNL Experience Manager] 6.5. Cfr. [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate. <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del service pack è disponibile su Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* In una distribuzione con MongoDB e più istanze, installa [!DNL Experience Manager] 6.5.20.0 in una delle istanze di authoring che utilizzano Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> L’Adobe non consiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.20.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup del `crx-repository` nel caso in cui sia necessario riportarlo indietro. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installare il service pack in [!DNL Experience Manager] 6,5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia di riavviare se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup del file [!DNL Experience Manager] dell&#39;istanza.

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Consulta [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta si apre una finestra di dialogo sull’interfaccia utente di Gestione pacchetti durante l’installazione del service pack. L’Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di avere la certezza che l’installazione sia andata a buon fine. In genere, questo problema si verifica in [!DNL Safari] ma può verificarsi in modo intermittente su qualsiasi browser.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente [!DNL Experience Manager] 6.5.20.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserisci la confezione in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza il [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` affinché i pacchetti nidificati vengano installati.

>[!NOTE]
>
>L&#39;Experience Manager 6.5.20.0 non supporta l&#39;installazione Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalidare l’installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo di questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa della versione aggiornata `Adobe Experience Manager (6.5.20.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (usa la console web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.18 o successiva (utilizzare la console Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installa Service Pack per [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Per istruzioni sull&#39;installazione del service pack in Experience Manager Forms, vedere [Istruzioni di installazione di Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funzione Forms adattivo, disponibile in [QuickStart per AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html), è progettata esclusivamente a scopo di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms, in quanto la funzionalità Adaptive Forms richiede una licenza appropriata.

### Installare il pacchetto di indice GraphQL per frammenti di contenuto Experience Manager{#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare [Frammento di contenuto di Experience Manager con pacchetto indice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

In questo modo puoi aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate.

Se non si installa questo pacchetto, è possibile che le query GraphQL risultino lente o non riuscite.

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar{#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.20.0 è disponibile nel [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come usare UberJar](/help/sites-developing/ht-projects-maven.md) e includere la seguente dipendenza nel POM del progetto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.20</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece che nell’archivio Maven pubblico di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Quindi, non c&#39;è `classifier`, con `apis` come valore, per `dependency` tag.

## Funzioni obsolete e rimosse{#removed-deprecated-features}

Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md/).

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->



* **Correlato a Oak**
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

* Aggiorna le query GraphQL che potrebbero aver utilizzato un nome API personalizzato per il modello di contenuto in modo da utilizzare il nome predefinito del modello di contenuto.

* Una query GraphQL può utilizzare `damAssetLucene` indice invece di `fragments` indice. Questa azione potrebbe causare l’errore o richiedere molto tempo per l’esecuzione delle query GraphQL.

  Per risolvere il problema: `damAssetLucene` deve essere configurato per includere le seguenti due proprietà in `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Dopo aver modificato la definizione dell’indice, è necessaria una reindicizzazione (`reindex` = `true`).

  Dopo questi passaggi, le query GraphQL dovrebbero funzionare più rapidamente.

* Quando si tenta di spostare, eliminare o pubblicare frammenti di contenuto, siti o pagine, si verifica un problema quando si recuperano i riferimenti ai frammenti di contenuto, poiché la query in background non riesce. In altre parole, la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell’indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se aggiorni il tuo [!DNL Experience Manager] dalla versione 6.5.0 alla versione 6.5.4 al service pack più recente su Java™ 11, vedi `RRD4JReporter` eccezioni in `error.log` file. Per interrompere le eccezioni, riavvia l’istanza di [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Gli utenti possono rinominare una cartella in una gerarchia in [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] fino alla ripubblicazione della cartella principale.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando l’integrazione di Adobe Target è configurata in [!DNL Experience Manager] se utilizzi l’API di Target Standard (autenticazione IMS), e successivamente esporti frammenti di esperienza in Target, verranno creati tipi di offerta errati. Invece del tipo &quot;Frammento di esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in granite/operations/maintenance.
   * La convalida lato server di Moduli adattivi non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nessuna finestra di manutenzione trovata in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Medie non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : timeout in attesa del completamento della modifica del registro, annullamento della registrazione.

* A partire da AEM 6.5.15, il motore JavaScript Rhino fornito da ```org.apache.servicemix.bundles.rhino``` Il bundle ha un nuovo comportamento di posizionamento. Script che utilizzano la modalità rigorosa (```use strict;```) devono dichiarare correttamente le loro variabili, altrimenti non vengono eseguite, generando invece un errore di runtime.

### Problemi noti per AEM Forms

#### Piattaforme supportate

* JDK 11.0.20 non è supportato per installare AEM Forms sul programma di installazione JEE. Per installare AEM Forms sul programma di installazione di JEE sono supportate solo JDK 11.0.19 o versioni precedenti. (FORMS-10659)

#### Installazione

* Sulla piattaforma JBoss® 7.1.4, quando l’utente installa il service pack Experience Manager 6.5.16.0 o versione successiva, `adobe-livecycle-jboss.ear` distribuzione non riuscita. (CQ-4351522, CQDOC-20159)

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) -->

* Dopo aver installato il programma di installazione completo AEM Service Pack 6.5.20.0, l’implementazione EAR non riesce su JEE utilizzando JBoss® Turnkey. <!-- UPDATE FOR EACH NEW RELEASE -->

Per risolvere il problema, individuare `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` file e aggiornamento `Adobe_Adobe_JAVA_HOME` a `Adobe_JAVA_HOME` per tutte le occorrenze prima di eseguire gestione configurazione. (CQDOC-20803)

#### Installare il frammento del servlet (AEM Service Pack 6.5.14.0 o precedente)

* Se stai eseguendo l’aggiornamento a AEM Service Pack 6.5.15.0 o versione successiva e l’istanza AEM funziona su Tomcat 8.5.88, è necessario installare il frammento del servlet. Esegui l&#39;installazione *prima di* procedere con l&#39;installazione di Service Pack 6.5.15.0 o versione successiva.
* È necessario installare il frammento del servlet per tutti i server applicazioni, eccetto quelli in esecuzione su JBoss® EAP 7.4.0.

**Per installare il frammento del servlet:**

1. Scarica il frammento servlet da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Avviare il server applicazioni.
1. Attendi che i registri si stabilizzino e controllino lo stato del bundle.
1. Apri i bundle della console web. L’URL predefinito è `http://[Server]:[Port]/system/console/bundles`.
1. Seleziona **[!UICONTROL Installa]** o **[!UICONTROL Aggiorna]**.
1. Seleziona il frammento scaricato
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. Seleziona **[!UICONTROL Installa]** o **[!UICONTROL Aggiorna]**.
1. Attendere la stabilizzazione del server applicazioni.
1. Arrestare il server applicazioni.

#### Moduli adattivi

* Quando viene pubblicato un modulo adattivo, tutte le sue dipendenze, inclusi i criteri, vengono ripubblicate, anche se non sono state apportate modifiche. (FORMS-10454)
* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata nel Browser proprietà. Per risolvere il problema, fai clic su per configurare un altro campo del modulo adattivo nello stesso editor.
* Quando gli utenti eseguono l’azione di invio, l’invio non riesce e viene visualizzato un errore:
  `javax.servlet.ServletException: java.lang.NoSuchMethodError`
Per risolvere il problema: [ricompilare gli script Sling come JSP™ Java e Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html#resolution). (FORMS-8542)
* Dopo aver installato AEM Service Pack 6.5.14.0 e versioni successive, gli utenti non sono in grado di selezionare un font dall’interfaccia utente di amministrazione di JEE per i documenti PDF quando passano a `Home` > `Services` > `PDF Generator` > `Adobe PDF Settings`, poiché l&#39;elenco dei caratteri appare vuoto. (FORMS-12095)
<!-- When a form is signed using the OOTB Scribble Signature component, it appears in the image dialogue but does not preview and appears blank when you click on it. (FORMS-12073). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md) -->
* In AEM Forms su JEE, il Forms HTML5 che utilizza il percorso di contesto non riesce a eseguire il rendering. (FORMS-12485, FORMS-12691). Per questo problema è disponibile un hotfix. Per scaricare e installare l’hotfix, consulta [Hotfix per Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md).
* Forms adattivo consente di utilizzare funzioni personalizzate con ECMAScript versione 5 o precedente. Quando una funzione personalizzata utilizza ECMAScript versione 6 o successiva, ad esempio le funzioni &#39;let&#39;, &#39;const&#39; o freccia, è possibile che l&#39;editor di regole non si apra correttamente.

#### AEM Forms su JEE

* Sono state segnalate vulnerabilità di sicurezza critiche per Struts 2 RCE, un framework di applicazioni web popolare e open-source per lo sviluppo di applicazioni web Java™ EE. Adobe rilasciato [AEM 6.5 Service Pack 19.1 (6.5.19.1)](/help/forms/using/mitigating-struts-2-rce-vulnerabilities-for-experience-manager-manager-form.md) per risolvere la vulnerabilità in AEM Forms su JEE.

<!--The font enumeration fails due to the missing Ps2Pdf service file.-->

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in questo [!DNL Experience Manager] 6.5 Service Pack:

* [Elenco dei bundle OSGi inclusi nell’Experience Manager 6.5.20.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi nell&#39;Experience Manager 6.5.20.0](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Iscriviti agli aggiornamenti dei prodotti con priorità Adobe](https://www.adobe.com/subscription/priority-product-update.html)
