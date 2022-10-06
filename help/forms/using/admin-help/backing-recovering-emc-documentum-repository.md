---
title: Backup e ripristino del repository EMC Documentum
seo-title: Backing up and recovering the EMC Documentum repository
description: Questo documento descrive le attività necessarie per eseguire il backup e il ripristino del repository EMC Documentum configurato per l'ambiente dei moduli AEM.
seo-description: This document describes the tasks required to back up and recover the EMC Documentum repository configured for your AEM forms environment.
uuid: ab3b1fb1-25b3-4c95-801f-82d4b58f05ff
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f146202f-25f1-46a0-9943-c483f5f09f9f
exl-id: bc21659f-88d6-4dff-8baf-12746e1b3ed9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Backup e ripristino del repository EMC Documentum {#backing-up-and-recovering-the-emc-documentum-repository}

Questa sezione descrive le attività necessarie per eseguire il backup e il ripristino del repository EMC Documentum configurato per l&#39;ambiente dei moduli AEM.

>[!NOTE]
>
>Queste istruzioni presuppongono l&#39;installazione e la configurazione dei moduli AEM con i connettori per ECM e EMC Documentum Content Server in base alle esigenze.

Per i processi di backup e ripristino sono disponibili due attività principali:

* Eseguire il backup (o il ripristino) dell’ambiente dei moduli AEM.
* Backup (o ripristino) di EMC Documentum Content Server.

>[!NOTE]
>
>Eseguire il backup dei dati dei moduli AEM prima di eseguire il backup del sistema EMC Documentum e successivamente ripristinare il sistema EMC Documentum prima di ripristinare l&#39;ambiente dei moduli AEM.

## Requisiti software {#software-requirements}

Per eseguire le attività di backup necessarie su EMC Documentum Content Server, acquistare un&#39;utility di terze parti appropriata, come EMC NetWorker da EMC o CYA SmartRecovery per EMC Documentum da CYA. Le istruzioni seguenti descrivono i passaggi necessari per l&#39;utilizzo del modulo EMC NetWorker versione 7.2.2.

Sono necessari i seguenti moduli EMC NetWorker:

* Modulo NetWorker
* Configurazione guidata NetWorker
* Configurazione guidata dispositivo NetWorker
* Modulo NetWorker per il tipo di database utilizzato da Content Server
* Modulo NetWorker per Documentum

## Preparazione di EMC Document Content Server per il backup e il ripristino {#preparing-the-emc-document-content-server-for-backup-and-recovery}

Questa sezione descrive l&#39;installazione e la configurazione del software EMC NetWorker sul server dei contenuti.

**Preparazione del server EMC Documentum per il backup**

1. In EMC Documentum Content Server, installare i moduli EMC NetWorker, accettando tutte le impostazioni predefinite.

   Durante i processi di installazione, viene richiesto di immettere il nome server del computer Content Server come *Nome server NetWorker*. Quando si installa il modulo EMC NetWorker per il database, scegliere un&#39;installazione &quot;Completa&quot;.

1. Utilizzando il contenuto di esempio riportato di seguito, crea un file di configurazione denominato *nsrnmd_win.cfg* e salvarlo in un percorso accessibile su Content Server. Questo file verrà chiamato dai comandi di backup e ripristino.

   Il testo seguente contiene caratteri di formattazione per le interruzioni di riga. Se si copia il testo in una posizione esterna al documento, copiare una parte alla volta e rimuovere i caratteri di formattazione quando si incolla il testo nella nuova posizione.

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # Please refer to the user Guides for details on all parameters, including
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

   Mantenere il campo password del file di configurazione `NMDDE_DM_PASSWD` vuoto. Imposta la password nel passaggio successivo.

1. Imposta la password del file di configurazione come segue:

   * Apri un prompt dei comandi e cambia in `[NetWorker_root]\Legato\nsr\bin`.
   * Esegui il comando seguente: `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. Crea i file batch eseguibili (.bat) utilizzati per il backup del database. (consultare la documentazione di NetWorker.) Imposta i dettagli nei file batch in base all&#39;installazione.

   * Backup completo del database (nsrnmddbf.bat):

      `NetWorker_database_module_root` `-s`*&lt;networker_server_name>* `-U``[username]` `-P`*[password ]*`-l full`*&lt;database_name>*

   * Backup del database incrementale (nsrnmddbi.bat):

      `[NetWorker_database_module_root]` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * Backup del registro di database (nsrnmddbl.bat):

      `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

      Dove:

      `[NetWorker_database_module_root]` è la directory di installazione del modulo NetWorker. Ad esempio, la directory di installazione predefinita per il modulo NetWorker per SQL Server è C:\Program Files\Legato\nsr\bin\nsrsqlsv.

      `NetWorker_Server_Name` è il server in cui è installato NetWorker.

      `username` &amp; `password` sono il nome utente e la password dell&#39;utente amministratore del database.

      `database_name` è il nome del database di cui eseguire il backup.

**Creare un dispositivo di backup**

1. Crea una nuova directory sul server EMC Documentum e condividi la cartella assegnando diritti completi a tutti gli utenti.
1. Avviare EMC NetWorker Administrator e fare clic su Media Management > Dispositivi.
1. Fare clic con il pulsante destro del mouse su Dispositivi e selezionare Crea.
1. Immetti i seguenti valori e fai clic su OK:

   **Nome:** Percorso completo della directory condivisa

   **Tipo di supporto:** `File`

1. Fare clic con il pulsante destro del mouse sul nuovo dispositivo e selezionare Operazioni.
1. Fare clic su Etichetta, immettere un nome, fare clic su OK e quindi su Montaggio.

Viene aggiunto un dispositivo al quale verranno salvati i file di backup. È possibile aggiungere più dispositivi di formati diversi.

## Backup di EMC Documentum Content Server {#back-up-the-emc-documentum-content-server}

Esegui le seguenti operazioni dopo aver completato un backup completo dei dati dei moduli AEM. (Vedi [Backup dei dati dei moduli AEM](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data).)

>[!NOTE]
>
>Gli script di comando richiedono il percorso completo del file nsrnmd_win.cfg creato in [Preparazione di EMC Document Content Server per il backup e il ripristino](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Apri un prompt dei comandi e cambia in `[NetWorker_root]\Legato\nsr\bin`.
1. Esegui il comando seguente:

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## Ripristino di EMC Documentum Content Server {#restore-the-emc-documentum-content-server}

Eseguire le operazioni seguenti prima di ripristinare i dati dei moduli AEM. (Vedi [Ripristino dei dati dei moduli AEM](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data).)

>[!NOTE]
>
>Gli script di comando richiedono il percorso completo del file nsrnmd_win.cfg creato in [Preparazione di EMC Document Content Server per il backup e il ripristino](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Arrestare il servizio Docbase che si sta ripristinando.
1. Avviare l&#39;utility NetWorker User per il modulo di database (ad esempio, *Utente NetWorker per SQL Server*).
1. Fare clic sullo strumento Ripristina, quindi selezionare Normale.
1. Sul lato sinistro dello schermo, selezionare il database del Docbase e fare clic sul pulsante Start sulla barra degli strumenti.
1. Quando il database viene ripristinato, riavviare il servizio Docbase.
1. Apri un prompt dei comandi e cambia in *[NetWorker_root]*\Legato\nsr\bin
1. Esegui il comando seguente:

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
