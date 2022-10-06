---
title: Miglioramento delle prestazioni del server applicazioni
seo-title: Enhancing application server performance
description: Questo documento descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server dell’applicazione AEM forms.
seo-description: This document describes optional settings that you can configure to improve the performance of your AEM forms application server.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---

# Miglioramento delle prestazioni del server applicazioni{#enhancing-application-server-performance}

Questo contenuto descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server dell’applicazione AEM forms.

## Configurazione delle origini dati del server applicazioni {#configuring-application-server-data-sources}

AEM forms utilizza l’archivio moduli AEM come origine dati. L’archivio dei moduli di AEM memorizza le risorse delle applicazioni e, in fase di esecuzione, i servizi possono recuperare le risorse dall’archivio come parte del completamento di un processo aziendale automatizzato.

L’accesso all’origine dati può essere significativo, a seconda del numero di moduli AEM in esecuzione e del numero di utenti simultanei che accedono all’applicazione. L&#39;accesso all&#39;origine dati può essere ottimizzato utilizzando il connection pooling. *Pooling di connessione* è una tecnica utilizzata per evitare il sovraccarico di creazione di nuove connessioni al database ogni volta che un&#39;applicazione o un oggetto server richiede l&#39;accesso al database. Il pool di connessioni viene generalmente utilizzato nelle applicazioni basate su Web e aziendali e viene in genere gestito da un server applicativo, ma non solo.

È importante configurare correttamente i parametri del pool di connessioni in modo da non esaurire mai le connessioni, il che può causare il deterioramento delle prestazioni dell&#39;applicazione.

Per configurare correttamente le impostazioni del pool di connessioni, è importante che l&#39;amministratore dell&#39;application server monitori il pool di connessioni nelle ore di punta della giornata. Il monitoraggio assicura che siano sempre disponibili connessioni sufficienti per applicazioni e utenti. La maggior parte dei server applicazioni include strumenti di monitoraggio.

Puoi monitorare diverse statistiche per ogni istanza di origine dati JDBC nel tuo dominio utilizzando la Console di amministrazione del server WebLogic. Per ulteriori informazioni, consulta la documentazione di WebLogic .

Quando l&#39;amministratore dell&#39;application server determina le impostazioni corrette del pool di connessioni, deve comunicare tali informazioni all&#39;amministratore del database. L&#39;amministratore del database necessita di queste informazioni perché il numero di connessioni al database corrisponde al numero di connessioni nel pool di connessioni per l&#39;origine dati. Quindi, completa i passaggi descritti di seguito per configurare le impostazioni del pool di connessioni per il server applicazioni e il tipo di origine dati.

### Configura le impostazioni del pool di connessioni per WebLogic per Oracle e MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. In Struttura del dominio, fai clic su Servizi > JDBC > Origini dati e, nel riquadro a destra, fai clic su IDP_DS.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Pool di connessioni e immetti un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento della capacità
   * Dimensioni cache istruzioni

1. Fare clic su Salva e quindi su Attiva modifiche.
1. Riavvia il server gestito WebLogic.

### Configurare le impostazioni del pool di connessioni per WebLogic per SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. In Cambia centro fare clic su Blocca e modifica.
1. In Struttura del dominio, fare clic su Servizi > JDBC > Origini dati e, nel riquadro a destra, fare clic su EDC_DS.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Pool di connessioni e immetti un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento della capacità
   * Dimensioni cache istruzioni

1. Fare clic su Salva e quindi su Attiva modifiche.
1. Riavvia il server gestito WebLogic.

### Configurare le impostazioni del pool di connessioni per WebSphere per DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Nella struttura di navigazione, fai clic su Risorse > JDBC > Provider JDBC. Nel riquadro a destra, fare clic sull&#39;origine dati creata, sia sul provider driver DB2 Universal JDBC che sul LiveCycle - db2 - IDP_DS.
1. In Proprietà aggiuntive fare clic su Origini dati e quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive fare clic su Proprietà pool di connessioni e immettere un valore nella casella Connessioni massime e nella casella Connessioni minime.
1. Fare clic su OK o Applica, quindi fare clic su Salva direttamente in configurazione principale.

### Configura le impostazioni del pool di connessioni per WebSphere, ad Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Nella struttura di navigazione, fai clic su Risorse > JDBC > Provider JDBC. Nel riquadro a destra, fare clic sull&#39;origine dati Oracle JDBC Driver creata.
1. In Proprietà aggiuntive fare clic su Origini dati e quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive fare clic su Proprietà pool di connessioni e immettere un valore nella casella Connessioni massime e nella casella Connessioni minime.
1. Fare clic su OK o Applica, quindi fare clic su Salva direttamente in configurazione principale.

### Configurare le impostazioni del pool di connessioni per WebSphere per SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Nella struttura di navigazione, fare clic su Risorse > JDBC > Provider JDBC e, nel riquadro a destra, fare clic sull&#39;origine dati del driver JDBC definito dall&#39;utente creata.
1. In Proprietà aggiuntive fare clic su Origini dati e quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive fare clic su Proprietà pool di connessioni e immettere un valore nella casella Connessioni massime e nella casella Connessioni minime:
1. Fare clic su OK o Applica, quindi fare clic su Salva direttamente in configurazione principale.

## Ottimizzazione dei documenti in linea e impatto sulla memoria JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Se si elaborano in genere documenti di dimensioni relativamente ridotte, è possibile migliorare le prestazioni associate alla velocità di trasferimento dei documenti e allo spazio di archiviazione. A tal fine, implementa le seguenti configurazioni di prodotto AEM forms:

* Aumentare la dimensione massima predefinita del documento in linea per i moduli AEM in modo che sia più grande della dimensione della maggior parte dei documenti.
* Per l&#39;elaborazione di file di grandi dimensioni, specificare le directory di archiviazione che si trovano su un sistema a disco ad alta velocità o su un disco RAM.

Le dimensioni massime in linea e le directory di archiviazione (la directory dei file temporanei dei moduli AEM e la directory GDS) sono configurate nella console di amministrazione.

### Dimensione del documento e dimensione massima in linea {#document-size-and-maximum-inline-size}

Quando un documento inviato per l’elaborazione da AEM moduli è inferiore o uguale alla dimensione massima predefinita del documento in linea, il documento viene memorizzato sul server in linea e il documento viene serializzato come oggetto Documento di Adobe. L’archiviazione dei documenti in linea può comportare vantaggi significativi in termini di prestazioni. Tuttavia, se si utilizza il flusso di lavoro dei moduli, il contenuto può anche essere memorizzato nel database a scopo di tracciamento. Pertanto, l’aumento della dimensione massima in linea può influenzare la dimensione del database.

Nel file system locale viene memorizzato un documento di dimensioni superiori alle dimensioni massime in linea. L&#39;oggetto Document di Adobe che viene trasferito da e verso il server è solo un puntatore a tale file.

Quando il contenuto del documento è in linea (ovvero inferiore alla dimensione in linea massima), il contenuto viene memorizzato nel database come parte del payload di serializzazione del documento. Pertanto, aumentare la dimensione massima in linea può influenzare la dimensione del database.

**Modificare le dimensioni massime in linea**

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistema di base > Configurazioni.
1. Immettere un valore nella casella Dimensione in linea massima documento predefinita e fare clic su OK.

   >[!NOTE]
   >
   >Il valore della proprietà Dimensione in linea massima del documento deve essere identico per AEM Forms nell’ambiente JEE e per il bundle AEM Forms on OSGi incluso in AEM Forms nell’ambiente JEE. Questo passaggio ha aggiornato il valore solo per AEM Forms nell’ambiente JEE e non per AEM Forms nel bundle OSGi incluso AEM Forms nell’ambiente JEE.

1. Riavvia l&#39;application server con la seguente proprietà di sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La proprietà di sistema di cui sopra sostituisce il valore della proprietà Dimensione in linea massima documento impostata per AEM Forms nell’ambiente JEE e il bundle AEM Forms on OSGi incluso AEM Forms nell’ambiente JEE.

>[!NOTE]
>
>La dimensione massima predefinita in linea è di 65536 byte.

### Dimensione massima heap della JVM {#jvm-maximum-heap-size}

Un aumento della dimensione massima in linea richiede più memoria per memorizzare i documenti serializzati. Pertanto, in genere richiede anche un aumento della dimensione massima dell&#39;heap JVM.

Un sistema sovraccarico che sta elaborando molti documenti può rapidamente saturare la memoria heap JVM. Per evitare un OutOfMemoryError, aumenta la dimensione massima dell&#39;heap JVM di una quantità corrispondente alla dimensione dei documenti in linea moltiplicata per il numero di documenti normalmente eseguiti in un dato momento.

Aumento della dimensione massima dell&#39;heap JVM = (dimensione dei documenti in linea) x (numero medio di documenti elaborati).

**Calcolo della dimensione massima dell&#39;heap della JVM**

In questo esempio, l&#39;heap massimo JVM corrente è impostato a 512 MB e la dimensione massima in linea è 64 KB. Il server deve essere configurato per lo scenario in cui vengono eseguiti 10 processi contemporaneamente e ogni processo ha 9 file di input e 1 file di risultato (un totale di 10 file per processo e 100 file elaborati simultaneamente). Tutte le dimensioni dei file sono inferiori a 512 KB.

Per memorizzare tutti i file in linea, imposta la dimensione massima in linea su almeno 512 KB.

L&#39;aumento richiesto nella dimensione massima dell&#39;heap JVM viene calcolato utilizzando la seguente equazione:

(512 KB) x (100) = 51200 KB, o 50 MB

La dimensione massima dell&#39;heap JVM deve essere aumentata di 50 MB per un totale di 562 MB.

**Considerazione della frammentazione dell’heap**

L&#39;impostazione delle dimensioni dei documenti in linea su valori di grandi dimensioni aumenta il rischio di un OutOfMemoryError sui sistemi che sono inclini a heap frammentazione. Per memorizzare un documento in linea, la memoria heap JVM deve avere spazio contiguo sufficiente. Alcuni sistemi operativi, JVM e algoritmi di raccolta degli oggetti inattivi sono soggetti a un heap della frammentazione. La frammentazione riduce la quantità di spazio heap contiguo e può portare a un OutOfMemoryError anche quando esiste spazio libero totale sufficiente.

Ad esempio, le operazioni precedenti sul server applicazioni hanno lasciato l&#39;heap JVM in uno stato frammentato e il Garbage Collector non può compattare il heap in modo sufficiente per recuperare grandi blocchi di spazio libero. È possibile che si verifichi un OutOfMemoryError anche se la dimensione massima dell&#39;heap JVM è stata regolata per un aumento della dimensione massima in linea.

Per tenere conto della frammentazione dell’heap, la dimensione del documento in linea non deve essere superiore allo 0,1% della dimensione totale dell’heap. Ad esempio, una dimensione massima dell&#39;heap JVM di 512 MB può supportare una dimensione massima in linea di 512 MB x 0.001 = 0,512 MB o 512 KB.

## Miglioramenti a WebSphere Application Server {#websphere-application-server-enhancements}

Questa sezione descrive le impostazioni specifiche di un ambiente WebSphere Application Server.

### Aumento della memoria massima assegnata alla JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Se si esegue Configuration Manager o si tenta di generare codice di distribuzione JavaBeans (EJB) Enterprise utilizzando l&#39;utilità della riga di comando *ejbdeploy* e si verifica un errore OutOfMemory, aumenta la quantità di memoria allocata alla JVM.

1. Modifica lo script ejbdeploy nel *[root appserver]*/deploy tool/itp/ directory:

   * (Windows) `ejbdeploy.bat`
   * (Linux e UNIX) `ejbdeploy.sh`

1. Trova il `-Xmx256M` e modificarlo in un valore più alto, ad esempio `-Xmx1024M`.
1. Salva il file.
1. Esegui il `ejbdeploy` comando o ridistribuzione tramite Configuration Manager.

## Miglioramento delle prestazioni di Windows Server 2003 con LDAP {#improving-windows-server-2003-performance-with-ldap}

Questo contenuto descrive le impostazioni specifiche di un ambiente del sistema operativo Microsoft Windows Server 2003.

L&#39;utilizzo del connection pooling sulla connessione di ricerca può ridurre il numero di porte necessarie fino al 50%. Questo perché la connessione utilizza sempre le stesse credenziali per un determinato dominio e il contesto e gli oggetti correlati vengono chiusi in modo esplicito.

### Configurare Windows Server per il pool di connessioni {#configure-your-windows-server-for-connection-pooling}

1. Fare clic su Start > Esegui per avviare l&#39;editor del Registro di sistema e, nella casella Apri, digitare `regedit` e fare clic su OK.
1. Vai alla chiave del Registro di sistema `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. Nel riquadro a destra dell&#39;editor del Registro di sistema, trova il nome del valore TcpTimedWaitDelay . Se il nome non viene visualizzato, selezionare Modifica > Nuovo > Valore DWORD dalla barra dei menu per aggiungere il nome.
1. Nella casella Nome digitare `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Se non vedi un cursore lampeggiante e `New Value #` nel riquadro fare clic con il pulsante destro del mouse nel pannello di destra, selezionare Rinomina e digitare nella casella Nome `TcpTimedWaitDelay`*.*

1. Ripetere il passaggio 4 per i nomi dei valori MaxUserPort, MaxHashTableSize e MaxFreeTcbs.
1. Fai doppio clic all’interno del riquadro di destra per impostare il valore TcpTimedWaitDelay . In Base, selezionare Decimale e, nella casella Valore, digitare `30`.
1. Fare doppio clic all&#39;interno del riquadro di destra per impostare il valore MaxUserPort. In Base, selezionare Decimale e, nella casella Valore, digitare `65534`.
1. Fare doppio clic all&#39;interno del riquadro di destra per impostare il valore MaxHashTableSize. In Base, selezionare Decimale e, nella casella Valore, digitare `65536`.
1. Fare doppio clic all&#39;interno del riquadro di destra per impostare il valore MaxFreeTcbs. In Base, selezionare Decimale e, nella casella Valore, digitare `16000`.

>[!NOTE]
>
>Possono verificarsi gravi problemi se si modifica il Registro di sistema in modo errato utilizzando l&#39;Editor del Registro di sistema o utilizzando un altro metodo. Questi problemi possono richiedere la reinstallazione del sistema operativo. Modificare il registro a proprio rischio.
