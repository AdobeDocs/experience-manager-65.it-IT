---
title: Aggiornamento di codice e personalizzazioni
seo-title: Aggiornamento di codice e personalizzazioni
description: Ulteriori informazioni sull'aggiornamento del codice personalizzato in AEM.
seo-description: Ulteriori informazioni sull'aggiornamento del codice personalizzato in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '2204'
ht-degree: 0%

---


# Aggiornamento del codice e delle personalizzazioni{#upgrading-code-and-customizations}

Durante la pianificazione e l&#39;aggiornamento, è necessario esaminare e affrontare i seguenti aspetti di un&#39;implementazione.

* [Aggiorna la base codici](#upgrade-code-base)
* [Allinea con struttura archivio 6.5](#align-repository-structure)
* [Personalizzazioni AEM](#aem-customizations)
* [Procedura di prova](#testing-procedure)

## Panoramica {#overview}

1. **Rilevatore**  pattern: eseguite il rilevatore di pattern come descritto nella pianificazione dell&#39;aggiornamento e descritto in dettaglio in  [questa ](/help/sites-deploying/pattern-detector.md) pagina per ottenere un report del rilevatore di pattern contenente ulteriori dettagli sulle aree che devono essere affrontate oltre alle API/ai bundle non disponibili nella versione di AEM di Target. Il rapporto Rilevamento pattern deve fornire un&#39;indicazione di eventuali incompatibilità nel codice; se non ne sono presenti altre, la distribuzione è già compatibile con la versione 6.5, è comunque possibile scegliere di eseguire un nuovo sviluppo per utilizzare la funzionalità 6.5, ma non è necessario solo per mantenere la compatibilità. In caso di incompatibilità segnalata, è possibile scegliere a) Eseguire in modalità compatibilità e posticipare lo sviluppo per le nuove funzionalità 6.5 o compatibilità, b) decidere di eseguire lo sviluppo dopo l&#39;aggiornamento e passare al passaggio 2. Per ulteriori informazioni, vedere [Compatibilità con le versioni precedenti nella AEM 6.5](/help/sites-deploying/backward-compatibility.md).

1. **Sviluppare la base codici per la versione 6.5 **- Creare un ramo o un repository dedicato per la base codice per la versione di Target. Utilizzate le informazioni provenienti dalla compatibilità pre-aggiornamento per pianificare aree di codice da aggiornare.
1. **Compilare con 6.5 Uber jar **- Aggiornare i POM della base di codice in modo che puntino a 6.5 uber jar e compilare il codice in base a questo.
1. **Aggiornamento AEM Personalizzazioni*** - *Eventuali personalizzazioni o estensioni da AEM devono essere aggiornate/convalidate per funzionare in 6.5 e aggiunte alla base di codici 6.5. Include Forms per la ricerca nell’interfaccia utente, Personalizzazioni risorse con /mnt/overlay

1. **Distribuisci in ambiente**  6.5 - Un&#39;istanza pulita di AEM 6.5 (Autore + Pubblicazione) dovrebbe essere presente in un ambiente Dev/QA. È necessario aggiornare la base di codice e distribuire un campione rappresentativo di contenuto (proveniente dalla produzione corrente).
1. **Convalida QA e correzione**  bug - QA deve convalidare l&#39;applicazione sia nelle istanze Author che Publish di 6.5. Eventuali bug rilevati devono essere corretti e impegnati nella base di codici 6.5. Ripetere Dev-Cycle secondo necessità fino a risolvere tutti i bug.

Prima di procedere con l&#39;aggiornamento è necessario disporre di una base di codice applicativo stabile che sia stata accuratamente testata rispetto alla versione di destinazione del AEM. Sulla base delle osservazioni fatte durante il test, potrebbero esserci modi per ottimizzare il codice personalizzato. Ciò potrebbe includere il refactoring del codice per evitare l&#39;attraversamento del repository, l&#39;indicizzazione personalizzata per ottimizzare la ricerca o l&#39;uso di nodi non ordinati in JCR, tra gli altri.

Oltre all&#39;opzione di aggiornare la base di codice e le personalizzazioni per l&#39;utilizzo con la nuova versione di AEM, 6.5 consente anche di gestire le personalizzazioni in modo più efficiente con la funzione di compatibilità con le versioni precedenti, come descritto in [questa pagina](/help/sites-deploying/backward-compatibility.md).

Come indicato sopra e mostrato nel diagramma seguente, l&#39;esecuzione del [Rilevatore di pattern](/help/sites-deploying/pattern-detector.md) nel primo passaggio vi aiuterà a valutare la complessità generale dell&#39;aggiornamento e se desiderate eseguire in modalità di compatibilità o aggiornare le vostre personalizzazioni per utilizzare tutte le nuove funzioni di AEM 6.5. Per ulteriori informazioni, vedere la pagina [Compatibilità con le versioni precedenti nella AEM 6.5](/help/sites-deploying/backward-compatibility.md).
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Aggiorna la base codici {#upgrade-code-base}

### Crea un ramo dedicato per il codice 6.5 nel controllo delle versioni {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Tutti i codici e le configurazioni richiesti per l&#39;implementazione AEM devono essere gestiti utilizzando un qualche tipo di controllo della versione. È necessario creare un ramo dedicato nel controllo della versione per gestire tutte le modifiche necessarie per la base di codice nella versione di destinazione del AEM. In questo ramo verrà gestito il test iterativo della base di codice rispetto alla versione di destinazione di AEM e correzioni di bug successive.

### Aggiornare la versione AEM Uber Jar {#update-the-aem-uber-jar-version}

AEM Uber jar include tutte AEM API come una singola dipendenza nel progetto Maven `pom.xml`. È sempre consigliabile includere Uber Jar come singola dipendenza invece di includere singole dipendenze API AEM. Quando si aggiorna la base di codice, la versione di Uber Jar deve essere modificata in modo da puntare alla versione di destinazione di AEM. Se il progetto è stato sviluppato su una versione di AEM prima dell&#39;esistenza di Uber Jar, tutte le singole dipendenze API AEM devono essere rimosse e sostituite da un&#39;unica inclusione dell&#39;Uber Jar per la versione di destinazione di AEM. La base di codice deve quindi essere ricompilata con la nuova versione di Uber Jar. Eventuali API o metodi obsoleti devono essere aggiornati per essere compatibili con la versione di destinazione di AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Eliminazione graduale dell&#39;utilizzo di Administrative Resource Resolver {#phase-out-use-of-administrative-resource-resolver}

L&#39;uso di una sessione amministrativa attraverso `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` era abbastanza diffuso nelle basi di codice prima di AEM 6.0. Tali metodi sono stati dichiarati obsoleti per motivi di sicurezza, in quanto forniscono un livello di accesso troppo ampio. [Nelle versioni future di Sling questi metodi verranno rimossi](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Si consiglia vivamente di rigenerare il codice in modo da utilizzare gli utenti del servizio. Ulteriori informazioni sugli utenti dei servizi e [come eliminare gradualmente le sessioni amministrative sono disponibili qui](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Query e indici di quercia {#queries-and-oak-indexes}

Qualsiasi utilizzo di query nella base di codici deve essere accuratamente testato nell&#39;ambito dell&#39;aggiornamento della base di codice. Per i clienti che effettuano l’aggiornamento da Jackrabbit 2 (versioni AEM precedenti alla 6.0), questo è particolarmente importante, in quanto Oak non indicizza automaticamente il contenuto e potrebbe essere necessario creare indici personalizzati. Se si esegue l&#39;aggiornamento da una versione AEM 6.x, le definizioni dell&#39;indice Oak potrebbero essere cambiate e avere effetti sulle query esistenti.

Sono disponibili diversi strumenti per l’analisi e l’analisi delle prestazioni delle query:

* [Strumenti indice AEM](/help/sites-deploying/queries-and-indexing.md)

* [Strumenti di diagnostica operazioni - Prestazioni query](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Oak Utils](https://oakutils.appspot.com/). Si tratta di uno strumento open source che non viene mantenuto dal Adobe .

### Classic UI Authoring {#classic-ui-authoring}

L’authoring con l’interfaccia classica è ancora disponibile in AEM 6.5 ma non è più disponibile. Ulteriori informazioni sono disponibili [qui](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Se l’applicazione è attualmente in esecuzione nell’ambiente di authoring dell’interfaccia classica, si consiglia di effettuare l’aggiornamento a AEM 6.5 e continuare a utilizzare l’interfaccia classica. La migrazione all&#39;interfaccia utente touch può essere pianificata come progetto separato da completare in diversi cicli di sviluppo. Per utilizzare l’interfaccia classica in AEM 6.5, sono necessarie diverse configurazioni OSGi per il commit nella base di codice. Per ulteriori dettagli su come configurare questo parametro, vedere [qui](/help/sites-administering/enable-classic-ui.md).

## Allinea con la struttura del repository 6.5 {#align-repository-structure}

Per semplificare gli aggiornamenti e garantire che le configurazioni non vengano sovrascritte durante un aggiornamento, il repository viene ristrutturato in 6.4 per separare il contenuto dalla configurazione.

È pertanto necessario spostare alcune impostazioni per non risiedere più in `/etc`, come era già avvenuto in passato. Per esaminare l&#39;intero insieme di problemi di ristrutturazione del repository che devono essere esaminati e inseriti nell&#39;aggiornamento alla AEM 6.4, vedere [Ristrutturazione del repository in AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizzazioni AEM {#aem-customizations}

È necessario identificare tutte le personalizzazioni all’ambiente di authoring AEM nella versione di AEM di origine. Una volta identificati, si consiglia di memorizzare ciascuna personalizzazione nel controllo della versione o almeno di eseguire il backup come parte di un pacchetto di contenuti. Tutte le personalizzazioni devono essere distribuite e convalidate in un ambiente QA o Staging che esegue la versione di destinazione di AEM prima di un aggiornamento della produzione.

### Sovrapposizioni in generale {#overlays-in-general}

È pratica comune estendere AEM fuori dalla funzionalità box sovrapponendo nodi e/o file in /libs con nodi aggiuntivi in /apps. Queste sovrapposizioni devono essere tracciate nel controllo della versione e verificate in base alla versione di destinazione del AEM. Se un file (sia JS, JSP, HTL) è sovrapposto, si consiglia di lasciare un commento su quale funzionalità è stata aumentata per un test di regressione più semplice sulla versione di destinazione di AEM. Ulteriori informazioni sulle sovrapposizioni in generale sono disponibili in [qui](/help/sites-developing/overlays.md). Le istruzioni per specifiche sovrapposizioni AEM sono disponibili di seguito.

### Aggiornamento della ricerca personalizzata Forms {#upgrading-custom-search-forms}

I facet di ricerca personalizzati richiedono alcune regolazioni manuali dopo l&#39;aggiornamento per funzionare correttamente. Per ulteriori dettagli, vedere [Aggiornamento della ricerca personalizzata per Forms](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personalizzazioni interfaccia utente risorse {#assets-ui-customizations}

>[!NOTE]
>
>Questa procedura è necessaria solo per gli aggiornamenti da versioni precedenti alla AEM 6.2.

Le istanze che dispongono di distribuzioni di risorse personalizzate devono essere preparate per l’aggiornamento. Ciò è necessario per garantire che tutto il contenuto personalizzato sia compatibile con la nuova struttura di nodi 6.4.

Per preparare le personalizzazioni all’interfaccia utente delle risorse, effettua le seguenti operazioni:

1. Nell&#39;istanza che deve essere aggiornata, aprire il CRXDE Lite andando a *https://server:port/crx/de/index.jsp*

1. Vai al nodo seguente:

   * `/apps/dam/content`

1. Rinominare il nodo di contenuto in **content_backup**. A tale scopo, fare clic con il pulsante destro del mouse sul riquadro dell&#39;elenco delle cartelle nella parte sinistra della finestra e scegliere **Rinomina**.

1. Dopo aver rinominato il nodo, create un nuovo nodo denominato content in `/apps/dam` denominato **content** e impostatene il tipo su **sling:Folder**.

1. Spostate tutti i nodi figlio di **content_backup** nel nodo di contenuto appena creato. A tale scopo, fare clic con il pulsante destro del mouse su ciascun nodo secondario nel riquadro di esplorazione e selezionare **Sposta**.

1. Eliminare il nodo **content_backup**.

1. I nodi aggiornati sotto `/apps/dam` con il tipo di nodo corretto di `sling:Folder` dovrebbero idealmente essere salvati nel controllo della versione e distribuiti con la base di codice o con un minimo di backup come pacchetto di contenuto.

### Generazione di ID risorsa per risorse esistenti {#generating-asset-ids-for-existing-assets}

Per generare ID di risorse per le risorse esistenti, aggiornate le risorse quando aggiornate l’istanza AEM in modo da eseguire AEM 6.5. Questo è necessario per abilitare la funzione [Informazioni sulle risorse](/help/assets/asset-insights.md). Per ulteriori dettagli, vedere [Aggiungi codice da incorporare](/help/assets/use-page-tracker.md#add-embed-code).

Per aggiornare le risorse, configura il pacchetto Associate Asset ID (ID risorsa associati) nella console JMX. A seconda del numero di risorse presenti nella directory archivio, `migrateAllAssets` potrebbe richiedere molto tempo. I nostri test interni stimano circa un&#39;ora per 125mila asset su TarMK.

![1487758945977](assets/1487758945977.png)

Se avete bisogno di ID risorsa per un sottoinsieme di tutte le risorse, utilizzate l&#39;API `migrateAssetsAtPath`.

Per tutti gli altri scopi, utilizzate l&#39;API `migrateAllAssets()`.

### Personalizzazioni  script InDesign {#indesign-script-customizations}

 Adobe consiglia di inserire script personalizzati nella posizione `/apps/settings/dam/indesign/scripts`. Per ulteriori informazioni sulle personalizzazioni  script InDesign, vedere [qui](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Ripristino delle configurazioni ContextHub {#recovering-contexthub-configurations}

Le configurazioni ContextHub sono interessate da un aggiornamento. Le istruzioni su come recuperare le configurazioni ContextHub esistenti sono disponibili [qui](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personalizzazioni del flusso di lavoro {#workflow-customizations}

È pratica comune aggiornare i flussi di lavoro di modifica per aggiungere o rimuovere funzionalità non necessarie. Un flusso di lavoro comune personalizzato è il flusso di lavoro [!UICONTROL DAM Update Asset]. Tutti i flussi di lavoro necessari per un&#39;implementazione personalizzata devono essere sottoposti a backup e memorizzati nel controllo delle versioni, in quanto possono essere sovrascritti durante un aggiornamento.

### Modelli modificabili {#editable-templates}

>[!NOTE]
>
>Questa procedura è necessaria solo per gli aggiornamenti di Siti che utilizzano Modelli modificabili di AEM 6.2

La struttura dei modelli modificabili è cambiata tra AEM 6.2 e 6.3. Se state effettuando l&#39;aggiornamento dalla versione 6.2 o precedente e il contenuto del sito è stato creato utilizzando modelli modificabili, dovrete utilizzare lo [Strumento Pulizia nodi reattivi](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). Lo strumento deve essere eseguito **dopo** un aggiornamento per ripulire il contenuto. Dovrà essere eseguito su livelli Autore e Pubblica.

### Modifiche all&#39;implementazione CUG {#cug-implementation-changes}

L&#39;implementazione di Gruppi di utenti chiusi è cambiata notevolmente per risolvere i limiti di prestazioni e scalabilità nelle versioni precedenti di AEM. La versione precedente di CUG era obsoleta in 6.3 e la nuova implementazione era supportata solo nell’interfaccia touch. Se state effettuando l&#39;aggiornamento da 6.2 o versioni precedenti, le istruzioni per effettuare la migrazione alla nuova implementazione CUG sono disponibili [qui](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procedura di verifica {#testing-procedure}

Dovrebbe essere preparato un piano di test completo per gli aggiornamenti di test. La verifica della base di codice aggiornata e dell’applicazione dovrà essere eseguita innanzitutto in ambienti più bassi. Eventuali bug rilevati devono essere corretti in modo iterativo fino a quando la base del codice non è stabile, solo allora gli ambienti di livello superiore dovrebbero essere aggiornati.

### Verifica della procedura di aggiornamento {#testing-the-upgrade-procedure}

La procedura di aggiornamento descritta qui deve essere testata sugli ambienti Dev e QA come documentato nel manuale di esecuzione personalizzato (vedere [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)). La procedura di aggiornamento deve essere ripetuta fino a quando tutte le fasi non sono documentate nel libro di esecuzione dell&#39;aggiornamento e il processo di aggiornamento non è uniforme.

### Aree di test di implementazione {#implementation-test-areas-}

Di seguito sono riportate le aree critiche di ogni implementazione AEM che dovrebbe essere coperta dal piano di test una volta che l&#39;ambiente è stato aggiornato e che la base di codice aggiornata è stata implementata.

<table>
 <tbody>
  <tr>
   <td><strong>Area di prova funzionale</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Siti pubblicati</td>
   <td>Verifica dell’implementazione AEM e del codice associato sul livello di pubblicazione<br /> tramite il dispatcher. Deve includere criteri per gli aggiornamenti di pagina e l'annullamento della validità della cache<br />.</td>
  </tr>
  <tr>
   <td>Authoring  </td>
   <td>Verificare l’implementazione AEM e il codice associato nel livello Autore. Deve includere finestre di dialogo e di authoring delle pagine e dei componenti.</td>
  </tr>
  <tr>
   <td>Integrazioni con le soluzioni di Marketing Cloud</td>
   <td>Convalida delle integrazioni con prodotti come Analytics, DTM e Target.</td>
  </tr>
  <tr>
   <td>Integrazioni con i sistemi di terze parti</td>
   <td>Le eventuali integrazioni di terze parti devono essere convalidate sia sui livelli Autore che Pubblica.</td>
  </tr>
  <tr>
   <td>Autenticazione, sicurezza e autorizzazioni</td>
   <td>Eventuali meccanismi di autenticazione come LDAP/SAML devono essere convalidati.<br /> Le autorizzazioni e i gruppi devono essere testati sia sull'autore che sugli <br /> editori.</td>
  </tr>
  <tr>
   <td>Query</td>
   <td>Gli indici e le query personalizzati devono essere testati insieme alle prestazioni delle query.</td>
  </tr>
  <tr>
   <td>Personalizzazioni interfaccia utente</td>
   <td>Eventuali estensioni o personalizzazioni dell’interfaccia AEM nell’ambiente di authoring.</td>
  </tr>
  <tr>
   <td>Flussi di lavoro</td>
   <td>Flussi di lavoro e funzionalità personalizzati e/o non inclusi.</td>
  </tr>
  <tr>
   <td>Test delle prestazioni</td>
   <td>Il test del carico deve essere eseguito sia sui livelli Autore che Pubblica per simulare scenari reali.</td>
  </tr>
 </tbody>
</table>

### Piano di test del documento e risultati {#document-test-plan-and-results}

Occorre creare un piano di prova che copra le aree di prova di attuazione sopra indicate. In molti casi sarà utile separare il piano di test dagli elenchi delle attività Autore e Pubblica. Questo piano di test deve essere eseguito negli ambienti Dev, QA e Stage prima di aggiornare gli ambienti Produzione. I risultati dei test e le metriche delle prestazioni devono essere acquisiti in ambienti inferiori per fornire un confronto quando si aggiornano gli ambienti Stage e Produzione.
