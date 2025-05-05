---
title: Configurare origini dati
description: Scopri come configurare diversi tipi di origini dati per creare modelli di dati per moduli.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
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

L&#39;integrazione dei dati supporta OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), l&#39;autenticazione di base e i tipi di autenticazione con chiave API predefiniti e consente l&#39;implementazione dell&#39;autenticazione personalizzata per l&#39;accesso ai servizi Web. Mentre i servizi RESTful, basati su SOAP e OData sono configurati nei Cloud Service AEM, JDBC per i database relazionali e il connettore per il profilo utente AEM sono configurati nella console web AEM.

## Configurare il database relazionale {#configure-relational-database}

È possibile configurare i database relazionali utilizzando Configurazione console Web AEM. Effettua le seguenti operazioni:

1. Passa alla console Web AEM all&#39;indirizzo `https://server:host/system/console/configMgr`.
1. Cerca la configurazione dell&#39;**dell&#39;origine dati in pool di connessione Apache Sling**. Seleziona per aprire la configurazione in modalità di modifica.
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
   > 1. Nel campo **[!UICONTROL Testo normale]**, specifica la password o qualsiasi stringa da crittografare e seleziona **[!UICONTROL Protect]**.
   >
   >Il testo crittografato viene visualizzato nel campo Testo protetto che è possibile specificare nella configurazione.

1. Abilitare **[!UICONTROL Test su prestito]** o **[!UICONTROL Test su restituzione]** per specificare che gli oggetti vengono convalidati prima di essere presi in prestito o restituiti rispettivamente da e al pool.
1. Specificare una query SQL SELECT nel campo **[!UICONTROL Query di convalida]** per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specificare una delle seguenti opzioni:

   * SELECT 1 (MySQL e MS SQL)
   * SELECT 1 da dual (Oracle)

1. Seleziona **[!UICONTROL Salva]** per salvare la configurazione.

   >[!NOTE]
   >
   > Se il modello dati di Forms contiene un oggetto che è una parola chiave riservata per il database relazionale, può causare problemi di aggiunta, aggiornamento o recupero di dati. Evita quindi di utilizzare tali oggetti nel modello dati del modulo.

## Configurare il profilo utente AEM {#configure-aem-user-profile}

Puoi configurare il profilo utente AEM utilizzando la configurazione del connettore profilo utente nella console web AEM. Effettua le seguenti operazioni:

1. Vai alla console Web AEM all&#39;indirizzo https://&#39;[server]:[porta]&#39;system/console/configMgr.
1. Cerca **[!UICONTROL Integrazioni dati di AEM Forms - Configurazione connettore profilo utente]** e seleziona per aprire la configurazione in modalità di modifica.
1. Nella finestra di dialogo Configurazione connettore profilo utente puoi aggiungere, rimuovere o aggiornare le proprietà del profilo utente. Le proprietà specificate sono disponibili per l&#39;utilizzo nel modello dati del modulo. Utilizza il seguente formato per specificare le proprietà del profilo utente:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Esempi:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >**&#42;** nell&#39;esempio precedente denota tutti i nodi sotto il nodo `profile/empLocation/` nel profilo utente AEM nella struttura CRXDE. Ciò significa che il modello dati del modulo può accedere alla proprietà `city` di tipo `string` presente in qualsiasi nodo sotto il nodo `profile/empLocation/`. Tuttavia, i nodi che contengono la proprietà specificata devono seguire una struttura coerente.

1. Seleziona **[!UICONTROL Salva]** per salvare la configurazione.

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

>[!NOTE]
>
>Per configurare i servizi cloud per i servizi RESTful, SOAP e OData è necessaria la configurazione della cartella Servizi cloud.

Tutte le configurazioni dei servizi cloud in AEM sono consolidate nella cartella `/conf` nell&#39;archivio AEM. Per impostazione predefinita, la cartella `conf` contiene la cartella `global` in cui è possibile creare configurazioni del servizio cloud. Tuttavia, devi abilitarlo manualmente per le configurazioni cloud. È inoltre possibile creare cartelle aggiuntive in `conf` per creare e organizzare le configurazioni del servizio cloud.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   * Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

   1. Nel **[!UICONTROL Browser configurazioni]**, selezionare la cartella `global` e selezionare **[!UICONTROL Proprietà]**.

   1. Nella finestra di dialogo **[!UICONTROL Proprietà configurazione]**, abilita **[!UICONTROL Configurazioni cloud]**.

   1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Nel **[!UICONTROL Browser configurazioni]**, selezionare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
1. Seleziona **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configurare i servizi web RESTful {#configure-restful-web-services}

È possibile descrivere il servizio Web RESTful utilizzando [le specifiche Swagger](https://swagger.io/specification/) in formato JSON o YAML in un file di definizione Swagger. Per configurare il servizio Web RESTful nei servizi cloud AEM, accertati di disporre del file Swagger sul file system o dell’URL in cui è ospitato il file.

Per configurare i servizi RESTful, effettuare le seguenti operazioni:

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio RESTful]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Avanti]**.
1. Specificare i dettagli seguenti per il servizio RESTful:

   * Selezionate URL o File dal menu a discesa Swagger Source, quindi specificate l&#39;URL Swagger nel file di definizione Swagger o caricate il file Swagger dal file system locale.
   * In base all’input di Swagger Source, i seguenti campi sono precompilati con i valori:

      * Schema: protocolli di trasferimento utilizzati dall’API REST. Il numero di tipi di schema visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nell&#39;origine Swagger.
      * Host: il nome di dominio o l’indirizzo IP dell’host che serve l’API REST. È un campo obbligatorio.
      * Percorso base: prefisso URL per tutti i percorsi API. È un campo facoltativo.\
        Se necessario, modifica i valori precompilati per questi campi.

   * Selezionare il tipo di autenticazione, ovvero Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), Autenticazione di base, Chiave API, Autenticazione personalizzata o Autenticazione reciproca, per accedere al servizio RESTful e fornire di conseguenza i dettagli per l&#39;autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specificare il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dall&#39;elenco a discesa **[!UICONTROL Posizione]** e specifica di conseguenza il nome dell&#39;intestazione o il parametro della query nel campo **[!UICONTROL Nome parametro]**.

   Se si seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, vedere [Autenticazione reciproca basata su certificato per i servizi Web RESTful e SOAP](#mutual-authentication).

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

### Configurazione client HTTP del modello dati modulo per ottimizzare le prestazioni {#fdm-http-client-configuration}

Il modello dati del modulo [!DNL Experience Manager Forms] durante l&#39;integrazione con i servizi Web RESTful come origine dati include configurazioni client HTTP per l&#39;ottimizzazione delle prestazioni.
Per configurare il client HTTP del modello dati modulo, effettua le seguenti operazioni:

1. Accedi all&#39;istanza Autore [!DNL Experience Manager Forms] come amministratore e passa a [!DNL Experience Manager] bundle della console Web. URL predefinito: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Selezionare **[!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST]**.

1. Nella finestra di dialogo Configurazione client HTTP del modello dati modulo [!UICONTROL &#x200B; per l&#39;origine dati REST]:

   * Specifica il numero massimo di connessioni consentite tra il modello di dati del modulo e i servizi Web RESTful nel campo **[!UICONTROL Limite di connessioni in totale]**. Il valore predefinito è 20 connessioni.

   * Specificare il numero massimo di connessioni consentite per ogni route nel campo **[!UICONTROL Limite di connessioni per ogni route]**. Il valore predefinito è 2 connessioni.

   * Nel campo **[!UICONTROL Keep alive]** specificare la durata per la quale una connessione HTTP persistente viene mantenuta attiva. Il valore predefinito è 15 secondi.

   * Nel campo **[!UICONTROL Timeout connessione]** specificare la durata dell&#39;attesa di una connessione da parte del server [!DNL Experience Manager Forms]. Il valore predefinito è 10 secondi.

   * Specificare il periodo di tempo massimo per l&#39;inattività tra due pacchetti di dati nel campo **[!UICONTROL Timeout socket]**. Il valore predefinito è 30 secondi.

## Configurare i servizi web dell’SOAP {#configure-soap-web-services}

I servizi Web basati su SOAP sono descritti utilizzando [le specifiche WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). Per configurare il servizio Web basato su SOAP nei servizi cloud AEM, verificare di disporre dell&#39;URL WSDL per il servizio Web e procedere come segue:

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio Web SOAP]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Avanti]**.
1. Specificare quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificare un valore in questo campo per sostituire l&#39;endpoint del servizio indicato in WSDL.
   * Selezionare il tipo di autenticazione, ovvero Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), Autenticazione di base, Autenticazione personalizzata, Token X509 o Autenticazione reciproca, per accedere al servizio SOAP e fornire i dettagli per l&#39;autenticazione.

     Se si seleziona **[!UICONTROL X509 Token]** come tipo di autenticazione, configurare il certificato X509. Per ulteriori informazioni, vedere [Configurare i certificati](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Specificare l&#39;alias KeyStore per il certificato X509 nel campo **[!UICONTROL Alias chiave]**. Nel campo **[!UICONTROL Durata]** specificare il tempo, in secondi, fino a quando la richiesta di autenticazione non rimane valida. Facoltativamente, seleziona per firmare il corpo del messaggio o l’intestazione della marca temporale o entrambi.

     Se si seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione, vedere [Autenticazione reciproca basata su certificato per i servizi Web RESTful e SOAP](#mutual-authentication).

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio Web SOAP.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL radice del servizio. Per configurare un servizio OData nei servizi cloud AEM, accertarsi di disporre dell&#39;URL principale del servizio ed eseguire le operazioni seguenti:

>[!NOTE]
>
>Il modello dati del modulo supporta [OData versione 4](https://www.odata.org/documentation/).
>Per una guida dettagliata alla configurazione di Microsoft Dynamics 365, online o on-premise, vedere [Configurazione di Microsoft Dynamics OData](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](../../forms/using/configure-data-sources.md#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio OData]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Successivo]**.
1. Specificare i dettagli seguenti per il servizio OData:

   * URL principale del servizio per il servizio OData da configurare.
   * Selezionare il tipo di autenticazione, ovvero Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), Autenticazione di base o Autenticazione personalizzata, per accedere al servizio OData e fornire i dettagli per l&#39;autenticazione.

   >[!NOTE]
   >
   >Seleziona il tipo di autenticazione OAuth 2.0 per connettersi ai servizi Microsoft Dynamics utilizzando l’endpoint OData come radice del servizio.

1. Selezionare **Crea** per creare la configurazione cloud per il servizio OData.

## Autenticazione reciproca basata su certificato per i servizi web RESTful e SOAP {#mutual-authentication}

Quando si abilita l&#39;autenticazione reciproca per il modello dati modulo, sia l&#39;origine dati che il server AEM che esegue il modello dati modulo autenticano l&#39;identità dell&#39;altro prima di condividere i dati. Puoi utilizzare l’autenticazione reciproca per le connessioni basate su REST e SOAP (origini dati). Per configurare l’autenticazione reciproca per un modello di dati modulo nell’ambiente AEM Forms:

1. Caricare la chiave privata (certificato) nel server [!DNL AEM Forms]. Per caricare la chiave privata:
   1. Accedi al server [!DNL AEM Forms] come amministratore.
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**. Selezionare l&#39;utente `fd-cloudservice` e selezionare **[!UICONTROL Proprietà]**.
   1. Apri la scheda **[!UICONTROL Registro chiavi]**, espandi l&#39;opzione **[!UICONTROL Aggiungi chiave privata dal file registro chiavi]**, carica il file registro chiavi, specifica alias, password e seleziona **[!UICONTROL Invia]**. Il certificato è stato caricato.  L’alias della chiave privata viene menzionato nel certificato e impostato durante la creazione del certificato.
1. Carica il certificato di attendibilità nell&#39;archivio fonti attendibili globale. Per caricare il certificato:
   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Archivio attendibile]**.
   1. Espandere l&#39;opzione **[!UICONTROL Aggiungi certificato da file CER]**, selezionare **[!UICONTROL Seleziona file certificato]**, caricare il certificato e selezionare **[!UICONTROL Invia]**.
1. Configura i servizi Web [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) come origine dati e seleziona **[!UICONTROL Autenticazione reciproca]** come tipo di autenticazione. Se si configurano più certificati autofirmati per l&#39;utente `fd-cloudservice`, specificare il nome dell&#39;alias chiave per il certificato.

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. Successivamente è possibile creare un modello dati modulo oppure, se è già stato creato un modello dati modulo senza un&#39;origine dati, è possibile associarlo alle origini dati configurate. Per ulteriori dettagli, vedere [Crea modello dati modulo](/help/forms/using/create-form-data-models.md).
