---
title: Configurare origini dati
seo-title: Configure data sources
description: Scopri come configurare diversi tipi di origini dati e come sfruttarle per creare modelli di dati modulo.
seo-description: Learn how to configure different types of data sources and leverage to create form data models.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: 98854fa3b852f511cf95adc13b945c06b1afff96
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 1%

---

# Configurare origini dati{#configure-data-sources}

![](do-not-localize/data-integeration.png)

L’integrazione dei dati di AEM Forms consente di configurare e connettersi a diverse origini dati. I seguenti tipi sono supportati come predefiniti. Tuttavia, con poca personalizzazione, puoi integrare anche altre origini dati.

* Database relazionali - MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS e Sybase
* Profilo utente AEM
* Servizi web RESTful
* Servizi web basati su SOAP
* Servizi OData

L’integrazione dei dati supporta i tipi di autenticazione predefiniti OAuth2.0, autenticazione di base e API Key e consente l’implementazione dell’autenticazione personalizzata per l’accesso ai servizi web. Mentre i servizi RESTful, basati su SOAP e OData sono configurati in AEM Cloud Services, JDBC per i database relazionali e il connettore per AEM profilo utente sono configurati in AEM console web.

## Configurare il database relazionale {#configure-relational-database}

È possibile configurare database relazionali utilizzando AEM configurazione della console Web. Effettua le seguenti operazioni:

1. Vai AEM console Web all&#39;indirizzo https://server:host/system/console/configMgr.
1. Cerca **[!UICONTROL Origine dati in pool di connessione Apache Sling]** configurazione. Tocca per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo di configurazione, specifica i dettagli del database da configurare, ad esempio:

   * Nome dell’origine dati
   * Proprietà del servizio origine dati che memorizza il nome dell&#39;origine dati
   * Nome della classe Java per il driver JDBC
   * URI di connessione JDBC
   * Nome utente e password per stabilire la connessione con il driver JDBC

   >[!NOTE]
   >
   >Prima di configurare l’origine dati, assicurati di crittografare le informazioni sensibili come le password. Per crittografare:
   >
   >    
   >    
   >    1. Vai su https://&#39;[server]:[porta]&#39;/system/console/crypto.
   >    1. In **[!UICONTROL Testo normale]** campo , specifica la password o qualsiasi stringa da crittografare e toccare **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >Il testo crittografato viene visualizzato nel campo Testo protetto che è possibile specificare nella configurazione.

1. Abilita **[!UICONTROL Test su credito]** o **[!UICONTROL Test al ritorno]** per specificare che gli oggetti vengono convalidati prima di essere presi in prestito o restituiti rispettivamente da e al pool.
1. Specificare una query SQL SELECT nel **[!UICONTROL Query di convalida]** campo per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specifica una delle seguenti opzioni:

   * SELECT 1 (MySQL e MS SQL)
   * SELECT 1 from dual (Oracle)

1. Tocca **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare AEM profilo utente {#configure-aem-user-profile}

È possibile configurare AEM profilo utente utilizzando la configurazione di User Profile Connector in AEM Web Console. Effettua le seguenti operazioni:

1. Vai AEM console Web all&#39;indirizzo https://&#39;[server]:[porta]&#39;system/console/configMgr.
1. Cerca **[!UICONTROL Integrazioni dei dati AEM Forms - Configurazione del connettore del profilo utente]** e tocca per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo Configurazione connettore profilo utente puoi aggiungere, rimuovere o aggiornare le proprietà del profilo utente. Le proprietà specificate saranno disponibili per l’uso nel modello dati del modulo. Utilizza il formato seguente per specificare le proprietà del profilo utente:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Esempi:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >La **&#42;** nell&#39;esempio precedente denota tutti i nodi sotto il `profile/empLocation/` in AEM profilo utente nella struttura CRXDE. Ciò significa che il modello dati del modulo può accedere al `city` proprietà di tipo `string` presenti in qualsiasi nodo sotto il `profile/empLocation/` nodo. Tuttavia, i nodi che contengono la proprietà specificata devono seguire una struttura coerente.

1. Tocca **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

>[!NOTE]
>
>La configurazione della cartella dei servizi cloud è necessaria per configurare i servizi cloud per i servizi RESTful, SOAP e OData.

Tutte le configurazioni di servizi cloud in AEM sono consolidate nella variabile `/conf` in AEM archivio. Per impostazione predefinita, la `conf` la cartella contiene `global` in cui puoi creare configurazioni di servizi cloud. Tuttavia, devi abilitarlo manualmente per le configurazioni cloud. Puoi anche creare cartelle aggiuntive in `conf` per creare e organizzare configurazioni di servizi cloud.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Vai a **[!UICONTROL Strumenti > Generale > Browser di configurazione]**.
   * Consulta la sezione [Browser di configurazione](/help/sites-administering/configurations.md) documentazione per ulteriori informazioni.
1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud o salta questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

   1. In **[!UICONTROL Browser di configurazione]**, seleziona `global` tocca e fai clic su **[!UICONTROL Proprietà]**.

   1. In **[!UICONTROL Proprietà di configurazione]** finestra di dialogo, attiva **[!UICONTROL Configurazioni cloud]**.

   1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. In **[!UICONTROL Browser di configurazione]**, tocca **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** , specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configurare i servizi web RESTful {#configure-restful-web-services}

Il servizio Web RESTful può essere descritto utilizzando [Specifiche Swagger](https://swagger.io/specification/) in formato JSON o YAML in un file di definizione Swagger. Per configurare il servizio Web RESTful in AEM Cloud Services, accertati di disporre del file Swagger sul file system o dell’URL in cui è ospitato il file.

Per configurare i servizi RESTful, procedi come segue:

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Vedi [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio RESTful]** dal **[!UICONTROL Tipo di servizio]** a discesa, se lo desideri, sfoglia e seleziona un’immagine in miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
1. Specifica i seguenti dettagli per il servizio RESTful:

   * Selezionare URL o File dal menu a discesa Sorgente Swagger e quindi specificare l&#39;URL Swagger nel file di definizione Swagger o caricare il file Swagger dal file system locale.
   * In base all’input Sorgente Swagger , i seguenti campi sono precompilati con valori:

      * Schema: I protocolli di trasferimento utilizzati dall’API REST. Il numero di tipi di schemi visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nell&#39;origine Swagger.
      * Host: Il nome di dominio o l’indirizzo IP dell’host che serve l’API REST. È un campo obbligatorio.
      * Percorso di base: Prefisso URL per tutti i percorsi API. È un campo facoltativo.\
         Se necessario, modifica i valori precompilati per questi campi.
   * Seleziona il tipo di autenticazione — Nessuno, OAuth2.0, Autenticazione di base, Chiave API, Autenticazione personalizzata o Autenticazione reciproca — per accedere al servizio RESTful e, di conseguenza, fornisci i dettagli per l’autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una delle seguenti opzioni dal menu **[!UICONTROL Posizione]** elenco a discesa e specifica il nome dell’intestazione o il parametro della query nel **[!UICONTROL Nome parametro]** di conseguenza.

   Se si seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, vedi [Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP](#mutual-authentication).

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

### Configurazione del client HTTP del modello dati modulo per ottimizzare le prestazioni {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] modello di dati modulo durante l’integrazione con i servizi web RESTful come origine dati include configurazioni client HTTP per l’ottimizzazione delle prestazioni.
Per configurare il client HTTP del modello di dati del modulo, effettua le seguenti operazioni:

1. Accedi a [!DNL Experience Manager Forms] Istanza autore come amministratore e vai a [!DNL Experience Manager] bundle della console web. L’URL predefinito è [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Tocca **[!UICONTROL Configurazione client HTTP del modello dati modulo per l’origine dati REST]**.

1. In [!UICONTROL Configurazione client HTTP del modello dati modulo per l’origine dati REST] finestra di dialogo:

   * Specificare il numero massimo di connessioni consentite tra il modello dati del modulo e i servizi web RESTful nella **[!UICONTROL Limite di connessione totale]** campo . Il valore predefinito è 20 connessioni.

   * Specificare il numero massimo di connessioni consentite per ogni route nella **[!UICONTROL Limite di connessione per rotta]** campo . Il valore predefinito è 2 connessioni.

   * Specifica la durata, per la quale una connessione HTTP persistente viene mantenuta in vita, nel **[!UICONTROL Mantieni vivo]** campo . Il valore predefinito è 15 secondi.

   * Specifica la durata per la quale il [!DNL Experience Manager Forms] il server attende una connessione da stabilire, nel **[!UICONTROL Timeout connessione]** campo . Il valore predefinito è 10 secondi.

   * Specifica il periodo di tempo massimo per l&#39;inattività tra due pacchetti di dati nel **[!UICONTROL Timeout del socket]** campo . Il valore predefinito è 30 secondi.


## Configurare i servizi Web SOAP {#configure-soap-web-services}

I servizi web basati su SOAP sono descritti utilizzando [Specifiche WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). Per configurare il servizio Web basato su SOAP in AEM Cloud Services, assicurati di disporre dell’URL WSDL per il servizio Web ed effettua le seguenti operazioni:

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Vedi [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio Web SOAP]** dal **[!UICONTROL Tipo di servizio]** a discesa, se lo desideri, sfoglia e seleziona un’immagine in miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
1. Specifica quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificare un valore in questo campo per sostituire l&#39;endpoint del servizio menzionato in WSDL.
   * Selezionare il tipo di autenticazione - Nessuno, OAuth2.0, Autenticazione di base, Autenticazione personalizzata, Token X509 o Autenticazione reciproca - per accedere al servizio SOAP e, di conseguenza, fornire i dettagli per l’autenticazione.

      Se si seleziona **[!UICONTROL Token X509]** come tipo di autenticazione, configura il certificato X509. Per ulteriori informazioni, consulta [Imposta certificati](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Specifica l&#39;alias KeyStore per il certificato X509 nel **[!UICONTROL Alias chiave]** campo . Specifica l’ora, in secondi, fino a quando la richiesta di autenticazione non rimane valida, nel **[!UICONTROL Tempo di vita]** campo . Facoltativamente, seleziona per firmare il corpo del messaggio o l’intestazione della marca temporale o entrambe.

      Se si seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, vedi [Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP](#mutual-authentication).

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio Web SOAP.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL principale del servizio. Per configurare un servizio OData in AEM Cloud Services, accertati di disporre dell’URL principale del servizio e procedi come segue:

>[!NOTE]
>
> Il modello dati del modulo supporta [OData versione 4](https://www.odata.org/documentation/).
>Per una guida dettagliata sulla configurazione di Microsoft Dynamics 365, online o on-premise, consulta [Configurazione di Microsoft Dynamics OData](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Vedi [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio OData]** dal **[!UICONTROL Tipo di servizio]** a discesa, se lo desideri, sfoglia e seleziona un’immagine in miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
1. Specifica i seguenti dettagli per il servizio OData:

   * URL principale del servizio per il servizio OData da configurare.
   * Seleziona il tipo di autenticazione (Nessuno, OAuth2.0, Autenticazione di base o Autenticazione personalizzata) per accedere al servizio OData e, di conseguenza, fornisci i dettagli per l’autenticazione.

   >[!NOTE]
   >
   >È necessario selezionare il tipo di autenticazione OAuth 2.0 per connettersi con i servizi Microsoft Dynamics utilizzando l’endpoint OData come radice del servizio.

1. Tocca **Crea** per creare la configurazione cloud per il servizio OData.

## Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP {#mutual-authentication}

Quando si abilita l’autenticazione reciproca per il modello dati modulo, sia l’origine dati che AEM server che esegue il modello dati modulo si autenticano reciprocamente prima di condividere i dati. È possibile utilizzare l’autenticazione reciproca per le connessioni basate su REST e SOAP (origini dati). Per configurare l’autenticazione reciproca per un modello di dati modulo nell’ambiente AEM Forms:

1. Carica la chiave privata (certificato) in [!DNL AEM Forms] server. Per caricare la chiave privata:
   1. Accedi al tuo [!DNL AEM Forms] come amministratore.
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**. Seleziona la `fd-cloudservice` utente e tocca **[!UICONTROL Proprietà]**.
   1. Apri **[!UICONTROL Keystore]** scheda , espandi **[!UICONTROL Aggiungi chiave privata dal file KeyStore]** , carica il file KeyStore, specifica gli alias, le password e tocca **[!UICONTROL Invia]**. Il certificato viene caricato.  L’alias della chiave privata è menzionato nel certificato e impostato durante la creazione del certificato.
1. Carica il certificato di attendibilità nell&#39;archivio locale globale. Per caricare il certificato:
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Archiviazione attendibile]**.
   1. Espandi la **[!UICONTROL Aggiungi certificato dal file CER]** opzione, tocca **[!UICONTROL Seleziona file di certificato]**, carica il certificato e tocca **[!UICONTROL Invia]**.
1. Configura [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) servizi web come origine dati e seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione. Se si configurano più certificati autofirmati per `fd-cloudservice` utente, specifica il nome dell&#39;alias chiave del certificato.

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. Successivamente è possibile creare un modello dati modulo oppure, se è già stato creato un modello dati modulo senza un’origine dati, è possibile associarlo alle origini dati appena configurate. Vedi [Crea modello dati modulo](/help/forms/using/create-form-data-models.md) per i dettagli.
