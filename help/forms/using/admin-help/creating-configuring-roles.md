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
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 0%

---


# Creazione e configurazione di ruoli{#creating-and-configuring-roles}

Utilizzando le pagine Web Gestione utente, potete associare utenti e gruppi a ruoli che fanno già parte del database Gestione utente. È inoltre possibile creare, modificare ed eliminare ruoli.

Gestione utente ha due tipi di ruoli:

**Ruoli eseguibili:** questo tipo di ruolo può essere modificato ed eliminato e le autorizzazioni per i ruoli possono essere aggiunte ed eliminate da questi tipi di ruolo. I ruoli creati vengono considerati come ruolo modificabile. Potete aggiungere o rimuovere utenti e gruppi assegnati a ruoli modificabili.

**Ruoli immutabili:** i ruoli predefiniti inclusi con Gestione utente sono immutabili. Questi ruoli non possono essere modificati o eliminati. Tuttavia, potete aggiungere o rimuovere utenti e gruppi assegnati a ruoli immutabili.

I ruoli modificabili e immutabili possono essere creati anche tramite le API dei moduli AEM.

## Ruoli predefiniti {#default-roles}

I seguenti ruoli predefiniti sono inclusi nel database Gestione utente.

**console di amministrazione Utente:** può accedere alla console di amministrazione.

**Amministratore applicazione:** può utilizzare tutte le funzioni di Workbench. È possibile utilizzare le pagine Applicazioni e Servizi nella console di amministrazione per configurare le proprietà di esecuzione, gli endpoint e la protezione del servizio.

**AEM moduli Amministratore:** può eseguire tutte le attività per tutti i servizi installati.

**Amministratore di sicurezza:** controlla le impostazioni di gestione utenti e gestisce gli utenti e i gruppi associati a qualsiasi dominio di User Manager

**Utente servizi:** può visualizzare e richiamare qualsiasi servizio

**Amministratore avanzato:** dispone dell&#39;accesso a tutte le funzionalità amministrative del sistema, compresi i servizi

**Amministratore trust:** può gestire le impostazioni di attendibilità PKI e le credenziali PKI gestite dalla pagina Gestione archivio attendibili nella console di amministrazione

### Altri ruoli predefiniti {#additional-default-roles}

I seguenti ruoli predefiniti aggiuntivi possono essere inclusi, a seconda dei componenti dei moduli AEM installati

**Utente applicazione di caricamento del documento:** può caricare documenti tramite Flex Remoting.

**Amministratore Forms:** può visualizzare e modificare le impostazioni dalla pagina Forms in Admin Console

**AEM moduli Contentspace Administrator:** È possibile visualizzare e modificare le impostazioni dalla pagina Content Services (obsoleto) nella console di amministrazione

**AEM moduli Contentspace Utente:** Può accedere alle pagine Web Contentspace (obsoleto)

**Amministratore del connettore Documentum:** È possibile visualizzare e modificare le impostazioni dalla pagina Connettore per EMC Documentum nella console di amministrazione

**AEM moduli FileNet Connector Administrator:** È possibile visualizzare e modificare le impostazioni dalla pagina Connettore per IBM FileNet nella console di amministrazione

**AEM moduli amministratore del connettore IBM CM:** È possibile visualizzare e modificare le impostazioni dalla pagina Connettore per IBM Content Manager nella console di amministrazione

**Amministratore Rights Management:** esegue tutte le attività necessarie per tutte le configurazioni server nelle relative pagine del Rights Management

**Rights Management utente finale:** può accedere alle pagine Web dell&#39;utente finale del Rights Management

**Rights Management Invita utente:** può invitare gli utenti

**Gestione Rights Management utenti invitati e locali:** può eseguire le attività necessarie per gestire tutti gli utenti invitati e locali nelle relative pagine del Rights Management

**Amministratore set di criteri di Rights Management:** esegue tutte le attività richieste per tutti i set di criteri nelle pagine di Rights Management rilevanti

**Rights Management Amministratore avanzato:** esegue tutte le attività richieste dalla pagina del Rights Management

**AEM moduli Amministratore area di lavoro:** È possibile visualizzare e modificare le impostazioni dalla pagina Area di lavoro nella console di amministrazione

***nota **: Flex Workspace è obsoleto per AEM rilascio di moduli.*

**Utente di Workspace:** può accedere all’applicazione per l’utente finale di Workspace

**Amministratore di output:** può visualizzare e modificare le impostazioni dalla pagina Output nella console di amministrazione

**Amministratore PDFG:** È possibile visualizzare e modificare le impostazioni dalla pagina Generatore PDF nella console di amministrazione

**Utente PDFG:** Può accedere a tutte le funzionalità non amministrative per PDF Generator

**Applicazione Web estensioni Acrobat Reader DC:** Uso dell&#39;applicazione Web estensioni Acrobat Reader DC

>[!NOTE]
>
>Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine Web degli utenti finali di Workspace per motivi di sicurezza. Poiché queste pagine possono esistere all&#39;esterno di un firewall, l&#39;autorizzazione delle attività a livello di amministrazione potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei moduli AEM Amministratore di Workspace o AEM I privilegi Utente di Workspace possono accedere alle pagine Web dell&#39;utente finale di Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM rilascio di moduli.

## Creare un ruolo {#create-a-role}

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

## Modifica autorizzazioni ruolo {#change-role-permissions}

Potete modificare le autorizzazioni per uno qualsiasi dei ruoli creati. Non è possibile modificare le autorizzazioni per i ruoli predefiniti dei moduli AEM inclusi nel prodotto.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo sono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizzate l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Selezionate il ruolo per il quale visualizzare le autorizzazioni e fate clic sulla scheda Autorizzazioni.
1. Per modificare queste autorizzazioni, fate clic su Trova autorizzazioni, selezionate le caselle di controllo relative alle autorizzazioni da aggiungere al ruolo, fate clic su OK, quindi su Salva.
1. Per eliminare un&#39;autorizzazione, selezionate l&#39;autorizzazione, fate clic su Elimina, quindi fate clic su Salva.

### AEM autorizzazioni dei moduli {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** aggiungere, rimuovere e modificare gli endpoint per un servizio

**Admin Console Accesso:** visualizzare la console di amministrazione

**Modifica certificato:** modificare le impostazioni di attendibilità di qualsiasi certificato nell&#39;archivio certificati

**Lettura certificato:** lettura di qualsiasi certificato nell&#39;archivio certificati attendibili

**Scrittura certificato:** aggiungere un certificato all&#39;archivio certificati

**Componente Aggiungi:** Installare un nuovo componente nel sistema

**Eliminazione componente:** Eliminare qualsiasi componente del sistema

**Lettura componente:** Leggere qualsiasi componente del sistema

**Contentspace Administrator:** Permission for Contentspace (obsoleto) Administrator

**Accesso alla console Contentspace:** Autorizzazione per accesso alla console Contentspace (obsoleto)

**Controllo delle impostazioni di base:** gestire le impostazioni nella pagina Impostazioni di sistema di base nella console di amministrazione

**CREATE_VERSION_PERM:** Creare una nuova versione di un servizio

**Modifica credenziali:** modificare le credenziali di firma nell&#39;archivio attendibili

**Lettura credenziali:** lettura delle credenziali di firma nell&#39;archivio certificati

**Scrittura credenziali:** aggiungere una credenziale di firma all&#39;archivio certificati

**Modifica CRL:** modificare qualsiasi CRL (elenco di revoca dei certificati) nell&#39;archivio certificati

**Lettura CRL:** lettura di un CRL nell&#39;archivio certificati

**Scrittura CRL:** aggiungere un CRL all&#39;archivio certificati

**Delega:** impostare un ACL su una risorsa

**DELETE_VERSION_PERM:** Eliminare una versione di un servizio

**Caricamento documento:** Caricare documenti nei moduli AEM

**Controllo del dominio:** creare, eliminare o modificare le impostazioni per qualsiasi dominio di Gestione utenti, inclusi i provider di autenticazione e directory

**Tipo evento Modifica:** Modifica ai tipi di evento

**Controllo rappresentazione identità:** Impersona identità in User Manager

**INVOKE_PERM:** richiamare tutte le operazioni su un servizio

**LCDS Data Model Control:** lettura e implementazione di modelli di dati in Data Services

**Aggiornamento di License Manager:informazioni** sulle licenze di aggiornamento

**MODIFY_CONFIG_PERM:** Modificare la configurazione di un servizio

**MODIFICA** DELLA VERSIONE DI UN SERVIZIO

**PDFGAdminPermission:amministratore** PDFG

**PDFGUserPermission:utente** PDFG

**PERM_DCTM_ADMIN:amministratore del connettore** Documentum

**PERM_FILENET_ADMIN:amministratore del connettore** FileNet

**PERM_FORMS_ADMIN:amministratore** Forms

**PERM_IBMCM_ADMIN:amministratore del connettore** IBM CM

**PERM_OUTPUT_ADMIN:amministratore** di output

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Utilizzare l&#39;applicazione Web delle estensioni Acrobat Reader DC

**PERM_SP_ADMIN:impostazioni** Gestisci connettore SharePoint

**PERM_WORKSPACE_ADMIN:Impostazioni** Gestisci area di lavoro

**PERM_WORKSPACE_USER:** Accedere all’applicazione per l’utente finale di Workspace

**Controllo entità:** gestire utenti e gruppi per qualsiasi dominio e gestire le assegnazioni di ruoli per tutti gli utenti e i gruppi in qualsiasi dominio

**Registrazione di processo Lettura/Eliminazione:** Elenco e recupero delle istanze di controllo del flusso di lavoro

**PROCESS_OWNER_PERM:** visualizzare i dati delle tendenze ed eseguire azioni amministrative su un servizio creato da un processo

**Lettura:** Lettura del contenuto di una risorsa

**READ_PERM:** Leggere o visualizzare un servizio

**Rinnova asserzione:** Rinnova asserzioni in Gestione utente

**delegato archivio:** impostare un ACL su una risorsa

**Lettura archivio:** lettura del contenuto di una risorsa

**Percorso archivio:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**Scrittura archivio:** Scrittura dei metadati e del contenuto dell&#39;archivio

**Rights Management Modifica proprietario criterio:** Modifica proprietario criterio

**Accesso alla console utente finale del Rights Management:** accedere all’interfaccia utente finale del Rights Management

**Rights Management Gestisci configurazione:** Gestisci configurazione server

**Rights Management Gestisci utenti invitati e locali:** gestire gli utenti invitati e locali

**Rights Management Gestisci set di criteri:** gestire tutti i criteri e i documenti all&#39;interno di qualsiasi set di criteri

**Rights Management Criteri Imposta Aggiungi coordinatore:** Aggiungi, rimuovi e modifica le autorizzazioni per i coordinatori di set di criteri

**Set di criteri di Rights Management Crea criterio:** creare un nuovo criterio per un set di criteri

**Set di criteri di Rights Management Elimina criterio:** rimuovere un criterio da un set di criteri

**Set di criteri di Rights Management Modifica criterio:** modificare un criterio in un set di criteri

**Set di criteri di Rights Management Gestisci autore documento:** quando si creano i set di criteri, si assegna agli utenti il ruolo di autore del documento. L&#39;autore del documento è l&#39;utente che protegge il documento con un criterio.

**Set di criteri di Rights Management Rimuovi coordinatore:** rimuovere un coordinatore di set di criteri da un set di criteri

**Set di criteri di Rights Management Revoca documento:** Revoca dell&#39;accesso ai documenti in un set di criteri

**Rights Management Criteri di commutazione set:** Cambiare criteri per un documento

**Rights Management impostazione criterio Annulla revoca documento:** Annullamento della revoca di un documento

**Evento visualizzazione set di criteri di Rights Management:** visualizzare eventi di criteri e documenti per qualsiasi criterio o documento all&#39;interno di un set di criteri

**Rights Management Visualizza eventi server:** cercare e visualizzare tutti gli eventi di controllo

**Controllo dei ruoli:** creare, eliminare e modificare i ruoli in Gestione utente

**Attivazione del servizio:** avvio di qualsiasi servizio, rendendolo disponibile per la chiamata

**Aggiungi servizio:** distribuisci un nuovo servizio nel Registro di sistema del servizio. Ciò include l&#39;aggiunta di nuovi processi e varianti di processo

**Disattivazione del servizio:** arresto di qualsiasi servizio nel sistema

**Eliminazione del servizio:** Eliminare qualsiasi servizio nel sistema, inclusi processi e varianti di processo

**Chiamata del servizio:** richiamare qualsiasi servizio nel Registro di sistema del servizio disponibile in fase di esecuzione

**Modifica servizio:** modifica le proprietà di configurazione di qualsiasi servizio del sistema. Ciò include il blocco e lo sblocco di un servizio nell&#39;IDE, nonché l&#39;aggiunta o la rimozione di endpoint da un servizio

**Lettura del servizio:** lettura di tutti i servizi del sistema. Questo include tutti i processi e le varianti di processo

**SERVICE_AGENT_PERM:** visualizzare i dati e interagire con le istanze di processo per un servizio creato da un processo

**SERVICE_MANAGER_PERM:** eseguire il bilanciamento del carico e altre azioni amministrative su un servizio creato da un processo

**START_STOP_PERM:** Avviare o arrestare un servizio

**SUPERVISOR_PERM:** visualizzare i dati delle istanze del processo per un servizio creato da un processo

**Navigazione:** Includere una risorsa in una richiesta di risorse elenco o leggere i metadati di una risorsa

**scrittura:** scrittura di metadati e contenuto dell&#39;archivio

**Apertura di file in Workbench**

Per visualizzare il contenuto della visualizzazione Risorse in Workbench e aprire i file per la visualizzazione, l&#39;utente richiede le seguenti autorizzazioni:

* Lettura archivio
* Percorso archivio
* Chiamata al servizio
* Lettura servizio

## Rimuovere un utente o un gruppo da un ruolo {#remove-a-user-or-group-from-a-role}

Utilizzate la pagina Gestione ruolo per rimuovere utenti e gruppi da un ruolo specifico. Se l’utente o il gruppo ha ereditato l’assegnazione del ruolo, non è possibile rimuovere il ruolo a livello di utente o gruppo. Rimuovere l&#39;utente o il gruppo dalla struttura di ereditarietà oppure rimuovere il ruolo dall&#39;elemento padre.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nome ruolo.

   Per impostazione predefinita, nella pagina Gestione ruolo sono visualizzati tutti i ruoli del database Gestione utente. Se l’elenco dei ruoli è grande, utilizzate l’area Trova nella parte superiore della pagina per cercare un nome di ruolo specifico.

1. Nell&#39;elenco dei ruoli, fate clic sul nome del ruolo da aggiornare, quindi fate clic sulla scheda Utenti ruolo. Viene visualizzato un elenco di utenti e gruppi associati al ruolo.
1. Selezionate le caselle di controllo che gli utenti e i gruppi devono rimuovere dal ruolo e fate clic su Annulla assegnazione.
1. Fate clic su Salva, quindi su OK.

