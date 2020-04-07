---
title: Note sulla versione di AEM 6.5 Service Pack
description: Note sulla versione specifiche di Adobe Experience Manager 6.5 Service Pack 4.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: fbe85c70ef993e4728bd76a327e1a27365cf1021

---


# Note sulla versione di Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | **Adobe Experience Manager 6.5** |
|---|---|
| Versione | 6.5.4.0 |
| Tipo | Versione Service Pack |
| Data | 05 marzo 2020 |
| URL di download | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0), distribuzione [software (Beta)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Contenuto in Adobe Experience Manager 6.5.4.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0 è un aggiornamento importante che include nuove funzioni, miglioramenti e prestazioni richiesti dai clienti chiave, stabilità, miglioramenti a livello di sicurezza, rilasciati a partire dalla release 6.5 di **aprile 2019**. Può essere installato sopra Adobe Experience Manager (AEM) 6.5.

Alcune funzioni chiave e miglioramenti introdotti in AEM 6.5.4.0 includono:

* AEM Assets è ora configurato con Brand Portal tramite la console Adobe I/O.

* È ora disponibile un nuovo passaggio [Genera output](../forms/using/aem-forms-workflow-step-reference.md) stampabile per i flussi di lavoro AEM Forms.

* [Supporto](../forms/using/resize-using-layout-mode.md) a più colonne per la modalità di layout per moduli adattivi e comunicazioni interattive.

* Supporto per [Rich Text](../forms/using/designing-form-template.md) nei moduli HTML5.

* [Miglioramenti](new-features-latest-service-pack.md#accessibility-enhancements) dell&#39;accessibilità in Experience Manager Assets.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.8.

* Ora potete sincronizzare le sottostrutture per contenuti selettivi su Contenuti multimediali *dinamici - Modalità* Scene7 invece di tutti i contenuti disponibili in `content/dam`.

* L&#39;integrazione del modello dati del modulo con il servizio Web SOAP ora supporta i gruppi di scelta o gli attributi sugli elementi.

* Le strutture di input o output SOAP e i dati complessi ora supportano la sostituzione di gruppi dinamici.

Per un elenco completo delle funzioni, degli elementi di rilievo e delle funzioni chiave introdotte nei precedenti service pack di AEM 6.5, consultate [Novità di Adobe Experience Manager 6.5 Service Pack 4](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Quando un URL di una pagina AEM Sites contiene due punti ( : ) o percentuale (%), il browser sottostante interrompe la risposta e i cicli della CPU mostrano un picco (NPR-32369, NPR-31918).

* Quando una pagina AEM Sites viene aperta per la modifica e un componente viene copiato, l&#39;azione Incolla non è disponibile per alcuni segnaposto (NPR-32317).

* Quando si apre la procedura guidata Gestisci pubblicazione, un frammento esperienza collegato a un componente core non viene visualizzato negli elenchi dei riferimenti pubblicati (NPR-32233).

* Il rendering della panoramica della Live Copy nell&#39;interfaccia touch richiede molto più tempo dell&#39;interfaccia classica (NPR-32149).

* Quando il server-time e il computer-time si trovano in fusi orari diversi, l&#39;ora di pubblicazione pianificata mostra l&#39;ora del server nell&#39;interfaccia utente touch, mentre nell&#39;interfaccia classica l&#39;ora del computer viene visualizzata (NPR-32077).

* AEM Sites non riesce ad aprire una pagina con un suffisso nell&#39;URL (NPR-32072).

* Quando un utente modifica un frammento di contenuto, viene ripristinata una variante eliminata del frammento di contenuto (NPR-32062).

* Gli utenti possono salvare un frammento di contenuto senza fornire informazioni nei campi richiesti (NPR-31988).

* kernel.js e ui.js non sono precompilati o memorizzati nella cache. Ciò comporta un ulteriore tempo per il rendering delle pagine (NPR-31891).

* Quando PageEventAuditListener è abilitato, la lunghezza della coda di commit aumenta. Incide sulle prestazioni di molte operazioni, come la pubblicazione in blocco, la navigazione e lo spostamento di risorse in massa (NPR-31890).

* Quando si trascinano i frammenti esperienza, viene osservato un tempo di risposta elevato (NPR-31878).

* Quando selezionate l’opzione Trascinate qui il componente nel segnaposto di una griglia reattiva, viene inviata una richiesta GET e la richiesta genera un errore HTTP 403 (NPR-31845).

* Quando si sposta il contenuto all&#39;interno della stessa cartella, l&#39;opzione di spostamento della pagina è disabilitata (NPR-31840).

* In modalità struttura modelli modificabili, l&#39;elenco dei componenti consentiti nel contenitore di layout presenta risultati non corretti. Nel contenitore di layout (NPR-31816) vengono visualizzati solo i componenti con finestra di dialogo di progettazione.

* Quando una pagina dispone di autorizzazioni di sola lettura per un utente, l&#39;opzione Apri proprietà è visibile in sites.html ma non in editor.html (NPR-31770).

* Quando un utente fa clic sul pulsante Crea, l&#39;opzione della pagina non è disponibile (NPR-31756).

* Impossibile sincronizzare la campagna nella campagna Adobe contenente il componente Importazione progettazione OOOTB (Out of the box) (NPR-31728).

* Quando si tenta di modificare un elenco di elenchi puntati in elenchi numerati, vengono modificati solo i primi due elementi dell&#39;elenco (NPR-31636).

* Quando una pagina viene decreata e viene selezionato il nodo figlio, nella finestra di dialogo di selezione viene ancora visualizzato il nodo iniziale. Quando la pagina viene creata e l&#39;utente fa clic su Sfoglia, la pagina reindirizza al nodo principale invece del nodo creato (NPR-31618).

* La finestra di dialogo di configurazione della visualizzazione non funziona correttamente per la funzione di personalizzazione Inbox (NPR-32503 e NPR-32492).

* Viene visualizzato un messaggio di errore durante la visualizzazione delle informazioni sul flusso di lavoro tramite Inbox (CQ-4282168).

### Assets {#assets-6540-enhancements}

* Il pulsante per attivare il flusso di lavoro nella pagina di raccolta delle risorse è disattivato (NPR-32471).

* In SPS (Scene7 Publishing System) viene creata una cartella senza nome quando si sposta una risorsa da una cartella all’altra in Experience Manager con configurazione Dynamic Media Scene7 (NPR-32440).

* L’azione per spostare tutte le risorse (tramite Seleziona tutto e quindi Sposta) in una cartella contenente le risorse pubblicate non riesce e ha esito negativo (NPR-32366).

* Generazione della rappresentazione per le risorse con ${extension} non riuscita (NPR-32294).

* Gli URL della cronologia delle versioni vengono visualizzati nel campo Con riferimento nella pagina Proprietà delle risorse (NPR-31889).

* Impossibile aprire il file ZIP scaricato da DAM tramite WinZip (NPR-32293).

* Le autorizzazioni originali di una cartella vengono aggiornate quando le Impostazioni cartella vengono aperte per cambiare il titolo della cartella o l&#39;immagine in miniatura e quindi salvate (NPR-32292).

* L&#39;icona Calendario per l&#39;attivazione pianificata non viene visualizzata nella colonna Stato (nell&#39;interfaccia classica dell&#39;elenco di risorse DAM) per le risorse la cui attivazione è pianificata per una data e un&#39;ora successive (NPR-32291).

* La creazione di snippet mediante i modelli di snippet genera un errore durante la ricerca delle raccolte durante il processo di creazione degli snippet (NPR-32290).

* Quando si selezionano più tag dal filtro di ricerca (NPR-32143), vengono attivate più query di ricerca.

* L’interfaccia utente di Experience Manager Assets visualizza i nomi dei file troncati quando vengono caricate risorse con più di 50 caratteri nel nome del file (NPR-32054).

* Tutte le caselle di controllo nel pannello Filtro vengono deselezionate quando la prima e la seconda casella di controllo sono deselezionate, quando sono state selezionate le caselle di controllo di livello due della struttura delle caselle di controllo in Adobe Stock (NPR-31919).

* La ricerca di file e cartelle con facet Omnisearch fa eccezione (NPR-31872).

* L&#39;evidenziazione dei campi per la selezione obbligatoria dei campi nell&#39;editor di metadati non viene rimossa neanche dopo aver selezionato il campo richiesto, quando le regole di dipendenza sono impostate nel modulo di schema di metadati corrispondente (NPR-31834).

* I nomi completi dei tag a livello di foglia (dalla gerarchia dei tag) non vengono visualizzati nella pagina Proprietà della risorsa (NPR-31820).

* L’utilizzo del comando Indietro dalla pagina Proprietà della risorsa nel browser Safari restituisce un errore (NPR-31753).

* La pagina dei risultati della ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente (NPR-31307).

* La pagina di dettaglio delle risorse PDF non mostra i pulsanti delle azioni eccetto A raccolta e Aggiungi rappresentazione in Experience Manager in esecuzione in modalità di esecuzione di Dynamic Media Scene7 (CQ-4286705).

* L’elaborazione delle risorse richiede troppo tempo durante il processo di caricamento batch di Scene7 (CQ-4286445).

* Il pulsante Salva non importa il set remoto quando l&#39;utente non ha apportato modifiche nell&#39;Editor set nel client per contenuti multimediali dinamici (CQ-4285690).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene assimilato in AEM (CQ-4283701).

* Lo stato non elaborato del predefinito per visualizzatori video per ritaglio avanzato viene visualizzato due volte sul testo del banner e sul nome del predefinito (CQ-4283517).

* L’altezza contenitore errata di un modello 3D caricato visualizzato in anteprima nel visualizzatore 3D viene visualizzata nella pagina dei dettagli della risorsa (CQ-4283309).

* Carosello Editor non si apre in IE 11 in modalità ibrida di Experience Manager (CQ-4255590).

* Lo stato attivo si blocca nel menu a discesa E-mail nella finestra di dialogo Download, nei browser Chrome e Safari (NPR-32067).

* La casella di controllo Sincronizza tutto il contenuto non è abilitata per impostazione predefinita quando si tenta di aggiungere la configurazione cloud DM su AEM (CQ-4288533).

### Interfaccia di base {#foundation-ui-6540}

* Il controllo del mouse passa al campo filtro precedente invece di rimanere nel campo filtro esistente durante la ricerca delle risorse mediante il pannello Filtro (NPR-32538).

* Assegnazione tag piattaforma: La ricerca di tag digitando nei campi tag mostra i tag al di fuori dei limiti principali e non rispetta la `rootPath` proprietà dei campi tag (NPR-31895).

* Interfaccia utente della piattaforma: Se nel campo di testo viene aggiunto un percorso non valido (NPR-31884), il browser del percorso si interrompe.

* La notifica viene nascosta dietro un menu fisso nella selezione delle pagine (NPR-31628).

### Platform {#platform-sling-6540}

* (HTL) I caratteri di sottolineatura sostituiscono i due punti nella sezione del percorso dell&#39;URL (NPR-32231).

### Progetti {#projects-6540}

* Il pulsante Crea non è visibile all&#39;utente anche se l&#39;utente dispone dell&#39;autorizzazione per creare un progetto nella sottocartella (NPR-31832).

### Traduzione progetti {#projects-translation-6540}

* La creazione di progetti di traduzione interrompe l&#39;interfaccia utente quando l&#39;opzione Rifila spazi è attivata in `Apache Sling JSP Script Handler` (NPR-32154).

* L&#39;errore nell&#39;interfaccia utente e l&#39;eccezione del punto Null nei registri di errore viene rilevato quando un tag, da tradurre, viene aggiunto a un progetto di traduzione (NPR-31896).

### Integrazioni {#integrations-6540}

* La generazione dell&#39;URL della libreria di avvio è basata solo su `path` e `library_name` valori dell&#39;API di Launch e non è basata su `library_path` valori (NPR-31550).

* Viene visualizzato un messaggio di errore durante l&#39;elaborazione degli elementi correlati a LiveFyre (FYR-12420).

### Editor modelli WCM {#wcm-template-editor-6540}

* In modalità struttura modelli modificabili, l&#39;elenco dei componenti consentiti nel contenitore di layout non visualizza il componente pulsante di collegamento (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Si è verificato un errore durante la selezione di una sovrapposizione e la selezione di componenti reattivi Trascinate qui i componenti (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* La configurazione cloud di destinazione non riesce. Errore: richiesta mbox di recupero (CQ-4279880).

### Brand Portal {#assets-brand-portal}

* Gli utenti di Brand Portal non sono in grado di pubblicare le risorse delle cartelle dei contributi in Risorse AEM al momento dell’aggiornamento ad Adobe I/O su AEM 6.5.4 (CQDOC-15655).

   Questo problema verrà risolto nel service pack successivo AEM 6.5.5.

   Per una correzione immediata su AEM 6.5.4, si consiglia di [scaricare l’hotfix](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e installarlo nell’istanza di creazione.


* I valori a discesa dello schema di metadati non sono visibili nelle proprietà delle risorse (CQ-4283287).

* Il sottoschema metadati non visualizza schede in base al tipo di mimetismo nelle proprietà delle risorse (CQ-4283288).

* Lo schema di metadati Annulla pubblicazione compila un messaggio di errore anche se lo schema viene rimosso nel backend.

* L&#39;immagine di anteprima non viene visualizzata per una risorsa pubblicata (CQ-4285886).

* L&#39;utente non può pubblicare o annullare la pubblicazione di risorse contenenti virgolette singole nel nome (CQ-4272686).

* I termini e le condizioni non vengono visualizzati durante il download di più risorse (CQ-4281224).

* Sono state risolte vulnerabilità di sicurezza minori.

### Communities {#communities}

* Il modulo Crea membro viene visualizzato come una pagina vuota (NPR-31997).

* L&#39;utente non è in grado di visualizzare il rapporto di Analytics sull&#39;istanza di creazione (NPR-30913).

### Quercia - Indicizzazione e query {#oak-indexing-6540}

* Documenti MS Word e MS Excel contenenti immagini JPEG, se analizzati con il parser Tika non riescono ad analizzare e la classe non trova errore (NPR-31952).

### Forms {#forms-6530}

>[!NOTE]
>
>Il Service Pack di AEM non include le correzioni per AEM Forms. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per AEM Forms su JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Gestione corrispondenza: Le lettere contengono caratteri aggiuntivi dopo l&#39;invio ai flussi di lavoro di post-elaborazione (NPR-32626).

* Gestione corrispondenza: Le lettere visualizzano un segnaposto a discesa come componente di testo dopo l&#39;invio ai flussi di lavoro successivi al processo (NPR-32539).

* Gestione corrispondenza: I valori predefiniti definiti nel modello di lettera non vengono visualizzati nella modalità Anteprima (NPR-32511).

* Moduli mobili: Il pulsante di invio viene visualizzato come espanso nelle dimensioni durante il rendering di un modulo XDP in una versione HTML (NPR-32514).

* Document Services: Problemi di accesso agli URL per Lettere e altre pagine dopo l’applicazione di Service Pack 2 (NPR-32508, NPR-32509).

* Document Services: Se il numero di transazioni su un server supera un limite specifico, la conversione da HTML a PDF non riesce e le impostazioni del tipo di file vengono rimosse dal server AEM Forms (NPR-32204).

* Moduli adattivi: Lo strumento di accessibilità del browser segnala gli errori nei moduli adattivi in base alle linee guida WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Moduli adattivi: Lo strumento di accessibilità del browser Chrome segnala un errore best practice (NPR-32310).

* Moduli adattivi: Problemi di traduzione durante la configurazione di un modulo adattivo incorporato in una pagina AEM Sites (NPR-32168).

* Workbench: Viene visualizzato un messaggio di errore durante l&#39;utilizzo dell&#39;operazione Ottieni proprietà PDF per il servizio Utilità PDF (NPR-32150).

* Document Security: Un file PDF protetto non viene aperto offline con l&#39;opzione DisableGlobalOfflineSynchronizationData impostata su True (NPR-32078).

* Designer: Se l&#39;opzione relativa ai tag è attivata, il bordo del sottomodulo scompare nell&#39;output PDF generato (NPR-32547, NPR-31983, NPR-31950).

* Designer: Se in una tabella sono presenti celle unite, il test di accessibilità non riesce per il file PDF di output convertito da un modulo XDP utilizzando il servizio di output (CQ-4285372).

* Foundation JEE: Se un server AEM Forms è disconnesso da un cluster, i problemi di memorizzazione nella cache ne impediscono la riconnessione al server (NPR-32412).

## Install 6.5.4.0 {#install}

**Requisiti di configurazione**

* AEM 6.5.4.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Il download del Service Pack è disponibile in Condivisione pacchetti Adobe, a cui puoi accedere direttamente dall’istanza di AEM 6.5.
* In una distribuzione con MongoDB e più istanze, installa AEM 6.5.4.0 in una delle istanze Autore tramite Gestione pacchetti.
* Prima di installare il Service Pack, assicurati di disporre di uno snapshot o di un nuovo backup dell’istanza AEM.
* Riavvia l’istanza prima dell’installazione. Anche se questa operazione è necessaria solo quando l’istanza è ancora in modalità di aggiornamento (e questo accade quando l’istanza è stata aggiornata da una versione precedente), è consigliabile riavviare l’istanza se questa è rimasta in esecuzione per un periodo più lungo.

>[!CAUTION]
>
>Adobe sconsiglia la rimozione o la disinstallazione del pacchetto AEM 6.5.4.0.

### Installare il Service Pack tramite Condivisione pacchetti {#install-service-pack-via-package-share}

Per installare il Service Pack in un’istanza AEM 6.5 esistente, effettua le seguenti operazioni:

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.4.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0).

1. Installa il pacchetto scaricato utilizzando Gestione pacchetti.

>[!NOTE]
>
>**La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude prematuramente durante l’installazione della versione 6.5.4.0**
>
>È consigliabile attendere che i registri degli errori si stabilizzino prima di accedere all’istanza. L&#39;utente deve attendere i registri specifici relativi alla disinstallazione del bundle dell&#39;utility di aggiornamento prima di assicurarsi che le installazioni abbiano esito positivo. Il problema si verifica in genere in Safari, ma può accadere in modo intermittente in qualsiasi browser.

**Installazione automatica**

Esistono due modi per installare automaticamente AEM 6.5.4.0 in un’istanza in esecuzione:

A. Inserite il pacchetto in ..*/crx-quickstart/install* cartella mentre il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.4.0 non supporta l’installazione tramite bootstrap.

**Convalidare l’installazione**

1. Nella pagina Informazioni sul prodotto (/system/console/ productinfo) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager, Version 6.5.4.0` in Prodotti installati.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. Il bundle OSGI org.apache.jackrabbit.oak-core è sulla versione 1.10.6 o successiva (Usa console Web: /system/console/bundle).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms. Le correzioni apportate in AEM Forms vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi.

>[!NOTE]
>
>AEM 6.5.4.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Se si utilizza una versione precedente del pacchetto di compatibilità AEM Forms e si aggiorna a AEM 6.5.4.0, installare la versione più recente del pacchetto di compatibilità AEM Forms dopo l&#39;installazione del pacchetto di componenti aggiuntivi di Forms.

1. Assicurati di aver installato il Service Pack di AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Le correzioni in AEM Forms su JEE vengono distribuite tramite un programma di installazione separato.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0011](https://helpx.adobe.com/it/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Programma di installazione di Workbench

Poiché si tratta di un programma di installazione completo, la dimensione del file è maggiore rispetto alla versione della patch. Disinstallare la versione precedente di Workbench prima di installare la nuova versione.

### UberJar {#uber-jar}

The UberJar for AEM 6.5.4.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

La versione aggiornata di UberJar per la versione 6.5.4.0 che include il pacchetto **com.fasterxml.jackson.core.asincc** è disponibile nell&#39;archivio [pubblico di](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4-1.0/)Adobe.

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Funzioni obsolete {#removed-deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete con AEM 6.5.4.0. Le funzioni pianificate per essere rimosse in una versione futura sono impostate per prime su obsoleto, con un&#39;opzione alternativa da utilizzare.

Si consiglia ai clienti di verificare se utilizzano la funzionalità o la funzionalità nella distribuzione corrente e di pianificare la modifica della propria implementazione per utilizzare l&#39;opzione alternativa.

| Area | Funzione | Sostituzione |
|---|---|---|
| Integrazioni | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Con l&#39;integrazione AEM e Target aggiornata in AEM 6.5 per supportare l&#39;API di Target Standard, che utilizza l&#39;autenticazione tramite Adobe IMS e I/O, e con il ruolo crescente di Adobe Launch nella strumentazione delle pagine AEM per l&#39;analisi e la personalizzazione, la procedura guidata di consenso è diventata funzionalmente irrilevante. | Configurare le connessioni di sistema, l&#39;autenticazione Adobe IMS e le integrazioni Adobe I/O tramite i rispettivi servizi cloud AEM |

## Problemi noti {#known-issues}

* Se la configurazione **delle risorse** collegate restituisce un messaggio di errore 404 dopo l’installazione, reinstallate manualmente i pacchetti **cq-remotedam-client-ui-content** e **cq-remotedam-client-ui-components** utilizzando Gestione pacchetti.
* Durante l’installazione di AEM 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * Quando l’integrazione di Target è configurata in AEM tramite l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * com.adobe.granite.Maintenance.impl.TaskScheduler: non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce se vengono utilizzate funzioni di aggregazione quali SUM, MAX e MIN. CQ-4274424
   * com.adobe.granite.Maintenance.impl.TaskScheduler - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva Dynamic Media non è visibile durante l’anteprima della risorsa tramite il visualizzatore di banner per e-commerce.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Nei documenti di testo seguenti sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in AEM 6.5.4.0

Elenco dei bundle OSGi inclusi in AEM 6.5.4.0

[Ottieni file](assets/6540_bundles.txt)

Elenco dei pacchetti di contenuti inclusi in AEM 6.5.4.0

[Ottieni file](assets/6540_packages.txt)

## Restricted sites {#restricted-sites}

Questi siti sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Per ulteriori informazioni sull’accesso al portale di assistenza,](https://daycare.day.com/public/contact.html)contattate l’assistenza clienti. Per ulteriori informazioni sull’accesso, consultate [Accesso al portale](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)di assistenza.

>[!MORE COME QUESTO]
>
>* [Note sulla versione di AEM 6.5](/help/release-notes/release-notes.md)
>* [Pagina del prodotto AEM](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentazione di AEM 6.5](https://helpx.adobe.com/it/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

