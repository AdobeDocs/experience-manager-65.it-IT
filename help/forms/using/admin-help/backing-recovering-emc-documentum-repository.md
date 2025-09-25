---
title: Backup e ripristino dell’archivio Documentum di EMC
description: In questo documento vengono descritte le attività necessarie per eseguire il backup e il ripristino dell’archivio Documentum di EMC configurato per l’ambiente AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bc21659f-88d6-4dff-8baf-12746e1b3ed9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '790'
ht-degree: 100%

---

# Backup e ripristino dell’archivio Documentum di EMC {#backing-up-and-recovering-the-emc-documentum-repository}

In questa sezione vengono descritte le attività necessarie per eseguire il backup e il ripristino dell’archivio Documentum di EMC configurato per l’ambiente AEM Forms.

>[!NOTE]
>
>Queste istruzioni presuppongono che AEM Forms con connettori di ECM e il server di gestione dei contenuti EMC Documentum siano installati e configurati in base alle esigenze.

Per i processi di backup e ripristino sono disponibili due attività principali:

* Backup (o ripristino) dell’ambiente AEM Forms.
* Backup (o ripristino) del server di gestione dei contenuti EMC Documentum.

>[!NOTE]
>
>Esegui il backup dei dati di AEM Forms prima di eseguire il backup del sistema EMC Documentum, quindi ripristina il sistema EMC Documentum prima di ripristinare l’ambiente AEM Forms.

## Requisiti software {#software-requirements}

Per eseguire le attività di backup necessarie sul server di gestione dei contenuti EMC Documentum, acquista un’utility di terze parti appropriata, ad esempio EMC NetWorker di EMC o CYA SmartRecovery per EMC Documentum di CYA. Le istruzioni seguenti descrivono i passaggi per l’utilizzo del modulo EMC NetWorker versione 7.2.2.

Sono necessari i seguenti moduli EMC NetWorker:

* Modulo NetWorker
* Procedura guidata per la configurazione di NetWorker
* Procedura guidata per la configurazione del dispositivo NetWorker
* Modulo NetWorker per il tipo di database utilizzato dal server di gestione dei contenuti
* Modulo NetWorker per Documentum

## Preparazione del server di gestione dei contenuti EMC Document per il backup e il ripristino {#preparing-the-emc-document-content-server-for-backup-and-recovery}

Questa sezione descrive l’installazione e la configurazione del software EMC NetWorker sul server di gestione dei contenuti.

**Preparare il server EMC Documentum per il backup**

1. Sul server di gestione dei contenuti EMC Documentum, installa i moduli EMC NetWorker, accettando tutte le impostazioni predefinite.

   Durante i processi di installazione, viene richiesto di immettere il nome del server del computer server di gestione dei contenuti come *Nome server NetWorker*. Quando installi il modulo EMC NetWorker per il database, scegli un’installazione “completa”.

1. Utilizzando il contenuto di esempio seguente, crea un file di configurazione denominato *nsrnmd_win.cfg* e salvalo in una posizione accessibile sul server di gestione dei contenuti. Il file verrà richiamato dai comandi di backup e ripristino.

   Il testo seguente contiene caratteri di formattazione per le interruzioni di riga. Se copi il testo in una posizione esterna al documento, copia una parte alla volta e rimuovi i caratteri di formattazione quando incolli il testo nella nuova posizione.

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # See the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   Mantieni vuoto il campo password `NMDDE_DM_PASSWD` del file di configurazione. La password verrà impostata nel passaggio successivo.

1. Imposta la password del file di configurazione come segue:

   * Apri un prompt dei comandi e passa a `[NetWorker_root]\Legato\nsr\bin`.
   * Esegui il comando seguente: `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. Crea i file batch eseguibili (.bat) utilizzati per eseguire il backup del database. Consulta la documentazione di NetWorker. Imposta i dettagli nei file batch in base all’installazione.

   * Backup completo del database (nsrnmddbf.bat):

     `NetWorker_database_module_root` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P`*[password ]*`-l full`*&lt;database_name>*

   * Backup incrementale del database (nsrnmddbi.bat):

     `[NetWorker_database_module_root]` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * Backup del registro del database (nsrnmddbl.bat):

     `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

     Dove:

     `[NetWorker_database_module_root]` è la directory di installazione del modulo NetWorker. Ad esempio, la directory di installazione predefinita per il modulo NetWorker per SQL Server è C:\Program Files\Legato\nsr\bin\nsrsqlsv.

     `NetWorker_Server_Name` è il server su cui è installato NetWorker.

     `username` e `password` sono il nome utente e la password dell’utente amministratore del database.

     `database_name` è il nome del database di cui si esegue il backup.

**Crea un dispositivo di backup**

1. Crea una directory sul server EMC Documentum e condividi la cartella concedendo i diritti completi a tutti gli utenti.
1. Avvia Amministratore EMC NetWorker e fai clic su Gestione contenuti multimediali > Dispositivi.
1. Fai clic con il pulsante destro del mouse su Dispositivi e seleziona Crea.
1. Immetti i seguenti valori e fai clic su OK:

   **Nome:** percorso completo della directory condivisa

   **Tipo di media:** `File`

1. Fai clic con il pulsante destro del mouse sul nuovo dispositivo e seleziona Operazioni.
1. Fai clic su Etichetta, immetti un nome, fai clic su OK, quindi su Monta.

Viene aggiunto un dispositivo in cui verranno salvati i file sottoposti a backup. Puoi aggiungere più dispositivi di formati diversi.

## Backup del server di gestione dei contenuti EMC Documentum {#back-up-the-emc-documentum-content-server}

Dopo aver terminato un backup completo dei dati dei moduli AEM, esegui le attività seguenti (consulta [Eseguire il backup dei dati dei moduli AEM](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data)).

>[!NOTE]
>
>Gli script di comando richiedono il percorso completo del file nsrnmd_win.cfg creato in [Preparazione del server di gestione dei contenuti EMC Documentum per il backup e il ripristino](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Apri un prompt dei comandi e passa a `[NetWorker_root]\Legato\nsr\bin`.
1. Esegui il comando seguente:

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## Ripristino del server di gestione dei contenuti EMC Documentum {#restore-the-emc-documentum-content-server}

Prima di ripristinare i dati dei moduli di AEM, esegui le operazioni seguenti (consulta [Ripristino dei dati di AEM Forms](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data)).

>[!NOTE]
>
>Gli script di comando richiedono il percorso completo del file nsrnmd_win.cfg creato in [Preparazione del server di gestione dei contenuti EMC Documentum per il backup e il ripristino](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Interrompi il servizio Docbase che stai ripristinando.
1. Avvia l’utilità Utente NetWorker per il modulo di database (ad esempio *Utente NetWorker per SQL Server*).
1. Fai clic sullo strumento Ripristina, quindi seleziona Normale.
1. Nella parte sinistra della schermata seleziona il database di Docbase e fai clic sul pulsante Avvia sulla barra degli strumenti.
1. Una volta ripristinato il database, riavvia il servizio Docbase.
1. Apri un prompt dei comandi e passa a *[NetWorker_root]*\Legato\nsr\bin
1. Esegui il comando seguente:

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
