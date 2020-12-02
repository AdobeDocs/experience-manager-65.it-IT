---
title: Come eseguire AEM con TarMK Cold Standby
seo-title: Come eseguire AEM con TarMK Cold Standby
description: Scoprite come creare, configurare e gestire una configurazione TarMK Cold Standby.
seo-description: Scoprite come creare, configurare e gestire una configurazione TarMK Cold Standby.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
translation-type: tm+mt
source-git-commit: a99c5794cee88d11ca3fb9eeed443c4d0178c7b3
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 0%

---


# Come eseguire AEM con TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Introduzione {#introduction}

La capacità di standby a freddo del Tar Micro Kernel consente a una o più istanze AEM di standby di collegarsi a un&#39;istanza primaria. Il processo di sincronizzazione è un modo solo, il che significa che viene eseguito solo dalle istanze primarie a quelle in standby.

Lo scopo delle istanze standby è quello di garantire una copia live dei dati del repository principale e garantire un interruttore rapido senza perdita di dati nel caso in cui il master non sia disponibile per qualsiasi motivo.

Il contenuto viene sincronizzato in modo lineare tra l&#39;istanza principale e le istanze in standby senza che sia necessario verificare l&#39;integrità del file o del repository. A causa di questa progettazione, le istanze in standby sono copie esatte dell&#39;istanza principale e non possono aiutare a mitigare le incongruenze sulle istanze primarie.

>[!NOTE]
>
>La funzione Cold Standby è studiata per proteggere gli scenari in cui è richiesta un&#39;elevata disponibilità nelle istanze **author**. Per le situazioni in cui è richiesta un&#39;elevata disponibilità su istanze **publish** che utilizzano il kernel Tar Micro,  Adobe consiglia di utilizzare una farm di pubblicazione.
>
>Per informazioni su ulteriori distribuzioni disponibili, consultate la pagina [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md).

## Come funziona {#how-it-works}

Nell&#39;istanza AEM principale, viene aperta una porta TCP che sta ascoltando i messaggi in arrivo. Attualmente, ci sono due tipi di messaggi che gli schiavi invieranno al padrone:

* un messaggio che richiede l&#39;ID segmento dell&#39;intestazione corrente
* un messaggio che richiede i dati del segmento con un ID specificato

La modalità standby richiede periodicamente l’ID del segmento dell’intestazione corrente del primario. Se il segmento è localmente sconosciuto, verrà recuperato. Se è già presente, i segmenti vengono confrontati e, se necessario, anche i segmenti a cui viene fatto riferimento.

>[!NOTE]
>
>Le istanze in standby non ricevono alcun tipo di richieste, perché sono in esecuzione in modalità solo sincronizzazione. L&#39;unica sezione disponibile in un&#39;istanza in standby è la console Web, per facilitare la configurazione del bundle e dei servizi.

Una tipica implementazione TarMK Cold Standby:

![chlimage_1](assets/chlimage_1.png)

## Altre caratteristiche {#other-characteristics}

### Robustezza {#robustness}

Il flusso di dati è progettato per rilevare e gestire automaticamente i problemi di connessione e di rete. Tutti i pacchetti vengono forniti con checksum e non appena si verificano problemi con la connessione o i pacchetti danneggiati, vengono attivati i meccanismi di ritentamento.

#### Spettacolo {#performance}

Abilitare TarMK Cold Standby sull&#39;istanza principale non ha quasi alcun impatto misurabile sulle prestazioni. Il consumo aggiuntivo della CPU è molto basso e l&#39;I/O del disco rigido e della rete non deve generare problemi di prestazioni.

Durante il processo di sincronizzazione, in standby è possibile che la CPU venga utilizzata a un livello elevato. Poiché la procedura non è multithread, non può essere accelerata utilizzando più core. Se non si modificano o si trasferiscono dati, non ci sarà alcuna attività misurabile. La velocità di connessione varia a seconda dell&#39;hardware e dell&#39;ambiente di rete, ma non dipende dalle dimensioni dell&#39;archivio o dall&#39;utilizzo di SSL. Tenete presente questo aspetto quando stimate il tempo necessario per una sincronizzazione iniziale o quando nel frattempo molti dati sono stati modificati sul nodo principale.

#### Sicurezza {#security}

Presupponendo che tutte le istanze vengano eseguite nella stessa area di protezione Intranet, il rischio di violazione della sicurezza viene notevolmente ridotto. Tuttavia, potete aggiungere un ulteriore livello di protezione abilitando le connessioni SSL tra gli slave e il master. In questo modo si riduce la possibilità che i dati siano compromessi da un uomo in mezzo.

Potete inoltre specificare le istanze in standby consentite per la connessione limitando l&#39;indirizzo IP delle richieste in arrivo. In questo modo si dovrebbe garantire che nessuno nella Intranet possa copiare il repository.

>[!NOTE]
>
>Si consiglia di aggiungere un sistema di bilanciamento del carico tra il dispatcher e i server che fanno parte della configurazione di Coldy Standby. Il sistema di bilanciamento del carico deve essere configurato in modo da indirizzare il traffico degli utenti solo all&#39;istanza **primario**, in modo da garantire la coerenza e impedire che il contenuto venga copiato sull&#39;istanza standby con metodi diversi dal meccanismo di standby a freddo.

## Creazione di una configurazione AEM TarMK Cold Standby {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>Il PID per l&#39;archivio nodi Segmento e il servizio di store Standby è stato modificato in AEM 6.3 rispetto alle versioni precedenti, come segue:
>
>* da org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService a org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* da org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>
Accertatevi di apportare le modifiche necessarie alla configurazione per riflettere questa modifica.

Per creare una configurazione TarMK in standby freddo, è innanzitutto necessario creare le istanze in standby eseguendo una copia del file system dell&#39;intera cartella di installazione del primario in una nuova posizione. È quindi possibile avviare ogni istanza con una modalità di esecuzione che ne specifica il ruolo ( `primary` o `standby`).

Di seguito è riportata la procedura da seguire per creare una configurazione con un’istanza master e un’istanza standby:

1. Installare AEM.

1. Arrestate l’istanza e copiate la cartella di installazione nel percorso in cui verrà eseguita l’istanza in standby freddo. Anche se eseguite da computer diversi, accertatevi di assegnare a ciascuna cartella un nome descrittivo (come *aem-primario* o *aem-standby*) per distinguere tra le istanze.
1. Andate alla cartella di installazione dell’istanza principale e:

   1. Controllare ed eliminare eventuali configurazioni OSGi precedenti che si possono avere in `aem-primary/crx-quickstart/install`

   1. Creare una cartella denominata `install.primary` in `aem-primary/crx-quickstart/install`

   1. Crea le configurazioni necessarie per l&#39;archivio nodi e l&#39;archivio dati preferiti in `aem-primary/crx-quickstart/install/install.primary`
   1. Create un file denominato `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` nella stessa posizione e configuratelo di conseguenza. Per ulteriori informazioni sulle opzioni di configurazione, vedere [Configurazione](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Se si utilizza un&#39;istanza AEM TarMK con un archivio dati esterno, creare una cartella denominata `crx3` in `aem-primary/crx-quickstart/install` denominata `crx3`

   1. Posizionare il file di configurazione dell&#39;archivio dati nella cartella `crx3`.

   Se, ad esempio, state eseguendo un&#39;istanza AEM TarMK con un archivio dati file esterno, avete bisogno dei seguenti file di configurazione:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Di seguito sono riportate configurazioni di esempio per l&#39;istanza principale:

   **Esempio** **oforg.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Esempio di org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Esempio di org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Avviate la modalità principale accertandovi di specificare la modalità di esecuzione principale:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Create un nuovo logger di registrazione Apache Sling per il pacchetto **org.apache.jackrabbit.oak.segment**. Impostate il livello di registro su &quot;Debug&quot; e indirizzate l&#39;output del registro su un file di registro separato, ad esempio */logs/tarmk-coldstandby.log*. Per ulteriori informazioni, vedere [Registrazione](/help/sites-deploying/configure-logging.md).
1. Andate alla posizione dell&#39;istanza **standby** e avviatela eseguendo il jar.
1. Create la stessa configurazione di registrazione utilizzata per il file principale. Quindi, arrestate l&#39;istanza.
1. Quindi, preparare l&#39;istanza standby. A tal fine, è possibile eseguire gli stessi passaggi dell&#39;istanza principale:

   1. Eliminate eventuali file presenti in `aem-standby/crx-quickstart/install`.
   1. Creare una nuova cartella denominata `install.standby` in `aem-standby/crx-quickstart/install`

   1. Create due file di configurazione denominati:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. Creare una nuova cartella denominata `crx3` in `aem-standby/crx-quickstart/install`

   1. Creare la configurazione dell&#39;archivio dati e posizionarla in `aem-standby/crx-quickstart/install/crx3`. Ad esempio, il file da creare è:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. Modificate i file e create le configurazioni necessarie.

   Di seguito sono riportati alcuni file di configurazione di esempio per una tipica istanza in standby:

   **Esempio di org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Esempio di org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Esempio di org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Avviare l&#39;istanza **standby** utilizzando la modalità di esecuzione standby:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

Il servizio può essere configurato anche tramite la console Web tramite:

1. Passate alla console Web all&#39;indirizzo: *https://serveraddress:serverport/system/console/configMgr*
1. Alla ricerca di un servizio denominato **Apache Jackrabbit Oak Segment Tar Cold Standby Service** e fare doppio clic su di esso per modificare le impostazioni.
1. Salvataggio delle impostazioni e riavvio delle istanze in modo da rendere effettive le nuove impostazioni.

>[!NOTE]
>
>È possibile controllare il ruolo di un&#39;istanza in qualsiasi momento controllando la presenza delle modalità di esecuzione **primario** o **standby** nella console Web delle impostazioni di Sling.
>
>A tale scopo, andare alla riga *https://localhost:4502/system/console/status-slingsettings* e controllare la riga **&quot;Run Modes&quot;**.

## Prima sincronizzazione {#first-time-synchronization}

Dopo il completamento del preparato e l&#39;avvio dello standby per la prima volta, si verificherà un traffico di rete pesante tra i casi in quanto lo standby raggiunge il primo. Potete consultare i registri per osservare lo stato della sincronizzazione.

In standby *tarmk-coldstandby.log*, sono disponibili le seguenti voci:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

Nel *error.log* dello standby è visibile una voce come questa:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

Nel frammento di registro sopra, *10.20.30.40* è l&#39;indirizzo IP del primario.

In **primario** *tarmk-coldstandby.log* sono disponibili le seguenti voci:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

In questo caso, il &quot;client&quot; menzionato nel registro è l&#39;istanza **standby**.

Una volta che queste voci non compaiono più nel registro, è possibile supporre che il processo di sincronizzazione sia completo.

Anche se le voci sopra riportate mostrano che il meccanismo di polling funziona correttamente, è spesso utile capire se vi sono dati che vengono sincronizzati durante il polling. Per eseguire questa operazione, cercare le voci seguenti:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Inoltre, quando si esegue con un `FileDataStore` non condiviso, messaggi come quelli riportati di seguito confermeranno che i file binari vengono trasmessi correttamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configurazione {#configuration}

Per il servizio Cold Standby sono disponibili le seguenti impostazioni OSGi:

* **Configurazione persistente:** se abilitata, questa opzione memorizzerà la configurazione nell’archivio invece dei tradizionali file di configurazione OSGi. Si consiglia di mantenere disattivata questa impostazione sui sistemi di produzione in modo che la configurazione primaria non venga estratta dallo standby.

* **Modalità (`mode`):** questa opzione consente di scegliere la modalità di esecuzione dell’istanza.

* **Porta (porta):** la porta da utilizzare per la comunicazione. Il valore predefinito è `8023`.

* **Host principale (`primary.host`):**  - l&#39;host dell&#39;istanza principale. Questa impostazione è applicabile solo per lo standby.
* **Intervallo di sincronizzazione (`interval`):** - questa impostazione determina l&#39;intervallo tra la richiesta di sincronizzazione ed è applicabile solo per l&#39;istanza standby.

* **Intervalli IP consentiti (`primary.allowed-client-ip-ranges`):** - gli intervalli IP da cui il principale consentirà le connessioni.
* **Protetto (`secure`):** Abilita crittografia SSL. Per poter utilizzare questa impostazione, è necessario che sia attivata in tutte le istanze.
* **Timeout lettura standby (`standby.readtimeout`):** timeout per le richieste inviate dall&#39;istanza standby, in millisecondi. L&#39;impostazione di timeout consigliata è 43200000. In genere si consiglia di impostare il timeout su un valore di almeno 12 ore.

* **Pulizia automatica standby (`standby.autoclean`):** chiama il metodo di pulizia se la dimensione dello store aumenta in un ciclo di sincronizzazione.

>[!NOTE]
>
>Si consiglia vivamente che il principale e lo standby abbiano ID di repository diversi per renderli identificabili separatamente per servizi come Offloading.
>
>Il modo migliore per assicurarsi che questo sia coperto è eliminando il file *sling.id* sullo standby e riavviando l&#39;istanza.

## Procedure di failover {#failover-procedures}

Nel caso in cui l&#39;istanza principale non riesca per qualsiasi motivo, potete impostare una delle istanze in standby per assumere il ruolo di primario modificando la modalità di esecuzione iniziale come descritto di seguito:

>[!NOTE]
>
>È inoltre necessario modificare i file di configurazione in modo che corrispondano alle impostazioni utilizzate per l&#39;istanza principale.

1. Accedete alla posizione in cui è installata l&#39;istanza standby e arrestatela.

1. Se con la configurazione è configurato un sistema di bilanciamento del carico, a questo punto è possibile rimuovere il sistema primario dalla configurazione del sistema di bilanciamento del carico.
1. Eseguire il backup della cartella `crx-quickstart` dalla cartella di installazione in standby. Può essere utilizzato come punto di partenza per la configurazione di un nuovo standby.

1. Riavviate l&#39;istanza utilizzando la modalità di esecuzione `primary`:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Aggiungete il nuovo elemento primario al sistema di bilanciamento del carico.
1. Creare e avviare una nuova istanza in standby. Per ulteriori informazioni, vedere la procedura riportata sopra in [Creazione di un AEM TarMK Cold Standby Setup](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Applicazione delle correzioni rapide a una configurazione in standby fredda {#applying-hotfixes-to-a-cold-standby-setup}

Il modo consigliato per applicare hotfix a una configurazione a freddo stanby è installarli nell&#39;istanza principale e poi clonarli in una nuova istanza a freddo standby con gli hotfix installati.

A tal fine, effettuate le seguenti operazioni:

1. Arrestate il processo di sincronizzazione sull&#39;istanza in standby a freddo accedendo alla console JMX e utilizzando **org.apache.jackrabbit.oak: Stato (&quot;Standby&quot;)**fagiolo. Per ulteriori informazioni su come eseguire questa operazione, vedere la sezione relativa al [Monitoraggio](#monitoring).
1. Arrestare l&#39;istanza in standby a freddo.
1. Installate l&#39;hotfix nell&#39;istanza principale. Per ulteriori dettagli su come installare un hotfix, vedere [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md).
1. Verificate i problemi dell&#39;istanza dopo l&#39;installazione.
1. Rimuovere l&#39;istanza in standby freddo eliminando la cartella di installazione.
1. Arrestate l&#39;istanza principale e duplicatela eseguendo una copia del file system dell&#39;intera cartella di installazione nella posizione dello standby freddo.
1. Riconfigurare il clone appena creato per fungere da istanza in standby a freddo. Per ulteriori dettagli, vedere [Creazione di un&#39;impostazione AEM TarMK Cold Standby.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Avviate sia l&#39;istanza di standby principale che quella fredda.

## Monitoraggio {#monitoring}

La funzione espone le informazioni utilizzando JMX o MBeans. In questo modo è possibile controllare lo stato corrente dello standby e del master utilizzando la [console JMX](/help/sites-administering/jmx-console.md). Le informazioni si trovano in un MBean di `type org.apache.jackrabbit.oak:type="Standby"`denominato `Status`.

**Standby**

Osservando un&#39;istanza in standby si espone un nodo. L’ID è in genere un UUID generico.

Questo nodo ha cinque attributi di sola lettura:

* `Running:` valore booleano che indica se il processo di sincronizzazione è in esecuzione o meno.

* `Mode:` Client: seguito dall’UUID utilizzato per identificare l’istanza. Questo UUUID verrà modificato ogni volta che la configurazione viene aggiornata.

* `Status:` una rappresentazione testuale dello stato corrente (come  `running` o  `stopped`).

* `FailedRequests:`il numero di errori consecutivi.
* `SecondsSinceLastSuccess:` il numero di secondi dall&#39;ultima comunicazione con il server riuscita. Se la comunicazione non è riuscita, viene visualizzata `-1`.

Sono inoltre disponibili tre metodi di fatturazione:

* `start():` avvia il processo di sincronizzazione.
* `stop():` interrompe il processo di sincronizzazione.
* `cleanup():` esegue l&#39;operazione di pulizia in standby.

**Principale**

Osservando il primario vengono esposte alcune informazioni generali tramite un MBean il cui valore ID è il numero di porta utilizzato dal servizio di standby TarMK (per impostazione predefinita 8023). La maggior parte dei metodi e degli attributi sono gli stessi della modalità standby, ma alcuni sono diversi:

* `Mode:` mostra sempre il valore  `primary`.

È inoltre possibile recuperare informazioni per un massimo di 10 client (istanze in standby) collegati al master. L&#39;ID MBean è l&#39;UUID dell&#39;istanza. Non esistono metodi fatturabili per questi MBeans, ma alcuni attributi di sola lettura molto utili:

* `Name:` l&#39;ID del client.
* `LastSeenTimestamp:` la marca temporale dell&#39;ultima richiesta in una rappresentazione testuale.
* `LastRequest:` l&#39;ultima richiesta del client.
* `RemoteAddress:` l&#39;indirizzo IP del client.
* `RemotePort:` la porta utilizzata dal client per l&#39;ultima richiesta.
* `TransferredSegments:` il numero totale di segmenti trasferiti a questo client.
* `TransferredSegmentBytes:`il numero totale di byte trasferiti a questo client.

## Manutenzione archivio in standby a freddo {#cold-standby-repository-maintenance}

### Pulizia revisioni {#revision-clean}

>[!NOTE]
>
>Se si esegue [Pulizia revisioni online](/help/sites-deploying/revision-cleanup.md) sull&#39;istanza principale, la procedura manuale riportata di seguito non è necessaria. Inoltre, se si utilizza la funzione di pulizia revisioni online, l&#39;operazione `cleanup ()` nell&#39;istanza standby verrà eseguita automaticamente.

>[!NOTE]
>
>Non eseguire la pulizia revisioni offline in standby. Non è necessario e non ridurrà la dimensione del segmento store.

 Adobe raccomanda di eseguire regolarmente la manutenzione per evitare un&#39;eccessiva crescita del repository nel tempo. Per eseguire manualmente la manutenzione del repository in standby a freddo, procedere come segue:

1. Arrestate il processo di standby sull&#39;istanza standby accedendo alla console JMX e utilizzando il **org.apache.jackrabbit.oak: Stato (&quot;Standby&quot;)** fagiolo. Per ulteriori informazioni su come eseguire questa operazione, vedere la sezione precedente su [Monitoring](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Arrestate l&#39;istanza AEM principale.
1. Eseguire lo strumento di compattazione quercia sull&#39;istanza principale. Per ulteriori dettagli, vedere [Gestione dell&#39;archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Avviate l’istanza principale.
1. Avviare il processo di standby sull&#39;istanza standby utilizzando lo stesso fagiolo JMX come descritto nel primo passaggio.
1. Controllate i registri e attendete il completamento della sincronizzazione. È possibile che in questo momento si verifichi una crescita sostanziale nel repository stand-by.
1. Eseguire l&#39;operazione `cleanup()` sull&#39;istanza standby, utilizzando lo stesso fagiolo JMX come descritto nel primo passaggio.

Potrebbe essere necessario più tempo del solito per completare la sincronizzazione con l&#39;istanza standby, in quanto la compattazione offline riscrive efficacemente la cronologia del repository, rendendo così più veloce il calcolo delle modifiche nei repository. Si noti inoltre che una volta completato il processo, le dimensioni del repository sullo standby saranno più o meno uguali a quelle del repository sul principale.

In alternativa, il repository principale può essere copiato in standby manualmente dopo aver eseguito la compattazione sul primario, in pratica ricreando lo standby ogni volta che la compattazione viene eseguita.

### Archivio dati raccolta oggetti inattivi {#data-store-garbage-collection}

È importante eseguire il processo di garbage collection sulle istanze del datastore del file di volta in volta, altrimenti i file binari eliminati rimarranno nel file system, fino a riempire l&#39;unità. Per eseguire la raccolta dei rifiuti, attenetevi alla procedura seguente:

1. Eseguire la manutenzione del repository in standby a freddo come descritto nella sezione [sopra](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Dopo il completamento del processo di manutenzione e il riavvio delle istanze:

   * Sul primario, eseguire la raccolta dei rifiuti dell&#39;archivio dati tramite il fagiolo JMX corrispondente come descritto in [questo articolo](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * In standby, la raccolta dei rifiuti nell&#39;archivio dati è disponibile solo tramite **BlobGarbageCollection** MBean - `startBlobGC()`. **RepositoryManagement **MBean non è disponibile nello standby.

   >[!NOTE]
   >
   >Se non si utilizza un archivio dati condiviso, la raccolta dei rifiuti deve essere eseguita prima sul computer principale e poi sullo standby.

