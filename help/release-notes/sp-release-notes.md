---
title: Note sulla versione di AEM 6.5 Service Pack
description: Note sulla versione specifiche di Adobe Experience Manager 6.5 Service Pack 3.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: bd0b8e1605f6d8f6cc04a4173731351df002a67d

---


# Note sulla versione di Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | **Adobe Experience Manager 6.5** |
|---|---|
| Versione | 6.5.3.0 |
| Tipo | Versione Service Pack |
| Data | 12 dicembre 2019 |
| URL di download | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0), distribuzione [software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aem.html#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.3.zip) |

## Contenuto in Adobe Experience Manager 6.5.3.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. Può essere installato sopra Adobe Experience Manager (AEM) 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.6.

* Experience Manager Assets ora supporta gli archivi ZIP creati utilizzando l&#39;algoritmo Deflate 64.

* La nuova colonna relativa alla data di creazione, ordinabile, è stata aggiunta nella visualizzazione a elenco DAM e nei risultati della ricerca di risorse nella visualizzazione a elenco.

* L’ordinamento delle risorse basato sulla colonna Nome è stato attivato nella visualizzazione Elenco.

* Dynamic Media ora supporta le risorse video SmartCrop. Smart Crop è una funzione guidata di apprendimento automatico che ritaglia un video mentre si sposta il fotogramma per seguire il punto focale della scena.

* Dynamic Media supporta le immagini intelligenti.

* Possibilità di [impostare le preferenze di Office](../forms/using/configure-out-of-office-settings.md) nei flussi di lavoro AEM.

* Possibilità di [condividere elementi](../forms/using/configure-shared-queues-osgi.md) Inbox o Inbox con altri utenti nei flussi di lavoro AEM.

* Possibilità di [generare comunicazioni interattive in modalità](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

* È stata aggiornata la versione di jQuery inclusa nel pacchetto ContextHub alla 3.4.1.

### Elenco delle modifiche {#list-of-changes}

#### Assets {#assets-6530-enhancements}

**Miglioramenti apportati al prodotto**

* Experience Manager Assets ora supporta gli archivi ZIP creati con l&#39;algoritmo Deflate 64 (NPR-27573).

* La nuova colonna relativa alla data di creazione, ordinabile, è stata aggiunta nella visualizzazione a elenco DAM e nei risultati della ricerca di risorse nella visualizzazione a elenco (NPR-31312).

* L&#39;ordinamento delle risorse in base alla colonna Nome è stato consentito nella vista Elenco (NPR-31299).

* I file di risorse GLB, GLTF, OBJ e STL supportano l’anteprima delle risorse nella pagina Dettagli risorsa in DAM (CQ-4282277).

* L&#39;evento ReplicationOnModifyListener viene attivato per i nodi di blocco durante il caricamento di blocchi in elementi multimediali dinamici (CQ-4281279).

* Dynamic Media ora supporta le risorse video SmartCrop. Smart Crop è una funzione guidata per l&#39;apprendimento automatico che ritaglia un video mentre si sposta il fotogramma per seguire il punto focale della scena (CQ-4278995).

* Dynamic Media supporta la funzione Smart Imaging (CQ-422249).

* La visualizzazione di ricerca/ricerca è stata impostata come visualizzazione predefinita nel selettore Foundation se i parametri di query vengono passati nella richiesta (NPR-31601).

**Problemi risolti**

* I metadati di alcuni documenti PDF non vengono aggiornati e salvati nel PDF quando si modifica il titolo (NPR-31629).

* La condivisione delle risorse non funziona per le risorse con il carattere &quot;+&quot; nei loro nomi (NPR-31547).

* Le modifiche nel modulo di ricerca predefinito Assets Admin * Search Rail non funzionano come previsto (NPR-31502).

* I suggerimenti non vengono visualizzati quando si utilizza Omnisearch nella visualizzazione delle risorse per la ricerca delle risorse (NPR-31496).

* I riferimenti alle risorse all&#39;interno delle raccolte non vengono aggiornati quando le risorse di riferimento vengono spostate in un&#39;altra posizione, nei casi in cui a una raccolta diversa fanno riferimento le stesse risorse da parte di utenti diversi (NPR-31486).

* I tag IPTC duplicati vengono aggiunti ai metadati delle risorse (NPR-31328).

* Il conteggio dei risultati della ricerca nell&#39;angolo in alto a destra non si aggiorna con precisione quando la ricerca viene attivata dalla barra laterale del filtro (NPR-31316).

* Tutte le caselle di controllo vengono deselezionate quando si deseleziona la casella di controllo di secondo livello nel filtro Tipo file e il testo nella barra di ricerca non è sincronizzato con le proprietà selezionate o non selezionate (NPR-31287).

* Tutti i membri (utenti/gruppi) non possono essere rimossi dalla sezione Membri di una cartella; quando si tenta di rimuovere tutti gli utenti, l&#39;utente connesso viene aggiunto all&#39;elenco (NPR-31171).

* Impossibile eliminare le risorse con il simbolo &quot;+&quot; nel nome del file (NPR-31162).

* Il menu a discesa Crea, visibile nel menu principale quando si seleziona una cartella, non mostra l&#39;opzione &quot;Cartella&quot; come opzione di creazione (NPR-30877).

* Selezione cartella L&#39;elemento dell&#39;azione Crea > Caricamento file non è presente quando ACL per Rifiuta jcr:removeChildNodes e jcr:removeNode sul percorso vengono applicati a un utente (NPR-30840).

* I flussi di lavoro DAM diventano obsoleti quando vengono caricate determinate risorse mp4, causando il blocco di tutti i flussi di lavoro rimanenti (NPR-30662).

* Errore di memoria insufficiente quando un file PDF di grandi dimensioni (di diversi Gigabyte) viene caricato in DAM e le relative risorse secondarie vengono elaborate (NPR-30614).

* Lo spostamento di massa delle risorse non riesce e viene visualizzato un messaggio di avviso (NPR-30610).

* I nomi delle risorse vengono modificati in lettere maiuscole quando si spostano le risorse da una cartella all’altra in AEM, in esecuzione in modalità di esecuzione Dynamic Media Scene 7 (NPR-31630).

* Durante la modifica di un set di immagini remoto, si verifica un errore per l’immagine che risiede nella cartella denominata come nome della società Scene 7 (NPR-31340).

* Le risorse multimediali dinamiche contenenti riferimenti non vengono pubblicate (NPR-31180).

* I caricamenti da AEM Dynamic Media - La modalità di esecuzione di Scene7 su Scene7 richiedono troppo tempo per essere completati (NPR-31048).

* L’area sensibile aggiunta a una risorsa immagine non è visibile tramite il visualizzatore immagini interattivo nella pagina dei dettagli della risorsa (NPR-30979).

* Vengono creati enormi processi di sling e il banner di elaborazione viene nuovamente visualizzato quando le azioni eseguite sulle risorse in AEM Assets vengono passate a Scene7 (NPR-30947).

* Si verifica un conflitto durante la creazione della copia in lingua delle risorse e delle risorse non caricate in Scene7 (NPR-30932).

* Le rappresentazioni dinamiche scaricate da AEM in esecuzione in modalità Dynamic Media Hybrid sono interrotte (sono di tipo testo con contenuto &quot;impossibile trovare l&#39;immagine&quot; invece del tipo di contenuto dell&#39;immagine) (NPR-30876).

* Il flusso di lavoro Codifica video elemento multimediale dinamico non riesce a generare la miniatura per il video migrato da Scene7 a Contenuti multimediali dinamici - Modalità di esecuzione di Scene7 (CQ-4282011).

* IpsApiException durante la migrazione delle risorse da un’istanza all’altra tramite ID società Scene7 diversi (CQ-4280548).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene assimilato in AEM (CQ-4283701).

* I pulsanti di scorrimento vengono visualizzati nel visualizzatore, se una risorsa 3D dispone di poche viste della fotocamera (CQ-4283322).

* Altezza contenitore errata di un modello 3D caricato visualizzato in anteprima nel visualizzatore dimensionale nella pagina Dettagli risorsa (CQ-4283309).

* I video non possono essere riprodotti con SmartCropVideoViewer su Internet Explorer 11 e Safari (CQ-4281422).

* L’utilizzo del pulsante Sposta per spostare più risorse, da una cartella all’altra, non riesce in AEM su Dynamic Media - modalità di esecuzione di Scene7 (CQ-4280384).

* I video distorti vengono visualizzati sui dettagli delle risorse quando il tipo MIME è diverso da MP4 (CQ-4279704).

* I video appena caricati in cartelle con profilo video restano nello stato di elaborazione anche dopo il completamento della percentuale di codifica al 100% (CQ-4279389).

* Lo spostamento delle risorse da una cartella crea un numero elevato di processi sling (chiamate API di Scene7) rispetto a quanto richiesto idealmente (CQ-4278664).

* In Scene 7, i nomi dei set di immagini vengono modificati in minuscolo quando viene creato un set di immagini (o un set di file multimediali) e vengono denominati con la convenzione di denominazione appropriata in DAM (CQ-4281112).

* Scene7 Migrator imposta lo stato di pubblicazione in modo errato (CQ-4263492).

* La ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) nella pagina dei risultati scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente nei frammenti di contenuto (CQ-4282898).

* I file PDF non sono indicizzati e il contenuto al loro interno non è ricercabile (CQ-4278916).

* Errore &quot;Gruppo non elencato dal selettore utente: previsto da false a uguale a true&quot; viene osservato per l&#39;aggiunta di Closed User Group con different `principalName` and `authorizableId` (CQ-4278177).

* La vista a colonne dell&#39;interfaccia utente delle risorse mostra tutti i percorsi indipendentemente dal percorso radice del tenant specifico (CQ-4278175).

* La ricerca del selettore delle risorse non funziona come previsto (CQ-4275886).

* Flussi di lavoro di rappresentazione non riusciti (CQ-4271928).

* DAM Event Purge elimina i dati evento più recenti (maxSavedActivities) e li contiene i dati creati in precedenza (NPR-31336).

* La pagina dei risultati della ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente (NPR-31307).

* La barra delle azioni e il conteggio delle risorse non si aggiornano quando si selezionano tutti gli elementi (cartelle o singole risorse) nell&#39;interfaccia utente touch (NPR-31118).

* In AEM viene visualizzata un’eccezione durante il polling per i dettagli del processo relativi a una risorsa (CQ-4283569).

#### Sites {#sites}

* Se l&#39;ereditarietà LiveCopy è interrotta, nelle pagine di LiveCopy sono visualizzati i collegamenti per la copia della lingua invece dei collegamenti LiveCopy (NPR-30980).
* Per una nuova Blueprint, Se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza righe vuote per gli altri record (NPR-31182).
* Quando un utente aggiunge caratteri giapponesi o coreani nella proprietà description di un menu, nel menu vengono visualizzati caratteri distorti per il testo in giapponese e in coreano. (NPR-31331).
* Editor Rich Text (RTE) non consente di inserire una tabella incorporata come voce di elenco (NPR-30879).
* Escluso, scaffolding Rich Text Editor (RTE). applica la dimensione del font in linea agli elementi, in modo imprevisto (NPR-31284).
* Quando un utente sposta lo stato attivo sui campi della barra a sinistra e utilizza una scelta rapida da tastiera per incollare il contenuto, viene incollato il contenuto degli Appunti dell’Editor pagina invece del contenuto copiato dai campi della barra a sinistra (NPR-31172).
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso dell’immagine viene memorizzato nel nodo componente invece del nodo multi-campo (NPR-30882).
* L&#39;API ResponsiveGridExporter non restituisce l&#39;interfaccia com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Il pacchetto com.day.cq.wcm.foundation.model.impl è dichiarato pacchetto privato (NPR-31398).
* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il `editor.html` prefisso e, `wcmmode=disabled`o in Publisher)., la richiesta termina con il codice di errore dello stato HTTP 500 (NPR-30743).
* Gli utenti non possono modificare la password e accedere alla pagina del profilo (NPR-31161).

#### Ricerca e interfaccia utente {#search-ui-interface}

* Quando si passa dalla vista Scheda alla vista Elenco in una pagina dei risultati di ricerca, si verifica un ritardo prima dello scorrimento della pagina (NPR-31286).

* La casella di controllo Seleziona tutto è nascosta nella vista Elenco dell&#39;interfaccia utente Siti (NPR-31614).

* Il conteggio Seleziona tutto in una pagina di risultati della ricerca non è corretto (NPR-31120).

* L&#39;editor di metadati visualizza i tag che non esistono (NPR-31119).

#### Traduzione {#translation}

* Due finestre a comparsa del calendario vengono visualizzate quando si seleziona l&#39;opzione Data scadenza in un processo di traduzione (NPR-31270).

#### Platform {#platform}

* L&#39;opzione Tipo mime nella console Web non funziona (NPR-31108).

* Il certificato client non è accettato durante la configurazione del single sign-on (NPR-31165).

* Gli aggiornamenti nella configurazione della dimensione del buffer per il servizio HTTP basato su Jetty non vengono salvati (NPR-30925).

* QueryBuilder supporta ora l&#39;ordine ``fn:name()`` nelle query xpath (NPR-31322).

* La struttura di attivazione duplicata viene creata al momento dell&#39;aggiornamento da AEM 6.3 (NPR-31513).

* Le richieste inoltrate non conservano le intestazioni di risposta impostate durante l&#39;autenticazione Sling (NPR-30013).

* La ricerca all&#39;interno dei componenti del selettore non funziona (NPR-31692).

* Viene visualizzato un errore quando si allega un file ZIP a un post di AEM Communities a causa di versioni diverse del bundle Apache POI e Apache Tika (NPR-31018).

* Il ``org.apache.sling.distribution.api`` bundle è nascosto nel gestore di configurazione e pertanto non è disponibile per i bundle personalizzati (NPR-31720).

#### Progetti {#projects}

* La sostituzione delle viste del calendario non funziona (NPR-31271).

#### Brand Portal {#assets-brand-portal}

**Miglioramenti apportati al prodotto**

* Il flusso di lavoro di importazione di Asset Sourcing in AEM Assets viene modificato per recuperare solo le risorse create di recente da Brand Portal ad AEM e per ignorare le risorse già presenti nella NUOVA cartella per evitare la replica (CQ-4278527).

**Problemi risolti**

* Quando si crea una nuova cartella Contribution nella funzione Asset Sourcing (CQ-4282825), viene visualizzata un’icona errata.
* Quando create una nuova cartella Contribution, una o entrambe le sottocartelle (NEW e SHARED) non vengono visualizzate all’interno della cartella Contribution (CQ-4282424).
* Il sistema genera un’eccezione se l’utente tenta di ripubblicare la cartella Contribution da AEM a Brand Portal dopo aver ricevuto nuove risorse nella cartella Contribution da Brand Portal end (CQ-4279740).
* La creazione di una cartella Contribution all’interno di una cartella Contribution (cartella nidificata) non è consentita per evitare la complessità (CQ-4278391).
* Il sistema genera un’eccezione durante il caricamento dell’elenco di utenti Brand Portal (file .csv) importato da AEM Admin Console. Nel file .csv sono obbligatori solo i campi Email, FirstName e LastName (CQ-4278390).

#### Communities {#communities}

**Problemi risolti**

* I collegamenti rapidi per gestire i gruppi (Open/Edit/Publish/Delete Groups) non sono visibili agli amministratori della community (Group admin/Site admin) (NPR-31627).
* Un blog inviato viene visualizzato solo se la pagina viene aggiornata/ricaricata manualmente (NPR-31599).
* La query JCR utilizzata dalla funzione &quot;Mentions&quot; è sensibile alle maiuscole/minuscole e richiede troppo tempo per restituire i risultati (NPR-31475).
* Il file UberJar di AEM 6.5 genera un&#39;eccezione, `cq-social-translation` bundle mancante nel file UberJar di AEM 6.5 (NPR-31186).
* Librerie Databind di Jackson aggiornate alla versione 2.9.9.3 per risolvere nuove vulnerabilità (NPR-30967).
* I titoli di Attività e Notifiche non sono coerenti (NPR-30941).
* La paginazione non funziona correttamente nei blog di Communities (NPR-30914).
* I rapporti di Analytics non vengono compilati nell’ambiente di authoring di AEM. Viene visualizzata una pagina vuota (NPR-30913).

#### Quercia {#oak}

* Aggiornamenti dell&#39;indice Lucene che rallentano il server di creazione (NPR-31548).

#### Forms {#forms-6530}

>[!NOTE]
>
>Il Service Pack di AEM non include le correzioni per AEM Forms. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per AEM Forms su JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Pacchetto di componenti aggiuntivi per Forms {#forms-add-on-package-6530}

**Moduli adattivi**

* Le stringhe contengono la chiave del dizionario durante la localizzazione dei moduli adattivi (NPR-31110).

**Comunicazione interattiva**

* **MissingNode.toString()** restituisce risultati imprecisi dopo aver aggiornato le librerie Jackson a 2.10.0 (NPR-31549).

* L&#39;editor di testo rimuove in modo casuale gli spazi dal testo copiato da Microsoft Word (NPR-31113).

**Gestione della corrispondenza**

* Le didascalie e le descrizioni comandi non vengono visualizzate durante la migrazione delle lettere da LiveCycle ES4SP1 ad AEM 6.5 (NPR-31615).

* **Durante il salvataggio delle lettere come bozze (NPR-30463), la formattazione del flusso di testo non è più supportata** .

**Flusso di lavoro**

* Il flusso di lavoro OSGi non riesce a causa dell&#39;utilizzo della CPU al 100% (NPR-31233).

**Moduli HTML5**

* Quando si genera l’anteprima HTML5 di un modulo XDP, viene visualizzato uno sfarfallio durante l’aggiunta di istanze di un sottomodulo (NPR-30909).

##### Moduli sul programma di installazione JEE {#forms-jee-installer-6530}

**Forms - Servizi basati su documenti**

* Il servizio Web SOAP che utilizza MTOM in un progetto .NET visualizza le eccezioni per i metodi AssemblerServiceClient invoke e HtmlToPDF2 (NPR-4281771).

**JEE per Foundation**

* La configurazione dell&#39;azione non carica i nomi dei processi per l&#39;azione di invio di un flusso di lavoro moduli (NPR-31478).

### Feature Pack inclusi {#feature-packs-included-6530}

>[!NOTE]
>
>Per i clienti di AEM Forms, è essenziale installare il pacchetto dei componenti aggiuntivi per AEM Forms dopo l’installazione del Service Pack, del Cumulative Fix Pack o del Feature Pack di AEM.

#### Forms - JEE di base {#forms-foundation-jee-feature}

* Supporto di AEM Forms per Oracle 18c (NPR-29155).

## Install 6.5.3.0 {#install}

**Requisiti di configurazione**

* AEM 6.5.3.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Il download del Service Pack è disponibile in Condivisione pacchetti Adobe, a cui puoi accedere direttamente dall’istanza di AEM 6.5.
* In una distribuzione con MongoDB e più istanze, installa AEM 6.5.3.0 in una delle istanze Autore tramite Gestione pacchetti.
* Prima di installare il Service Pack, assicurati di disporre di uno snapshot o di un nuovo backup dell’istanza AEM.
* Riavvia l’istanza prima dell’installazione. Anche se questa operazione è necessaria solo quando l’istanza è ancora in modalità di aggiornamento (e questo accade quando l’istanza è stata aggiornata da una versione precedente), è consigliabile riavviare l’istanza se questa è rimasta in esecuzione per un periodo più lungo.

>[!CAUTION]
>
>Adobe sconsiglia la rimozione o la disinstallazione del pacchetto AEM 6.5.3.0.

### Installare il Service Pack tramite Condivisione pacchetti {#install-service-pack-via-package-share}

Per installare il Service Pack in un’istanza AEM 6.5 esistente, effettua le seguenti operazioni:

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.3.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. Installa il pacchetto scaricato utilizzando Gestione pacchetti.

>[!NOTE]
>
>**La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude prematuramente durante l’installazione della versione 6.5.3.0**
>
>È consigliabile attendere che i registri degli errori si stabilizzino prima di accedere all’istanza. L&#39;utente deve attendere i registri specifici relativi alla disinstallazione del bundle dell&#39;utility di aggiornamento prima di assicurarsi che le installazioni abbiano esito positivo. Il problema si verifica in genere in Safari, ma può accadere in modo intermittente in qualsiasi browser.

**Installazione automatica**

Esistono due modi per installare automaticamente AEM 6.5.3.0 in un’istanza in esecuzione:

A. Inserite il pacchetto in ..*/crx-quickstart/install* cartella mentre il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.3.0 non supporta l’installazione tramite bootstrap.

**Convalidare l’installazione**

1. Nella pagina Informazioni sul prodotto (/system/console/ productinfo) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager, Version 6.5.3.0` in Prodotti installati.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. Il bundle OSGI org.apache.jackrabbit.oak-core è sulla versione 1.10.6 o successiva (Usa console Web: /system/console/bundle).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms. Le correzioni apportate in AEM Forms vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi.

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Se si utilizza una versione precedente del pacchetto di compatibilità AEM Forms e si aggiorna a AEM 6.5.3.0, installare la versione più recente del pacchetto di compatibilità AEM Forms dopo l&#39;installazione del pacchetto di componenti aggiuntivi Forms.

1. Assicurati di aver installato il Service Pack di AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Le correzioni in AEM Forms su JEE vengono distribuite tramite un programma di installazione separato.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Programma di installazione di Workbench

Poiché si tratta di un programma di installazione completo, la dimensione del file è maggiore rispetto alla versione della patch. Disinstallare la versione precedente di Workbench prima di installare la nuova versione.

## UberJar {#uber-jar}

The UberJar for AEM 6.5.3.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Funzioni obsolete {#removed-deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete con AEM 6.5.3.0. Le funzioni pianificate per essere rimosse in una versione futura sono impostate per prime su obsoleto, con un&#39;opzione alternativa da utilizzare.

Si consiglia ai clienti di verificare se utilizzano la funzionalità o la funzionalità nella distribuzione corrente e di pianificare la modifica della propria implementazione per utilizzare l&#39;opzione alternativa.

| Area | Funzione | Sostituzione |
|---|---|---|
| Integrazioni | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Con l&#39;integrazione AEM e Target aggiornata in AEM 6.5 per supportare l&#39;API di Target Standard, che utilizza l&#39;autenticazione tramite Adobe IMS e I/O, e con il ruolo crescente di Adobe Launch nella strumentazione delle pagine AEM per l&#39;analisi e la personalizzazione, la procedura guidata di consenso è diventata funzionalmente irrilevante. | Configurare le connessioni di sistema, l&#39;autenticazione Adobe IMS e le integrazioni Adobe I/O tramite i rispettivi servizi cloud AEM |

## Problemi noti {#known-issues}

* Se la configurazione **delle risorse** connesse restituisce un messaggio di errore 404 dopo l’installazione di AEM 6.5.3.0, reinstallate manualmente i pacchetti di componenti **** cq-remotedam-client-ui-content **e** cq-remotedam-client-ui utilizzando Gestione pacchetti.
* Durante l’installazione di AEM 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * Quando l’integrazione di Target è configurata in AEM tramite l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * com.adobe.granite.Maintenance.impl.TaskScheduler: non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce se vengono utilizzate funzioni di aggregazione quali SUM, MAX e MIN. CQ-4274424
   * com.adobe.granite.Maintenance.impl.TaskScheduler - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva Dynamic Media non è visibile durante l’anteprima della risorsa tramite il visualizzatore di banner per e-commerce.

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei documenti di testo seguenti sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in AEM 6.5.3.0

Elenco dei bundle OSGi inclusi in AEM 6.5.3.0

[Ottieni file](assets/6530_bundles.txt)

Elenco dei pacchetti di contenuti inclusi in AEM 6.5.3.0

[Ottieni file](assets/sp_6530_packages.txt)

## Helpful Resources {#helpful-resources}

* [Note sulla versione di AEM 6.5](/help/release-notes/release-notes.md)
* [Pagina del prodotto AEM](https://www.adobe.com/solutions/web-experience-management.html)
* [Supporto per sviluppatori AEM](https://docs.adobe.com/content/ddc/en.html)
* [Documentazione di AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe Priority Product Updates](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## Siti con limitazioni {#restricted-sites}

Questi siti sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Per ulteriori informazioni sull’accesso al portale di assistenza,](https://daycare.day.com/public/contact.html)contattate l’assistenza clienti. Per ulteriori informazioni sull’accesso, consultate [Accesso al portale](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)di assistenza.
