---
title: Impostazioni generali di AEM Forms
description: Scopri come configurare le impostazioni della pagina Configurazioni principali nella console di amministrazione che possono contribuire a migliorare le prestazioni del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 1b76b30d8db59e6ad98af1d29f17443442d5378e
workflow-type: ht
source-wordcount: '1774'
ht-degree: 100%

---

# Impostazioni generali di AEM Forms {#general-aem-forms-settings}

La pagina Configurazioni principali della console di amministrazione fornisce le impostazioni che possono contribuire a migliorare le prestazioni del sistema. Dopo aver configurato o aggiornato queste impostazioni, riavvia il server applicazioni.

>[!NOTE]
>
> * Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.
> * Si consiglia di utilizzare il comando “Ctrl + C” per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

Per informazioni sull’attivazione della modalità di backup sicuro, consulta [Attivazione e disattivazione della modalità di backup sicuro](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>I file nella directory temporanea e i documenti di lunga durata nella directory principale di archiviazione dei documenti globale (GDS) possono contenere informazioni utente riservate, ad esempio informazioni che richiedono credenziali speciali quando si accede utilizzando le API o le interfacce utente. È, quindi, importante che questa directory sia protetta correttamente utilizzando tutti i metodi disponibili per il sistema operativo. È consigliabile che solo l’account del sistema operativo utilizzato per eseguire il server applicazioni disponga dell’accesso in lettura e scrittura a questa directory.


1. Nella console di amministrazione, seleziona **[!UICONTROL Impostazioni > Impostazioni sistema core > Configurazioni]**.
1. Nella pagina Configurazioni core, modifica le opzioni in base alle esigenze e seleziona **[!UICONTROL OK]**. Per informazioni dettagliate sulle opzioni, consulta [Opzioni di configurazioni core](configure-general-aem-forms-settings.md#core-configurations-options).


## Opzioni di configurazioni core {#core-configurations-options}

**Posizione della directory temporanea** Percorso della directory in cui AEM Forms creerà i file temporanei del prodotto. Se il valore di questa impostazione è vuoto, la posizione per impostazione predefinita viene impostata sulla directory temporanea di sistema. Verifica che la directory temporanea sia una cartella scrivibile.

>[!NOTE]
>
>Verifica che la directory temporanea si trovi nel file system locale. AEM Forms non supporta una directory temporanea in una posizione remota.

**Directory principale di archiviazione documenti globale** *ndash; la directory principale di archiviazione documenti globale (GDS) viene utilizzata per i seguenti scopi:

* Archiviazione di documenti di lunga durata. I documenti di lunga durata non hanno un tempo di scadenza e persistono finché non vengono rimossi (ad esempio, i file PDF utilizzati in un processo di flusso di lavoro). I documenti di lunga durata sono una parte critica dello stato generale del sistema. Se alcuni o tutti questi documenti vengono persi o danneggiati, il server Forms potrebbe diventare instabile. Pertanto, è importante che questa directory sia memorizzata su un dispositivo RAID.
* Archiviazione dei documenti temporanei necessari durante l’elaborazione.

>[!NOTE]
>
>Puoi, inoltre, abilitare l’archiviazione dei documenti nel database di AEM Forms. Tuttavia, le prestazioni del sistema sono migliori quando utilizzi la GDS.

* Trasferimento di documenti tra nodi in un cluster. Se esegui AEM Forms in un ambiente cluster, questa directory deve essere accessibile da tutti i nodi del cluster.
* Ricezione dei parametri in entrata dalle chiamate API remote.

Se non specifichi una directory principale GDS, per impostazione predefinita la directory viene impostata su una directory del server applicazioni:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>La modifica del valore dell’impostazione della directory principale GDS deve essere eseguita con particolare attenzione. La directory GDS viene utilizzata per memorizzare sia i file di lunga durata utilizzati all’interno di un processo sia i componenti di prodotto critici di AEM Forms. La modifica della posizione della directory GDS rappresenta una modifica importante del sistema. Una configurazione errata della posizione della directory GDS renderà AEM Forms non funzionante e potrebbe richiedere una reinstallazione completa di AEM Forms. Se specifichi una nuova posizione per la directory GDS, è necessario arrestare il server applicazioni e migrare i dati prima di riavviare il server. L’amministratore di sistema deve spostare tutti i file dalla posizione precedente alla nuova posizione, mantenendo la struttura interna della directory.

>[!NOTE]
>
>Non specificare la stessa directory per la directory temporanea e la directory GDS.

Per ulteriori informazioni sulla directory GDS, consulta [Preparazione all’installazione di AEM Forms (server singolo)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Posizione della directory dei font del server Adobe** *ndash; digita il percorso della directory che contiene i font del server Adobe. Questi font vengono installati con AEM Forms. La posizione predefinita per questi font è la directory [aem-forms root]/fonts. Se questa directory non è accessibile, puoi copiare i font altrove e utilizzare questa impostazione per specificare la nuova posizione.

**Posizione della directory font clientela** *ndash; digita il percorso di una directory contenente font aggiuntivi che desideri utilizzare.

***nota **: i font vengono selezionati dalla cache dei font del sistema Windows ed è necessario riavviare il sistema per aggiornare la cache. Dopo aver specificato la directory dei font della clientela, assicurati di riavviare il sistema in cui è installato AEM Forms.*

**Posizione della directory dei font di sistema** *ndash; digita il percorso della directory dei font fornita dal sistema operativo. È possibile aggiungere più directory, separate da un punto e virgola **;**.

**Posizione del file di configurazione dei servizi dati** *ndash; specifica la posizione del file services-config.xml. Per impostazione predefinita, questo file è incorporato nel file adobe-core-appserver.ear e non è accessibile all’utente. Una copia del file services-config.xml predefinito si trova in [aem-formsroot]\sdk\misc\DataServices\Server-Configuration. Se hai modificato e spostato questo file, digita la nuova posizione in questo campo.

Il file di configurazione dei servizi dati consente di personalizzare le impostazioni dei servizi dati, ad esempio il tipo di autenticazione e l’output di debug.

Questa impostazione è vuota per impostazione predefinita.

**Dimensione massima (byte) predefinita del documento in linea** *ndash; numero massimo di byte conservati in memoria per il passaggio di documenti tra vari componenti di AEM Forms. Utilizza questa impostazione per ottimizzare le prestazioni. I documenti inferiori a questo numero vengono archiviati nella memoria e mantenuti nel database. I documenti che superano questo limite massimo vengono archiviati sul disco rigido.

Questa impostazione è obbligatoria. Il valore predefinito è 65536 byte.

**Timeout eliminazione documento predefinito (secondi)** *ndash; la quantità massima di tempo, in secondi, durante la quale un documento passato tra vari componenti di AEM Form viene considerato attivo. Trascorso questo tempo, i file utilizzati per memorizzare il documento saranno rimossi. Utilizza questa impostazione per controllare l’utilizzo dello spazio su disco.

Questa impostazione è obbligatoria. Il valore predefinito è 600 secondi.

**Intervallo di sweep del documento (secondi)** *ndash; la quantità di tempo, in secondi, tra i tentativi di eliminare i file che non sono più necessari e sono stati utilizzati per passare i dati del documento tra i servizi.

Questa impostazione è obbligatoria. Il valore predefinito è 30 secondi.

**Abilita FIPS** *ndash; seleziona questa opzione per abilitare la modalità FIPS. Lo standard FIPS (Federal Information Processing Standard) 140-2 è uno standard di crittografia definito dal governo degli Stati Uniti. Quando viene eseguito in modalità FIPS, AEM Forms limita la protezione dei dati agli algoritmi approvati da FIPS 140-2 utilizzando il modulo di crittografia RSA BSAFE Crypto-C 2.1.

La modalità FIPS non supporta gli algoritmi di crittografia utilizzati nelle versioni di Adobe Acrobat® precedenti alla 7.0. Se la modalità FIPS è attivata e si utilizza il servizio crittografia per crittografare il PDF utilizzando una password con un livello di compatibilità impostato su Acrobat 5, il tentativo di crittografia non riuscirà e verrà restituito un errore.

In generale, quando FIPS è abilitato, il servizio Assembler non applica la crittografia della password a nessun documento. Se si tenta di eseguire questa operazione, viene generata una FIPSModeException che indica che “la crittografia della password non è consentita in modalità FIPS.” Inoltre, l’elemento PDFsFromBookmarks nella descrizione del documento XML (DDX) non è supportato in modalità FIPS quando il documento di base è crittografato con password.

>[!NOTE]
>
>Il software AEM Forms non convalida il codice per garantire la compatibilità FIPS. Fornisce una modalità operativa FIPS in modo che gli algoritmi approvati da FIPS vengano utilizzati per i servizi di crittografia dalle librerie approvate da FIPS (RSA).

**Abilita WSDL** *ndash; seleziona questa opzione per abilitare la generazione del linguaggio WSDL (Web Service Definition Language) per tutti i servizi che fanno parte di AEM Forms.

Abilita questa opzione negli ambienti di sviluppo, in cui gli sviluppatori utilizzano la generazione WSDL per creare le applicazioni client. Puoi scegliere di disabilitare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

**Abilita l’archiviazione dei documenti nel database** *ndash; seleziona questa opzione per memorizzare i documenti di lunga durata nel database di AEM Forms. L’attivazione di questa opzione non elimina la necessità di una directory GDS. Tuttavia, la scelta di questa opzione semplifica i backup di AEM Forms. Se utilizzi solo il GDS, un backup comporta il posizionamento del sistema dei moduli FormsAEM di AEM e il completamento dei backup del database e del GDS. Se selezioni l’opzione del database, il backup comporta il completamento del backup del database per una nuova installazione o il completamento del backup del database e del backup unico del GDS per un aggiornamento. Potrebbe essere necessaria una gestione aggiuntiva del database per eliminare processi e dati, rispetto a una configurazione che utilizza solo il GDS. Quando il database viene utilizzato per l’archiviazione dei documenti, consulta Opzioni di backup.

**Abilita il monitoraggio delle chiamate DSC** *ndash; quando questa opzione è selezionata, AEM Forms tiene traccia delle statistiche di chiamata, ad esempio il numero di chiamate, il tempo impiegato per la chiamata e il numero di errori nelle chiamate. Queste informazioni vengono memorizzate in un bean JMX, per consentirti di utilizzare Java™ JConsole o un software di terze parti per esaminare le statistiche. Se non desideri visualizzare queste statistiche, deseleziona questa opzione per migliorare le prestazioni di AEM Forms.

**Abilita RDS** *ndash; se selezioni questa opzione, in AEM Forms verrà abilitato il servlet Remote Development Services (RDS). Quando questa opzione è abilitata, gli strumenti lato client possono interagire con Data Services per eseguire operazioni quali la distribuzione o l’annullamento della distribuzione di modelli per la creazione di destinazioni ed endpoint o per il rilevamento dei modelli distribuiti negli endpoint. Per impostazione predefinita, questa opzione non è selezionata.

**Consenti richieste RDS non sicure** *ndash; se questa opzione è selezionata, non è necessario che le richieste RDS utilizzino https. Per impostazione predefinita, questa opzione non è selezionata e tutte le comunicazioni con Data Services devono essere richieste https.

**Consenti il caricamento di documenti non protetti da applicazioniFlex** *ndash; Per caricare documenti da applicazioni Adobe Flex® in AEM Forms, il servlet di caricamento file utilizzato richiede che gli utenti siano autenticati e autorizzati. All’utente deve essere assegnato il ruolo di utente dell’applicazione Caricamento documento o un altro ruolo che includa l’autorizzazione al caricamento del documento. In questo modo si evita che utenti non autorizzati carichino documenti sul server AEM Forms. Seleziona questa opzione per disattivare questa funzionalità di protezione in un ambiente di sviluppo o per garantire la compatibilità con le versioni precedenti di AEM Forms. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, consulta “Richiamare AEM Forms utilizzando il servizio di comunicazione remota di AEM Forms” in Programmare con AEM Forms.

**Consenti il caricamento di documenti non protetti dalle applicazioni Java SDK** *ndash; I caricamenti HTTP DocumentManager devono essere protetti. Per impostazione predefinita, i caricamenti HTTP richiedono che gli utenti siano autenticati e autorizzati prima di poter caricare documenti. All’utente deve essere assegnato il ruolo Utente dei servizi o un altro ruolo contenente l’autorizzazione a richiamare il servizio. In questo modo si evita che utenti non autorizzati possano caricare documenti sul server Forms. Seleziona questa opzione se vuoi disattivare questa funzionalità di protezione in un ambiente di sviluppo, per garantire la compatibilità con le versioni precedenti di AEM Forms o in base alla configurazione del firewall. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, consulta “Richiamare AEM Forms utilizzando l’API Java” in Programmare con AEM Forms.
