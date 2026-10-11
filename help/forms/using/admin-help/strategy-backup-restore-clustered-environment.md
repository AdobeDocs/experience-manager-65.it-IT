---
title: Strategia di backup e ripristino in un ambiente in cluster
description: Se l’implementazione di AEM Forms memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia per eseguire il backup di tali dati, garantendo che rimangano sincronizzati con i dati di AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 98c96349-f253-475f-b646-352269814a38
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 7%
---
# Strategia di backup e ripristino in un ambiente in cluster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Se l’implementazione di AEM Forms memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia per eseguire il backup di tali dati, garantendo che rimangano sincronizzati con i dati di AEM Forms. Inoltre, l’applicazione deve essere progettata in modo da essere sufficientemente solida per gestire uno scenario in cui i database aggiuntivi non sono sincronizzati. Si consiglia vivamente di eseguire le operazioni di database nel contesto di una transazione per mantenere uno stato coerente.

È necessario eseguire il backup delle seguenti parti del sistema AEM Forms per ripristinare eventuali errori:

* Database utilizzato da AEM Forms
* GDS con dati di lunga durata e altri documenti persistenti
* database AEM (crx-repository)

>[!NOTE]
>
>È necessario eseguire il backup di tutti gli altri dati utilizzati dalla configurazione di AEM Forms, ad esempio i caratteri del cliente, i dati dei connettori e così via.

## Eseguire il backup di un ambiente cluster {#back-up-a-clustered-environment}

In questo argomento vengono illustrate le strategie seguenti per eseguire il backup di qualsiasi ambiente cluster di AEM Form:

* Backup offline con downtime
* Backup non in linea senza tempi di inattività (backup di un nodo secondario che viene arrestato)
* Backup online senza tempi di inattività ma con ritardo nella risposta
* Eseguire il backup del file delle proprietà di Bootstrap

### Backup offline con downtime {#offline-backup-with-downtime}

1. Arrestare l&#39;intero cluster e i servizi correlati. (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, eseguire il backup del database, di GDS e dei connettori. (vedi [File per il backup e il ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup offline dell’archivio di AEM, effettua le seguenti operazioni:

   1. Per ogni nodo cluster, eseguire il backup del file che contiene l&#39;ID del nodo cluster.
   1. Eseguire il backup di tutti i file di qualsiasi nodo cluster secondario, incluse le sottodirectory.
   1. Eseguire il backup dell&#39;ID di sistema/repository di ciascun nodo cluster separatamente.

   Per i passaggi dettagliati, vedere [Backup e ripristino](https://helpx.adobe.com/it/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Eseguire il backup di qualsiasi altro dato, ad esempio i caratteri del cliente.
1. Riavviare il cluster.

### Backup offline senza downtime {#offline-backup-with-no-downtime}

1. Attiva la modalità di backup continuo. (vedere [Accesso alle modalità di backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Lascia la modalità di backup continuo dopo un ripristino.

1. Arrestare i nodi secondari del cluster relativi ad AEM. (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, eseguire il backup del database, di GDS e dei connettori. (vedi [File per il backup e il ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup offline dell’archivio di AEM, effettua le seguenti operazioni:

   1. Per ogni nodo cluster, eseguire il backup del file che contiene l&#39;ID del nodo cluster.
   1. Eseguire il backup di tutti i file di qualsiasi nodo cluster secondario, incluse le sottodirectory.
   1. Eseguire il backup repository/system.id di ogni nodo cluster separatamente.

   Per i passaggi dettagliati, vedere [Backup e ripristino](https://helpx.adobe.com/it/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Eseguire il backup di qualsiasi altro dato, ad esempio i caratteri del cliente.
1. Riavviare il cluster.

### Backup online senza tempi di inattività ma con ritardo nella risposta {#online-backup-with-no-downtime-but-delay-in-response}

1. Attiva la modalità di backup continuo. (vedere [Accesso alle modalità di backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Lascia la modalità di backup continuo dopo un ripristino.

1. Arrestare i nodi secondari del cluster relativi ad AEM. (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Su qualsiasi nodo, eseguire il backup del database, di GDS e dei connettori. (vedi [File per il backup e il ripristino](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Per eseguire il backup online dell’archivio di AEM, effettua le seguenti operazioni:

   1. Per ogni nodo del cluster, eseguire il backup del file che contiene il file cluster_node.id.
   1. Eseguire il backup repository/system.id di ogni nodo cluster separatamente.
   1. Su qualsiasi nodo secondario, eseguire un backup online dell&#39;archivio per i passaggi dettagliati vedere Backup online.

1. Eseguire il backup di qualsiasi altro dato, ad esempio i caratteri del cliente.
1. Riavviare il cluster.

### Eseguire il backup del file delle proprietà di Bootstrap {#back-up-the-bootstrap-properties-file}

Quando si crea un cluster AEM, nel server applicazioni viene creato un file delle proprietà per tutti i nodi secondari. Si consiglia di eseguire il backup del file delle proprietà di Bootstrap. È possibile trovare il file nella posizione seguente sul server applicazioni:

* JBoss®: nella directory BIN
* WebLogic: nella directory di dominio
* WebSphere®: nella directory del profilo

Eseguire il backup del file per lo scenario di disaster recovery del nodo secondario di AEM e sostituirlo nella posizione specificata sul server applicazioni, se ripristinato.

## Ripristino in un ambiente cluster {#recovery-in-a-clustered-environment}

In caso di errore dell&#39;intero cluster o di un singolo nodo, ripristinarlo utilizzando il backup.

Per il ripristino di un singolo nodo, arrestare il nodo singolo ed eseguire la procedura di ripristino del singolo nodo.

Nel caso in cui l&#39;intero cluster non riesca a causa di errori quali l&#39;arresto anomalo del database, effettuare le seguenti operazioni. Il ripristino dipende dal metodo di backup utilizzato.

### Ripristino di un singolo nodo {#restoring-a-single-node}

1. Arresta il nodo danneggiato.

   >[!NOTE]
   >
   >Se il nodo danneggiato è un nodo primario di AEM, arrestare l&#39;intero nodo del cluster.

1. Ricreare il sistema fisico da un&#39;immagine di sistema.
1. Applica patch o aggiornamenti ad AEM Forms che sono stati applicati dopo la creazione dell’immagine. Queste informazioni sono state registrate durante la procedura di backup. I moduli AEM devono essere ripristinati allo stesso livello di patch utilizzato al momento del backup del sistema.
1. (*Facoltativo*) Se tutti gli altri nodi funzionano correttamente, è possibile che anche l&#39;archivio AEM sia danneggiato. In questo caso, nel file error.log dell’archivio AEM verrà visualizzato un messaggio di dissincronizzazione dell’archivio.

   Per ripristinare l’archivio, effettua le seguenti operazioni.

   >[!NOTE]
   >
   >Se un backup dell’archivio crx compresso è stato portato online, decomprimerlo in qualsiasi posizione e seguire il processo di ripristino offline.

   1. Eliminare le directory repository, shared, version e workspace nella directory clusterNode del nodo.
   1. Ripristinare il backup del nodo del cluster (incluse le sottodirectory) nel nodo.
   1. Elimina il file clusterNode/revision.log sul nodo.
   1. Elimina il file .lock sul nodo, se esistente.
   1. Elimina l’eventuale repository/system.id sul nodo.
   1. Eliminare i file &ast;&ast;/listener.properties sul nodo, se presenti.
   1. Ripristina repository/cluster_node.id per i singoli nodi cluster.

>[!NOTE]
>
>Considera i seguenti punti:

* Se il nodo non riuscito era un nodo primario di AEM, copia tutto il contenuto dalla cartella dell’archivio secondario (crx-repository\crx.0000, dove 0000 può essere qualsiasi cifra) alla cartella dell’archivio crx-repository\ ed elimina la cartella dell’archivio secondario.
* Prima di riavviare qualsiasi nodo cluster, accertarsi di eliminare l&#39;archivio /clustered.txt dal nodo principale.
* Verificare che il nodo primario sia avviato per primo e, dopo l&#39;attivazione, avviare altri nodi.

### Ripristino dell&#39;intero cluster {#restoring-the-entire-cluster}

1. Arrestare tutti i nodi del cluster.
1. Ricreare il sistema fisico da un&#39;immagine di sistema.
1. Applicazione di patch o aggiornamenti ai moduli di AEM FormsAEM applicati dopo la creazione dell&#39;immagine. Queste informazioni sono state registrate nella fase 1 della procedura di backup. I moduli AEM devono essere ripristinati allo stesso livello di patch utilizzato al momento del backup del sistema.
1. Ripristinare il database, GDS e i connettori.
1. Per ripristinare l’archivio AEM offline, effettua le seguenti operazioni:

   >[!NOTE]
   >
   >Se un backup dell’archivio crx compresso è stato portato online, decomprimerlo in qualsiasi posizione e seguire il processo di ripristino offline.

   1. In tutti i nodi del cluster, eliminare le directory repository, shared, version e workspace nella directory clusterNode.
   1. Elimina tutti i file e le directory nella directory condivisa.
   1. Ripristinare il backup del nodo del cluster (comprese le sottodirectory) in un nodo del cluster.
   1. Copiare tutti i file del nodo cluster ripristinato in tutti gli altri nodi cluster. Al termine, ogni nodo cluster contiene gli stessi dati.
   1. Eliminare il file clusterNode/revision.log in tutti i nodi del cluster.
   1. Eliminare il blocco in tutti i nodi del cluster, se esistente.
   1. Eliminare tutti i nodi del cluster repository/system.id, se esiste.
   1. Eliminare i file &ast;&ast;/listener.properties su tutti i nodi del cluster, se esistenti.
   1. Ripristina repository/cluster_node.id per i singoli nodi cluster.

>[!NOTE]
>
>Considera i seguenti punti:

* Se il nodo non riuscito era un nodo primario di AEM, copia tutto il contenuto dalla cartella dell’archivio secondario (sembra crx-repository\crx.0000, dove 0000 può essere qualsiasi cifra) alla cartella dell’archivio crx-repository\.
* Prima di riavviare qualsiasi nodo cluster, accertarsi di eliminare l&#39;archivio /clustered.txt dal nodo principale.
* Verificare che il nodo primario sia avviato per primo e, dopo l&#39;attivazione, avviare altri nodi.

## Backup e ripristino del nodo di pubblicazione della soluzione per la gestione della corrispondenza {#back-up-and-restore-correspondence-management-solution-publish-node}

Il nodo dell&#39;editore non ha alcuna relazione primario-secondario in un ambiente cluster. È possibile eseguire il backup di qualsiasi nodo di Publisher seguendo [Backup e ripristino](https://helpx.adobe.com/it/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Ripristino di un singolo nodo di pubblicazione {#recover-a-single-publisher-node}

1. Chiudi il nodo da recuperare e non esegui alcuna attività di pubblicazione fino a quando il nodo non è nuovamente attivo.
1. Ripristinare il nodo di pubblicazione utilizzando [Ripristino del backup](https://helpx.adobe.com/it/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Ripristinare un cluster {#recover-a-cluster}

1. Arrestare il cluster.
1. Ripristinare il nodo di pubblicazione utilizzando [Ripristino del backup](https://helpx.adobe.com/it/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. Avvia il nodo principale seguito dal nodo secondario del cluster di authoring.
