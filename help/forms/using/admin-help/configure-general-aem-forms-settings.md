---
title: Impostazioni generali di AEM Forms
seo-title: Impostazioni generali di AEM Forms
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

---


# Impostazioni generali di AEM Forms {#general-aem-forms-settings}

La pagina Configurazioni di base nella console di amministrazione fornisce impostazioni che consentono di migliorare le prestazioni del sistema. Dopo aver configurato o aggiornato queste impostazioni, riavviate il server applicazione.

Per informazioni sull&#39;abilitazione della modalità di backup sicuro, consultate [Attivazione e disattivazione della modalità](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)di backup sicura.


>[!NOTE]
>
>I file nella directory temporanea e i documenti a lunga durata nella directory principale GDS (Document Storage) globale possono contenere informazioni utente sensibili, ad esempio informazioni che richiedono credenziali speciali quando vi si accede utilizzando le API o le interfacce utente. È pertanto importante che questa directory sia adeguatamente protetta utilizzando qualsiasi metodo disponibile per il sistema operativo. Si consiglia che solo l&#39;account del sistema operativo utilizzato per eseguire il server applicazione abbia accesso in lettura e scrittura a questa directory.


1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Impostazioni di sistema di base > Configurazioni]**.
1. Nella pagina Configurazioni di base, modificate le opzioni come richiesto e fate clic su **[!UICONTROL OK]**. Per informazioni dettagliate sulle opzioni, consultate Opzioni [Configurazioni](configure-general-aem-forms-settings.md#core-configurations-options)principali.


## Opzioni delle configurazioni di base {#core-configurations-options}

**Posizione della directory** temporanea Il percorso della directory in cui i moduli AEM creeranno i file temporanei dei prodotti. Se il valore di questa impostazione è vuoto, per impostazione predefinita la posizione corrisponde alla directory temporanea del sistema. Verificate che la directory temporanea sia una cartella scrivibile.

>[!NOTE]
>
>Assicurarsi che la directory temporanea si trovi nel file system locale. I moduli AEM non supportano una directory temporanea in una posizione remota.

**Directory** radice dell&#39;archivio documenti globale La directory radice dell&#39;archivio documenti globale (GDS) è utilizzata per i seguenti scopi:

* Memorizzazione di documenti di lunga durata. I documenti di lunga durata non hanno un tempo di scadenza e rimangono inalterati finché non vengono rimossi (ad esempio, i file PDF utilizzati in un processo di workflow). I documenti di lunga durata sono una parte fondamentale dello stato generale del sistema. Se alcuni o tutti questi documenti sono persi o danneggiati, il server dei moduli potrebbe diventare instabile. Pertanto, è importante che questa directory sia memorizzata su un dispositivo RAID.
* Memorizzazione dei documenti temporanei necessari durante l&#39;elaborazione.

>[!NOTE]
>
>È inoltre possibile abilitare l&#39;archiviazione documenti nel database moduli di AEM. Tuttavia, le prestazioni del sistema sono migliori quando si utilizza il GDS.

* Trasferimento di documenti tra nodi di un cluster. Se si esegue AEM Forms in un ambiente cluster, questa directory deve essere accessibile da tutti i nodi del cluster.
* Ricezione dei parametri in arrivo dalle chiamate API remote.

Se non si specifica una directory radice GDS, per impostazione predefinita la directory corrisponde a una directory del server applicazione:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>La modifica del valore dell&#39;impostazione della directory principale GDS deve essere effettuata con particolare attenzione. La directory GDS viene utilizzata per memorizzare sia i file longevi utilizzati in un processo che i componenti critici dei moduli AEM. La modifica della posizione della directory GDS è una modifica importante del sistema. La configurazione non corretta della posizione della directory GDS renderà i moduli AEM inattivi e potrebbe richiedere una reinstallazione completa dei moduli AEM. Se si specifica una nuova posizione per la directory GDS, è necessario arrestare il server applicazione e migrare i dati prima di riavviare il server. L&#39;amministratore di sistema deve spostare tutti i file dalla posizione precedente alla nuova posizione, ma mantenere la struttura di directory interna.

>[!NOTE]
>
>Non specificare la stessa directory per la directory temp e la directory GDS.

Per ulteriori informazioni sulla directory GDS, consultate [Preparazione all&#39;installazione di moduli AEM (Single Server)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Posizione della directory** Font di Adobe Server Digitare il percorso della directory che contiene i font del server Adobe. Questi font vengono installati con i moduli AEM. Il percorso predefinito per questi font è la directory principale [/font dei moduli]aem. Se questa directory non è accessibile, potete copiare i font altrove e utilizzare questa impostazione per specificare il nuovo percorso.

**Posizione della directory** Font del cliente Digitare il percorso di una directory che contiene i font aggiuntivi che si desidera utilizzare.

***nota **: I font vengono selezionati dalla cache dei font di sistema di Windows e per aggiornare la cache è necessario riavviare il sistema. Dopo aver specificato la directory dei font per il cliente, accertatevi di riavviare il sistema in cui sono installati i moduli AEM.*

**Posizione della directory** Font di sistema Digitare il percorso della directory dei font fornita dal sistema operativo in uso. È possibile aggiungere più directory, separate da un punto e virgola **;**.

**Percorso del file** di configurazione di Data Services Specifica il percorso del file services-config.xml. Per impostazione predefinita, questo file è incorporato nel file adobe-core-appserver.ear e non è accessibile all&#39;utente. Una copia del file services-config.xml predefinito si trova nella directory principale [\sdk\misc\DataServices\Server-Configuration dei moduli]aem. Se il file è stato modificato e spostato, digitare la nuova posizione in questo campo.

Il file di configurazione di Data Services consente la personalizzazione delle impostazioni di Data Services, ad esempio il tipo di autenticazione e l&#39;output di debug.

Questa impostazione è vuota per impostazione predefinita.

**Dimensioni massime predefinite del documento in linea (byte)** Il numero massimo di byte conservati in memoria durante il passaggio di documenti tra vari componenti di moduli AEM. Use this setting for performance tuning. I documenti di dimensioni inferiori a questo numero vengono memorizzati e memorizzati nel database. Documents that exceed this maximum are stored on the hard drive.

Questa impostazione è obbligatoria. Il valore predefinito è 65536 byte.

**Default document disposal timeout (seconds)** The maximum amount of time, in seconds, during which a document being passed between various AEM forms components is considered active. Una volta trascorso tale periodo, i file utilizzati per memorizzare il documento sono soggetti a rimozione. Use this setting to control the usage of disk space.

Questa impostazione è obbligatoria. Il valore predefinito è 600 secondi.

**Document sweep interval (seconds)** The amount of time, in seconds, between attempts to delete files that are no longer needed and were used to pass document data between services.

Questa impostazione è obbligatoria. Il valore predefinito è 30 secondi.

**Enable FIPS** Select this option to enable FIPS mode. Federal Information Processing Standard (FIPS) 140-2 is a U.S. government-defined cryptology standard. When running in FIPS mode, AEM forms restricts data protection to FIPS 140-2 approved algorithms by using the RSA BSAFE Crypto-C 2.1 encryption module.

FIPS mode does not support encryption algorithms that are used in Adobe Acrobat® versions earlier than 7.0. If FIPS mode is enabled and you use the Encryption service to encrypt the PDF by using a password with a compatibility level set to Acrobat 5, the encryption attempt will fail with an error.

In general, when FIPS is enabled, the Assembler service will not apply password encryption to any document. If this is attempted, a FIPSModeException is thrown indicating that &quot;Password encryption is not permitted in FIPS mode.&quot; Inoltre, l&#39;elemento PDFsFromBookmarks della descrizione documento XML (DDX) non è supportato in modalità FIPS se il documento di base è crittografato con password.

>[!NOTE]
>
>Il software per moduli AEM non convalida il codice per garantire la compatibilità FIPS. Fornisce una modalità di funzionamento FIPS in modo che gli algoritmi approvati FIPS siano utilizzati per i servizi di crittografia dalle librerie approvate FIPS (RSA).

**Abilita WSDL** Selezionate questa opzione per abilitare la generazione del linguaggio WSDL (Web Service Definition Language) per tutti i servizi che fanno parte di moduli AEM.

Enable this option in development environments, where developers use WSDL generation to build their client applications. Potete scegliere di disabilitare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

**Abilita archiviazione documenti nel database** Selezionate questa opzione per memorizzare documenti di lunga durata nel database dei moduli AEM. L&#39;attivazione di questa opzione non elimina la necessità di una directory GDS. Tuttavia, scegliendo questa opzione è possibile semplificare i backup dei moduli AEM. Se si utilizza solo il GDS, un backup comporta l’implementazione del sistema di moduli AEM in modalità di backup e il completamento dei backup del database e del GDS. Se si seleziona l&#39;opzione del database, il backup prevede il completamento del backup del database per una nuova installazione o il completamento del backup del database e il backup una tantum del GDS per un aggiornamento. Potrebbe essere necessaria una gestione aggiuntiva del database per eliminare processi e dati rispetto a una configurazione solo GDS. (Vedere Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti.)

**Abilita statistica** chiamate DSC Quando questa opzione è selezionata, AEM Forms tiene traccia delle statistiche di chiamata, come il numero di chiamate, la quantità di tempo impiegato per richiamare e il numero di errori nelle chiamate. Queste informazioni sono memorizzate in un fagiolo JMX in modo da poter utilizzare Java™ JConsole o software di terze parti per consultare le statistiche. Se non si desidera visualizzare queste statistiche, deselezionare questa opzione per migliorare le prestazioni dei moduli AEM.

**Abilita RDS** Quando si seleziona questa opzione, il servlet Servizi di sviluppo remoto (RDS) viene attivato nei moduli AEM. Quando questa opzione è abilitata, gli strumenti lato client possono interagire con Data Services per eseguire operazioni quali l&#39;implementazione o l&#39;annullamento della distribuzione di modelli per creare destinazioni ed endpoint, o per scoprire quali modelli sono stati distribuiti negli endpoint. Per impostazione predefinita, questa opzione non è selezionata.

**Consenti richiesta** RDS non sicura Se questa opzione è selezionata, le richieste RDS non devono utilizzare https. Per impostazione predefinita, questa opzione non è selezionata e tutte le comunicazioni a Data Services devono essere richieste https.

**Consenti caricamento di documenti non protetti dalle applicazioni Flex:** Il servlet di caricamento dei file utilizzato per caricare i documenti dalle applicazioni Adobe Flex® ai moduli AEM richiede che gli utenti siano autenticati e autorizzati prima di poter caricare i documenti. All&#39;utente deve essere assegnato il ruolo Utente applicazione Caricamento documento o un altro ruolo che include l&#39;autorizzazione Caricamento documento. Questo consente di impedire agli utenti non autorizzati di caricare documenti nel server moduli AEM. Selezionate questa opzione se desiderate disattivare questa funzione di protezione in un ambiente di sviluppo o per garantire la compatibilità con le versioni precedenti dei moduli AEM. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, consultate &quot;Invoking AEM forms Using AEM forms Remoting&quot; (Invocare moduli AEM utilizzando la funzionalità REMIX moduli AEM) nella programmazione con i moduli AEM.

**Consenti caricamento di documenti non protetti dalle applicazioni Java SDK:** I caricamenti HTTP DocumentManager devono essere protetti. Per impostazione predefinita, i caricamenti HTTP richiedono che gli utenti siano autenticati e autorizzati prima di poter caricare i documenti. All&#39;utente deve essere assegnato il ruolo Utente servizi o un altro ruolo che contiene l&#39;autorizzazione Richiamo servizi. Questo consente di impedire agli utenti non autorizzati di caricare documenti nel server dei moduli. Selezionate questa opzione se desiderate disattivare questa funzione di protezione in un ambiente di sviluppo, per compatibilità con le versioni precedenti dei moduli AEM o in base alla configurazione del firewall in uso. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, consultate &quot;Richiamo di moduli AEM tramite l&#39;API Java&quot; nella programmazione con i moduli AEM.
