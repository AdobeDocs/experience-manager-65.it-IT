---
title: Come eseguire AEM con lo standby a freddo TarMK
seo-title: How to Run AEM with TarMK Cold Standby
description: Scopri come creare, configurare e mantenere una configurazione di standby a freddo TarMK.
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 88e4d8b56aa844e9a264615250971d0afdb68137
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# Come eseguire AEM con lo standby a freddo TarMK{#how-to-run-aem-with-tarmk-cold-standby}

## Introduzione {#introduction}

La capacità di standby a freddo del Tar Micro Kernel consente a una o più istanze di AEM di standby di connettersi a un&#39;istanza primaria. Il processo di sincronizzazione è un modo solo che significa che viene eseguito solo dalle istanze primarie alle istanze di standby.

Lo scopo delle istanze di standby è quello di garantire una Live Data Copy dell’archivio principale e garantire un rapido switch senza perdita di dati nel caso in cui il master non sia disponibile per qualsiasi motivo.

Il contenuto viene sincronizzato in modo lineare tra l’istanza primaria e le istanze di standby senza alcun controllo dell’integrità per quanto riguarda la corruzione del file o dell’archivio. A causa di questa progettazione, le istanze di standby sono copie esatte dell&#39;istanza primaria e non possono contribuire a mitigare le incongruenze sulle istanze primarie.

>[!NOTE]
>
>La funzione di standby a freddo è destinata a garantire scenari in cui è richiesta un&#39;elevata disponibilità **autore** istanze. Per le situazioni in cui è richiesta un&#39;elevata disponibilità **pubblicare** istanze che utilizzano il kernel Tar Micro, Adobe consiglia di utilizzare una farm di pubblicazione.
>
>Per informazioni su ulteriori distribuzioni disponibili, consulta la sezione [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md) pagina.

>[!NOTE]
>
>Quando l&#39;istanza Standby viene impostata o derivata dal nodo primario, consente solo l&#39;accesso alla seguente console (per le attività relative all&#39;amministrazione):
>
>* Console web OSGI
>
>Altre console non sono accessibili.

## Come funziona {#how-it-works}

Nell&#39;istanza AEM primaria viene aperta una porta TCP in ascolto dei messaggi in arrivo. Attualmente, ci sono due tipi di messaggi che gli schiavi invieranno al padrone:

* un messaggio che richiede l’ID segmento dell’intestazione corrente
* un messaggio che richiede dati di segmento con un ID specificato

Lo standby richiede periodicamente l’ID del segmento dell’intestazione corrente del primario. Se il segmento è localmente sconosciuto, verrà recuperato. Se è già presente, i segmenti vengono confrontati e, se necessario, verranno richiesti anche i segmenti a cui si fa riferimento.

>[!NOTE]
>
>Le istanze di standby non ricevono alcun tipo di richieste, perché sono in esecuzione in modalità di solo sincronizzazione. L&#39;unica sezione disponibile in un&#39;istanza di standby è la Web Console, al fine di facilitare la configurazione dei bundle e dei servizi.

Una tipica implementazione TarMK Cold Standby:

![chlimage_1](assets/chlimage_1.png)

## Altre caratteristiche {#other-characteristics}

### Robustezza {#robustness}

Il flusso di dati è progettato per rilevare e gestire automaticamente i problemi di connessione e di rete. Tutti i pacchetti sono raggruppati con checksum e non appena si verificano problemi con la connessione o i pacchetti danneggiati si verificano nuovi tentativi meccanismi vengono attivati.

#### Spettacolo {#performance}

Abilitare lo standby a freddo TarMK sull&#39;istanza primaria non ha quasi alcun impatto misurabile sulle prestazioni. Il consumo aggiuntivo della CPU è molto basso e l&#39;I/O del disco rigido e della rete extra non deve produrre problemi di prestazioni e prestazioni.

In standby è possibile prevedere un elevato consumo di CPU durante il processo di sincronizzazione. Poiché la procedura non è multithread, non può essere accelerata utilizzando più core. Se non vengono modificati o trasferiti dati, non vi sarà alcuna attività misurabile. La velocità di connessione varia a seconda dell’ambiente hardware e di rete, ma non dipende dalle dimensioni dell’archivio o dall’utilizzo SSL. Tieni presente questo aspetto quando stimi il tempo necessario per una sincronizzazione iniziale o quando nel frattempo molti dati sono stati modificati sul nodo principale.

#### Sicurezza {#security}

Supponendo che tutte le istanze siano eseguite nella stessa area di sicurezza Intranet, il rischio di violazione della sicurezza è notevolmente ridotto. Tuttavia, puoi aggiungere un livello di sicurezza aggiuntivo abilitando le connessioni SSL tra gli slave e il master. In questo modo si riduce la possibilità che i dati siano compromessi da un uomo in mezzo.

È inoltre possibile specificare le istanze in standby consentite per la connessione limitando l’indirizzo IP delle richieste in arrivo. Questo dovrebbe aiutare a garantire che nessuno nella Intranet possa copiare l’archivio.

>[!NOTE]
>
>Si consiglia di aggiungere un load balancer tra il Dispatcher e i server che fanno parte della configurazione di Coldy Standby. Il load balancer deve essere configurato per indirizzare il traffico dell’utente solo al **primario** per garantire la coerenza e impedire che il contenuto venga copiato nell’istanza di standby con mezzi diversi dal meccanismo di standby a freddo.

## Creazione di una configurazione di standby a freddo AEM TarMK {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>Il PID per l’archivio dei nodi di segmento e il servizio di archivio in standby è cambiato in AEM 6.3 rispetto alle versioni precedenti come segue:
>
>* da org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService su org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* da org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService su org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>Assicurati di apportare le regolazioni di configurazione necessarie per riflettere questa modifica.

Per creare una configurazione di standby a freddo TarMK, devi prima creare le istanze di standby eseguendo una copia del file system dell&#39;intera cartella di installazione della cartella principale in una nuova posizione. Puoi quindi avviare ogni istanza con una modalità runmode che ne specifichi il ruolo ( `primary` o `standby`).

Di seguito è riportata la procedura da seguire per creare una configurazione con un master e un&#39;istanza di standby:

1. Installa AEM.

1. Arresta l’istanza e copia la relativa cartella di installazione nel percorso da cui verrà eseguita l’istanza di standby a freddo. Anche se eseguito da computer diversi, assicurati di assegnare a ciascuna cartella un nome descrittivo (come *aem-primary* o *aem-standby*) per distinguere tra le istanze.
1. Vai alla cartella di installazione dell&#39;istanza primaria e:

   1. Controlla ed elimina eventuali configurazioni OSGi precedenti che potresti avere in `aem-primary/crx-quickstart/install`

   1. Crea una cartella denominata `install.primary` sotto `aem-primary/crx-quickstart/install`

   1. Crea le configurazioni richieste per l’archivio dei nodi preferiti e l’archivio dati in `aem-primary/crx-quickstart/install/install.primary`
   1. Crea un file denominato `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` nella stessa posizione e configurala di conseguenza. Per ulteriori informazioni sulle opzioni di configurazione, vedi [Configurazione](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Se utilizzi un&#39;istanza AEM TarMK con un archivio dati esterno, crea una cartella denominata `crx3` sotto `aem-primary/crx-quickstart/install` denominato `crx3`

   1. Posiziona il file di configurazione dell’archivio dati in `crx3` cartella.

   Se, ad esempio, esegui un&#39;istanza AEM TarMK con un archivio dati file esterno, hai bisogno di questi file di configurazione:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Di seguito trovi configurazioni di esempio per l’istanza primaria:

   **Esempio di** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

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

1. Avvia l&#39;attività primaria assicurandoti di specificare la modalità di esecuzione primaria:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Crea un nuovo logger di registrazione Sling Apache per **org.apache.jackrabbit.oak.segment** pacchetto. Imposta il livello di log su &quot;Debug&quot; e punta l&#39;output del log su un file di log separato, come */logs/tarmk-coldstandby.log*. Per ulteriori informazioni, consulta [Registrazione](/help/sites-deploying/configure-logging.md).
1. Passa alla posizione del **secondario** e avvialo eseguendo il jar.
1. Crea la stessa configurazione di registrazione della principale. Quindi, ferma l&#39;istanza.
1. Quindi, prepara l&#39;istanza di standby. A questo scopo, esegui gli stessi passaggi dell’istanza primaria:

   1. Elimina i file che potrebbero essere presenti in `aem-standby/crx-quickstart/install`.
   1. Crea una nuova cartella denominata `install.standby` sotto `aem-standby/crx-quickstart/install`

   1. Crea due file di configurazione denominati:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. Crea una nuova cartella denominata `crx3` sotto `aem-standby/crx-quickstart/install`

   1. Crea la configurazione dell’archivio dati e inseriscila in `aem-standby/crx-quickstart/install/crx3`. Per questo esempio, il file da creare è:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. Modifica i file e crea le configurazioni necessarie.

   Di seguito sono riportati alcuni file di configurazione di esempio per una tipica istanza di standby:

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

1. Avvia la **secondario** ad esempio utilizzando la modalità di esecuzione in standby:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

Il servizio può essere configurato anche tramite la console Web tramite:

1. Andando alla console Web all&#39;indirizzo: *https://serveraddress:serverport/system/console/configMgr*
1. Ricerca di un servizio denominato **Servizio di standby a freddo del segmento Tar Jackrabbit Oak Apache** e fai doppio clic su di esso per modificare le impostazioni.
1. Salvataggio delle impostazioni e riavvio delle istanze in modo che le nuove impostazioni possano avere effetto.

>[!NOTE]
>
>Puoi controllare il ruolo di un&#39;istanza in qualsiasi momento controllando la presenza di **primario** o **secondario** modalità di esecuzione nella console Web delle impostazioni Sling.
>
>Questo può essere fatto andando *https://localhost:4502/system/console/status-slingsettings* e controllare **&quot;Modalità di esecuzione&quot;** linea.

## Prima sincronizzazione {#first-time-synchronization}

Una volta completata la preparazione e avviato lo standby per la prima volta, il traffico di rete tra le istanze sarà intenso, in quanto lo standby raggiunge il livello principale. È possibile consultare i registri per osservare lo stato della sincronizzazione.

In standby *tarmk-coldstandby.log*, vedrai voci come:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

Nel sistema di standby *error.log*, dovresti visualizzare una voce come questa:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

Nello snippet di log di cui sopra, *10.20.30.40* è l&#39;indirizzo IP del principale.

In **primario** *tarmk-coldstandby.log*, vedrai voci come:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

In questo caso, il &quot;client&quot; menzionato nel registro è il **secondario** istanza.

Una volta che queste voci smettono di comparire nel registro, puoi tranquillamente presumere che il processo di sincronizzazione sia completo.

Sebbene le voci di cui sopra mostrano che il meccanismo di polling funziona correttamente, spesso è utile capire se ci sono dati in fase di sincronizzazione mentre si verifica il polling. A questo scopo, cerca voci come:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Inoltre, quando si esegue con un `FileDataStore`, messaggi come il seguente confermeranno che i file binari vengono trasmessi correttamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configurazione {#configuration}

Per il servizio di standby a freddo sono disponibili le seguenti impostazioni OSGi:

* **Configurazione persistente:** se attivato, la configurazione verrà memorizzata nell’archivio anziché nei file di configurazione OSGi tradizionali. Si consiglia di mantenere questa impostazione disabilitata sui sistemi di produzione in modo che la configurazione primaria non venga estratta dallo standby.

* **Modalità (`mode`):** in questo modo verrà scelta la modalità runmode dell&#39;istanza.

* **Porta (porta):** la porta da utilizzare per la comunicazione. Il valore predefinito è `8023`.

* **Host principale (`primary.host`):** - l&#39;host dell&#39;istanza primaria. Questa impostazione è applicabile solo per lo standby.
* **Intervallo di sincronizzazione (`interval`):** - questa impostazione determina l&#39;intervallo tra la richiesta di sincronizzazione ed è applicabile solo per l&#39;istanza di standby.

* **Intervalli IP consentiti (`primary.allowed-client-ip-ranges`):** - gli intervalli IP da cui il principale consente le connessioni.
* **Secure (`secure`):** Abilita la crittografia SSL. Per utilizzare questa impostazione, deve essere abilitata su tutte le istanze.
* **Timeout lettura standby (`standby.readtimeout`):** Timeout per le richieste emesse dall&#39;istanza di standby in millisecondi. Il valore predefinito utilizzato è 60000 (un minuto).

* **Pulizia automatica in standby (`standby.autoclean`):** Chiama il metodo di pulizia se la dimensione dell&#39;archivio aumenta su un ciclo di sincronizzazione.

>[!NOTE]
>
>Si consiglia vivamente che il principale e lo standby abbiano ID archivio diversi per renderli identificabili separatamente per servizi come Offloading.
>
>Il modo migliore per assicurarsi che questo sia coperto è eliminando il *sling.id* in standby e riavvia l&#39;istanza.

## Procedure di failover {#failover-procedures}

Nel caso in cui l&#39;istanza primaria non riesca per qualsiasi motivo, è possibile impostare una delle istanze di standby per assumere il ruolo del primario modificando la modalità di esecuzione iniziale come descritto di seguito:

>[!NOTE]
>
>Anche i file di configurazione devono essere modificati in modo che corrispondano alle impostazioni utilizzate per l&#39;istanza primaria.

1. Vai nel punto in cui è installata l&#39;istanza di standby e interromperla.

1. Se hai un load balancer configurato con la configurazione, a questo punto puoi rimuovere il principale dalla configurazione del load balancer.
1. Esegui il backup del `crx-quickstart` dalla cartella di installazione di standby. Può essere utilizzato come punto di partenza quando si imposta un nuovo standby.

1. Riavvia l&#39;istanza utilizzando `primary` modalità di esecuzione:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Aggiungi il nuovo primario al load balancer.
1. Crea e avvia una nuova istanza di standby. Per ulteriori informazioni, consulta la procedura sopra descritta su [Creazione di una configurazione di standby a freddo AEM TarMK](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Applicazione degli hotfix a una configurazione di standby a freddo {#applying-hotfixes-to-a-cold-standby-setup}

Il modo consigliato per applicare gli hotfix a una configurazione stanby a freddo è installarli nell&#39;istanza primaria e poi clonarli in una nuova istanza standby a freddo con gli hotfix installati.

Per farlo, segui i passaggi descritti di seguito:

1. Arresta il processo di sincronizzazione sull&#39;istanza di standby a freddo andando alla console JMX e utilizzando il **org.apache.jackrabbit.oak: Stato (&quot;Standby&quot;)**bean Per ulteriori informazioni su come eseguire questa operazione, consulta la sezione su [Monitoraggio](#monitoring).
1. Arrestare l&#39;istanza di standby a freddo.
1. Installa l&#39;hotfix sull&#39;istanza primaria. Per ulteriori dettagli su come installare un hotfix, vedi [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md).
1. Testa l&#39;istanza per i problemi successivi all&#39;installazione.
1. Rimuovere l&#39;istanza standby a freddo eliminando la relativa cartella di installazione.
1. Arrestare l&#39;istanza primaria e clonarla eseguendo una copia del file system dell&#39;intera cartella di installazione nella posizione dello standby a freddo.
1. Riconfigura il clone appena creato per fungere da istanza di standby a freddo. Per ulteriori dettagli, consulta [Creazione di una configurazione di standby a freddo AEM TarMK.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Avviare sia le istanze di standby principale che quelle di standby a freddo.

## Monitoraggio {#monitoring}

La funzione espone le informazioni utilizzando JMX o MBeans. In questo modo è possibile controllare lo stato corrente dello standby e del master utilizzando [Console JMX](/help/sites-administering/jmx-console.md). Le informazioni si trovano in un MBean di `type org.apache.jackrabbit.oak:type="Standby"`denominato `Status`.

**Standby**

Osservando un&#39;istanza di standby si espone un nodo. L’ID è in genere un UUID generico.

Questo nodo ha cinque attributi di sola lettura:

* `Running:` valore booleano che indica se il processo di sincronizzazione è in esecuzione o meno.

* `Mode:` Client: seguito dall’UUID utilizzato per identificare l’istanza. Tieni presente che questo UUID cambierà ogni volta che la configurazione viene aggiornata.

* `Status:` una rappresentazione testuale dello stato corrente (come `running` o `stopped`).

* `FailedRequests:`il numero di errori consecutivi.
* `SecondsSinceLastSuccess:` il numero di secondi dall&#39;ultima comunicazione riuscita con il server. Verrà visualizzato `-1` se non è stata effettuata alcuna comunicazione.

Sono inoltre disponibili tre metodi richiamabili:

* `start():` avvia il processo di sincronizzazione.
* `stop():` interrompe il processo di sincronizzazione.
* `cleanup():` esegue l&#39;operazione di pulizia in standby.

**Principale**

Osservando il principale si espongono alcune informazioni generali tramite un MBean il cui valore ID è il numero di porta utilizzato dal servizio di standby TarMK (8023 per impostazione predefinita). La maggior parte dei metodi e degli attributi sono gli stessi utilizzati per lo standby, ma alcuni sono diversi:

* `Mode:` mostrerà sempre il valore `primary`.

È inoltre possibile recuperare informazioni per un massimo di 10 client (istanze di standby) collegati al master. L&#39;ID MBean è l&#39;UUID dell&#39;istanza. Non esistono metodi richiamabili per questi MBeans, ma alcuni attributi di sola lettura molto utili:

* `Name:` ID del client.
* `LastSeenTimestamp:` la marca temporale dell’ultima richiesta in una rappresentazione testuale.
* `LastRequest:` l’ultima richiesta del client.
* `RemoteAddress:` l’indirizzo IP del client.
* `RemotePort:` la porta utilizzata dal client per l’ultima richiesta.
* `TransferredSegments:` il numero totale di segmenti trasferiti a questo client.
* `TransferredSegmentBytes:`il numero totale di byte trasferiti al client.

## Manutenzione dell&#39;archivio in standby a freddo {#cold-standby-repository-maintenance}

### Pulizia revisioni {#revision-clean}

>[!NOTE]
>
>Se esegui [Pulizia revisioni online](/help/sites-deploying/revision-cleanup.md) sull&#39;istanza primaria non è necessaria la procedura manuale presentata di seguito. Inoltre, se utilizzi il cleanup delle revisioni online, la `cleanup ()` l&#39;operazione sull&#39;istanza di standby viene eseguita automaticamente.

>[!NOTE]
>
>Non eseguire la pulizia revisioni offline in standby. Non è necessario e non ridurrà la dimensione del segmentstore.

L&#39;Adobe consiglia di eseguire regolarmente la manutenzione per evitare una crescita eccessiva del repository nel tempo. Per eseguire manualmente la manutenzione dell&#39;archivio in standby a freddo, segui i passaggi seguenti:

1. Arresta il processo di standby sull&#39;istanza di standby andando alla console JMX e utilizzando il **org.apache.jackrabbit.oak: Stato (&quot;Standby&quot;)** fagiolo. Per ulteriori informazioni su come eseguire questa operazione, consulta la sezione precedente su [Monitoraggio](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Interrompi l&#39;istanza AEM primaria.
1. Esegui lo strumento di compattazione oak sull&#39;istanza primaria. Per ulteriori dettagli, consulta [Manutenzione dell’archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Avvia l&#39;istanza primaria.
1. Avvia il processo di standby sull&#39;istanza di standby utilizzando lo stesso fagiolo JMX come descritto nel primo passaggio.
1. Controlla i registri e attendi il completamento della sincronizzazione. È possibile che in questo momento si assista a una crescita sostanziale nell&#39;archivio di standby.
1. Esegui il `cleanup()` sull&#39;istanza di standby, utilizzando lo stesso fagiolo JMX come descritto nel primo passaggio.

Potrebbe essere necessario più tempo del solito perché l&#39;istanza di standby completi la sincronizzazione con la principale, in quanto la compattazione offline riscrive efficacemente la cronologia dell&#39;archivio, rendendo il calcolo delle modifiche negli archivi più tempo. Va inoltre notato che una volta completato questo processo, la dimensione dell’archivio sullo standby sarà approssimativamente uguale alla dimensione dell’archivio sul principale.

In alternativa, l&#39;archivio primario può essere copiato manualmente sullo standby dopo aver eseguito la compattazione sul primario, essenzialmente ricostruendo lo standby ogni volta che la compattazione viene eseguita.

### Archivio dati raccolta oggetti inattivi {#data-store-garbage-collection}

È importante eseguire la raccolta degli oggetti inattivi sulle istanze del datastore del file di tanto in tanto come altrimenti, i file binari eliminati rimarranno sul filesystem, infine riempire l&#39;unità. Per eseguire la raccolta degli oggetti inattivi, segui la procedura seguente:

1. Eseguire la manutenzione dell’archivio in standby a freddo come descritto nella sezione [sopra](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Al termine del processo di manutenzione e al riavvio delle istanze:

   * Sul primario, esegui la raccolta degli oggetti inattivi dell&#39;archivio dati tramite i fagioli JMX pertinenti come descritto in [articolo](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * In standby, la raccolta degli oggetti inattivi nell’archivio dati è disponibile solo tramite il **BlobGarbageCollection** MBean - `startBlobGC()`. Il file **RepositoryManagement **MBean non è disponibile nello standby.

   >[!NOTE]
   >
   >Nel caso in cui non si utilizzi un archivio dati condiviso, la raccolta degli oggetti inattivi dovrà prima essere eseguita sul computer primario e poi sul sistema di standby.
