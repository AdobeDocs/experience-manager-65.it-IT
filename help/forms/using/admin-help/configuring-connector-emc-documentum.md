---
title: Configurazione del connettore per EMC Documentum
description: Scopri come configurare il connettore per EMC Documentum per consentire la comunicazione tra AEM Forms ed EMC Documentum.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1032'
ht-degree: 100%

---

# Configurazione del connettore per EMC Documentum {#configuring-connector-for-emc-documentum}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il connettore per EMC Documentum consente la comunicazione tra AEM Forms ed EMC Documentum. Per ulteriori informazioni di base, consulta “Connettori per ECM” in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

L’impostazione del connettore per EMC Documentum comporta la configurazione della connessione al server e delle credenziali dell’archivio.

>[!NOTE]
>
>Nelle versioni precedenti, le risorse potevano essere salvate in un archivio ECM. Nella versione corrente, le risorse vengono salvate nell’archivio nativo di AEM Forms e i servizi del provider dell’archivio sono diventati obsoleti. La migrazione delle risorse da un archivio ECM all’archivio AEM Forms viene eseguita quando esegui un aggiornamento ad AEM Forms. Per ulteriori informazioni, consulta la Guida all’aggiornamento di AEM Forms per il server applicazioni in uso.

## Configurazione della connessione al server {#configuring-the-server-connection}

Questa sezione descrive le attività di Connector per EMC Documentum che puoi eseguire nella pagina Impostazioni di configurazione.

>[!NOTE]
>
>Se stai configurando tutte le impostazioni contemporaneamente, fai clic una sola volta su Salva.

### Configurare il server {#configure-the-server}

È necessario configurare le informazioni sul server di gestione della connessione. Queste informazioni sono necessarie per il collegamento agli archivi dei contenuti Documentum e avviare il connettore per EMC Documentum.

1. Nella console di amministrazione, fai clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell’area Informazioni configurazione Documentum inserisci il nome host o l’indirizzo IP e il numero di porta del gestore della connessione. Il numero di porta deve essere un numero intero positivo, ad esempio 1489.
1. Fai clic su Salva.

### Configurare le credenziali dell’entità principale {#configure-principal-credentials}

Quando configuri le credenziali principali, il nome dell’archivio fornito dipende dal fatto che durante l’accesso venga fornito un nome di archivio esplicito.

Se inserisci un nome utente o una password errati, otterrai i seguenti risultati, a seconda del fatto che il servizio sia attualmente in esecuzione o meno:

* Se il servizio provider di archivio EMC Documentum e il servizio connettore dell’archivio EMC Documentum Content vengono interrotti, quando salvi le informazioni di configurazione del servizio, non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un’eccezione e il servizio non verrà avviato.
* Se il servizio provider di archivio EMC Documentum o il servizio connettore dell’archivio EMC Documentum Content sono avviati, quando salvi le informazioni di configurazione del servizio, il servizio tenta immediatamente di convalidare le informazioni relative alle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

1. Nella console di amministrazione, fai clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell’area Informazioni sulle credenziali dell’entità Documentum digita il nome utente e la password di un utente con privilegi di amministratore privilegiato.
1. Se durante l’accesso non fornisci un nome di archivio esplicito, inserisci il nome dell’archivio a cui sono associate le credenziali.
1. Fai clic su Salva.

### Modificare il provider di servizi di archivio {#change-the-repository-service-provider}

Puoi configurare il provider di servizi di archivio da utilizzare con Documentum. Le chiamate al servizio dell’archivio sono delegate al provider configurato. Sono disponibili le seguenti opzioni:

**Nome del provider del servizio di archivio corrente:** il nome del provider del servizio di archivio corrente

**Provider di archivio ECM Documentum:** imposta il provider dell’archivio Documentum come provider di archivio. Questa opzione è stata dichiarata obsoleta

**Provider di archivio:** imposta il provider dell’archivio nativo come provider di archivio

>[!NOTE]
>
>Per selezionare un provider di servizi di archivio diverso da quelli elencati, configura RepositoryService in Applicazioni e servizi > Gestione servizi. <!-- Fix broken link (See Managing Services) -->.

1. Nella console di amministrazione, fai clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell’area Informazioni provider di servizi di archivio seleziona il provider di servizi di archivio alternativo.
1. Fai clic su Salva.

## Configurazione delle credenziali dell’archivio {#configuring-repository-credentials}

Le informazioni sulle credenziali Documentum vengono utilizzate nel contesto del sistema AEM Forms. Le credenziali dell’archivio sono specifiche per determinati archivi in Documentum. Puoi fornire le credenziali per un numero qualsiasi di archivi; tuttavia, è possibile specificare un solo set di credenziali per archivio.

### Aggiungere credenziali archivio {#add-a-repository-credential}

1. Nella console di amministrazione fai clic su Servizi > Connettore di EMC Documentum > Impostazioni delle credenziali dell’archivio.
1. Fai clic su Aggiungi. Viene visualizzata la pagina Informazioni sulle credenziali del sistema Documentum.
1. Inserisci un nome per l’archivio.
1. Inserisci un nome utente e una password.
1. Fai clic su Salva.

Se il connettore dell’archivio dei contenuti per EMC Documentum e/o il servizio dell’archivio per EMC Documentum sono in esecuzione, le informazioni sulle credenziali vengono verificate rispetto all’archivio specificato prima di essere memorizzate nel database. Se le credenziali non sono valide o sono presenti, viene visualizzato un messaggio di errore.

### Rimuovere le credenziali di un archivio {#remove-a-repository-credential}

1. Nella console di amministrazione, fai clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Seleziona la casella di controllo accanto all’archivio da cui rimuovere le credenziali e fai clic su Rimuovi. Le credenziali per l’archivio selezionato vengono rimosse dal database.

### Modificare il nome utente e la password per le credenziali di un archivio {#change-the-user-name-and-password-for-a-repository-credential}

1. Nella console di amministrazione, fai clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Fai clic sul nome dell’archivio per cui modificare le credenziali.
1. Modifica il nome utente o la password dell’archivio o entrambi (il nome dell’archivio è di sola lettura).
1. Fai clic su Salva.

Se il connettore dell’archivio dei contenuti per EMC Documentum e/o il servizio dell’archivio per EMC Documentum sono in esecuzione, le informazioni sulle credenziali vengono verificate rispetto all’archivio specificato prima di essere memorizzate nel database. Se le credenziali non sono valide o sono presenti, viene visualizzato un messaggio di errore.

## Abilitare la richiesta di condivisione delle code di attività di Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Sono necessari alcuni passaggi manuali per garantire il corretto funzionamento della funzione Richiesta di condivisione della coda delle attività in Workspace con il connettore di EMC Documentum.

1. Dopo aver distribuito AEM Forms e installato Workbench, accedi a Workbench e apri la vista Risorse. Da questa vista potrai determinare dove si trova il file QueueSharing.swf.
1. Trascina il file QueueSharing.swf dalla vista Risorse al desktop di Windows o in una posizione equivalente, a seconda del sistema operativo in uso.
1. Nella console di amministrazione, fai clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nella sezione Informazioni sul provider del servizio di archivio modifica il provider dell’archivio configurato nel provider dell’archivio di EMC Documentum.
1. Avvia Workbench e copia il file QueueSharing.swf dalla posizione in cui lo hai copiato originariamente (ad esempio il desktop di Windows o un’altra posizione) in una directory esistente all’interno dell’archivio di EMC Documentum.
1. Nella vista Processi di Workbench apri il processo di condivisione della coda.
1. Nella vista Variabili apri le proprietà della variabile “theForm” e modifica l’URI in modo che corrisponda al percorso in cui hai inserito il file QueueSharing.swf al passaggio 5.
1. Salva il processo.
1. Esegui la migrazione dl processo all’ambiente di produzione in base ai criteri della tua organizzazione.
