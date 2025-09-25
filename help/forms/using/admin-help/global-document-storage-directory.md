---
title: Directory di archiviazione globale dei documenti
description: La directory di archiviazione globale dei documenti (Global Document Storage, GDS) è una directory utilizzata per archiviare i file di lunga durata utilizzati all’interno di un processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '684'
ht-degree: 100%

---

# Directory di archiviazione globale dei documenti{#global-document-storage-directory}

La *directory di archiviazione documenti globale (GDS)* è una directory utilizzata per archiviare i file di lunga durata utilizzati all’interno di un processo. Questi file includono PDF, criteri e modelli di modulo. I file di lunga durata sono una parte fondamentale dello stato complessivo di molte distribuzioni di AEM Forms. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server Forms potrebbe diventare instabile. I documenti di input per le chiamate di processo asincrone sono archiviati anche nella directory GDS e devono essere disponibili per elaborare le richieste. È importante tenere presente l’affidabilità del file system che ospita la directory GDS. Utilizza un array ridondante di dischi indipendenti (RAID) o un’altra tecnologia appropriata per la qualità e il livello di servizio richiesti.

I file di lunga durata possono contenere informazioni utente riservate. Per accedere a queste informazioni potrebbero essere necessarie credenziali speciali utilizzando le API di AEM Forms o le interfacce utente. È importante che la directory GDS sia protetta correttamente tramite il sistema operativo. Solo l’account amministratore utilizzato per eseguire il server applicazioni deve disporre dell’accesso in lettura/scrittura alla directory GDS.

Oltre a selezionare una directory sicura e ad alta disponibilità per GDS, puoi anche scegliere di abilitare l’archiviazione dei documenti nel database. Tieni presente che anche se si utilizza il database di AEM Forms per l’archiviazione dei documenti, AEM Forms richiede ancora la directory GDS. Consulta [Opzioni di backup quando il database viene utilizzato per l’archiviazione dei documenti](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

I dati dell’applicazione AEM Forms risiedono nella directory GDS e nel database di AEM Forms. Nella tabella seguente vengono descritti i dati e le relative posizioni.

<table>
 <thead>
  <tr>
   <th><p>Dati di AEM Forms</p></th>
   <th><p>Database</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Dati dell’applicazione (utenti, ruoli, processi, criteri, endpoint, eventi e così via).</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Contenitori di servizi distribuiti</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Gestione documenti </p></td>
   <td><p>No</p></td>
   <td><p>Sì</p></td>
  </tr>
  <tr>
   <td><p>Archivio moduli</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Configurazione sistema</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Cartelle esaminate</p></td>
   <td><p>No</p></td>
   <td><p>Sì</p></td>
  </tr>
 </tbody>
</table>

## Configurazione della directory GDS {#configuring-the-gds-directory}

La posizione della directory GDS può essere configurata manualmente durante il processo di installazione di AEM Forms. Se l’impostazione relativa alla posizione rimane vuota durante l’installazione, per impostazione predefinita viene utilizzata una directory nell’installazione del server applicazioni nel modo seguente:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Modificare la posizione GDS predefinita {#change-the-default-gds-location}

Puoi modificare la posizione di GDS nella console di amministrazione al termine dell’installazione di AEM Forms. Riposiziona manualmente i dati per completare il processo.

>[!NOTE]
>
> * Esegui la migrazione dei dati nel modo seguente in modo da prevenire una perdita di dati.
> * Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.


1. Accedi alla console di amministrazione e fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
2. Nella casella Directory di archiviazione globale dei documenti, immetti il percorso completo della nuova directory GDS e quindi fai clic su OK.
3. Arresta immediatamente il server applicazioni.
4. Sposta tutti i file dalla vecchia directory GDS alla nuova posizione, mantenendo la struttura della directory interna.
5. Riavvia il server applicazioni.

## Informazioni sui file di distribuzione {#about-deployment-files}

AEM Forms è costituito da due tipi di file di distribuzione, i contenitori del servizio e i file EAR di Java 2 Platform, Enterprise Edition (J2EE). I file EAR sono costituiti da pacchetti di applicazioni J2EE standard che contengono le funzionalità di base di AEM Forms. I file EAR specifici del server applicazioni sono i seguenti:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

L’implementazione di AEM Forms comporta la distribuzione dei file EAR assemblati e dei file di supporto nel server applicazioni in cui intendi eseguire la soluzione AEM Forms. Se hai configurato e assemblato più moduli, quelli distribuibili vengono inclusi all’interno dei file EAR distribuibili. Per distribuire questi file, copiali nella directory *[appserver home]*\server\all\deploy directory.

I moduli e i file di archivio dei moduli di AEM sono inclusi in file JAR. Poiché non sono file di tipo J2EE, non vengono distribuiti nel server applicazioni. Vengono invece copiati nella directory GDS e nel database di AEM Forms viene memorizzato un riferimento alla loro posizione. Per questo motivo, la directory GDS deve essere condivisa tra tutti i nodi del cluster. Tutti i nodi devono avere accesso alla directory di archiviazione centrale per le DSC.

>[!NOTE]
>
>Prima di distribuire i contenitori di servizi, assicurati di aver creato e configurato la directory GDS. (Consulta [Configurazione della directory GDS](global-document-storage-directory.md#configuring-the-gds-directory))
