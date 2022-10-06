---
title: Configurazione del connettore per EMC Documentum
seo-title: Configuring Connector for EMC Documentum
description: Informazioni su come configurare il connettore per EMC Documentum per consentire la comunicazione tra moduli AEM e EMC Documentum.
seo-description: Learn how to configure the Connector for EMC Documentum to enable communication between AEM forms and EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Configurazione del connettore per EMC Documentum {#configuring-connector-for-emc-documentum}

Il connettore per EMC Documentum consente la comunicazione tra i moduli AEM e EMC Documentum. Per ulteriori informazioni di base, consulta &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

La configurazione del connettore per EMC Documentum comporta la configurazione della connessione al server e delle credenziali del repository.

>[!NOTE]
>
>Nelle versioni precedenti , le risorse potevano essere memorizzate in un archivio ECM. Nella versione corrente, le risorse vengono memorizzate nell’archivio nativo dei moduli di AEM e i servizi del fornitore dell’archivio sono diventati obsoleti. La migrazione delle risorse da un archivio ECM all’archivio dei moduli AEM viene eseguita quando si esegue un aggiornamento ai moduli AEM. Per ulteriori informazioni, vedere la guida all’aggiornamento dei moduli AEM per il server delle applicazioni.

## Configurazione della connessione al server {#configuring-the-server-connection}

In questo argomento vengono descritte le attività di Connettore per EMC Documentum che è possibile eseguire nella pagina Impostazioni di configurazione.

>[!NOTE]
>
>Se si configurano tutte le impostazioni contemporaneamente, è sufficiente fare clic su Salva una sola volta.

### Configurare il server {#configure-the-server}

È necessario configurare le informazioni sul server di connection broker. Queste informazioni sono necessarie per la connessione ai repository dei contenuti Documentum e per l&#39;avvio del connettore per EMC Documentum.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni di configurazione Documentum, immettere il nome host o l&#39;indirizzo IP e il numero di porta del broker di connessione. Il numero di porta deve essere un numero intero positivo (ad esempio, 1489).
1. Fai clic su Salva.

### Configurare le credenziali principali {#configure-principal-credentials}

Durante la configurazione delle credenziali principali, il nome dell&#39;archivio fornito dipende dal fatto che durante l&#39;accesso sia stato fornito un nome di archivio esplicito.

Se immetti un nome utente o una password non corretti, otterrai i seguenti risultati, a seconda che il servizio sia attualmente in esecuzione:

* Se il servizio EMC Documentum Repository Provider e il servizio EMC Documentum Content Repository Connector vengono arrestati, quando si salvano le informazioni sulla configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un’eccezione e il servizio non verrà avviato.
* Se si avvia il servizio EMC Documentum Repository Provider o il servizio EMC Documentum Content Repository Connector, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni delle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni sulle credenziali principali di Documentum digitare il nome utente e la password di un utente con privilegi di super amministratore.
1. Se durante l&#39;accesso non viene fornito un nome di archivio esplicito, immettere il nome del repository a cui sono associate le credenziali.
1. Fai clic su Salva.

### Modificare il provider del servizio del repository {#change-the-repository-service-provider}

È possibile configurare il provider di servizi di repository da utilizzare con Documentum. Le chiamate al servizio archivio vengono delegate al provider configurato. Sono disponibili le seguenti opzioni:

**Nome provider servizio archivio corrente:** Nome del provider di servizi di archivio corrente

**Provider repository ECM Documentum:** Rende il provider del repository Documentum il provider del repository. Questa opzione è stata dichiarata obsoleta

**provider archivio:** Rende il provider del repository nativo il provider del repository

>[!NOTE]
>
>Per selezionare un provider di servizi del repository diverso da quelli elencati, configurare RepositoryService in Applicazioni e servizi > Gestione dei servizi. <!-- Fix broken link (See Managing Services) -->.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni sul provider di servizi di archivio selezionare il provider di servizi di archivio alternativo.
1. Fai clic su Salva.

## Configurazione delle credenziali del repository {#configuring-repository-credentials}

Le informazioni sulle credenziali Documentum vengono utilizzate nel contesto del sistema dei moduli AEM. Le credenziali del repository sono specifiche per archivi specifici in Documentum. È possibile fornire le credenziali per qualsiasi numero di archivi; tuttavia, è possibile specificare un solo set di credenziali per archivio.

### Aggiungere una credenziale del repository {#add-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni credenziali repository.
1. Fate clic su Aggiungi. Viene visualizzata la pagina Informazioni sulle credenziali di sistema Documentum.
1. Immettere un nome per il repository.
1. Immetti un nome utente e una password.
1. Fai clic su Salva.

Se il servizio Content Repository Connector per EMC Documentum e/o il servizio Repository per EMC Documentum sono in esecuzione, le informazioni delle credenziali vengono verificate rispetto al repository specificato prima di essere archiviate nel database. Se le credenziali non sono valide o esistono, viene visualizzato un messaggio di errore.

### Rimuovere una credenziale del repository {#remove-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Selezionare la casella di controllo accanto all&#39;archivio da cui rimuovere le credenziali e fare clic su Rimuovi. Le credenziali per l&#39;archivio selezionato vengono rimosse dal database.

### Modificare il nome utente e la password per una credenziale del repository {#change-the-user-name-and-password-for-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Fare clic sul nome dell&#39;archivio per cui modificare le credenziali.
1. Modificare il nome utente o la password dell’archivio o entrambi. Il nome del repository è di sola lettura.
1. Fai clic su Salva.

Se il servizio Content Repository Connector per EMC Documentum e/o il servizio Repository per EMC Documentum sono in esecuzione, le informazioni delle credenziali vengono verificate rispetto al repository specificato prima di essere archiviate nel database. Se le credenziali non sono valide o esistono, viene visualizzato un messaggio di errore.

## Abilita la richiesta di condivisione delle code delle attività di Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Sono necessari alcuni passaggi manuali per garantire che la funzionalità Richiesta di condivisione della coda task in Workspace funzioni correttamente con il connettore per EMC Documentum.

1. Dopo aver distribuito AEM moduli e installato Workbench, accedi a Workbench e apri la visualizzazione Risorse. Il percorso del file QueueSharing.swf viene determinato da questa visualizzazione.
1. Trascinare il file QueueSharing.swf dalla Vista risorse sul desktop Windows o in una posizione equivalente, a seconda del sistema operativo in uso.
1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. In Repository Service Provider Information, modificare il provider del repository configurato in EMC Documentum Repository Provider.
1. Avviare Workbench e copiare il file QueueSharing.swf dal percorso in cui è stato originariamente copiato (ad esempio, il desktop Windows o un altro percorso) in una directory esistente all&#39;interno del repository EMC Documentum.
1. Nella visualizzazione Processi di Workbench, apri il processo Condivisione coda.
1. Nella vista Variabili, aprire le proprietà della variabile &quot;theForm&quot; e modificare l&#39;URI in modo che corrisponda al percorso in cui è stato inserito il file QueueSharing.swf nel passaggio 5.
1. Salva il processo.
1. Esegui la migrazione del processo all’ambiente di produzione in base ai criteri aziendali.
