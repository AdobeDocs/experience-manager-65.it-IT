---
title: Configurazione del connettore per IBM FileNet
description: Scopri come configurare il connettore per IBM FileNet per abilitare la comunicazione tra i moduli AEM e IBM FileNet.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORM
exl-id: f4045df5-a35b-41d7-910e-971017148597
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# Configurazione del connettore per IBM FileNet {#configuring-connector-for-ibm-filenet}

Il connettore per IBM FileNet consente la comunicazione tra i moduli AEM e IBM FileNet. Per ulteriori informazioni di base, vedere &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Nelle versioni precedenti, le risorse potevano essere memorizzate in un archivio ECM. In questa versione, le risorse vengono memorizzate nell’archivio nativo dei moduli AEM e i servizi Provider archivio sono stati dichiarati obsoleti. La migrazione delle risorse da un archivio ECM all’archivio dei moduli AEM viene eseguita quando si esegue un aggiornamento ai moduli AEM. Per ulteriori informazioni, consulta la guida all’aggiornamento dei moduli AEM per il tuo server applicazioni.

## Configurare la connessione al motore di contenuto {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine fornisce servizi software per la gestione dei contenuti aziendali e degli oggetti aziendali definiti dal cliente nei repository di contenuto FileNet.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Nella casella URL motore di contenuto immettere l&#39;URL di connessione completo. Ad esempio:

   Se si utilizza FileNet Content Engine 4.x con trasporto CEWS, immettere:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Se si utilizza FileNet Content Engine 4.x con trasporto EJB, supportato solo in WebLogic, immettere:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Nell&#39;elenco Schema protezione credenziali selezionare uno dei seguenti livelli di protezione:

   * **Cancella:** Invia credenziali in rete in modalità non protetta
   * **Simmetrico:** Invia credenziali crittografate in rete

1. Nella casella Percorso file di crittografia immettere il percorso del file di crittografia:

   * Se si seleziona Cancella come schema di protezione delle credenziali, questa parola chiave e il relativo valore vengono ignorati.
   * Se si seleziona Simmetrico come schema di protezione delle credenziali, il percorso immesso punta alla posizione di un file di crittografia sul server Forms contenente le chiavi di crittografia da utilizzare.

1. Nella casella Archivio oggetti predefinito immettere il connettore dell&#39;archivio oggetti a cui i moduli AEM si connettono per impostazione predefinita.
1. Nella casella Nome utente immettere il nome utente di un utente con diritti di accesso all&#39;archivio oggetti predefinito specificato nel passaggio precedente.
1. Nella casella Password, immettere la password per l&#39;utente e fare clic su Salva.

## Configurare le impostazioni del motore di processo {#configure-the-process-engine-settings}

Il connettore per IBM FileNet contiene il connettore del motore di processo per il servizio IBM FileNet, utilizzato per interagire con il motore di processo IBM FileNet. È possibile configurare le impostazioni per questo servizio.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Per abilitare l&#39;utilizzo del connettore del motore di processo per il servizio IBM FileNet, selezionare Usa servizio connettore del motore di processo.
1. Nella casella Router di processo/Punto di connessione immettere il nome host o l&#39;indirizzo IP e il numero di porta seguiti dal nome del router di processo. Ad esempio:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Nella casella Nome utente immettere il nome utente utilizzato per connettersi al motore di elaborazione.
1. Nella casella Password immettere la password utilizzata per connettersi al motore di elaborazione e fare clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se si immette un nome utente o una password errati durante la configurazione della connessione al motore di contenuto o alle impostazioni del motore di processo, si otterranno i seguenti risultati, a seconda che i servizi siano attualmente in esecuzione:

* Se entrambi i servizi Provider repository per IBM FileNet e Connettore repository dei contenuti per IBM FileNet vengono arrestati, quando si salvano le informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un&#39;eccezione e il servizio non verrà avviato.
* Se viene avviato il servizio Provider repository per IBM FileNet o il connettore repository dei contenuti per IBM FileNet, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni sulle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

## Modificare il provider di servizi dell’archivio {#change-the-repository-service-provider}

È possibile configurare il provider del servizio di repository da utilizzare con FileNet. Le chiamate al servizio archivio sono delegate al provider configurato.

Sono disponibili le seguenti opzioni:

**Nome provider archivio corrente:** Nome del provider di servizi di repository corrente

**Provider archivio IBM FileNet:** Rende il provider del repository FileNet il provider del repository. Questa opzione è obsoleta.

**provider di repository:** Rende il provider del repository nativo il provider del repository

>[!NOTE]
>
>Per selezionare un provider di servizi del repository diverso da quelli elencati, configurare RepositoryService in Applicazioni e servizi. <!-- Fix broken link(See Managing Services) -->

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Nell&#39;area Informazioni provider di servizi di repository selezionare il provider di servizi di repository alternativo e quindi fare clic su Salva.
