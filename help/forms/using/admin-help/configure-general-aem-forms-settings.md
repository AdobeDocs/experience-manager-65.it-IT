---
title: Impostazioni generali  AEM Forms
seo-title: Impostazioni generali  AEM Forms
description: Scoprite come configurare le impostazioni della pagina Configurazioni di base nella console di amministrazione per migliorare le prestazioni del sistema.
seo-description: Scoprite come configurare le impostazioni della pagina Configurazioni di base nella console di amministrazione per migliorare le prestazioni del sistema.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 1%

---


# Impostazioni generali  AEM Forms {#general-aem-forms-settings}

La pagina Configurazioni di base nella console di amministrazione fornisce impostazioni che consentono di migliorare le prestazioni del sistema. Dopo aver configurato o aggiornato queste impostazioni, riavviate il server applicazione.

Per informazioni sull&#39;abilitazione della modalità di backup sicuro, vedere [Attivazione e disattivazione della modalità di backup sicuro](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>I file nella directory temporanea e i documenti a lunga durata nella directory principale GDS (Document Storage) globale possono contenere informazioni utente sensibili, ad esempio informazioni che richiedono credenziali speciali quando vi si accede utilizzando le API o le interfacce utente. È pertanto importante che questa directory sia adeguatamente protetta utilizzando qualsiasi metodo disponibile per il sistema operativo. Si consiglia che solo l&#39;account del sistema operativo utilizzato per eseguire il server applicazione abbia accesso in lettura e scrittura a questa directory.


1. Nella console di amministrazione, fare clic su **[!UICONTROL Impostazioni > Impostazioni di sistema principali > Configurazioni]**.
1. Nella pagina Configurazioni principali, modificate le opzioni in base alle esigenze e fate clic su **[!UICONTROL OK]**. Per informazioni dettagliate sulle opzioni, vedere [Opzioni delle configurazioni di base](configure-general-aem-forms-settings.md#core-configurations-options).


## Opzioni configurazioni di base {#core-configurations-options}

**Posizione della** directory temporaneaPercorso della directory in cui AEM moduli creeranno file temporanei di prodotto. Se il valore di questa impostazione è vuoto, per impostazione predefinita la posizione corrisponde alla directory temporanea del sistema. Verificate che la directory temporanea sia una cartella scrivibile.

>[!NOTE]
>
>Assicurarsi che la directory temporanea si trovi nel file system locale. AEM moduli non supporta una directory temporanea in una posizione remota.

**Directory radice** dell&#39;archivio documenti globaleLa directory radice dell&#39;archivio documenti globale (GDS) viene utilizzata per i seguenti scopi:

* Memorizzazione di documenti di lunga durata. I documenti di lunga durata non hanno un tempo di scadenza e rimangono inalterati finché non vengono rimossi (ad esempio, i file PDF utilizzati in un processo di workflow). I documenti di lunga durata sono una parte fondamentale dello stato generale del sistema. Se alcuni o tutti questi documenti sono persi o danneggiati, il server dei moduli potrebbe diventare instabile. Pertanto, è importante che questa directory sia memorizzata su un dispositivo RAID.
* Memorizzazione dei documenti temporanei necessari durante l&#39;elaborazione.

>[!NOTE]
>
>È inoltre possibile abilitare l&#39;archiviazione dei documenti nel database dei moduli AEM. Tuttavia, le prestazioni del sistema sono migliori quando si utilizza il GDS.

* Trasferimento di documenti tra nodi di un cluster. Se si esegue AEM moduli in un ambiente cluster, è necessario che la directory sia accessibile da tutti i nodi del cluster.
* Ricezione dei parametri in arrivo dalle chiamate API remote.

Se non si specifica una directory radice GDS, per impostazione predefinita la directory corrisponde a una directory del server applicazione:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>La modifica del valore dell&#39;impostazione della directory principale GDS deve essere effettuata con particolare attenzione. La directory GDS viene utilizzata per memorizzare sia i file longevi utilizzati all&#39;interno di un processo che i componenti critici AEM dei prodotti dei moduli. La modifica della posizione della directory GDS è una modifica importante del sistema. La configurazione non corretta della posizione della directory GDS renderà AEM moduli inattivi e potrebbe richiedere la reinstallazione completa dei moduli AEM. Se si specifica una nuova posizione per la directory GDS, è necessario arrestare il server applicazione e migrare i dati prima di riavviare il server. L&#39;amministratore di sistema deve spostare tutti i file dalla posizione precedente alla nuova posizione, ma mantenere la struttura di directory interna.

>[!NOTE]
>
>Non specificare la stessa directory per la directory temp e la directory GDS.

Per ulteriori informazioni sulla directory GDS, vedere [Preparazione all&#39;installazione dei moduli AEM (Server singolo)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Posizione della** directory dei font del server di Adobe Digitare il percorso della directory che contiene i font del server di Adobe . Questi font vengono installati con AEM moduli. Il percorso predefinito per questi font è la directory [aem-forms root]/fonts. Se questa directory non è accessibile, potete copiare i font altrove e utilizzare questa impostazione per specificare il nuovo percorso.

**Posizione della** directory Font clienteDigitare il percorso di una directory che contiene i font aggiuntivi che si desidera utilizzare.

***nota **: I font vengono selezionati dalla cache dei font di sistema di Windows e per aggiornare la cache è necessario riavviare il sistema. Dopo aver specificato la directory dei font del cliente, assicurarsi di riavviare il sistema in cui sono installati AEM moduli.*

**Posizione della** directory Font di sistemaDigitare il percorso della directory dei font fornita dal sistema operativo in uso. È possibile aggiungere più directory, separate da un punto e virgola **;**.

**Percorso del** file di configurazione di Data ServicesSpecifica il percorso del file services-config.xml. Per impostazione predefinita, questo file è incorporato nel file adobe-core-appserver.ear e non è accessibile all&#39;utente. Una copia del file services-config.xml predefinito si trova in [aem-forms root]\sdk\misc\DataServices\Server-Configuration. Se il file è stato modificato e spostato, digitare la nuova posizione in questo campo.

Il file di configurazione di Data Services consente la personalizzazione delle impostazioni di Data Services, ad esempio il tipo di autenticazione e l&#39;output di debug.

Questa impostazione è vuota per impostazione predefinita.

**Dimensioni massime predefinite del documento (byte)** Il numero massimo di byte conservati in memoria durante il passaggio di documenti tra vari componenti AEM. Utilizzare questa impostazione per ottimizzare le prestazioni. I documenti di dimensioni inferiori a questo numero vengono memorizzati e memorizzati nel database. I documenti che superano questo limite massimo vengono memorizzati sul disco rigido.

Questa impostazione è obbligatoria. Il valore predefinito è 65536 byte.

**Timeout predefinito per lo smaltimento dei documenti (secondi)** Il tempo massimo, in secondi, durante il quale un documento passato tra i vari componenti dei moduli AEM viene considerato attivo. Una volta trascorso tale periodo, i file utilizzati per memorizzare il documento sono soggetti a rimozione. Utilizzare questa impostazione per controllare l&#39;utilizzo dello spazio su disco.

Questa impostazione è obbligatoria. Il valore predefinito è 600 secondi.

**Intervallo di sweep documento (secondi)** Il tempo, in secondi, tra i tentativi di eliminazione di file non più necessari e utilizzati per trasmettere i dati del documento tra i servizi.

Questa impostazione è obbligatoria. Il valore predefinito è 30 secondi.

**Abilita** FIPSSeglezionare questa opzione per abilitare la modalità FIPS. Il Federal Information Processing Standard (FIPS) 140-2 è uno standard di crittografia definito dal governo degli Stati Uniti. In modalità FIPS, AEM moduli limita la protezione dei dati agli algoritmi approvati FIPS 140-2 utilizzando il modulo di crittografia RSA BSAFE Crypto-C 2.1.

La modalità FIPS non supporta gli algoritmi di cifratura utilizzati in  versioni di Adobe Acrobat® precedenti alla 7.0. Se la modalità FIPS è abilitata e si utilizza il servizio di cifratura per cifrare il PDF utilizzando una password con un livello di compatibilità impostato su  Acrobat 5, il tentativo di cifratura non riuscirà con un errore.

In generale, quando FIPS è abilitato, il servizio Assembler non applicherà la crittografia della password ad alcun documento. Se si tenta di eseguire questa operazione, viene generata un&#39;eccezione FIPSModeException che indica che la crittografia della password non è consentita in modalità FIPS. Inoltre, l&#39;elemento PDFsFromBookmarks della descrizione documento XML (DDX) non è supportato in modalità FIPS se il documento di base è crittografato con password.

>[!NOTE]
>
>AEM software dei moduli non convalida il codice per garantire la compatibilità FIPS. Fornisce una modalità di funzionamento FIPS in modo che gli algoritmi approvati FIPS siano utilizzati per i servizi di crittografia dalle librerie approvate FIPS (RSA).

**Abilitare** WSDLSelezionare questa opzione per abilitare la generazione del linguaggio WSDL (Web Service Definition Language) per tutti i servizi che fanno parte di moduli AEM.

Abilitate questa opzione negli ambienti di sviluppo, dove gli sviluppatori utilizzano la generazione WSDL per creare le applicazioni client. Potete scegliere di disabilitare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

**Abilitare l&#39;archiviazione dei documenti nel** databaseSelezionare questa opzione per memorizzare i documenti di lunga durata nel database dei moduli di AEM. L&#39;attivazione di questa opzione non elimina la necessità di una directory GDS. Tuttavia, scegliendo questa opzione è possibile semplificare AEM backup dei moduli. Se si utilizza solo il GDS, un backup richiede il posizionamento del sistema di moduli AEM AEM in modalità di backup e il completamento dei backup del database e del GDS. Se si seleziona l&#39;opzione del database, il backup prevede il completamento del backup del database per una nuova installazione o il completamento del backup del database e il backup una tantum del GDS per un aggiornamento. Potrebbe essere necessaria una gestione aggiuntiva del database per eliminare processi e dati rispetto a una configurazione solo GDS. (Vedere Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti.)

**Abilita** statistica chiamate DSCquando questa opzione è selezionata, AEM moduli tiene traccia delle statistiche di chiamata, come il numero di chiamate, la quantità di tempo impiegato per richiamare e il numero di errori nelle chiamate. Queste informazioni sono memorizzate in un fagiolo JMX in modo da poter utilizzare Java™ JConsole o software di terze parti per consultare le statistiche. Se non si desidera visualizzare queste statistiche, deselezionare questa opzione per migliorare le prestazioni AEM moduli.

**Attiva** RDSSelezione di questa opzione consente di abilitare il servlet Servizi di sviluppo remoto (RDS) all&#39;interno AEM moduli. Quando questa opzione è abilitata, gli strumenti lato client possono interagire con Data Services per eseguire operazioni quali l&#39;implementazione o l&#39;annullamento della distribuzione di modelli per creare destinazioni ed endpoint, o per scoprire quali modelli sono stati distribuiti negli endpoint. Per impostazione predefinita, questa opzione non è selezionata.

**Consenti** richiesta RDS non protettaSe questa opzione è selezionata, le richieste RDS non devono utilizzare https. Per impostazione predefinita, questa opzione non è selezionata e tutte le comunicazioni a Data Services devono essere richieste https.

**Consenti caricamento di documenti non protetti dalle applicazioni Flex:** il servlet di caricamento dei file utilizzato per caricare documenti da  applicazioni Flex® Adobi a AEM moduli richiede che gli utenti siano autenticati e autorizzati prima di poter caricare documenti. All&#39;utente deve essere assegnato il ruolo Utente applicazione Caricamento documento o un altro ruolo che include l&#39;autorizzazione Caricamento documento. Questo consente di impedire agli utenti non autorizzati di caricare documenti nel server AEM moduli. Selezionare questa opzione se si desidera disattivare questa funzione di protezione in un ambiente di sviluppo o per garantire la compatibilità con versioni precedenti dei moduli AEM. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, vedere &quot;Invocazione AEM moduli utilizzando AEM rimozione dei moduli&quot; in Programmazione con AEM moduli.

**Consenti caricamento di documenti non protetti dalle applicazioni Java SDK: i caricamenti** HTTP Document Manager devono essere protetti. Per impostazione predefinita, i caricamenti HTTP richiedono che gli utenti siano autenticati e autorizzati prima di poter caricare i documenti. All&#39;utente deve essere assegnato il ruolo Utente servizi o un altro ruolo che contiene l&#39;autorizzazione Richiamo servizi. Questo consente di impedire agli utenti non autorizzati di caricare documenti nel server dei moduli. Selezionare questa opzione se si desidera disattivare questa funzione di protezione in un ambiente di sviluppo, per garantire la compatibilità con versioni precedenti dei moduli AEM o in base alla configurazione del firewall in uso. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, vedere &quot;Chiamata di moduli AEM tramite l&#39;API Java&quot; nella programmazione con AEM moduli.
