---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova informazioni sulla versione, novità, procedure guidate di installazione e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5
mini-toc-levels: 4
source-git-commit: 015c36cad1e7da98888609622cf2150842d40c66
workflow-type: tm+mt
source-wordcount: '3485'
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

### [!DNL Forms]

* **Generazione di rapporti sulle transazioni in AEM Forms su JEE**: è stata introdotta la funzionalità di reporting delle transazioni per AEM Forms su JEE, che consente la registrazione completa delle transazioni relative ai documenti, come conversioni, rappresentazioni e invii. Questo miglioramento aumenta l’efficienza e facilita una migliore conservazione dei documenti. La funzione è disabilitata per impostazione predefinita. Puoi abilitarlo dall’interfaccia utente di amministrazione.
* **Sicurezza avanzata con supporto ECDSA**: AEM Forms ora offre un solido supporto per l’algoritmo ECDSA (Elliptic Curve Digital Signature Algorithm) su entrambi gli stack JEE e OSGi. Gli utenti possono ora firmare, certificare e verificare i documenti di PDF con maggiore sicurezza. Gli algoritmi di curva EC supportati includono:
   * Curva ellittica ECDSA P256 con algoritmo di digest SHA256
   * Curva ellittica ECDSA P384 con algoritmo di digest SHA384
   * Curva ellittica ECDSA P512 con algoritmo di digest SHA512
* **Compatibilità perfetta con Windows 11 per Forms Designer**: AEM Forms Designer ora supporta Windows 11, garantendo un’installazione e un funzionamento senza problemi. Gli utenti possono effettuare l’aggiornamento a Windows 11 senza dover reinstallare Forms Designer o preoccuparsi di problemi di compatibilità, garantendo la continuità del flusso di lavoro.
* **Migliore accessibilità con ruolo &quot;Caption&quot; personalizzato in AEM Forms Designer**: AEM Forms Designer ora include un ruolo di accessibilità personalizzato denominato &quot;Didascalia&quot;, che consente agli utenti di creare XDP con elementi di didascalia personalizzati. Questa funzione migliora l’accessibilità consentendo agli utenti di integrare didascalie personalizzate nelle progettazioni dei documenti in modo da migliorare l’inclusività e l’esperienza utente.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problemi risolti in Service Pack 20 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### Interfaccia utente amministratore{#sites-adminui-6520}

* Il `Workflow Title` il campo è contrassegnato con `*` come richiesto, ma non esiste alcuna convalida. (SITES-16491)

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* Le cartelle di configurazione nidificate non erano più supportate e le cartelle dei modelli per frammenti di contenuto non erano più visibili dopo l’aggiornamento a AEM 6.5.18 o a AEM 6.5.19. (SITES-18110)
* Alcune sottocartelle non sono in grado di scegliere da modelli di frammenti di contenuto ereditati. Deve supportare le cartelle senza `jcr:content` , anche se le cartelle DAM create tramite l’interfaccia utente dispongono di tale nodo. (SITES-17943)

#### [!DNL Content Fragments] - API GRAPHQL {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* Durante l’esecuzione di una query GraphQL in [risultati filtro](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) utilizzando variabili facoltative, se un valore specifico è **non** fornito per la variabile facoltativa, la variabile viene ignorata nella valutazione del filtro. (SITES-17051)

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - API REST{#sites-restapi-6520}

* Con l&#39;aggiornamento del `org.json` libreria, si è verificata una modifica nel modo in cui i numeri decimali sono stati deserializzati. Prima venivano convertiti &quot;per impostazione predefinita&quot; in doppi e ora in BigDecimals. Al contrario, i valori delle proprietà dei metadati, memorizzati tramite l’API REST, devono essere convertiti in Double da BigDecimal. (SITES-16857)

#### Back-end core{#sites-core-backend-6520}

* Quando si utilizza la pubblicazione rapida di un frammento di contenuto, questo continua a essere caricato e non viene pubblicato. In altre parole, la pubblicazione rapida non funziona per i frammenti di contenuto dopo un aggiornamento del service pack da AEM 6.5.7 a AEM 6.5.17. Quando l’utente tentava di eseguire una pubblicazione gestita, questa funzionava. Tuttavia, quando hanno provato la pubblicazione rapida, non veniva pubblicata. In particolare, `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` ha causato il malfunzionamento del sistema. (SITES-17311)
* I frammenti di contenuto non possono essere serializzati con l’esportatore Jackson: il caricamento della pagina si interrompe quando in una pagina viene fatto riferimento a un frammento di contenuto (viene utilizzato il codice di esportazione Jackson) ed eventuali tag aggiunti a un frammento di contenuto. (SITES-18096)

#### Componenti core{#sites-core-components-6520}

* L’installazione del pacchetto dei componenti core CIF sull’AEM causa `:type` valore dei componenti esistenti da modificare. In seguito alla modifica, non verranno più riprodotte sulle pagine a cui sono state aggiunte. (SITES-17601)

#### Integrazione di Campaign{#sites-campaign-integration-6520}

* L’AEM utilizzava un elenco Consentiti di, noto anche come `whitelist`-a causa di un rapporto di vulnerabilità. Il inserisco nell&#39;elenco Consentiti di impediva ai clienti di utilizzare le funzionalità necessarie. (SITES-16822)

#### Frammenti di esperienza{#sites-experiencefragments-6520}

* MSM per frammenti di esperienza ora supporta il rollout in blocco nelle strutture di contenuto dei frammenti di esperienza, incluse cartelle e sottocartelle. (SITES-16004)

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - Live Copy{#sites-msm-live-copies-6520}

* Un &quot;`Is not modifiable`&quot;viene generata un’eccezione durante il rollout del componente. In particolare, un `org.apache.sling.servlets.post.impl.operations.ModifyOperation` si verifica un’eccezione durante l’elaborazione della risposta. (SITES-18809)
* Impossibile eseguire il rollout delle modifiche a specifiche Live Copy di frammenti esperienza. (SITES-17930)
* Quando un utente aggiunge un’annotazione a un componente in una pagina blueprint e poi la esegue su rollout, il conteggio delle annotazioni in Live Copy non viene visualizzato correttamente. (SITES-17099)
* Il pulsante Rollout MSM dalla pagina padre alla pagina figlio è interrotto nell’interfaccia utente grafica touch; se selezionata, viene visualizzato il seguente errore: `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)

#### Editor pagina{#sites-pageeditor-6520}

* L’anteprima dell’Editor temi di Forms è interrotta. Quando si seleziona Anteprima, è visibile solo un&#39;icona di caricamento. (SITES-17164)

### [!DNL Assets]{#assets-6520}

* Impossibile convalidare i campi basati su regole nell’helper dell’editor di metadati e visualizza un messaggio di errore &quot;Campi obbligatori mancanti&quot;. (ASSETS-31396)
* Quando un PDF viene spostato in un&#39;altra posizione, **[!UICONTROL Visualizza pagina]** scompare. (ASSETS-30538)
* Impossibile selezionare un&#39;immagine con autorizzazioni di lettura. (ASSETS-32199)
* Impossibile modificare le dimensioni della scheda nelle impostazioni di visualizzazione. (ASSETS-31667)
* Il caricamento non riesce durante il caricamento del tipo di file .oft. (ASSETS-30109)
* Quando tenti di aggiungere al rapporto un campo di metadati personalizzato come colonna aggiuntiva, le caselle di controllo non sono selezionate. (ASSETS-31671)
* L’operazione di spostamento delle risorse non funziona correttamente in Experience Manager Service Pack 16. (ASSETS-30598)

#### [!DNL Dynamic Media]{#assets-dm-6520}

* Quando una risorsa viene caricata nell’AEM, il `Update_asset` viene attivato il flusso di lavoro. Tuttavia, il flusso di lavoro non viene mai completato. Il flusso di lavoro viene completato solo fino al passaggio di caricamento del prodotto. Il passaggio successivo è il caricamento batch di Scene7, ma tale processo non viene inserito nell’AEM. (ASSETS-30443)
* Hai bisogno di un modo migliore per gestire correttamente i video non Dynamic Medie nel componente Dynamic Medie. Questo problema causava un’istanza di eccezione `dynamicmedia_sly.js`. (ASSETS-31301)
* L’anteprima funziona per tutte le risorse, i set di video adattivi e i video. Tuttavia, genera un errore 403 per `.m3u8` file (che, tra l&#39;altro, funzionano ancora tramite collegamenti pubblici). (ASSETS-31882)
* Il `scene7SmartCropProcessingStatus` stato corretto. Metadati video di ritaglio avanzato utilizzati per mostrare l’errore anche in caso di esito positivo. (ASSETS-31255)

### [!DNL Forms]{#forms-6520}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* Quando un utente tenta di integrare AEM Forms in una piattaforma di posta con un URL pubblicato dell’AEM, AEM Forms non aggiunge `method=post` durante il rendering della pagina. Questo problema si verifica anche se `POST` è impostato nell’azione di invio con l’URL. In questo modo la piattaforma di posta non lo riconosce come forma. (FORMS-12614)
* Quando un utente seleziona il campo data con un modello di visualizzazione in AEM Form Service Pack 6.5.18.0, non può selezionare la data corrente utilizzando la tastiera. (FORMS-12736)
* In AEM Forms Service Pack 6.5.17.0 e Service Pack 6.5.18.0, quando un utente passa da un mese all’altro nel widget del calendario, il componente Selezione data mostra una riga in più. (FORMS-11869)
* Quando un utente fa clic su un’immagine utilizzando &quot;Scatta una foto&quot; nel componente Allegato su un dispositivo iOS, tutte le immagini vengono aggiunte alla cartella con lo stesso nome. (FORMS-12224)
* Quando un utente aggiorna un’opzione esistente in un gruppo di pulsanti di scelta, vengono pubblicati valori di traduzione errati. (FORMS-12575)
* Quando un utente aggiunge caratteri a un modulo adattivo su un dispositivo Android™, può digitare più del numero massimo definito di caratteri nel campo Testo su focus out, su dispositivi Android™. Tuttavia, funziona quando un utente seleziona il tipo di input HTML5. (FORMS-12748)
* A causa delle etichette corrispondenti Arial® etichettate da e Arial®, gli assistenti vocali non sono in grado di distinguere tra queste due. Per risolvere il problema: l’etichetta &quot;aria-labelledby&quot; è sostituita da &quot;aria-descripedby&quot; per i campi modulo. (FORMS-12436)
* Quando un autore utilizza il componente &quot;Forms adattivo - Incorpora (v2)&quot; per incorporare un modulo adattivo nella propria pagina Sites e il modulo incorporato contiene un componente CAPTCHA (CAPTCHA Service -> reCAPTCHA, Settings -> reCAPTCHA-v2), la pagina del sito non viene riprodotta quando l’utente tenta di visualizzare la pagina del sito utilizzando &quot;Visualizza come pubblicato&quot; nell’istanza di authoring. Il seguente errore viene visualizzato come (FORMS-11859):
  `Failed to construct 'URL': Invalid base URL at Object.renderRecaptcha`

* Quando un utente tenta di selezionare la data utilizzando il componente del selettore data, il valore non viene aggiornato e viene visualizzato NULL. (FORMS-12742, FORMS-12736)

* Quando un utente esegue l’aggiornamento a AEM Form Service Pack 6.5.19.0, dopo aver aggiornato una nuova lingua nel dizionario esistente non viene unito alle righe &quot;guideContainer&quot; per aggiungere una lingua a un modulo. (FORMS-12947)

* In AEM Forms Service Pack 6.5.19.0, l’operazione del servizio web richiamata su Java™ 11 non riesce e viene visualizzato l’errore (FORMS-12329):
  `java.lang.NoClassDefFoundError message:sun/misc/BASE64Decoder`

* Quando un utente richiama l’operazione di &quot;ricezione&quot; per &quot;EmailService&quot; su AEM Forms Service Pack 6.5.18.0, viene generata un’eccezione (FORMS-12050):
  `java.util.ServiceConfigurationError: javax.mail.Provider: Provider com.sun.mail.imap.IMAPProvider not a subtype`

* Quando la modalità FIPS è abilitata in AEM Forms Service Pack 6.5.18.0, la creazione di un utente in DOM predefinito non riesce e viene visualizzato l’errore (FORMS-11857):
  `com.adobe.idp.cx.a: error seeding random number generator`

* Quando un utente seleziona i font nell’interfaccia ADMINUI sotto il percorso `Home>Services>PDF Generator>Adobe PDF Settings`, non viene selezionato. Inoltre, in un profilo standard o personalizzato, la casella di riepilogo di Tipi di carattere disponibili è vuota. Di conseguenza, non è possibile personalizzare il sottoelenco di **Incorpora sempre** o **Non incorporare mai**. L’utente non è in grado di configurare il font dei propri PDF con PDF Generator. I registri non mostrano alcun messaggio di errore rilevante. (FORMS-12095)

* In AEM Forms Service Pack 6.5.18.0, l’utente non è in grado di creare le impostazioni di sicurezza, non visualizza alcun errore o registro del server, ma sullo schermo viene visualizzato un messaggio di errore popup. (FORMS-12212)

* Quando un utente su AEM Forms Service Pack 6.5.18.0 invia un modulo adattivo sul flusso di lavoro JEE, l’allegato nel modulo adattivo non viene inviato al processo JEE, causando un errore dell’applicazione. (FORMS-12232, FORMS-12228)

* Quando un utente converte PDF in PDF/A-2b o PDF/A-3B, la conversione non riesce, l’errore viene visualizzato come segue: (FORMS-12790)

  ```
  OCCD contains Order key that does not reference all layers.
  -> Optional content configuration dictionary has no Name entry.
  -> Font not embedded (and text rendering mode not 3).
  obj(65, 0)
  Page: 1
  -> Font not embedded (and text rendering mode not 3).
  obj(67, 0)
  Page: 1
  -> PDF/A entry missing. 
  -> PDF/A entry missing.
  ```

* In AEM Forms 6.5.18.0, quando viene pubblicato un modulo adattivo, tutte le sue dipendenze, inclusi i criteri, vengono ripubblicate, anche se non sono state apportate modifiche. (FORMS-10454)

* Quando un utente seleziona &quot;Microsoft SharePoint&quot; durante l’esecuzione del gestore della configurazione in AEM Forms 6.5.19.1 con la configurazione JBoss® Turnkey, l’installazione del LiveCycle JBoss® EAR non riesce e viene visualizzato il seguente errore: (FORMS-12463)

  ` Caused by: org.jboss.as.server.deployment.DeploymentUnitProcessingException: WFLYEE0031: Unable to process modules in application.xml for EAR ["/C:/AEM/jboss/bin/content/ adobe-livecycle-jboss.ear "], module file adobe-connectorformssharepoint-config-ejb.jar not found.`

#### [!DNL Forms Designer] {#forms-designer-6520}


* Quando un utente effettua l’aggiornamento ad AEM Forms Service Pack 6.5.18.0 a causa di una gestione delle eccezioni mancante, gli XDP passati attraverso il servizio di output con l’opzione PDF con tag abilitata hanno esito negativo. (LC-3921757)

* Quando un utente genera un PDF utilizzando AEM Forms Designer, i livelli di intestazione vengono taggati nella struttura di accessibilità insieme all’elemento grafico, ad esempio una casella di rettangolo. (LC-3921687)

* In AEM Forms Designer installato tramite Workbench, le informazioni sulla versione non sono esplicite nel `Control Panel/Programs/Programs and Features`. (LC-3921976)

<!--* When a user creates an XDP on AEM Forms Designer, the user is not able to add the custom Caption Tag. (LC-3921246)-->

* Quando un utente crea un XDP in AEM Forms Designer, nell’output PDF il tag Button Form non è nidificato nel tag paragrafo principale (p-tag). (LC-3921719)

* Quando un utente crea un XDP in AEM Forms Designer, nell’output PDF quando un utente naviga tra i tag del modulo, viene taggato anche l’oggetto di sfondo. (LC-3921687)

### Foundation {#foundation-6520}

#### Communities {#communities-6520}

* Diagnostica sincronizzazione utenti non riuscita dopo la configurazione della sincronizzazione utenti. (NPR-41693)

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### Integrazioni{#integrations-6520}

* Rimuovi tutto il codice e le dipendenze di Adobe Search&amp;Promote da AEM 6.5. (NPR-40856)

#### Localizzazione{#localization-6520}

* Aria-label &quot;close&quot; non è localizzato in **[!UICONTROL Risorse]** > **[!UICONTROL File]**, seleziona una cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]** > **[!UICONTROL Autorizzazioni]** scheda > nome membro. (NPR-41705)
* La descrizione del comando per il **[!UICONTROL Password archivio chiavi]** nella pagina SSL Setup (Impostazione SSL) per le impostazioni internazionali ENG, FRA, KOR, DEU e PTB. (NPR-41367)

#### Platform{#foundation-platform-6520}

* Problema durante l’integrazione di Campaign con AEM causato dal fatto che il servlet /api non restituisce lo schema corretto nel json href. Il motivo era che l’AEM non stava ricevendo l’intestazione X-Forward-Proto che costrinse la richiesta a rispondere con uno schema HTTP invece che HTTPS. Pertanto, è necessario aggiungere la possibilità di attivare/disattivare la selezione dello schema in base a una configurazione OSGI. (GRANITE-48454)

#### Sling{#foundation-sling-6520}

* Il `org.apache.sling.resourceMerger` il bundle 1.4.2 genera un’eccezione da AEM 6.5, Service Pack 17 e versioni successive. La fusione di risorse Sling 1.4.4 deve essere inclusa in Service Pack 20. (NPR-41630)

#### Traduzione{#foundation-translation-6520}

* In seguito alla distribuzione di AEM 6.5 Service Pack 18, si è verificato un problema con la scheda Filtri nell’Editor delle regole di traduzione. Quando si seleziona un contesto, facendo clic su Modifica > Salva, alla successiva apertura dello stesso contesto viene visualizzata una virgoletta doppia come carattere HTML. In sostanza, le regole di traduzione non venivano salvate correttamente. (NPR-41624)
* Problemi relativi alle traduzioni di frammenti di contenuto, in cui le stringhe tradotte vengono rimandate dal provider di traduzione all’AEM, ma rimangono bloccate nel `/content/projects` senza aggiornare i frammenti di contenuto. (NPR-41516)
* Durante la creazione di una copia per lingua viene visualizzato un messaggio di errore. Si verifica in una pagina in cui è presente un frammento di contenuto a cui si fa riferimento in una proprietà della pagina, utilizzando modelli per frammenti di contenuto. (NPR-41441)
* I collegamenti nei frammenti esperienza non vengono regolati nella lingua corretta durante la copia in lingua. Il frammento di esperienza punta invece alla lingua principale. (NPR-41343)

#### Interfaccia utente{#foundation-ui-6520}

* Si verifica un errore della console dopo un aggiornamento a AEM 6.5, Service Pack 18. L’errore si trova in `coralUI3.js` e si verifica quando si seleziona un elenco a discesa in AEM. Nello specifico, si verifica con un `onOverlayToggle` evento. L’errore `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` viene visualizzato. (NPR-41467)
* Nell&#39;AEM, **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Assegnazione tag]** > **[!UICONTROL Crea]** > **[!UICONTROL Crea tag]**, immissione di caratteri non latini nel **Titolo** causa la **Nome** campo da compilare con il solo trattino ( `-` ). (NPR-41623)
* L&#39;anno di copyright non è corretto in `About Adobe Experience Manager` . (NPR-41526)
* Non tradotti **[!UICONTROL Proprietà profilo]** durante la modifica delle impostazioni utente. Si verifica in tutte le lingue. (NPR-41365)

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


### Problemi noti per AEM Forms {#known-issues-aem-forms-6520}

* Dopo l’aggiornamento da AEM 6.5 Forms Service Pack 18 (6.5.18.0) o AEM 6.5 Forms Service Pack 19 (6.5.19.0) a AEM 6.5 Forms Service Pack 20 (6.5.20.0), gli utenti riscontrano un errore di compilazione JSP. Non possono aprire o creare moduli adattivi e si verificano errori con altre interfacce AEM come l’editor di pagine, l’interfaccia utente di AEM Forms e l’editor di flussi di lavoro AEM. Viene visualizzato un messaggio di errore simile al seguente:

  `Unable to compile class for JSP: An error occurred at line: 162 in the jsp file: /libs/granite/ui/components/coral/foundation/anchorbutton/anchorbutton.jsp The method transformLinkInUriIfExternal(String) is undefined for the type ComponentHelper`

  Per risolvere il problema:

   1. Scarica l’hotfix per il sistema operativo in uso:

   * [Hotfix per Microsoft Windows](/help/release-notes/assets/Hotfix-windows.zip)
   * [Hotfix per Linux](/help/release-notes/assets/Hotfix-Linux.zip)
   * [Hotfix per Apple macOS](/help/release-notes/assets/Hotfix-osx.zip)

   1. Carica e installa il pacchetto (.zip) tramite Gestione pacchetti.

* Il servizio di precompilazione ha esito negativo con un’eccezione NPE nelle comunicazioni interattive. (CQDOC-21355)

<!--Known issues in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of known issues for forms is added to this section post the release.-->

<!--
#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

-->

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
