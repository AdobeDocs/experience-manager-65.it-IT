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
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 0%

---

# Creazione e configurazione di ruoli{#creating-and-configuring-roles}

Utilizzando le pagine Web Gestione utente, è possibile associare utenti e gruppi a ruoli che fanno già parte del database Gestione utente. È inoltre possibile creare, modificare ed eliminare ruoli.

Gestione utenti dispone di due tipi di ruoli:

**Ruoli modificabili:** È possibile modificare ed eliminare questo tipo di ruolo e aggiungere ed eliminare autorizzazioni di ruolo da questi tipi di ruolo. Qualsiasi ruolo creato viene considerato mutabile. Puoi aggiungere o rimuovere utenti e gruppi assegnati a ruoli modificabili.

**Ruoli immutabili:** I ruoli predefiniti inclusi in Gestione utente sono ruoli immutabili. Non è possibile modificare o eliminare questi ruoli. Tuttavia, puoi aggiungere o rimuovere utenti e gruppi assegnati a ruoli immutabili.

I ruoli mutabili e immutabili possono essere creati anche tramite le API dei moduli AEM.

## Ruoli predefiniti {#default-roles}

I seguenti ruoli predefiniti sono inclusi nel database User Management.

**console di amministrazione Utente:** Può accedere alla console di amministrazione.

**Amministratore applicazioni:** Può utilizzare tutte le funzioni di Workbench. È possibile utilizzare le pagine Applicazioni e servizi della console di amministrazione per configurare le proprietà, gli endpoint e la sicurezza del runtime del servizio.

**Amministratore di moduli AEM:** Può eseguire tutte le attività per tutti i servizi installati.

**Amministratore sicurezza:** Controlla le impostazioni di User Management e gestisce gli utenti e i gruppi associati a qualsiasi dominio User Manager

**Utente servizi:** Può visualizzare e richiamare qualsiasi servizio

**Amministratore privilegiato:** Ha accesso a tutte le funzionalità amministrative del sistema, inclusi i servizi

**Amministratore fonti attendibili:** Consente di gestire le impostazioni di attendibilità PKI e le credenziali PKI gestite dalla pagina Gestione archivio fonti attendibili nella console di amministrazione

### Ruoli predefiniti aggiuntivi {#additional-default-roles}

A seconda dei componenti dei moduli AEM installati, è possibile includere i seguenti ruoli predefiniti

**Utente applicazione caricamento documento:** È possibile caricare documenti utilizzando la funzione di comunicazione remota di Flex.

**Amministratore Forms:** Può visualizzare e modificare le impostazioni dalla pagina Forms in Admin Console

**Amministratore dello spazio dei contenuti di AEM forms:** È possibile visualizzare e modificare le impostazioni dalla pagina Content Services (obsoleto) nella console di amministrazione

**L’AEM forma l’utente di Content Space:** Può accedere alle pagine web di Contentspace (obsoleto)

**Documentum Connector Administrator:** Possibilità di visualizzare e modificare le impostazioni dalla pagina Connettore per EMC Documentum nella console di amministrazione

**Amministratore di FileNet Connector per AEM forms:** Può visualizzare e modificare le impostazioni dalla pagina Connettore per IBM FileNet nella console di amministrazione

**L’AEM forma l’amministratore del connettore IBM CM:** Può visualizzare e modificare le impostazioni dalla pagina Connettore per IBM Content Manager nella console di amministrazione

**Amministratore Rights Management:** Esegue tutte le attività necessarie per tutte le configurazioni server nelle pagine di Rights Management pertinenti

**Utente finale Rights Management:** Può accedere alle pagine web degli utenti finali del Rights Management

**Utente invito Rights Management:** Può invitare utenti

**Gestione Rights Management utenti invitati e locali:** Può eseguire le attività necessarie per gestire tutti gli utenti invitati e locali sulle pagine di Rights Management pertinenti

**Amministratore set di criteri di Rights Management:** Esegue tutte le attività necessarie per tutti i set di criteri nelle pagine di Rights Management pertinenti

**Amministratore privilegiato Rights Management:** Esegue tutte le attività necessarie dalla pagina Rights Management

**Amministratore di Workspace per AEM Forms:** Può visualizzare e modificare le impostazioni dalla pagina Workspace in Administration Console

***nota **: Flex Workspace è obsoleto per il rilascio di moduli AEM.*

**Utente Workspace:** Può accedere all’applicazione per utenti finali di Workspace

**Amministratore di output:** Può visualizzare e modificare le impostazioni dalla pagina Output in Admin Console

**Amministratore PDFG:** Può visualizzare e modificare le impostazioni dalla pagina PDF Generator nella console di amministrazione

**Utente PDF:** Può accedere a tutte le funzionalità non amministrative di PDF Generator

**Applicazione Web per estensioni Acrobat Reader DC:** Può utilizzare l’applicazione web Acrobat Reader DC extensions

>[!NOTE]
>
>Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine Web degli utenti finali di Workspace per motivi di sicurezza. Poiché queste pagine possono esistere all&#39;esterno di un firewall, consentire attività a livello di amministrazione potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di Amministratore di Workspace per i moduli AEM o di Utente di Workspace per i moduli AEM possono accedere alle pagine Web degli utenti finali di Workspace.

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

**Accesso Admin Console:** Visualizzare la console di amministrazione

**Modifica certificato:** Modificare le impostazioni di attendibilità di qualsiasi certificato nell&#39;archivio fonti attendibili

**Lettura certificato:** Leggi qualsiasi certificato nell&#39;archivio fonti attendibili

**Scrittura certificato:** Aggiungere un certificato all&#39;archivio fonti attendibili

**Aggiunta componente:** Installare un nuovo componente nel sistema

**Eliminazione componente:** Elimina qualsiasi componente nel sistema

**Lettura componente:** Leggi qualsiasi componente del sistema

**Amministratore area contenuti:** Autorizzazione per l&#39;amministratore di Contentspace (obsoleto)

**Accesso alla console Contentspace:** Autorizzazione per l’accesso alla console Spazio dei contenuti (obsoleto)

**Controllo impostazioni core:** Gestisci le impostazioni nella pagina Impostazioni sistema core di Administration Console

**CREATE_VERSION_PERM:** Creare una versione di un servizio

**Modifica credenziali:** Modificare le credenziali di firma nell&#39;archivio fonti attendibili

**Lettura credenziali:** Leggere le credenziali di firma nell&#39;archivio fonti attendibili

**Scrittura credenziali:** Aggiungi credenziali di firma all&#39;archivio fonti attendibili

**Modifica CRL:** Modificare un elenco di revoche di certificati (CRL) nell’archivio fonti attendibili

**Lettura CRL:** Leggi qualsiasi CRL nell’archivio fonti attendibili

**Scrittura CRL:** Aggiungere un CRL all&#39;archivio fonti attendibili

**Delega:** Impostare un ACL su una risorsa

**DELETE_VERSION_PERM:** Eliminare una versione di un servizio

**Caricamento documento:** Caricare documenti nei moduli AEM

**Controllo dominio:** Creare, eliminare o modificare le impostazioni per qualsiasi dominio di User Management, inclusi i relativi provider di autenticazione e directory

**Modifica tipo evento:** Modifica in tipi di evento

**Controllo rappresentazione identità:** Rappresenta l’identità in User Manager

**INVOKE_PERM:** Richiama tutte le operazioni su un servizio

**Controllo modello dati LCDS:** Lettura e distribuzione di modelli dati in Data Services

**Aggiornamento License Manager:** Aggiorna informazioni licenza

**MODIFY_CONFIG_PERM:** Modificare la configurazione di un servizio

**TERMINE** Modificare la versione di un servizio

**PDFGAdminPermission:** Amministratore PDFG

**PDFGUserPermission:** Utente PDFG

**PERM_DCTM_ADMIN:** Amministratore Documentum Connector

**PERM_FILENET_ADMIN** Amministratore di FileNet Connector

**PERM_FORMS_ADMIN:** Amministratore Forms

**PERM_IBMCM_ADMIN:** Amministratore del connettore IBM CM

**PERM_OUTPUT_ADMIN:** Amministratore di output

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Utilizzare l’applicazione web Acrobat Reader DC extensions

**PERM_SP_ADMIN:** Gestione impostazioni connettore SharePoint

**PERM_WORKSPACE_ADMIN:** Gestisci impostazioni area di lavoro

**PERM_WORKSPACE_USER:** Accedere all’applicazione per l’utente finale di Workspace

**Controllo principale:** Gestisci utenti e gruppi per qualsiasi dominio e gestisci le assegnazioni dei ruoli per tutti gli utenti e i gruppi in qualsiasi dominio

**Elabora registrazione lettura/eliminazione:** Elencare e recuperare le istanze di controllo del flusso di lavoro

**PROCESS_OWNER_PERM:** Visualizzare i dati sulle tendenze ed eseguire azioni amministrative su un servizio creato da un processo

**Leggi:** Leggere il contenuto di una risorsa

**READ_PERM:** Lettura o visualizzazione di un servizio

**Rinnova asserzione:** Rinnovare le asserzioni in Gestione utente

**Delegato archivio:** Impostare un ACL su una risorsa

**Lettura archivio:** Leggere il contenuto di una risorsa

**Archivio trasversale:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**Scrittura archivio:** Scrittura di metadati e contenuti dell’archivio

**Proprietario criteri di modifica Rights Management:** Modifica proprietario criterio

**Accesso console utenti finali Rights Management:** Accedi all’interfaccia utente utente del Rights Management

**Configurazione gestione Rights Management:** Gestisci configurazione server

**Gestione Rights Management utenti invitati e locali:** Gestire gli utenti invitati e locali

**Rights Management Gestisci set di criteri:** Gestire tutte le policy e i documenti all’interno di qualsiasi set di policy

**Aggiungi coordinatore set di criteri di Rights Management:** Aggiungere, rimuovere e modificare le autorizzazioni per i coordinatori di set di criteri

**Criteri di Rights Management Imposta Crea criterio:** Creare un criterio per un set di criteri

**Criterio di Rights Management Imposta criteri di eliminazione:** Rimuovere un criterio da un set di criteri

**Criterio di Rights Management Imposta criteri di modifica:** Modificare un criterio in un set di criteri

**Criteri di Rights Management Imposta Gestisci autore documento:** Quando si creano i set di criteri, si assegna agli utenti il ruolo di autore del documento. L’autore del documento è l’utente che lo protegge mediante una policy.

**Coordinatore rimozione set di criteri di Rights Management:** Rimuovere un coordinatore di set di criteri da un set di criteri

**Documento set di criteri di Rights Management:** Revoca dell’accesso ai documenti di un set di criteri

**Criterio di Rights Management Imposta criteri:** Cambiare criteri per un documento

**Documento annullamento revoca set di criteri di Rights Management:** Annullamento della revoca di un documento

**Evento visualizzazione set di criteri di Rights Management:** Visualizzare eventi relativi a criteri e documenti per qualsiasi criterio o documento all&#39;interno di un set di criteri

**Eventi server di visualizzazione Rights Management:** Cerca e visualizza tutti gli eventi di audit

**Controllo ruolo:** Creare, eliminare e modificare ruoli in Gestione utente

**Attivazione servizio:** Avvia qualsiasi servizio, rendendolo disponibile per la chiamata

**Aggiunta servizio:** Distribuire un nuovo servizio nel Registro di sistema. Ciò include l’aggiunta di nuovi processi e varianti di processo

**Disattivazione servizio:** Arresta qualsiasi servizio nel sistema

**Eliminazione servizio:** Elimina qualsiasi servizio nel sistema, inclusi processi e varianti di processo

**Richiamo servizio:** Richiama qualsiasi servizio disponibile nel Registro di sistema del servizio in fase di esecuzione

**Modifica servizio:** Modifica le proprietà di configurazione di qualsiasi servizio nel sistema. Ciò include il blocco e lo sblocco di un servizio nell&#39;IDE e l&#39;aggiunta o la rimozione di endpoint da un servizio

**Lettura servizio:** Leggi tutti i servizi nel sistema. Questo include tutti i processi e le varianti di processo

**SERVICE_AGENT_PERM:** Visualizzare i dati e interagire con le istanze di processo per un servizio creato da un processo

**SERVICE_MANAGER_PERM:** Eseguire il bilanciamento del carico e altre azioni amministrative su un servizio creato da un processo

**START_STOP_PERM:** Avviare o arrestare un servizio

**SUPERVISOR_PERM:** Visualizzare i dati dell&#39;istanza di processo per un servizio creato da un processo

**Attraversa:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**Scrivi:** Scrittura di metadati e contenuti dell’archivio

**Apertura di file in Workbench**

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
