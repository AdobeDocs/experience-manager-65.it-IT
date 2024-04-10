---
title: Controlli post-aggiornamento e risoluzione dei problemi
description: Scopri come risolvere i problemi che potrebbero verificarsi dopo un aggiornamento.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: ceac2b52-6885-496d-9517-5fc7291ad070
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1793'
ht-degree: 0%

---

# Controlli post-aggiornamento e risoluzione dei problemi{#post-upgrade-checks-and-troubleshooting}

## Controlli post-aggiornamento {#post-upgrade-checks}

Dopo il [Aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md) per finalizzare l’aggiornamento, devono essere eseguite le seguenti attività. Si presume che l’AEM sia stato avviato con il file jar 6.5 e che la base di codice aggiornata sia stata distribuita.

* [Verifica dei registri per il completamento dell&#39;aggiornamento](#main-pars-header-290365562)

* [Verificare i bundle OSGi](#main-pars-header-1637350649)

* [Verifica versione Oak](#main-pars-header-1293049773)

* [Inspect: cartella PreUpgradeBackup](#main-pars-header-988995987)

* [Convalida iniziale delle pagine](#main-pars-header-20827371)
* [Applicazione dei Service Pack per AEM](#main-pars-header-215142387)

* [Migrazione delle funzioni AEM](#main-pars-header-1434457709)

* [Verifica configurazioni di manutenzione pianificate](#main-pars-header-1552730183)

* [Abilita agenti di replica](#main-pars-header-823243751)

* [Abilita processi pianificati personalizzati](#main-pars-header-244535083)

* [Esegui piano di test](#main-pars-header-1167972233)

### Verifica registri per aggiornamento completato {#verify-logs-for-upgrade-success}

**upgrade.log**

In passato, il controllo dello stato di post-aggiornamento dell’istanza richiedeva un’attenta ispezione di vari file di registro, parti dell’archivio e il modulo di avvio. La generazione di un rapporto post-aggiornamento può aiutare a rilevare gli aggiornamenti difettosi prima della pubblicazione.

Lo scopo principale di questa funzione è ridurre la necessità di interpretazione manuale o logica di analisi complessa su più endpoint necessari per qualificare il successo di un aggiornamento. La soluzione fornisce informazioni inequivocabili che consentono ai sistemi di automazione esterni di reagire in caso di esito positivo o negativo di un aggiornamento.

In particolare, garantisce che:

* Gli errori di aggiornamento rilevati dal framework di aggiornamento sono centralizzati in un unico rapporto di aggiornamento.
* Il rapporto sull’aggiornamento include indicatori sul necessario intervento manuale.

Per risolvere questo problema, sono state apportate modifiche alla modalità di generazione dei registri in `upgrade.log` file.

Di seguito è riportato un report di esempio che non mostra errori durante l’aggiornamento:

![1487887443006](assets/1487887443006.png)

Di seguito è riportato un report di esempio che mostra un bundle non installato durante il processo di aggiornamento:

![1487887532730](assets/1487887532730.png)

**error.log**

Il file error.log deve essere esaminato attentamente durante e dopo l’avvio dell’AEM utilizzando la versione target jar. Eventuali avvertenze o errori devono essere esaminati. In generale, è consigliabile cercare i problemi all’inizio del registro. Gli errori che si verificano più avanti nel registro possono in realtà essere effetti collaterali di una causa principale che viene richiamata all’inizio del file. Se si verificano errori e avvisi ripetuti, vedi di seguito per [Analisi dei problemi relativi all’aggiornamento](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verificare i bundle OSGi {#verify-osgi-bundles}

Passa alla console OSGi `/system/console/bundles` e per vedere se eventuali bundle non vengono avviati. Se uno o più bundle sono in stato di installazione, consulta `error.log` per determinare il problema principale.

### Verifica versione Oak {#verify-oak-version}

In seguito all’aggiornamento, dovresti notare che la versione Oak è stata aggiornata a **1.10.2.**. Per verificare la versione Oak, passa alla console OSGi e osserva la versione associata ai bundle Oak: Oak Core, Oak Commons, Oak Segment Tar.

### Cartella PreUpgradeBackup di Inspect {#inspect-preupgradebackup-folder}

Durante l’aggiornamento, AEM tenta di eseguire il backup delle personalizzazioni e di memorizzarle sotto `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Per visualizzare questa cartella in CRXDE Liti, potrebbe essere necessario [abilita temporaneamente CRXDE Liti](/help/sites-administering/enabling-crxde-lite.md).

La cartella con il timestamp deve avere una proprietà denominata `mergeStatus` con un valore di `COMPLETED`. Il **to-process** la cartella deve essere vuota e la **sovrascritto** node indica quali nodi sono stati sovrascritti durante l’aggiornamento. Il contenuto sotto il nodo degli avanzi indica il contenuto che non è stato possibile unire in modo sicuro durante l’aggiornamento. Se l’implementazione dipende da uno qualsiasi dei nodi secondari (e non già installati dal pacchetto di codice aggiornato), deve essere unita manualmente.

Disattiva CRXDE Liti seguendo questo esercizio se si trova in un ambiente di stage o produzione.

### Convalida iniziale delle pagine {#initial-validation-of-pages}

Eseguire una convalida iniziale su diverse pagine dell’AEM. Se si aggiorna un ambiente di authoring, aprire la pagina Start e la pagina di benvenuto ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). In entrambi gli ambienti Author e Publish, apri alcune pagine di applicazioni e verifica che vengano riprodotte correttamente. In caso di problemi, consultare il `error.log` per la risoluzione dei problemi.

### Applicazione dei Service Pack per AEM {#apply-aem-service-packs}

Se sono stati rilasciati, applicare i Service Pack AEM 6.5 pertinenti.

### Migrazione delle funzionalità AEM {#migrate-aem-features}

Diverse funzioni dell’AEM richiedono passaggi aggiuntivi dopo l’aggiornamento. Un elenco completo di queste funzioni e dei passaggi necessari per migrarle all&#39;AEM 6.5 è disponibile sul sito [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) pagina.

### Verifica configurazioni di manutenzione pianificate {#verify-scheduled-maintenance-configurations}

#### Abilita raccolta oggetti inattivi dell’archivio dati {#enable-data-store-garbage-collection}

Se utilizzi un archivio dati file, accertati che l’attività Raccolta oggetti inattivi dell’archivio dati sia abilitata e aggiunta all’elenco Manutenzione settimanale. Le istruzioni sono descritte [qui](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Questa operazione non è consigliata per le installazioni dell’archivio dati personalizzato S3 o quando si utilizza un archivio dati condiviso.

#### Abilita pulizia revisioni online {#enable-online-revision-cleanup}

Se utilizzi MongoMK o il nuovo formato di segmento TarMK, accertati che l’attività Pulizia revisioni sia abilitata e aggiunta all’elenco Manutenzione giornaliera. Istruzioni descritte [qui](/help/sites-deploying/revision-cleanup.md).

### Esegui piano di test {#execute-test-plan}

Esegui piano di test dettagliato in base a come definito [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) sotto **Procedura di prova** sezione.

### Abilita agenti di replica {#enable-replication-agents}

Dopo aver aggiornato e convalidato completamente l’ambiente di pubblicazione, abilita gli agenti di replica nell’ambiente di authoring. Verifica che gli agenti siano in grado di connettersi alle rispettive istanze Publish. Vedere U [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md) per ulteriori dettagli sull’ordine degli eventi.

### Abilita processi pianificati personalizzati {#enable-custom-scheduled-jobs}

A questo punto è possibile abilitare tutti i processi pianificati come parte della base di codice.

## Analisi Dei Problemi Relativi All’Aggiornamento {#analyzing-issues-with-upgrade}

Questa sezione descrive alcuni scenari di problemi che si potrebbero verificare durante la procedura di aggiornamento a AEM 6.3.

Questi scenari dovrebbero aiutare a individuare la causa principale dei problemi relativi all’aggiornamento e dovrebbero aiutare a identificare i problemi specifici del progetto o del prodotto.

### Migrazione dell’archivio non riuscita  {#repository-migration-failing-}

La migrazione dei dati da CRX2 a Oak dovrebbe essere fattibile per qualsiasi scenario a partire da Istanze di origine basate su CQ 5.4. Accertati di seguire esattamente le istruzioni di aggiornamento riportate in questo documento, che includono la preparazione del `repository.xml`, accertandosi che non venga avviato alcun autenticatore personalizzato tramite JAAS e che l’istanza sia stata controllata per individuare incoerenze prima di avviare la migrazione.

Se la migrazione non riesce ancora, puoi capire qual è la causa principale esaminando il `upgrade.log`. Se il problema non è ancora noto, segnalalo all’Assistenza clienti.

### Aggiornamento Non Eseguito {#the-upgrade-did-not-run}

Prima di iniziare i passaggi di preparazione, assicurati di eseguire il **sorgente** eseguendolo prima con il comando Java™ -jar aem-quickstart.jar. Questo è necessario per assicurarsi che il file quickstart.properties sia generato correttamente. Se manca, l’aggiornamento non funzionerà. In alternativa, è possibile verificare se il file è presente cercando in `crx-quickstart/conf` nella cartella di installazione dell’istanza di origine. Inoltre, quando si avvia AEM per avviare l’aggiornamento, questo deve essere eseguito con il comando Java™ -jar aem-quickstart.jar. L’avvio da uno script di avvio non avvia AEM in modalità di aggiornamento.

### Impossibile aggiornare pacchetti e bundle  {#packages-and-bundles-fail-to-update-}

Nel caso in cui i pacchetti non vengano installati durante l’aggiornamento, i bundle in essi contenuti non verranno aggiornati. Questa categoria di problemi è causata da una configurazione errata dell’archivio dati. Vengono inoltre visualizzati come **ERRORE** e **AVVERTI** messaggi in error.log. Poiché nella maggior parte di questi casi l’accesso predefinito potrebbe non funzionare, puoi utilizzare CRXDE direttamente per verificare e individuare i problemi di configurazione.

### Alcuni bundle AEM non passano allo stato attivo {#some-aem-bundles-are-not-switching-to-the-active-state}

Se sono presenti bundle che non si avviano, verifica la presenza di eventuali dipendenze non soddisfatte.

Nel caso in cui il problema sia presente ma si basi su un’installazione non riuscita del pacchetto che ha portato a un mancato aggiornamento dei bundle, questi verranno considerati incompatibili per la nuova versione. Per ulteriori informazioni su come risolvere il problema, consulta **Impossibile aggiornare pacchetti e bundle** sopra.

Si consiglia inoltre di confrontare l’elenco dei bundle di una nuova istanza AEM 6.5 con quello aggiornato per rilevare i bundle che non sono stati aggiornati. Questo fornirà un ambito più vicino di cosa cercare nel `error.log`.

### Bundle personalizzati non passano allo stato attivo {#custom-bundles-not-switching-to-the-active-state}

Se i bundle personalizzati non passano allo stato attivo, è probabile che ci sia codice che non importa l’API di modifica. Questo nella maggior parte dei casi porterà a dipendenze non soddisfatte.

L’API rimossa deve essere contrassegnata come obsoleta in una delle versioni precedenti. Le istruzioni su una migrazione diretta del codice sono disponibili in questo avviso di elementi obsoleti. Adobe mira al controllo delle versioni semantiche, ove possibile, in modo che le versioni possano indicare modifiche che causano interruzioni.

È inoltre consigliabile verificare se la modifica che ha causato il problema è necessaria e, in caso contrario, ripristinarla. Controlla anche se l’aumento di versione dell’esportazione del pacchetto è stato aumentato più del necessario, seguendo un rigoroso controllo delle versioni semantiche.

### Interfaccia utente di Platform non funzionante {#malfunctioning-platform-ui}

Se alcune funzionalità dell’interfaccia utente non funzionano correttamente dopo l’aggiornamento, è necessario innanzitutto verificare la presenza di sovrapposizioni personalizzate dell’interfaccia. Alcune strutture potrebbero essere state modificate e la sovrapposizione potrebbe richiedere un aggiornamento o risultare obsoleta.

Quindi, controlla eventuali errori JavaScript che possono essere tracciati fino alle estensioni aggiunte personalizzate collegate alle librerie client. Lo stesso vale per i CSS personalizzati che potrebbero causare problemi al layout dell’AEM.

Infine, verifica la presenza di errori di configurazione che JavaScript potrebbe non essere in grado di risolvere. Questo accade in genere con le estensioni disattivate in modo improprio.

### Componenti personalizzati, modelli o estensioni dell’interfaccia utente non funzionanti {#malfunctioning-custom-components-templates-or-ui-extensions}

In genere, le cause principali di questi problemi sono le stesse dei bundle non avviati o dei pacchetti non installati, con l’unica differenza che i problemi iniziano a verificarsi quando si utilizzano i componenti per la prima volta.

Il modo per trattare il codice personalizzato errato è quello di eseguire prima i test di fumo per identificare la causa. Una volta trovato, consulta i consigli in questo [link] sezione dell&#39;articolo per i modi di fissarli.

### Personalizzazioni mancanti in /etc {#missing-customizations-under-etc}

`/apps` e `/libs` sono gestiti correttamente dall’aggiornamento, ma le modifiche in `/etc` potrebbe essere necessario ripristinare manualmente da `/var/upgrade/PreUpgradeBackup` dopo l&#39;upgrade. Verificare la presenza di eventuali contenuti da unire manualmente in questa posizione.

### Analisi dei file error.log e upgrade.log {#analyzing-the-error.log-and-upgrade.log}

Nella maggior parte delle situazioni, i registri devono essere consultati per gli errori per individuare la causa di un problema. Tuttavia, con gli aggiornamenti, è anche necessario monitorare i problemi di dipendenza in quanto i vecchi bundle potrebbero non essere aggiornati correttamente.

Il modo migliore per farlo è quello di eliminare error.log rimuovendo tutti i messaggi che si prevede non siano correlati al problema che stai affrontando. Puoi eseguire questa operazione tramite uno strumento come grep, utilizzando:

```shell
grep -v UnrelatedErrorString
```

Alcuni messaggi di errore potrebbero non essere immediatamente esplicativi. In questo caso, anche esaminare il contesto in cui si verificano può essere utile per capire dove è stato creato l’errore. È possibile separare l’errore utilizzando:

* `grep -B` per aggiungere righe prima dell’errore;

oppure

* `grep -A` per aggiungere righe dopo.

In alcuni casi è possibile trovare anche messaggi WARN in quanto possono esserci casi validi che portano a questo stato e l’applicazione non è sempre in grado di decidere se si tratta di un errore effettivo. Assicurati di consultare anche questi messaggi.

### Contattare il supporto Adobe {#contacting-adobe-support}

Se hai già esaminato i consigli in questa pagina e riscontri ancora problemi, contatta l’Assistenza Adobe. Per fornire quante più informazioni possibili al tecnico del supporto che lavora al tuo caso, assicurati di includere il file upgrade.log dal tuo aggiornamento.
