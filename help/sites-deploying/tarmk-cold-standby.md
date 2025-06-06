---
title: Come eseguire l’AEM con TarMK Cold Standby
description: Scopri come creare, configurare e gestire una configurazione TarMK Cold Standby.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 0%

---

# Come eseguire l’AEM con TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Introduzione {#introduction}

La capacità di standby a freddo del microkernel Tar consente a una o più istanze di Adobe Experience Manager (AEM) in standby di connettersi a un&#39;istanza primaria. Il processo di sincronizzazione è unidirezionale, ovvero viene eseguito solo dalle istanze primarie a quelle in standby.

Lo scopo delle istanze in standby è garantire una Live Data Copy dell’archivio master e garantire un passaggio rapido senza perdita di dati nel caso in cui il master non sia disponibile per qualsiasi motivo.

Il contenuto viene sincronizzato in modo lineare tra l’istanza primaria e le istanze in standby senza che venga eseguita alcuna verifica di integrità per individuare eventuali danneggiamenti a livello di file o archivio. A causa di questa progettazione, le istanze in standby sono copie esatte dell’istanza primaria e non possono aiutare a mitigare le incoerenze sulle istanze primarie.

>[!NOTE]
>
>La funzione di standby a freddo è destinata a proteggere gli scenari in cui è richiesta un&#39;elevata disponibilità sulle istanze **Author**. Per le situazioni in cui è richiesta un&#39;elevata disponibilità nelle istanze **Publish** che utilizzano il microkernel Tar, l&#39;Adobe consiglia di utilizzare una farm di pubblicazione.
>
>Per informazioni su altre distribuzioni disponibili, consulta la pagina [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Quando l&#39;istanza Standby è configurata o derivata dal nodo Principale, consente solo l&#39;accesso alla seguente console (per le attività relative all&#39;amministrazione):
>
>* Console web OSGI
>
>Altre console non sono accessibili.

## Come funziona {#how-it-works}

Nell&#39;istanza AEM primaria viene aperta una porta TCP in ascolto dei messaggi in arrivo. Attualmente, esistono due tipi di messaggi che gli schiavi inviano al master:

* un messaggio che richiede l’ID del segmento dell’head corrente
* un messaggio che richiede i dati del segmento con un ID specificato

Lo standby richiede periodicamente l’ID del segmento dell’intestazione corrente del primario. Se il segmento è localmente sconosciuto, viene recuperato. Se è già presente, i segmenti vengono confrontati e, se necessario, vengono richiesti anche i segmenti di riferimento.

>[!NOTE]
>
>Le istanze in standby non ricevono alcun tipo di richiesta perché sono in esecuzione in modalità di sola sincronizzazione. L’unica sezione disponibile in un’istanza in standby è la console web, per facilitare la configurazione di bundle e servizi.

Una tipica distribuzione TarMK Cold Standby:

![chlimage_1](assets/chlimage_1.png)

## Altre caratteristiche {#other-characteristics}

### Robustezza {#robustness}

Il flusso di dati è progettato per rilevare e gestire automaticamente i problemi di connessione e di rete. Tutti i pacchetti sono raggruppati con checksum e quando si verificano problemi con la connessione o pacchetti danneggiati, vengono attivati meccanismi di esecuzione di nuovi tentativi.

#### Prestazioni {#performance}

L’abilitazione dello standby a freddo di TarMK sull’istanza principale non ha quasi alcun impatto misurabile sulle prestazioni. Il consumo aggiuntivo di CPU è basso e il disco rigido e l&#39;I/O di rete in eccesso non dovrebbero produrre problemi di prestazioni.

In standby, è possibile prevedere un consumo elevato della CPU durante il processo di sincronizzazione. Poiché la procedura non è multithreading, non può essere velocizzata utilizzando più core. Se non vengono modificati o trasferiti dati, non esiste alcuna attività misurabile. La velocità di connessione varia a seconda dell’hardware e dell’ambiente di rete, ma non dipende dalle dimensioni dell’archivio o dall’utilizzo SSL. Tieni presente questo aspetto durante la stima del tempo necessario per una sincronizzazione iniziale o quando nel frattempo sono stati modificati molti dati sul nodo principale.

#### Sicurezza {#security}

Supponendo che tutte le istanze vengano eseguite nella stessa area di sicurezza Intranet, il rischio di violazione della sicurezza risulta notevolmente ridotto. Tuttavia, è possibile aggiungere un ulteriore livello di sicurezza abilitando le connessioni SSL tra gli schiavi e il master. In questo modo si riduce la possibilità che i dati vengano compromessi da un uomo nel mezzo.

Inoltre, è possibile specificare le istanze in standby a cui è consentito connettersi limitando l’indirizzo IP delle richieste in ingresso. Ciò dovrebbe contribuire a garantire che nessuno nella Intranet possa copiare l’archivio.

>[!NOTE]
>
>Si consiglia di aggiungere un load balancer tra Dispatcher e i server che fanno parte della configurazione di standby a freddo. Il load balancer deve essere configurato in modo da indirizzare il traffico utente solo all&#39;istanza **primary**. Ciò è necessario per garantire la coerenza ed evitare che il contenuto venga copiato nell’istanza in standby con mezzi diversi dal meccanismo di standby a freddo.

## Creazione di una configurazione AEM TarMK Cold Standby {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>Il PID per l’archivio dei nodi di segmento e il servizio archivio in standby sono cambiati in AEM 6.3 rispetto alle versioni precedenti come segue:
>
>* da org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService in org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* da org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService in org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>Effettuare le regolazioni di configurazione necessarie in modo che riflettano questa modifica.

Per creare una configurazione TarMK cold standby, creare innanzitutto le istanze standby eseguendo una copia dell&#39;intera cartella di installazione del primario in un nuovo percorso. È quindi possibile avviare ogni istanza con una modalità di esecuzione che specifichi il relativo ruolo ( `primary` o `standby`).

Di seguito è riportata la procedura da seguire per creare una configurazione con una istanza principale e una in standby:

1. Installare AEM.

1. Arrestare l&#39;istanza e copiare la cartella di installazione nel percorso da cui viene eseguita l&#39;istanza di standby a freddo. Anche se si esegue da computer diversi, assicurarsi di assegnare a ogni cartella un nome descrittivo (ad esempio *aem-primary* o *aem-standby*) per differenziare le istanze.
1. Vai alla cartella di installazione dell’istanza primaria e:

   1. Verifica ed elimina eventuali configurazioni OSGi precedenti che potresti avere in `aem-primary/crx-quickstart/install`

   1. Crea una cartella denominata `install.primary` in `aem-primary/crx-quickstart/install`

   1. Creare le configurazioni richieste per l&#39;archivio nodi e l&#39;archivio dati preferiti in `aem-primary/crx-quickstart/install/install.primary`
   1. Creare un file denominato `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` nella stessa posizione e configurarlo di conseguenza. Per ulteriori informazioni sulle opzioni di configurazione, vedere [Configurazione](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Se si utilizza un&#39;istanza di AEM TarMK con un archivio dati esterno, creare una cartella denominata `crx3` in `aem-primary/crx-quickstart/install` denominata `crx3`

   1. Inserire il file di configurazione dell&#39;archivio dati nella cartella `crx3`.

   Ad esempio, se esegui un’istanza AEM TarMK con un archivio dati file esterno, sono necessari i seguenti file di configurazione:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Di seguito sono riportate alcune configurazioni di esempio per l’istanza principale:

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

1. Avvia l’esecuzione primaria accertandosi di specificare la modalità di esecuzione primaria:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Crea un logger di registrazione Apache Sling per il pacchetto **org.apache.jackrabbit.oak.segment**. Impostare il livello di registro su &quot;Debug&quot; e puntare l&#39;output del registro su un file di registro separato, ad esempio */logs/tarmk-coldstandby.log*. Per ulteriori informazioni, vedere [Registrazione](/help/sites-deploying/configure-logging.md).
1. Vai alla posizione dell&#39;istanza **standby** e avviala eseguendo il file jar.
1. Crea la stessa configurazione di registrazione del principale. Quindi, arresta l’istanza.
1. Quindi, prepara l’istanza in standby. Per farlo, esegui gli stessi passaggi dell’istanza principale:

   1. Eliminare tutti i file eventualmente presenti in `aem-standby/crx-quickstart/install`.
   1. Crea una cartella denominata `install.standby` in `aem-standby/crx-quickstart/install`

   1. Crea due file di configurazione denominati:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. Crea una cartella denominata `crx3` in `aem-standby/crx-quickstart/install`

   1. Creare la configurazione dell&#39;archivio dati e inserirla in `aem-standby/crx-quickstart/install/crx3`. In questo esempio, il file da creare è:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. Modifica i file e crea le configurazioni necessarie.

   Di seguito sono riportati alcuni file di configurazione per una tipica istanza in standby:

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

1. Avvia l&#39;istanza **standby** utilizzando la modalità di esecuzione in standby:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

Il servizio può essere configurato anche tramite la console web:

1. Accesso alla console Web all&#39;indirizzo: *https://serveraddress:serverport/system/console/configMgr*
1. È in corso la ricerca di un servizio denominato **Apache Jackrabbit Oak Segment Tar Cold Standby Service** e fare doppio clic su di esso per modificare le impostazioni.
1. Salvataggio delle impostazioni e riavvio delle istanze in modo che le nuove impostazioni possano avere effetto.

>[!NOTE]
>
>Puoi controllare il ruolo di un&#39;istanza in qualsiasi momento controllando la presenza delle modalità di esecuzione **primary** o **standby** nella console Web Impostazioni Sling.
>
>Per eseguire questa operazione, vai a *https://localhost:4502/system/console/status-slingsettings* e controlla la riga **&quot;Modalità di esecuzione&quot;**.

## Prima sincronizzazione {#first-time-synchronization}

Una volta completata la preparazione e avviato lo standby per la prima volta, si verifica un intenso traffico di rete tra le istanze quando lo standby raggiunge il livello primario. È possibile consultare i registri per osservare lo stato della sincronizzazione.

In standby *tarmk-coldstandby.log*, è possibile visualizzare le voci seguenti:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

Nel *error.log* dello standby dovrebbe essere visualizzata una voce come questa:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

Nel frammento di registro precedente, *10.20.30.40* è l&#39;indirizzo IP del primario.

In **primary** *tarmk-coldstandby.log* sono presenti le voci seguenti:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

In questo caso, il &quot;client&quot; menzionato nel registro è l&#39;istanza **standby**.

Una volta che queste voci non sono più visualizzate nel registro, puoi tranquillamente supporre che il processo di sincronizzazione sia completo.

Anche se le voci precedenti mostrano che il meccanismo di polling funziona correttamente, spesso è utile capire se vi sono dati sincronizzati mentre si verifica il polling. A tale scopo, cercare voci come le seguenti:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Inoltre, quando si esegue con un `FileDataStore` non condiviso, i messaggi come quelli riportati di seguito confermano che i file binari vengono trasmessi correttamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configurazione {#configuration}

Per il servizio di standby a freddo sono disponibili le seguenti impostazioni OSGi:

* **Configurazione persistente:** se abilitata, la configurazione viene archiviata nell&#39;archivio anziché nei file di configurazione OSGi tradizionali. L&#39;Adobe consiglia di mantenere l&#39;impostazione disabilitata sui sistemi di produzione in modo che la configurazione principale non venga richiamata dallo standby.

* **Modalità (`mode`):** consente di scegliere la modalità di esecuzione dell&#39;istanza.

* **Porta (porta):** la porta da utilizzare per la comunicazione. Il valore predefinito è `8023`.

* **Host primario (`primary.host`):** - host dell&#39;istanza primaria. Questa impostazione è applicabile solo allo standby.
* **Intervallo di sincronizzazione (`interval`):** - questa impostazione determina l&#39;intervallo tra le richieste di sincronizzazione ed è applicabile solo per l&#39;istanza in standby.

* **Intervalli IP consentiti (`primary.allowed-client-ip-ranges`):** - Intervalli IP da cui il primario consente le connessioni.
* **Proteggi (`secure`):** Abilita crittografia SSL. Per utilizzare questa impostazione, è necessario che sia attivata su tutte le istanze.
* **Timeout lettura in standby (`standby.readtimeout`):** Timeout per le richieste emesse dall&#39;istanza in standby in millisecondi. Il valore predefinito utilizzato è 60000 (un minuto).

* **Pulizia automatica standby (`standby.autoclean`):** Chiama il metodo di pulizia se la dimensione dell&#39;archivio aumenta durante un ciclo di sincronizzazione.

>[!NOTE]
>
>L’Adobe consiglia di utilizzare ID di archivio diversi per primario e standby, in modo che siano identificabili separatamente per servizi come Offload.
>
>Il modo migliore per assicurarsi che ciò sia coperto è quello di eliminare *sling.id* in standby e riavviare l&#39;istanza.

## Procedure di failover {#failover-procedures}

Nel caso in cui l’istanza principale non riesca per qualsiasi motivo, puoi impostare una delle istanze in standby per assumere il ruolo di principale modificando la modalità di esecuzione iniziale come descritto di seguito:

>[!NOTE]
>
>Modifica i file di configurazione in modo che corrispondano alle impostazioni utilizzate per l’istanza principale.

1. Andare alla posizione in cui è installata l&#39;istanza di standby e arrestarla.

1. Nel caso in cui sia configurato un load balancer con la configurazione, a questo punto è possibile rimuovere il primario dalla configurazione del load balancer.
1. Backup della cartella `crx-quickstart` dalla cartella di installazione in standby. Può essere utilizzato come punto di partenza quando si imposta una nuova modalità di standby.

1. Riavviare l&#39;istanza utilizzando la modalità di esecuzione `primary`:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Aggiungi il nuovo primario al load balancer.
1. Crea e avvia una nuova istanza in standby. Per ulteriori informazioni, vedere la procedura precedente in [Creazione di un&#39;installazione di standby a freddo di AEM TarMK](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Applicazione di hotfix a una configurazione di standby a freddo {#applying-hotfixes-to-a-cold-standby-setup}

Per applicare gli hotfix a una configurazione di standby a freddo, si consiglia di installarli nell&#39;istanza principale e quindi di clonarli in una nuova istanza di standby a freddo con gli hotfix installati.

Per farlo, segui i passaggi descritti di seguito:

1. Arresta il processo di sincronizzazione sull’istanza in standby a freddo passando alla console JMX e utilizzando **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**&#x200B;bean. Per ulteriori informazioni su come eseguire questa operazione, vedere la sezione relativa al [monitoraggio](#monitoring).
1. Arrestare l&#39;istanza di standby a freddo.
1. Installa l’hotfix sull’istanza primaria. Per ulteriori dettagli su come installare un hotfix, vedi [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md).
1. Verificare la presenza di eventuali problemi dopo l&#39;installazione.
1. Rimuovere l&#39;istanza di standby a freddo eliminando la relativa cartella di installazione.
1. Arrestare l&#39;istanza primaria e clonarla eseguendo una copia del file system dell&#39;intera cartella di installazione nella posizione dello standby a freddo.
1. Riconfigura il clone appena creato in modo che agisca come istanza di standby a freddo. Vedere [Creazione di un&#39;installazione di standby a freddo di AEM TarMK.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Avviare le istanze di standby primario e a freddo.

## Monitoraggio {#monitoring}

La funzione espone informazioni utilizzando JMX o MBean. In questo modo è possibile controllare lo stato corrente dello standby e del master utilizzando la [console JMX](/help/sites-administering/jmx-console.md). Le informazioni sono disponibili in un MBean di `type org.apache.jackrabbit.oak:type="Standby"` denominato `Status`.

**Standby**

Osservando un’istanza in standby, puoi esporre un nodo. L’ID è in genere un UUID generico.

Questo nodo dispone di cinque attributi di sola lettura:

* Valore booleano `Running:` che indica se il processo di sincronizzazione è in esecuzione o meno.

* Client `Mode:`: seguito dall&#39;UUID utilizzato per identificare l&#39;istanza. Questo UUID cambia ogni volta che la configurazione viene aggiornata.

* `Status:` una rappresentazione testuale dello stato corrente (come `running` o `stopped`).

* `FailedRequests:`il numero di errori consecutivi.
* `SecondsSinceLastSuccess:` il numero di secondi dall&#39;ultima comunicazione riuscita con il server. Se non è stata effettuata una comunicazione corretta, visualizza `-1`.

Sono inoltre disponibili tre metodi richiamabili:

* `start():` avvia il processo di sincronizzazione.
* `stop():` interrompe il processo di sincronizzazione.
* `cleanup():` esegue l&#39;operazione di pulizia in standby.

**Principale**

L’osservazione del primario espone alcune informazioni generali tramite un MBean il cui valore ID è il numero di porta utilizzato dal servizio di standby TarMK (8023 per impostazione predefinita). La maggior parte dei metodi e degli attributi sono gli stessi della modalità standby, ma alcuni differiscono tra loro:

* `Mode:` mostra sempre il valore `primary`.

È inoltre possibile recuperare le informazioni per un massimo di dieci client (istanze in standby) connessi al master. L’ID MBean è l’UUID dell’istanza. Non esistono metodi richiamabili per questi MBean, ma alcuni utili attributi di sola lettura:

* `Name:` ID del client.
* `LastSeenTimestamp:` il timestamp dell&#39;ultima richiesta in una rappresentazione testuale.
* `LastRequest:` l&#39;ultima richiesta del client.
* `RemoteAddress:` indirizzo IP del client.
* `RemotePort:` la porta utilizzata dal client per l&#39;ultima richiesta.
* `TransferredSegments:` il numero totale di segmenti trasferiti a questo client.
* `TransferredSegmentBytes:`numero totale di byte trasferiti al client.

## Manutenzione archivio in standby a freddo {#cold-standby-repository-maintenance}

### Pulizia revisioni {#revision-clean}

>[!NOTE]
>
>Se si esegue [Pulizia revisioni in linea](/help/sites-deploying/revision-cleanup.md) sull&#39;istanza principale, la procedura manuale illustrata di seguito non è necessaria. Inoltre, se si utilizza la pulizia delle revisioni in linea, l&#39;operazione `cleanup ()` sull&#39;istanza in standby viene eseguita automaticamente.

>[!NOTE]
>
>Non eseguire la pulizia revisioni offline in standby. Non è necessario e non riduce le dimensioni dell’archivio segmenti.

L’Adobe consiglia di eseguire regolarmente la manutenzione per evitare una crescita eccessiva dell’archivio nel tempo. Per eseguire manualmente la manutenzione dell’archivio in standby a freddo, effettua le seguenti operazioni:

1. Arrestare il processo di standby nell&#39;istanza di standby accedendo alla console JMX e utilizzando il bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Per ulteriori informazioni su come eseguire questa operazione, consulta la sezione precedente sul [monitoraggio](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Arresta l’istanza AEM primaria.
1. Esegui lo strumento di compattazione di Oak sull’istanza principale. Per ulteriori dettagli, vedere [Gestione dell&#39;archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Avvia l’istanza primaria.
1. Avvia il processo di standby sull’istanza in standby utilizzando lo stesso bean JMX descritto nel primo passaggio.
1. Guarda i registri e attendi il completamento della sincronizzazione. È possibile che attualmente si osservi una crescita notevole nell’archivio in standby.
1. Eseguire l&#39;operazione `cleanup()` sull&#39;istanza in standby, utilizzando lo stesso bean JMX descritto nel primo passaggio.

Potrebbe essere necessario più tempo del solito perché l’istanza in standby completi la sincronizzazione con la directory principale, poiché la compattazione offline riscrive efficacemente la cronologia dell’archivio, rendendo così più lungo il calcolo delle modifiche negli archivi. Al termine di questo processo, le dimensioni dell’archivio in standby sono all’incirca le stesse dell’archivio nell’archivio primario.

In alternativa, l’archivio primario può essere copiato manualmente in standby dopo l’esecuzione della compattazione sul principale, essenzialmente ricostruendo lo standby ogni volta che viene eseguita la compattazione.

### Raccolta oggetti inattivi in archivio dati {#data-store-garbage-collection}

È importante eseguire di tanto in tanto la Garbage Collection sulle istanze dell’archivio dati dei file. In caso contrario, i file binari eliminati rimangono nel file system e finiscono per riempire l’unità. Per eseguire la raccolta di oggetti inattivi, attieniti alla procedura seguente:

1. Eseguire la manutenzione dell&#39;archivio in standby a freddo come descritto nella sezione [precedente](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Dopo il completamento del processo di manutenzione e il riavvio delle istanze:

   * Sul database primario, eseguire la raccolta di oggetti inattivi dell&#39;archivio dati tramite il bean JMX pertinente come descritto in [Esecuzione della raccolta di oggetti inattivi dell&#39;archivio dati tramite la console JMX](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * In standby, la raccolta di oggetti inattivi dell&#39;archivio dati è disponibile solo tramite **BlobGarbageCollection** MBean - `startBlobGC()`. **RepositoryManagement** MBean non disponibile in standby.

   >[!NOTE]
   >
   >Se non utilizzi un archivio dati condiviso, esegui prima la raccolta di oggetti inattivi sul server principale e quindi in standby.
