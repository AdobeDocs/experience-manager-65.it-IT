---
title: Configurare le origini dati
seo-title: Configurare le origini dati
description: Scoprite come configurare diversi tipi di origini dati e utilizzare i moduli per creare modelli di dati.
seo-description: Scoprite come configurare diversi tipi di origini dati e utilizzare i moduli per creare modelli di dati.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: ee2b13f2fc1f044f119ff54f332844d458663287
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 0%

---


# Configurare le origini dati{#configure-data-sources}

![](do-not-localize/data-integeration.png)

 Integrazione dei dati AEM Forms consente di configurare e connettersi a origini dati diverse. I seguenti tipi sono supportati out-of-the-box. Tuttavia, con poca personalizzazione, è possibile integrare anche altre origini dati.

* Database relazionali - MySQL, Microsoft SQL Server, IBM DB2 e Oracle RDBMS
* AEM profilo utente
* Servizi Web RESTful
* Servizi Web basati su SOAP
* Servizi OData

L&#39;integrazione dei dati supporta tipi di autenticazione oututh2.0, autenticazione di base e chiave API out-of-the-box e consente l&#39;implementazione dell&#39;autenticazione personalizzata per l&#39;accesso ai servizi Web. Mentre i servizi RESTful, SOAP e OData sono configurati in AEM Cloud Services, JDBC per i database relazionali e il connettore per AEM profilo utente è configurato in AEM console Web.

## Configurare il database relazionale {#configure-relational-database}

È possibile configurare i database relazionali utilizzando AEM Configurazione console Web. Effettua le seguenti operazioni:

1. Passate AEM console Web all’indirizzo https://server:host/system/console/configMgr.
1. Cerca la configurazione **[!UICONTROL Apache Sling Connection Pooled DataSource]** . Toccate per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo di configurazione, specificate i dettagli per il database da configurare, ad esempio:

   * Nome dell&#39;origine dati
   * Proprietà del servizio origine dati che memorizza il nome dell&#39;origine dati
   * Nome della classe Java per il driver JDBC
   * URI connessione JDBC
   * Nome utente e password per stabilire la connessione con il driver JDBC

   >[!NOTE]
   >
   >Prima di configurare l&#39;origine dati, assicurarsi di crittografare le informazioni riservate come password. Per crittografare:
   >
   >    
   >    
   >    1. Accedete a https://&#39;[server]:[porta]&#39;/system/console/crypto.
   >    1. Nel campo Testo **** normale, specificate la password o qualsiasi stringa da cifrare e toccate **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >Il testo cifrato viene visualizzato nel campo Testo protetto che è possibile specificare nella configurazione.

1. Abilitare **[!UICONTROL Test su prestito]** o **[!UICONTROL Test su ritorno]** per specificare che gli oggetti vengono convalidati prima di essere presi in prestito o restituiti da e verso il pool, rispettivamente.
1. Specificare una query SQL SELECT nel campo Query **[!UICONTROL di]** convalida per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specificate una delle seguenti opzioni:

   * SELECT 1 (MySQL e MS SQL)
   * SELECT 1 from dual (Oracle)

1. Toccate **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare AEM profilo utente {#configure-aem-user-profile}

È possibile configurare AEM profilo utente mediante la configurazione Connettore profilo utente in AEM console Web. Effettua le seguenti operazioni:

1. Passate AEM console Web in https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Cerca **[!UICONTROL integrazioni dati AEM Forms - Configurazione]** connettore profilo utente e tocca per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo Configurazione connettore profilo utente, potete aggiungere, rimuovere o aggiornare le proprietà del profilo utente. Le proprietà specificate saranno disponibili per l&#39;uso nel modello dati del modulo. Utilizzate il formato seguente per specificare le proprietà del profilo utente:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Esempi:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >L&#39;esempio ***** riportato sopra indica tutti i nodi sotto il `profile/empLocation/` nodo nel profilo utente AEM struttura CRXDE. Ciò significa che il modello dati modulo può accedere alla `city` proprietà di tipo `string` presente in qualsiasi nodo sotto il `profile/empLocation/` nodo. Tuttavia, i nodi che contengono la proprietà specificata devono seguire una struttura coerente.

1. Toccate **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

>[!NOTE]
La configurazione della cartella dei servizi cloud è necessaria per configurare i servizi cloud per i servizi RESTful, SOAP e OData.

Tutte le configurazioni del servizio cloud in AEM sono consolidate nella `/conf` cartella AEM repository. Per impostazione predefinita, la `conf` cartella contiene la `global` cartella in cui è possibile creare configurazioni del servizio cloud. Tuttavia, è necessario abilitarlo manualmente per le configurazioni cloud. Potete anche creare ulteriori cartelle in `conf` per creare e organizzare le configurazioni del servizio cloud.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Go to **[!UICONTROL Tools > General > Configuration Browser]**.
1. Effettuate le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud o saltate questo passaggio per creare e configurare un&#39;altra cartella per le configurazioni del servizio cloud.

   1. Nel browser **** Configurazione, selezionate la `global` cartella e toccate **[!UICONTROL Proprietà]**.

   1. Nella finestra di dialogo Proprietà **** configurazione, abilita Configurazioni **** Cloud.

   1. Toccate **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Nel browser **** Configurazione, toccate **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]** , specificate un titolo per la cartella e abilitate **[!UICONTROL Cloud Configurations]**.
1. Toccate **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configurare i servizi Web RESTful {#configure-restful-web-services}

Il servizio Web RESTful può essere descritto utilizzando le specifiche [](https://swagger.io/specification/) Swagger in formato JSON o YAML in un file di definizione Swagger. Per configurare il servizio Web RESTful nei servizi cloud di AEM, accertatevi di disporre del file Swagger nel file system o dell&#39;URL in cui è ospitato il file.

Per configurare i servizi RESTful, effettuate le seguenti operazioni:

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini]** dati. Toccate per selezionare la cartella in cui desiderate creare una configurazione cloud.

   Consultate [Configurare la cartella per le configurazioni](../../forms/using/configure-data-sources.md#cloud-folder) del servizio cloud per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Toccate **[!UICONTROL Crea]** per aprire la procedura guidata **** Crea configurazione origine dati. Specificate un nome ed eventualmente un titolo per la configurazione, selezionate **[!UICONTROL RESTful Service]** dal menu a discesa **[!UICONTROL Service Type]** (Tipo **[!UICONTROL servizio), oppure, facoltativamente, sfogliate e selezionate una miniatura per la configurazione, quindi toccate]** Next (Avanti).
1. Specificare i seguenti dettagli per il servizio RESTful:

   * Selezionate URL o File dal menu a discesa Sorgente swagger, quindi specificate l&#39;URL Swagger per il file di definizione Swagger oppure caricate il file Swagger dal file system locale.
   * In base all&#39;input Sorgente Swagger, i seguenti campi sono precompilati con valori:

      * Schema: I protocolli di trasferimento utilizzati dall&#39;API REST. Il numero di tipi di schema visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nell&#39;origine Swagger.
      * Host: Il nome di dominio o l&#39;indirizzo IP dell&#39;host che fornisce l&#39;API REST. È un campo obbligatorio.
      * Percorso di base: Prefisso URL per tutti i percorsi API. È un campo facoltativo.\
         Se necessario, modificate i valori precompilati per questi campi.
   * Selezionare il tipo di autenticazione — Nessuno, OAuth2.0, autenticazione di base, chiave API, autenticazione personalizzata o autenticazione reciproca — per accedere al servizio RESTful e fornire quindi i dettagli per l&#39;autenticazione.

   Se selezionate Chiave **** API come tipo di autenticazione, specificate il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Selezionate una di queste opzioni dall&#39;elenco a discesa **[!UICONTROL Posizione]** e specificate di conseguenza il nome dell&#39;intestazione o il parametro di query nel campo Nome **** parametro.

   Se si seleziona Autenticazione **** reciproca come tipo di autenticazione, vedere Autenticazione reciproca basata su [certificato per i servizi](#mutual-authentication)Web RESTful e SOAP.

1. Toccate **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

## Configurare i servizi Web SOAP {#configure-soap-web-services}

I servizi Web basati su SOAP sono descritti utilizzando le specifiche [WSDL (](https://www.w3.org/TR/wsdl)Web Services Description Language). Per configurare il servizio Web basato su SOAP nei servizi cloud AEM, accertatevi di disporre dell&#39;URL WSDL per il servizio Web ed effettuate le seguenti operazioni:

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini]** dati. Toccate per selezionare la cartella in cui desiderate creare una configurazione cloud.

   Consultate [Configurare la cartella per le configurazioni](../../forms/using/configure-data-sources.md#cloud-folder) del servizio cloud per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Toccate **[!UICONTROL Crea]** per aprire la procedura guidata **** Crea configurazione origine dati. Specificate un nome ed eventualmente un titolo per la configurazione, selezionate **[!UICONTROL SOAP Web Service]** dal menu a discesa **[!UICONTROL Service Type]** (Tipo **[!UICONTROL servizio), oppure, facoltativamente, sfogliate e selezionate una miniatura per la configurazione, quindi toccate]** Next (Avanti).
1. Specificate quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificate un valore in questo campo per ignorare l&#39;endpoint del servizio indicato in WSDL.
   * Selezionare il tipo di autenticazione — Nessuno, OAuth2.0, autenticazione di base, autenticazione personalizzata, token X509 o autenticazione reciproca — per accedere al servizio SOAP e fornire di conseguenza i dettagli per l&#39;autenticazione.

      Se selezionate Token **** X509 come tipo di autenticazione, configurate il certificato X509. Per ulteriori informazioni, vedere [Configurare i certificati](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Specificate l&#39;alias KeyStore per il certificato X509 nel campo Alias **** chiave. Specificate il tempo, in secondi, fino a quando la richiesta di autenticazione non rimane valida, nel campo **[!UICONTROL Tempo di vita]** . Facoltativamente, selezionare per firmare il corpo del messaggio, l&#39;intestazione della marca temporale o entrambe.

      Se si seleziona Autenticazione **** reciproca come tipo di autenticazione, vedere Autenticazione reciproca basata su [certificato per i servizi](#mutual-authentication)Web RESTful e SOAP.

1. Toccate **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio Web SOAP.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL principale del servizio. Per configurare un servizio OData nei servizi cloud AEM, accertatevi di disporre dell’URL principale del servizio per il servizio ed effettuate le seguenti operazioni:

>[!NOTE]
Per una guida dettagliata sulla configurazione di Microsoft Dynamics 365, in linea o in locale, vedere Configurazione [di](/help/forms/using/ms-dynamics-odata-configuration.md)Microsoft Dynamics OData.

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini]** dati. Toccate per selezionare la cartella in cui desiderate creare una configurazione cloud.

   Consultate [Configurare la cartella per le configurazioni](../../forms/using/configure-data-sources.md#cloud-folder) del servizio cloud per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Toccate **[!UICONTROL Crea]** per aprire la procedura guidata **** Crea configurazione origine dati. Specificate un nome ed eventualmente un titolo per la configurazione, selezionate **[!UICONTROL OData Service]** dal menu a discesa **[!UICONTROL Service Type]** (Tipo **[!UICONTROL servizio), oppure, facoltativamente, sfogliate e selezionate una miniatura per la configurazione, quindi toccate]** Next (Avanti).
1. Specificate i seguenti dettagli per il servizio OData:

   * URL radice del servizio per il servizio OData da configurare.
   * Selezionare il tipo di autenticazione — Nessuno, OAuth2.0, autenticazione di base o autenticazione personalizzata — per accedere al servizio OData e fornire quindi i dettagli per l&#39;autenticazione.

   >[!NOTE]
   È necessario selezionare il tipo di autenticazione OAuth 2.0 per connettersi con i servizi di Microsoft Dynamics utilizzando l&#39;endpoint OData come radice del servizio.

1. Toccate **Crea** per creare la configurazione cloud per il servizio OData.

## Autenticazione reciproca basata su certificato per i servizi Web RESTful e SOAP {#mutual-authentication}

Se si abilita l&#39;autenticazione reciproca per il modello di dati del modulo, sia l&#39;origine dati che AEM server in cui è in esecuzione il modello dati del modulo eseguono l&#39;autenticazione reciproca prima della condivisione dei dati. È possibile utilizzare l&#39;autenticazione reciproca per connessioni REST e SOAP (origini dati). Per configurare l&#39;autenticazione reciproca per un modello dati modulo nell&#39;ambiente AEM Forms :

1. Caricate la chiave privata (certificato) sul [!DNL AEM Forms] server. Per caricare la chiave privata:
   1. Accedete al [!DNL AEM Forms] server come amministratore.
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**. Selezionate l’ `fd-cloudservice` utente e toccate **[!UICONTROL Proprietà]**.
   1. Aprite la scheda **[!UICONTROL Keystore]** , espandete l&#39;opzione **[!UICONTROL Aggiungi chiave privata dal file]** KeyStore, caricate il file KeyStore, specificate gli alias, le password e toccate **[!UICONTROL Invia]**. Il certificato viene caricato.  L&#39;alias della chiave privata viene indicato nel certificato e impostato durante la creazione del certificato.
1. Carica il certificato di affidabilità in Global Trust Store. Per caricare il certificato:
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > Archivio **** attendibili.
   1. Espandete l&#39;opzione **[!UICONTROL Aggiungi certificato dal file]** CER, toccate **[!UICONTROL Seleziona file]** certificato, caricate il certificato e toccate **[!UICONTROL Invia]**.
1. Configurare i servizi Web [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) come origine dati e selezionare Autenticazione **** reciproca come tipo di autenticazione. Se configurate più certificati autofirmati per `fd-cloudservice` l&#39;utente, specificate il nome alias chiave per il certificato.

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. È quindi possibile creare un modello dati del modulo o, se è già stato creato un modello dati del modulo senza un&#39;origine dati, è possibile associarlo alle origini dati appena configurate. Per informazioni dettagliate, vedere [Creazione di un modello](/help/forms/using/create-form-data-models.md) dati modulo.
