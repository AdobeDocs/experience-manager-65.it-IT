---
title: Creazione e configurazione di ruoli
seo-title: Creating and configuring roles
description: Scopri come associare utenti e gruppi a ruoli che fanno già parte del database User Management. Puoi anche creare, modificare ed eliminare ruoli.
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---

# Creazione e configurazione di ruoli{#creating-and-configuring-roles}

Utilizzando le pagine web Gestione utente, puoi associare utenti e gruppi a ruoli che fanno già parte del database Gestione utente. Puoi anche creare, modificare ed eliminare ruoli.

La gestione utente dispone di due tipi di ruoli:

**Ruoli variabili:** Questo tipo di ruolo può essere modificato ed eliminato e le autorizzazioni per i ruoli possono essere aggiunte ed eliminate da questi tipi di ruolo. Qualsiasi ruolo creato viene considerato mutabile. Puoi aggiungere o rimuovere utenti e gruppi assegnati a ruoli modificabili.

**Ruoli immutabili:** I ruoli predefiniti inclusi con Gestione utente sono immutabili. Questi ruoli non possono essere modificati o eliminati. È tuttavia possibile aggiungere o rimuovere utenti e gruppi assegnati a ruoli immutabili.

È inoltre possibile creare ruoli mutabili e immutabili tramite le API dei moduli AEM.

## Ruoli predefiniti {#default-roles}

I seguenti ruoli predefiniti sono inclusi nel database User Management.

**console di amministrazione Utente:** Può accedere alla console di amministrazione.

**Amministratore dell&#39;applicazione:** Utilizza tutte le funzionalità di Workbench. Può utilizzare le pagine Applicazioni e servizi nella console di amministrazione per configurare proprietà, endpoint e sicurezza di esecuzione del servizio.

**Amministratore AEM moduli:** È in grado di eseguire tutte le attività per tutti i servizi installati.

**Amministratore della sicurezza:** Controlla le impostazioni di User Management e gestisce gli utenti e i gruppi associati a qualsiasi dominio di User Manager

**Utente servizi:** Può visualizzare e richiamare qualsiasi servizio

**Amministratore avanzato:** Ha accesso a tutte le funzionalità amministrative del sistema, compresi i servizi

**Amministratore di attendibilità:** È possibile gestire le impostazioni di attendibilità PKI e le credenziali PKI gestite dalla pagina Gestione archivio attendibili nella console di amministrazione

### Altri ruoli predefiniti {#additional-default-roles}

Possono essere inclusi i seguenti ruoli predefiniti aggiuntivi, a seconda dei componenti dei moduli AEM installati

**Utente applicazione di caricamento documenti:** Può caricare documenti utilizzando Flex Remoting.

**Amministratore Forms:** Può visualizzare e modificare le impostazioni dalla pagina Forms in Admin Console

**Amministratore di spazio dei AEM moduli:** Può visualizzare e modificare le impostazioni dalla pagina Content Services (Obsoleto) nella console di amministrazione

**AEM moduli Contentspace Utente:** Può accedere alle pagine web Contentspace (Obsoleto)

**Amministratore Documentum Connector:** È possibile visualizzare e modificare le impostazioni dalla pagina Connettore per EMC Documentum nella console di amministrazione

**Amministratore del connettore FileNet di AEM:** Può visualizzare e modificare le impostazioni dalla pagina Connector for IBM FileNet nella console di amministrazione

**Amministratore del connettore IBM CM per moduli AEM:** Può visualizzare e modificare le impostazioni dalla pagina Connector for IBM Content Manager nella console di amministrazione

**Amministratore di Rights Management:** Esegue tutte le attività necessarie per tutte le configurazioni del server nelle pagine dei Rights Management pertinenti

**Utente finale Rights Management:** Accesso alle pagine web dell&#39;utente finale del Rights Management

**Rights Management invito utente:** Può invitare gli utenti

**Gestione Rights Management utenti invitati e locali:** Può eseguire le attività necessarie per gestire tutti gli utenti invitati e locali nelle pagine dei Rights Management pertinenti

**Amministratore set di criteri di Rights Management:** Esegue tutte le attività necessarie per tutti i set di criteri nelle pagine dei Rights Management rilevanti

**Amministratore avanzato Rights Management:** Esegue tutte le attività richieste dalla pagina Rights Management

**Amministratore di AEM Workspace:** Può visualizzare e modificare le impostazioni dalla pagina Workspace in Admin Console

***nota **: Flex Workspace è obsoleto per AEM versione dei moduli.*

**Utente area di lavoro:** Può accedere all’applicazione utente finale di Workspace

**Amministratore output:** Può visualizzare e modificare le impostazioni dalla pagina Output in Admin Console

**Amministratore PDFG:** Può visualizzare e modificare le impostazioni dalla pagina PDF Generator nella console di amministrazione

**Utente PDFG:** Può accedere a tutte le funzionalità non amministrative di PDF Generator

**Applicazione Web Acrobat Reader DC extensions:** Può utilizzare l&#39;applicazione Web Acrobat Reader DC extensions

>[!NOTE]
>
>Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine web dell’utente finale di Workspace per motivi di sicurezza. Poiché queste pagine possono esistere al di fuori di un firewall, l’autorizzazione delle attività a livello di amministrazione potrebbe comportare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di amministratore di Workspace o AEM forms Workspace possono accedere alle pagine Web degli utenti finali di Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.

## Creare un ruolo {#create-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nuovo ruolo.
1. Nella casella Nome ruolo digitare un nome per il ruolo e, facoltativamente, digitare una descrizione del ruolo, quindi fare clic su Avanti.

   >[!NOTE]
   >
   >Quando si utilizza MySQL, non è possibile creare due ruoli che hanno lo stesso nome ma differiscono nell&#39;uso di caratteri estesi. Ad esempio, se si tenta di creare un ruolo denominato abcde quando esiste già un ruolo denominato âbcdè, si verifica un errore.

1. Fare clic su Trova autorizzazioni, selezionare le autorizzazioni da aggiungere al ruolo.
1. Fare clic su OK e quindi su Avanti.
1. Assegna questo ruolo a utenti e gruppi:

   * Fare clic su Trova utenti/gruppi.
   * Nella casella Trova digitare i criteri di ricerca.
   * Selezionare Nome, E-mail o ID utente, quindi selezionare Utenti, Gruppi o Utenti e gruppi.
   * Selezionare il dominio, selezionare il numero di risultati da visualizzare e fare clic su Trova.
   * Selezionare le caselle di controllo relative agli utenti e ai gruppi a cui assegnare il ruolo e fare clic su OK.

1. Per visualizzare i dettagli utente e gruppo, seleziona l’entità.
1. Fare clic su OK e quindi su Fine.

## Modificare un ruolo {#edit-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Fare clic sul ruolo da modificare, modificare le impostazioni generali e fare clic su Salva.
1. Per modificare le autorizzazioni del ruolo, fare clic sulla scheda Autorizzazioni ed eseguire le operazioni seguenti:

   * Per aggiungere nuove autorizzazioni, fare clic su Trova autorizzazioni, selezionare le caselle di controllo relative alle autorizzazioni da aggiungere, fare clic su OK e quindi su Salva.
   * Per eliminare un’autorizzazione dal ruolo, selezionare la casella di controllo relativa all’autorizzazione, fare clic su Elimina, quindi fare clic su Salva.

1. Per gestire a chi è assegnato il ruolo, fai clic sulla scheda Utenti ruolo ed esegui le seguenti attività:

   * Per assegnare il ruolo a nuovi utenti e gruppi, fare clic su Trova utenti/gruppi e completare le informazioni di ricerca. Selezionare la casella di controllo relativa a ciascun utente e gruppo a cui assegnare il ruolo, fare clic su OK e quindi su Salva.
   * Per rimuovere il ruolo, selezionare la casella di controllo relativa agli utenti o al gruppo, fare clic su Annulla assegnazione e quindi su Salva.

## Eliminare un ruolo {#delete-a-role}

È possibile eliminare uno qualsiasi dei ruoli creati, ma non i ruoli predefiniti dei moduli AEM inclusi nel prodotto.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Selezionare la casella di controllo relativa al ruolo da eliminare, fare clic su Elimina e quindi su OK.

## Assegnare un ruolo a utenti e gruppi {#assign-a-role-to-users-and-groups}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificare le informazioni per limitare la ricerca e fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Per ordinare l’elenco, fai clic su una delle intestazioni di colonna.
1. Selezionare le caselle di controllo accanto agli utenti e ai gruppi da associare a un ruolo e fare clic su Assegna ruolo.
1. Selezionare il ruolo da assegnare all&#39;utente o al gruppo e fare clic su OK.

Puoi anche assegnare ruoli utilizzando la pagina Gestione ruoli .

## Determinare chi è assegnato a un ruolo {#determine-who-is-assigned-to-a-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nella pagina Dettagli ruolo , fai clic sulla scheda Utenti ruolo . Viene visualizzato un elenco di utenti e gruppi che sono direttamente associati al ruolo.

## Modificare le autorizzazioni del ruolo {#change-role-permissions}

Puoi modificare le autorizzazioni per uno qualsiasi dei ruoli creati. Non è possibile modificare le autorizzazioni per i ruoli modulo AEM predefiniti inclusi nel prodotto.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Seleziona il ruolo per cui visualizzare le autorizzazioni e fai clic sulla scheda Autorizzazioni .
1. Per modificare queste autorizzazioni, fare clic su Trova autorizzazioni, selezionare le caselle di controllo relative alle autorizzazioni da aggiungere al ruolo, fare clic su OK e quindi su Salva.
1. Per eliminare un’autorizzazione, selezionarla, fare clic su Elimina, quindi su Salva.

### Autorizzazioni AEM moduli {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Aggiungere, rimuovere e modificare gli endpoint di un servizio

**Admin Console di accesso:** Visualizzare la console di amministrazione

**Modifica certificato:** Modificare le impostazioni di attendibilità di qualsiasi certificato nell&#39;archivio attendibilità

**Certificato letto:** Leggi qualsiasi certificato nell&#39;archivio fonti attendibili

**Scrittura certificato:** Aggiungi un certificato all’archivio attendibilità

**Aggiungi componente:** Installare un nuovo componente nel sistema

**Elimina componente:** Elimina qualsiasi componente del sistema

**Lettura componente:** Leggi qualsiasi componente del sistema

**Amministratore di Contentspace:** Autorizzazione per l&#39;amministratore di Contentspace (obsoleto)

**Accesso alla console Contentspace:** Autorizzazione per l’accesso alla console Contentspace (obsoleto)

**Controllo impostazioni core:** Gestire le impostazioni nella pagina Impostazioni sistema core in Admin Console

**CREATE_VERSION_PERM:** Creare una nuova versione di un servizio

**Modifica credenziale:** Modificare le credenziali di firma nell&#39;archivio attendibilità

**Lettura credenziali:** Leggere le credenziali di firma nell&#39;archivio attendibilità

**Scrittura credenziale:** Aggiungi una credenziale di firma all’archivio attendibilità

**Modifica CRL:** Modificare un CRL (Elenco di revoca certificati) nell&#39;archivio certificati

**Lettura CRL:** Leggere qualsiasi CRL nell&#39;archivio certificati

**Scrittura CRL:** Aggiungere un CRL all&#39;archivio certificati

**Delega:** Impostare un ACL su una risorsa

**DELETE_VERSION_PERM:** Eliminare una versione di un servizio

**Caricamento documento:** Caricare documenti nei moduli AEM

**Controllo dominio:** Creare, eliminare o modificare le impostazioni per qualsiasi dominio di Gestione utente, inclusi i provider di autenticazione e directory

**Modifica tipo evento:** Modifica ai tipi di evento

**Controllo rappresentazione identità:** Impersona identità in User Manager

**INVOKE_PERM:** Richiama di tutte le operazioni su un servizio

**Controllo del modello dati LCDS:** Lettura e distribuzione dei modelli di dati in Servizi dati

**Aggiornamento di License Manager:** Aggiornare le informazioni sulla licenza

**MODIFY_CONFIG_PERM:** Modificare la configurazione di un servizio

**TERMINE** Modificare la versione di un servizio

**PDFGAdminPermission:** Amministratore PDFG

**PDFGUserPermission:** Utente PDFG

**PERM_DCTM_ADMIN:** Amministratore Documentum Connector

**PERM_FILENET_ADMIN:** Amministratore del connettore FileNet

**PERM_FORMS_ADMIN:** Amministratore Forms

**PERM_IBMCM_ADMIN:** Amministratore del connettore IBM CM

**PERM_OUTPUT_ADMIN:** Amministratore di output

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Utilizzare l&#39;applicazione Web Acrobat Reader DC extensions

**PERM_SP_ADMIN:** Gestire le impostazioni del connettore SharePoint

**PERM_WORKSPACE_ADMIN:** Gestire le impostazioni di Workspace

**PERM_WORKSPACE_USER:** Accedere all’applicazione utente finale Workspace

**Controllo principale:** Gestisci utenti e gruppi per qualsiasi dominio e gestisci le assegnazioni di ruolo per tutti gli utenti e i gruppi in qualsiasi dominio

**Lettura/eliminazione della registrazione del processo:** Elencare e recuperare le istanze di controllo del flusso di lavoro

**PROCESS_OWNER_PERM:** Visualizzare i dati delle tendenze ed eseguire azioni amministrative su un servizio creato da un processo

**Leggi:** Leggere il contenuto di una risorsa

**READ_PERM:** Lettura o visualizzazione di un servizio

**Rinnova asserzione:** Rinnova asserzioni in Gestione utente

**Delegato archivio:** Impostare un ACL su una risorsa

**Lettura archivio:** Leggere il contenuto di una risorsa

**Percorso archivio:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**Scrittura archivio:** Scrivere metadati e contenuti dell&#39;archivio

**Proprietario del criterio di modifica Rights Management:** Cambia proprietario del criterio

**Accesso alla console utente finale del Rights Management:** Accedi all&#39;interfaccia utente finale del Rights Management

**Configurazione gestione Rights Management:** Gestire la configurazione del server

**Gestione Rights Management utenti invitati e locali:** Gestione degli utenti invitati e locali

**Rights Management Gestisci set di criteri:** Gestisci tutti i criteri e i documenti all&#39;interno di qualsiasi set di criteri

**Imposta criterio Rights Management Aggiungi coordinatore:** Aggiunta, rimozione e modifica delle autorizzazioni per i coordinatori dei set di criteri

**Criterio di creazione set di criteri di Rights Management:** Creare un nuovo criterio per un set di criteri

**Criterio di eliminazione set di criteri di Rights Management:** Rimuovere un criterio da un set di criteri

**Criterio di modifica set di criteri di Rights Management:** Modificare un criterio in un set di criteri

**Set di criteri di Rights Management Gestisci autore documenti:** Quando si creano set di criteri, si assegna agli utenti il ruolo di editore del documento. L&#39;autore del documento è l&#39;utente che protegge il documento con un criterio.

**Coordinatore rimozione set di criteri di Rights Management:** Rimuovere un coordinatore del set di criteri da un set di criteri

**Documento Revoca set di criteri di Rights Management:** Revoca dell&#39;accesso ai documenti in un set di criteri

**Criterio di commutazione set di criteri di Rights Management:** Cambia criteri per un documento

**Rights Management Criteri Imposta documento di annullamento revoca:** Annullamento della revoca di un documento

**Evento di visualizzazione set di criteri di Rights Management:** Visualizzare gli eventi dei criteri e dei documenti per qualsiasi criterio o documento all&#39;interno di un set di criteri

**Eventi server di visualizzazione Rights Management:** Ricerca e visualizzazione di tutti gli eventi di controllo

**Controllo del ruolo:** Creare, eliminare e modificare ruoli in Gestione utente

**Attivazione servizio:** Avvia qualsiasi servizio, rendendolo disponibile per la chiamata

**Aggiungi servizio:** Distribuire un nuovo servizio nel Registro di sistema del servizio. Ciò include l&#39;aggiunta di nuovi processi e varianti di processo

**Disattivazione del servizio:** Arresta qualsiasi servizio nel sistema

**Elimina servizio:** Elimina qualsiasi servizio nel sistema, inclusi processi e varianti di processo

**Richiamo del servizio:** Richiama qualsiasi servizio nel Registro di sistema del servizio disponibile in fase di esecuzione

**Modifica servizio:** Modifica le proprietà di configurazione di qualsiasi servizio nel sistema. Ciò include il blocco e lo sblocco di un servizio nell&#39;IDE e l&#39;aggiunta o la rimozione di endpoint da un servizio

**Lettura servizio:** Leggi tutti i servizi del sistema. Ciò include tutti i processi e le varianti di processo

**SERVICE_AGENT_PERM:** Visualizzare i dati e interagire con le istanze di processo per un servizio creato da un processo

**SERVICE_MANAGER_PERM:** Eseguire il bilanciamento del carico e altre azioni amministrative su un servizio creato da un processo

**START_STOP_PERM:** Avviare o interrompere un servizio

**SUPERVISOR_PERM:** Visualizzare i dati dell&#39;istanza del processo per un servizio creato da un processo

**Viaggio:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**Scrivi:** Scrivere metadati e contenuti dell&#39;archivio

**Apertura di file in Workbench**

Per visualizzare il contenuto della visualizzazione Risorse in Workbench e aprire i file da visualizzare, un utente richiede le seguenti autorizzazioni:

* Lettura archivio
* Percorso archivio
* Richiamo del servizio
* Lettura servizio

## Rimuovere un utente o un gruppo da un ruolo {#remove-a-user-or-group-from-a-role}

Utilizza la pagina Gestione dei ruoli per rimuovere utenti e gruppi da un particolare ruolo. Se l&#39;utente o il gruppo ha ereditato l&#39;assegnazione di ruolo, non è possibile rimuovere il ruolo a livello di utente o gruppo. Rimuovere l&#39;utente o il gruppo dalla struttura di ereditarietà o rimuovere il ruolo dal padre.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo vengono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizza l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nell’elenco dei ruoli, fai clic sul nome del ruolo da aggiornare, quindi fai clic sulla scheda Utenti ruolo . Viene visualizzato un elenco di utenti e gruppi associati al ruolo .
1. Selezionare le caselle di controllo relative agli utenti e ai gruppi da rimuovere dal ruolo e fare clic su Annulla assegnazione.
1. Fare clic su Salva e quindi su OK.
