---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova informazioni sulla versione, novità, procedure guidate di installazione e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5
mini-toc-levels: 4
source-git-commit: 41ef1b05e4082bb50b93ff6511542ed56a77497c
workflow-type: tm+mt
source-wordcount: '3433'
ht-degree: 1%

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
| Versione | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | Giovedì 23 novembre 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] La versione 6.5.19.0 include nuove funzioni, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la disponibilità iniziale della versione 6.5 di aprile 2019. [Installa il service pack](#install) il [!DNL Experience Manager] 6.5

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Alcune delle funzioni e dei miglioramenti principali di questa versione includono:

**Funzioni principali**

* A

**Miglioramenti principali**

* S

**Funzione obsoleta**

* ActiveMQ nell’AEM è obsoleto. ActiveMQ è stato utilizzato per la comunicazione tra due istanze di pubblicazione AEM. L’Adobe consiglia ai clienti di utilizzare ora un load balancer.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problemi risolti in Service Pack 19 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

* U

#### Accessibilità{#sites-accessibility-6519}

* In una pagina di AEM Sites, quando esegui lo zoom del 200% sulla pagina, i collegamenti **[!UICONTROL Copia lingua]** e **[!UICONTROL Rapporto CSV]** nella barra Riferimenti (References) non viene più visualizzata. (SITES-11011) NORMALE

#### Interfaccia utente amministratore{#sites-adminui-6519}

* Canale AEM Screens **[!UICONTROL Anteprima]** non funziona o non viene visualizzata nel dashboard. (SITES-15730) CRITICO
* Durante un’operazione di spostamento della pagina, se l’interfaccia utente non è in grado di visualizzare i riferimenti ma indica che questi vengono ripubblicati automaticamente, vengono *non* ripubblicato. (SITES-16435) PRINCIPALE
* In AEM 6.5 con Service Pack 16 o 17, quando nella visualizzazione a elenco dei siti con la colonna &quot;Flusso di lavoro&quot; abilitata, non è possibile ordinare l’elenco in base agli elementi in tale colonna. Non viene eseguito alcun ordinamento. (SITES-15385) PRINCIPALE
* Per un modello di pagina di reindirizzamento, il campo di reindirizzamento è stato reso obbligatorio. Tuttavia, la convalida del campo obbligatorio non viene applicata né funziona in questi due scenari: quando una pagina viene creata senza un valore di reindirizzamento obbligatorio; non può creare una pagina di reindirizzamento. La convalida non funziona quando si naviga utilizzando i tasti di scelta rapida e quando il campo è contrassegnato come non valido, non procede. (SITES-15903) NORMALE
* Alcuni **Collegamenti in ingresso** non venivano inclusi nel conteggio visualizzato in **Riferimenti** pannello. Ad esempio, il pannello mostrava **Collegamenti in entrata (6)** ma in realtà c&#39;erano nove collegamenti in arrivo. (SITES-14816) NORMALE

#### Interfaccia classica{#sites-classicui-6519}

* Dopo l&#39;installazione dell&#39;hotfix in SITES-15827, i titoli delle finestre di dialogo con spazi tra le parole venivano sostituiti con `" "`. Anche le interruzioni di riga venivano rimosse. (SITES-16089) PRINCIPALE
* I titoli codificati delle finestre di dialogo determinano ora una doppia codifica del titolo. (SITES-15841) NORMALE
* L’aggiornamento dei server AEM dal service pack 6.5.16 al 6.5.17 ha prodotto una doppia codifica per i titoli della finestra di dialogo dell’interfaccia classica. (SITES-15634) NORMALE

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* Nell’Editor frammento di contenuto viene visualizzato il messaggio Errore interno del server. (SITES-13550) CRITICO
* L&#39;aggiornamento del `org.json` tramite NPR-41291 ha causato conversioni di errori di dati in `DefaultDataTypeConverter` del `cfm-impl` pacchetto. La conversione del tipo di dati deve essere più flessibile. (SITES-16473) NORMALE
* Visualizzazione del messaggio di errore: &quot;Impossibile confrontare questa versione del frammento di contenuto con la versione corrente a causa di contenuto non compatibile&quot;. I frammenti di contenuto devono essere comparabili, ma non lo sono. (SITES-16317) NORMALE
* L’URL JS del selettore risorse è stato modificato da
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
a
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068) NORMALE
* Adattare il nuovo schema di risposta API dei metadati Polaris per l’integrazione CFM-Polaris. (SITES-15166) NORMALE
* Tutti i frammenti di contenuto devono essere elencati in cui si fa riferimento al frammento di contenuto selezionato. Al contrario, i riferimenti alle risorse nel pannello dei riferimenti ai frammenti di contenuto mostrano 0 (zero) riferimenti. (SITES-15036) NORMALE

#### Back-end core{#sites-core-backend-6519}

* Migliorare `StyleImpl`. (SITES-15164) NORMALE

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Integrazione di Campaign{#sites-campaign-integration-6519}

* Sul componente firma (`/apps/fpl/components/campaign/signature`), il collegamento Externalizer non funzionava. Se il commento HTML sopra il tag immagine è stato rimosso, il dominio non veniva aggiunto all’origine immagine. Questo problema è stato riscontrato solo con il componente firma nell’ambiente di produzione, non nell’ambiente di staging. (SITES-16120) NORMALE

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### Componenti di base (legacy){#sites-foundation-components-legacy-6519}

* Il componente Adobe Experience Manager (AEM) Sites Search interrompe l’interfaccia utente di. (SITES-15087) NORMALE

#### GraphQL Query Editor{#sites-graphql-query-editor-6519}

* L’interfaccia utente di GraphQL Editor non consente di scorrere tutte le query persistenti in presenza di un numero elevato di query (ad esempio, più di 25). (SITES-16008) PRINCIPALE
* GraphQL Editor non salva lo stato di pubblicazione delle query persistenti. Nell’editor di GraphQL viene visualizzato il pulsante Annulla pubblicazione, ma l’icona che indica che la query persistente è pubblicata non viene visualizzata. L’aggiornamento della pagina mostra che la query persistente non è nemmeno pubblicata. (SITES-15858) PRINCIPALE

#### Lanci{#sites-launches-6519}

* Le modifiche nell’archivio non vengono salvate a causa di `Oak0001` conflitti durante la modifica di più pagine o la creazione del contenuto. È normale eseguire un nuovo tentativo in un evento di questo tipo, ma ciò non si verifica. (SITES-14840) PRINCIPALE

#### MSM - Live Copy{#sites-msm-live-copies-6519}

* Il pulsante di rollout MSM non funziona nell’interfaccia utente grafica touch. (SITES-16991) PRINCIPALE
* Il riferimento collegamento non viene aggiornato all’interno del frammento di esperienza durante la creazione di una Live Copy o il rollout di un frammento di esperienza. (SITES-15460) NORMALE

#### Editor pagina{#sites-pageeditor-6519}

* La selezione di più tipi di file di documento nel filtro del tipo di risorsa non funziona nella console della pagina. Nessun risultato viene trovato anche se sono disponibili i risultati di un particolare tipo di file. Di conseguenza, gli autori non sono in grado di filtrare più documenti. Devono utilizzare più tipi di documenti e devono filtrarli uno alla volta. (SITES-14047) PRINCIPALE
* Dopo aver aggiornato un’istanza da AEM 6.5.17 e AEM 6.5.18, dall’interno dell’Editor pagina, se selezioni **[!UICONTROL Pubblica pagina]**, viene reindirizzato a un URL che non esiste. L’utente deve essere reindirizzato alla procedura guidata di pubblicazione. (SITES-15856) NORMALE
* (SITES-15704) NORMALE
* Copia ridondante dagli Appunti AEM durante un&#39;operazione Incolla dagli Appunti del sistema operativo. (SITES-15704) NORMALE
* In Assets, selezione **[!UICONTROL Documenti]**, quindi sotto **[!UICONTROL Filtertype]**, selezione **[!UICONTROL Microsoft® Word]** o **[!UICONTROL Microsoft® Excel]** non mostra alcun risultato anche se esistono file di entrambi i tipi. (SITES-14837) NORMALE

### [!DNL Assets]{#assets-6519}

* Impossibile distinguere la pubblicazione delle risorse in Experience Manager o Brand Portal. [NPR-41320]
* Quando crei o salvi una cartella pubblica, in un dashboard di amministrazione vengono creati tre gruppi. [ASSETS-26700]
* Nel pannello di ricerca, quando selezioni le caselle di controllo e deselezioni una qualsiasi di esse, tutte le caselle di controllo vengono deselezionate. [ASSETS-26377]

#### [!DNL Dynamic Media]{#assets-dm-6519}

* Dopo il caricamento di una risorsa in AEM, `update_asset` viene attivato il flusso di lavoro. Il flusso di lavoro non viene mai completato. Osservando le istanze del flusso di lavoro, il flusso di lavoro termina con il passaggio di caricamento del prodotto. Il passaggio successivo è il caricamento in batch di scene7. L’utente può vedere che la risorsa si trova in Scene7 dall’app Dynamic Media Classic. (ASSETS-30443) CRITICO
* Un servlet personalizzato (endpoint API) restituisce un nome file Dynamic Medie (Scene7) errato. Si verifica quando una risorsa viene eliminata e sostituita con una risorsa con lo stesso nome. Il servlet personalizzato restituisce il vecchio nome di file Dynamic Medie (Scene7), mentre una chiamata API &quot;jcr&quot; restituisce il nome di file corretto. (ASSETS-29476) PRINCIPALE
* Anche dopo aver disattivato la sincronizzazione a livello di cartella, i registri mostrano il trigger &quot;Scene7 ReplicateOnModifyListener&quot;. Il `ReplicateOnModifyListener/Worker` deve ignorare l’elaborazione di risorse di cartelle e frammenti di contenuto non Dynamic Medie. (ASSETS-26705) PRINCIPALE
* Le persone ipovedenti sono interessate se la messa a fuoco non è visibile negli elementi a discesa (Solo contenuto, Visualizza, Altre opzioni) in modalità bianco e nero ad alto contrasto. (ASSETS-25759) NORMALE
* Le persone ipovedenti sono interessate se il rapporto di contrasto della luminosità per il testo di una pagina è inferiore a 4,5:1. (ASSETS-25756) NORMALE
* Dopo l’invio dei dati, gli assistenti vocali non narrano il messaggio a comparsa visualizzato. (ASSETS-25755) NORMALE
* Gli assistenti vocali non riconoscono punti di riferimento nella pagina (Dynamic Medie; creazione di un profilo di codifica video) se navigano utilizzando il tasto di scelta rapida punto di riferimento/area geografica `D/R`. (ASSETS-25752) NORMALE
* Gli assistenti vocali non riconoscono più punti di riferimento nella pagina (Dynamic Medie; creazione di video interattivi) quando vengono spostati utilizzando il tasto di scelta rapida punto di riferimento/area geografica `D/R`. (ASSETS-25750) NORMALE
* Gli assistenti vocali (NVDA/JAWS/Narrator) non riconoscono i punti di riferimento in **Modifica risorsa** durante la navigazione utilizzando i tasti di scelta rapida `D/R`. (ASSETS-25744) NORMALE
* L’utente riceve un messaggio di processo asincrono vuoto o falso, ma la risorsa connessa è stata pubblicata correttamente. (ASSETS-29342) BANALE

### [!DNL Forms]{#forms-6519}

Correzioni in [!DNL Experience Manager] Forms vengono forniti tramite un pacchetto aggiuntivo separato una settimana dopo il [!DNL Experience Manager] Data di rilascio del Service Pack. In questo caso, il rilascio del pacchetto aggiuntivo Forms AEM 6.5.19.0 è pianificato per giovedì 30 novembre 2023. Un elenco di correzioni e miglioramenti per Forms verrà aggiunto a questa sezione dopo la versione di.

* Aggiunta dell’elenco di controllo di accesso per `fd-cloudservice` per poter leggere o aggiornare le configurazioni di Microsoft® in `cloudconfigs/microsoftoffice`. (FORMS-11142) NORMALE

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

### Foundation{#foundation-6519}

* La creazione di una copia per lingua a livello di directory principale della lingua non regola i percorsi nella pagina. Nel caso in cui sia stata creata la copia per lingua, non per la directory principale della lingua ma per le pagine al suo interno, il percorso è cambiato correttamente. (NPR-41364) PRINCIPALE
* La descrizione comando &quot;Relative Date Presentation&quot; (Presentazione data relativa) può essere chiusa solo premendo ESC sulla tastiera. La descrizione deve chiudersi quando l’utente seleziona una parte dell’interfaccia utente. (NPR-41394) NORMALE
* Stringa non localizzata `Something went wrong while adding the private key.` quando si aggiunge un file di chiave privata errato in **Modifica utente** > **Registro chiavi**. (NPR-41366) NORMALE
* Sono necessarie icone per Microsoft® SharePoint e Microsoft® One Drive nell&#39;ambiente AEM 6.5. (NPR-41354) NORMALE
* Mancata corrispondenza ID utente/password non localizzata. stringa in **Sicurezza** > **Utente** > **Crea** . (NPR-41245) NORMALE
* Il codice popover e i gestori eventi vengono caricati due volte, interrompendo le interfacce utente basate su Coral3 create dall&#39;utente. (NPR-41171) NORMALE
* La deselezione non funziona correttamente dopo aver utilizzato &quot;Seleziona tutto&quot; nella console AEM Sites. (NPR-41304) NON GRAVE

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### Integrazioni{#integrations-6519}

* I collegamenti SMS in una campagna e-mail AEM non sono scritti correttamente; contengono un elemento di ancoraggio HTML. (NPR-41211) PRINCIPALE
* Il testo utilizzato nella schermata di configurazione dell&#39;account non deve utilizzare il nuovo tipo di credenziali. (NPR-41210) NORMALE
* Spostamento dello scheduler di importazione report di Analytics da `ManagedPollConfig` ai processi sling. Quando due diversi framework di analisi sono stati allegati con suite di rapporti diverse a due siti diversi, `ManagedPollConfig` ne urla solo uno. (NPR-41209) NORMALE
* Quando il valore viene reimpostato sul valore predefinito, il pulsante dell’intervallo temporale selezionato in precedenza rimane attivato. Nel dashboard di approfondimenti sul contenuto dell’AEM, per impostazione predefinita l’intervallo di tempo è impostato sulla settimana e mostra gli approfondimenti sul contenuto come dati settimanali. Ora, se l’utente seleziona altre opzioni per l’intervallo di tempo, ad esempio ora, giorno, mese e anno, i dati cambiano in base al valore selezionato. Tuttavia, se i valori vengono reimpostati, per impostazione predefinita l’intervallo di tempo visibile è settimana, ma viene comunque selezionata l’opzione intervallo di tempo selezionato in precedenza. (NPR-41246) NON GRAVE

#### Oak{#oak-6519}

* L&#39;utilità Backport consente di limitare le scritture su AEM in caso di ritardo dell&#39;indicizzazione asincrona. (NPR-40985) PRINCIPALE

#### Platform{#foundation-platform-6519}

* Le query QueryBuilder con parentesi quadre non vengono convertite correttamente in xpath. (NPR-41298) NORMALE

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### Progetti di traduzione{#foundation-translation-6519}

* Durante la creazione della copia per lingua della pagina &quot;A&quot;, deve creare automaticamente le copie per lingua delle pagine, dei frammenti di esperienza, dei frammenti di contenuto e delle risorse a cui si fa riferimento. Inoltre, la nuova copia per lingua della pagina &quot;A&quot; nel nuovo percorso deve avere i suoi riferimenti aggiornati alle rispettive copie per lingua appena create delle pagine, dei frammenti di esperienza, dei frammenti di contenuto e delle risorse. (NPR-41076) NORMALE

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### Flusso di lavoro{#foundation-workflow-6519}

* Impossibile completare un&#39;attività nella casella in entrata. Quando si tenta di completare l’attività e selezionare un’azione, nel menu a discesa viene visualizzato solo un valore &quot;non definito&quot;. Ciò significa che gli utenti non possono applicare il service pack AEM 6.5.18. (NPR-41402) PRINCIPALE
* Impossibile completare le attività nella casella in entrata. Nell’elenco a discesa non è presente alcun valore (solo &quot;indefinito&quot;) quando si tenta di completare l’attività per i file ZIP, i rapporti sulle risorse, lo spostamento (riuscito o non riuscito) o la scadenza delle risorse. (NPR-41305) PRINCIPALE
* Quando un utente seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > istanze, quindi seleziona il flusso di lavoro in esecuzione e fai clic su **[!UICONTROL Visualizza payload]**, genera una pagina di errore 500. (NPR-41325) NORMALE


## Installa [!DNL Experience Manager] 6.5.18.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0 richiede [!DNL Experience Manager] 6.5. Cfr. [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate. <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del service pack è disponibile su Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip).
* In una distribuzione con MongoDB e più istanze, installa [!DNL Experience Manager] 6.5.19.0 in una delle istanze di authoring che utilizzano Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> L’Adobe non consiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.19.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup del `crx-repository` nel caso in cui sia necessario riportarlo indietro. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installare il service pack in [!DNL Experience Manager] 6,5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia di riavviare se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup del file [!DNL Experience Manager] dell&#39;istanza.

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Consulta [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta si apre una finestra di dialogo sull’interfaccia utente di Gestione pacchetti durante l’installazione del service pack. L’Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di avere la certezza che l’installazione sia andata a buon fine. In genere, questo problema si verifica in [!DNL Safari] ma può verificarsi in modo intermittente su qualsiasi browser.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente [!DNL Experience Manager] 6.5.19.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserisci la confezione in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza il [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` affinché i pacchetti nidificati vengano installati.

>[!NOTE]
>
>L&#39;Experience Manager 6.5.19.0 non supporta l&#39;installazione Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalidare l’installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo di questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa della versione aggiornata `Adobe Experience Manager (6.5.19.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (usa la console web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.16 o successiva (utilizzare la console Web: `/system/console/bundles`). <!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installa Service Pack per [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Per istruzioni sull&#39;installazione del service pack in Experience Manager Forms, vedere [Istruzioni di installazione di Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funzione di AEM Forms, ad esempio Forms adattivo, disponibile in [QuickStart per AEM 6.5](https://experienceleague.corp.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html), sono destinati esclusivamente a scopi di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms.



### Installare il pacchetto di indice GraphQL per frammenti di contenuto Experience Manager{#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare [Frammento di contenuto di Experience Manager con pacchetto indice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

In questo modo puoi aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate.

Se non si installa questo pacchetto, è possibile che le query GraphQL risultino lente o non riuscite.

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar{#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.19.0 è disponibile nel [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come usare UberJar](/help/sites-developing/ht-projects-maven.md) e includere la seguente dipendenza nel POM del progetto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece che nell’archivio Maven pubblico di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Quindi, non c&#39;è `classifier`, con `apis` come valore, per `dependency` tag.

## Funzioni obsolete e rimosse{#removed-deprecated-features}

Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md/).

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* **La pubblicazione delle pagine non funziona nell’Editor pagina dopo l’aggiornamento a Service Pack 18 (6.5.19.0)**

  <!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0--> Dopo aver aggiornato un&#39;istanza di AEM AEM 6.5.0.0—6.5.17.0 a 6.5.19.0, quando si fa clic su **Pubblica pagina** Nell’Editor pagina, vieni reindirizzato a un URL che non esiste.

  Per risolvere il problema, eseguire una delle operazioni seguenti:

   * Rimuovi la seguente proprietà &quot;path&quot;.

     `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

   * Incolla l’URL corretto direttamente nel browser.

     `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html`



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

* Le versioni JDK superiori a 1.8.0_281 non sono supportate per il server WebLogic JEE. (FORMS-8498, CQDOC-20383)
* As [!DNL Microsoft® Windows Server 2019] non supporta [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] non supporta le installazioni chiavi in mano per [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20 non è supportato per installare AEM Forms sul programma di installazione JEE. Per installare AEM Forms sul programma di installazione di JEE sono supportate solo JDK 11.0.19 o versioni precedenti. (FORMS-10659)

#### Installazione

* Sulla piattaforma JBoss® 7.1.4, quando l’utente installa il service pack Experience Manager 6.5.16.0 o versione successiva, `adobe-livecycle-jboss.ear` distribuzione non riuscita. (CQ-4351522, CQDOC-20159)
* Dopo l’aggiornamento a AEM Forms 6.5.18.0 JBoss® Turnkey Full Installer Environment in Windows Server 2022, durante la compilazione del codice dell’applicazione client di output utilizzando Java™ 11, può verificarsi il seguente errore di compilazione:

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  Per risolvere il problema, effettuare le seguenti operazioni:
   1. Accedi a `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` e decomprimi `adobe-output-client.jar` per estrarre `Manifest.mf` file.
   1. Aggiornare il `Manifest.mf` rimuovendo la voce `${clover.jar.name}` dall&#39;attributo class-path.

      >[!NOTE]
      >
      > È inoltre possibile utilizzare uno strumento di modifica locale, ad esempio 7-zip, per aggiornare `Manifest.mf` file.

   1. Salva il file aggiornato `Manifest.mf` nel `adobe-output-client.jar` archivio.
   1. Salva il file modificato `adobe-output-client.jar` ed eseguire di nuovo l&#39;installazione. (CQDOC-20878)
* Dopo aver installato il programma di installazione completo AEM Service Pack 6.5.19.0, l’implementazione EAR non riesce su JEE utilizzando JBoss® Turnkey.
Per risolvere il problema, individuare `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` file e aggiornamento `Adobe_Adobe_JAVA_HOME` a `Adobe_JAVA_HOME` per tutte le occorrenze prima di eseguire gestione configurazione. (CQDOC-20803)

#### Moduli adattivi

* Quando viene pubblicato un modulo adattivo, tutte le sue dipendenze, inclusi i criteri, vengono ripubblicate, anche se non sono state apportate modifiche. (FORMS-10454)
* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata nel Browser proprietà. Per risolvere il problema, fai clic su per configurare un altro campo del modulo adattivo nello stesso editor.
* Quando un URL di reindirizzamento viene impostato nel contenitore guida di un modulo adattivo, la firma in linea non funziona più. (FORMS-10493)
* Non è possibile pubblicare tutti i modelli di documento record (DoR). Vengono pubblicati solo i modelli DoR basati sulle impostazioni internazionali inglesi e i relativi modelli DoR basati su Forms associati. (FORMS-10535)

#### Comunicazioni interattive

* Dopo l’aggiornamento a AEM Service Pack 18, non è possibile aprire la comunicazione interattiva con grandi immagini in linea in modalità Modifica. (FORMS-10578) Per risolvere il problema, effettua le seguenti operazioni:

   1. Scarica [Hotfix-FORMS-10578](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) dal collegamento SD.
   1. Estrai il file di archivio Hotfix per ottenere un pacchetto Experience Manager (.zip) e i file bundle (.jar).
   1. Carica e installa il pacchetto (.zip) tramite Gestione pacchetti.
   1. Apri i bundle di Gestione configurazione `https://server:host/system/console/bundles`, carica e installa il bundle (.jar).

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.19.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Elenco dei bundle OSGi inclusi nell’Experience Manager 6.5.19.0](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi nell&#39;Experience Manager 6.5.19.0](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)
