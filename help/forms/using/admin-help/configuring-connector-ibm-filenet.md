---
title: Configurazione del connettore per IBM FileNet
seo-title: Configurazione del connettore per IBM FileNet
description: Scopri come configurare il connettore per IBM FileNet per abilitare la comunicazione tra i moduli AEM e IBM FileNet.
seo-description: Scopri come configurare il connettore per IBM FileNet per abilitare la comunicazione tra i moduli AEM e IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurazione del connettore per IBM FileNet {#configuring-connector-for-ibm-filenet}

Il connettore per IBM FileNet consente la comunicazione tra i moduli AEM e IBM FileNet. Per ulteriori informazioni di base, vedere &quot;Connettori per l&#39;ECM&quot; nella Guida di riferimento dei [servizi](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Nelle versioni precedenti, le risorse potevano essere memorizzate in un repository ECM. In questa versione, le risorse vengono memorizzate nell&#39;archivio nativo dei moduli di AEM e i servizi dei fornitori di repository non sono più disponibili. La migrazione delle risorse da un archivio ECM all&#39;archivio dei moduli AEM viene effettuata quando si esegue un aggiornamento ai moduli AEM. Per ulteriori informazioni, consultate la guida all&#39;aggiornamento moduli AEM per il server delle applicazioni.

## Configurare la connessione al motore di contenuto {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine offre servizi software per la gestione dei contenuti aziendali e degli oggetti aziendali definiti dal cliente nei repository dei contenuti FileNet.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Nella casella URL motore di contenuto, immettete l’URL di connessione completo. Esempio:

   Se si utilizza FileNet Content Engine 4.x con trasporto CEWS, immettere:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Se si utilizza FileNet Content Engine 4.x con trasporto EJB, supportato solo su WebLogic, immettere:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Nell&#39;elenco Schema protezione credenziali, selezionare uno dei seguenti livelli di protezione:

   * **** Cancella: Invia le credenziali in rete in una modalità non protetta
   * **** Simmetrico: Invia credenziali crittografate in rete

1. Nella casella Posizione file di cifratura, immettere il percorso del file di cifratura:

   * Se è stato selezionato Cancella come schema di protezione delle credenziali, questa parola chiave e il relativo valore vengono ignorati.
   * Se si è selezionata l&#39;opzione Simmetrico come schema di protezione delle credenziali, il percorso immesso punta alla posizione di un file di cifratura nel server dei moduli che contiene le chiavi di crittografia da utilizzare.

1. Nella casella Archivio oggetti predefinito, immettere il connettore per l&#39;archivio oggetti a cui i moduli AEM si connettono per impostazione predefinita.
1. Nella casella Nome utente, immettere il nome utente di un utente che dispone dei diritti di accesso all&#39;archivio oggetti predefinito specificato nel passaggio precedente.
1. Nella casella Password, immettete la password per l’utente e fate clic su Salva.

## Configurare le impostazioni del motore di processo {#configure-the-process-engine-settings}

Il connettore per IBM FileNet contiene il connettore Process Engine per il servizio IBM FileNet, utilizzato per interagire con IBM FileNet Process Engine. Potete configurare le impostazioni per questo servizio.

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Per abilitare l&#39;uso del connettore del motore di processo per il servizio FileNet IBM, selezionare Usa il servizio del connettore del motore di processo.
1. Nella casella Router processo/Punto di connessione, immettere il nome host o l&#39;indirizzo IP e il numero di porta seguiti dal nome del router di processo. Esempio:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Nella casella Nome utente, immettere il nome utente utilizzato per connettersi al motore di processo.
1. Nella casella Password immettere la password utilizzata per connettersi al motore di elaborazione e fare clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se immettete un nome utente o una password non corretti durante la configurazione della connessione a Content Engine o alle impostazioni del motore di elaborazione, otterrete i seguenti risultati, a seconda che i servizi siano attualmente in esecuzione:

* Se il servizio Repository Provider per IBM FileNet e il connettore Content Repository per il servizio IBM FileNet sono entrambi interrotti, al momento del salvataggio delle informazioni sulla configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un&#39;eccezione e il servizio non verrà avviato.
* Se si avvia il servizio Repository Provider per IBM FileNet o Content Repository Connector per il servizio IBM FileNet, quando si salvano le informazioni sulla configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni delle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

## Modifica del provider del servizio repository {#change-the-repository-service-provider}

È possibile configurare il provider del servizio repository da utilizzare con FileNet. Le chiamate al servizio repository sono delegate al provider configurato.

Sono disponibili le seguenti opzioni:

**** Nome provider repository corrente: Nome del provider di servizi repository corrente

**** Provider repository IBM FileNet: Rende il provider del repository FileNet il provider del repository.  Questa opzione è stata rimossa.

**** provider repository: Imposta il provider del repository nativo come fornitore del repository

***Nota **: Per selezionare un provider di servizi repository diverso da quelli elencati, configurare RepositoryService in Applicazioni e servizi.<!-- Fix broken link(See Managing Services) -->*

1. Nella console di amministrazione, fare clic su Servizi > Connettore per IBM FileNet.
1. Nell&#39;area Informazioni su Repository Service Provider, selezionare il provider di servizi repository alternativo, quindi fare clic su Salva.

