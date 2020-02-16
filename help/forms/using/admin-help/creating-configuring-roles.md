---
title: Creazione e configurazione di ruoli
seo-title: Creazione e configurazione di ruoli
description: Scoprite come associare utenti e gruppi a ruoli che fanno già parte del database Gestione utente. È inoltre possibile creare, modificare ed eliminare ruoli.
seo-description: Scoprite come associare utenti e gruppi a ruoli che fanno già parte del database Gestione utente. È inoltre possibile creare, modificare ed eliminare ruoli.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Creazione e configurazione di ruoli{#creating-and-configuring-roles}

Utilizzando le pagine Web Gestione utente, potete associare utenti e gruppi a ruoli che fanno già parte del database Gestione utente. È inoltre possibile creare, modificare ed eliminare ruoli.

Gestione utente ha due tipi di ruoli:

**** Ruoli eseguibili: Questo tipo di ruolo può essere modificato ed eliminato e le autorizzazioni per i ruoli possono essere aggiunte ed eliminate da questi tipi di ruolo. I ruoli creati vengono considerati come ruolo modificabile. Potete aggiungere o rimuovere utenti e gruppi assegnati a ruoli modificabili.

**** Ruoli immutabili: I ruoli predefiniti inclusi con Gestione utente sono ruoli immutabili. Questi ruoli non possono essere modificati o eliminati. Tuttavia, potete aggiungere o rimuovere utenti e gruppi assegnati a ruoli immutabili.

È inoltre possibile creare ruoli modificabili e immutabili tramite le API dei moduli AEM.

## Ruoli predefiniti {#default-roles}

I seguenti ruoli predefiniti sono inclusi nel database Gestione utente.

**** console di amministrazione Utente: Può accedere alla console di amministrazione.

**** Amministratore applicazione: Può utilizzare tutte le funzioni di Workbench. È possibile utilizzare le pagine Applicazioni e Servizi nella console di amministrazione per configurare le proprietà di esecuzione, gli endpoint e la protezione del servizio.

**** Amministratore moduli AEM: Può eseguire tutte le attività per tutti i servizi installati.

**** Amministratore protezione: Controlla le impostazioni di gestione utenti e gestisce utenti e gruppi associati a qualsiasi dominio di User Manager

**** Utente servizi: Può visualizzare e richiamare qualsiasi servizio

**** Amministratore avanzato: Ha accesso a tutte le funzionalità amministrative del sistema, compresi i servizi

**** Amministratore trust: È possibile gestire le impostazioni di attendibilità PKI e le credenziali PKI gestite dalla pagina Gestione store attendibile nella console di amministrazione

### Altri ruoli predefiniti {#additional-default-roles}

A seconda dei componenti AEM installati, possono essere inclusi i seguenti ruoli predefiniti aggiuntivi

**** Utente applicazione di caricamento documenti: Può caricare documenti utilizzando Flex Remoting.

**** Amministratore moduli: Può visualizzare e modificare le impostazioni dalla pagina Moduli nella console di amministrazione

**** AEM Forms Contentspace Administrator: Può visualizzare e modificare le impostazioni dalla pagina Content Services (obsoleto) nella console di amministrazione

**** AEM forms Contentspace User: Accesso alle pagine Web Contentspace (obsoleto)

**** Amministratore del connettore Documentum: È possibile visualizzare e modificare le impostazioni dalla pagina Connettore per EMC Documentum nella console di amministrazione

**** AEM Forms FileNet Connector Administrator: Può visualizzare e modificare le impostazioni dalla pagina Connettore per IBM FileNet nella console di amministrazione

**** AEM Forms IBM CM Connector Administrator: Può visualizzare e modificare le impostazioni dalla pagina Connector for IBM Content Manager nella console di amministrazione

**** Amministratore di Rights Management: Esegue tutte le attività richieste per tutte le configurazioni del server nelle pagine Rights Management pertinenti

**** Utente finale di Rights Management: Accesso alle pagine Web dell&#39;utente finale di Rights Management

**** Utente invito Rights Management: Può invitare gli utenti

**** Rights Management Manage Invitati e Utenti locali: Può eseguire le attività necessarie per gestire tutti gli utenti invitati e locali nelle relative pagine di Rights Management

**** Amministratore set di criteri di Rights Management: Esegue tutte le attività richieste per tutti i set di criteri nelle relative pagine di Rights Management

**** Amministratore avanzato di Rights Management: Esegue tutte le attività richieste dalla pagina Rights Management

**** AEM Forms Workspace Administrator: Può visualizzare e modificare le impostazioni dalla pagina Area di lavoro nella console di amministrazione

***nota **:Flex Worksapce è obsoleto per la versione dei moduli AEM.*

**** Utente area di lavoro: Accesso all’applicazione per l’utente finale di Workspace

**** Amministratore di output: Può visualizzare e modificare le impostazioni dalla pagina Output nella console di amministrazione

**** Amministratore PDFG: Può visualizzare e modificare le impostazioni dalla pagina PDF Generator nella console di amministrazione

**** Utente PDFG: Può accedere a tutte le funzionalità non amministrative di PDF Generator

**** Applicazione Web con estensioni Acrobat Reader DC: Uso dell’applicazione Web con le estensioni Acrobat Reader DC

>[!NOTE]
>
>Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine Web degli utenti finali di Workspace per motivi di sicurezza. Poiché queste pagine possono esistere all&#39;esterno di un firewall, l&#39;autorizzazione delle attività a livello di amministrazione potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di amministratore di AEM Forms Workspace o di amministratore di AEM Workspace possono accedere alle pagine Web degli utenti finali di Workspace.

>[!NOTE]
>
>Flex Worksapce è obsoleto per la versione dei moduli AEM.

## Creazione di un ruolo {#create-a-role}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nuovo ruolo.
1. Nella casella Nome ruolo digitare un nome per il ruolo e, facoltativamente, digitare una descrizione del ruolo, quindi fare clic su Avanti.

   >[!NOTE]
   >
   >Quando si utilizza MySQL, non è possibile creare due ruoli con lo stesso nome ma con caratteri estesi diversi. Ad esempio, se si tenta di creare un ruolo denominato abcde quando esiste già un ruolo denominato âbcdè, si verifica un errore.

1. Fate clic su Trova autorizzazioni, selezionate le autorizzazioni da aggiungere al ruolo.
1. Fare clic su OK, quindi su Avanti.
1. Assegna questo ruolo a utenti e gruppi:

   * Fate clic su Trova utenti/gruppi.
   * Nella casella Trova, digitate i criteri di ricerca.
   * Selezionate Nome, E-mail o ID utente, quindi selezionate Utenti, Gruppi o Utenti e gruppi.
   * Selezionate il dominio, selezionate il numero di risultati da visualizzare e fate clic su Trova.
   * Selezionate le caselle di controllo relative agli utenti e ai gruppi a cui assegnare il ruolo e fate clic su OK.

1. Per visualizzare i dettagli utente e gruppo, selezionate l&#39;entità.
1. Fare clic su OK, quindi su Fine.

## Modifica di un ruolo {#edit-a-role}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo sono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizzate l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Fate clic sul ruolo da modificare, modificate le impostazioni generali e fate clic su Salva.
1. Per modificare le autorizzazioni dei ruoli, fate clic sulla scheda Autorizzazioni ed effettuate le seguenti operazioni:

   * Per aggiungere nuove autorizzazioni, fate clic su Trova autorizzazioni, selezionate le caselle di controllo relative alle autorizzazioni da aggiungere, fate clic su OK, quindi su Salva.
   * Per eliminare un&#39;autorizzazione dal ruolo, selezionate la casella di controllo per l&#39;autorizzazione, fate clic su Elimina, quindi su Salva.

1. Per gestire il ruolo assegnato, fare clic sulla scheda Utenti ruolo ed effettuare le seguenti operazioni:

   * Per assegnare il ruolo a nuovi utenti e gruppi, fate clic su Trova utenti/gruppi e completate la ricerca. Selezionate la casella di controllo per ciascun utente e gruppo a cui assegnare il ruolo, fate clic su OK, quindi su Salva.
   * Per rimuovere il ruolo, selezionate la casella di controllo relativa agli utenti o al gruppo, fate clic su Annulla assegnazione e quindi su Salva.

## Eliminare un ruolo {#delete-a-role}

È possibile eliminare uno qualsiasi dei ruoli creati, ma non i ruoli predefiniti dei moduli AEM inclusi nel prodotto.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo sono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizzate l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Selezionate la casella di controllo relativa al ruolo da eliminare, fate clic su Elimina, quindi su OK.

## Assegnazione di un ruolo a utenti e gruppi {#assign-a-role-to-users-and-groups}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificate le informazioni per limitare la ricerca e fate clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Potete ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Selezionate le caselle accanto agli utenti e ai gruppi da associare a un ruolo e fate clic su Assegna ruolo.
1. Selezionate il ruolo da assegnare all’utente o al gruppo e fate clic su OK.

È inoltre possibile assegnare i ruoli utilizzando la pagina Gestione ruolo.

## Determinare chi è assegnato a un ruolo {#determine-who-is-assigned-to-a-role}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo sono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizzate l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nella pagina Dettagli ruolo, fate clic sulla scheda Utenti ruolo. Viene visualizzato un elenco di utenti e gruppi che sono direttamente associati al ruolo.

## Modifica delle autorizzazioni per i ruoli {#change-role-permissions}

Potete modificare le autorizzazioni per uno qualsiasi dei ruoli creati. Non è possibile modificare le autorizzazioni per i ruoli predefiniti dei moduli AEM inclusi nel prodotto.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo sono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizzate l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Selezionate il ruolo per il quale visualizzare le autorizzazioni e fate clic sulla scheda Autorizzazioni.
1. Per modificare queste autorizzazioni, fate clic su Trova autorizzazioni, selezionate le caselle di controllo relative alle autorizzazioni da aggiungere al ruolo, fate clic su OK, quindi su Salva.
1. Per eliminare un&#39;autorizzazione, selezionate l&#39;autorizzazione, fate clic su Elimina, quindi fate clic su Salva.

### Autorizzazioni per i moduli AEM {#aem-forms-permissions}

**** ADD_REMOVE_ENDPOINT_PERM: Aggiunta, rimozione e modifica di endpoint per un servizio

**** Login Admin Console: Visualizzare la console di amministrazione

**** Modifica certificato: Modificare le impostazioni di attendibilità di qualsiasi certificato nell&#39;archivio attendibili

**** Lettura certificato: Lettura di qualsiasi certificato nell&#39;archivio certificati

**** Scrittura certificato: Aggiunta di un certificato all&#39;archivio certificati

**** Aggiungi componente: Installare un nuovo componente nel sistema

**** Eliminazione componente: Eliminare qualsiasi componente nel sistema

**** Lettura componente: Leggere qualsiasi componente del sistema

**** Amministratore Contentspace: Autorizzazione per l&#39;amministratore di Contentspace (obsoleto)

**** Accesso alla console Contentspace: Autorizzazione per l&#39;accesso alla console Contentspace (obsoleto)

**** Controllo delle impostazioni principali: Gestione delle impostazioni nella pagina Impostazioni di sistema di base nella console di amministrazione

**** CREATE_VERSION_PERM: Creare una nuova versione di un servizio

**** Modifica credenziali: Modifica delle credenziali di firma nell&#39;archivio attendibili

**** Lettura credenziali: Leggere qualsiasi credenziale di firma nell&#39;archivio attendibili

**** Scrittura credenziali: Aggiunta di una credenziale di firma all&#39;archivio certificati

**** Modifica CRL: Modificare qualsiasi CRL (Elenco Revoca certificati) nell&#39;archivio attendibili

**** Lettura CRL: Leggere qualsiasi CRL nell&#39;archivio certificati

**** Scrittura CRL: Aggiungere un CRL all&#39;archivio certificati

**** Delega: Impostare un ACL su una risorsa

**** DELETE_VERSION_PERM: Eliminare una versione di un servizio

**** Caricamento documento: Caricare i documenti nei moduli AEM

**** Controllo dominio: Creare, eliminare o modificare le impostazioni per qualsiasi dominio di gestione utenti, inclusi i provider di autenticazione e directory

**** Modifica tipo evento: Modifica ai tipi di evento

**** Controllo rappresentazione identità: Impersona identità in User Manager

**** INVOKE_PERM: Richiamo di tutte le operazioni su un servizio

**** Controllo modello dati LCDS: Lettura e implementazione di modelli di dati in Data Services

**** Aggiornamento di License Manager: Aggiornamento delle informazioni sulla licenza

**** MODIFY_CONFIG_PERM: Modificare la configurazione di un servizio

**TERMINE** Modifica della versione di un servizio

**** PDFGAdminPermission: Amministratore PDFG

**** PDFGUserPermission: Utente PDFG

**** PERM_DCTM_ADMIN: Amministratore Documentum Connector

**** PERM_FILENET_ADMIN: Amministratore del connettore FileNet

**** PERM_FORMS_ADMIN: Amministratore Forms

**** PERM_IBMCM_ADMIN: Amministratore del connettore IBM CM

**** PERM_OUTPUT_ADMIN: Amministratore di Output

**** PERM_READER_EXTENSIONS_WEB_APPLICATION: Utilizzo dell’applicazione Web con le estensioni Acrobat Reader DC

**** PERM_SP_ADMIN: Gestione impostazioni connettore SharePoint

**** PERM_WORKSPACE_ADMIN: Gestione impostazioni Workspace

**** PERM_WORKSPACE_USER: Accedere all’applicazione per l’utente finale Workspace

**** Controllo principale: Gestione di utenti e gruppi per qualsiasi dominio e gestione delle assegnazioni di ruoli per tutti gli utenti e i gruppi in qualsiasi dominio

**** Lettura/eliminazione della registrazione di processo: Elenca e recupera le istanze di controllo del flusso di lavoro

**** PROCESS_OWNER_PERM: Visualizzare i dati di tendenza ed eseguire azioni amministrative su un servizio creato da un processo

**** Leggi: Lettura del contenuto di una risorsa

**** READ_PERM: Lettura o visualizzazione di un servizio

**** Rinnova asserzione: Rinnova asserzioni in Gestione utente

**** Delegato repository: Impostare un ACL su una risorsa

**** Lettura archivio: Lettura del contenuto di una risorsa

**** Percorso archivio: Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**** Scrittura archivio: Scrivere metadati e contenuto dell&#39;archivio

**** Proprietario criteri di modifica di Rights Management: Cambia proprietario criterio

**** Login alla console utente finale di Rights Management: Accesso all&#39;interfaccia utente finale di Rights Management

**** Configurazione di Rights Management Manage: Gestisci configurazione server

**** Rights Management Manage Invitati e Utenti locali:Gestione degli utenti invitati e locali

**** Set di criteri di gestione di Rights Management: Gestisci tutti i criteri e i documenti all&#39;interno di qualsiasi set di criteri

**** Coordinatore Aggiungi set di criteri di gestione diritti: Aggiunta, rimozione e modifica delle autorizzazioni per i coordinatori di set di criteri

**** Criteri di creazione set di criteri di Rights Management: Creare un nuovo criterio per un set di criteri

**** Criteri di eliminazione set di criteri di Rights Management: Rimozione di un criterio da un set di criteri

**** Criteri di modifica set di criteri di Rights Management: Modificare un criterio in un set di criteri

**** Rights Management Policy Set Manage Document Publisher:Quando create dei set di criteri, assegnate agli utenti il ruolo di autore del documento. L&#39;autore del documento è l&#39;utente che protegge il documento con un criterio.

**** Rights Management Policy Set Remove Coordinator: Rimozione di un coordinatore di set di criteri da un set di criteri

**** Il set di criteri di Rights Management Revoca documento: Revoca dell&#39;accesso ai documenti in un set di criteri

**** Criteri di modifica set di criteri di Rights Management: Cambiare i criteri per un documento

**** Criterio Rights Management: Annulla revoca documento: Annullamento della revoca di un documento

**** Evento di visualizzazione set di criteri di Rights Management: Visualizzare gli eventi dei criteri e dei documenti per qualsiasi criterio o documento all&#39;interno di un set di criteri

**** Eventi del server Rights Management View: Cerca e visualizza tutti gli eventi di controllo

**** Controllo ruolo: Creazione, eliminazione e modifica di ruoli in Gestione utente

**** Attivazione servizio: Avviate qualsiasi servizio, rendendolo disponibile per la chiamata

**** Service Add: Implementare un nuovo servizio nel registro di sistema del servizio. Ciò include l&#39;aggiunta di nuovi processi e varianti di processo

**** Disattivazione del servizio: Arrestare qualsiasi servizio nel sistema

**** Eliminazione servizio: Eliminare qualsiasi servizio nel sistema, compresi processi e varianti di processo

**** Chiamata del servizio: Richiama qualsiasi servizio nel Registro di sistema del servizio disponibile in fase di esecuzione

**** Modifica servizio: Modificate le proprietà di configurazione di qualsiasi servizio del sistema. Ciò include il blocco e lo sblocco di un servizio nell&#39;IDE, nonché l&#39;aggiunta o la rimozione di endpoint da un servizio

**** Lettura servizio: Leggere tutti i servizi del sistema. Questo include tutti i processi e le varianti di processo

**** SERVICE_AGENT_PERM: Visualizzare i dati e interagire con le istanze di processo per un servizio creato da un processo

**** SERVICE_MANAGER_PERM: Eseguire il bilanciamento del carico e altre azioni amministrative su un servizio creato da un processo

**** START_STOP_PERM: Avviare o arrestare un servizio

**** SUPERVISOR_PERM: Visualizzare i dati dell&#39;istanza del processo per un servizio creato da un processo

**** Traverso: Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**** Scrivi: Scrivere metadati e contenuto dell&#39;archivio

**Apertura di file in Workbench**

Per visualizzare il contenuto della visualizzazione Risorse in Workbench e aprire i file per la visualizzazione, l&#39;utente richiede le seguenti autorizzazioni:

* Lettura archivio
* Percorso archivio
* Chiamata del servizio
* Lettura servizio

## Rimozione di un utente o un gruppo da un ruolo {#remove-a-user-or-group-from-a-role}

Utilizzate la pagina Gestione ruolo per rimuovere utenti e gruppi da un ruolo specifico. Se l’utente o il gruppo ha ereditato l’assegnazione del ruolo, non è possibile rimuovere il ruolo a livello di utente o gruppo. Rimuovere l&#39;utente o il gruppo dalla struttura di ereditarietà oppure rimuovere il ruolo dall&#39;elemento padre.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo sono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizzate l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nell&#39;elenco dei ruoli, fate clic sul nome del ruolo da aggiornare, quindi fate clic sulla scheda Utenti ruolo. Viene visualizzato un elenco di utenti e gruppi associati al ruolo.
1. Selezionate le caselle di controllo che gli utenti e i gruppi devono rimuovere dal ruolo e fate clic su Annulla assegnazione.
1. Fate clic su Salva, quindi su OK.

