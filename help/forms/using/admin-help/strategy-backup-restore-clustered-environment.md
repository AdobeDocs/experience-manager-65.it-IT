---
title: Strategia di backup e ripristino in un ambiente cluster
seo-title: Strategy for backup and restore in a clustered environment
description: Se l’implementazione dei moduli di AEM memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia di backup dei dati, in modo che rimangano sincronizzati con i dati dei moduli di AEM.
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 0%

---

# Strategia di backup e ripristino in un ambiente cluster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Se l’implementazione dei moduli di AEM memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia di backup dei dati, in modo che rimangano sincronizzati con i dati dei moduli di AEM. Inoltre, l&#39;applicazione deve essere progettata in modo che sia abbastanza robusta da gestire uno scenario in cui i database aggiuntivi non sono sincronizzati. Si consiglia vivamente di eseguire qualsiasi operazione di database nel contesto di una transazione per mantenere uno stato coerente.

È necessario eseguire il backup delle seguenti parti del sistema di moduli AEM per recuperare da eventuali errori:

* Database utilizzato dai moduli AEM
* GDS con dati di lunga durata e altri documenti persistenti
* Database AEM (archivio crx)

>[!NOTE]
>
>È necessario eseguire il backup di tutti gli altri dati utilizzati dalla configurazione dei moduli di AEM, ad esempio i font dei clienti, i dati dei connettori e così via.

## Eseguire il backup di un ambiente cluster {#back-up-a-clustered-environment}

Questo argomento illustra le seguenti strategie per eseguire il backup di qualsiasi ambiente cluster AEM forms:

* Backup offline con tempi di inattività
* Backup offline senza tempi di inattività (backup di un nodo secondario arrestato)
* Backup online senza tempi di inattività ma ritardo nella risposta
* Esegui il backup del file delle proprietà Bootstrap

### Backup offline con tempi di inattività {#offline-backup-with-downtime}

1. Arrestare l&#39;intero cluster e i servizi correlati. (vedi [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, esegui il backup del database, di GDS e dei connettori. (vedi [File di backup e ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup AEM repository offline, effettua le seguenti operazioni:

   1. Per ogni nodo del cluster, esegui il backup del file contenente l&#39;id del nodo del cluster.
   1. Esegui il backup di tutti i file di qualsiasi nodo secondario del cluster, incluse le sottodirectory.
   1. Esegui separatamente il backup dell&#39;ID archivio/sistema di ciascun nodo del cluster.

   Per i passaggi dettagliati vedi [Backup e ripristino](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Esegui il backup di qualsiasi altro dato, ad esempio i font del cliente.
1. Riavvia il cluster.

### Backup offline senza tempi di inattività {#offline-backup-with-no-downtime}

1. Accedere alla modalità di backup continuo. (vedi [Accesso alle modalità di backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Lasciare la modalità di backup in esecuzione dopo un ripristino.

1. Spegni uno dei nodi secondari del cluster per quanto riguarda AEM. (vedi [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, esegui il backup del database, di GDS e dei connettori. (vedi [File di backup e ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup AEM repository offline, effettua le seguenti operazioni:

   1. Per ogni nodo del cluster, esegui il backup del file contenente l&#39;id del nodo del cluster.
   1. Esegui il backup di tutti i file di qualsiasi nodo secondario del cluster, incluse le sottodirectory.
   1. Esegui separatamente il backup repository/system.id di ogni nodo del cluster.

   Per i passaggi dettagliati vedi [Backup e ripristino](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Esegui il backup di qualsiasi altro dato, ad esempio i font del cliente.
1. Riavvia il cluster.

### Backup online senza tempi di inattività ma ritardo nella risposta {#online-backup-with-no-downtime-but-delay-in-response}

1. Accedere alla modalità di backup continuo. (vedi [Accesso alle modalità di backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Lasciare la modalità di backup in esecuzione dopo un ripristino.

1. Spegni uno dei nodi secondari del cluster per quanto riguarda AEM. (vedi [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, esegui il backup del database, di GDS e dei connettori. (vedi [File di backup e ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup online AEM repository, esegui i seguenti passaggi:

   1. Per ogni nodo del cluster, esegui il backup del file contenente il cluster_node.id.
   1. Esegui separatamente il backup repository/system.id di ogni nodo del cluster.
   1. Su qualsiasi nodo secondario, eseguire un backup online dell&#39;archivio per i passaggi dettagliati vedere Backup online.

1. Esegui il backup di qualsiasi altro dato, ad esempio i font del cliente.
1. Riavvia il cluster.

### Esegui il backup del file delle proprietà Bootstrap {#back-up-the-bootstrap-properties-file}

Quando creiamo un cluster AEM, viene creato un file di proprietà nel server applicazioni per tutti i nodi secondari. Si consiglia di eseguire il backup del file delle proprietà Bootstrap. È possibile trovare il file nel seguente percorso sul server dell&#39;applicazione:

* JBoss®: nella directory BIN
* WebLogic: nella directory del dominio
* WebSphere®: nella directory dei profili

Eseguire il backup del file per lo scenario di disaster recovery AEM nodo secondario e sostituirlo nel percorso specificato sul server applicazioni, se ripristinato.

## Ripristino in un ambiente cluster {#recovery-in-a-clustered-environment}

Se si verifica un errore dell&#39;intero cluster o di un singolo nodo, ripristinarlo utilizzando il backup.

Per un ripristino a nodo singolo, arrestare il nodo singolo ed eseguire la procedura di ripristino a nodo singolo.

Se l&#39;intero cluster non riesce a causa di errori come arresto anomalo del database, esegui i seguenti passaggi. Il ripristino dipende dal metodo di backup utilizzato.

### Ripristino di un singolo nodo {#restoring-a-single-node}

1. Interrompi il nodo danneggiato.

   >[!NOTE]
   >
   >Se il nodo danneggiato è un nodo primario AEM, spegnere l&#39;intero nodo del cluster.

1. Ricrea il sistema fisico da un&#39;immagine di sistema.
1. Applicare patch o aggiornamenti ai moduli AEM applicati dopo la creazione dell’immagine. Queste informazioni sono state registrate durante la procedura di backup. AEM moduli devono essere recuperati allo stesso livello di patch di quando il sistema è stato sottoposto a backup.
1. (*Facoltativo*) Se tutti gli altri nodi funzionano bene, è possibile che anche l&#39;archivio AEM sia danneggiato. In questo caso, vedrai un messaggio di annullamento della sincronizzazione dell&#39;archivio nel file error.log dell&#39;archivio AEM.

   Per ripristinare l&#39;archivio, esegui i seguenti passaggi.

   >[!NOTE]
   >
   >Se un backup zip crx-repository è stato portato online, decomprimerlo in qualsiasi posizione e seguire il processo di ripristino offline.

   1. Elimina le directory repository, shared, version e workspaces nella directory clusterNode del nodo.
   1. Ripristina il backup del nodo del cluster (incluse le sottodirectory) sul nodo .
   1. Elimina il file clusterNode/revision.log sul nodo .
   1. Elimina il blocco sul nodo, se esiste.
   1. Elimina il file repository/system.id sul nodo , se presente.
   1. Elimina i file &amp;ast;&amp;ast;/listener.properties sul nodo, se presenti.
   1. Ripristina repository/cluster_node.id per i singoli nodi del cluster.

>[!NOTE]
>
>Considera i seguenti punti:

* Se il nodo non riuscito era un nodo primario AEM, copia tutto il contenuto dalla cartella archivio secondaria (crx-repository\crx.0000 dove 0000 può essere a qualsiasi cifra) nella cartella archivio crx-repository\ ed elimina la cartella archivio secondaria.
* Prima di riavviare qualsiasi nodo del cluster, assicurati di eliminare l&#39;archivio /clustered.txt dal nodo principale.
* Assicurati che il nodo primario sia avviato prima e dopo che è attivo, avvia altri nodi.

### Ripristino dell&#39;intero cluster {#restoring-the-entire-cluster}

1. Interrompi tutti i nodi del cluster.
1. Ricrea il sistema fisico da un&#39;immagine di sistema.
1. Applica patch o aggiornamenti ai moduli AEMAEM applicati dopo la creazione dell’immagine. Queste informazioni sono state registrate nella fase 1 della procedura di backup. AEM moduli devono essere recuperati allo stesso livello di patch di quando il sistema è stato sottoposto a backup.
1. Ripristinare il database, GDS e i connettori.
1. Per ripristinare l&#39;archivio AEM offline, procedi come segue:

   >[!NOTE]
   >
   >Se un backup zip crx-repository è stato portato online, decomprimerlo in qualsiasi posizione e seguire il processo di ripristino offline.

   1. Su tutti i nodi del cluster, elimina le directory archivio, condivise, versione e aree di lavoro nella directory clusterNode .
   1. Elimina tutti i file e le directory nella directory condivisa.
   1. Ripristinare il backup del nodo del cluster (incluse le sottodirectory) in un nodo del cluster.
   1. Copia tutti i file del nodo cluster ripristinato in tutti gli altri nodi del cluster. Al termine, ogni nodo del cluster contiene gli stessi dati.
   1. Elimina il file clusterNode/revision.log su tutti i nodi del cluster.
   1. Elimina il blocco su tutti i nodi del cluster, se esiste.
   1. Elimina tutti i nodi del cluster repository/system.id, se presenti.
   1. Elimina i file &amp;ast;&amp;ast;/listener.properties su tutti i nodi del cluster, se presenti.
   1. Ripristina repository/cluster_node.id per i singoli nodi del cluster.

>[!NOTE]
>
>Considera i seguenti punti:

* Se il nodo non riuscito era un nodo primario AEM, copia tutto il contenuto dalla cartella archivio secondaria (assomiglia a crx-repository\crx.0000 dove 0000 può essere a qualsiasi cifra) nella cartella archivio crx-repository\.
* Prima di riavviare qualsiasi nodo del cluster, assicurati di eliminare l&#39;archivio /clustered.txt dal nodo principale.
* Assicurati che il nodo primario sia avviato prima e dopo che è attivo, avvia altri nodi.

## Esegui il backup e ripristina il nodo di pubblicazione della soluzione di gestione della corrispondenza {#back-up-and-restore-correspondence-management-solution-publish-node}

Il nodo editore non ha alcuna relazione primaria-secondaria in un ambiente cluster. È possibile eseguire il backup di qualsiasi nodo di Publisher eseguendo le operazioni seguenti [Backup e ripristino](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recupera un singolo nodo di pubblicazione {#recover-a-single-publisher-node}

1. Spegni il nodo che deve essere recuperato e non eseguire alcuna attività di pubblicazione fino a quando il nodo non è di nuovo attivo.
1. Ripristina il nodo Pubblica utilizzando [Ripristino del backup](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recuperare un cluster {#recover-a-cluster}

1. Spegnere il cluster.
1. Ripristina il nodo Pubblica utilizzando [Ripristino del backup](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. Avvia il nodo principale seguito dal nodo secondario del cluster di authoring.
