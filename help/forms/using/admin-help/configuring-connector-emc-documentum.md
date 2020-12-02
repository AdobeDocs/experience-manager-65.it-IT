---
title: Configurazione del connettore per EMC Documentum
seo-title: Configurazione del connettore per EMC Documentum
description: Informazioni su come configurare il connettore per EMC Documentum per consentire la comunicazione tra AEM moduli e EMC Documentum.
seo-description: Informazioni su come configurare il connettore per EMC Documentum per consentire la comunicazione tra AEM moduli e EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 1%

---


# Configurazione del connettore per EMC Documentum {#configuring-connector-for-emc-documentum}

Il connettore per EMC Documentum consente la comunicazione tra i moduli AEM e EMC Documentum. Per ulteriori informazioni, vedere &quot;Connettori per l&#39;ECM&quot; in [Guida di riferimento dei servizi](https://www.adobe.com/go/learn_aemforms_services_63).

La configurazione del connettore per EMC Documentum comporta la configurazione della connessione del server e delle credenziali del repository.

>[!NOTE]
>
>Nelle versioni precedenti, le risorse potevano essere memorizzate in un repository ECM. Nella versione corrente, le risorse sono memorizzate nell&#39;archivio nativo dei moduli AEM e i servizi di Provider dell&#39;archivio sono stati dichiarati obsoleti. La migrazione delle risorse da un archivio ECM all&#39;archivio dei moduli AEM viene eseguita quando si esegue un aggiornamento ai moduli AEM. Per ulteriori informazioni, vedere la guida all&#39;aggiornamento dei moduli AEM per il server delle applicazioni.

## Configurazione della connessione del server {#configuring-the-server-connection}

In questo argomento vengono descritte le attività relative al connettore per EMC Documentum che è possibile eseguire nella pagina Impostazioni di configurazione.

>[!NOTE]
>
>Se state configurando tutte le impostazioni contemporaneamente, è sufficiente fare clic su Salva una sola volta.

### Configurare il server {#configure-the-server}

È necessario configurare le informazioni sul server del broker di connessione. Queste informazioni sono necessarie per connettersi ai repository dei contenuti Documentum e per avviare il connettore per EMC Documentum.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni sulla configurazione di Documentum, immettere il nome host o l&#39;indirizzo IP e il numero di porta del broker di connessione. Il numero di porta deve essere un numero intero positivo (ad esempio, 1489).
1. Fate clic su Salva.

### Configurare le credenziali dell&#39;entità {#configure-principal-credentials}

Quando si configurano le credenziali dell&#39;entità, il nome dell&#39;archivio fornito dipende dal fatto che durante l&#39;accesso sia stato fornito un nome di repository esplicito.

Se immettete un nome utente o una password non corretta, otterrete i seguenti risultati, a seconda che il servizio sia attualmente in esecuzione:

* Se il servizio EMC Documentum Repository Provider e il servizio EMC Documentum Content Repository Connector vengono interrotti, al momento del salvataggio delle informazioni sulla configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un&#39;eccezione e il servizio non verrà avviato.
* Se si avvia il servizio EMC Documentum Repository Provider o il servizio EMC Documentum Content Repository Connector, al momento del salvataggio delle informazioni di configurazione del servizio il servizio tenta di convalidare immediatamente le informazioni delle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni sulle credenziali principali di Documentum, digitare il nome utente e la password di un utente con privilegi di super amministratore.
1. Se durante l&#39;accesso non viene fornito un nome di repository esplicito, immettete il nome di repository a cui sono associate le credenziali.
1. Fate clic su Salva.

### Modifica del provider del servizio directory archivio {#change-the-repository-service-provider}

È possibile configurare il provider del servizio repository da utilizzare con Documentum. Le chiamate al servizio repository sono delegate al provider configurato. Sono disponibili le seguenti opzioni:

**Nome provider di servizi repository corrente:** nome del provider di servizi repository corrente

**Fornitore di repository ECM Documentum:** rende il provider di repository Documentum il fornitore del repository. Questa opzione è stata rimossa

**provider del repository:** rende il provider del repository nativo il provider del repository

>[!NOTE]
>
>Per selezionare un provider di servizi di repository diverso da quelli elencati, configurare RepositoryService in Applicazioni e servizi > Gestione dei servizi. <!-- Fix broken link (See Managing Services) -->.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni su Repository Service Provider, selezionare il provider di servizi repository alternativo.
1. Fate clic su Salva.

## Configurazione delle credenziali del repository {#configuring-repository-credentials}

Le informazioni sulle credenziali Documentum vengono utilizzate nel contesto del sistema dei moduli AEM. Le credenziali del repository sono specifiche per i repository specifici in Documentum. È possibile fornire le credenziali per qualsiasi numero di repository; tuttavia, potete specificare un solo set di credenziali per repository.

### Aggiungere una credenziale archivio {#add-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni credenziali repository.
1. Fate clic su Aggiungi. Viene visualizzata la pagina Informazioni sulle credenziali del sistema Documentum.
1. Immettete un nome per la directory archivio.
1. Immettete un nome utente e una password.
1. Fate clic su Salva.

Se il connettore Content Repository per il servizio EMC Documentum e/o il servizio Repository per EMC Documentum sono in esecuzione, le informazioni sulle credenziali vengono verificate rispetto al repository specificato prima di essere archiviate nel database. Se le credenziali non sono valide o esistono, viene visualizzato un messaggio di errore.

### Rimuovere una credenziale del repository {#remove-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Selezionare la casella di controllo accanto all&#39;archivio da cui rimuovere le credenziali e fare clic su Rimuovi. Le credenziali per l&#39;archivio selezionato vengono rimosse dal database.

### Modificare il nome utente e la password di una credenziale dell&#39;archivio {#change-the-user-name-and-password-for-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Fare clic sul nome della directory archivio per cui modificare le credenziali.
1. Modificate il nome utente o la password dell’archivio oppure entrambi. Il nome del repository è di sola lettura.
1. Fate clic su Salva.

Se il connettore Content Repository per il servizio EMC Documentum e/o il servizio Repository per EMC Documentum sono in esecuzione, le informazioni sulle credenziali vengono verificate rispetto al repository specificato prima di essere archiviate nel database. Se le credenziali non sono valide o esistono, viene visualizzato un messaggio di errore.

## Abilita la richiesta di condivisione delle code di attività di Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Sono necessari alcuni passaggi manuali per garantire che la funzionalità Richiesta di condivisione della coda di task in Workspace funzioni correttamente con il connettore per EMC Documentum.

1. Dopo aver distribuito AEM moduli e installato Workbench, accedere a Workbench e aprire la visualizzazione Risorse. Il percorso in cui si trova il file QueueSharing.swf da questa visualizzazione verrà determinato.
1. Trascinate il file QueueSharing.swf dalla vista Risorse al desktop Windows o in una posizione equivalente, a seconda del sistema operativo in uso.
1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. In Informazioni sui provider di servizi di repository, modificare il provider di repository configurato in EMC Documentum Repository Provider.
1. Avviare Workbench e copiare il file QueueSharing.swf dal percorso in cui è stato originariamente copiato (ad esempio, il desktop di Windows o un altro percorso) in una directory esistente all&#39;interno del repository di EMC Documentum.
1. Nella visualizzazione Processi di Workbench, aprire il processo di condivisione delle code.
1. Nella visualizzazione Variabili, aprire le proprietà della variabile &quot;theForm&quot; e modificare l&#39;URI in modo che corrisponda al percorso in cui è stato inserito il file QueueSharing.swf al punto 5.
1. Salvare il processo.
1. Esegui la migrazione del processo all&#39;ambiente di produzione in base ai criteri aziendali.

