---
title: Gestione programmatica degli endpoint
seo-title: Programmatically Managing Endpoints
description: Utilizza il servizio Registro endpoint per aggiungere endpoint EJB, aggiungere endpoint SOAP, aggiungere endpoint per cartelle controllate, aggiungere endpoint e-mail, aggiungere endpoint per la comunicazione remota, aggiungere endpoint per Gestione attività, modificare endpoint, rimuovere endpoint e recuperare informazioni sul connettore dell’endpoint.
seo-description: Use the Endpoint Registry service to add EJB endpoints, add SOAP endpoint, add Watched Folder endpoints, add Email endpoints, add  Remoting endpoints, add Task Manager endpoints, modify endpoints, remove endpoints, and retrieve endpoint connector information.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '10801'
ht-degree: 1%

---

# Gestione programmatica degli endpoint {#programmatically-managing-endpoints}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

**Informazioni sul servizio Registro di sistema degli endpoint**

Il servizio Registro endpoint consente di gestire gli endpoint a livello di programmazione. Ad esempio, puoi aggiungere a un servizio i seguenti tipi di endpoint:

* EJB
* SOAP
* Cartella controllata
* E-mail
* (Obsoleto per i moduli AEM) Comunicazione remota
* Gestione attività

>[!NOTE]
>
>Gli endpoint di comunicazione remota SOAP, EJB e (obsoleti per i moduli AEM su JEE) vengono creati automaticamente per ogni servizio attivato. Gli endpoint SOAP ed EJB abilitano SOAP ed EJB per tutte le operazioni del servizio.

Un endpoint remoto consente ai client Flex di richiamare le operazioni sul servizio AEM Forms a cui viene aggiunto l’endpoint. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

Gli endpoint E-mail, Gestione attività e Cartella controllata espongono solo un’operazione specifica del servizio. L&#39;aggiunta di questi endpoint richiede un secondo passaggio di configurazione per selezionare un metodo da richiamare, impostare i parametri di configurazione e specificare le mappature dei parametri di input e output.

È possibile organizzare gli endpoint di TaskManager in gruppi denominati *categorie*. Queste categorie vengono quindi esposte a Workspace tramite TaskManager, con gli utenti finali che visualizzano gli endpoint di TaskManager man mano che vengono categorizzati. In Workspace, gli utenti finali visualizzano queste categorie nel riquadro di navigazione. Gli endpoint all’interno di ogni categoria vengono visualizzati come schede di processo nella pagina Avvia processi di Workspace.

Puoi eseguire queste attività utilizzando il servizio Registro endpoint:

* Aggiungere endpoint EJB. (vedere [Aggiunta di endpoint EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Aggiungere endpoint SOAP. (vedere [Aggiunta di endpoint SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Aggiungi endpoint di cartella controllata (vedere [Aggiunta di endpoint per cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* Aggiungi endpoint e-mail. (vedere [Aggiunta di endpoint e-mail](programmatically-endpoints.md#adding-email-endpoints).)
* Aggiungere endpoint remoti. (vedere [Aggiunta di endpoint remoti](programmatically-endpoints.md#adding-remoting-endpoints).)
* Aggiungere endpoint di TaskManager (vedere [Aggiunta di endpoint TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* Modificare gli endpoint (vedere [Modifica degli endpoint](programmatically-endpoints.md#modifying-endpoints).)
* Rimuovi endpoint (vedere [Rimozione degli endpoint](programmatically-endpoints.md#removing-endpoints).)
* Recuperare le informazioni sul connettore endpoint (vedere [Recupero informazioni sul connettore endpoint](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Aggiunta di endpoint EJB {#adding-ejb-endpoints}

Puoi aggiungere in modo programmatico un endpoint EJB a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint EJB a un servizio, si consente a un&#39;applicazione client di richiamare il servizio utilizzando la modalità EJB. In altre parole, quando imposti le proprietà di connessione necessarie per richiamare AEM Forms, puoi selezionare la modalità EJB. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Non è possibile aggiungere un endpoint EJB utilizzando i servizi Web.

>[!NOTE]
>
>In genere, un endpoint EJB viene aggiunto a un servizio per impostazione predefinita. Tuttavia, un endpoint EJB può essere aggiunto a un processo distribuito a livello di programmazione o quando un endpoint EJB viene rimosso e deve essere aggiunto di nuovo.

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un endpoint EJB a un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un `EndpointRegistry Client` oggetto.
1. Imposta attributi endpoint EJB.
1. Creare un endpoint EJB.
1. Abilita l’endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Prima di poter aggiungere un endpoint EJB a livello di programmazione, è necessario creare un `EndpointRegistryClient` oggetto.

**Imposta attributi endpoint EJB**

Per creare un endpoint EJB per un servizio, specificare i valori seguenti:

* **Identificatore del connettore**: specifica il tipo di endpoint da creare. Per creare un endpoint EJB, specificare `EJB`.
* **Descrizione**: specifica la descrizione dell&#39;endpoint.
* **Nome**: specifica il nome dell&#39;endpoint.
* **Identificatore del servizio**: specifica il servizio a cui appartiene l&#39;endpoint.
* **Nome operazione**: specifica il nome dell&#39;operazione richiamata tramite l&#39;endpoint. Quando crei un endpoint EJB, specifica un carattere jolly ( `*`). Tuttavia, se si desidera specificare un&#39;operazione specifica anziché richiamare tutte le operazioni di servizio, specificare il nome dell&#39;operazione anziché utilizzare il carattere jolly ( `*`).

**Creare un endpoint EJB**

Dopo aver impostato gli attributi dell&#39;endpoint EJB, è possibile creare un endpoint EJB per un servizio.

**Abilita l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Dopo aver abilitato l’endpoint, puoi utilizzarlo per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo all’interno della console di amministrazione.

**Consulta anche**

[Aggiunta di un endpoint EJB tramite API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiunta di un endpoint EJB tramite API Java {#adding-an-ejb-endpoint-using-the-java-api}

Aggiungi un endpoint EJB utilizzando l’API Java:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java. (

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Imposta attributi endpoint EJB.

   * Creare un `CreateEndpointInfo` mediante il costruttore.
   * Specifica il valore dell’identificatore del connettore richiamando `CreateEndpointInfo` dell&#39;oggetto `setConnectorId` e passando il valore stringa `EJB`.
   * Specifica la descrizione dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setDescription` e fornendo un valore stringa che descrive l’endpoint.
   * Specifica il nome dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome.
   * Specifica il servizio a cui appartiene l’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setServiceId` e passando un valore stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando `CreateEndpointInfo` dell&#39;oggetto `setOperationName` e passare un valore stringa che specifica il nome dell&#39;operazione. Per gli endpoint SOAP ed EJB, specificare un carattere jolly ( `*`), che implica tutte le operazioni.

1. Creare un endpoint EJB.

   Creare l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando il `CreateEndpointInfo` oggetto. Questo metodo restituisce un `Endpoint` oggetto che rappresenta il nuovo endpoint EJB.

1. Abilita l’endpoint.

   Abilita l’endpoint richiamando `EndpointRegistryClient` metodo enable dell&#39;oggetto e passaggio di `Endpoint` oggetto restituito da `createEndpoint` metodo.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: aggiunta di un endpoint EJB utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint SOAP {#adding-soap-endpoints}

Puoi aggiungere a livello di programmazione un endpoint SOAP a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint SOAP, si consente a un&#39;applicazione client di richiamare il servizio utilizzando la modalità SOAP. In altre parole, quando si impostano le proprietà di connessione necessarie per richiamare AEM Forms, è possibile selezionare la modalità SOAP.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint SOAP utilizzando i servizi Web.

>[!NOTE]
>
>In genere, un endpoint SOAP viene aggiunto a un servizio per impostazione predefinita. Tuttavia, un endpoint SOAP può essere aggiunto a un processo distribuito a livello di programmazione o quando un endpoint SOAP viene rimosso e deve essere aggiunto di nuovo.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per aggiungere un endpoint SOAP a un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un `EndpointRegistryClient` oggetto.
1. Impostare gli attributi dell&#39;endpoint SOAP.
1. Creare un endpoint SOAP.
1. Abilita l’endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Questi file JAR sono necessari per creare un endpoint SOAP. Tuttavia, se utilizzi l’endpoint SOAP per richiamare il servizio, devi aggiungere dei file JAR. Per informazioni sui file JAR di AEM Forms, consulta [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Per aggiungere a livello di programmazione un endpoint SOAP a un servizio, è necessario creare un `EndpointRegistryClient` oggetto.

**Impostare gli attributi dell’endpoint SOAP**

Per aggiungere un endpoint SOAP a un servizio, specificare i valori seguenti:

* **Valore dell’identificatore del connettore**: specifica il tipo di endpoint da creare. Per creare un endpoint SOAP, specifica `SOAP`.
* **Descrizione**: specifica la descrizione dell&#39;endpoint.
* **Nome**: specifica il nome dell&#39;endpoint.
* **Valore dell’identificatore del servizio**: specifica il servizio a cui appartiene l&#39;endpoint.
* **Nome operazione**: specifica il nome dell&#39;operazione richiamata tramite l&#39;endpoint. Durante la creazione di un endpoint SOAP, specifica un carattere jolly ( `*`). Tuttavia, se si desidera specificare un&#39;operazione specifica anziché richiamare tutte le operazioni di servizio, specificare il nome dell&#39;operazione anziché utilizzare il carattere jolly ( `*`).

**Creare un endpoint SOAP**

Dopo aver impostato gli attributi dell&#39;endpoint SOAP, è possibile creare un endpoint SOAP.

**Abilita l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiungere un endpoint SOAP utilizzando l’API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere un endpoint SOAP utilizzando l’API Java {#add-a-soap-endpoint-using-the-java-api}

Aggiungere un endpoint SOAP a un servizio utilizzando l’API Java:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Impostare gli attributi dell&#39;endpoint SOAP.

   * Creare un `CreateEndpointInfo` mediante il costruttore.
   * Specifica il valore dell’identificatore del connettore richiamando `CreateEndpointInfo` dell&#39;oggetto `setConnectorId` e passando il valore stringa `SOAP`.
   * Specifica la descrizione dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setDescription` e fornendo un valore stringa che descrive l’endpoint.
   * Specifica il nome dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome.
   * Specifica il servizio a cui appartiene l’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setServiceId` e passando un valore stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando `CreateEndpointInfo` dell&#39;oggetto `setOperationName` e passando un valore stringa che specifica il nome dell&#39;operazione. Per gli endpoint SOAP ed EJB, specificare un carattere jolly ( `*`), che implica tutte le operazioni.

1. Creare un endpoint SOAP.

   Creare l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando il `CreateEndpointInfo` oggetto. Questo metodo restituisce un `Endpoint` oggetto che rappresenta il nuovo endpoint SOAP.

1. Abilita l’endpoint.

   Abilita l’endpoint richiamando `EndpointRegistryClient` metodo enable dell&#39;oggetto e passare il `Endpoint` oggetto restituito da `createEndpoint` metodo.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: aggiunta di un endpoint SOAP utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint per cartelle controllate {#adding-watched-folder-endpoints}

Puoi aggiungere in modo programmatico un endpoint di cartella controllata a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint di tipo Cartella controllata, si consente agli utenti di inserire un file, ad esempio un file PDF, in una cartella. Quando il file viene inserito nella cartella, il servizio configurato viene richiamato e modifica il file. Dopo aver eseguito l&#39;operazione specificata, il servizio salva il file modificato in una cartella di output specificata. Una cartella controllata è configurata per essere analizzata a un intervallo di velocità fisso o con una pianificazione cron, ad esempio ogni lunedì, mercoledì e venerdì a mezzogiorno.

Ai fini dell’aggiunta a livello di programmazione di un endpoint di cartella controllata a un servizio, considera il seguente processo di breve durata denominato *Crittografia documento*. (vedere [Informazioni sui processi di AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Questa procedura accetta un documento PDF PDF non protetto come valore di input e quindi lo trasmette al servizio di crittografia `EncryptPDFUsingPassword` operazione. Il documento PDF viene crittografato con una password e il documento PDF crittografato con password è il valore di output di questo processo. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF crittografato con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint di cartella controllata utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-2}

Per aggiungere un endpoint di cartella controllata a un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un `EndpointRegistryClient` oggetto.
1. Imposta gli attributi dell’endpoint della cartella controllata.
1. Specifica i valori di configurazione.
1. Definite i valori dei parametri di input.
1. Definite un valore per il parametro di output.
1. Crea un endpoint per la cartella controllata.
1. Abilita l’endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Per aggiungere a livello di programmazione un endpoint di cartella controllata, è necessario creare un `EndpointRegistryClient` oggetto.

**Imposta attributi endpoint cartella controllata**

Per creare un endpoint di cartella controllata per un servizio, specifica i seguenti valori:

* **Identificatore del connettore**: specifica il tipo di endpoint creato. Per creare un endpoint di cartella controllata, specifica `WatchedFolder`.
* **Descrizione**: specifica la descrizione dell&#39;endpoint.
* **Nome**: specifica il nome dell&#39;endpoint.
* **Identificatore del servizio**: specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint di cartella controllata al processo introdotto in questa sezione (un processo diventa un servizio quando viene attivato utilizzando Workbench), specifica `EncryptDocument`.
* **Nome operazione**: specifica il nome dell&#39;operazione richiamata tramite l&#39;endpoint. In genere, quando si crea un endpoint di cartella controllata per un servizio che ha avuto origine da un processo creato in Workbench, il nome dell’operazione è `invoke`.

**Specificare i valori di configurazione**

È necessario specificare i valori di configurazione per un endpoint di cartella controllata quando si aggiunge a livello di programmazione un endpoint di cartella controllata a un servizio. Questi valori di configurazione vengono specificati da un amministratore se un endpoint di cartella controllata viene aggiunto utilizzando la console di amministrazione.

L&#39;elenco seguente specifica i valori di configurazione impostati quando si aggiunge a livello di programmazione un endpoint di cartella controllata a un servizio:

* **url**: specifica il percorso della cartella controllata. In un ambiente cluster, questo valore deve puntare a una cartella di rete condivisa accessibile da tutti i computer del cluster.
* **asincrono**: identifica il tipo di chiamata come asincrona o sincrona. I processi transitori e sincroni possono essere richiamati solo in modo sincrono. Il valore predefinito è true. Si consiglia l’asincronia.
* **cronExpression**: utilizzato dal quarzo per pianificare il polling della directory di input.
* **purgeDuration**: questo è un attributo obbligatorio. I file e le cartelle nella cartella dei risultati vengono eliminati quando sono più vecchi di questo valore. Questo valore è misurato in giorni. Questo attributo è utile per garantire che la cartella dei risultati non sia piena. Un valore pari a -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
* **repeatInterval**: intervallo, in secondi, per la scansione della cartella controllata per l’input. A meno che la limitazione non sia abilitata, questo valore deve essere più lungo del tempo necessario per elaborare un processo medio; in caso contrario, il sistema potrebbe sovraccaricare. Il valore predefinito è 5.
* **repeatCount**: numero di volte in cui una cartella controllata esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.
* **throttleOn**: limita il numero di processi della cartella controllata che possono essere elaborati in un dato momento. Il numero massimo di processi è determinato dal valore batchSize.
* **userName**: nome utente utilizzato per richiamare un servizio di destinazione dalla cartella controllata. Questo valore è obbligatorio. Il valore predefinito è SuperAdmin.
* **domainName**: dominio dell’utente. Questo valore è obbligatorio. Il valore predefinito è DefaultDom.
* **batchSize**: numero di file o cartelle da raccogliere per analisi. Utilizzare questo valore per evitare un sovraccarico del sistema; la scansione di troppi file contemporaneamente può causare un arresto anomalo. Il valore predefinito è 2.
* **waitTime**: tempo, in millisecondi, di attesa prima della scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 36.000.000 di millisecondi (un’ora) e il file è stato creato un minuto fa, il file viene acquisito dopo 59 o più minuti. Questo attributo è utile per garantire che un file o una cartella sia completamente copiato nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il download richiede dieci minuti, impostare il tempo di attesa su 10&amp;ast;60 &amp;ast;1000 millisecondi. Questa impostazione impedisce alla cartella controllata di eseguire la scansione del file se non è rimasto in attesa per dieci minuti. Il valore predefinito è 0.
* **excludeFilePattern**: pattern utilizzato da una cartella controllata per determinare quali file e cartelle analizzare e raccogliere. Qualsiasi file o cartella con questo modello non verrà analizzato per l&#39;elaborazione. Questa impostazione è utile quando l&#39;input è una cartella contenente più file. Il contenuto della cartella può essere copiato in una cartella il cui nome verrà scelto dalla cartella controllata. Questo passaggio impedisce alla cartella controllata di selezionare una cartella da elaborare prima che venga completamente copiata nella cartella di input. Ad esempio, se il valore excludeFilePattern è `data*`, tutti i file e le cartelle corrispondenti `data*` non vengono prelevati. Ciò include file e cartelle denominati `data1`, `data2`e così via. Inoltre, è possibile aggiungere al modello pattern dei caratteri jolly per specificare i pattern dei file. La cartella controllata modifica l’espressione regolare per supportare i pattern con caratteri jolly, ad esempio `*.*` e `*.pdf`. Questi pattern di caratteri jolly non sono supportati dalle espressioni regolari.
* **includeFilePattern**: pattern utilizzato dalla cartella controllata per determinare quali cartelle e file analizzare e raccogliere. Ad esempio, se questo valore è `*`, tutti i file e le cartelle corrispondenti `input*` vengono prelevati. Ciò include file e cartelle denominati `input1`, `input2`e così via. Il valore predefinito è `*`. Questo valore indica tutti i file e le cartelle. Inoltre, è possibile aggiungere al modello pattern dei caratteri jolly per specificare i pattern dei file. La cartella controllata modifica l’espressione regolare per supportare i pattern con caratteri jolly, ad esempio `*.*` e `*.pdf`. Questi pattern di caratteri jolly non sono supportati dalle espressioni regolari. Questo valore è obbligatorio.
* **resultFolderName**: cartella in cui vengono memorizzati i risultati salvati. Questa posizione può essere un percorso di directory assoluto o relativo. Se i risultati non vengono visualizzati in questa cartella, selezionare la cartella con errori. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Il valore predefinito è `result/%Y/%M/%D/`. Questa è la cartella dei risultati all’interno della cartella controllata.
* **preserveFolderName**: posizione in cui vengono archiviati i file dopo la scansione e il prelievo corretti. Questo percorso può essere assoluto, relativo o nullo. Il valore predefinito è `preserve/%Y/%M/%D/`.
* **failureFolderName**: cartella in cui vengono salvati i file con errori. Questo percorso è sempre relativo alla cartella controllata. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Il valore predefinito è `failure/%Y/%M/%D/`.
* **preserveOnFailure**: mantiene i file di input in caso di mancata esecuzione dell’operazione su un servizio. Il valore predefinito è true.
* **overwriteDuplicateFilename**: quando è impostato su true, i file nella cartella dei risultati e nella cartella di mantenimento vengono sovrascritti. Se è impostato su false, vengono utilizzati per il nome i file e le cartelle con un suffisso di indice numerico. Il valore predefinito è false.

**Definire i valori dei parametri di input**

Quando crei un endpoint di cartella controllata, devi definire i valori dei parametri di input. In altre parole, devi descrivere i valori di input passati all’operazione richiamata dalla cartella controllata. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di input denominato `InDoc` e il suo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint di cartella controllata per questo processo (dopo l’attivazione, il processo diventa un servizio), devi definire il valore del parametro di input.

Per definire i valori dei parametri di input necessari per un endpoint di cartella controllata, specifica i seguenti valori:

**Nome parametro di input**: nome del parametro di input. Il nome di un valore di input viene specificato in Workbench per un processo. Se il valore di input appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di input viene specificato nel file component.xml. Ad esempio, il nome del parametro di input per il processo introdotto in questa sezione è `InDoc`.

**Tipo di mappatura**: utilizzato per configurare i valori di input necessari per richiamare l’operazione di servizio. Esistono due tipi di mappatura:

* `Literal`: l’endpoint della cartella controllata utilizza il valore immesso nel campo così come viene visualizzato. Sono supportati tutti i tipi Java di base. Ad esempio, se un’API utilizza input come String, long, int e Boolean, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.
* `Variable`: il valore immesso è un pattern di file che la cartella controllata utilizza per scegliere l’input. Se ad esempio si seleziona Variabile per il tipo di mapping e il documento di input deve essere un file PDF, è possibile specificare `*.pdf`come valore di mappatura.

**Valore di mappatura**: specifica il valore del tipo di mappatura. Ad esempio, se selezioni un `Variable` tipo di mappatura, puoi specificare `*.pdf` come pattern del file.

**Tipo di dati**: specifica il tipo di dati dei valori di input. Ad esempio, il tipo di dati del valore di input del processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Definisci un valore per il parametro di output**

Quando crei un endpoint di cartella controllata, devi definire un valore per il parametro di output. In altre parole, devi descrivere il valore di output restituito dal servizio richiamato dall’endpoint della cartella controllata. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di output denominato `SecuredDoc` e il suo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint di cartella controllata per questo processo (dopo l’attivazione, il processo diventa un servizio), devi definire il valore del parametro di output.

Per definire il valore di un parametro di output necessario per un endpoint di tipo Cartella controllata, specificare i seguenti valori:

**Nome parametro di output**: nome del parametro di output. Il nome di un valore di output del processo è specificato in Workbench. Se il valore di output appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di output viene specificato nel file component.xml. Ad esempio, il nome del parametro di output per il processo introdotto in questa sezione è `SecuredDoc`.

**Tipo di mappatura**: utilizzato per configurare l’output del servizio e dell’operazione. Sono disponibili le seguenti opzioni:

* Se il servizio restituisce un singolo oggetto (un singolo documento), il modello è `%F.pdf` e la destinazione di origine è sourcefilename.pdf. Ad esempio, il processo introdotto in questa sezione restituisce un singolo documento. Di conseguenza, il tipo di mappatura può essere definito come `%F.pdf` ( `%F` significa utilizzare il nome file specificato). Il pattern `%E` specifica l&#39;estensione del documento di input.
* Se il servizio restituisce un elenco, il modello è `Result\%F\`e la destinazione di origine è Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se il servizio restituisce una mappa, il modello è `Result\%F\`e la destinazione di origine è Result\sourcefilename\file1 e Result\sourcefilename\file2. Se la mappa contiene più oggetti, il modello è `Result\%F.pdf` e la destinazione di origine è Result\sourcefilename1.pdf (output 1), Result\sourcefilenam2.pdf (output 2) e così via.

**Tipo di dati**: specifica il tipo di dati del valore restituito. Ad esempio, il tipo di dati del valore restituito del processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Creare un endpoint di cartella controllata**

Dopo aver impostato gli attributi e i valori di configurazione dell’endpoint e aver definito i valori dei parametri di input e output, è necessario creare l’endpoint della cartella controllata.

**Abilita l’endpoint**

Dopo aver creato un endpoint di cartella controllata, devi abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo all’interno della console di amministrazione.

**Consulta anche**

[Aggiungere un endpoint di cartella controllata utilizzando l’API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere un endpoint di cartella controllata utilizzando l’API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Aggiungi un endpoint Watched Folder utilizzando l’API Java di AEM Forms:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Imposta gli attributi dell’endpoint della cartella controllata.

   * Creare un `CreateEndpointInfo` mediante il costruttore.
   * Specifica il valore dell’identificatore del connettore richiamando `CreateEndpointInfo` dell&#39;oggetto `setConnectorId` e passando il valore stringa `WatchedFolder`.
   * Specifica la descrizione dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setDescription` e fornendo un valore stringa che descrive l’endpoint.
   * Specifica il nome dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome.
   * Specifica il servizio a cui appartiene l’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setServiceId` e passando un valore stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando `CreateEndpointInfo` dell&#39;oggetto `setOperationName` e passando un valore stringa che specifica il nome dell&#39;operazione. In genere, durante la creazione di un endpoint di cartella controllata per un servizio che ha avuto origine da un processo creato in Workbench, viene richiamato il nome dell’operazione.

1. Specifica i valori di configurazione.

   Per ogni valore di configurazione da impostare per l’endpoint della cartella controllata, è necessario richiamare `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` metodo. Ad esempio, per impostare `url` valore di configurazione, richiama il `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e passa i seguenti valori stringa:

   * Valore stringa che specifica il nome del valore di configurazione. Quando si imposta `url` valore di configurazione, specifica `url`.
   * Valore stringa che specifica il valore della configurazione. Quando si imposta `url` valore di configurazione, specifica il percorso della cartella controllata.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori di configurazione impostati per il servizio EncryptDocument, vedere l&#39;esempio di codice Java disponibile in [QuickStart: aggiunta di un endpoint per cartelle controllate utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Definite i valori dei parametri di input.

   Definisci un valore per il parametro di input richiamando `CreateEndpointInfo` dell&#39;oggetto `setInputParameterMapping` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome del parametro di input. Ad esempio, il nome del parametro di input per il servizio EncryptDocument è `InDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di input. Ad esempio, il tipo di dati della proprietà `InDoc` il parametro di input è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mappatura. Ad esempio, puoi specificare `variable`.
   * Valore stringa che specifica il valore del tipo di mapping. Ad esempio, è possibile specificare &amp;ast;.pdf come modello di file.

   >[!NOTE]
   >
   >Richiama `setInputParameterMapping` metodo per ciascun valore del parametro di input da definire. Poiché il processo EncryptDocument dispone di un solo parametro di input, è necessario richiamare questo metodo una volta.

1. Definite un valore per il parametro di output.

   Definisci un valore per il parametro di output richiamando `CreateEndpointInfo` dell&#39;oggetto `setOutputParameterMapping` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome del parametro di output. Ad esempio, il nome del parametro di output per il servizio EncryptDocument è `SecuredDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di output. Ad esempio, il tipo di dati della proprietà `SecuredDoc` il parametro di output è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mappatura. Ad esempio, puoi specificare `%F.pdf`.

1. Crea un endpoint per la cartella controllata.

   Creare l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando il `CreateEndpointInfo` oggetto. Questo metodo restituisce un `Endpoint` oggetto che rappresenta l&#39;endpoint della cartella controllata.

1. Abilita l’endpoint.

   Abilita l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `enable` e passando il `Endpoint` oggetto restituito da `createEndpoint` metodo.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: aggiunta di un endpoint per cartelle controllate utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### File costante dei valori di configurazione della cartella controllata {#watched-folder-configuration-values-constant-file}

Il [QuickStart: aggiunta di un endpoint per cartelle controllate utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utilizza un file costante che deve far parte del progetto Java per compilare l’avvio rapido. Questo file costante rappresenta i valori di configurazione che devono essere impostati quando si aggiunge un endpoint di cartella controllata. Il codice Java seguente rappresenta il file costante.

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## Aggiunta di endpoint e-mail {#adding-email-endpoints}

Puoi aggiungere in modo programmatico un endpoint e-mail a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint e-mail, gli utenti potranno inviare un messaggio e-mail con uno o più file allegati a un account e-mail specifico. Viene quindi richiamata l&#39;operazione di configurazione del servizio e vengono modificati i file. Dopo aver eseguito l&#39;operazione specificata, il servizio invia al mittente un messaggio di posta elettronica contenente i file modificati come allegati.

Ai fini dell’aggiunta programmatica di un endpoint e-mail a un servizio, considera il seguente processo di breve durata denominato *MyApplication\EncryptDocument*. Per informazioni sui processi di breve durata, consulta [Informazioni sui processi di AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Questa procedura accetta un documento PDF PDF non protetto come valore di input e quindi lo trasmette al servizio di crittografia `EncryptPDFUsingPassword` operazione. Questo processo crittografa il documento PDF con una password e restituisce il documento PDF crittografato con password come valore di output. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF crittografato con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint e-mail utilizzando i servizi web.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per aggiungere un endpoint e-mail a un servizio, esegui le seguenti attività:

1. Includi file di progetto.
1. Creare un `EndpointRegistryClient` oggetto.
1. Imposta gli attributi dell’endpoint e-mail.
1. Specifica i valori di configurazione.
1. Definite i valori dei parametri di input.
1. Definite un valore per il parametro di output.
1. Crea l’endpoint e-mail.
1. Abilita l’endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Prima di poter aggiungere un endpoint e-mail a livello di programmazione, è necessario creare un `EndpointRegistryClient` oggetto.

**Impostare gli attributi dell’endpoint e-mail**

Per creare un endpoint e-mail per un servizio, specifica i seguenti valori:

* **Valore dell’identificatore del connettore**: specifica il tipo di endpoint creato. Per creare un endpoint e-mail, specifica `Email`.
* **Descrizione**: specifica una descrizione per l&#39;endpoint.
* **Nome**: specifica il nome dell&#39;endpoint.
* **Valore dell’identificatore del servizio**: specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint e-mail al processo introdotto in questa sezione (un processo diventa un servizio quando viene attivato utilizzando Workbench), specifica `EncryptDocument`.
* **Nome operazione**: specifica il nome dell&#39;operazione richiamata tramite l&#39;endpoint. In genere, durante la creazione di un endpoint e-mail per un servizio che ha avuto origine da un processo creato in Workbench, il nome dell’operazione è `invoke`.

**Specificare i valori di configurazione**

È necessario specificare i valori di configurazione per un endpoint e-mail quando si aggiunge programmaticamente un endpoint e-mail a un servizio. Questi valori di configurazione vengono specificati da un amministratore se viene aggiunto un endpoint e-mail utilizzando la console di amministrazione.

>[!NOTE]
>
>L’account e-mail monitorato è un account speciale utilizzato solo per l’endpoint e-mail. Questo account non è un account e-mail di un utente normale. L’account e-mail di un utente normale non deve essere configurato come account utilizzato dal provider e-mail, in quanto quest’ultimo elimina i messaggi dalla casella in entrata una volta completati.

I seguenti valori di configurazione vengono impostati quando si aggiunge a livello di programmazione un endpoint e-mail a un servizio:

* **cronExpression**: espressione cron se l’e-mail deve essere pianificata utilizzando un’espressione cron.
* **repeatCount**: numero di volte in cui l’endpoint e-mail esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.
* **repeatInterval**: velocità di scansione in secondi utilizzata dal ricevitore per il controllo della posta in arrivo. Il valore predefinito è 10.
* **startDelay**: tempo di attesa per la scansione dopo l’avvio della pianificazione. L&#39;ora predefinita è 0.
* **batchSize**: numero di messaggi e-mail elaborati dal destinatario per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.
* **userName**: nome utente utilizzato per richiamare un servizio target da e-mail. Il valore predefinito è `SuperAdmin`.
* **domainName**: valore di configurazione obbligatorio. Il valore predefinito è `DefaultDom`.
* **domainPattern**: specifica i pattern di dominio dei messaggi e-mail in arrivo accettati dal provider. Ad esempio, se `adobe.com` viene utilizzato, vengono elaborate solo le e-mail da adobe.com, le e-mail da altri domini vengono ignorate.
* **filePattern**: specifica i modelli di file allegati in ingresso accettati dal provider. Ciò include i file con estensioni di file specifiche (&amp;ast;.dat, &amp;ast;.xml), i file con nomi specifici (dati) e i file con espressioni composite nel nome e nell&#39;estensione (&amp;ast;.[dD][aA]&#39;porta&#39;). Il valore predefinito è `*`.
* **recipientSuccessfulJob**: indirizzo e-mail a cui vengono inviati i messaggi per indicare i processi riusciti. Per impostazione predefinita, un messaggio di processo riuscito viene sempre inviato al mittente. Se si digita `sender`, i risultati delle e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica destinatari aggiuntivi con indirizzi e-mail, ciascuno separato da una virgola. Per disattivare questa opzione, lasciare vuoto questo valore. In alcuni casi, potrebbe essere utile attivare un processo e non inviare una notifica e-mail del risultato. Il valore predefinito è `sender`.
* **recipientFailedJob**: indirizzo e-mail a cui vengono inviati i messaggi per indicare i processi non riusciti. Per impostazione predefinita, un messaggio di processo non riuscito viene sempre inviato al mittente. Se si digita `sender`, i risultati delle e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica destinatari aggiuntivi con indirizzi e-mail, ciascuno separato da una virgola. Per disattivare questa opzione, lasciare vuoto questo valore. Il valore predefinito è `sender`.
* **inboxHost**: nome host della casella in entrata o indirizzo IP da sottoporre a scansione per il provider e-mail.
* **inboxPort**: porta utilizzata dal server e-mail. Il valore predefinito per POP3 è 110 e quello per IMAP è 143. Se SSL è abilitato, il valore predefinito per POP3 è 995 e quello per IMAP è 993.
* **inboxProtocol**: protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della casella in entrata. Le opzioni sono `IMAP` o `POP3`. Il server di posta host della casella in entrata deve supportare questi protocolli.
* **inboxTimeOut**: timeout in secondi per l’attesa delle risposte della casella in entrata da parte del provider e-mail. Il valore predefinito è 60.
* **inboxUser**: nome utente necessario per accedere all’account e-mail. A seconda del server e della configurazione di e-mail, questa potrebbe essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.
* **inboxPassword**: password per l’utente della casella in entrata.
* **inboxSSLEnabled**: imposta questo valore per forzare il provider di posta elettronica a utilizzare SSL quando invii messaggi di notifica di risultati o errori. Verificare che l&#39;host IMAP o POP3 supporti SSL.
* **smtpHost**: nome host del server di posta a cui il provider di posta elettronica invia risultati e messaggi di errore.
* **smtpPort**: il valore predefinito per la porta SMTP è 25.
* **smtpUser**: account utente che il provider di posta elettronica utilizzerà per inviare notifiche e-mail relative a risultati ed errori.
* **smtpPassword**: password per l’account SMTP. Alcuni server di posta non richiedono una password SMTP.
* **charSet**: set di caratteri utilizzato dal provider e-mail. Il valore predefinito è `UTF-8`.
* **smtpSSLEnabled**: imposta questo valore per forzare il provider di posta elettronica a utilizzare SSL quando invii messaggi di notifica di risultati o errori. Verificare che l&#39;host SMTP supporti SSL.
* **failedJobFolder**: specifica una directory in cui memorizzare i risultati quando il server di posta SMTP non è operativo.
* **asincrono**: quando è impostato su synchronous, tutti i documenti di input vengono elaborati e viene restituita una singola risposta. Quando è impostato su asincrono, viene inviata una risposta per ciascun documento di input elaborato. Ad esempio, viene creato un endpoint e-mail per il processo introdotto in questo argomento e viene inviato un messaggio e-mail alla casella in entrata dell’endpoint contenente più documenti di PDF non protetti. Quando tutti i documenti PDF sono crittografati con una password e se l’endpoint è configurato come sincrono, viene inviato un unico messaggio e-mail di risposta con tutti i documenti PDF protetti allegati. Se l’endpoint è configurato come asincrono, viene inviato un messaggio e-mail di risposta separato per ogni documento di PDF protetto. Ogni messaggio e-mail contiene come allegato un singolo documento PDF. Il valore predefinito è asincrono.

**Definire i valori dei parametri di input**

Quando crei un endpoint e-mail, devi definire i valori dei parametri di input. In altre parole, devi descrivere i valori di input passati all’operazione richiamata dall’endpoint e-mail. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di input denominato `InDoc` e il suo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint e-mail per questo processo (dopo l’attivazione, un processo diventa un servizio), devi definire il valore del parametro di input.

Per definire i valori dei parametri di input necessari per un endpoint e-mail, specifica i seguenti valori:

**Nome parametro di input**: nome del parametro di input. Il nome di un valore di input viene specificato in Workbench per un processo. Se il valore di input appartiene a un&#39;operazione di servizio (un servizio di Forms che non è un processo creato in Workbench), il nome di input viene specificato nel file component.xml. Ad esempio, il nome del parametro di input per il processo introdotto in questa sezione è `InDoc`.

**Tipo di mappatura**: utilizzato per configurare i valori di input necessari per richiamare l’operazione di servizio. Di seguito sono riportati due tipi di mapping:

* `Literal`: l’endpoint E-mail utilizza il valore immesso nel campo così come viene visualizzato. Sono supportati tutti i tipi Java di base. Ad esempio, se un’API utilizza input come String, long, int e Boolean, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.
* `Variable`: il valore immesso è un modello di file utilizzato dall’endpoint e-mail per scegliere l’input. Se ad esempio si seleziona Variabile per il tipo di mapping e il documento di input deve essere un file PDF, è possibile specificare `*.pdf` come valore di mappatura.

**Valore di mappatura**: specifica il valore del tipo di mappatura. Ad esempio, se selezioni un tipo di mappatura Variabile, puoi specificare `*.pdf` come pattern del file.

**Tipo di dati**: specifica il tipo di dati dei valori di input. Ad esempio, il tipo di dati del valore di input del processo introdotto in questa sezione è com.adobe.idp.Document.

**Definisci un valore per il parametro di output**

Quando crei un endpoint e-mail, devi definire un valore di parametro di output. In altre parole, devi descrivere il valore di output restituito dal servizio richiamato dall’endpoint e-mail. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di output denominato `SecuredDoc` e il suo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint e-mail per questo processo (dopo l’attivazione, un processo diventa un servizio), devi definire il valore del parametro di output.

Per definire il valore di un parametro di output necessario per un endpoint e-mail, specifica i seguenti valori:

**Nome parametro di output**: nome del parametro di output. Il nome di un valore di output del processo è specificato in Workbench. Se il valore di output appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di output viene specificato nel file component.xml. Ad esempio, il nome del parametro di output per il processo introdotto in questa sezione è `SecuredDoc`.

**Tipo di mappatura**: utilizzato per configurare l’output del servizio e dell’operazione. Sono disponibili le seguenti opzioni:

* Se il servizio restituisce un singolo oggetto (un singolo documento), il modello è `%F.pdf` e la destinazione di origine è sourcefilename.pdf. Ad esempio, il processo introdotto in questa sezione restituisce un singolo documento. Di conseguenza, il tipo di mappatura può essere definito come `%F.pdf` ( `%F` significa utilizzare il nome file specificato). Il pattern `%E` specifica l&#39;estensione del documento di input.
* Se il servizio restituisce un elenco, il modello è `Result\%F\`e la destinazione di origine è Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se il servizio restituisce una mappa, il modello è `Result\%F\`e la destinazione di origine è Result\sourcefilename\file1 e Result\sourcefilename\file2. Se la mappa contiene più oggetti, il modello è `Result\%F.pdf` e la destinazione di origine è Result\sourcefilename1.pdf (output 1), Result\sourcefilenam2.pdf (output 2) e così via.

**Tipo di dati**: specifica il tipo di dati del valore restituito. Ad esempio, il tipo di dati del valore restituito del processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Creare l’endpoint e-mail**

Dopo aver impostato gli attributi e i valori di configurazione dell’endpoint e-mail e aver definito i valori dei parametri di input e di output, è necessario creare l’endpoint e-mail.

**Abilita l’endpoint**

Dopo aver creato un endpoint e-mail, devi abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo all’interno della console di amministrazione.

**Consulta anche**

[Aggiungere un endpoint e-mail utilizzando l’API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere un endpoint e-mail utilizzando l’API Java {#add-an-email-endpoint-using-the-java-api}

Aggiungi un endpoint e-mail utilizzando l’API Java:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Imposta gli attributi dell’endpoint e-mail.

   * Creare un `CreateEndpointInfo` mediante il costruttore.
   * Specifica il valore dell’identificatore del connettore richiamando `CreateEndpointInfo` dell&#39;oggetto `setConnectorId` e passando il valore stringa `Email`.
   * Specifica la descrizione dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setDescription` e fornendo un valore stringa che descrive l’endpoint.
   * Specifica il nome dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome.
   * Specifica il servizio a cui appartiene l’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setServiceId` e passando un valore stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando `CreateEndpointInfo` dell&#39;oggetto `setOperationName` e passando un valore stringa che specifica il nome dell&#39;operazione. In genere, durante la creazione di un endpoint e-mail per un servizio che ha avuto origine da un processo creato in Workbench, viene richiamato il nome dell’operazione.

1. Specifica i valori di configurazione.

   Per ogni valore di configurazione da impostare per l’endpoint e-mail, è necessario richiamare `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` metodo. Ad esempio, per impostare `smtpHost` valore di configurazione, richiama il `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome del valore di configurazione. Quando si imposta `smtpHost` valore di configurazione, specifica `smtpHost`.
   * Valore stringa che specifica il valore della configurazione. Quando si imposta `smtpHost` valore di configurazione, specifica un valore stringa che specifichi il nome del server SMTP.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori di configurazione impostati per il servizio EncryptDocument introdotti in questa sezione, vedere l&#39;esempio di codice Java disponibile in [QuickStart: aggiunta di un endpoint e-mail tramite API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Definite i valori dei parametri di input.

   Definisci un valore per il parametro di input richiamando `CreateEndpointInfo` dell&#39;oggetto `setInputParameterMapping` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome del parametro di input. Ad esempio, il nome del parametro di input per il servizio EncryptDocument è `InDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di input. Ad esempio, il tipo di dati della proprietà `InDoc` il parametro di input è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mappatura. Ad esempio, puoi specificare `variable`.
   * Valore stringa che specifica il valore del tipo di mapping. Ad esempio, è possibile specificare &amp;ast;.pdf come modello di file.

   >[!NOTE]
   >
   >Richiama `setInputParameterMapping` metodo per ciascun valore del parametro di input da definire. Poiché il processo EncryptDocument dispone di un solo parametro di input, è necessario richiamare questo metodo una volta.

1. Definite un valore per il parametro di output.

   Definisci un valore per il parametro di output richiamando `CreateEndpointInfo` dell&#39;oggetto `setOutputParameterMapping` e fornendo i seguenti valori:

   * Valore stringa che specifica il nome del parametro di output. Ad esempio, il nome del parametro di output per il servizio EncryptDocument è `SecuredDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di output. Ad esempio, il tipo di dati della proprietà `SecuredDoc` il parametro di output è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mappatura. Ad esempio, puoi specificare `%F.pdf`.

1. Crea l’endpoint e-mail.

   Creare l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando il `CreateEndpointInfo` oggetto. Questo metodo restituisce un `Endpoint` oggetto che rappresenta l’endpoint E-mail.

1. Abilita l’endpoint.

   Abilita l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `enable` e passando il `Endpoint` oggetto restituito da `createEndpoint` metodo.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: aggiunta di un endpoint per cartelle controllate utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### File costante valori configurazione e-mail {#email-configuration-values-constant-file}

Il [QuickStart: aggiunta di un endpoint e-mail tramite API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) utilizza un file costante che deve far parte del progetto Java per compilare l’avvio rapido. Questo file costante rappresenta i valori di configurazione che devono essere impostati quando si aggiunge un endpoint e-mail. Il codice Java seguente rappresenta il file costante.

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## Aggiunta di endpoint remoti {#adding-remoting-endpoints}

>[!NOTE]
>
>API di LiveCycle Remoting obsolete per i moduli AEM su JEE.

Puoi aggiungere in modo programmatico un endpoint remoto a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint remoto, si consente a un&#39;applicazione Flex di richiamare il servizio utilizzando la comunicazione remota. (vedere [Richiamare AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Ai fini dell&#39;aggiunta programmatica di un endpoint remoto a un servizio, considerare il seguente processo di breve durata denominato *Crittografia documento*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Questa procedura accetta un documento PDF PDF non protetto come valore di input e quindi lo trasmette al servizio di crittografia `EncryptPDFUsingPassword` operazione. Il documento PDF viene crittografato con una password e il documento PDF crittografato con password è il valore di output di questo processo. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF crittografato con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

Per illustrare come aggiungere un endpoint remoto a un servizio, questa sezione aggiunge un endpoint remoto a un servizio denominato EncryptDocument.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint remoto utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-4}

Per rimuovere un endpoint da un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un `EndpointRegistryClient` oggetto.
1. Impostare gli attributi dell&#39;endpoint remoto.
1. Crea un endpoint remoto.
1. Abilita l’endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Per aggiungere un endpoint remoto a livello di programmazione, è necessario creare un `EndpointRegistryClient` oggetto.

**Imposta attributi endpoint remoti**

Per creare un endpoint remoto per un servizio, specificare i valori seguenti:

* **Valore dell’identificatore del connettore**: specifica il tipo di endpoint creato. Per creare un endpoint remoto, specificare `Remoting`.
* **Descrizione**: specifica la descrizione dell&#39;endpoint.
* **Nome**: specifica il nome dell&#39;endpoint.
* **Valore dell’identificatore del servizio**: specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint remoto al processo introdotto in questa sezione (un processo diventa un servizio quando viene attivato in Workbench), specifica `EncryptDocument`.
* **Nome operazione**: specifica il nome dell&#39;operazione richiamata tramite l&#39;endpoint. Durante la creazione di un endpoint remoto, specificare un carattere jolly (&amp;ast;).

**Creare un endpoint remoto**

Dopo aver impostato gli attributi dell&#39;endpoint remoto, è possibile creare un endpoint remoto per un servizio.

**Abilita l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando un endpoint remoto è abilitato, consente a un client Flex di richiamare il servizio.

**Consulta anche**

[Aggiungere un endpoint remoto tramite API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere un endpoint remoto tramite API Java {#add-a-remoting-endpoint-using-the-java-api}

Aggiungi un endpoint remoto utilizzando l’API Java:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Impostare gli attributi dell&#39;endpoint remoto.

   * Creare un `CreateEndpointInfo` mediante il costruttore.
   * Specifica il valore dell’identificatore del connettore richiamando `CreateEndpointInfo` dell&#39;oggetto `setConnectorId` e passando il valore stringa `Remoting`.
   * Specifica la descrizione dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setDescription` e fornendo un valore stringa che descrive l’endpoint.
   * Specifica il nome dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome.
   * Specifica il servizio a cui appartiene l’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setServiceId` e passando un valore stringa che specifica il nome del servizio.
   * Specifica l’operazione richiamata da `CreateEndpointInfo` dell&#39;oggetto `setOperationName` e passando un valore stringa che specifica il nome dell&#39;operazione. Per un endpoint remoto, specifica un carattere jolly (&amp;ast;).

1. Crea un endpoint remoto.

   Creare l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando il `CreateEndpointInfo` oggetto. Questo metodo restituisce un `Endpoint` oggetto che rappresenta il nuovo endpoint remoto.

1. Abilita l’endpoint.

   Abilita l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `enable` e passando il `Endpoint` oggetto restituito da `createEndpoint` metodo.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: aggiunta di un endpoint remoto tramite API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint TaskManager {#adding-taskmanager-endpoints}

Puoi aggiungere a livello di programmazione un endpoint TaskManager a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint TaskManager a un servizio, si consente a un utente di Workspace di richiamare il servizio. In altre parole, un utente che lavora in Workspace può richiamare un processo che ha un endpoint TaskManager corrispondente.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint TaskManager utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-5}

Per aggiungere un endpoint TaskManager a un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un `EndpointRegistryClient` oggetto.
1. Crea una categoria per l’endpoint.
1. Impostare gli attributi dell&#39;endpoint TaskManager.
1. Creare un endpoint TaskManager.
1. Abilita l’endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Prima di poter aggiungere un endpoint TaskManager a livello di programmazione, è necessario creare un `EndpointRegistryClient` oggetto.

**Creare una categoria per l’endpoint**

Le categorie vengono utilizzate per organizzare i servizi all’interno di Workspace. In altre parole, un utente di Workspace può richiamare un servizio che ha un endpoint TaskManager selezionando una categoria all’interno di Workspace. Durante la creazione di un endpoint TaskManager, è possibile fare riferimento a una categoria esistente o crearne una nuova a livello di programmazione.

>[!NOTE]
>
>In questa sezione viene creata una nuova categoria come parte dell&#39;aggiunta di un endpoint TaskManager a un servizio.

**Impostare gli attributi dell&#39;endpoint TaskManager**

Per creare un endpoint TaskManager per un servizio, specificare i valori seguenti:

* **Identificatore del connettore**: specifica il tipo di endpoint creato. Per creare un endpoint TaskManager, specificare `TaskManagerConnector`.
* **Descrizione**: specifica la descrizione dell&#39;endpoint.
* **Nome**: specifica il nome dell&#39;endpoint.
* **Identificatore del servizio**: specifica il servizio a cui appartiene l&#39;endpoint.
* **Categoria**: specifica un valore dell&#39;identificatore di categoria associato all&#39;endpoint TaskManager.
* **Nome operazione**: in genere, durante la creazione di un endpoint TaskManager per un servizio che ha avuto origine da un processo creato in Workbench, il nome dell’operazione è `invoke`.

**Creare un endpoint TaskManager**

Dopo aver impostato gli attributi di un endpoint TaskManager, è possibile creare un endpoint TaskManager per un servizio.

**Abilita l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio dall’interno di Workspace. Dopo aver abilitato l’endpoint, puoi visualizzarlo all’interno della console di amministrazione.

**Consulta anche**

[Aggiungere un endpoint TaskManager utilizzando l’API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere un endpoint TaskManager utilizzando l’API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Aggiungi un endpoint TaskManager utilizzando l’API Java:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Crea una categoria per l’endpoint.

   * Creare un `CreateEndpointCategoryInfo` mediante il costruttore e passando i seguenti valori:

      * Valore stringa che specifica il valore identificatore della categoria
      * Valore stringa che specifica la descrizione della categoria

   * Crea la categoria richiamando il `EndpointRegistryClient` dell&#39;oggetto `createEndpointCategory` e passando il `CreateEndpointCategoryInfo` oggetto. Questo metodo restituisce un `EndpointCategory` oggetto che rappresenta la nuova categoria.

1. Impostare gli attributi dell&#39;endpoint TaskManager.

   * Creare un `CreateEndpointInfo` mediante il costruttore.
   * Specifica il valore dell’identificatore del connettore richiamando `CreateEndpointInfo` dell&#39;oggetto `setConnectorId` e passando il valore stringa `TaskManagerConnector`.
   * Specifica la descrizione dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setDescription` e fornendo un valore stringa che descrive l’endpoint.
   * Specifica il nome dell’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome.
   * Specifica il servizio a cui appartiene l’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setServiceId` e passando un valore stringa che specifica il nome del servizio.
   * Specifica la categoria a cui appartiene l’endpoint richiamando `CreateEndpointInfo` dell&#39;oggetto `setCategoryId` e passando un valore stringa che specifica il valore dell&#39;identificatore di categoria. È possibile richiamare `EndpointCategory` dell&#39;oggetto `getId` per ottenere il valore dell&#39;identificatore di questa categoria.
   * Specificare l&#39;operazione richiamata richiamando `CreateEndpointInfo` dell&#39;oggetto `setOperationName` e passando un valore stringa che specifica il nome dell&#39;operazione. In genere, durante la creazione di un’ `TaskManager` endpoint per un servizio che ha avuto origine da un processo creato in Workbench, il nome dell’operazione è `invoke`.

1. Creare un endpoint TaskManager.

   Creare l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando il `CreateEndpointInfo` oggetto. Questo metodo restituisce un `Endpoint` oggetto che rappresenta il nuovo endpoint TaskManager.

1. Abilita l’endpoint.

   Abilita l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `enable` e passando il `Endpoint` oggetto restituito da `createEndpoint` metodo.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: aggiunta di un endpoint TaskManager utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modifica degli endpoint {#modifying-endpoints}

Puoi modificare programmaticamente un endpoint esistente utilizzando l’API Java di AEM Forms. Modificando un endpoint, è possibile modificarne il comportamento. Si consideri, ad esempio, un endpoint di cartella controllata che specifica una cartella utilizzata come cartella controllata. Puoi modificare in modo programmatico i valori di configurazione che appartengono all’endpoint &quot;cartella controllata&quot;, affinché un’altra cartella funzioni come cartella controllata. Per informazioni sui valori di configurazione che appartengono a un endpoint di cartella controllata, consulta [Aggiunta di endpoint per cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints).

Per dimostrare come modificare un endpoint, questa sezione modifica un endpoint di cartella controllata cambiando la cartella che si comporta come la cartella controllata.

>[!NOTE]
>
>Non è possibile modificare un endpoint utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-6}

Per modificare un endpoint, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un `EndpointRegistryClient` oggetto.
1. Recupera il punto finale.
1. Specificare nuovi valori di configurazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Per modificare un endpoint a livello di programmazione, è necessario creare un `EndpointRegistryClient` oggetto.

**Recupera il punto finale da modificare**

Prima di poter modificare un endpoint, è necessario recuperarlo. Per recuperare un endpoint, è necessario connettersi come utente che può accedere a un endpoint. È consigliabile connettersi come amministratore. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Per recuperare un endpoint, recuperate un elenco di endpoint. È quindi possibile eseguire un&#39;iterazione nell&#39;elenco, cercando l&#39;endpoint specifico da rimuovere. Ad esempio, è possibile individuare un endpoint determinando il servizio corrispondente all&#39;endpoint e il tipo di endpoint. Quando individuate il punto finale, potete modificarlo.

**Specificare nuovi valori di configurazione**

Quando modifichi un endpoint, specifica i nuovi valori di configurazione. Ad esempio, per modificare un endpoint di cartella controllata, reimposta tutti i valori di configurazione dell’endpoint di cartella controllata, non solo quelli che desideri modificare. Per informazioni sui valori di configurazione che appartengono a un endpoint di cartella controllata, consulta [Aggiunta di endpoint per cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Per informazioni sui valori di configurazione che appartengono a un endpoint e-mail, consulta [Aggiunta di endpoint e-mail](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Impossibile modificare il servizio richiamato dall&#39;endpoint. Se tenti di modificare il servizio, viene generata un’eccezione. Per modificare il servizio associato a un determinato endpoint, rimuovi l’endpoint e creane uno nuovo. (vedere [Rimozione degli endpoint](programmatically-endpoints.md#removing-endpoints).)

**Consulta anche**

[Modifica di un endpoint tramite API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modifica di un endpoint tramite API Java {#modifying-an-endpoint-using-the-java-api}

Modifica un endpoint utilizzando l’API Java:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperate il punto finale da modificare.

   * Recuperare un elenco di tutti gli endpoint a cui l&#39;utente corrente (specificati nelle proprietà della connessione) può accedere richiamando il `EndpointRegistryClient` dell&#39;oggetto `getEndpoints` e il passaggio di un `PagingFilter` oggetto che funge da filtro. È possibile passare un `(PagingFilter)null` per restituire tutti gli endpoint. Questo metodo restituisce un `java.util.List` oggetto in cui ogni elemento è un `Endpoint` oggetto. Per informazioni su `PagingFilter` oggetto, vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Effettua iterazione attraverso `java.util.List` per determinare se dispone di endpoint. Se esistono endpoint, ogni elemento è un `EndPoint` dell&#39;istanza.
   * Determinare il servizio corrispondente a un endpoint richiamando `EndPoint` dell&#39;oggetto `getServiceId` metodo. Questo metodo restituisce un valore stringa che specifica il nome del servizio.
   * Determinare il tipo di endpoint richiamando `EndPoint` dell&#39;oggetto `getConnectorId` metodo. Questo metodo restituisce un valore stringa che specifica il tipo di endpoint. Ad esempio, se l’endpoint è un endpoint di tipo Cartella controllata, questo metodo restituisce `WatchedFolder`.

1. Specificare nuovi valori di configurazione.

   * Creare un `ModifyEndpointInfo` richiamando il relativo costruttore.
   * Per ogni valore di configurazione da impostare, richiama `ModifyEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` metodo. Ad esempio, per impostare il valore di configurazione dell’URL, richiama `ModifyEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e trasmettere i seguenti valori:

      * Valore stringa che specifica il nome del valore di configurazione. Ad esempio, per impostare `url` valore di configurazione, specifica `url`.
      * Valore stringa che specifica il valore della configurazione. Per definire un valore per `url` valore di configurazione, specifica il percorso della cartella controllata.

   * Richiama `EndpointRegistryClient` dell&#39;oggetto `modifyEndpoint` e trasmettere il `ModifyEndpointInfo` oggetto.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: modifica di un endpoint tramite API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rimozione degli endpoint {#removing-endpoints}

Puoi rimuovere in modo programmatico un endpoint da un servizio utilizzando l’API Java di AEM Forms. Dopo aver rimosso un endpoint, non è possibile richiamare il servizio utilizzando il metodo di chiamata abilitato per l&#39;endpoint. Ad esempio, se si rimuove un endpoint SOAP da un servizio, non è possibile richiamare il servizio utilizzando la modalità SOAP.

Per dimostrare come rimuovere un endpoint da un servizio, in questa sezione viene rimosso un endpoint EJB da un servizio denominato *Crittografia documento*.

>[!NOTE]
>
>Non è possibile rimuovere un endpoint utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-7}

Per rimuovere un endpoint da un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un `EndpointRegistryClient` oggetto.
1. Recupera il punto finale.
1. Rimuovi l’endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client EndpointRegistry**

Per rimuovere un endpoint a livello di programmazione, è necessario creare un `EndpointRegistryClient` oggetto.

**Recupera l’endpoint da rimuovere**

Prima di rimuovere un endpoint, è necessario recuperarlo. Per recuperare un endpoint, è necessario connettersi come utente che può accedere a un endpoint. È consigliabile connettersi come amministratore. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Per recuperare un endpoint, recuperate un elenco di endpoint. È quindi possibile eseguire un&#39;iterazione nell&#39;elenco, cercando l&#39;endpoint specifico da rimuovere. Ad esempio, è possibile individuare un endpoint determinando il servizio corrispondente all&#39;endpoint e il tipo di endpoint. Quando individuate l&#39;endpoint, potete rimuoverlo.

**Rimuovi l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo all’interno della console di amministrazione.

**Consulta anche**

[Rimozione di un endpoint tramite API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimozione di un endpoint tramite API Java {#removing-an-endpoint-using-the-java-api}

Rimuovi un endpoint utilizzando l’API Java:

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client EndpointRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EndpointRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperate l&#39;endpoint da rimuovere.

   * Recuperare un elenco di tutti gli endpoint a cui l&#39;utente corrente (specificati nelle proprietà della connessione) ha accesso richiamando `EndpointRegistryClient` dell&#39;oggetto `getEndpoints` e il passaggio di un `PagingFilter` oggetto che funge da filtro. È possibile trasmettere `(PagingFilter)null` per restituire tutti gli endpoint. Questo metodo restituisce un `java.util.List` oggetto in cui ogni elemento è un `Endpoint` oggetto.
   * Effettua iterazione attraverso `java.util.List` per determinare se dispone di endpoint. Se esistono endpoint, ogni elemento è un `EndPoint` dell&#39;istanza.
   * Determinare il servizio corrispondente a un endpoint richiamando `EndPoint` dell&#39;oggetto `getServiceId` metodo. Questo metodo restituisce un valore stringa che specifica il nome del servizio.
   * Determinare il tipo di endpoint richiamando `EndPoint` dell&#39;oggetto `getConnectorId` metodo. Questo metodo restituisce un valore stringa che specifica il tipo di endpoint. Ad esempio, se l’endpoint è un endpoint EJB, questo metodo restituisce `EJB`.

1. Rimuovi l’endpoint.

   Rimuovi l’endpoint richiamando `EndpointRegistryClient` dell&#39;oggetto `remove` e passando il `EndPoint` oggetto che rappresenta l&#39;endpoint da rimuovere.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: rimozione di un endpoint tramite API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recupero informazioni sul connettore endpoint {#retrieving-endpoint-connector-information}

Puoi recuperare in modo programmatico informazioni sui connettori di endpoint utilizzando l’API di AEM Forms. Un connettore consente a un endpoint di richiamare un servizio utilizzando vari metodi di chiamata. Ad esempio, un connettore di cartella controllata consente a un endpoint di richiamare un servizio utilizzando le cartelle controllate. Recuperando a livello di programmazione le informazioni sui connettori endpoint, è possibile recuperare i valori di configurazione associati a un connettore, ad esempio i valori di configurazione richiesti e quelli facoltativi.

Per illustrare come recuperare informazioni sui connettori di endpoint, in questa sezione vengono recuperate informazioni su un connettore di cartella controllata. (vedere [Aggiunta di endpoint per cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Non è possibile recuperare informazioni sugli endpoint utilizzando i servizi Web.

>[!NOTE]
>
>In questo argomento viene utilizzato `ConnectorRegistryClient` API per recuperare informazioni sui connettori endpoint. (vedere [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Riepilogo dei passaggi {#summary_of_steps-8}

Per recuperare le informazioni sul connettore dell&#39;endpoint, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un `ConnectorRegistryClient` oggetto.
1. Specifica il tipo di connettore.
1. Recupera i valori di configurazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto client ConnectorRegistry**

Per recuperare in modo programmatico le informazioni sul connettore dell&#39;endpoint, creare un `ConnectorRegistryClient` oggetto.

**Specifica il tipo di connettore**

Specificare il tipo di connettore da cui recuperare le informazioni. Esistono i seguenti tipi di connettori:

* **EJB**: consente a un&#39;applicazione client di richiamare un servizio utilizzando la modalità EJB.
* **SOAP**: consente a un&#39;applicazione client di richiamare un servizio utilizzando la modalità SOAP.
* **Cartella controllata**: abilita le cartelle controllate per richiamare un servizio.
* **E-mail**: abilita i messaggi e-mail per richiamare un servizio.
* **Remoting**: consente a un&#39;applicazione client Flex di richiamare un servizio.
* **ConnettoreGestioneAttività**: consente a un utente di Workspace di richiamare un servizio dall’interno di Workspace.

**Recuperare i valori di configurazione**

Dopo aver specificato il tipo di connettore, è possibile recuperare informazioni sul connettore, ad esempio il valore di configurazione supportato. Ad esempio, per qualsiasi connettore, puoi determinare quali valori di configurazione sono richiesti e quali facoltativi.

**Consulta anche**

[Recuperare le informazioni sul connettore dell’endpoint utilizzando l’API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare le informazioni sul connettore dell’endpoint utilizzando l’API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recupera le informazioni sul connettore dell’endpoint utilizzando l’API Java:

1. Includi file di progetto. .

   Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client ConnectorRegistry.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `ConnectorRegistryClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Specifica il tipo di connettore.

   Specifica il tipo di connettore richiamando `ConnectorRegistryClient` dell&#39;oggetto `getEndpointDefinition` e passando un valore stringa che specifica il tipo di connettore. Ad esempio, per specificare il tipo di connettore della cartella controllata, passa il valore stringa `WatchedFolder`. Questo metodo restituisce un `Endpoint` oggetto che corrisponde al tipo di connettore.

1. Recupera i valori di configurazione.

   * Recupera i valori di configurazione associati all’interno di questo endpoint richiamando `Endpoint` dell&#39;oggetto `getConfigParameters` metodo. Questo metodo restituisce un array di `ConfigParameter` oggetti.
   * Recupera le informazioni su ciascun valore di configurazione recuperando ogni elemento all’interno dell’array. Ogni elemento è un `ConfigParameter` oggetto. Ad esempio, puoi determinare se il valore di configurazione è obbligatorio o facoltativo richiamando il `ConfigParameter` dell&#39;oggetto `isRequired` metodo. Se il valore di configurazione è obbligatorio, questo metodo restituisce `true`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[QuickStart: recupero delle informazioni sul connettore dell’endpoint tramite API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
