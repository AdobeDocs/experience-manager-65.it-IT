---
title: Post Upgrade Checks e risoluzione dei problemi
seo-title: Post Upgrade Checks e risoluzione dei problemi
description: Scoprite come risolvere i problemi che possono verificarsi dopo un aggiornamento.
seo-description: Scoprite come risolvere i problemi che possono verificarsi dopo un aggiornamento.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---


# Post Upgrade Checks and Troubleshooting{#post-upgrade-checks-and-troubleshooting}

## Post Upgrade Checks {#post-upgrade-checks}

In seguito all&#39; [Aggiornamento diretto](/help/sites-deploying/in-place-upgrade.md), per finalizzare l&#39;aggiornamento è necessario eseguire le seguenti attività. Si presume AEM sia stato avviato con il JAR 6.5 e che la base di codice aggiornata sia stata distribuita.

* [Verificare i registri per il successo dell&#39;aggiornamento](#main-pars-header-290365562)

* [Verificare i pacchetti OSGi](#main-pars-header-1637350649)

* [Verifica versione Oak](#main-pars-header-1293049773)

* [ Inspect la cartella PreUpgradeBackup](#main-pars-header-988995987)

* [Convalida iniziale delle pagine](#main-pars-header-20827371)
* [Applica AEM Service Pack](#main-pars-header-215142387)

* [Migrazione AEM funzionalità](#main-pars-header-1434457709)

* [Verifica configurazioni di manutenzione pianificate](#main-pars-header-1552730183)

* [Abilita agenti di replica](#main-pars-header-823243751)

* [Abilita processi pianificati personalizzati](#main-pars-header-244535083)

* [Esegui piano di test](#main-pars-header-1167972233)

### Verificare i registri per il successo dell&#39;aggiornamento {#verify-logs-for-upgrade-success}

**upgrade.log**

In passato, ispezionare lo stato post aggiornamento dell&#39;istanza richiedeva un&#39;attenta ispezione di vari file di registro, parti dell&#39;archivio e il launchpad. La generazione di un rapporto post aggiornamento può aiutare a rilevare gli aggiornamenti difettosi prima di andare live.

Lo scopo principale di questa funzione è quello di ridurre la necessità di interpretare manualmente o di eseguire complesse analisi logiche tra più endpoint richiesti per qualificare il successo di un aggiornamento. La soluzione mira a fornire informazioni univoche per i sistemi di automazione esterni per reagire al successo o al fallimento identificato di un aggiornamento.

In particolare, garantisce che:

* Gli errori di aggiornamento rilevati dal framework di aggiornamento possono essere centralizzati in un unico rapporto di aggiornamento;
* Il rapporto di aggiornamento include indicatori relativi all&#39;intervento manuale necessario.

Per ovviare a questo problema, sono state apportate modifiche al modo in cui i registri vengono generati nel file `upgrade.log`.

Di seguito è riportato un esempio di rapporto che non mostra errori durante l&#39;aggiornamento:

![1487887443006](assets/1487887443006.png)

Di seguito è riportato un esempio di rapporto che mostra un bundle non installato durante il processo di aggiornamento:

![1487887532730](assets/1487887532730.png)

**error.log**

Il file error.log deve essere attentamente rivisto durante e dopo l&#39;avvio di AEM utilizzando il file jar della versione di destinazione. Eventuali avvertenze o errori devono essere rivisti. In generale è meglio cercare problemi all’inizio del registro. Gli errori che si verificano successivamente nel registro possono in realtà essere effetti collaterali di una causa principale che viene richiamata in anticipo nel file. Se si verificano errori e avvisi ripetuti, vedere di seguito per [Analisi dei problemi relativi all&#39;aggiornamento](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verificare i pacchetti OSGi {#verify-osgi-bundles}

Passate alla console OSGi `/system/console/bundles` e verificate se non sono stati avviati pacchetti. Se uno stato di installazione contiene dei bundle, consultate la sezione `error.log` per determinare il problema principale.

### Verifica versione Oak {#verify-oak-version}

Dopo l&#39;aggiornamento, la versione di Oak è stata aggiornata a **1.10.2**. Per verificare la versione Oak, andate alla console OSGi e osservate la versione associata ai bundle Oak: Oak Core, Oak Commons, Oak Segment Tar.

###  cartella Inspect PreUpgradeBackup {#inspect-preupgradebackup-folder}

Durante l&#39;aggiornamento AEM tentare di eseguire il backup delle personalizzazioni e archiviarle sotto `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Per visualizzare questa cartella in CRXDE Lite, potrebbe essere necessario [abilitare temporaneamente CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

La cartella con la marca temporale deve avere una proprietà denominata `mergeStatus` con un valore di `COMPLETED`. La cartella **to-process** deve essere vuota e il nodo **sovrascritto** indica quali nodi sono stati sovrascritti durante l&#39;aggiornamento. Il contenuto al di sotto del nodo **leftovers** indica il contenuto che non è stato possibile unire in modo sicuro durante l&#39;aggiornamento. Se l’implementazione dipende da uno dei nodi figlio (e non è già installata dal pacchetto di codice aggiornato), dovrà essere unita manualmente.

Disabilitare CRXDE Lite dopo questo esercizio se in un ambiente Stage o Produzione.

### Convalida iniziale delle pagine {#initial-validation-of-pages}

Eseguire una convalida iniziale rispetto a più pagine in AEM. Se si esegue l&#39;aggiornamento di un ambiente Authoring, aprire la pagina iniziale e la pagina di benvenuto ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Sia nell’ambiente Authoring che in quello Publish, aprite alcune pagine dell’applicazione e verificate che il rendering sia corretto. In caso di problemi, consultare la sezione `error.log` per la risoluzione dei problemi.

### Applica AEM Service Pack {#apply-aem-service-packs}

Applicare eventuali Service Pack AEM 6.5 pertinenti se sono stati rilasciati.

### Migra AEM funzionalità {#migrate-aem-features}

Diverse funzionalità in AEM richiedono passaggi aggiuntivi dopo l&#39;aggiornamento. Un elenco completo di queste funzionalità e dei passaggi per la migrazione nella AEM 6.5 è disponibile nella pagina [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

### Verifica configurazioni di manutenzione pianificata {#verify-scheduled-maintenance-configurations}

#### Abilita raccolta oggetti inattivi archivio dati {#enable-data-store-garbage-collection}

Se si utilizza un archivio dati file, verificare che l&#39;attività di raccolta dei dati nell&#39;archivio dati sia abilitata e aggiunta all&#39;elenco Manutenzione settimanale. Le istruzioni sono indicate [qui](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Questa opzione non è consigliata per le installazioni dell&#39;archivio dati personalizzato S3 o quando si utilizza un archivio dati condiviso.

#### Abilita pulizia revisioni online {#enable-online-revision-cleanup}

Se si utilizza MongoMK o il nuovo formato di segmento TarMK, assicurarsi che l&#39;attività Revision Clean Up sia abilitata e aggiunta all&#39;elenco Daily Maintenance (Manutenzione giornaliera). Istruzioni indicate [qui](/help/sites-deploying/revision-cleanup.md).

### Esegui piano di test {#execute-test-plan}

Eseguire un piano di test dettagliato rispetto a quanto definito [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) nella sezione **Procedura di test**.

### Abilita agenti di replica {#enable-replication-agents}

Una volta aggiornato e convalidato l’ambiente di pubblicazione, abilitate gli agenti di replica nell’ambiente di authoring. Verificate che gli agenti siano in grado di connettersi alle rispettive istanze di pubblicazione. Per ulteriori informazioni sull&#39;ordine degli eventi, vedere U [pgrade Procedure](/help/sites-deploying/upgrade-procedure.md).

### Abilita processi pianificati personalizzati {#enable-custom-scheduled-jobs}

Tutti i processi pianificati come parte della base di codice possono essere attivati a questo punto.

## Analisi dei problemi relativi all&#39;aggiornamento {#analyzing-issues-with-upgrade}

Questa sezione contiene alcuni scenari di problema che potrebbero verificarsi durante la procedura di aggiornamento a AEM 6.3.

Questi scenari dovrebbero aiutare a individuare la causa principale dei problemi correlati all&#39;aggiornamento e dovrebbero aiutare a identificare i problemi specifici di progetto o prodotto.

### Migrazione archivio non riuscita {#repository-migration-failing-}

La migrazione dei dati da CRX2 a Oak dovrebbe essere fattibile per qualsiasi scenario che inizia con Istanze sorgente in base a CQ 5.4. Accertatevi di seguire esattamente le istruzioni di aggiornamento contenute in questo documento, che includono la preparazione di `repository.xml`, verificando che nessun autenticatore personalizzato venga avviato tramite JAAS e che l&#39;istanza sia stata controllata per individuare eventuali incoerenze prima di avviare la migrazione.

Se la migrazione continua a non riuscire, è possibile individuare la causa principale dell&#39;errore ispezionando la `upgrade.log`. Se il problema non è ancora noto, segnalatelo all&#39;Assistenza clienti.

### L&#39;Aggiornamento Non È Stato Eseguito {#the-upgrade-did-not-run}

Prima di avviare i passaggi di preparazione, assicurarsi di eseguire prima l&#39;istanza **source** eseguendola con il comando java -jar aem-quickstart.jar. Questo è necessario per essere sicuri che il file quickstart.properties sia generato correttamente. Se manca, l&#39;aggiornamento non funzionerà. In alternativa, potete verificare la presenza del file cercando in `crx-quickstart/conf` nella cartella di installazione dell&#39;istanza di origine. Inoltre, quando si avvia AEM per avviare l&#39;aggiornamento, questo deve essere eseguito con il comando java -jar aem-quickstart.jar. L&#39;avvio da uno script iniziale non verrà avviato AEM in modalità di aggiornamento.

### Pacchetti e pacchetti non aggiornati {#packages-and-bundles-fail-to-update-}

Nel caso in cui i pacchetti non vengano installati durante l&#39;aggiornamento, nemmeno i pacchetti che contengono verranno aggiornati. Questa categoria di problemi è in genere causata da configurazione errata dell&#39;archivio dati. Vengono visualizzati anche come messaggi **ERROR** e **WARN** nel file error.log. Poiché nella maggior parte di questi casi l&#39;accesso predefinito potrebbe non funzionare, è possibile utilizzare CRXDE direttamente per ispezionare e individuare i problemi di configurazione.

### Alcuni pacchetti AEM non passano allo stato attivo {#some-aem-bundles-are-not-switching-to-the-active-state}

In caso di pacchetti che non si avviano, è necessario verificare la presenza di eventuali dipendenze non soddisfatte.

Nel caso in cui il problema sia presente ma si basa su un&#39;installazione del pacchetto non riuscita che ha portato all&#39;assenza dell&#39;aggiornamento, i bundle verranno considerati incompatibili per la nuova versione. Per ulteriori informazioni su come risolvere questo problema, vedere **Pacchetti e pacchetti non aggiornati** sopra.

Si consiglia inoltre di confrontare l&#39;elenco dei bundle di una nuova istanza AEM 6.5 con quella aggiornata per rilevare i bundle che non sono stati aggiornati. Questo fornirà un ambito più ampio di cosa cercare in `error.log`.

### Pacchetti personalizzati che non passano allo stato attivo {#custom-bundles-not-switching-to-the-active-state}

Nel caso in cui i bundle personalizzati non passino allo stato attivo, è molto probabile che ci sia codice che non importa l&#39;API di modifica. Questo porterà più spesso a dipendenze insoddisfatte.

Le API rimosse devono essere contrassegnate come obsolete in una delle precedenti versioni. In questo avviso di obsolescenza è possibile trovare istruzioni su una migrazione diretta del codice.  Adobe mira al controllo delle versioni semantiche laddove possibile, in modo che le versioni possano indicare eventuali modifiche interrotte.

È inoltre meglio verificare se la modifica che ha causato il problema fosse assolutamente necessaria e ripristinarla se non lo è. Verificate inoltre se l&#39;aumento di versione dell&#39;esportazione del pacchetto è stato aumentato più del necessario, in seguito a rigorose versioni semantiche.

### Interfaccia utente della piattaforma non funzionante {#malfunctioning-platform-ui}

In caso di alcune funzionalità dell&#39;interfaccia utente che non funzionano correttamente dopo l&#39;aggiornamento, è innanzitutto necessario verificare la presenza di sovrapposizioni personalizzate dell&#39;interfaccia. Alcune strutture potrebbero essere cambiate e la sovrapposizione potrebbe richiedere un aggiornamento o essere obsoleta.

Quindi, verificate la presenza di eventuali errori Javascript che possono essere tracciati fino alle estensioni aggiunte personalizzate collegate alle librerie client. Lo stesso può valere per CSS personalizzato che potrebbe causare problemi al layout AEM.

Infine, verificate la presenza di errori di configurazione che Javascript potrebbe non essere in grado di gestire. Questo è in genere il caso con estensioni disattivate in modo improprio.

### Componenti personalizzati, modelli o estensioni dell&#39;interfaccia utente non funzionanti {#malfunctioning-custom-components-templates-or-ui-extensions}

Nella maggior parte dei casi, le cause principali di questi problemi sono le stesse che si verificano per i bundle che non vengono avviati o per i pacchetti che non vengono installati con l&#39;unica differenza che i problemi iniziano quando si utilizzano i componenti per la prima volta.

Il modo per affrontare il codice personalizzato errato è di eseguire prima prove di fumo per identificare la causa. Una volta trovata, consultate le raccomandazioni in questa sezione [link] dell&#39;articolo per trovare i modi per risolverle.

### Personalizzazioni mancanti in /etc {#missing-customizations-under-etc}

`/apps` e  `/libs` sono gestiti bene dall&#39;aggiornamento, ma le modifiche in  `/etc` potrebbero dover essere ripristinate manualmente da  `/var/upgrade/PreUpgradeBackup` dopo l&#39;aggiornamento. Verificate che in questa posizione sia presente qualsiasi contenuto da unire manualmente.

### Analisi di error.log e upgrade.log {#analyzing-the-error.log-and-upgrade.log}

Nella maggior parte dei casi i registri devono essere consultati per individuare eventuali errori al fine di individuare la causa di un problema. Tuttavia, in caso di aggiornamenti è anche necessario monitorare i problemi di dipendenza in quanto i pacchetti obsoleti potrebbero non essere aggiornati correttamente.

Il modo migliore per eseguire questa operazione consiste nell&#39;eliminare il file error.log rimuovendo tutti i messaggi che si prevede non siano correlati al problema che si sta affrontando. Potete farlo tramite strumenti come grep, utilizzando:

```shell
grep -v UnrelatedErrorString
```

Alcuni messaggi di errore potrebbero non essere immediatamente esplicativi. In questo caso, è possibile esaminare il contesto in cui si verifica l&#39;errore per comprendere meglio dove è stato creato. Potete separare l&#39;errore utilizzando:

* `grep -B` per aggiungere righe prima dell&#39;errore;

o

* `grep -A` per aggiungere righe dopo.

In alcuni casi si possono trovare errori anche i messaggi di AVVISO in quanto ci possono essere casi validi che portano a questo stato e l&#39;applicazione non è sempre in grado di decidere se si tratta di un errore reale. Controlla anche questi messaggi.

### Contattare  supporto del Adobe {#contacting-adobe-support}

Se avete letto i consigli presenti in questa pagina e state ancora riscontrando dei problemi, contattate  supporto del Adobe. Per fornire il maggior numero possibile di informazioni al tecnico del supporto che lavora sul vostro caso, accertatevi di includere il file upgrade.log dall&#39;aggiornamento.
