---
title: Directory di archiviazione documenti globali
seo-title: Directory di archiviazione documenti globali
description: La directory GDS (Global document storage) è una directory utilizzata per memorizzare i file longevi utilizzati all'interno di un processo.
seo-description: La directory GDS (Global document storage) è una directory utilizzata per memorizzare i file longevi utilizzati all'interno di un processo.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 1%

---


# Directory di archiviazione documenti globali{#global-document-storage-directory}

La directory *Global document storage (GDS)* è una directory utilizzata per memorizzare i file longevi utilizzati in un processo. Tali file includono PDF, criteri e modelli di modulo. I file di lunga durata rappresentano una parte fondamentale dello stato generale di molte distribuzioni di moduli AEM. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server dei moduli potrebbe diventare instabile. I documenti di input per le chiamate asincrone dei processi vengono inoltre memorizzati nella directory GDS e devono essere disponibili per l’elaborazione delle richieste. È importante considerare l&#39;affidabilità del file system che ospita la directory GDS. Utilizzate un array ridondante di dischi indipendenti (RAID) o altre tecnologie, in base alla qualità e al livello di servizio richiesti.

I file di lunga durata possono contenere informazioni utente sensibili. Queste informazioni possono richiedere credenziali speciali quando vi si accede utilizzando le API dei moduli AEM o le interfacce utente. È importante che la directory GDS sia adeguatamente protetta attraverso il sistema operativo. Solo l&#39;account amministratore utilizzato per eseguire il server applicazione deve disporre dell&#39;accesso in lettura/scrittura alla directory GDS.

Oltre a selezionare una directory sicura e a disponibilità elevata per GDS, potete anche scegliere di abilitare l&#39;archiviazione dei documenti nel database. Tenere presente che anche utilizzando il database dei moduli AEM per l&#39;archiviazione dei documenti, AEM moduli richiede ancora la directory GDS. (Vedere [Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM i dati dell&#39;applicazione dei moduli risiedono nella directory GDS e nel database dei moduli AEM. Nella tabella seguente sono descritti i dati e le relative posizioni.

<table>
 <thead>
  <tr>
   <th><p>Dati AEM moduli</p></th>
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
   <td><p>Repository Forms</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Configurazione del sistema</p></td>
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

La posizione della directory GDS può essere configurata manualmente durante il processo di installazione dei moduli AEM. Se l&#39;impostazione della posizione rimane vuota durante l&#39;installazione, per impostazione predefinita la posizione corrisponde a una directory nell&#39;installazione del server applicazione, come segue:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Modificare il percorso GDS predefinito {#change-the-default-gds-location}

Al termine dell&#39;installazione dei moduli di AEM, è possibile modificare la posizione di GDS nella console di amministrazione. Per completare il processo, è necessario riposizionare manualmente i dati.

>[!NOTE]
>
>Esegui la migrazione dei dati nel modo seguente o si verificherà una perdita di dati.

1. Accedete alla console di amministrazione e fate clic su Impostazioni > Impostazioni di sistema principali > Configurazioni.
1. Nella casella Directory archivio documenti globale immettere il percorso completo della nuova directory GDS, quindi fare clic su OK.
1. Chiudere immediatamente il server dell&#39;applicazione.
1. Spostate tutti i file dalla vecchia directory GDS alla nuova posizione, mantenendo la struttura della directory interna.
1. Riavviate il server applicazione.

## Informazioni sui file di distribuzione {#about-deployment-files}

AEM moduli è costituito da due tipi di file di distribuzione, i contenitori del servizio e i file EAR della piattaforma Java 2, Enterprise Edition (J2EE). I file EAR sono costituiti da pacchetti di applicazioni J2EE standard che contengono le funzionalità di base dei moduli AEM. I file EAR specifici del server dell’applicazione sono i seguenti:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

L&#39;implementazione AEM moduli prevede la distribuzione dei file EAR assemblati e dei file di supporto al server applicazione in cui si prevede di eseguire la soluzione di moduli AEM. Se avete configurato e assemblato più moduli, i moduli distribuibili vengono assemblati all&#39;interno dei file EAR distribuibili. Per distribuire questi file, copiateli nella *[home]*\server\all\deploy directory.

I moduli e AEM file di archivio dei moduli vengono assemblati in file JAR. Poiché non sono file di tipo J2EE, non vengono distribuiti nel server applicazioni. Vengono invece copiati nella directory GDS e nel database dei moduli AEM viene memorizzato un riferimento alla relativa posizione. Per questo motivo, la directory GDS deve essere condivisa tra tutti i nodi del cluster. Tutti i nodi devono avere accesso alla directory di memorizzazione centrale per i DSC.

>[!NOTE]
>
>Prima di distribuire i contenitori di servizi, accertatevi di aver creato e configurato la directory GDS. (Vedere [Configurazione della directory GDS](global-document-storage-directory.md#configuring-the-gds-directory))

