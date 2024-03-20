---
title: Configurazione del connettore per EMC Documentum
description: Scopri come configurare il connettore per EMC Documentum per abilitare la comunicazione tra i moduli AEM e EMC Documentum.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Configurazione del connettore per EMC Documentum {#configuring-connector-for-emc-documentum}

Il connettore per EMC Documentum consente la comunicazione tra i moduli AEM ed EMC Documentum. Per ulteriori informazioni di base, vedere &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

L&#39;impostazione del connettore per EMC Documentum comporta la configurazione della connessione al server e delle credenziali del repository.

>[!NOTE]
>
>Nelle versioni precedenti , le risorse potevano essere memorizzate in un archivio ECM. Nella versione corrente, le risorse vengono memorizzate nell’archivio nativo dei moduli AEM e i servizi del provider dell’archivio sono stati dichiarati obsoleti. La migrazione delle risorse da un archivio ECM all’archivio dei moduli AEM viene eseguita quando si esegue un aggiornamento ai moduli AEM. Per ulteriori informazioni, consulta la guida all’aggiornamento dei moduli AEM per il tuo server applicazioni.

## Configurazione della connessione al server {#configuring-the-server-connection}

In questo argomento vengono descritte le attività di Connector per EMC Documentum che è possibile eseguire nella pagina Impostazioni di configurazione.

>[!NOTE]
>
>Se si stanno configurando tutte le impostazioni contemporaneamente, è sufficiente fare clic una sola volta su Salva.

### Configurare il server {#configure-the-server}

È necessario configurare le informazioni sul server di Gestore connessione. Queste informazioni sono necessarie per connettersi ai repository dei contenuti Documentum e avviare il connettore per EMC Documentum.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni configurazione Documentum immettere il nome host o l&#39;indirizzo IP e il numero di porta del gestore di connessione. Il numero di porta deve essere un numero intero positivo, ad esempio 1489.
1. Fai clic su Salva.

### Configurare le credenziali dell’entità {#configure-principal-credentials}

Quando si configurano le credenziali principali, il nome del repository fornito dipende dal fatto che durante l&#39;accesso venga fornito un nome di repository esplicito.

Se si immette un nome utente o una password errati, si otterranno i seguenti risultati, a seconda che il servizio sia attualmente in esecuzione:

* Se il servizio EMC Documentum Repository Provider e il servizio EMC Documentum Content Repository Connector vengono interrotti, quando si salvano le informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un&#39;eccezione e il servizio non verrà avviato.
* Se viene avviato il servizio EMC Documentum Repository Provider o il servizio EMC Documentum Content Repository Connector, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni sulle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni sulle credenziali dell&#39;entità Documentum digitare il nome utente e la password di un utente con privilegi di amministratore privilegiato.
1. Se durante l&#39;accesso non viene fornito un nome di repository esplicito, immettere il nome del repository a cui sono associate le credenziali.
1. Fai clic su Salva.

### Modificare il provider di servizi dell’archivio {#change-the-repository-service-provider}

È possibile configurare il provider di servizi di repository da utilizzare con Documentum. Le chiamate al servizio archivio sono delegate al provider configurato. Sono disponibili le seguenti opzioni:

**Nome del provider di servizi dell&#39;archivio corrente:** Nome del provider di servizi di repository corrente

**Provider repository ECM Documentum:** Rende il provider del repository Documentum il provider del repository. Questa opzione è obsoleta

**provider di repository:** Rende il provider del repository nativo il provider del repository

>[!NOTE]
>
>Per selezionare un provider di servizi del repository diverso da quelli elencati, configurare RepositoryService in Applicazioni e servizi > Gestione servizi. <!-- Fix broken link (See Managing Services) -->.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nell&#39;area Informazioni provider di servizi di repository selezionare il provider di servizi di repository alternativo.
1. Fai clic su Salva.

## Configurazione delle credenziali dell’archivio {#configuring-repository-credentials}

Le informazioni sulle credenziali Documentum vengono utilizzate nel contesto del sistema dei moduli AEM. Le credenziali del repository sono specifiche per determinati repository in Documentum. È possibile fornire le credenziali per un numero qualsiasi di repository; tuttavia, è possibile specificare un solo set di credenziali per repository.

### Aggiungi credenziali archivio {#add-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni credenziali del repository.
1. Fai clic su Aggiungi. Viene visualizzata la pagina Informazioni sulle credenziali di Documentum System.
1. Immettere un nome per l&#39;archivio.
1. Immettere un nome utente e una password.
1. Fai clic su Salva.

Se il servizio Content Repository Connector per EMC Documentum e/o il servizio Repository per EMC Documentum sono in esecuzione, le informazioni sulle credenziali vengono verificate rispetto al repository specificato prima di essere memorizzate nel database. Se le credenziali non sono valide o esistono, viene visualizzato un messaggio di errore.

### Rimuovere le credenziali di un repository {#remove-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Selezionare la casella di controllo accanto al repository da cui rimuovere le credenziali e fare clic su Rimuovi. Le credenziali per l&#39;archivio selezionato vengono rimosse dal database.

### Modificare il nome utente e la password per le credenziali di un repository {#change-the-user-name-and-password-for-a-repository-credential}

1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Fai clic sul nome dell’archivio per cui modificare le credenziali.
1. Modificare il nome utente o la password dell&#39;archivio o entrambi. Il nome dell&#39;archivio è di sola lettura.
1. Fai clic su Salva.

Se il servizio Content Repository Connector per EMC Documentum e/o il servizio Repository per EMC Documentum sono in esecuzione, le informazioni sulle credenziali vengono verificate rispetto al repository specificato prima di essere memorizzate nel database. Se le credenziali non sono valide o esistono, viene visualizzato un messaggio di errore.

## Abilita la richiesta di condivisione delle code di attività di Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Sono necessari alcuni passaggi manuali per garantire il corretto funzionamento della funzione Request for Sharing of Task Queue (Richiesta di condivisione della coda di attività) in Workspace con Connector for EMC Documentum.

1. Dopo aver distribuito i moduli AEM e aver installato Workbench, accedi a Workbench e apri la visualizzazione Risorse. Da questa visualizzazione verrà determinato dove si trova il file QueueSharing.swf.
1. Trascinare il file QueueSharing.swf dalla visualizzazione Risorse al desktop di Windows o in una posizione equivalente, a seconda del sistema operativo in uso.
1. Nella console di amministrazione, fare clic su Servizi > Connettore per EMC Documentum > Impostazioni di configurazione.
1. Nella sezione Informazioni sul provider di servizi del repository modificare il provider del repository configurato in EMC Documentum Repository Provider.
1. Avviare Workbench e copiare il file QueueSharing.swf dal percorso in cui è stato originariamente copiato (ad esempio, il desktop Windows o un altro percorso) in una directory esistente all&#39;interno del repository EMC Documentum.
1. Nella vista Processi di Workbench, aprire il processo Condivisione coda.
1. Nella visualizzazione Variabili aprire le proprietà della variabile &quot;theForm&quot; e modificare l&#39;URI in modo che corrisponda al percorso in cui è stato inserito il file QueueSharing.swf al passaggio 5.
1. Salvare il processo.
1. Migra il processo all’ambiente di produzione in base ai criteri della tua organizzazione.
