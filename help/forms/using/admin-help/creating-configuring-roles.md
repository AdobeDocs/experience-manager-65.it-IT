---
title: Creazione e configurazione di ruoli
description: Scopri come associare utenti e gruppi a ruoli che fanno già parte del database di User Management. È inoltre possibile creare, modificare ed eliminare ruoli.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 0%

---

# Creazione e configurazione di ruoli{#creating-and-configuring-roles}

Utilizzando le pagine Web Gestione utente, è possibile associare utenti e gruppi a ruoli che fanno già parte del database Gestione utente. È inoltre possibile creare, modificare ed eliminare ruoli.

Gestione utenti dispone di due tipi di ruoli:

**Ruoli modificabili:** È possibile modificare ed eliminare questo tipo di ruolo e aggiungere ed eliminare le autorizzazioni di ruolo da questi tipi di ruolo. Qualsiasi ruolo creato viene considerato mutabile. Puoi aggiungere o rimuovere utenti e gruppi assegnati a ruoli modificabili.

**Ruoli immutabili:** I ruoli predefiniti inclusi in Gestione utenti non sono modificabili. Non è possibile modificare o eliminare questi ruoli. Tuttavia, puoi aggiungere o rimuovere utenti e gruppi assegnati a ruoli immutabili.

I ruoli mutabili e immutabili possono essere creati anche tramite le API dei moduli AEM.

## Ruoli predefiniti {#default-roles}

I seguenti ruoli predefiniti sono inclusi nel database User Management.

**console di amministrazione Utente:** può accedere alla console di amministrazione.

**Amministratore applicazioni:** può utilizzare tutte le funzionalità di Workbench. È possibile utilizzare le pagine Applicazioni e servizi della console di amministrazione per configurare le proprietà, gli endpoint e la sicurezza del runtime del servizio.

**L&#39;amministratore dei moduli AEM:** può eseguire tutte le attività per tutti i servizi installati.

**Amministratore sicurezza:** controlla le impostazioni di gestione utente e gestisce gli utenti e i gruppi associati a qualsiasi dominio di User Manager

**Utente servizi:** può visualizzare e richiamare qualsiasi servizio

**Amministratore privilegiato:** ha accesso a tutte le funzionalità amministrative del sistema, inclusi i servizi

**Amministratore attendibilità:** può gestire le impostazioni di attendibilità PKI e le credenziali PKI gestite dalla pagina Gestione archivio attendibilità nella console di amministrazione

### Ruoli predefiniti aggiuntivi {#additional-default-roles}

A seconda dei componenti dei moduli AEM installati, è possibile includere i seguenti ruoli predefiniti

**Utente applicazione di caricamento documento:** può caricare documenti con Flex Remoting.

**Amministratore Forms:** può visualizzare e modificare le impostazioni dalla pagina Forms in Administration Console

**L&#39;amministratore dello spazio dei contenuti dei moduli AEM:** può visualizzare e modificare le impostazioni dalla pagina Content Services (obsoleto) nella console di amministrazione

**L&#39;AEM forma lo spazio dei contenuti Utente:** Può accedere alle pagine Web dello spazio dei contenuti (obsoleto)

**Documentum Connector Administrator:** può visualizzare e modificare le impostazioni dalla pagina Connector per EMC Documentum nella console di amministrazione

**L&#39;amministratore del connettore FileNet di AEM forms:** può visualizzare e modificare le impostazioni dalla pagina Connettore per IBM FileNet nella console di amministrazione

**L&#39;AEM forma l&#39;amministratore del connettore IBM CM:** può visualizzare e modificare le impostazioni dalla pagina Connettore per IBM Content Manager nella console di amministrazione

**Amministratore di Rights Management:** esegue tutte le attività necessarie per tutte le configurazioni del server nelle pagine di Rights Management pertinenti

**Utente finale Rights Management:** può accedere alle pagine Web dell&#39;utente finale del Rights Management

**Invita utente Rights Management:** può invitare utenti

**Rights Management Gestisci utenti invitati e locali:** può eseguire le attività necessarie per gestire tutti gli utenti invitati e locali nelle pagine di Rights Management pertinenti

**Amministratore set di criteri di Rights Management:** esegue tutte le attività necessarie per tutti i set di criteri nelle relative pagine di Rights Management

**Amministratore privilegiato Rights Management:** esegue tutte le attività necessarie dalla pagina Rights Management

**L&#39;amministratore di Workspace di AEM forms:** può visualizzare e modificare le impostazioni dalla pagina Workspace in Administration Console

***nota **: l&#39;area di lavoro Flex è obsoleta per la versione dei moduli AEM.*

**Utente Workspace:** può accedere all&#39;applicazione dell&#39;utente finale Workspace

**Amministratore di output:** può visualizzare e modificare le impostazioni dalla pagina Output in Administration Console

**Amministratore PDFG:** può visualizzare e modificare le impostazioni dalla pagina PDF Generator nella console di amministrazione

**Utente PDFG:** può accedere a tutte le funzionalità non amministrative per PDF Generator

**Applicazione Web per estensioni Acrobat Reader DC:** può utilizzare l&#39;applicazione Web per estensioni Acrobat Reader DC

>[!NOTE]
>
>Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine Web degli utenti finali di Workspace per motivi di sicurezza. Poiché queste pagine possono esistere all&#39;esterno di un firewall, consentire attività a livello di amministrazione potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di amministratore di Workspace per i moduli AEM o di utente Workspace per i moduli AEM possono accedere alle pagine Web degli utenti finali di Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per il rilascio di moduli AEM.

## Creare un ruolo {#create-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nuovo ruolo.
1. Nella casella Nome ruolo digitare un nome per il ruolo e, facoltativamente, digitare una descrizione del ruolo e quindi fare clic su Avanti.

   >[!NOTE]
   >
   >Quando si utilizza MySQL, non è possibile creare due ruoli che hanno lo stesso nome ma differiscono nell&#39;uso dei caratteri estesi. Ad esempio, se si tenta di creare un ruolo denominato abcde quando esiste già un ruolo denominato âbcdè, viene generato un errore.

1. Fai clic su Trova autorizzazioni, quindi seleziona le autorizzazioni da aggiungere al ruolo.
1. Fare clic su OK e quindi su Avanti.
1. Assegna questo ruolo a utenti e gruppi:

   * Fare clic su Trova utenti/gruppi.
   * Nella casella Trova digitare i criteri di ricerca.
   * Seleziona Nome, E-mail o ID utente, quindi seleziona Utenti, Gruppi o Utenti e gruppi.
   * Selezionare il dominio, selezionare il numero di risultati da visualizzare e fare clic su Trova.
   * Selezionare le caselle di controllo relative agli utenti e ai gruppi a cui assegnare questo ruolo e fare clic su OK.

1. Per visualizzare i dettagli di utenti e gruppi, selezionare l&#39;entità.
1. Fare clic su OK e quindi su Fine.

## Modificare un ruolo {#edit-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli nel database Gestione utente. Se l&#39;elenco dei ruoli è di grandi dimensioni, utilizzare l&#39;area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Fare clic sul ruolo da modificare, modificare le impostazioni generali e fare clic su Salva.
1. Per modificare le autorizzazioni per i ruoli, fare clic sulla scheda Autorizzazioni ed eseguire le operazioni seguenti:

   * Per aggiungere nuove autorizzazioni, fare clic su Trova autorizzazioni, selezionare le caselle di controllo relative alle autorizzazioni da aggiungere, fare clic su OK e quindi su Salva.
   * Per eliminare un&#39;autorizzazione dal ruolo, selezionare la casella di controllo relativa all&#39;autorizzazione, fare clic su Elimina e quindi su Salva.

1. Per gestire gli utenti a cui è assegnato il ruolo, fare clic sulla scheda Utenti ruolo ed eseguire le operazioni seguenti:

   * Per assegnare il ruolo a nuovi utenti e gruppi, fare clic su Trova utenti/gruppi e completare le informazioni di ricerca. Selezionare la casella di controllo per ogni utente e gruppo a cui assegnare il ruolo, fare clic su OK e quindi su Salva.
   * Per rimuovere il ruolo, selezionare la casella di controllo relativa agli utenti o al gruppo, fare clic su Annulla assegnazione e quindi su Salva.

## Eliminare una mansione {#delete-a-role}

Puoi eliminare uno qualsiasi dei ruoli creati, ma non quello predefinito dei moduli AEM che sono inclusi nel prodotto.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli nel database Gestione utente. Se l&#39;elenco dei ruoli è di grandi dimensioni, utilizzare l&#39;area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Selezionare la casella di controllo relativa al ruolo da eliminare, fare clic su Elimina e quindi su OK.

## Assegnare un ruolo a utenti e gruppi {#assign-a-role-to-users-and-groups}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificare le informazioni per limitare la ricerca e fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. È possibile ordinare l&#39;elenco facendo clic su una delle intestazioni di colonna.
1. Selezionare le caselle di controllo accanto agli utenti e ai gruppi da associare a un ruolo e fare clic su Assegna ruolo.
1. Selezionare il ruolo da assegnare all&#39;utente o al gruppo e fare clic su OK.

È inoltre possibile assegnare ruoli utilizzando la pagina Gestione ruolo.

## Determinare chi è assegnato a una mansione {#determine-who-is-assigned-to-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli nel database Gestione utente. Se l&#39;elenco dei ruoli è di grandi dimensioni, utilizzare l&#39;area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nella pagina Dettagli ruolo fare clic sulla scheda Utenti ruolo. Viene visualizzato un elenco di utenti e gruppi direttamente associati al ruolo.

## Modifica autorizzazioni ruolo {#change-role-permissions}

Puoi modificare le autorizzazioni per qualsiasi ruolo creato. Non è possibile modificare le autorizzazioni per i ruoli predefiniti dei moduli AEM inclusi nel prodotto.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli nel database Gestione utente. Se l&#39;elenco dei ruoli è di grandi dimensioni, utilizzare l&#39;area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Selezionare il ruolo per il quale visualizzare le autorizzazioni e fare clic sulla scheda Autorizzazioni.
1. Per modificare queste autorizzazioni, fare clic su Trova autorizzazioni, selezionare le caselle di controllo relative alle autorizzazioni da aggiungere al ruolo, fare clic su OK e quindi su Salva.
1. Per eliminare un&#39;autorizzazione, selezionarla, fare clic su Elimina e quindi su Salva.

### Autorizzazioni per i moduli AEM {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Aggiungere, rimuovere e modificare endpoint per un servizio

**Accesso Admin Console:** Visualizza la console di amministrazione

**Modifica certificato:** Modificare le impostazioni di attendibilità di qualsiasi certificato nell&#39;archivio fonti attendibili

**Lettura certificato:** Lettura di qualsiasi certificato nell&#39;archivio fonti attendibili

**Scrittura certificato:** Aggiungere un certificato all&#39;archivio fonti attendibili

**Aggiunta componente:** Installare un nuovo componente nel sistema

**Eliminazione componente:** Eliminare qualsiasi componente nel sistema

**Lettura componente:** Lettura di qualsiasi componente nel sistema

**Amministratore di Contentspace:** Autorizzazione per l&#39;amministratore di Contentspace (obsoleto)

**Accesso alla console Contentspace:** Autorizzazione per l&#39;accesso alla console Contentspace (obsoleto)

**Controllo impostazioni di base:** Gestisci le impostazioni nella pagina Impostazioni sistema di base di Administration Console

**CREATE_VERSION_PERM:** Crea una versione di un servizio

**Modifica credenziali:** Modificare le credenziali di firma nell&#39;archivio fonti attendibili

**Credenziali lette:** Leggere le credenziali di firma nell&#39;archivio fonti attendibili

**Scrittura credenziali:** Aggiungere una credenziale di firma all&#39;archivio fonti attendibili

**Modifica CRL:** Modificare qualsiasi CRL (elenco di revoche di certificati) nell&#39;archivio fonti attendibili

**Lettura CRL:** Lettura di qualsiasi CRL nell&#39;archivio fonti attendibili

**Scrittura CRL:** Aggiungere un CRL all&#39;archivio fonti attendibili

**Delega:** Imposta un ACL su una risorsa

**DELETE_VERSION_PERM:** Eliminare una versione di un servizio

**Caricamento documento:** Caricamento documenti in moduli AEM

**Controllo dominio:** Creare, eliminare o modificare le impostazioni per qualsiasi dominio di gestione utenti, inclusi i provider di autenticazione e directory

**Modifica tipo evento:** Modifica tipi evento

**Controllo rappresentazione identità:** Impersona in User Manager

**INVOKE_PERM:** Richiama tutte le operazioni su un servizio

**Controllo modello dati LCDS:** leggere e distribuire modelli dati in Data Services

**Aggiornamento gestione licenze:** Aggiornare le informazioni sulla licenza

**MODIFY_CONFIG_PERM:** Modificare la configurazione di un servizio

**TERMINE** Modificare la versione di un servizio

**PDFGAdminPermission:** amministratore PDFG

**PDFGUserPermission:** utente PDFG

**PERM_DCTM_ADMIN:** Amministratore Documentum Connector

**PERM_FILENET_ADMIN:** Amministratore di FileNet Connector

**PERM_FORMS_ADMIN:** amministratore Forms

**PERM_IBMCM_ADMIN:** Amministratore del connettore IBM CM

**PERM_OUTPUT_ADMIN:** Amministratore di output

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Utilizza l&#39;applicazione Web Acrobat Reader DC extensions

**PERM_SP_ADMIN:** Gestisci impostazioni connettore SharePoint

**PERM_WORKSPACE_ADMIN:** Gestisci impostazioni Workspace

**PERM_WORKSPACE_USER:** Accedi all&#39;applicazione dell&#39;utente finale di Workspace

**Controllo entità:** Consente di gestire utenti e gruppi per qualsiasi dominio e di gestire le assegnazioni dei ruoli per tutti gli utenti e i gruppi in qualsiasi dominio

**Elabora registrazione Lettura/eliminazione:** Elenca e recupera le istanze di controllo del flusso di lavoro

**PROCESS_OWNER_PERM:** Visualizza i dati sulle tendenze ed esegue azioni amministrative su un servizio creato da un processo

**Lettura:** lettura del contenuto di una risorsa

**READ_PERM:** Leggi o visualizza un servizio

**Rinnova asserzione:** Rinnova asserzioni in Gestione utenti

**Delegato archivio:** Imposta un ACL su una risorsa

**Lettura archivio:** Lettura del contenuto di una risorsa

**Archivio trasversale:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**Scrittura archivio:** Scrittura metadati e contenuto archivio

**Proprietario criteri di modifica di Rights Management:** Modifica proprietario criteri

**Accesso alla console dell&#39;utente finale del Rights Management:** Accesso all&#39;interfaccia utente dell&#39;utente finale del Rights Management

**Rights Management Gestisci configurazione:** Gestisci configurazione server

**Rights Management Gestisci utenti invitati e locali:** Gestisci utenti invitati e locali

**Rights Management Gestisci set di criteri:** Gestisci tutti i criteri e i documenti in qualsiasi set di criteri

**Coordinatore aggiunta set di criteri di Rights Management:** Aggiungere, rimuovere e modificare le autorizzazioni per i coordinatori set di criteri

**Criteri di Rights Management Imposta Crea criterio:** Crea un criterio per un set di criteri

**Criterio di Rights Management:** Rimuovere un criterio da un set di criteri

**Criterio di Rights Management Imposta modifica criterio:** Modificare un criterio in un set di criteri

**Criteri di Rights Management Gestisci autore documento:** Quando si creano i set di criteri, si assegna agli utenti il ruolo di autore del documento. L’autore del documento è l’utente che lo protegge mediante una policy.

**Coordinatore rimozione set di criteri di Rights Management:** Rimuovere un coordinatore set di criteri da un set di criteri

**Set di criteri di Rights Management: revoca documento:** Revoca dell&#39;accesso ai documenti in un set di criteri

**Criteri di Rights Management:** Criteri di cambio per un documento

**Documento di annullamento revoca impostazione criteri di Rights Management:** Annullamento della revoca di un documento

**Evento visualizzazione set di criteri di Rights Management:** Visualizza gli eventi dei criteri e dei documenti per qualsiasi criterio o documento incluso in un set di criteri

**Rights Management Visualizza eventi server:** Cerca e visualizza tutti gli eventi di controllo

**Controllo ruolo:** Creare, eliminare e modificare ruoli in Gestione utente

**Attivazione servizio:** Avvia qualsiasi servizio, rendendolo disponibile per la chiamata

**Aggiunta servizio:** Distribuire un nuovo servizio nel Registro di sistema. Ciò include l’aggiunta di nuovi processi e varianti di processo

**Disattivazione servizio:** Arrestare qualsiasi servizio nel sistema

**Eliminazione servizio:** Eliminare qualsiasi servizio nel sistema, inclusi i processi e le varianti di processo

**Richiamo servizio:** Richiama qualsiasi servizio nel Registro di sistema del servizio disponibile in fase di esecuzione

**Modifica servizio:** Modificare le proprietà di configurazione di qualsiasi servizio nel sistema. Ciò include il blocco e lo sblocco di un servizio nell&#39;IDE e l&#39;aggiunta o la rimozione di endpoint da un servizio

**Lettura servizio:** Leggere tutti i servizi nel sistema. Questo include tutti i processi e le varianti di processo

**SERVICE_AGENT_PERM:** Visualizza i dati e interagisce con le istanze di processo per un servizio creato da un processo

**SERVICE_MANAGER_PERM:** Eseguire il bilanciamento del carico e altre azioni amministrative in un servizio creato da un processo

**START_STOP_PERM:** Avviare o arrestare un servizio

**SUPERVISOR_PERM:** Visualizza i dati dell&#39;istanza di processo per un servizio creato da un processo

**Attraversamento:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**Scrittura:** Scrittura di metadati e contenuto del repository

**Apertura dei file in Workbench**

Per visualizzare il contenuto della vista Risorse in Workbench e aprire i file per la visualizzazione, un utente deve disporre delle seguenti autorizzazioni:

* Lettura archivio
* Archivio trasversale
* Richiamo servizio
* Lettura servizio

## Rimuovere un utente o un gruppo da un ruolo {#remove-a-user-or-group-from-a-role}

Utilizzare la pagina Gestione dei ruoli per rimuovere utenti e gruppi da un ruolo specifico. Se l&#39;utente o il gruppo ha ereditato l&#39;assegnazione del ruolo, non è possibile rimuovere il ruolo a livello di utente o di gruppo. Rimuovere l&#39;utente o il gruppo dalla struttura di ereditarietà oppure il ruolo dall&#39;elemento padre.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli nel database Gestione utente. Se l&#39;elenco dei ruoli è di grandi dimensioni, utilizzare l&#39;area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nell&#39;elenco dei ruoli fare clic sul nome del ruolo da aggiornare e quindi sulla scheda Utenti ruolo. Viene visualizzato un elenco di utenti e gruppi associati al ruolo.
1. Selezionare le caselle di controllo relative agli utenti e ai gruppi da rimuovere dal ruolo e fare clic su Annulla assegnazione.
1. Fare clic su Salva e quindi su OK.
