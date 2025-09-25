---
title: Miglioramento delle prestazioni del server applicazioni
description: In questo documento vengono descritte le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server applicazioni AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1882'
ht-degree: 100%

---

# Miglioramento delle prestazioni del server applicazioni{#enhancing-application-server-performance}

Questo contenuto descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server applicazioni AEM Forms.

## Configurazione delle origini dati del server applicazioni {#configuring-application-server-data-sources}

AEM Forms utilizza l’archivio AEM Forms come origine dati. L’archivio di AEM Forms archivia le risorse delle applicazioni e, in fase di esecuzione, i servizi possono recuperare le risorse dall’archivio come parte del completamento di un processo aziendale automatizzato.

L’accesso all’origine dati può essere significativo, a seconda del numero di moduli di AEM Forms in esecuzione e del numero di utenti simultanei che accedono all’applicazione. L’accesso all’origine dati può essere ottimizzato utilizzando il pooling di connessioni. Il *pooling di connessioni* è una tecnica utilizzata per evitare il sovraccarico di creare nuove connessioni al database ogni volta che un’applicazione o un oggetto server richiede l’accesso al database. Il pool di connessioni viene in genere utilizzato nelle applicazioni aziendali e basate su Web e gestito da un server applicazioni, ma non esclusivamente.

È importante configurare correttamente i parametri del pool di connessioni in modo da non esaurire mai le connessioni, il che può causare un deterioramento delle prestazioni dell’applicazione.

Per configurare correttamente le impostazioni del pool di connessioni, è importante che l’amministratore del server applicazioni monitori il pool di connessioni durante le ore di punta della giornata. Il monitoraggio garantisce che siano sempre disponibili connessioni sufficienti per applicazioni e utenti. La maggior parte dei server applicazioni include strumenti di monitoraggio.

È possibile monitorare varie statistiche per ogni istanza dell’origine dati JDBC nel dominio utilizzando la console di amministrazione del server WebLogic. Per maggiori dettagli, consulta la documentazione di WebLogic.

Quando l’amministratore del server applicazioni determina le impostazioni corrette del pool di connessioni, l’utente deve comunicare tali informazioni all’amministratore del database. Queste informazioni sono necessarie all’amministratore del database perché il numero di connessioni al database è uguale al numero di connessioni nel pool di connessioni per l’origine dati. Completa quindi i passaggi per configurare le impostazioni del pool di connessioni per il server applicazioni e il tipo di origine dati come descritto di seguito.

### Configurare le impostazioni del pool di connessioni per WebLogic per Oracle e MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. In Struttura dominio, fai clic su Servizi > JDBC > Origini dati e nel riquadro destro fai clic su IDP_DS.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Pool di connessioni e immetti un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento di capacità
   * Dimensioni cache istruzioni

1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavvia il server gestito da WebLogic.

### Configurare le impostazioni del pool di connessioni per WebLogic per SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. In Cambia centro fai clic su Blocca e modifica.
1. In Struttura dominio fai clic su Servizi > JDBC > Origini dati e, nel riquadro destro, fai clic su EDC_DS.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Pool di connessioni e immetti un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento di capacità
   * Dimensioni cache istruzioni

1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavvia il server gestito da WebLogic.

### Configurare le impostazioni del pool di connessioni per WebSphere per DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Nella struttura di navigazione, fai clic su Risorse > JDBC > Provider JDBC. Nel riquadro a destra, fai clic sull’origine dati creata, ovvero Provider driver JDBC universale DB2 o LiveCycle - db2 - IDP_DS.
1. In Proprietà aggiuntive, fai clic su Origini dati e quindi seleziona IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fai clic su Proprietà pool di connessioni e inserisci un valore nella casella Connessioni massime e Connessioni minime.
1. Fai clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.

### Configurare le impostazioni del pool di connessioni per WebSphere per Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Nella struttura di navigazione, fai clic su Risorse > JDBC > Provider JDBC. Nel riquadro destro, fai clic sull’origine dati Oracle JDBC Driver creata.
1. In Proprietà aggiuntive, fai clic su Origini dati e quindi seleziona IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fai clic su Proprietà pool di connessioni e inserisci un valore nella casella Connessioni massime e Connessioni minime.
1. Fai clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.

### Configurare le impostazioni del pool di connessioni per WebSphere per SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Nella struttura di navigazione, fai clic su Risorse > JDBC > Provider JDBC e nel riquadro destro, fai clic sull’origine dati Driver JDBC definita dall’utente creata.
1. In Proprietà aggiuntive, fai clic su Origini dati e quindi seleziona IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fai clic su Proprietà pool di connessioni e inserisci un valore nelle caselle Connessioni massime e Connessioni minime:
1. Fai clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.

## Ottimizzazione dei documenti in linea e impatto sulla memoria JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Se in genere vengono elaborati documenti di dimensioni relativamente ridotte, è possibile migliorare le prestazioni associate alla velocità di trasferimento dei documenti e allo spazio di archiviazione. A questo scopo, implementa le seguenti configurazioni di prodotto per AEM Forms:

* Aumenta la dimensione in linea di massima predefinita del documento per AEM Forms in modo che sia maggiore della dimensione della maggior parte dei documenti.
* Per l’elaborazione di file più grandi, specifica le directory di archiviazione che si trovano su un sistema a disco ad alta velocità o su un disco RAM.

Le dimensioni massime in linea e le directory di archiviazione (la directory dei file temporanei di AEM Forms e la directory GDS) sono configurate nella console di amministrazione.

### Dimensione del documento e dimensione massima in linea {#document-size-and-maximum-inline-size}

Quando un documento inviato per l’elaborazione da AEM Forms è inferiore o uguale alla dimensione in linea massima del documento predefinita, il documento viene archiviato sul server in linea e serializzato come oggetto documento di Adobe. L’archiviazione dei documenti in linea può comportare notevoli vantaggi in termini di prestazioni. Tuttavia, se utilizzi un flusso di lavoro per moduli, il contenuto può anche essere archiviato nel database a scopo di tracciamento. Pertanto, l’aumento della dimensione massima in linea può influire sulle dimensioni del database.

Nel file system locale viene archiviato un documento con dimensioni superiori alla dimensione massima in linea. L’oggetto documento Adobe trasferito da e verso il server è solo un puntatore a tale file.

Quando il contenuto del documento è in linea, ovvero inferiore alla dimensione massima in linea, viene archiviato nel database come parte del payload di serializzazione del documento. Pertanto, l’aumento della dimensione massima in linea può influenzare la dimensione del database.

**Modifica la dimensione massima in linea**

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
1. Inserisci un valore nella casella Dimensione in linea massima documento predefinita e fai clic su OK.

   >[!NOTE]
   >
   >Il valore della proprietà Dimensione massima in linea del documento deve essere identico per AEM Forms sull’ambiente JEE e per AEM Forms sul bundle OSGi incluso AEM Forms sull’ambiente JEE. Questa procedura ha aggiornato il valore solo per AEM Forms sull’ambiente JEE e non per AEM Forms sul bundle OSGi, includeso AEM Forms sull’ambiente JEE.

1. Riavvia il server applicazioni con la seguente proprietà di sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La suddetta proprietà di sistema sostituisce il valore della proprietà Dimensione massima in linea del documento impostata per AEM Forms sull’ambiente JEE e AEM Forms sul bundle OSGi incluso AEM Forms sull’ambiente JEE.

>[!NOTE]
>
>La dimensione massima predefinita in linea è di 65536 byte.

### Dimensione heap massima JVM {#jvm-maximum-heap-size}

Un aumento della dimensione massima in linea richiede una maggiore quantità di memoria per l’archiviazione dei documenti serializzati. Pertanto, in genere richiede anche un aumento della dimensione heap massima JVM.

Un sistema con un carico elevato che elabora molti documenti può saturare rapidamente la memoria heap JVM. Per evitare un errore OutOfMemoryError, aumenta la dimensione heap massima JVM di una quantità corrispondente alla dimensione dei documenti in linea moltiplicata per il numero di documenti che vengono in genere eseguiti in un determinato momento.

Aumento dimensione heap massima JVM = (dimensione documenti in linea) x (numero medio di documenti elaborati).

**Calcolo della dimensione heap massima JVM**

In questo esempio, l’heap massimo JVM corrente è impostato su 512 MB e la dimensione massima in linea è 64 KB. Il server deve essere configurato per lo scenario in cui vengono eseguiti contemporaneamente 10 processi e ogni processo ha 9 file di input e 1 file di risultati (un totale di 10 file per processo e 100 file elaborati simultaneamente). Tutti i file hanno dimensioni inferiori a 512 KB.

Per archiviare tutti i file in linea, imposta la dimensione massima in linea ad almeno 512 KB.

L’aumento richiesto della dimensione heap massima JVM viene calcolato utilizzando la seguente equazione:

(512 KB) x (100) = 51200 KB o 50 MB

La dimensione heap massima JVM deve essere aumentata di 50 MB per un totale di 562 MB.

**Considerare la frammentazione heap**

Impostando la dimensione dei documenti in linea su valori elevati aumenta il rischio di un OutOfMemoryError nei sistemi soggetti a frammentazione heap. Per archiviare un documento in linea, la memoria heap JVM deve disporre di spazio contiguo sufficiente. Alcuni sistemi operativi, JVM e algoritmi di raccolta oggetti inattivi sono soggetti a frammentazione heap. La frammentazione riduce la quantità di spazio heap contiguo e può causare un OutOfMemoryError anche in presenza di spazio libero totale sufficiente.

Ad esempio, le operazioni precedenti sul server applicazioni hanno lasciato l’heap JVM in uno stato frammentato e la raccolta di oggetti inattivi non è in grado di compattare l’heap in modo sufficiente per recuperare grandi blocchi di spazio libero. Può verificarsi un OutOfMemoryError anche se la dimensione heap massima JVM è stata regolata per un aumento della dimensione in linea massima.

Per tenere conto della frammentazione heap, la dimensione del documento in linea non deve essere superiore allo 0,1% della dimensione heap totale. Ad esempio, una dimensione heap massima JVM di 512 MB può supportare una dimensione in linea massima di 512 MB x 0,001 = 0,512 MB o 512 KB.

## Miglioramenti del Server applicazioni WebSphere {#websphere-application-server-enhancements}

Questa sezione descrive le impostazioni specifiche di un ambiente server applicazioni WebSphere.

### Aumento della memoria massima allocata a JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Se incontri un errore OutOfMemory durante l’esecuzione di Gestione configurazione o nel tentativo di generare codice di distribuzione Enterprise JavaBeans (EJB) utilizzando l’utilità della riga di comando *ejbdeploy*, aumenta la quantità di memoria allocata alla JVM.

1. Modifica lo script ejbdeploy nella directory *[appserver root]*/deploytool/itp/:

   * (Windows) `ejbdeploy.bat`
   * (Linux e UNIX) `ejbdeploy.sh`

1. Trova il parametro `-Xmx256M` e modificalo in un valore superiore, ad esempio `-Xmx1024M`.
1. Salva il file.
1. Esegui il comando `ejbdeploy` o ridistribuiscilo utilizzando Gestione configurazione.

## Migliorare le prestazioni di Windows Server 2003 con LDAP {#improving-windows-server-2003-performance-with-ldap}

Questo contenuto descrive le impostazioni specifiche di un ambiente del sistema operativo Microsoft Windows Server 2003.

L’utilizzo del pooling di connessioni sulla connessione di ricerca può ridurre il numero di porte necessarie fino al 50%. Questo perché la connessione utilizza sempre le stesse credenziali per un determinato dominio e il contesto e gli oggetti correlati vengono chiusi in modo esplicito.

### Configurare Windows Server per il pooling di connessioni {#configure-your-windows-server-for-connection-pooling}

1. Fai clic su Avvio > Esegui per avviare l’editor del Registro e nella casella Apri digita `regedit` e fai clic su OK.
1. Passa alla chiave del Registro `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. Nel riquadro di destra dell’editor del Registro trova il nome del valore TcpTimedWaitDelay. Se il nome non viene mostrato, seleziona Modifica > Nuovo > Valore DWORD dalla barra dei menu per aggiungere il nome.
1. Nella casella Nome, digita `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Se nella casella non vedi un cursore lampeggiante e `New Value #`, fai clic con il pulsante destro del mouse all’interno del pannello di destra, seleziona Rinomina e nella casella Nome digita `TcpTimedWaitDelay`*.*

1. Ripeti il passaggio 4 per i nomi di valore MaxUserPort, MaxHashTableSize e MaxFreeTcbs.
1. Fai doppio clic all’interno del riquadro destro per impostare il valore TcpTimedWaitDelay. In Base, seleziona Decimale e, nella casella Valore, digita `30`.
1. Fai doppio clic all’interno del riquadro destro per impostare il valore MaxUserPort. In Base, seleziona Decimale e, nella casella Valore, digita `65534`.
1. Fai doppio clic all’interno del riquadro destro per impostare il valore MaxHashTableSize. In Base, seleziona Decimale e, nella casella Valore, digita `65536`.
1. Fai doppio clic all’interno del riquadro destro per impostare il valore MaxFreeTcbs. In Base, seleziona Decimale e, nella casella Valore, digita `16000`.

>[!NOTE]
>
>È possibile che si verifichino problemi gravi modificando il registro in modo errato oppure utilizzando l’Editor del Registro o un altro metodo. Per questi problemi potrebbe essere necessario reinstallare il sistema operativo. Modifica il registro a tuo rischio e pericolo.
