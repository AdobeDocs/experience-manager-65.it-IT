---
title: Risoluzione dei problemi
seo-title: Risoluzione dei problemi
description: In questo articolo vengono trattati alcuni dei problemi di installazione che potrebbero verificarsi AEM.
seo-description: In questo articolo vengono trattati alcuni dei problemi di installazione che potrebbero verificarsi AEM.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---


# Risoluzione dei problemi{#troubleshooting}

Questa sezione contiene informazioni dettagliate sui registri disponibili per la risoluzione dei problemi e include anche informazioni su alcuni dei problemi che potrebbero verificarsi AEM.

## Risoluzione dei problemi relativi alle prestazioni dell&#39;autore {#troubleshoot-author-performance}

L’analisi di prestazioni lente sull’istanza Authoring può diventare piuttosto complessa. Come primo passo è necessario determinare su quale livello dello stack tecnologico le prestazioni diminuiscono.

La seguente struttura decisionale fornisce indicazioni per ridurre il collo di bottiglia.

![chlimage_1-75](assets/chlimage_1-75.png)

## Ottimizzazione di base {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configurazione dei file di registro e dei registri di controllo {#configuring-log-files-and-audit-logs}

AEM registra i registri dettagliati che potresti voler configurare per risolvere eventuali problemi di installazione. Per ulteriori informazioni, vedere la sezione [Uso dei record di controllo e dei file](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) di registro.

## Utilizzo dell’opzione Verbose {#using-the-verbose-option}

Quando si avvia AEM WCM, è possibile aggiungere l&#39;opzione -v (verbose) alla riga di comando come in: java -jar cq-wcm-quickstart-&lt;versione>.jar -v.

L&#39;opzione dettagliata visualizza parte dell&#39;output del registro Quickstart nella console, in modo che possa essere utilizzata per la risoluzione dei problemi.

## Problemi comuni di installazione {#common-installation-issues}

La sezione seguente descrive alcuni problemi di installazione e le relative soluzioni.

### Se si fa doppio clic sul file JAR non si verifica alcun effetto o si apre il file JAR con un altro programma (ad esempio, archive manager) {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

In genere indica un problema con la configurazione dell&#39;ambiente desktop del sistema operativo per l&#39;apertura di file con estensione .jar. Potrebbe inoltre indicare che non è installato Java o che si sta utilizzando una versione non supportata di Java.

Poiché i file JAR utilizzano il formato ZIP onnipresente, alcuni dei programmi di archiviazione possono configurare automaticamente il desktop per aprire i file JAR come file di archivio.

Per risolvere i problemi, effettuate le seguenti operazioni:

* Verificate che sia installata almeno la versione 1.6 di Java.
* Provate a utilizzare il menu di scelta rapida (in genere fate clic con il pulsante destro del mouse) AEM WCM Quickstart e selezionate &quot;Apri con....&quot;
* Verificate se Java o Sun Java è elencato e provate a eseguire AEM WCM con esso. Se avete installato più versioni Java, selezionate quella supportata.

   Se avete successo con questo passaggio, e i sistemi operativi offrono un&#39;opzione per utilizzare sempre il programma selezionato per eseguire i file .jar, selezionatelo. Il doppio clic dovrebbe funzionare da ora in poi.

* A volte la reinstallazione della versione Java supportata consente di ripristinare l&#39;associazione corretta.
* È sempre possibile eseguire CRX utilizzando la riga di comando o gli script start/stop come descritto in precedenza in questo documento.

### La mia applicazione in esecuzione su CRX genera errori di memoria insufficiente {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Vedere anche [Analisi dei problemi](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)di memoria.


Il CRX stesso ha un&#39;ingombro di memoria molto basso. Se l&#39;applicazione in esecuzione in CRX ha requisiti di memoria maggiori o richiede operazioni con molta memoria (ad esempio, transazioni di grandi dimensioni), l&#39;istanza JVM in cui è in esecuzione CRX deve essere avviata con le impostazioni di memoria appropriate.

Utilizzare le opzioni dei comandi Java per definire le impostazioni di memoria della JVM (ad esempio, java -Xmx512m -jar crx&amp;ast;.jar per impostare l&#39;altezza su 512 MB).

Specificare l&#39;opzione di impostazione della memoria quando si avvia AEM WCM dalla riga di comando. È inoltre possibile modificare gli script di avvio/arresto di WCM AEM o gli script personalizzati per la gestione AEM avvio di WCM per definire le impostazioni di memoria richieste.

Se avete già definito la dimensione dell’heapsize a 512 MB, potete analizzare ulteriormente il problema della memoria creando un’immagine di dump dell’heap:

Per creare automaticamente un dump dell&#39;heap in caso di esaurimento della memoria, utilizzare il comando seguente:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

Questo genera un file di dump dell&#39;heap (**java_...hprof**) ogni volta che il processo non dispone di memoria sufficiente. Il processo può continuare a essere eseguito dopo la generazione del dump dell&#39;heap. Solitamente, un file di dump heap è sufficiente per analizzare il problema.

### La schermata di benvenuto di AEM non viene visualizzata nel browser quando si fa doppio clic su AEM Quickstart {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

In alcune situazioni, le schermate di benvenuto AEM WCM non vengono visualizzate automaticamente anche se l&#39;archivio stesso è in esecuzione correttamente. Ciò può dipendere dalla configurazione del sistema operativo, dalla configurazione del browser o da fattori simili.

Il sintomo comune è che la finestra AEM WCM Quickstart visualizza &quot;AEM WCM start up, in attesa dell&#39;avvio del server....&quot; Se il messaggio viene visualizzato per un periodo di tempo relativamente lungo, immettete l’URL WCM AEM nella finestra del browser manualmente, utilizzando la porta predefinita 4502 oppure la porta su cui è in esecuzione l’istanza: http://localhost:4502/.

Inoltre, i registri potrebbero rivelare il motivo per cui il browser non si avvia.

A volte, la finestra AEM WCM Quickstart contiene il messaggio &quot;AEM WCM in esecuzione su http://localhost:port/&quot; e il browser non si avvia automaticamente. In questo caso, fate clic sull’URL nella AEM finestra WCM Quickstart (si tratta di un collegamento ipertestuale) oppure immettete manualmente l’URL nel browser.

Se tutto il resto non riesce, controllare i registri per scoprire cosa è successo.

## Risoluzione dei problemi relativi alle installazioni con un server applicazioni {#troubleshooting-installations-with-an-application-server}

### Pagina non trovata restituita quando si richiede una pagina geometrixx-outdoor {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**Applicabile a WebLogic 10.3.5 e JBoss 5.1**

Quando una richiesta a pagina geometrixx-outdoors/en restituisce un 404 (Page Not Folio), potete verificare di aver impostato la proprietà sling aggiuntiva nel file sling.properties necessario per questi Application Server specifici.

Consultate i passaggi *Implementazione AEM applicazione* Web per i dettagli.

### La dimensione dell&#39;intestazione della risposta può essere maggiore di 4 Kb {#response-header-size-can-be-greater-than-kb}

502 errori possono indicare che il server Web non è in grado di gestire le dimensioni dell&#39;intestazione AEM risposta HTTP. AEM generare intestazioni di risposta HTTP che includono cookie di dimensione maggiore di 4Kb. Accertatevi che il contenitore del servlet sia configurato in modo che la dimensione massima dell’intestazione della risposta possa superare i 4 kb.

Ad esempio, per Tomcat 7.0, l’attributo maxHttpHeaderSize del connettore [](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) HTTP controlla le limitazioni delle dimensioni dell’intestazione.

## Uninstalling Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Poiché AEM installato in una singola directory, non è necessario installare un&#39;utilità di disinstallazione. La disinstallazione può essere semplice come l&#39;eliminazione dell&#39;intera directory di installazione, anche se la modalità di disinstallazione AEM dipende da ciò che si desidera ottenere e da quale archivio permanente si utilizza.

Se la memorizzazione persistente è incorporata nella directory di installazione, ad esempio, nell&#39;installazione predefinita di TarPM, l&#39;eliminazione di cartelle rimuove anche i dati.

>[!NOTE]
>
> Adobe consiglia vivamente di eseguire il backup del repository prima di eliminare AEM. Se si elimina l&#39;intero &lt;cq-install-directory>, si elimina il repository. Per conservare i dati del repository prima di eliminare, spostare o copiare la cartella &lt;cq-install-directory>/crx-quickstart/repository altrove prima di eliminare le altre cartelle.

Se l&#39;installazione di AEM utilizza un archivio esterno, ad esempio un server di database, la rimozione della cartella non rimuove automaticamente i dati, ma rimuove la configurazione di storage, il che rende difficile il ripristino del contenuto JCR.

### I file JSP non sono compilati su JBoss {#jsp-files-are-not-compiled-on-jboss}

Se installate o aggiornate i file JSP in  Experience Manager su JBoss e i servlet corrispondenti non vengono compilati, accertatevi che il compilatore JBoss JSP sia configurato correttamente. Per informazioni, consultate l&#39;articolo sui[problemi di compilazione JSP in JBoss](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) .
