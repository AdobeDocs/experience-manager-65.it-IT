---
title: Configurare origini dati
description: Scopri come configurare diversi tipi di origini dati per creare modelli di dati per moduli.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 1%

---

# Configurare origini dati{#configure-data-sources}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html) |
| AEM 6.5 | Questo articolo |


![Integrazione dei dati](do-not-localize/data-integeration.png)

L’integrazione dei dati di AEM Forms consente di configurare e connettersi a diverse origini dati. Sono supportati i seguenti tipi pronti all’uso. Tuttavia, con una personalizzazione ridotta, puoi integrare anche altre origini dati.

* Database relazionali: MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS, postgreSQL e Sybase
* Profilo utente AEM
* Servizi Web RESTful
* Servizi web basati su SOAP
* Servizi OData

L’integrazione dei dati supporta OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base e tipi di autenticazione con chiave API pronti all’uso e che consentono l’implementazione dell’autenticazione personalizzata per l’accesso ai servizi web. Mentre i servizi RESTful, SOAP-based e OData sono configurati nei Cloud Service AEM, JDBC per i database relazionali e il connettore per il profilo utente AEM sono configurati nella console web AEM.

## Configurare il database relazionale {#configure-relational-database}

È possibile configurare i database relazionali utilizzando Configurazione console Web AEM. Effettua le seguenti operazioni:

1. Vai alla console web dell’AEM all’indirizzo `https://server:host/system/console/configMgr`.
1. Cerca **[!UICONTROL Origine dati in pool di connessione Apache Sling]** configurazione. Seleziona per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo di configurazione specificare i dettagli del database che si desidera configurare, ad esempio:

   * Nome dell’origine dati
   * Proprietà del servizio origine dati che memorizza il nome dell&#39;origine dati
   * Nome classe Java per il driver JDBC
   * URI connessione JDBC
   * Nome utente e password per stabilire la connessione con il driver JDBC

   >[!NOTE]
   >
   >Prima di configurare l&#39;origine dati, assicurarsi di crittografare informazioni riservate come le password. Per crittografare:
   >
   > 1. Vai a https://&#39;[server]:[porta]&#39;/system/console/crypto.
   > 1. In **[!UICONTROL Testo normale]** , specificare la password o qualsiasi stringa da crittografare e selezionare **[!UICONTROL Protect]**.
   >
   >Il testo crittografato viene visualizzato nel campo Testo protetto che è possibile specificare nella configurazione.

1. Abilita **[!UICONTROL Test su prestito]** o **[!UICONTROL Test al ritorno]** per specificare che gli oggetti vengono convalidati prima di essere presi in prestito o restituiti rispettivamente da e al pool.
1. Specificare una query SQL SELECT in **[!UICONTROL Query di convalida]** per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specificare una delle seguenti opzioni:

   * SELECT 1 (MySQL e MS SQL)
   * SELECT 1 da dual (Oracle)

1. Seleziona **[!UICONTROL Salva]** per salvare la configurazione.

   >[!NOTE]
   >
   > Se il modello dati di Forms contiene un oggetto che è una parola chiave riservata per il database relazionale, può causare problemi di aggiunta, aggiornamento o recupero di dati. Evita quindi di utilizzare tali oggetti nel modello dati del modulo.

## Configurare il profilo utente AEM {#configure-aem-user-profile}

Puoi configurare il profilo utente AEM utilizzando la configurazione del connettore profilo utente nella console web AEM. Effettua le seguenti operazioni:

1. Vai alla console web dell’AEM all’indirizzo https://&#39;[server]:[porta]&#39;system/console/configMgr.
1. Cerca **[!UICONTROL Integrazioni dei dati di AEM Forms - Configurazione del connettore del profilo utente]** e seleziona per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo Configurazione connettore profilo utente puoi aggiungere, rimuovere o aggiornare le proprietà del profilo utente. Le proprietà specificate sono disponibili per l&#39;utilizzo nel modello dati del modulo. Utilizza il seguente formato per specificare le proprietà del profilo utente:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Esempi:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >Il **&#42;** nell’esempio precedente indica tutti i nodi sotto il `profile/empLocation/` nodo nel profilo utente AEM nella struttura CRXDE. Significa che il modello dati del modulo può accedere a `city` proprietà di tipo `string` presente in qualsiasi nodo sotto `profile/empLocation/` nodo. Tuttavia, i nodi che contengono la proprietà specificata devono seguire una struttura coerente.

1. Seleziona **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

>[!NOTE]
>
Per configurare i servizi cloud per i servizi RESTful, SOAP e OData è necessaria la configurazione della cartella Servizi cloud.

Tutte le configurazioni dei servizi cloud in AEM sono consolidate in `/conf` cartella nell’archivio AEM. Per impostazione predefinita, il `conf` la cartella contiene `global` cartella in cui è possibile creare le configurazioni di cloud service. Tuttavia, devi abilitarlo manualmente per le configurazioni cloud. Puoi anche creare ulteriori cartelle in `conf` per creare e organizzare le configurazioni di cloud service.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   * Consulta la [Browser configurazioni](/help/sites-administering/configurations.md) per ulteriori informazioni.
1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

   1. In **[!UICONTROL Browser configurazioni]**, seleziona la `global` cartella e seleziona **[!UICONTROL Proprietà]**.

   1. In **[!UICONTROL Proprietà di configurazione]** finestra di dialogo, abilita **[!UICONTROL Configurazioni cloud]**.

   1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. In **[!UICONTROL Browser configurazioni]**, seleziona **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** , specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
1. Seleziona **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configurare i servizi web RESTful {#configure-restful-web-services}

Il servizio web RESTful può essere descritto utilizzando [Specifiche Swagger](https://swagger.io/specification/) in formato JSON o YAML in un file di definizione Swagger. Per configurare il servizio Web RESTful nei servizi cloud AEM, accertati di disporre del file Swagger sul file system o dell’URL in cui è ospitato il file.

Per configurare i servizi RESTful, effettuare le seguenti operazioni:

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Seleziona **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio RESTful]** dal **[!UICONTROL Tipo di servizio]** , sfogliare e selezionare un&#39;immagine di miniatura per la configurazione e selezionare **[!UICONTROL Successivo]**.
1. Specificare i dettagli seguenti per il servizio RESTful:

   * Selezionate URL o File dal menu a discesa Origine Swagger, quindi specificate l&#39;URL Swagger nel file di definizione Swagger o caricate il file Swagger dal file system locale.
   * In base all’input di Sorgente Swagger, i seguenti campi sono precompilati con i valori:

      * Schema: protocolli di trasferimento utilizzati dall’API REST. Il numero di tipi di schema visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nell&#39;origine Swagger.
      * Host: il nome di dominio o l’indirizzo IP dell’host che serve l’API REST. È un campo obbligatorio.
      * Percorso base: prefisso URL per tutti i percorsi API. È un campo facoltativo.\
        Se necessario, modifica i valori precompilati per questi campi.

   * Seleziona il tipo di autenticazione: Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base, chiave API, autenticazione personalizzata o autenticazione reciproca per accedere al servizio RESTful e fornire di conseguenza i dettagli per l’autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dalla **[!UICONTROL Posizione]** e specificare il nome dell&#39;intestazione o il parametro di query nell&#39; **[!UICONTROL Nome parametro]** di conseguenza.

   Se si seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, consulta [Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP](#mutual-authentication).

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

### Configurazione client HTTP del modello dati modulo per ottimizzare le prestazioni {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] il modello dati del modulo durante l’integrazione con i servizi web RESTful come origine dati include configurazioni client HTTP per l’ottimizzazione delle prestazioni.
Per configurare il client HTTP del modello dati modulo, effettua le seguenti operazioni:

1. Accedi a [!DNL Experience Manager Forms] Crea istanza come amministratore e passa a [!DNL Experience Manager] bundle della console web. L’URL predefinito è [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Seleziona **[!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST]**.

1. In [!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST] finestra di dialogo:

   * Specifica il numero massimo di connessioni consentite tra il modello di dati del modulo e i servizi web RESTful nel **[!UICONTROL Limite di connessioni in totale]** campo. Il valore predefinito è 20 connessioni.

   * Specificare il numero massimo di connessioni consentite per ogni route nella **[!UICONTROL Limite di connessione per ciclo di lavorazione]** campo. Il valore predefinito è 2 connessioni.

   * Specifica la durata per la quale una connessione HTTP persistente viene mantenuta attiva nel **[!UICONTROL Mantieni vivo]** campo. Il valore predefinito è 15 secondi.

   * Specifica la durata, per la quale [!DNL Experience Manager Forms] il server attende che venga stabilita una connessione, nel **[!UICONTROL Timeout della connessione]** campo. Il valore predefinito è 10 secondi.

   * Specifica il periodo massimo di inattività tra due pacchetti di dati nella **[!UICONTROL Timeout socket]** campo. Il valore predefinito è 30 secondi.

## Configurare i servizi web SOAP {#configure-soap-web-services}

I servizi web basati su SOAP sono descritti utilizzando [Specifiche di Web Services Description Language (WSDL)](https://www.w3.org/TR/wsdl). Per configurare il servizio Web basato su SOAP nei servizi cloud AEM, verificare di disporre dell&#39;URL WSDL per il servizio Web e procedere come segue:

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Seleziona **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio web SOAP]** dal **[!UICONTROL Tipo di servizio]** , sfogliare e selezionare un&#39;immagine di miniatura per la configurazione e selezionare **[!UICONTROL Successivo]**.
1. Specificare quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificare un valore in questo campo per sostituire l&#39;endpoint del servizio indicato in WSDL.
   * Seleziona il tipo di autenticazione: Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base, autenticazione personalizzata, token X509 o autenticazione reciproca per accedere al servizio SOAP e fornire di conseguenza i dettagli per l&#39;autenticazione.

     Se si seleziona **[!UICONTROL Token X509]** come tipo di autenticazione, configura il certificato X509. Per ulteriori informazioni, consulta [Configurare i certificati](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Specifica l’alias KeyStore per il certificato X509 in **[!UICONTROL Alias chiave]** campo. Specifica il tempo, in secondi, rimanente la validità della richiesta di autenticazione, nel **[!UICONTROL Time To Live]** campo. Facoltativamente, seleziona per firmare il corpo del messaggio o l’intestazione della marca temporale o entrambi.

     Se si seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, consulta [Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP](#mutual-authentication).

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio web SOAP.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL radice del servizio. Per configurare un servizio OData nei servizi cloud AEM, accertarsi di disporre dell&#39;URL principale del servizio ed eseguire le operazioni seguenti:

>[!NOTE]
>
Il modello dati del modulo supporta [OData versione 4](https://www.odata.org/documentation/).
Per una guida dettagliata alla configurazione di Microsoft Dynamics 365, online o on-premise, consulta [Configurazione Microsoft Dynamics OData](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Seleziona **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio OData]** dal **[!UICONTROL Tipo di servizio]** , sfogliare e selezionare un&#39;immagine di miniatura per la configurazione e selezionare **[!UICONTROL Successivo]**.
1. Specificare i dettagli seguenti per il servizio OData:

   * URL principale del servizio per il servizio OData da configurare.
   * Seleziona il tipo di autenticazione: Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base o autenticazione personalizzata: per accedere al servizio OData e fornire i dettagli per l&#39;autenticazione.

   >[!NOTE]
   >
   Seleziona il tipo di autenticazione OAuth 2.0 per connettersi ai servizi Microsoft Dynamics utilizzando l’endpoint OData come radice del servizio.

1. Seleziona **Crea** per creare la configurazione cloud per il servizio OData.

## Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP {#mutual-authentication}

Quando si abilita l&#39;autenticazione reciproca per il modello dati modulo, sia l&#39;origine dati che il server AEM che esegue il modello dati modulo autenticano l&#39;identità dell&#39;altro prima di condividere i dati. È possibile utilizzare l’autenticazione reciproca per le connessioni basate su REST e SOAP (origini dati). Per configurare l’autenticazione reciproca per un modello di dati modulo nell’ambiente AEM Forms:

1. Carica la chiave privata (certificato) in [!DNL AEM Forms] server. Per caricare la chiave privata:
   1. Accedi al tuo [!DNL AEM Forms] come amministratore.
   1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**. Seleziona la `fd-cloudservice` utente e seleziona **[!UICONTROL Proprietà]**.
   1. Apri **[!UICONTROL Registro chiavi]** , espandere la scheda **[!UICONTROL Aggiungi chiave privata da file registro chiavi]** , carica il file KeyStore, specifica gli alias, le password e seleziona **[!UICONTROL Invia]**. Il certificato è stato caricato.  L’alias della chiave privata viene menzionato nel certificato e impostato durante la creazione del certificato.
1. Carica il certificato di attendibilità nell&#39;archivio fonti attendibili globale. Per caricare il certificato:
   1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Archivio fonti attendibili]**.
   1. Espandi **[!UICONTROL Aggiungi certificato da file CER]** , seleziona **[!UICONTROL Seleziona file di certificato]**, carica il certificato e seleziona **[!UICONTROL Invia]**.
1. Configura [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) servizi web come origine di dati e selezionare **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione. Se si configurano più certificati autofirmati per `fd-cloudservice` utente, specifica il nome dell’alias chiave per il certificato.

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. Successivamente è possibile creare un modello dati modulo oppure, se è già stato creato un modello dati modulo senza un&#39;origine dati, è possibile associarlo alle origini dati configurate. Consulta [Crea modello dati modulo](/help/forms/using/create-form-data-models.md) per i dettagli.
