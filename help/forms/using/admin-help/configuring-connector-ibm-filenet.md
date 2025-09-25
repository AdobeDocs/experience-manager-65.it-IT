---
title: Configurazione del connettore per IBM FileNet
description: Scopri come configurare il connettore per IBM FileNet per abilitare la comunicazione tra AEM Forms e IBM FileNet.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORM
exl-id: f4045df5-a35b-41d7-910e-971017148597
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '742'
ht-degree: 100%

---

# Configurazione del connettore per IBM FileNet {#configuring-connector-for-ibm-filenet}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il connettore per IBM FileNet consente la comunicazione tra AEM Forms e IBM FileNet. Per ulteriori informazioni di base, consulta “Connettori per ECM” in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Nelle versioni precedenti, le risorse potevano essere memorizzate in un archivio ECM. In questa versione, le risorse vengono memorizzate nell’archivio nativo di AEM Forms e i servizi del provider dell’archivio sono stati dichiarati obsoleti. La migrazione delle risorse da un archivio ECM all’archivio AEM Forms viene eseguita quando esegui un aggiornamento ad AEM Forms. Per ulteriori informazioni, consulta la Guida all’aggiornamento di AEM Forms per il server applicazioni in uso.

## Configurare la connessione al sistema di gestione del contenuto {#configure-the-connection-to-the-content-engine}

Il sistema di gestione dei contenuti FileNet P8 di IBM fornisce servizi software per la gestione dei contenuti aziendali e degli oggetti definiti dal cliente nell’archivio dei contenuti FileNet.

1. Nella console di amministrazione fai clic su Servizi > Connettore per IBM FileNet.
1. Nella casella URL del sistema di gestione dei contenuti inserisci l’URL di connessione completo. Ad esempio:

   Se stai utilizzando il sistema di gestione dei contenuti FileNet 4.x con trasporto CEWS, inserisci:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Se stai utilizzando il sistema di gestione dei contenuti FileNet 4.x con trasporto EJB, supportato solo in WebLogic, inserisci:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Nell’elenco Schema di protezione delle credenziali seleziona uno dei seguenti livelli di protezione:

   * **Cancella:** invia credenziali in rete in modalità non protetta
   * **Simmetrico:** invia credenziali crittografate in rete

1. Nella casella Posizione del file di crittografia inserisci il percorso del file di crittografia:

   * Se hai selezionato Cancella come schema di protezione delle credenziali, questa parola chiave e il relativo valore vengono ignorati.
   * Se hai selezionato Simmetrico come schema di protezione delle credenziali, il percorso inserito punta alla posizione di un file di crittografia sul server Forms contenente le chiavi di crittografia da utilizzare.

1. Nella casella Archivio oggetti predefinito inserisci il connettore dell’archivio di oggetti a cui AEM Forms si connette per impostazione predefinita.
1. Nella casella Nome utente inserisci il nome di un utente con diritti di accesso all’archivio di oggetti predefinito che hai specificato nel passaggio precedente.
1. Nella casella Password inserisci la password per l’utente e fai clic su Salva.

## Configurare le impostazioni del motore di processo {#configure-the-process-engine-settings}

Il connettore per IBM FileNet contiene il connettore del motore di processo per il servizio IBM FileNet, utilizzato per interagire con il motore di processo di IBM FileNet. Puoi configurare le impostazioni per questo servizio.

1. Nella console di amministrazione fai clic su Servizi > Connettore per IBM FileNet.
1. Per abilitare l’utilizzo del connettore del motore di processo per il servizio IBM FileNet, seleziona Usa il servizio connettore del motore di processo.
1. Nella casella Router di processo/punto di connessione inserisci il nome host o l’indirizzo IP e il numero di porta seguiti dal nome del router di processo. Ad esempio:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Nella casella Nome utente inserisci il nome utente utilizzato per connettersi al motore di processo.
1. Nella casella Password inserisci la password utilizzata per connettersi al motore di processo e fai clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se inserisci un nome utente o una password errati durante la configurazione della connessione al sistema di gestione dei contenuti o alle impostazioni del motore di processo, otterrai i seguenti risultati, a seconda che i servizi siano attualmente in esecuzione:

* Se entrambi i servizi Provider dell’archivio per IBM FileNet e Connettore dell’archivio dei contenuti per IBM FileNet vengono interrotti, quando salvi le informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un’eccezione e il servizio non verrà avviato.
* Se viene avviato il servizio Provider dell’archivio per IBM FileNet o Connettore dell’archivio dei contenuti per IBM FileNet, quando salvi le informazioni di configurazione del servizio, quest’ultimo tenta di convalidare immediatamente le informazioni sulle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

## Modificare il provider di servizi di archivio {#change-the-repository-service-provider}

Puoi configurare il provider di servizio dell’archivio da utilizzare con FileNet. Le chiamate al servizio dell’archivio sono delegate al provider configurato.

Sono disponibili le seguenti opzioni:

**Nome del provider dell’archivio corrente:** Nome del provider di servizi repository corrente

**Provider dell’archivio di IBM FileNet:** imposta il provider dell’archivio di FileNet come provider dell’archivio. Questa opzione è obsoleta.

**Provider dell’archivio:** imposta il provider dell’archivio nativo come provider dell’archivio

>[!NOTE]
>
>Per selezionare un provider di servizi dell’archivio diverso da quelli elencati, configura RepositoryService in Applicazioni e servizi. <!-- Fix broken link(See Managing Services) -->

1. Nella console di amministrazione fai clic su Servizi > Connettore per IBM FileNet.
1. Nell’area Informazioni provider di servizi di archivio, seleziona il provider di servizi di archivio alternativo e quindi fai clic su Salva.
