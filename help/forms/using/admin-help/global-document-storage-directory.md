---
title: Directory di archiviazione dei documenti globali
seo-title: Global document storage directory
description: La directory GDS (Global Document Storage) è una directory utilizzata per memorizzare file longevi utilizzati all’interno di un processo.
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# Directory di archiviazione dei documenti globali{#global-document-storage-directory}

La *archiviazione globale dei documenti (GDS)* directory è una directory utilizzata per memorizzare file longevi utilizzati all’interno di un processo. Tali file includono PDF, criteri e modelli di modulo. I file longevi sono una parte critica dello stato generale di molte distribuzioni di moduli AEM. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server dei moduli potrebbe diventare instabile. I documenti di input per le chiamate asincrone dei processi sono anche memorizzati nella directory GDS e devono essere disponibili per elaborare le richieste. È importante considerare l&#39;affidabilità del file system che ospita la directory GDS. Utilizzare un array ridondante di dischi indipendenti (RAID) o altra tecnologia appropriata per la qualità e il livello di servizio richiesti.

I file di lunga durata possono contenere informazioni utente sensibili. Queste informazioni possono richiedere credenziali speciali quando vi si accede utilizzando le API o le interfacce utente dei moduli AEM. È importante che la directory GDS sia adeguatamente protetta attraverso il sistema operativo. Solo l&#39;account amministratore utilizzato per eseguire l&#39;application server deve avere accesso in lettura/scrittura alla directory GDS.

Oltre a selezionare una directory sicura e altamente disponibile per GDS, puoi anche scegliere di abilitare l&#39;archiviazione dei documenti nel database. Tieni presente che anche utilizzando il database dei moduli AEM per l’archiviazione dei documenti, AEM moduli richiede ancora la directory GDS. (Vedi [Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

I dati dell’applicazione AEM forms risiedono nella directory GDS e nel database dei moduli AEM. Nella tabella seguente sono descritti i dati e le relative posizioni.

<table>
 <thead>
  <tr>
   <th><p>Dati dei moduli AEM</p></th>
   <th><p>Database</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Dati applicazione (utenti, ruoli, processi, criteri, endpoint, eventi e così via)</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Contenitori di servizi distribuiti</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Document Manager </p></td>
   <td><p>No</p></td>
   <td><p>Sì</p></td>
  </tr>
  <tr>
   <td><p>Archivio Forms</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Configurazione del sistema</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Cartelle controllate</p></td>
   <td><p>No</p></td>
   <td><p>Sì</p></td>
  </tr>
 </tbody>
</table>

## Configurazione della directory GDS {#configuring-the-gds-directory}

La posizione della directory GDS può essere configurata manualmente durante il processo di installazione dei moduli AEM. Se l&#39;impostazione di posizione rimane vuota durante l&#39;installazione, il percorso viene impostato automaticamente su una directory nell&#39;installazione dell&#39;application server come segue:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Modificare la posizione GDS predefinita {#change-the-default-gds-location}

Al termine dell’installazione dei moduli di AEM, è possibile modificare la posizione GDS nella console di amministrazione. Per completare il processo, devi spostare manualmente i dati.

>[!NOTE]
>
>Esegui la migrazione dei dati nel modo seguente o si verificherà una perdita di dati.

1. Accedi alla console di amministrazione e fai clic su Impostazioni > Impostazioni sistema di base > Configurazioni.
1. Nella casella Directory di archiviazione globale dei documenti immettere il percorso completo della nuova directory GDS, quindi fare clic su OK.
1. Spegnere immediatamente l&#39;application server.
1. Spostare tutti i file dalla vecchia directory GDS alla nuova posizione, mantenendo la struttura della directory interna.
1. Riavvia il server applicazioni.

## Informazioni sui file di distribuzione {#about-deployment-files}

I moduli AEM sono costituiti da due tipi di file di distribuzione, i contenitori di servizio e i file EAR Java 2 Platform, Enterprise Edition (J2EE). I file EAR sono costituiti da bundle di applicazioni J2EE standard che contengono la funzionalità di base dei moduli AEM. I file EAR specifici del server dell&#39;applicazione sono i seguenti:

* adobe-core-*[appserver]* orecchio
* adobe-core-*[appserver]*-*[OS]* orecchio

L’implementazione di AEM moduli comporta la distribuzione dei file EAR assemblati e dei file di supporto al server dell’applicazione in cui si prevede di eseguire la soluzione di moduli AEM. Se hai configurato e assemblato più moduli, i moduli distribuibili vengono assemblati all’interno dei file EAR distribuibili. Per distribuire questi file, copiali nel *[home dell&#39;appserver]*\server\all\deploy directory.

I file di archivio moduli e moduli AEM vengono assemblati in file JAR. Poiché non sono file di tipo J2EE, non vengono distribuiti nel server applicazioni. Vengono invece copiati nella directory GDS e un riferimento alla relativa posizione viene memorizzato nel database dei moduli AEM. Per questo motivo, la directory GDS deve essere condivisa tra tutti i nodi del cluster. Tutti i nodi devono avere accesso alla directory di archiviazione centrale per i DSC.

>[!NOTE]
>
>Prima di distribuire i contenitori del servizio, assicurati di aver creato e configurato la directory GDS. (Vedi [Configurazione della directory GDS](global-document-storage-directory.md#configuring-the-gds-directory))
