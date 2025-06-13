---
title: Risoluzione dei problemi di installazione con AEM
description: Questo articolo descrive alcuni dei problemi di installazione che potresti incontrare con AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 0%

---

# Risoluzione dei problemi di installazione con AEM{#troubleshooting}

AEM Questa sezione include informazioni dettagliate sui registri disponibili per aiutarti a risolvere eventuali problemi e informazioni su alcuni di essi.

## Risolvere i problemi relativi alle prestazioni dell&#39;autore {#troubleshoot-author-performance}

L’analisi delle prestazioni lente nell’istanza di authoring può diventare complessa. Come primo passo è necessario capire a quale livello dello stack tecnologico le prestazioni stanno diminuendo.

Il seguente albero decisionale fornisce indicazioni per ridurre il collo di bottiglia.

![chlimage_1-75](assets/chlimage_1-75.png)

## Ottimizzazione di base {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configurazione dei file di registro e dei registri di controllo {#configuring-log-files-and-audit-logs}

AEM registra registri dettagliati che è possibile configurare per la risoluzione dei problemi di installazione. Per informazioni, vedere la sezione [Utilizzo dei record di controllo e dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Utilizzo dell&#39;opzione Dettagliato {#using-the-verbose-option}

Quando si avvia AEM WCM, è possibile aggiungere l’opzione -v (dettagliata) alla riga di comando come in: java -jar cq-wcm-quickstart-&lt;versione>.jar -v.

L’opzione dettagliata visualizza parte dell’output del registro Quickstart sulla console, in modo che possa essere utilizzato per la risoluzione dei problemi.

## Problemi comuni di installazione {#common-installation-issues}

Nella sezione seguente vengono descritti alcuni problemi di installazione e le relative soluzioni.

### Fare doppio clic sul file JAR Quickstart non ha alcun effetto o apre il file JAR con un altro programma (ad esempio, Archive Manager). {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

Questo problema indica in genere un problema relativo alla configurazione dell&#39;ambiente desktop del sistema operativo per l&#39;apertura di file con estensione .jar. Potrebbe anche indicare che non hai installato Java™ o che stai utilizzando una versione di Java non supportata™.

Poiché i file jar utilizzano il formato ZIP onnipresente, alcuni programmi di archiviazione possono configurare automaticamente il desktop per aprire i file jar come file di archivio.

Per risolvere i problemi, effettuare le seguenti operazioni:

* Verifica di avere installato almeno Java™ versione 1.6.
* Prova un menu contestuale (in genere con un clic con il pulsante destro del mouse) su AEM WCM Quickstart e seleziona &quot;Apri con&quot;....
* Verifica se Java™ o Sun Java™ è elencato e prova a eseguire AEM WCM con esso. Se hai installato più versioni di Java™, seleziona quella supportata.

  Se si esegue questo passaggio e il sistema operativo in uso offre l&#39;opzione di utilizzare sempre il programma selezionato per eseguire i file .jar, selezionarlo. D’ora in poi il doppio clic dovrebbe funzionare.

* A volte la reinstallazione della versione Java™ supportata aiuta a ripristinare l’associazione corretta.
* È sempre possibile eseguire CRX utilizzando la riga di comando o gli script di avvio/arresto come descritto in precedenza in questo documento.

### La mia applicazione in esecuzione su CRX genera errori di memoria insufficiente {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Vedi anche [Analizzare i problemi di memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).


La stessa CRX ha un ingombro di memoria ridotto. Se l’applicazione in esecuzione in CRX ha requisiti di memoria più elevati o richiede operazioni che richiedono molta memoria (ad esempio, transazioni di grandi dimensioni), l’istanza JVM in cui viene eseguito CRX deve essere avviata con le impostazioni di memoria appropriate.

Utilizza le opzioni di comando Java™ per definire le impostazioni di memoria della JVM (ad esempio, java -Xmx512m -jar crx&ast;.jar per impostare heapsize su 512 MB).

Specificare l&#39;opzione di impostazione della memoria durante l&#39;avvio di AEM WCM dalla riga di comando. È inoltre possibile modificare gli script di avvio/arresto di AEM WCM o gli script personalizzati per la gestione dell&#39;avvio di AEM WCM per definire le impostazioni di memoria richieste.

Se hai già definito l’heapsize su 512 MB, puoi analizzare ulteriormente il problema della memoria creando un’immagine heap.

Per creare automaticamente un’immagine heap quando la memoria è esaurita, utilizza il comando seguente:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &ast;.jar

Questo metodo genera un file dell&#39;immagine heap (**java_...hprof**) ogni volta che il processo esaurisce la memoria. Il processo può continuare a essere eseguito dopo la generazione dell’immagine heap.

Spesso per analizzare il problema sono necessari tre file dell’immagine heap, raccolti in un periodo di tempo:

* Prima che si verifichi un errore
* Durante l&#39;errore 1
* Durante l&#39;errore 2
* *Sarebbe opportuno raccogliere informazioni anche dopo la risoluzione dell&#39;evento*

Questi possono essere confrontati per vedere le modifiche e come gli oggetti usano la memoria.

>[!NOTE]
>
>Se raccogli regolarmente tali informazioni o hai esperienza nella lettura delle immagini heap, un file dell’immagine heap può essere sufficiente per analizzare il problema.

### La schermata iniziale di AEM non viene visualizzata nel browser dopo aver fatto doppio clic su AEM Quickstart {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

In alcune situazioni, le schermate di benvenuto di AEM WCM non vengono visualizzate automaticamente anche se l’archivio stesso è in esecuzione correttamente. Questo problema può dipendere dalla configurazione del sistema operativo, dalla configurazione del browser o da fattori simili.

Il sintomo comune è che nella finestra AEM WCM Quickstart viene visualizzato &quot;Avvio di AEM WCM in corso, in attesa dell’avvio del server&quot;.... Se il messaggio viene visualizzato per un periodo di tempo relativamente lungo, immetti manualmente l’URL di AEM WCM nella finestra del browser utilizzando la porta 4502 predefinita o la porta su cui è in esecuzione l’istanza: http://localhost:4502/.

Inoltre, i registri possono rivelare il motivo per cui il browser non si avvia.

A volte, nella finestra AEM WCM Quickstart viene visualizzato il messaggio &quot;AEM WCM in esecuzione su http://localhost:port/&quot; e il browser non si avvia automaticamente. In questo caso, fai clic sull’URL nella finestra AEM WCM Quickstart (si tratta di un collegamento ipertestuale) o immetti manualmente l’URL nel browser.

Se tutto il resto non funziona, controlla i registri per scoprire cosa è successo.

### Il sito web non viene caricato o ha esito negativo a intermittenza con Java™ 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}

Si è verificato un problema noto con AEM 6.5 in esecuzione su Java™ 11, a causa del quale il sito web potrebbe non venire caricato o non funzionare in modo intermittente.

Se si verifica questo problema, eseguire le operazioni seguenti:

1. Apri il file `sling.properties` nella cartella `crx-quickstart/conf/`
1. Individua la seguente riga:

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. Sostituiscilo con quanto segue:

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. Riavvia l’istanza.

## Risoluzione dei problemi relativi alle installazioni con un server applicazioni {#troubleshooting-installations-with-an-application-server}

### Pagina non trovata restituita durante la richiesta di una pagina geometrixx-outdoor {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**Si applica a WebLogic 10.3.5 e JBoss® 5.1**

Quando una richiesta inviata a geometrixx-outdoors/en page restituisce un valore 404 (Pagina non trovata), è possibile verificare di aver impostato la proprietà sling aggiuntiva nel file sling.properties necessaria per questi Application Server specifici.

Per informazioni dettagliate, consulta i passaggi *Distribuisci applicazione Web AEM*.

### La dimensione dell’intestazione di risposta può essere maggiore di 4 KB {#response-header-size-can-be-greater-than-kb}

Gli errori 502 possono indicare che il server web non può gestire le dimensioni dell’intestazione di risposta HTTP di AEM. AEM può generare intestazioni di risposta HTTP che includono cookie di dimensioni superiori a 4 KB. Assicurati che il contenitore del servlet sia configurato in modo che la dimensione massima dell’intestazione di risposta possa superare i 4 KB.

Ad esempio, per Tomcat 7.0, l&#39;attributo maxHttpHeaderSize del [connettore HTTP](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) controlla le limitazioni relative alla dimensione dell&#39;intestazione.

## Disinstallazione di Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Poiché AEM viene installato in un&#39;unica directory, non è necessaria un&#39;utilità di disinstallazione. La disinstallazione può essere semplice come l’eliminazione dell’intera directory di installazione, anche se il modo in cui disinstalli AEM dipende da cosa desideri ottenere e da quale archiviazione persistente utilizzi.

Se l&#39;archiviazione persistente è incorporata nella directory di installazione, ad esempio nell&#39;installazione TarPM predefinita, l&#39;eliminazione delle cartelle comporta anche la rimozione dei dati.

>[!NOTE]
>
>Adobe consiglia di eseguire il backup dell’archivio prima di eliminare AEM. Se si elimina l&#39;intero &lt;cq-installation-directory>, verrà eliminato anche l&#39;archivio. Per conservare i dati del repository prima dell&#39;eliminazione, spostare o copiare la cartella &lt;cq-installation-directory>/crx-quickstart/repository altrove prima di eliminare le altre cartelle.

Se l’installazione di AEM utilizza un archivio esterno, ad esempio un server di database, la rimozione della cartella non rimuove automaticamente i dati, ma rimuove la configurazione di archiviazione, rendendo difficile il ripristino del contenuto JCR.
