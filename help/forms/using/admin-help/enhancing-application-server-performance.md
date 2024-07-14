---
title: Miglioramento delle prestazioni del server applicazioni
description: Questo documento descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server applicazioni AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# Miglioramento delle prestazioni del server applicazioni{#enhancing-application-server-performance}

Questo contenuto descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server applicazioni AEM Forms.

## Configurazione delle origini dati del server applicazioni {#configuring-application-server-data-sources}

I moduli AEM utilizzano l’archivio dei moduli AEM come origine di dati. Il repository dei moduli AEM memorizza le risorse delle applicazioni e, in fase di esecuzione, i servizi possono recuperare le risorse dal repository come parte del completamento di un processo aziendale automatizzato.

L’accesso all’origine dati può essere significativo, a seconda del numero di moduli AEM in esecuzione e del numero di utenti simultanei che accedono all’applicazione. L’accesso all’origine dati può essere ottimizzato utilizzando il connection pooling. *Il connection pooling* è una tecnica utilizzata per evitare il sovraccarico di creare nuove connessioni al database ogni volta che un oggetto server o applicativo richiede l&#39;accesso al database. Il connection pooling viene in genere utilizzato nelle applicazioni aziendali e basate su Web e viene in genere gestito da un server applicazioni, ma non solo.

È importante configurare correttamente i parametri del pool di connessioni in modo da non esaurire mai le connessioni, il che può causare un deterioramento delle prestazioni dell&#39;applicazione.

Per configurare correttamente le impostazioni del connection pool, è importante che l&#39;amministratore del server applicazioni monitori il connection pool durante le ore di punta della giornata. Il monitoraggio garantisce che siano sempre disponibili connessioni sufficienti per applicazioni e utenti. La maggior parte dei server delle applicazioni include strumenti di monitoraggio.

È possibile monitorare varie statistiche per ogni istanza dell&#39;origine dati JDBC nel dominio utilizzando la console di amministrazione del server WebLogic. Per informazioni dettagliate, consulta la documentazione di WebLogic.

Quando l&#39;amministratore del server applicazioni determina le impostazioni corrette del connection pool, l&#39;utente deve comunicare tali informazioni all&#39;amministratore del database. Queste informazioni sono necessarie all&#39;amministratore del database perché il numero di connessioni al database è uguale al numero di connessioni nel pool di connessioni per l&#39;origine dati. Completare quindi i passaggi per configurare le impostazioni del connection pool per il server applicazioni e il tipo di origine dati come descritto di seguito.

### Configurare le impostazioni del pool di connessioni per WebLogic per Oracle e MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. In Struttura dominio fare clic su Servizi > JDBC > Origini dati e nel riquadro destro fare clic su IDP_DS.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Pool di connessioni e immetti un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento di capacità
   * Statement Cache Size

1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

### Configurare le impostazioni del pool di connessioni per WebLogic per SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. In Cambia centro fare clic su Blocca e modifica.
1. In Struttura dominio fare clic su Servizi > JDBC > Origini dati e nel riquadro destro fare clic su EDC_DS.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Pool di connessioni e immetti un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento di capacità
   * Statement Cache Size

1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

### Configurare le impostazioni del connection pool per WebSphere per DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Nella struttura di navigazione, fai clic su Risorse > JDBC > Provider JDBC. Nel riquadro di destra fare clic sull&#39;origine dati creata, ovvero Provider driver DB2 Universal JDBC oppure LiveCycle - db2 - IDP_DS.
1. In Proprietà aggiuntive fare clic su Origini dati e quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fare clic su Proprietà connection pool e immettere un valore nelle caselle Numero massimo connessioni e Numero minimo connessioni.
1. Fare clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.

### Configurare le impostazioni del connection pool per WebSphere, ad Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Nella struttura di navigazione, fai clic su Risorse > JDBC > Provider JDBC. Nel riquadro destro fare clic sull&#39;origine dati Oracle Driver JDBC creata.
1. In Proprietà aggiuntive fare clic su Origini dati e quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fare clic su Proprietà connection pool e immettere un valore nelle caselle Numero massimo connessioni e Numero minimo connessioni.
1. Fare clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.

### Configurare le impostazioni del pool di connessioni per WebSphere per SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Nella struttura di navigazione fare clic su Risorse > JDBC > Provider JDBC e nel riquadro destro fare clic sull&#39;origine dati Driver JDBC definita dall&#39;utente creata.
1. In Proprietà aggiuntive fare clic su Origini dati e quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fare clic su Proprietà connection pool e immettere un valore nelle caselle Numero massimo connessioni e Numero minimo connessioni:
1. Fare clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.

## Ottimizzazione dei documenti in linea e impatto sulla memoria JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Se in genere si elaborano documenti di dimensioni relativamente ridotte, è possibile migliorare le prestazioni associate alla velocità di trasferimento dei documenti e allo spazio di archiviazione. Per farlo, implementa le seguenti configurazioni di prodotto per i moduli AEM:

* Aumentare la dimensione in linea massima del documento predefinito per i moduli AEM in modo che sia maggiore della dimensione della maggior parte dei documenti.
* Per l&#39;elaborazione di file di grandi dimensioni, specificare le directory di archiviazione che si trovano su un sistema a disco ad alta velocità o su un disco RAM.

Le dimensioni massime in linea e le directory di archiviazione (l’AEM forma la directory dei file temporanei e la directory GDS) sono configurate nella console di amministrazione.

### Dimensione del documento e dimensione massima in linea {#document-size-and-maximum-inline-size}

Quando un documento inviato per l&#39;elaborazione dai moduli AEM è inferiore o uguale alla dimensione in linea massima del documento predefinita, il documento viene memorizzato sul server in linea e serializzato come oggetto documento di Adobe. L&#39;archiviazione dei documenti in linea può comportare notevoli vantaggi in termini di prestazioni. Tuttavia, se utilizzi un flusso di lavoro per moduli, il contenuto può anche essere memorizzato nel database a scopo di tracciamento. Pertanto, l’aumento della dimensione massima in linea può influire sulle dimensioni del database.

Nel file system locale viene memorizzato un documento con dimensioni superiori alla dimensione massima in linea. L&#39;oggetto Adobe Document trasferito da e verso il server è solo un puntatore a tale file.

Quando il contenuto del documento è allineato, ovvero inferiore alla dimensione massima in linea, viene memorizzato nel database come parte del payload di serializzazione del documento. Pertanto, l’aumento della dimensione massima in linea può influenzare la dimensione del database.

**Modifica la dimensione massima in linea**

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
1. Immettere un valore nella casella Dimensione in linea massima documento predefinita e fare clic su OK.

   >[!NOTE]
   >
   >Il valore della proprietà Dimensione massima in linea del documento deve essere identico per AEM Forms nell’ambiente JEE e per AEM Forms nel bundle OSGi incluso AEM Forms nell’ambiente JEE. Questa procedura ha aggiornato il valore solo per l’ambiente AEM Forms su JEE e non per il bundle AEM Forms su OSGi, includendo AEM Forms sull’ambiente JEE.

1. Riavviare il server applicazioni con la seguente proprietà di sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La suddetta proprietà di sistema sostituisce il valore della proprietà Dimensione massima in linea del documento impostata per AEM Forms nell’ambiente JEE e AEM Forms nel bundle OSGi incluso AEM Forms nell’ambiente JEE.

>[!NOTE]
>
>La dimensione massima predefinita in linea è di 65536 byte.

### Dimensione heap massima JVM {#jvm-maximum-heap-size}

Un aumento della dimensione massima in linea richiede una maggiore quantità di memoria per l&#39;archiviazione dei documenti serializzati. Pertanto, in genere richiede anche un aumento della dimensione heap massima JVM.

Un sistema con un carico elevato che elabora molti documenti può saturare rapidamente la memoria heap JVM. Per evitare un errore OutOfMemoryError, aumenta la dimensione heap massima JVM di un importo corrispondente alla dimensione dei documenti in linea moltiplicata per il numero di documenti che vengono in genere eseguiti in un determinato momento.

Aumento dimensione heap massima JVM = (dimensione documenti in linea) x (numero medio di documenti elaborati).

**Calcolo della dimensione heap massima JVM**

In questo esempio, l’heap massimo JVM corrente è impostato su 512 MB e la dimensione massima in linea è 64 KB. Il server deve essere configurato per lo scenario in cui vengono eseguiti contemporaneamente 10 processi e ogni processo ha 9 file di input e 1 file di risultati (un totale di 10 file per processo e 100 file elaborati simultaneamente). Tutti i file hanno dimensioni inferiori a 512 KB.

Per memorizzare tutti i file in linea, impostate la dimensione massima in linea di almeno 512 KB.

L’aumento richiesto della dimensione heap massima JVM viene calcolato utilizzando la seguente equazione:

(512 KB) x (100) = 51200 KB o 50 MB

La dimensione heap massima JVM deve essere aumentata di 50 MB per un totale di 562 MB.

**Considerazione della frammentazione heap**

Se si impostano su valori elevati le dimensioni dei documenti in linea, si rischia di generare un errore OutOfMemoryError nei sistemi soggetti a frammentazione heap. Per memorizzare un documento in linea, la memoria heap JVM deve disporre di spazio contiguo sufficiente. Alcuni sistemi operativi, JVM e algoritmi di Garbage Collection sono soggetti a frammentazione heap. La frammentazione riduce la quantità di spazio heap contiguo e può causare un errore OutOfMemoryError anche in presenza di spazio libero totale sufficiente.

Ad esempio, le operazioni precedenti sul server applicazioni hanno lasciato l’heap JVM in uno stato frammentato e il Garbage Collector non è in grado di compattare l’heap in modo sufficiente per recuperare grandi blocchi di spazio libero. È possibile che si verifichi un errore OutOfMemoryError anche se la dimensione heap massima JVM è stata regolata per un aumento della dimensione inline massima.

Per tenere conto della frammentazione heap, la dimensione del documento in linea non deve essere superiore allo 0,1% della dimensione heap totale. Ad esempio, una dimensione heap massima JVM di 512 MB può supportare una dimensione inline massima di 512 MB x 0,001 = 0,512 MB o 512 KB.

## Miglioramenti dell&#39;Application Server WebSphere {#websphere-application-server-enhancements}

Questa sezione descrive le impostazioni specifiche di un ambiente Application Server WebSphere.

### Aumento della memoria massima allocata a JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Se si esegue Configuration Manager o si tenta di generare codice di distribuzione Enterprise JavaBeans (EJB) utilizzando l&#39;utilità della riga di comando *ejbdeploy* e si verifica un errore OutOfMemory, aumentare la quantità di memoria allocata alla JVM.

1. Modificare lo script ejbdeploy nella directory *[appserver root]*/deploytool/itp/:

   * (Windows) `ejbdeploy.bat`
   * (Linux e UNIX) `ejbdeploy.sh`

1. Trovare il parametro `-Xmx256M` e modificarlo in un valore superiore, ad esempio `-Xmx1024M`.
1. Salva il file.
1. Eseguire il comando `ejbdeploy` o ridistribuirlo utilizzando Configuration Manager.

## Miglioramento delle prestazioni di Windows Server 2003 con LDAP {#improving-windows-server-2003-performance-with-ldap}

Questo contenuto descrive le impostazioni specifiche di un ambiente del sistema operativo Microsoft Windows Server 2003.

L’utilizzo del connection pooling sulla connessione di ricerca può ridurre il numero di porte necessarie fino al 50%. Questo perché la connessione utilizza sempre le stesse credenziali per un determinato dominio e il contesto e gli oggetti correlati vengono chiusi in modo esplicito.

### Configurare Windows Server per il connection pooling {#configure-your-windows-server-for-connection-pooling}

1. Fare clic su Start > Esegui per avviare l&#39;editor del Registro di sistema e nella casella Apri digitare `regedit` e fare clic su OK.
1. Vai alla chiave del Registro di sistema `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. Nel riquadro di destra dell&#39;editor del Registro di sistema trovare il nome del valore TcpTimedWaitDelay. Se il nome non viene visualizzato, selezionate Modifica > Nuovo > Valore DWORD dalla barra dei menu per aggiungere il nome.
1. Nella casella Nome digitare `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Se nella casella non è presente un cursore lampeggiante e `New Value #`, fare clic con il pulsante destro del mouse all&#39;interno del pannello di destra, selezionare Rinomina e nella casella Nome digitare `TcpTimedWaitDelay`*.*

1. Ripetere il passaggio 4 per i nomi di valore MaxUserPort, MaxHashTableSize e MaxFreeTcbs.
1. Fare doppio clic all&#39;interno del riquadro destro per impostare il valore TcpTimedWaitDelay. In Base selezionare Decimale e nella casella Valore digitare `30`.
1. Fare doppio clic all&#39;interno del riquadro destro per impostare il valore MaxUserPort. In Base selezionare Decimale e nella casella Valore digitare `65534`.
1. Fare doppio clic all&#39;interno del riquadro destro per impostare il valore MaxHashTableSize. In Base selezionare Decimale e nella casella Valore digitare `65536`.
1. Fare doppio clic all&#39;interno del riquadro destro per impostare il valore MaxFreeTcbs. In Base selezionare Decimale e nella casella Valore digitare `16000`.

>[!NOTE]
>
>È possibile che si verifichino problemi gravi se si modifica il Registro di sistema in modo errato utilizzando l&#39;Editor del Registro di sistema o un altro metodo. Per questi problemi potrebbe essere necessario reinstallare il sistema operativo. Modificare il Registro di sistema a proprio rischio e pericolo.
