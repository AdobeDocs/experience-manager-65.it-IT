---
title: Miglioramento delle prestazioni del server applicazione
seo-title: Miglioramento delle prestazioni del server applicazione
description: Questo documento descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server dell'applicazione AEM moduli.
seo-description: Questo documento descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server dell'applicazione AEM moduli.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
translation-type: tm+mt
source-git-commit: a26bc4e4ea10370dd2fc3403500004b9e378c418
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---


# Miglioramento delle prestazioni del server applicazione{#enhancing-application-server-performance}

Questo contenuto descrive le impostazioni facoltative che è possibile configurare per migliorare le prestazioni del server dell&#39;applicazione dei moduli AEM.

## Configurazione delle origini dati del server applicazione {#configuring-application-server-data-sources}

AEM moduli utilizza l&#39;archivio moduli AEM come origine dati. L&#39;archivio moduli AEM memorizza le risorse delle applicazioni e, in fase di esecuzione, i servizi possono recuperare le risorse dall&#39;archivio nel corso del processo aziendale automatizzato.

L&#39;accesso all&#39;origine dati può essere significativo, a seconda del numero di moduli AEM in esecuzione e del numero di utenti simultanei che accedono all&#39;applicazione. L&#39;accesso all&#39;origine dati può essere ottimizzato utilizzando il pool di connessioni. *Il* pool di connessioni è una tecnica utilizzata per evitare il sovraccarico necessario per creare nuove connessioni al database ogni volta che un&#39;applicazione o un oggetto server richiede l&#39;accesso al database. Il pool di connessioni è in genere utilizzato nelle applicazioni Web e aziendali ed è in genere gestito da un server applicazione, ma non solo a esso.

È importante configurare correttamente i parametri del pool di connessioni in modo da non esaurire mai le connessioni, il che può causare il deterioramento delle prestazioni dell&#39;applicazione.

Per configurare correttamente le impostazioni del pool di connessioni, è importante che l&#39;amministratore del server applicazioni controlli il pool di connessioni nelle ore di punta del giorno. Il monitoraggio assicura che siano sempre disponibili connessioni sufficienti per applicazioni e utenti. La maggior parte dei server applicazioni include strumenti di monitoraggio.

È possibile monitorare diverse statistiche per ogni istanza di origine dati JDBC nel dominio utilizzando la console di amministrazione del server WebLogic. Per ulteriori informazioni, consulta la documentazione WebLogic.

Quando l&#39;amministratore del server applicazioni determina le impostazioni corrette del pool di connessioni, deve comunicare tali informazioni all&#39;amministratore del database. L&#39;amministratore del database necessita di queste informazioni perché il numero di connessioni al database è uguale al numero di connessioni nel pool di connessioni per l&#39;origine dati. Quindi, completare i passaggi per configurare le impostazioni del pool di connessioni per il server applicazione e il tipo di origine dati come descritto di seguito.

### Configurare le impostazioni del pool di connessioni per WebLogic per  Oracle e MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. In Struttura dominio, fare clic su Servizi > JDBC > Origini dati e, nel riquadro a destra, fare clic su IDP_DS.
1. Nella schermata successiva, fate clic sulla scheda Configurazione > Pool di connessioni e immettete un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento capacità
   * Dimensioni cache istruzioni

1. Fate clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

### Configurare le impostazioni del pool di connessioni per WebLogic per SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. In Centro modifiche, fate clic su Blocca e modifica.
1. In Struttura dominio, fare clic su Servizi > JDBC > Origini dati e, nel riquadro a destra, fare clic su EDC_DS.
1. Nella schermata successiva, fate clic sulla scheda Configurazione > Pool di connessioni e immettete un valore nelle caselle seguenti:

   * Capacità iniziale
   * Capacità massima
   * Incremento capacità
   * Dimensioni cache istruzioni

1. Fate clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

### Configurare le impostazioni del pool di connessioni per WebSphere per DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Nella struttura di navigazione, fate clic su Risorse > JDBC > Fornitori JDBC. Nel riquadro a destra, fare clic sull&#39;origine dati creata, DB2 Universal JDBC Driver Provider o LiveCycle - db2 - IDP_DS.
1. In Proprietà aggiuntive, fare clic su Origini dati, quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fare clic su Proprietà pool di connessioni e immettere un valore nelle caselle Connessioni massime e Connessioni minime.
1. Fate clic su OK o Applica, quindi fate clic su Salva direttamente in configurazione principale.

### Configurare le impostazioni del pool di connessioni per WebSphere per  Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Nella struttura di navigazione, fate clic su Risorse > JDBC > Fornitori JDBC. Nel riquadro a destra, fare clic sull&#39;origine dati del driver Oracle JDBC  creata.
1. In Proprietà aggiuntive, fare clic su Origini dati, quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fare clic su Proprietà pool di connessioni e immettere un valore nelle caselle Connessioni massime e Connessioni minime.
1. Fate clic su OK o Applica, quindi fate clic su Salva direttamente in configurazione principale.

### Configurare le impostazioni del pool di connessioni per WebSphere per SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Nella struttura di navigazione, fare clic su Risorse > JDBC > Fornitori JDBC e, nel riquadro a destra, fare clic sull&#39;origine dati del driver JDBC definita dall&#39;utente creata.
1. In Proprietà aggiuntive, fare clic su Origini dati, quindi selezionare IDP_DS.
1. Nella schermata successiva, in Proprietà aggiuntive, fate clic su Proprietà pool di connessioni e immettete un valore nelle caselle Numero massimo di connessioni e Connessioni minime:
1. Fate clic su OK o Applica, quindi fate clic su Salva direttamente in configurazione principale.

## Ottimizzazione dei documenti in linea e impatto sulla memoria JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Se si elaborano in genere documenti di dimensioni relativamente ridotte, è possibile migliorare le prestazioni associate alla velocità di trasferimento del documento e allo spazio di archiviazione. A tal fine, implementa le seguenti configurazioni di prodotto AEM moduli:

* Aumentare la dimensione massima predefinita del documento in linea per AEM moduli in modo che sia maggiore della dimensione della maggior parte dei documenti.
* Per l&#39;elaborazione di file di grandi dimensioni, specificate le directory di memorizzazione che si trovano su un sistema a disco ad alta velocità o su un disco RAM.

La dimensione massima in linea e le directory di memorizzazione (la directory AEM dei file temporanei e la directory GDS) sono configurate nella console di amministrazione.

### Dimensioni documento e dimensione massima in linea {#document-size-and-maximum-inline-size}

Quando un documento inviato per l&#39;elaborazione da AEM moduli è minore o uguale alla dimensione inline massima predefinita del documento, il documento viene memorizzato sul server in linea e serializzato come oggetto Document  Adobe. La memorizzazione dei documenti in linea può comportare notevoli vantaggi in termini di prestazioni. Tuttavia, se si utilizza il flusso di lavoro dei moduli, il contenuto potrebbe anche essere memorizzato nel database a scopo di monitoraggio. Pertanto, l&#39;aumento della dimensione massima in linea potrebbe influenzare la dimensione del database.

Nel file system locale viene memorizzato un documento con dimensioni superiori a quelle massime. L&#39;oggetto Document del Adobe  che viene trasferito da e verso il server è solo un puntatore al file.

Quando il contenuto del documento è inline (ovvero inferiore alla dimensione massima in linea), il contenuto viene memorizzato nel database come parte del payload di serializzazione del documento. Pertanto, l&#39;aumento della dimensione massima in linea può influenzare la dimensione del database.

**Modificare la dimensione massima in linea**

1. Nella console di amministrazione, fate clic su Settings (Impostazioni) > Core System Settings (Impostazioni sistema di base) > Configurations (Configurazioni).
1. Immettete un valore nella casella Dimensioni inline massime documento predefinite e fate clic su OK.

   >[!NOTE]
   >
   >Il valore della proprietà Dimensione in linea massima documento deve essere identico per  AEM Forms nell&#39;ambiente JEE e  AEM Forms nel bundle OSGi incluso  AEM Forms nell&#39;ambiente JEE. Questo passaggio ha aggiornato il valore solo per  AEM Forms sull&#39;ambiente JEE e non per  AEM Forms sul bundle OSGi incluso  AEM Forms sull&#39;ambiente JEE.

1. Riavviate il server applicazione con la seguente proprietà di sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >Le proprietà di sistema sopra menzionate sostituiscono il valore della proprietà Document Max Inline Size impostata per  AEM Forms nell&#39;ambiente JEE e  AEM Forms nel bundle OSGi incluso  AEM Forms nell&#39;ambiente JEE.

>[!NOTE]
>
>La dimensione massima predefinita in linea è 65536 byte.

### Dimensione massima heap JVM {#jvm-maximum-heap-size}

Un aumento della dimensione massima in linea richiede più memoria per la memorizzazione dei documenti serializzati. Pertanto, in genere richiede anche un aumento della dimensione massima dell&#39;heap JVM.

Un sistema sovraccarico che elabora molti documenti può rapidamente saturare la memoria heap JVM. Per evitare un OutOfMemoryError, aumentare la dimensione massima dell&#39;heap JVM di un importo corrispondente alla dimensione dei documenti in linea moltiplicata per il numero di documenti generalmente eseguiti in un dato momento.

Aumento della dimensione massima dell&#39;heap JVM = (dimensione documenti in linea) x (numero medio di documenti elaborati).

**Calcolo della dimensione massima dell&#39;heap JVM**

In questo esempio, l&#39;heap massimo JVM corrente è impostato su 512 MB e la dimensione massima in linea è 64 KB. Il server deve essere configurato per lo scenario in cui 10 processi vengono eseguiti contemporaneamente e ogni processo ha 9 file di input e 1 file di risultati (un totale di 10 file per processo e 100 file elaborati contemporaneamente). Tutti i file hanno dimensioni inferiori a 512 KB.

Per memorizzare tutti i file in linea, impostate la dimensione massima in linea su almeno 512 KB.

L&#39;aumento richiesto nella dimensione massima dell&#39;heap JVM è calcolato utilizzando la seguente equazione:

(512 KB) x (100) = 51200 KB, o 50 MB

La dimensione massima dell&#39;heap JVM deve essere aumentata di 50 MB per un totale di 562 MB.

**Considerazione della frammentazione dell&#39;heap**

Se si impostano le dimensioni dei documenti in linea su valori elevati, si aumenta il rischio di un errore OutOfMemoryError sui sistemi che sono inclini a un&#39;elevata frammentazione. Per memorizzare un documento in linea, la memoria heap JVM deve disporre di spazio contiguo sufficiente. Alcuni sistemi operativi, JVM e algoritmi di raccolta dei rifiuti sono inclini ad accumulare la frammentazione. La frammentazione riduce la quantità di spazio heap contiguo e può portare a un OutOfMemoryError anche quando esiste spazio totale sufficiente.

Ad esempio, le operazioni precedenti sul server delle applicazioni hanno lasciato l&#39;heap JVM in uno stato frammentato e il Garbage Collector non è in grado di comprimere l&#39;heap abbastanza da recuperare grandi blocchi di spazio libero. È possibile che si verifichi un errore OutOfMemory anche se la dimensione massima dell&#39;heap JVM è stata regolata in modo da aumentare la dimensione massima in linea.

Per tenere conto della frammentazione dell&#39;heap, la dimensione del documento in linea non deve essere superiore allo 0,1% della dimensione totale dell&#39;heap. Ad esempio, una dimensione massima dell&#39;heap JVM di 512 MB può supportare una dimensione massima in linea di 512 MB x 0.001 = 0,512 MB, o 512 KB.

## Miglioramenti di WebSphere Application Server {#websphere-application-server-enhancements}

Questa sezione descrive le impostazioni specifiche di un ambiente WebSphere Application Server.

### Incremento della memoria massima allocata alla JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Se si esegue Configuration Manager o si tenta di generare codice di implementazione JavaBeans Enterprise (EJB) utilizzando l&#39;utilità della riga di comando *ejbdeployment* e si verifica un errore OutOfMemory, aumentare la quantità di memoria allocata alla JVM.

1. Modificate lo script ejbdeployment nella directory *[appserver root]*/deploytool/itp/:

   * (Windows) `ejbdeploy.bat`
   * (Linux e UNIX) `ejbdeploy.sh`

1. Trovate il parametro `-Xmx256M` e modificatelo in un valore più alto, ad esempio `-Xmx1024M`.
1. Salvate il file.
1. Eseguire il comando `ejbdeploy` o ridistribuire utilizzando Configuration Manager.

## Miglioramento delle prestazioni di Windows Server 2003 con LDAP {#improving-windows-server-2003-performance-with-ldap}

Questo contenuto descrive le impostazioni specifiche di un ambiente del sistema operativo Microsoft Windows Server 2003.

L&#39;utilizzo del pool di connessioni sulla connessione di ricerca può ridurre il numero di porte necessarie fino al 50%. Questo perché la connessione utilizza sempre le stesse credenziali per un determinato dominio e il contesto e gli oggetti correlati sono chiusi in modo esplicito.

### Configurazione di Windows Server per il pool di connessioni {#configure-your-windows-server-for-connection-pooling}

1. Fare clic su Start > Esegui per avviare l&#39;editor del Registro di sistema e, nella casella Apri, digitare `regedit` e fare clic su OK.
1. Vai alla chiave del Registro di sistema `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. Nel riquadro a destra dell’editor del Registro di sistema, individuate il nome del valore TcpTimedWaitDelay. Se il nome non viene visualizzato, selezionate Modifica > Nuovo > Valore DWORD dalla barra dei menu per aggiungere il nome.
1. Nella casella Nome, digitare `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Se non viene visualizzato un cursore lampeggiante e `New Value #` all&#39;interno della casella, fare clic con il pulsante destro del mouse nel pannello di destra, selezionare Rinomina e digitare `TcpTimedWaitDelay`*nella casella Nome.*

1. Ripetere il passaggio 4 per i nomi dei valori MaxUserPort, MaxHashTableSize e MaxFreeTcbs.
1. Fate doppio clic nel riquadro a destra per impostare il valore TcpTimedWaitDelay. In Base, selezionare Decimale e, nella casella Valore, digitare `30`.
1. Fare doppio clic nel riquadro di destra per impostare il valore MaxUserPort. In Base, selezionare Decimale e, nella casella Valore, digitare `65534`.
1. Fare doppio clic nel riquadro di destra per impostare il valore MaxHashTableSize. In Base, selezionare Decimale e, nella casella Valore, digitare `65536`.
1. Fare doppio clic nel riquadro di destra per impostare il valore MaxFreeTcbs. In Base, selezionare Decimale e, nella casella Valore, digitare `16000`.

>[!NOTE]
>
>Si possono verificare gravi problemi se si modifica il Registro di sistema in modo errato utilizzando l&#39;Editor del Registro di sistema o utilizzando un altro metodo. Questi problemi possono richiedere la reinstallazione del sistema operativo. Modificare il registro a proprio rischio.

