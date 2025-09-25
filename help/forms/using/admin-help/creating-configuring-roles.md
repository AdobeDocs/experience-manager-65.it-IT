---
title: Creare e configurare i ruoli
description: Scopri come associare utenti e gruppi a ruoli che fanno già parte del database di Gestione utenti. Puoi inoltre creare, modificare ed eliminare i ruoli.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '2495'
ht-degree: 100%

---

# Creare e configurare i ruoli{#creating-and-configuring-roles}

Utilizzando le pagine web di Gestione utente, puoi associare utenti e gruppi a ruoli che fanno già parte del database di Gestione utente. Puoi inoltre creare, modificare ed eliminare i ruoli.

Gestione utente dispone di due tipi di ruoli:

**Ruoli modificabili:** puoi modificare ed eliminare questo tipo di ruolo e aggiungere ed eliminare le autorizzazioni di ruolo da questi tipi di ruolo. Qualsiasi ruolo creato viene considerato modificabile. Puoi aggiungere o rimuovere utenti e gruppi assegnati a ruoli modificabili.

**Ruoli non modificabili:** i ruoli predefiniti inclusi in Gestione utente sono ruoli non modificabili. Questi ruoli non possono essere modificati né eliminati. Tuttavia, puoi aggiungere o rimuovere utenti e gruppi assegnati ai ruoli non modificabili.

I ruoli modificabili e non modificabili possono essere creati anche tramite le API di AEM Forms.

## Ruoli predefiniti {#default-roles}

I seguenti ruoli predefiniti sono inclusi nel database di Gestione utente.

**Utente della console di amministrazione:** può accedere alla console di amministrazione.

**Amministratore di applicazioni:** può utilizzare tutte le funzionalità di Workbench. Può utilizzare le pagine Applicazioni e servizi della console di amministrazione per configurare le proprietà, gli endpoint e la sicurezza dell’esecuzione del servizio.

**Amministratore di AEM Forms:** può eseguire tutte le attività per tutti i servizi installati.

**Amministratore della sicurezza:** controlla le impostazioni di Gestione utente e gestisce utenti e gruppi associati a qualsiasi dominio di Gestione utente

**Utente dei servizi:** può visualizzare e richiamare qualsiasi servizio

**Amministratore con privilegi:** ha accesso a tutte le funzionalità amministrative del sistema, inclusi i servizi

**Amministratore dell’attendibilità:** può gestire le impostazioni di attendibilità PKI e le credenziali PKI gestite dalla pagina Gestione archivio fonti attendibili nella console di amministrazione

### Ruoli predefiniti aggiuntivi {#additional-default-roles}

A seconda dei componenti di AEM Form che hai installato, puoi includere i seguenti ruoli predefiniti aggiuntivi

**Utente dell’applicazione Caricamento documento:** può caricare documenti con il servizio di remoting Flex.

**Amministratore di Forms:** può visualizzare e modificare le impostazioni dalla pagina Forms nella console di amministrazione

**Amministratore dello spazio dei contenuti di AEM Forms:** può visualizzare e modificare le impostazioni nella pagina Content Services (obsoleto) nella console di amministrazione

**Utente dello spazio dei contenuti di AEM Forms:** può accedere alle pagine web di Spazio dei contenuti (obsoleto)

**Amministratore del connettore Documentum:** può visualizzare e modificare le impostazioni nella pagina Connettore per EMC Documentum nella console di amministrazione

**Amministratore del connettore FileNet di AEM Forms:** può visualizzare e modificare le impostazioni nella pagina Connettore per IBM FileNet nella console di amministrazione

**Amministratore del connettore IBM CM di AEM Forms:** può visualizzare e modificare le impostazioni nella pagina Connettore per IBM Content Manager nella console di amministrazione

**Amministratore di Rights Management:** esegue tutte le attività necessarie per tutte le configurazioni del server nelle pagine di Rights Management pertinenti

**Utente finale di Rights Management:** può accedere alle pagine web dell’utente finale di Rights Management

**Utente degli inviti di Rights Management:** può invitare utenti

**Utente gestore di utenti invitati e locali di Rights Management:** può eseguire le attività necessarie per gestire tutti gli utenti invitati e locali nelle pagine di Rights Management pertinenti

**Amministratore dei set di criteri di Rights Management:** esegue tutte le attività necessarie per tutti i set di criteri nelle pagine di Rights Management pertinenti

**Amministratore con privilegi di Rights Management:** esegue tutte le attività necessarie nella pagina Rights Management

**Amministratore dell’area di lavoro di AEM Forms:** può visualizzare e modificare le impostazioni nella pagina dell’area di lavoro nella console di amministrazione

***Nota **: Flex Workspace è obsoleto per AEM Forms.*

**Utente dell’area di lavoro:** può accedere all’applicazione per utenti finali dell’area di lavoro

**Amministratore di Output:** può visualizzare e modificare le impostazioni nella pagina Output nella console di amministrazione

**Amministratore di PDFG:** può visualizzare e modificare le impostazioni nella pagina di PDF Generator nella console di amministrazione

**Utente di PDFG:** può accedere a tutte le funzionalità non amministrative di PDF Generator

**Applicazione web per Estensioni di Acrobat Reader DC:** può utilizzare l’applicazione web per le Estensioni di Acrobat Reader DC

>[!NOTE]
>
>Per motivi di sicurezza gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine web degli utenti finali dell’area di lavoro. Poiché queste pagine possono esistere all’esterno di un firewall, consentire attività a livello di amministratore potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di amministratore dell’area di lavoro di AEM Forms o di utente dell’area di lavoro di AEM Forms possono accedere alle pagine web degli utenti finali dell’area di lavoro.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.

## Creare un ruolo {#create-a-role}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nuovo ruolo.
1. Nella casella Nome ruolo, digita un nome per il ruolo e, facoltativamente, digita una descrizione del ruolo e, quindi, fai clic su Avanti.

   >[!NOTE]
   >
   >Quando utilizzi MySQL, non puoi creare due ruoli che hanno lo stesso nome, ma differiscono nell’uso dei caratteri estesi. Ad esempio, se si tenta di creare un ruolo denominato abcde quando esiste già un ruolo denominato âbcdè, viene generato un errore.

1. Fai clic su Trova autorizzazioni, quindi seleziona le autorizzazioni da aggiungere al ruolo.
1. Fai clic su OK e, quindi, su Avanti.
1. Assegna questo ruolo a utenti e gruppi:

   * Fai clic su Trova utenti/gruppi.
   * Nella casella Trova, digita i criteri di ricerca.
   * Seleziona Nome, E-mail o ID utente, quindi seleziona Utenti, Gruppi o Utenti e gruppi.
   * Seleziona il dominio, seleziona il numero di risultati da visualizzare e fai clic su Trova.
   * Seleziona le caselle di controllo relative agli utenti e ai gruppi a cui assegnare questo ruolo e fai clic su OK.

1. Per visualizzare i dettagli di utenti e gruppi, seleziona l’entità.
1. Fai clic su OK e, quindi, su Fine.

## Modificare un ruolo {#edit-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è di grandi dimensioni, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Fai clic sul ruolo da modificare, modifica le impostazioni generali e fai clic su Salva.
1. Per modificare le autorizzazioni per i ruoli, fai clic sulla scheda Autorizzazioni ed esegui le operazioni seguenti:

   * Per aggiungere nuove autorizzazioni, fai clic su Trova autorizzazioni, seleziona le caselle di controllo relative alle autorizzazioni da aggiungere, fai clic su OK e, quindi, su Salva.
   * Per eliminare un’autorizzazione dal ruolo, seleziona la casella di controllo relativa all’autorizzazione, fai clic su Elimina e quindi su Salva.

1. Per gestire gli utenti a cui è assegnato il ruolo, fai clic sulla scheda Utenti ruolo ed esegui le operazioni seguenti:

   * Per assegnare il ruolo a nuovi utenti e gruppi, fai clic su Trova utenti/gruppi e completa le informazioni di ricerca. Seleziona la casella di controllo per ogni utente e gruppo a cui vuoi assegnare il ruolo, fai clic su OK e quindi su Salva.
   * Per rimuovere il ruolo, seleziona la casella di controllo corrispondente agli utenti o al gruppo, fai clic su Annulla assegnazione e quindi su Salva.

## Eliminare un ruolo {#delete-a-role}

Puoi eliminare qualsiasi ruolo che hai creato, ma non i ruoli predefiniti di AEM Forms inclusi nel prodotto.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è di grandi dimensioni, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Seleziona la casella di controllo corrispondente al ruolo da eliminare, fai clic su Elimina e quindi su OK.

## Assegnare un ruolo a utenti e gruppi {#assign-a-role-to-users-and-groups}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specifica le informazioni per limitare la ricerca e fai clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Puoi ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Seleziona le caselle di controllo accanto agli utenti e ai gruppi da associare a un ruolo e fai clic su Assegna ruolo.
1. Seleziona il ruolo da assegnare all’utente o al gruppo e fai clic su OK.

Puoi anche assegnare ruoli utilizzando la pagina Gestione ruolo.

## Determinare chi è assegnato a un ruolo {#determine-who-is-assigned-to-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è di grandi dimensioni, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nella pagina Dettagli ruolo fai clic sulla scheda Utenti ruolo. Viene visualizzato un elenco di utenti e gruppi direttamente associati al ruolo.

## Modificare le autorizzazioni del ruolo {#change-role-permissions}

Puoi modificare le autorizzazioni per qualsiasi ruolo che hai creato. Non puoi modificare le autorizzazioni per i ruoli predefiniti di AEM Forms inclusi nel prodotto.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è di grandi dimensioni, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Seleziona il ruolo per il quale visualizzare le autorizzazioni e fai clic sulla scheda Autorizzazioni.
1. Per modificare queste autorizzazioni, fai clic su Trova autorizzazioni, seleziona le caselle di controllo relative alle autorizzazioni da aggiungere al ruolo, fai clic su OK, quindi su Salva.
1. Per eliminare un’autorizzazione, selezionala, fai clic su Elimina, quindi su Salva.

### Autorizzazioni di AEM Forms {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** aggiungi, rimuovi e modifica gli endpoint di un servizio

**Accesso ad Admin Console:** visualizza la console di amministrazione

**Modifica certificato:** modifica le impostazioni di attendibilità di qualsiasi certificato nell’archivio fonti attendibili

**Lettura certificato:** leggi qualsiasi certificato nell’archivio fonti attendibili

**Scrittura certificato:** aggiungi un certificato all’archivio fonti attendibili

**Aggiunta componente:** installa un nuovo componente nel sistema

**Eliminazione componente:** elimina qualsiasi componente nel sistema

**Lettura componente:** leggi qualsiasi componente nel sistema

**Amministratore di Contentspace:** autorizzazione per l’amministratore di Contentspace (obsoleto)

**Accesso alla console di Contentspace:** autorizzazione per l’accesso alla console di Contentspace (obsoleto)

**Controllo impostazioni core:** gestisci le impostazioni nella pagina Impostazioni sistema core della console di amministrazione

**CREATE_VERSION_PERM:** crea la versione di un servizio

**Modifica credenziali:** modifica le credenziali per la firma nell’archivio fonti attendibili

**Lettura credenziali:** leggi le credenziali per la firma nell’archivio fonti attendibili

**Scrittura credenziali:** aggiungi una credenziale per la firma all’archivio fonti attendibili

**Modifica CRL:** modifica qualsiasi Certificate Revocation List (CRL) nell’archivio fonti attendibili

**Lettura CRL:** leggi qualsiasi CRL nell’archivio fonti attendibili

**Scrittura CRL:** aggiungi un CRL all’archivio fonti attendibili

**Delega:** imposta un ACL su una risorsa

**DELETE_VERSION_PERM:** elimina una versione di un servizio

**Caricamento documento:** carica documenti in AEM Forms

**Controllo dominio:** crea, elimina o modifica le impostazioni di qualsiasi dominio di Gestione utente, inclusi i relativi provider di autenticazione e directory

**Modifica tipo evento:** modifica i tipi di evento

**Controllo rappresentazione identità:** rappresenta un’identità in Gestione utente

**INVOKE_PERM:** richiama tutte le operazioni su un servizio

**Controllo modello dati LCDS:** leggi e distribuisci i modelli dati nei servizi dati

**Aggiornamento gestione licenze:** aggiorna le informazioni sulla licenza

**MODIFY_CONFIG_PERM:** modifica la configurazione di un servizio

**TERM** modifica la versione di un servizio

**PDFGAdminPermission:** amministratore di PDFG

**PDFGUserPermission:** utente di PDFG

**PERM_DCTM_ADMIN:** amministratore del connettore di Documentum

**PERM_FILENET_ADMIN:** amministratore del connettore di FileNet

**PERM_FORMS_ADMIN:** amministratore di Forms

**PERM_IBMCM_ADMIN:** amministratore del connettore di IBM CM

**PERM_OUTPUT_ADMIN:** amministratore di Output

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** utilizza l’applicazione web delle Estensioni di Acrobat Reader DC

**PERM_SP_ADMIN:** gestisci le impostazioni del connettore di SharePoint

**PERM_WORKSPACE_ADMIN:** gestisci le impostazioni dell’area di lavoro

**PERM_WORKSPACE_USER:** accedi all’applicazione per l’utente finale dell’area di lavoro

**Controllo entità:** gestisci utenti e gruppi per qualsiasi dominio e le assegnazioni dei ruoli per tutti gli utenti e i gruppi in qualsiasi dominio

**Lettura/eliminazione registrazione del processo:** elenca e recupera le istanze di controllo del flusso di lavoro

**PROCESS_OWNER_PERM:** visualizza i dati sulle tendenze ed esegui azioni amministrative su un servizio creato da un processo

**Leggi:** leggi il contenuto di una risorsa

**READ_PERM:** leggi o visualizza un servizio

**Rinnova asserzione:** rinnova le asserzioni in Gestione utenti

**Delega archivio:** imposta ACL su una risorsa

**Leggi archivio:** leggi il contenuto di una risorsa

**Scorri archivio:** includi una risorsa in una richiesta elenco di risorse o leggi i metadati di una risorsa

**Scrivi archivio:** scrivi metadati e contenuto dell’archivio

**Modifica proprietario del criterio di Gestione dei diritti:** modifica il proprietario del criterio

**Accedi alla console dell’utente finale di Gestione dei diritti:** accedi all’interfaccia utente dell’utente finale di Gestione dei diritti

**Gestisci la configurazione di Gestione dei diritti:** gestisci la configurazione del server

**Gestisci gli utenti invitati e locali di Gestione dei diritti:** gestisci gli utenti invitati e locali

**Gestisci i set di criteri di Gestione dei diritti:** gestisci tutti i criteri e i documenti in qualsiasi set di criteri

**Aggiungi coordinatore del set di criteri di Gestione dei diritti:** aggiungi, rimuovi e modifica le autorizzazioni per i coordinatori dei set di criteri

**Crea criterio per set di criteri di Gestione dei diritti:** crea un criterio per un set di criteri

**Elimina criterio dal set di criteri di Gestione dei diritti:** elimina un criterio da un set di criteri

**Modifica criterio del set di criteri di Gestione dei diritti:** modifica un criterio in un set di criteri

**Gestisci set di criteri editore del documento di Gestione dei diritti:** quando crei set di criteri, assegni agli utenti il ruolo di editore del documento. L’editore del documento è l’utente che protegge il documento mediante un criterio.

**Rimuovi coordinatore del set di criteri di Gestione dei diritti:** rimuovi un coordinatore del set di criteri da un set di criteri

**Revoca il documento nel set di criteri di Gestione dei diritti:** revoca l’areaccesso ai documenti di un set di criteri

**Cambia criterio del set di criteri di Gestione dei diritti:** cambia i criteri di un documento

**Annulla la revoca del documento del set di criteri di Gestione dei diritti:** annulla la revoca di un documento

**Visualizza evento del set di criteri di Gestione dei diritti:** visualizza gli eventi per qualsiasi criterio o documento incluso in un set di criteri

**Visualizza eventi del server di Gestione dei diritti:** cerca e visualizza tutti gli eventi di audit

**Controlla i ruoli:** crea, elimina e modifica i ruoli in Gestione utente

**Attiva il servizio:** avvia qualsiasi servizio, rendendolo disponibile per la chiamata

**Aggiungi il servizio:** distribuisci un nuovo servizio nel registro dei servizi. Include l’aggiunta di nuovi processi e varianti di processo

**Disattiva il servizio:** arresta qualsiasi servizio nel sistema

**Elimina il servizio:** elimina qualsiasi servizio nel sistema, inclusi i processi e le varianti di processo

**Richiama il servizio:** richiama qualsiasi servizio del registro di sistema disponibile in fase di esecuzione

**Modifica il servizio:** modifica le proprietà di configurazione di qualsiasi servizio nel sistema. Include il blocco e lo sblocco di un servizio nell’IDE e l’aggiunta o la rimozione di endpoint da un servizio

**Leggi il servizio:** leggi qualsiasi servizio nel sistema. Include tutti i processi e le varianti di processo

**SERVICE_AGENT_PERM:** visualizza i dati e interagisci con le istanze di processo per un servizio creato da un processo

**SERVICE_MANAGER_PERM:** esegui il bilanciamento del carico e altre azioni amministrative in un servizio creato da un processo

**START_STOP_PERM:** avvia o arresta un servizio

**SUPERVISOR_PERM:** visualizza i dati dell’istanza del processo per un servizio creato da un processo

**Scorri:** includi una risorsa in una richiesta elenco di risorse o leggi i metadati di una risorsa

**Scrivi:** scrivi i metadati e il contenuto del repository

**Aprire file in Workbench**

Per accedere al contenuto della visualizzazione Risorse in Workbench e aprire i file per la visualizzazione, un utente deve disporre delle seguenti autorizzazioni:

* Leggi archivio
* Scorri archivio
* Richiama il servizio
* Leggi il servizio

## Rimuovere un utente o un gruppo da un ruolo {#remove-a-user-or-group-from-a-role}

Utilizza la pagina Gestione ruolo per rimuovere utenti e gruppi da un ruolo specifico. Se l’utente o il gruppo ha ereditato l’assegnazione del ruolo, non sarà possibile rimuovere il ruolo a livello di utente o di gruppo. Rimuovere l’utente o il gruppo dalla struttura di ereditarietà oppure il ruolo dall’elemento padre.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è di grandi dimensioni, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nell’elenco dei ruoli fai clic sul nome del ruolo da aggiornare e quindi sulla scheda Utenti ruolo. Viene visualizzato un elenco di utenti e gruppi associati al ruolo.
1. Seleziona le caselle di controllo relative agli utenti e ai gruppi da rimuovere dal ruolo e fai clic su Annulla assegnazione.
1. Fai clic su Salva e quindi su OK.
