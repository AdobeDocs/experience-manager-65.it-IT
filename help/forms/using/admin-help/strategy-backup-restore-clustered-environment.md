---
title: Strategia per il backup e il ripristino in un ambiente cluster
seo-title: Strategia per il backup e il ripristino in un ambiente cluster
description: Se l'implementazione dei moduli AEM memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia per il backup di tali dati, in modo che rimangano sincronizzati con i dati dei moduli AEM.
seo-description: Se l'implementazione dei moduli AEM memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia per il backup di tali dati, in modo che rimangano sincronizzati con i dati dei moduli AEM.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Strategia per il backup e il ripristino in un ambiente cluster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Se l&#39;implementazione dei moduli AEM memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia per il backup di tali dati, in modo che rimangano sincronizzati con i dati dei moduli AEM. Inoltre, l&#39;applicazione deve essere progettata in modo da essere sufficientemente robusta per gestire uno scenario in cui i database aggiuntivi non sono sincronizzati. È vivamente consigliato che qualsiasi operazione del database eseguita sia eseguita nel contesto di una transazione per mantenere uno stato coerente.

È necessario eseguire il backup delle seguenti parti del sistema dei moduli di AEM per recuperare da eventuali errori:

* Database utilizzato dai moduli AEM
* GDS con dati longevi e altri documenti persistenti
* Database AEM (archivio crx)

>[!NOTE]
>
>È necessario eseguire il backup di tutti gli altri dati utilizzati dalla configurazione dei moduli AEM, ad esempio i font del cliente, i dati dei connettori e così via.

## Eseguire il backup di un ambiente cluster {#back-up-a-clustered-environment}

Questo argomento illustra le strategie seguenti per il backup di qualsiasi ambiente cluster di moduli AEM:

* Backup offline con tempi di inattività
* Backup offline senza tempi di inattività (backup di un nodo slave che viene arrestato)
* Backup online senza tempi di inattività ma ritardo nella risposta
* Eseguire il backup del file delle proprietà di Bootstrap

### Backup offline con tempi di inattività {#offline-backup-with-downtime}

1. Arrestate l&#39;intero cluster e i servizi correlati. (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, eseguire il backup del database, di GDS e dei connettori. (vedere [File per il backup e il ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup dell’archivio AEM offline, effettuate le seguenti operazioni:

   1. Per ciascun nodo del cluster, eseguite il backup del file che contiene l&#39;ID del nodo del cluster.
   1. Esegui il backup di tutti i file di qualsiasi nodo del cluster slave, incluse le sottodirectory.
   1. Eseguire separatamente il backup dell&#39;ID del repository o del sistema di ciascun nodo del cluster.
   Per i passaggi dettagliati, consultate [Backup e ripristino](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Esegui il backup di qualsiasi altro dato, ad esempio i font del cliente.
1. Riavviate il cluster.

### Backup offline senza tempi di inattività {#offline-backup-with-no-downtime}

1. Accedete alla modalità di backup continuo. (vedere [Inserimento delle modalità](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)di backup)

   Si noti che è necessario lasciare la modalità di backup a scorrimento dopo un ripristino.

1. Arrestate i nodi slave del cluster rispetto ad AEM. (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, eseguire il backup del database, di GDS e dei connettori. (vedere [File per il backup e il ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup dell’archivio AEM offline, effettuate le seguenti operazioni:

   1. Per ciascun nodo del cluster, eseguite il backup del file che contiene l&#39;ID del nodo del cluster.
   1. Esegui il backup di tutti i file di qualsiasi nodo del cluster slave, incluse le sottodirectory.
   1. Eseguire il backup di repository/system.id di ciascun nodo del cluster separatamente.
   Per i passaggi dettagliati, consultate [Backup e ripristino](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Esegui il backup di qualsiasi altro dato, ad esempio i font del cliente.
1. Riavviate il cluster.

### Backup online senza tempi di inattività ma ritardo nella risposta {#online-backup-with-no-downtime-but-delay-in-response}

1. Accedete alla modalità di backup continuo. (vedere [Inserimento delle modalità](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)di backup)

   Si noti che è necessario lasciare la modalità di backup a scorrimento dopo un ripristino.

1. Arrestate i nodi slave del cluster rispetto ad AEM. (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, eseguire il backup del database, di GDS e dei connettori. (vedere [File per il backup e il ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup dell’archivio AEM online, effettuate le seguenti operazioni:

   1. Per ciascun nodo del cluster, eseguite il backup del file che contiene il cluster_node.id.
   1. Eseguire il backup di repository/system.id di ciascun nodo del cluster separatamente.
   1. Su qualsiasi nodo slave, eseguire un backup online del repository per i passaggi dettagliati vedere Backup online.

1. Esegui il backup di qualsiasi altro dato, ad esempio i font del cliente.
1. Riavviate il cluster.

### Eseguire il backup del file delle proprietà di Bootstrap {#back-up-the-bootstrap-properties-file}

Quando creiamo un cluster AEM, viene creato un file di proprietà nel server applicazione per tutti i nodi slave. È consigliabile eseguire il backup del file delle proprietà di Bootstrap. Il file si trova nel seguente percorso sul server dell’applicazione:

* JBoss: nella directory BIN
* WebLogic: nella directory del dominio
* WebSphere: nella directory del profilo

È necessario eseguire il backup del file per lo scenario di disaster recovery del nodo slave di AEM e sostituirlo nel percorso specificato sul server dell’applicazione, se ripristinato.

## Ripristino in un ambiente cluster {#recovery-in-a-clustered-environment}

In caso di guasto dell&#39;intero cluster o di un singolo nodo, è necessario ripristinarlo utilizzando il backup.

Per un ripristino a nodo singolo, è sufficiente chiudere il nodo singolo ed eseguire la procedura di ripristino a nodo singolo.

Se l&#39;intero cluster ha esito negativo a causa di errori come arresto anomalo del database, è necessario eseguire i seguenti passaggi. Il ripristino dipende dal metodo di backup utilizzato.

### Ripristino di un singolo nodo {#restoring-a-single-node}

1. Arrestare il nodo danneggiato.

   >[!NOTE]
   >
   >Se il nodo danneggiato è un nodo master AEM, chiudi l’intero nodo del cluster.

1. Ricreare il sistema fisico da un&#39;immagine del sistema.
1. Applicare patch o aggiornamenti ai moduli AEM applicati dopo la creazione dell&#39;immagine. Queste informazioni sono state registrate durante la procedura di backup. I moduli AEM devono essere recuperati allo stesso livello di patch esistente al momento del backup del sistema.
1. (*Facoltativo*) Se tutti gli altri nodi funzionano correttamente, è possibile che anche l’archivio AEM sia danneggiato. In questo caso, nel file error.log dell&#39;archivio AEM verrà visualizzato un messaggio di non sincronizzazione dell&#39;archivio.

   Per ripristinare il repository, eseguire le operazioni seguenti.

   >[!NOTE]
   >
   >Se il backup del repository crx compresso è stato portato online, decomprimetelo in qualsiasi posizione e seguite il processo di ripristino offline.

   1. Eliminare le directory archivio, condivisa, versione e aree di lavoro nella directory clusterNode del nodo.
   1. Ripristinare il backup del nodo del cluster (incluse le sottodirectory) nel nodo.
   1. Eliminare il file clusterNode/revision.log sul nodo.
   1. Eliminate il blocco .lock sul nodo, se presente.
   1. Eliminate l&#39;eventuale repository/system.id sul nodo.
   1. Elimina i file &amp;ast;&amp;ast;/listener.properties sul nodo, se presenti.
   1. Ripristina repository/cluster_node.id per singoli nodi del cluster.

>[!NOTE]
>
>Considerate quanto segue:

* Se il nodo non riuscito è un nodo master AEM, copiate tutto il contenuto dalla cartella dell&#39;archivio slave (crx-repository\crx.0000 dove 0000 può essere costituito da qualsiasi cifra) nella cartella dell&#39;archivio crx-repository\ ed eliminate la cartella dell&#39;archivio slave.
* Prima di riavviare un nodo cluster, assicurarsi di eliminare l&#39;archivio /clustered.txt dal nodo master.
* Assicurarsi che il nodo master sia avviato per primo e che, una volta completamente attivato, avvii altri nodi.

### Ripristino dell’intero cluster {#restoring-the-entire-cluster}

1. Arrestate tutti i nodi del cluster.
1. Ricreare il sistema fisico da un&#39;immagine del sistema.
1. Applicazione di patch o aggiornamenti ai moduli AEMiformi AEM applicati dopo la creazione dell&#39;immagine. Queste informazioni sono state registrate nel passaggio 1 della procedura di backup. I moduli AEM devono essere recuperati allo stesso livello di patch esistente al momento del backup del sistema.
1. Ripristinare il database, GDS e i connettori.
1. Per ripristinare l’archivio AEM offline, effettuate le seguenti operazioni:

   >[!NOTE]
   >
   >Se il backup del repository crx compresso è stato portato online, decomprimetelo in qualsiasi posizione e seguite il processo di ripristino offline.

   1. In tutti i nodi del cluster, eliminate le directory archivio, condivisa, versione e aree di lavoro nella directory clusterNode.
   1. Eliminate tutti i file e le directory nella directory condivisa.
   1. Ripristinare il backup del nodo del cluster (incluse le sottodirectory) in un nodo del cluster.
   1. Copiate tutti i file del nodo del cluster ripristinato in tutti gli altri nodi del cluster. Una volta fatto, ogni nodo del cluster contiene gli stessi dati.
   1. Eliminate il file clusterNode/revision.log in tutti i nodi del cluster.
   1. Eliminate il blocco su tutti i nodi del cluster, se presente.
   1. Eliminate i repository/system.id di tutti i nodi del cluster, se presenti.
   1. Elimina i file &amp;ast;&amp;ast;/listener.properties, se presenti, su tutti i nodi del cluster.
   1. Ripristina repository/cluster_node.id per singoli nodi del cluster.

>[!NOTE]
>
>Considerate quanto segue:

* Se il nodo non riuscito era un nodo master AEM, copiate tutto il contenuto dalla cartella dell&#39;archivio slave (simile a crx-repository\crx.0000 dove 0000 può essere costituito da qualsiasi cifra) nella cartella dell&#39;archivio crx.
* Prima di riavviare un nodo cluster, assicurarsi di eliminare l&#39;archivio /clustered.txt dal nodo master.
* Assicurarsi che il nodo master sia avviato per primo e che, una volta completamente attivato, avvii altri nodi.

## Eseguire il backup e ripristinare il nodo di pubblicazione della soluzione di gestione della corrispondenza {#back-up-and-restore-correspondence-management-solution-publish-node}

Il nodo editore non ha alcuna relazione master-slave in un ambiente cluster. È possibile eseguire il backup di qualsiasi nodo Publisher seguendo [Backup e Ripristino](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

### Ripristino di un singolo nodo editore {#recover-a-single-publisher-node}

1. Arrestate il nodo che deve essere recuperato e non eseguite alcuna attività di pubblicazione finché il nodo non viene nuovamente attivato.
1. Ripristinare il nodo Pubblica mediante il [ripristino del backup](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring del backup).

### Ripristino di un cluster {#recover-a-cluster}

1. Arrestate il cluster.
1. Ripristinare il nodo Pubblica mediante il [ripristino del backup](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring del backup).
1. Avviate il nodo master seguito dal nodo slave del cluster di autori.

