---
title: Configurazione del connettore per IBM FileNet
seo-title: Configuring Connector for IBM FileNet
description: Scopri come configurare il connettore per IBM FileNet per abilitare la comunicazione tra AEM moduli e IBM FileNet.
seo-description: Learn how to configure the Connector for IBM FileNet to enable communication between AEM forms and IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# Configurazione del connettore per IBM FileNet {#configuring-connector-for-ibm-filenet}

Il connettore per IBM FileNet consente la comunicazione tra AEM moduli e IBM FileNet. Per ulteriori informazioni di base, consulta &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Nelle versioni precedenti, le risorse potevano essere memorizzate in un archivio ECM. In questa versione, le risorse vengono memorizzate nell’archivio nativo dei moduli AEM e i servizi del fornitore dell’archivio sono diventati obsoleti. La migrazione delle risorse da un archivio ECM all’archivio dei moduli AEM viene eseguita quando si esegue un aggiornamento ai moduli AEM. Per ulteriori informazioni, vedere la guida all’aggiornamento dei moduli AEM per il server delle applicazioni.

## Configurare la connessione al motore di contenuto {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine fornisce servizi software per la gestione dei contenuti aziendali e degli oggetti aziendali definiti dal cliente negli archivi di contenuti FileNet.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Nella casella URL motore di contenuto , immetti l’URL di connessione completo. Esempio:

   Se utilizzi FileNet Content Engine 4.x con trasporto CEWS, immetti:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Se utilizzi FileNet Content Engine 4.x con trasporto EJB, supportato solo su WebLogic, immetti:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Nell&#39;elenco Schema di protezione delle credenziali, selezionare uno dei seguenti livelli di protezione:

   * **Cancella:** Invia credenziali in tutta la rete in modalità non protetta
   * **Simmetrica:** Invia credenziali crittografate in tutta la rete

1. Nella casella Percorso file crittografia immettere il percorso del file di crittografia:

   * Se hai selezionato Cancella come schema di protezione delle credenziali, questa parola chiave e il relativo valore vengono ignorati.
   * Se è stato selezionato Simmetrico come schema di protezione delle credenziali, il percorso immesso indica la posizione di un file di crittografia sul server dei moduli che contiene le chiavi di crittografia da utilizzare.

1. Nella casella Archivio oggetti predefinito, immettere il connettore dell’archivio oggetti a cui si AEM i moduli per impostazione predefinita.
1. Nella casella Nome utente immettere il nome utente di un utente con diritti di accesso all&#39;archivio oggetti predefinito specificato nel passaggio precedente.
1. Nella casella Password immettere la password per l&#39;utente e fare clic su Salva.

## Configurare le impostazioni del motore di processo {#configure-the-process-engine-settings}

Il connettore per IBM FileNet contiene il connettore del motore di processo per il servizio IBM FileNet, utilizzato per interagire con il motore di processo IBM FileNet. Puoi configurare le impostazioni per questo servizio.

1. Nella console di amministrazione, fare clic su Servizi >Connettore per IBM FileNet.
1. Per abilitare l&#39;uso del connettore del motore di processo per il servizio IBM FileNet, selezionare Usa il servizio del connettore del motore di processo.
1. Nella casella Router del processo/Punto di connessione immettere il nome host o l&#39;indirizzo IP e il numero di porta seguiti dal nome del router di processo. Esempio:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Nella casella Nome utente immettere il nome utente utilizzato per connettersi al motore di processo.
1. Nella casella Password immettere la password utilizzata per connettersi al motore di elaborazione e fare clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se immetti un nome utente o una password non corretti durante la configurazione della connessione al motore di contenuto o alle impostazioni del modulo di gestione del processo, otterrai i seguenti risultati, a seconda che i servizi siano attualmente in esecuzione:

* Se il servizio Provider archivio per IBM FileNet e il connettore dell&#39;archivio dei contenuti per il servizio IBM FileNet vengono arrestati, quando si salvano le informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un’eccezione e il servizio non verrà avviato.
* Se si avvia il servizio Provider del repository per IBM FileNet o il connettore del repository dei contenuti per il servizio FileNet IBM, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni delle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

## Modificare il provider del servizio del repository {#change-the-repository-service-provider}

È possibile configurare il provider di servizi di archivio da utilizzare con FileNet. Le chiamate al servizio archivio vengono delegate al provider configurato.

Sono disponibili le seguenti opzioni:

**Nome provider repository corrente:** Nome del provider di servizi di archivio corrente

**Provider archivio IBM FileNet:** Rende il provider del repository FileNet il provider del repository. Questa opzione è stata dichiarata obsoleta.

**provider archivio:** Rende il provider del repository nativo il provider del repository

>[!NOTE]
>
>Per selezionare un provider di servizi di archivio diverso da quelli elencati, configurare RepositoryService in Applicazioni e servizi. <!-- Fix broken link(See Managing Services) -->

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Nell&#39;area Informazioni sul provider di servizi di archivio selezionare il provider di servizi di archivio alternativo, quindi fare clic su Salva.
