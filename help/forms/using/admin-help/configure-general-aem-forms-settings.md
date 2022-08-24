---
title: Impostazioni generali di AEM Forms
seo-title: General AEM Forms settings
description: Scopri come configurare le impostazioni della pagina Configurazioni principali nella console di amministrazione per migliorare le prestazioni del sistema.
seo-description: Learn to configure the Core Configurations page settings in administration console that can help improve system performance.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 1%

---

# Impostazioni generali di AEM Forms {#general-aem-forms-settings}

La pagina Configurazioni di base nella console di amministrazione fornisce impostazioni che possono contribuire a migliorare le prestazioni del sistema. Dopo aver configurato o aggiornato queste impostazioni, riavvia l&#39;application server.

Per informazioni sull&#39;abilitazione della modalità di backup sicuro, vedi [Abilitazione e disabilitazione della modalità di backup sicuro](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>I file nella directory temporanea e i documenti a lungo termine nella directory principale GDS (Global Document Storage) possono contenere informazioni utente sensibili, ad esempio informazioni che richiedono credenziali speciali quando vi si accede utilizzando le API o le interfacce utente. Pertanto, è importante che questa directory sia adeguatamente protetta utilizzando tutti i metodi disponibili per il sistema operativo. Si consiglia che solo l&#39;account del sistema operativo utilizzato per eseguire il server applicazioni abbia accesso in lettura e scrittura a questa directory.


1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Impostazioni del sistema di base > Configurazioni]**.
1. Nella pagina Configurazioni principali, modifica le opzioni in base alle esigenze e fai clic su **[!UICONTROL OK]**. Per informazioni dettagliate sulle opzioni, vedi [Opzioni delle configurazioni core](configure-general-aem-forms-settings.md#core-configurations-options).


## Opzioni delle configurazioni core {#core-configurations-options}

**Posizione della directory temporanea** Percorso della directory in cui AEM moduli creeranno file temporanei di prodotto. Se il valore di questa impostazione è vuoto, il percorso viene impostato automaticamente sulla directory temporanea del sistema. Assicurati che la directory temporanea sia una cartella scrivibile.

>[!NOTE]
>
>Verificare che la directory temporanea si trovi nel file system locale. I moduli AEM non supportano una directory temporanea in un percorso remoto.

**Directory principale di archiviazione documenti globale** La directory principale GDS (Global Document Storage) viene utilizzata per i seguenti scopi:

* Archiviazione di documenti di lunga durata. I documenti di lunga durata non hanno un tempo di scadenza e persistono finché non vengono rimossi (ad esempio, i file PDF utilizzati all’interno di un processo di flusso di lavoro). I documenti di lunga durata costituiscono una parte critica dello stato generale del sistema. Se alcuni o tutti questi documenti sono persi o danneggiati, il server dei moduli potrebbe diventare instabile. Pertanto, è importante che questa directory sia memorizzata su un dispositivo RAID.
* Memorizzazione dei documenti temporanei necessari durante l&#39;elaborazione.

>[!NOTE]
>
>È inoltre possibile abilitare l’archiviazione dei documenti nel database dei moduli AEM. Tuttavia, le prestazioni del sistema sono migliori quando si utilizza il GDS.

* Trasferimento di documenti tra nodi in un cluster. Se si eseguono moduli AEM in un ambiente cluster, questa directory deve essere accessibile da tutti i nodi all&#39;interno del cluster.
* Ricezione dei parametri in arrivo dalle chiamate API remote.

Se non si specifica una directory radice GDS, la directory viene impostata automaticamente su una directory del server dell&#39;applicazione:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>La modifica del valore dell&#39;impostazione della directory principale GDS deve essere effettuata con particolare attenzione. La directory GDS viene utilizzata per memorizzare sia i file di lunga durata utilizzati all’interno di un processo che i componenti di prodotto dei moduli di AEM critici. Cambiare la posizione della directory GDS è un cambiamento importante del sistema. La configurazione errata della posizione della directory GDS renderà i moduli AEM non operativi e potrebbe richiedere una reinstallazione completa dei moduli AEM. Se si specifica una nuova posizione per la directory GDS, è necessario arrestare l&#39;application server e eseguire la migrazione dei dati prima del riavvio del server. L&#39;amministratore di sistema deve spostare tutti i file dalla posizione precedente alla nuova posizione, ma mantenere la struttura della directory interna.

>[!NOTE]
>
>Non specificare la stessa directory per la directory temporanea e la directory GDS.

Per ulteriori informazioni sulla directory GDS, vedi [Preparazione all’installazione di moduli AEM (server singolo)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Posizione della directory Font del server Adobe** Digitare il percorso della directory contenente i font del server di Adobe. Questi font vengono installati con AEM moduli. La posizione predefinita per questi font è la [root di aem forms]/fonts directory. Se questa directory non è accessibile, è possibile copiare i font altrove e utilizzare questa impostazione per specificare la nuova posizione.

**Posizione della directory Font del cliente** Digitare il percorso di una directory contenente i font aggiuntivi che si desidera utilizzare.

***nota **: I font vengono selezionati dalla cache dei font di sistema di Windows ed è necessario un riavvio del sistema per aggiornare la cache. Dopo aver specificato la directory dei font per il cliente, assicurarsi di riavviare il sistema in cui sono installati AEM moduli.*

**Posizione della directory dei font di sistema** Digitare il percorso della directory dei font fornita dal sistema operativo in uso. È possibile aggiungere più directory, separate da punto e virgola **;**.

**Posizione del file di configurazione di Data Services** Specifica il percorso del file services-config.xml. Per impostazione predefinita, questo file è incorporato nel file adobe-core-appserver.ear e non è accessibile all’utente. Una copia del file services-config.xml predefinito si trova in [root di aem forms]\sdk\misc\DataServices\Server-Configuration. Se il file è stato modificato e spostato, digitare la nuova posizione in questo campo.

Il file di configurazione di Data Services consente la personalizzazione delle impostazioni di Data Services, ad esempio il tipo di autenticazione e l&#39;output di debug.

Per impostazione predefinita, questa impostazione è vuota.

**Dimensioni massime in linea del documento predefinite (byte)** Il numero massimo di byte conservati in memoria quando si trasmettono documenti tra i vari componenti AEM dei moduli. Utilizzare questa impostazione per ottimizzare le prestazioni. I documenti di dimensioni inferiori a questo numero vengono memorizzati in memoria e memorizzati nel database. I documenti che superano questo limite massimo sono memorizzati sul disco rigido.

Questa impostazione è obbligatoria. Il valore predefinito è 65536 byte.

**Timeout predefinito di eliminazione del documento (secondi)** Il tempo massimo, in secondi, durante il quale un documento passato tra vari componenti di moduli di AEM viene considerato attivo. Una volta trascorso questo periodo di tempo, i file utilizzati per memorizzare questo documento sono soggetti a rimozione. Utilizzare questa impostazione per controllare l&#39;utilizzo dello spazio su disco.

Questa impostazione è obbligatoria. Il valore predefinito è 600 secondi.

**Intervallo di scansione del documento (secondi)** Tempo, in secondi, tra i tentativi di eliminazione dei file non più necessari e utilizzati per trasmettere i dati dei documenti tra i servizi.

Questa impostazione è obbligatoria. Il valore predefinito è 30 secondi.

**Abilita FIPS** Selezionare questa opzione per attivare la modalità FIPS. Il Federal Information Processing Standard (FIPS) 140-2 è uno standard di cristologia definito dal governo degli Stati Uniti. In modalità FIPS, i moduli AEM limitano la protezione dei dati agli algoritmi approvati FIPS 140-2 utilizzando il modulo di crittografia RSA BSAFE Crypto-C 2.1.

La modalità FIPS non supporta gli algoritmi di cifratura utilizzati nelle versioni Adobe Acrobat® precedenti alla 7.0. Se la modalità FIPS è abilitata e si utilizza il servizio di cifratura per cifrare il PDF utilizzando una password con un livello di compatibilità impostato su Acrobat 5, il tentativo di cifratura non riuscirà con un errore.

In generale, quando FIPS è abilitato, il servizio Assembler non applicherà la crittografia della password ad alcun documento. Se si tenta di eseguire questa operazione, viene generata un&#39;eccezione FIPSModeException che indica che &quot;La crittografia della password non è consentita in modalità FIPS&quot;. Inoltre, l&#39;elemento PDFsFromBookmarks della descrizione del documento XML (DDX) non è supportato in modalità FIPS quando il documento di base è crittografato tramite password.

>[!NOTE]
>
>AEM software forms non convalida il codice per garantire la compatibilità FIPS. Fornisce una modalità di funzionamento FIPS in modo che gli algoritmi approvati FIPS siano utilizzati per i servizi di crittografia dalle librerie approvate FIPS (RSA).

**Abilita WSDL** Selezionare questa opzione per abilitare la generazione WSDL (Web Service Definition Language) per tutti i servizi che fanno parte di moduli AEM.

Abilita questa opzione negli ambienti di sviluppo in cui gli sviluppatori utilizzano la generazione WSDL per creare le applicazioni client. È possibile disattivare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

**Abilita archiviazione documenti nel database** Selezionare questa opzione per memorizzare documenti di lunga durata nel database dei moduli AEM. L&#39;abilitazione di questa opzione non elimina la necessità di una directory GDS. Tuttavia, la scelta di questa opzione semplifica i backup AEM moduli. Se utilizzi solo il GDS, un backup comporta il posizionamento del sistema AEM formsAEM forms in modalità di backup e il completamento dei backup del database e del GDS. Se si seleziona l&#39;opzione del database, il backup comporta il completamento del backup del database per una nuova installazione o il completamento del backup del database e il backup una tantum del GDS per un aggiornamento. Potrebbe essere necessaria una gestione aggiuntiva del database per eliminare processi e dati rispetto a una configurazione solo GDS. (Vedere Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti.)

**Abilita statistica chiamata DSC** Quando questa opzione è selezionata, AEM maschere traccia le statistiche di chiamata, ad esempio il numero di chiamate, la quantità di tempo impiegato per richiamare e il numero di errori nelle chiamate. Queste informazioni vengono memorizzate in un file JMX in modo da poter utilizzare Java™ JConsole o software di terze parti per esaminare le statistiche. Se non si desidera visualizzare queste statistiche, deselezionare questa opzione per migliorare le prestazioni dei moduli AEM.

**Abilita RDS** Quando si seleziona questa opzione, il servlet Servizi di sviluppo remoto (RDS) viene attivato all’interno di AEM moduli. Quando questa opzione è abilitata, gli strumenti lato client possono interagire con Data Services per eseguire operazioni quali distribuire o annullare la distribuzione di modelli per creare destinazioni e endpoint o per scoprire quali modelli sono stati distribuiti negli endpoint. Per impostazione predefinita, questa opzione non è selezionata.

**Consenti richiesta RDS non protetta** Quando questa opzione è selezionata, le richieste RDS non devono utilizzare https. Per impostazione predefinita, questa opzione non è selezionata e tutte le comunicazioni ai servizi dati devono essere richieste https.

**Consenti caricamento di documenti non protetti da applicazioni Flex:** Il servlet di caricamento dei file utilizzato per caricare i documenti dalle applicazioni di Adobe Flex® nei AEM moduli richiede l’autenticazione e l’autorizzazione degli utenti prima di poter caricare i documenti. All&#39;utente deve essere assegnato il ruolo Utente applicazione di caricamento documento o un altro ruolo che include l&#39;autorizzazione Caricamento documento. Questo consente di impedire agli utenti non autorizzati di caricare documenti nel server dei moduli di AEM. Selezionare questa opzione se si desidera disattivare questa funzione di protezione in un ambiente di sviluppo o per garantire la compatibilità con versioni precedenti di moduli AEM. Per impostazione predefinita, questa opzione non è selezionata. Per ulteriori informazioni, vedere &quot;Invocazione di moduli AEM utilizzando AEM Remoting dei moduli&quot; in Programmazione di moduli AEM.

**Consenti caricamento di documenti non protetti da applicazioni SDK Java:** I caricamenti HTTP DocumentManager devono essere protetti. Per impostazione predefinita, i caricamenti HTTP richiedono che gli utenti siano autenticati e autorizzati prima di poter caricare i documenti. All&#39;utente deve essere assegnato il ruolo Utente servizi o un altro ruolo che contiene l&#39;autorizzazione Richiamo servizio. Questo consente di impedire agli utenti non autorizzati di caricare documenti sul server dei moduli. Selezionare questa opzione se si desidera disattivare questa funzione di protezione in un ambiente di sviluppo, per garantire la compatibilità con le versioni precedenti dei moduli AEM o in base alla configurazione del firewall. Per impostazione predefinita, questa opzione non è selezionata. Per ulteriori informazioni, vedere &quot;Invocazione di moduli AEM utilizzando l’API Java&quot; in Programmazione con moduli AEM.
