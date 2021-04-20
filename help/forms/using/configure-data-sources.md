---
title: Configurare origini dati
seo-title: Configurare origini dati
description: Scopri come configurare diversi tipi di origini dati e come sfruttarle per creare modelli di dati modulo.
seo-description: Scopri come configurare diversi tipi di origini dati e come sfruttarle per creare modelli di dati modulo.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: Form Data Model
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 0%

---


# Configura origini dati{#configure-data-sources}

![](do-not-localize/data-integeration.png)

L’integrazione dei dati di AEM Forms consente di configurare e connettersi a diverse origini dati. I seguenti tipi sono supportati come predefiniti. Tuttavia, con poca personalizzazione, puoi integrare anche altre origini dati.

* Database relazionali - MySQL, Microsoft SQL Server, IBM DB2 e Oracle RDBMS
* Profilo utente AEM
* Servizi web RESTful
* Servizi web basati su SOAP
* Servizi OData

L’integrazione dei dati supporta i tipi di autenticazione predefiniti OAuth2.0, autenticazione di base e API Key e consente l’implementazione dell’autenticazione personalizzata per l’accesso ai servizi web. Mentre i servizi RESTful, basati su SOAP e OData sono configurati in AEM Cloud Services, JDBC per i database relazionali e il connettore per AEM profilo utente sono configurati in AEM console web.

## Configurare il database relazionale {#configure-relational-database}

È possibile configurare database relazionali utilizzando AEM configurazione della console Web. Effettua le seguenti operazioni:

1. Vai AEM console Web all&#39;indirizzo https://server:host/system/console/configMgr.
1. Cerca la configurazione **[!UICONTROL Apache Sling Connection Pooled DataSource]** . Tocca per aprire la configurazione in modalità di modifica.
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
   >    1. Vai a https://&#39;[server]:[port]&#39;/system/console/crypto.
   >    1. Nel campo **[!UICONTROL Testo normale]** , specifica la password o qualsiasi stringa da crittografare e tocca **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >Il testo crittografato viene visualizzato nel campo Testo protetto che è possibile specificare nella configurazione.

1. Abilitare **[!UICONTROL Test su prestito]** o **[!UICONTROL Test su ritorno]** per specificare che gli oggetti vengono convalidati prima di essere presi in prestito o restituiti rispettivamente da e al pool.
1. Specificare una query SQL SELECT nel campo **[!UICONTROL Query di convalida]** per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specifica una delle seguenti opzioni:

   * SELECT 1 (MySQL e MS SQL)
   * SELECT 1 from dual (Oracle)

1. Tocca **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare AEM profilo utente {#configure-aem-user-profile}

È possibile configurare AEM profilo utente utilizzando la configurazione di User Profile Connector in AEM Web Console. Effettua le seguenti operazioni:

1. Vai AEM console Web all&#39;indirizzo https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Cerca **[!UICONTROL Integrazioni dati AEM Forms - Configurazione connettore profilo utente]** e tocca per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo Configurazione connettore profilo utente puoi aggiungere, rimuovere o aggiornare le proprietà del profilo utente. Le proprietà specificate saranno disponibili per l’uso nel modello dati del modulo. Utilizza il formato seguente per specificare le proprietà del profilo utente:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Esempi:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >Il ***** nell&#39;esempio precedente denota tutti i nodi sotto il nodo `profile/empLocation/` nel profilo utente AEM nella struttura CRXDE. Ciò significa che il modello dati del modulo può accedere alla proprietà `city` di tipo `string` presente in qualsiasi nodo sotto il nodo `profile/empLocation/`. Tuttavia, i nodi che contengono la proprietà specificata devono seguire una struttura coerente.

1. Tocca **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

>[!NOTE]
La configurazione della cartella dei servizi cloud è necessaria per configurare i servizi cloud per i servizi RESTful, SOAP e OData.

Tutte le configurazioni del servizio cloud in AEM sono consolidate nella cartella `/conf` nell’archivio AEM. Per impostazione predefinita, la cartella `conf` contiene la cartella `global` in cui è possibile creare configurazioni del servizio cloud. Tuttavia, devi abilitarlo manualmente per le configurazioni cloud. Puoi anche creare cartelle aggiuntive in `conf` per creare e organizzare configurazioni di servizi cloud.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Vai a **[!UICONTROL Strumenti > Generale > Browser di configurazione]**.
   * Per ulteriori informazioni, consulta la documentazione [Browser configurazioni](/help/sites-administering/configurations.md) .
1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud o salta questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

   1. Nel **[!UICONTROL Browser configurazioni]**, seleziona la cartella `global` e tocca **[!UICONTROL Proprietà]**.

   1. Nella finestra di dialogo **[!UICONTROL Proprietà configurazione]**, abilita **[!UICONTROL Configurazioni cloud]**.

   1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Nel **[!UICONTROL Browser di configurazione]**, tocca **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configura i servizi web RESTful {#configure-restful-web-services}

Il servizio Web RESTful può essere descritto utilizzando [Specifiche Swagger](https://swagger.io/specification/) in formato JSON o YAML in un file di definizione Swagger. Per configurare il servizio Web RESTful in AEM Cloud Services, accertati di disporre del file Swagger sul file system o dell’URL in cui è ospitato il file.

Per configurare i servizi RESTful, procedi come segue:

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni dei servizi cloud, consulta [Configurare la cartella per le configurazioni dei servizi cloud.](../../forms/using/configure-data-sources.md#cloud-folder)

1. Tocca **[!UICONTROL Crea]** per aprire la **[!UICONTROL procedura guidata Crea configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL RESTful Service]** dal menu a discesa **[!UICONTROL Tipo di servizio]**, se lo desideri, sfoglia e seleziona un&#39;immagine di miniatura per la configurazione, quindi tocca **[!UICONTROL Avanti]**.
1. Specifica i seguenti dettagli per il servizio RESTful:

   * Selezionare URL o File dal menu a discesa Sorgente Swagger e quindi specificare l&#39;URL Swagger nel file di definizione Swagger o caricare il file Swagger dal file system locale.
   * In base all’input Sorgente Swagger , i seguenti campi sono precompilati con valori:

      * Schema: I protocolli di trasferimento utilizzati dall’API REST. Il numero di tipi di schemi visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nell&#39;origine Swagger.
      * Host: Il nome di dominio o l’indirizzo IP dell’host che serve l’API REST. È un campo obbligatorio.
      * Percorso di base: Prefisso URL per tutti i percorsi API. È un campo facoltativo.\
         Se necessario, modifica i valori precompilati per questi campi.
   * Seleziona il tipo di autenticazione — Nessuno, OAuth2.0, Autenticazione di base, Chiave API, Autenticazione personalizzata o Autenticazione reciproca — per accedere al servizio RESTful e, di conseguenza, fornisci i dettagli per l’autenticazione.

   Se selezioni **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Selezionare una di queste opzioni dall&#39;elenco a discesa **[!UICONTROL Posizione]** e specificare di conseguenza il nome dell&#39;intestazione o il parametro della query nel campo **[!UICONTROL Nome parametro]**.

   Se selezioni **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, consulta [Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP](#mutual-authentication).

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

### Configurazione del client HTTP del modello dati modulo per ottimizzare le prestazioni {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] modello di dati modulo durante l’integrazione con i servizi web RESTful come origine dati include configurazioni client HTTP per l’ottimizzazione delle prestazioni.
Per configurare il client HTTP del modello di dati del modulo, effettua le seguenti operazioni:

1. Accedi a [!DNL Experience Manager Forms] Author Instance come amministratore e vai ai bundle della console Web [!DNL Experience Manager]. L&#39;URL predefinito è [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Tocca **[!UICONTROL Configurazione client HTTP per il modello dati modulo per l’origine dati REST]**.

1. Nella finestra di dialogo [!UICONTROL Configurazione client HTTP per il modello dati modulo per l’origine dati REST] :

   * Specificare il numero massimo di connessioni consentite tra il modello dati del modulo e i servizi Web RESTful nel campo **[!UICONTROL Limite di connessione in totale]**. Il valore predefinito è 20 connessioni.

   * Specificare il numero massimo di connessioni consentite per ogni rotta nel campo **[!UICONTROL Limite di connessione per ogni rotta]**. Il valore predefinito è 2 connessioni.

   * Specifica la durata per la quale una connessione HTTP permanente viene mantenuta in vita nel campo **[!UICONTROL Mantieni in vita]** . Il valore predefinito è 15 secondi.

   * Specifica la durata, per la quale il server [!DNL Experience Manager Forms] attende una connessione da stabilire, nel campo **[!UICONTROL Timeout connessione]**. Il valore predefinito è 10 secondi.

   * Specifica il periodo di tempo massimo per l&#39;inattività tra due pacchetti di dati nel campo **[!UICONTROL Timeout socket]** . Il valore predefinito è 30 secondi.


## Configurare i servizi Web SOAP {#configure-soap-web-services}

I servizi Web basati su SOAP sono descritti utilizzando le specifiche [WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). Per configurare il servizio Web basato su SOAP in AEM Cloud Services, assicurati di disporre dell’URL WSDL per il servizio Web ed effettua le seguenti operazioni:

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni dei servizi cloud, consulta [Configurare la cartella per le configurazioni dei servizi cloud.](../../forms/using/configure-data-sources.md#cloud-folder)

1. Tocca **[!UICONTROL Crea]** per aprire la **[!UICONTROL procedura guidata Crea configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio Web SOAP]** dal menu a discesa **[!UICONTROL Tipo di servizio]**, sfoglia facoltativamente e seleziona un&#39;immagine di miniatura per la configurazione, quindi tocca **[!UICONTROL Avanti]**.
1. Specifica quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificare un valore in questo campo per sostituire l&#39;endpoint del servizio menzionato in WSDL.
   * Selezionare il tipo di autenticazione - Nessuno, OAuth2.0, Autenticazione di base, Autenticazione personalizzata, Token X509 o Autenticazione reciproca - per accedere al servizio SOAP e, di conseguenza, fornire i dettagli per l’autenticazione.

      Se selezioni **[!UICONTROL X509 Token]** come tipo di autenticazione, configura il certificato X509. Per ulteriori informazioni, consulta [Configurare i certificati](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Specifica l&#39;alias KeyStore per il certificato X509 nel campo **[!UICONTROL Alias chiave]** . Specifica l&#39;ora, in secondi, fino a quando la richiesta di autenticazione non rimane valida, nel campo **[!UICONTROL Time To Live]** . Facoltativamente, seleziona per firmare il corpo del messaggio o l’intestazione della marca temporale o entrambe.

      Se selezioni **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, consulta [Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP](#mutual-authentication).

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio Web SOAP.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL principale del servizio. Per configurare un servizio OData in AEM Cloud Services, accertati di disporre dell’URL principale del servizio e procedi come segue:

>[!NOTE]
Per una guida dettagliata alla configurazione di Microsoft Dynamics 365, online o on-premise, consulta [Configurazione di Microsoft Dynamics OData](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni dei servizi cloud, consulta [Configurare la cartella per le configurazioni dei servizi cloud.](../../forms/using/configure-data-sources.md#cloud-folder)

1. Tocca **[!UICONTROL Crea]** per aprire la **[!UICONTROL procedura guidata Crea configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio OData]** dal menu a discesa **[!UICONTROL Tipo di servizio]**, se lo desideri, sfoglia e seleziona un&#39;immagine di miniatura per la configurazione, quindi tocca **[!UICONTROL Avanti]**.
1. Specifica i seguenti dettagli per il servizio OData:

   * URL principale del servizio per il servizio OData da configurare.
   * Seleziona il tipo di autenticazione (Nessuno, OAuth2.0, Autenticazione di base o Autenticazione personalizzata) per accedere al servizio OData e, di conseguenza, fornisci i dettagli per l’autenticazione.

   >[!NOTE]
   È necessario selezionare il tipo di autenticazione OAuth 2.0 per connettersi con Microsoft Dynamics Services utilizzando l’endpoint OData come radice del servizio.

1. Tocca **Crea** per creare la configurazione cloud per il servizio OData.

## Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP {#mutual-authentication}

Quando si abilita l’autenticazione reciproca per il modello dati modulo, sia l’origine dati che AEM server che esegue il modello dati modulo si autenticano reciprocamente prima di condividere i dati. È possibile utilizzare l’autenticazione reciproca per le connessioni basate su REST e SOAP (origini dati). Per configurare l’autenticazione reciproca per un modello di dati modulo nell’ambiente AEM Forms:

1. Carica la chiave privata (certificato) sul server [!DNL AEM Forms] . Per caricare la chiave privata:
   1. Accedi al tuo server [!DNL AEM Forms] come amministratore.
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**. Seleziona l&#39;utente `fd-cloudservice` e tocca **[!UICONTROL Proprietà]**.
   1. Apri la scheda **[!UICONTROL Registro chiavi]**, espandi l&#39;opzione **[!UICONTROL Aggiungi chiave privata dal file KeyStore]**, carica il file KeyStore, specifica gli alias, le password e tocca **[!UICONTROL Invia]**. Il certificato viene caricato.  L’alias della chiave privata è menzionato nel certificato e impostato durante la creazione del certificato.
1. Carica il certificato di attendibilità nell&#39;archivio locale globale. Per caricare il certificato:
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Archivio fonti attendibili]**.
   1. Espandi l’opzione **[!UICONTROL Aggiungi certificato dal file CER]**, tocca **[!UICONTROL Seleziona file certificato]**, carica il certificato e tocca **[!UICONTROL Invia]**.
1. Configura i servizi web [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) come origine dei dati e seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione. Se si configurano più certificati autofirmati per l&#39;utente `fd-cloudservice`, specificare il nome dell&#39;alias chiave per il certificato.

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. Successivamente è possibile creare un modello dati modulo oppure, se è già stato creato un modello dati modulo senza un’origine dati, è possibile associarlo alle origini dati appena configurate. Per ulteriori informazioni, vedere [Creare un modello dati modulo](/help/forms/using/create-form-data-models.md) .
