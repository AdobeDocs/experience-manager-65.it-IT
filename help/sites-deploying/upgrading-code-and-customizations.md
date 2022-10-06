---
title: Aggiornamento di codice e personalizzazioni
seo-title: Upgrading Code and Customizations
description: Ulteriori informazioni sull'aggiornamento del codice personalizzato in AEM.
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 0%

---

# Aggiornamento di codice e personalizzazioni{#upgrading-code-and-customizations}

Quando si pianifica un aggiornamento, è necessario esaminare e risolvere i seguenti aspetti di un&#39;implementazione.

* [Aggiornare la base di codice](#upgrade-code-base)
* [Allinea con la struttura dell’archivio 6.5](#align-repository-structure)
* [Personalizzazioni AEM](#aem-customizations)
* [Procedura di prova](#testing-procedure)

## Panoramica {#overview}

1. **Rilevatore pattern** - Eseguire il rilevatore pattern come descritto nella pianificazione dell’aggiornamento e descritto in dettaglio in [questa pagina](/help/sites-deploying/pattern-detector.md) per ottenere un rapporto del rilevatore di pattern che contenga ulteriori dettagli sulle aree da risolvere, oltre alle API/bundle non disponibili nella versione di Target di AEM. Il rapporto di rilevamento pattern deve fornire un’indicazione di eventuali incompatibilità nel codice. Se non ne sono presenti altre, la distribuzione è già compatibile con la versione 6.5, è comunque possibile scegliere di eseguire nuovi sviluppi per utilizzare la funzionalità 6.5, ma non è necessaria solo per mantenere la compatibilità. In caso di incompatibilità segnalate, puoi scegliere di a) eseguire in modalità compatibilità e differire lo sviluppo per le nuove funzioni 6.5 o compatibilità, b) decidere di eseguire lo sviluppo dopo l&#39;aggiornamento e passare al passaggio 2. Vedi [Compatibilità con le versioni precedenti in AEM 6.5](/help/sites-deploying/backward-compatibility.md) per ulteriori dettagli.

1. **Sviluppa una base di codice per la versione 6.5 **- Crea un ramo o un archivio dedicato per la base di codice per la versione di Target. Utilizza le informazioni della compatibilità pre-aggiornamento per pianificare le aree di codice da aggiornare.
1. **Compila con jar da 6.5 Uber **- Aggiorna i POM della base del codice in modo che puntino al jar da 6.5 uber e compila il codice in base a questo.
1. **Aggiorna personalizzazioni AEM*** - *Eventuali personalizzazioni o estensioni da AEM devono essere aggiornate/convalidate per funzionare in 6.5 e aggiunte alla base di codice 6.5. Include Forms per la ricerca nell’interfaccia utente, Personalizzazioni risorse, qualsiasi cosa che utilizzi /mnt/overlay

1. **Implementare in ambiente 6.5** - Un’istanza pulita di AEM 6.5 (Author + Publish) deve essere visibile in un ambiente di sviluppo/controllo qualità. È necessario distribuire una base di codice aggiornata e un campione rappresentativo di contenuto (proveniente dalla produzione corrente).
1. **Convalida QA e correzione bug** - QA deve convalidare l&#39;applicazione sia sulle istanze Author che Publish della versione 6.5. Eventuali bug trovati devono essere corretti e impegnati nella base di codice 6.5. Ripetere Dev-Cycle se necessario fino a quando tutti i bug non sono corretti.

Prima di procedere con un aggiornamento è necessario disporre di una base di codice dell&#39;applicazione stabile che sia stata testata accuratamente sulla versione di destinazione di AEM. Sulla base delle osservazioni fatte durante il test potrebbero esserci modi per ottimizzare il codice personalizzato. Ciò potrebbe includere il refactoring del codice per evitare l’attraversamento dell’archivio, l’indicizzazione personalizzata per ottimizzare la ricerca o l’uso di nodi non ordinati in JCR, tra gli altri.

Oltre all&#39;opzione di aggiornamento della base di codice e delle personalizzazioni per l&#39;utilizzo con la nuova versione di AEM, la versione 6.5 consente anche di gestire le personalizzazioni in modo più efficiente con la funzionalità Compatibilità con le versioni precedenti descritta in [questa pagina](/help/sites-deploying/backward-compatibility.md).

Come indicato sopra e mostrato nel diagramma seguente, eseguire il [Rilevatore pattern](/help/sites-deploying/pattern-detector.md) nel primo passaggio ti aiuterà a valutare la complessità complessiva dell’aggiornamento e se desideri eseguire in modalità di compatibilità o aggiornare le tue personalizzazioni per utilizzare tutte le nuove funzionalità di AEM 6.5. Vedi la [Compatibilità con le versioni precedenti in AEM 6.5](/help/sites-deploying/backward-compatibility.md) per ulteriori dettagli.
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Aggiornare la base di codice {#upgrade-code-base}

### Creare un ramo dedicato per il codice 6.5 nel controllo delle versioni {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Tutti i codici e le configurazioni necessari per l’implementazione AEM devono essere gestiti utilizzando una qualche forma di controllo della versione. È necessario creare un ramo dedicato nel controllo della versione per gestire tutte le modifiche necessarie per la base di codice nella versione di destinazione di AEM. In questo ramo verrà gestito il test iterativo della base di codice rispetto alla versione di destinazione di AEM e successive correzioni di bug.

### Aggiorna la versione AEM Uber Jar {#update-the-aem-uber-jar-version}

Il jar Uber AEM include tutte le API AEM come una singola dipendenza nel progetto Maven `pom.xml`. È sempre consigliabile includere il Jar Uber come una singola dipendenza invece di includere singole dipendenze API AEM. Quando si aggiorna la base di codice, la versione del Jar Uber deve essere modificata in modo da puntare alla versione di destinazione di AEM. Se il progetto è stato sviluppato su una versione di AEM precedente all’esistenza del JAR Uber, tutte le singole dipendenze API AEM devono essere rimosse e sostituite da un’unica inclusione del JAR Uber per la versione di destinazione di AEM. La base di codice deve quindi essere ricompilata rispetto alla nuova versione del JAR Uber. Eventuali API o metodi obsoleti devono essere aggiornati per essere compatibili con la versione di destinazione di AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Utilizzo del risolutore risorse amministrative in fase di abbandono {#phase-out-use-of-administrative-resource-resolver}

L&#39;uso di una sessione amministrativa attraverso `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` era piuttosto diffuso nelle basi di codice prima del AEM 6.0. Questi metodi sono stati dichiarati obsoleti per motivi di sicurezza in quanto offrono un livello di accesso troppo ampio. [Nelle versioni future di Sling questi metodi verranno rimossi](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). È vivamente consigliato effettuare il refactoring di qualsiasi codice per utilizzare invece gli utenti del servizio. Ulteriori informazioni su Utenti del servizio e [come eliminare gradualmente le sessioni amministrative è disponibile qui](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Query e indici Oak {#queries-and-oak-indexes}

Qualsiasi utilizzo delle query nella base di codice deve essere testato accuratamente nell’ambito dell’aggiornamento della base di codice. Per i clienti che eseguono l’aggiornamento da Jackrabbit 2 (versioni AEM precedenti alla 6.0), questo è particolarmente importante in quanto Oak non indicizza automaticamente il contenuto e potrebbe essere necessario creare indici personalizzati. Se si esegue l&#39;aggiornamento da una versione di AEM 6.x, le definizioni predefinite dell&#39;indice Oak potrebbero essere cambiate e potrebbero influenzare le query esistenti.

Sono disponibili diversi strumenti per l’analisi e l’analisi delle prestazioni delle query:

* [Strumenti indice AEM](/help/sites-deploying/queries-and-indexing.md)

* [Strumenti di diagnosi delle operazioni - Prestazioni delle query](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Utilizzo Oak](https://oakutils.appspot.com/). Si tratta di uno strumento open source non gestito dall’Adobe.

### Authoring con interfaccia classica {#classic-ui-authoring}

L’authoring con interfaccia classica è ancora disponibile in AEM 6.5 ma è obsoleto. Ulteriori informazioni sono disponibili [qui](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Se l’applicazione è attualmente in esecuzione nell’ambiente di authoring dell’interfaccia classica, si consiglia di effettuare l’aggiornamento a AEM 6.5 e continuare a utilizzare l’interfaccia classica. La migrazione all’interfaccia utente touch può quindi essere pianificata come progetto separato da completare in diversi cicli di sviluppo. Per utilizzare l’interfaccia classica in AEM 6.5 sono necessarie diverse configurazioni OSGi per eseguire il commit nella base di codice. Per ulteriori dettagli su come configurare questa funzionalità, consulta [qui](/help/sites-administering/enable-classic-ui.md).

## Allinea con la struttura dell’archivio 6.5 {#align-repository-structure}

Per semplificare gli aggiornamenti e garantire che le configurazioni non vengano sovrascritte durante un aggiornamento, l’archivio viene ristrutturato in 6.4 per separare il contenuto dalla configurazione.

Pertanto, alcune impostazioni devono essere spostate per non risiedere più in `/etc` come in passato. Per esaminare l&#39;intera serie di problemi di ristrutturazione dell&#39;archivio che devono essere rivisti e accolti nell&#39;aggiornamento al AEM 6.4, vedi [Ristrutturazione dell’archivio in AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizzazioni AEM  {#aem-customizations}

È necessario identificare tutte le personalizzazioni dell’ambiente di authoring AEM nella versione sorgente di AEM. Una volta identificate, si consiglia di archiviare ogni personalizzazione nel controllo della versione o almeno eseguirne il backup come parte di un pacchetto di contenuti. Tutte le personalizzazioni devono essere distribuite e convalidate in un ambiente di controllo qualità o di staging che esegue la versione di destinazione di AEM prima di un aggiornamento della produzione.

### Sovrapposizioni in generale {#overlays-in-general}

È una pratica comune estendere AEM funzionalità predefinita sovrapponendo nodi e/o file sotto /libs con nodi aggiuntivi sotto /apps. Queste sovrapposizioni devono essere tracciate nel controllo della versione e testate rispetto alla versione di destinazione di AEM. Se un file (sia JS, JSP, HTL) è sovrapposto, si consiglia di lasciare un commento su quale funzionalità è stata aumentata per facilitare il test di regressione sulla versione di destinazione di AEM. Ulteriori informazioni sulle sovrapposizioni in generale sono disponibili [qui](/help/sites-developing/overlays.md). Di seguito sono riportate le istruzioni per specifiche sovrapposizioni di AEM.

### Aggiornamento di Custom Search Forms {#upgrading-custom-search-forms}

Per funzionare correttamente, i facet di ricerca personalizzati richiedono alcune regolazioni manuali dopo l’aggiornamento. Per ulteriori dettagli, consulta [Aggiornamento di Custom Search Forms](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personalizzazioni dell’interfaccia utente Assets {#assets-ui-customizations}

>[!NOTE]
>
>Questa procedura è necessaria solo per gli aggiornamenti da versioni precedenti alla AEM 6.2.

Le istanze che dispongono di implementazioni personalizzate di Assets devono essere preparate per l’aggiornamento. Questo è necessario per garantire che tutto il contenuto personalizzato sia compatibile con la nuova struttura a nodi 6.4.

Per preparare le personalizzazioni all’interfaccia utente di Assets, effettua le seguenti operazioni:

1. Nell’istanza che deve essere aggiornata, apri CRXDE Lite scegliendo *https://server:port/crx/de/index.jsp*

1. Vai al seguente nodo:

   * `/apps/dam/content`

1. Rinomina il nodo di contenuto in **content_backup**. Per eseguire questa operazione, fai clic con il pulsante destro del mouse sul riquadro dell&#39;esploratore nella parte sinistra della finestra e scegli **Rinomina**.

1. Una volta rinominato il nodo, crea un nuovo nodo denominato contenuto in `/apps/dam` denominato **content** e imposta il tipo di nodo su **sling:Folder**.

1. Sposta tutti i nodi figlio di **content_backup** al nodo di contenuto appena creato. Per eseguire questa operazione, fai clic con il pulsante destro del mouse su ciascun nodo figlio nel riquadro Esplora risorse e seleziona **Sposta**.

1. Elimina **content_backup** nodo.

1. I nodi aggiornati sotto `/apps/dam` con il tipo di nodo corretto di `sling:Folder` dovrebbe idealmente essere salvato nel controllo della versione e distribuito con la base di codice o almeno con il backup come pacchetto di contenuto.

### Generazione degli ID risorsa per le risorse esistenti {#generating-asset-ids-for-existing-assets}

Per generare gli ID risorsa per le risorse esistenti, aggiorna le risorse quando aggiorni l’istanza AEM per eseguire AEM 6.5. Questo è necessario per abilitare il [Funzionalità Approfondimenti risorse](/help/assets/asset-insights.md). Per ulteriori dettagli, consulta [Aggiungi codice di incorporamento](/help/assets/use-page-tracker.md#add-embed-code).

Per aggiornare le risorse, configura il pacchetto Associa ID risorsa nella console JMX. A seconda del numero di risorse presenti nell’archivio, `migrateAllAssets` può richiedere molto tempo. I nostri test interni stimano circa un&#39;ora per 125mila asset su TarMK.

![1487758945977](assets/1487758945977.png)

Se hai bisogno di ID risorsa per un sottoinsieme di tutte le risorse, utilizza `migrateAssetsAtPath` API.

Per tutti gli altri scopi, utilizza `migrateAllAssets()` API.

### Personalizzazioni degli script di InDesign {#indesign-script-customizations}

Adobe consiglia di inserire script personalizzati in `/apps/settings/dam/indesign/scripts` posizione. Sono disponibili ulteriori informazioni sulle personalizzazioni degli script di InDesign [qui](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Ripristino delle configurazioni ContextHub {#recovering-contexthub-configurations}

Le configurazioni di ContextHub sono interessate da un aggiornamento. È possibile trovare istruzioni su come recuperare le configurazioni esistenti di ContextHub [qui](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personalizzazioni dei flussi di lavoro {#workflow-customizations}

È prassi comune aggiornare i flussi di lavoro di modifica predefiniti per aggiungere o rimuovere funzionalità non necessarie. Un flusso di lavoro comune personalizzato è il [!UICONTROL Risorsa di aggiornamento DAM] workflow. Tutti i flussi di lavoro necessari per un’implementazione personalizzata devono essere sottoposti a backup e archiviati nel controllo della versione, in quanto possono essere sovrascritti durante un aggiornamento.

### Modelli modificabili {#editable-templates}

>[!NOTE]
>
>Questa procedura è necessaria solo per gli aggiornamenti di Sites che utilizzano modelli modificabili dalla AEM 6.2

La struttura dei modelli modificabili è stata modificata tra AEM 6.2 e 6.3. Se si esegue l&#39;aggiornamento da 6.2 o versioni precedenti e se il contenuto del sito è generato utilizzando modelli modificabili, sarà necessario utilizzare la [Strumento Pulizia nodi reattivi](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). Lo strumento deve essere eseguito **dopo** un aggiornamento per pulire il contenuto. Sarà necessario eseguirlo sia su livelli di authoring che di pubblicazione.

### Modifiche all’implementazione del CUG {#cug-implementation-changes}

L’implementazione dei gruppi di utenti chiusi è cambiata notevolmente per risolvere i limiti di prestazioni e scalabilità delle versioni precedenti di AEM. La versione precedente di CUG è stata dichiarata obsoleta nella versione 6.3 e la nuova implementazione è supportata solo nell’interfaccia utente touch. Se stai effettuando l’aggiornamento da 6.2 o versioni precedenti, puoi trovare le istruzioni per eseguire la migrazione alla nuova implementazione CUG [qui](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procedura di prova {#testing-procedure}

È necessario preparare un piano di prova completo per gli aggiornamenti dei test. Prima di eseguire il test della base di codice e dell’applicazione aggiornata in ambienti inferiori, è necessario eseguire il test. Eventuali bug rilevati devono essere corretti in modo iterativo fino a quando la base del codice non è stabile, solo in questo caso gli ambienti di livello superiore devono essere aggiornati.

### Verifica della procedura di aggiornamento {#testing-the-upgrade-procedure}

La procedura di aggiornamento descritta qui deve essere testata sugli ambienti di sviluppo e controllo qualità come documentato nel manuale di esecuzione personalizzato (vedi [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md)). La procedura di aggiornamento deve essere ripetuta fino a quando tutti i passaggi non sono documentati nel manuale di esecuzione dell&#39;aggiornamento e il processo di aggiornamento non è scorrevole.

### Aree di test di implementazione  {#implementation-test-areas-}

Di seguito sono elencate le aree critiche di qualsiasi implementazione AEM che devono essere coperte dal piano di test una volta che l’ambiente è stato aggiornato e la base di codice aggiornata è stata distribuita.

<table>
 <tbody>
  <tr>
   <td><strong>Area di test funzionale</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Siti pubblicati</td>
   <td>Verifica dell’implementazione AEM e del codice associato sul livello di pubblicazione<br /> tramite il dispatcher. Deve includere criteri per gli aggiornamenti di pagina e<br /> annullamento della validità della cache.</td>
  </tr>
  <tr>
   <td>Authoring  </td>
   <td>Verifica dell’implementazione AEM e del codice associato sul livello di authoring. Deve includere la pagina, l’authoring dei componenti e le finestre di dialogo.</td>
  </tr>
  <tr>
   <td>Integrazioni con le soluzioni Marketing Cloud</td>
   <td>Convalida delle integrazioni con prodotti come Analytics, DTM e Target.</td>
  </tr>
  <tr>
   <td>Integrazioni con sistemi di terze parti</td>
   <td>Eventuali integrazioni di terze parti devono essere convalidate sia sui livelli Author che Publish .</td>
  </tr>
  <tr>
   <td>Autenticazione, sicurezza e autorizzazioni</td>
   <td>Eventuali meccanismi di autenticazione come LDAP/SAML devono essere convalidati.<br /> Le autorizzazioni e i gruppi devono essere testati sia su Author che su Publish<br /> livelli.</td>
  </tr>
  <tr>
   <td>Query</td>
   <td>Gli indici e le query personalizzati devono essere testati insieme alle prestazioni delle query.</td>
  </tr>
  <tr>
   <td>Personalizzazioni dell’interfaccia utente</td>
   <td>Eventuali estensioni o personalizzazioni dell’interfaccia utente AEM nell’ambiente di authoring.</td>
  </tr>
  <tr>
   <td>Flussi di lavoro</td>
   <td>Workflow e funzionalità personalizzati e/o predefiniti.</td>
  </tr>
  <tr>
   <td>Test delle prestazioni</td>
   <td>Il test del carico deve essere eseguito sia sui livelli Author che Publish, in modo da simulare scenari reali.</td>
  </tr>
 </tbody>
</table>

### Piano di test dei documenti e risultati {#document-test-plan-and-results}

Occorre creare un piano di test che copra le aree di test di attuazione sopra indicate. In molti casi sarà utile separare il piano di test dagli elenchi di attività Autore e Pubblica . Questo piano di test deve essere eseguito in ambienti di sviluppo, controllo qualità e stage prima di aggiornare gli ambienti di produzione. I risultati dei test e le metriche delle prestazioni devono essere acquisiti in ambienti inferiori per fornire un confronto durante l’aggiornamento degli ambienti Stage e Production.
