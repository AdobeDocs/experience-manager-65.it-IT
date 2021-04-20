---
title: Gestione programmatica degli endpoint
seo-title: Gestione programmatica degli endpoint
description: Utilizzare il servizio Registro di sistema degli endpoint per aggiungere endpoint EJB, aggiungere endpoint SOAP, aggiungere endpoint Watched Folder, aggiungere endpoint e-mail, aggiungere endpoint Remoting, aggiungere endpoint Task Manager, modificare endpoint, rimuovere endpoint e recuperare informazioni sul connettore degli endpoint.
seo-description: Utilizzare il servizio Registro di sistema degli endpoint per aggiungere endpoint EJB, aggiungere endpoint SOAP, aggiungere endpoint Watched Folder, aggiungere endpoint e-mail, aggiungere endpoint Remoting, aggiungere endpoint Task Manager, modificare endpoint, rimuovere endpoint e recuperare informazioni sul connettore degli endpoint.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '10864'
ht-degree: 1%

---


# Gestione programmatica degli endpoint {#programmatically-managing-endpoints}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Registro di sistema di Endpoint**

Il servizio Registro endpoint consente di gestire gli endpoint in modo programmatico. Ad esempio, puoi aggiungere a un servizio i seguenti tipi di endpoint:

* EJB
* SOAP
* Cartella osservata
* E-mail
* (Funzione obsoleta per i moduli AEM) Remoting
* Gestione attività

>[!NOTE]
>
>Gli endpoint di tipo remoto SOAP, EJB e (obsoleti per i moduli AEM su JEE) vengono creati automaticamente per ogni servizio attivato. Gli endpoint SOAP ed EJB abilitano SOAP ed EJB per tutte le operazioni del servizio.

Un endpoint remoto consente ai client Flex di richiamare le operazioni sul servizio AEM Forms a cui è stato aggiunto l’endpoint. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare le operazioni sul servizio pertinente.

Gli endpoint Email, Task Manager e Watched Folder mostrano solo un&#39;operazione specifica del servizio. Per aggiungere questi endpoint è necessario un secondo passaggio di configurazione per selezionare un metodo da richiamare, impostare i parametri di configurazione e specificare le mappature dei parametri di input e output.

È possibile organizzare gli endpoint di TaskManager in gruppi denominati *categories*. Queste categorie vengono quindi esposte a Workspace tramite TaskManager e gli utenti finali visualizzano gli endpoint di TaskManager durante la loro classificazione. In Workspace, gli utenti finali visualizzano queste categorie nel riquadro di navigazione. Gli endpoint all’interno di ciascuna categoria vengono visualizzati come schede di processo nella pagina Processi iniziali in Workspace.

È possibile eseguire queste operazioni utilizzando il servizio Registro di sistema Endpoint:

* Aggiungi gli endpoint EJB. (Vedere [Aggiunta di endpoint EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Aggiungi endpoint SOAP. (Vedere [Aggiunta di endpoint SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Aggiungi endpoint per cartelle controllate (consulta [Aggiunta di endpoint per cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints)).
* Aggiungi endpoint e-mail. (Consulta [Aggiunta di endpoint e-mail](programmatically-endpoints.md#adding-email-endpoints).)
* Aggiungi endpoint di tipo Remoting. (Vedere [Aggiunta di endpoint remoti](programmatically-endpoints.md#adding-remoting-endpoints).)
* Aggiungi endpoint TaskManager (vedere [Aggiunta di endpoint TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints)).
* Modificare gli endpoint (vedere [Modifica degli endpoint](programmatically-endpoints.md#modifying-endpoints).)
* Rimuovere gli endpoint (vedere [Rimozione di endpoint](programmatically-endpoints.md#removing-endpoints).)
* Recupera le informazioni sul connettore endpoint (consulta [Recupero informazioni sul connettore endpoint](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Aggiunta di endpoint EJB {#adding-ejb-endpoints}

Puoi aggiungere programmaticamente un endpoint EJB a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint EJB a un servizio, stai abilitando un&#39;applicazione client per richiamare il servizio utilizzando la modalità EJB. In altre parole, quando si impostano le proprietà di connessione necessarie per richiamare AEM Forms, è possibile selezionare la modalità EJB. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Non è possibile aggiungere un endpoint EJB utilizzando i servizi Web.

>[!NOTE]
>
>In genere, un endpoint EJB viene aggiunto a un servizio per impostazione predefinita, tuttavia, un endpoint EJB può essere aggiunto a un processo distribuito a livello di programmazione o quando un endpoint EJB è stato rimosso e deve essere aggiunto di nuovo.

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un endpoint EJB a un servizio, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistry Client`.
1. Impostare gli attributi dell’endpoint EJB.
1. Crea un endpoint EJB.
1. Attiva l&#39;endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Prima di poter aggiungere programmaticamente un endpoint EJB, è necessario creare un oggetto `EndpointRegistryClient` .

**Impostare gli attributi dell’endpoint EJB**

Per creare un endpoint EJB per un servizio, specifica i seguenti valori:

* **Identificatore** del connettore: Specifica il tipo di endpoint da creare. Per creare un endpoint EJB, specifica `EJB`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Identificatore** del servizio: Specifica il servizio a cui appartiene l&#39;endpoint.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. Quando crei un endpoint EJB, specifica un carattere jolly ( `*`). Tuttavia, se desideri specificare un’operazione specifica anziché richiamare tutte le operazioni del servizio, specifica il nome dell’operazione anziché il carattere jolly ( `*`).

**Creare un endpoint EJB**

Dopo aver impostato gli attributi dell&#39;endpoint EJB, puoi creare un endpoint EJB per un servizio.

**Abilitare l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Dopo aver abilitato l’endpoint, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiunta di un endpoint EJB tramite l’API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiunta di un endpoint EJB utilizzando l&#39;API Java {#adding-an-ejb-endpoint-using-the-java-api}

Aggiungi un endpoint EJB utilizzando l&#39;API Java:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java. (

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare gli attributi dell’endpoint EJB.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specifica il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `EJB`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `setName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifichi il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che specifichi il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passare un valore stringa che specifica il nome dell&#39;operazione. Per gli endpoint SOAP e EJB, specifica un carattere jolly ( `*`) che implica tutte le operazioni.

1. Crea un endpoint EJB.

   Creare il punto finale richiamando il metodo `createEndpoint` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint EJB.

1. Attiva l&#39;endpoint.

   Abilita l’endpoint richiamando il metodo enable dell’oggetto `EndpointRegistryClient` e passando l’oggetto `Endpoint` restituito dal metodo `createEndpoint` .

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Aggiunta di un endpoint EJB tramite l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint SOAP {#adding-soap-endpoints}

Puoi aggiungere programmaticamente un endpoint SOAP a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint SOAP, si abilita un&#39;applicazione client per richiamare il servizio utilizzando la modalità SOAP. In altre parole, quando si impostano le proprietà di connessione necessarie per richiamare AEM Forms, è possibile selezionare la modalità SOAP.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint SOAP utilizzando i servizi Web.

>[!NOTE]
>
>In genere, un endpoint SOAP viene aggiunto a un servizio per impostazione predefinita, tuttavia, un endpoint SOAP può essere aggiunto a un processo distribuito a livello di programmazione o quando un endpoint SOAP è stato rimosso e deve essere aggiunto di nuovo.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per aggiungere un endpoint SOAP a un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Impostare gli attributi dell’endpoint SOAP.
1. Creare un endpoint SOAP.
1. Attiva l&#39;endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Questi file JAR sono necessari per creare un endpoint SOAP. Tuttavia, è necessario aggiungere file JAR se si utilizza l’endpoint SOAP per richiamare il servizio. Per informazioni sui file JAR di AEM Forms, consulta [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per aggiungere programmaticamente un endpoint SOAP a un servizio, è necessario creare un oggetto `EndpointRegistryClient` .

**Impostare gli attributi dell’endpoint SOAP**

Per aggiungere un endpoint SOAP a un servizio, specificare i seguenti valori:

* **Valore** dell&#39;identificatore del connettore: Specifica il tipo di endpoint da creare. Per creare un endpoint SOAP, specificare `SOAP`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Valore** dell&#39;identificatore del servizio: Specifica il servizio a cui appartiene l&#39;endpoint.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. Durante la creazione di un endpoint SOAP, specificare un carattere jolly ( `*`). Tuttavia, se desideri specificare un’operazione specifica anziché richiamare tutte le operazioni del servizio, specifica il nome dell’operazione anziché il carattere jolly ( `*`).

**Creare un endpoint SOAP**

Dopo aver impostato gli attributi dell’endpoint SOAP, è possibile creare un endpoint SOAP.

**Abilitare l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiungere un endpoint SOAP utilizzando l’API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungi un endpoint SOAP utilizzando l&#39;API Java {#add-a-soap-endpoint-using-the-java-api}

Aggiungi un endpoint SOAP a un servizio utilizzando l&#39;API Java:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare gli attributi dell’endpoint SOAP.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specifica il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `SOAP`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `setName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifichi il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che specifichi il nome del servizio.
   * Specificare l&#39;operazione che viene richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. Per gli endpoint SOAP e EJB, specifica un carattere jolly ( `*`) che implica tutte le operazioni.

1. Creare un endpoint SOAP.

   Creare il punto finale richiamando il metodo `createEndpoint` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint SOAP.

1. Attiva l&#39;endpoint.

   Abilita l’endpoint richiamando il metodo enable dell’oggetto `EndpointRegistryClient` e passando l’oggetto `Endpoint` restituito dal metodo `createEndpoint` .

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Aggiunta di un endpoint SOAP utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint cartelle controllate {#adding-watched-folder-endpoints}

Puoi aggiungere programmaticamente un endpoint Cartella osservata a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint per cartelle controllate, gli utenti possono inserire un file (ad esempio un file PDF) in una cartella. Quando il file viene inserito nella cartella, viene richiamato il servizio configurato e viene manipolato il file. Dopo aver eseguito l&#39;operazione specificata, il servizio salva il file modificato in una cartella di output specificata. Una cartella controllata è configurata per la scansione a un intervallo a tasso fisso o con un programma cron, ad esempio ogni lunedì, mercoledì e venerdì a mezzogiorno.

Ai fini dell&#39;aggiunta programmatica di un endpoint Cartella osservata a un servizio, considera il seguente processo di breve durata denominato *EncryptDocument*. (Consulta [Informazioni sui processi AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Questo processo accetta un documento PDF non protetto come valore di input e quindi trasmette il documento PDF non protetto all&#39;operazione `EncryptPDFUsingPassword` del servizio di cifratura. Il documento PDF è crittografato con una password e il documento PDF crittografato con password è il valore di output di questo processo. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF crittografato con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint per cartelle controllate utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-2}

Per aggiungere a un servizio un endpoint di tipo Cartella controllata, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Imposta gli attributi dell&#39;endpoint della cartella controllata.
1. Specifica i valori di configurazione.
1. Definisci i valori dei parametri di input.
1. Definire un valore del parametro di output.
1. Crea un endpoint per cartelle controllate.
1. Attiva l&#39;endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per aggiungere programmaticamente un endpoint Cartella osservata, è necessario creare un oggetto `EndpointRegistryClient` .

**Impostare gli attributi dell’endpoint della cartella controllata**

Per creare un endpoint per cartelle controllate per un servizio, specificare i seguenti valori:

* **Identificatore** del connettore: Specifica il tipo di endpoint creato. Per creare un endpoint per cartelle controllate, specificare `WatchedFolder`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Identificatore** del servizio: Specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint Cartella osservata al processo introdotto in questa sezione (un processo diventa un servizio quando viene attivato tramite Workbench), specificare `EncryptDocument`.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. In genere, durante la creazione di un endpoint per cartelle controllate per un servizio creato da un processo creato in Workbench, il nome dell’operazione è `invoke`.

**Specificare i valori di configurazione**

È necessario specificare i valori di configurazione per un endpoint di una cartella sottoposta a controllo quando si aggiunge in modo programmatico un endpoint di una cartella sottoposta a controllo a un servizio. Questi valori di configurazione vengono specificati da un amministratore se viene aggiunto un endpoint per cartelle controllate utilizzando la console di amministrazione.

L&#39;elenco seguente specifica i valori di configurazione impostati durante l&#39;aggiunta programmatica di un endpoint di tipo Cartella sottoposta a controllo a un servizio:

* **url**: Specifica il percorso della cartella controllata. In un ambiente cluster, questo valore deve puntare a una cartella di rete condivisa accessibile da ogni computer del cluster.
* **asincrono**: Identifica il tipo di chiamata come asincrono o sincrono. I processi transitori e sincroni possono essere richiamati solo in modo sincrono. Il valore predefinito è vero. È consigliato l’utilizzo asincrono.
* **cronExpression**: Utilizzato dal quarzo per pianificare il polling della directory di input. Per informazioni dettagliate sulla configurazione dell&#39;espressione cron, consulta [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html).
* **purgeDuration**: Questo è un attributo obbligatorio. I file e le cartelle nella cartella dei risultati vengono eliminati quando sono più vecchi di questo valore. Questo valore viene misurato in giorni. Questo attributo è utile per garantire che la cartella dei risultati non sia piena. Il valore -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
* **repeatInterval**: L&#39;intervallo, in secondi, per la scansione della cartella sottoposta a controllo per l&#39;input. A meno che non sia abilitata la limitazione, questo valore deve essere più lungo del tempo necessario per elaborare un lavoro medio; in caso contrario, il sistema potrebbe sovraccaricarsi. Il valore predefinito è 5.
* **repeatCount**: Il numero di volte in cui una cartella osservata esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.
* **throttleOn**: Limita il numero di processi delle cartelle controllate che possono essere elaborati in un dato momento. Il numero massimo di processi è determinato dal valore batchSize.
* **userName**: Nome utente utilizzato per richiamare un servizio di destinazione dalla cartella sottoposta a controllo. Questo valore è obbligatorio. Il valore predefinito è SuperAdmin.
* **domainName**: Dominio dell’utente. Questo valore è obbligatorio. Il valore predefinito è DefaultDom.
* **batchSize**: Numero di file o cartelle da raccogliere per scansione. Utilizzare questo valore per evitare un sovraccarico sul sistema; la scansione di troppi file alla volta può causare un arresto anomalo. Il valore predefinito è 2.
* **waitTime**: Tempo, in millisecondi, di attesa prima della scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 36.000.000 millisecondi (un&#39;ora) e il file è stato creato un minuto fa, questo file viene acquisito dopo che sono passati 59 o più minuti. Questo attributo è utile per garantire che un file o una cartella venga copiata completamente nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il file richiede dieci minuti per il download, impostare il tempo di attesa su 10&amp;ast;60 &amp;ast;1000 millisecondi. Questa impostazione impedisce alla cartella controllata di eseguire la scansione del file se non è in attesa da dieci minuti. Il valore predefinito è 0.
* **excludeFilePattern**: Il pattern utilizzato da una cartella controllata per determinare quali file e cartelle analizzare e raccogliere. Qualsiasi file o cartella con questo pattern non verrà analizzato per l’elaborazione. Questa impostazione è utile quando l’input è una cartella che contiene più file. Il contenuto della cartella può essere copiato in una cartella con un nome che verrà scelto dalla cartella controllata. Questo passaggio impedisce alla cartella controllata di raccogliere una cartella da elaborare prima che la cartella venga completamente copiata nella cartella di input. Ad esempio, se il valore excludeFilePattern è `data*`, non verranno prelevati tutti i file e le cartelle corrispondenti a `data*`. Sono inclusi file e cartelle denominati `data1`, `data2` e così via. Inoltre, il pattern può essere completato con pattern di caratteri jolly per specificare i pattern di file. La cartella controllata modifica l’espressione regolare per supportare i pattern dei caratteri jolly quali `*.*` e `*.pdf`. Questi pattern di caratteri jolly non sono supportati da espressioni regolari.
* **includeFilePattern**: Il pattern utilizzato dalla cartella controllata per determinare le cartelle e i file da analizzare e raccogliere. Ad esempio, se questo valore è `*`, vengono prelevati tutti i file e le cartelle corrispondenti a `input*`. Sono inclusi file e cartelle denominati `input1`, `input2` e così via. Il valore predefinito è `*`. Questo valore indica tutti i file e le cartelle. Inoltre, il pattern può essere completato con pattern di caratteri jolly per specificare i pattern di file. La cartella controllata modifica l’espressione regolare per supportare i pattern dei caratteri jolly quali `*.*` e `*.pdf`. Questi pattern di caratteri jolly non sono supportati da espressioni regolari. Questo valore è obbligatorio.
* **resultFolderName**: Cartella in cui vengono archiviati i risultati salvati. Questa posizione può essere un percorso di directory assoluto o relativo. Se i risultati non vengono visualizzati in questa cartella, controlla la cartella degli errori. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Il valore predefinito è `result/%Y/%M/%D/`. Questa è la cartella dei risultati all&#39;interno della cartella controllata.
* **preserveFolderName**: Il percorso in cui vengono archiviati i file dopo la scansione e il ritiro riusciti. Questa posizione può essere un percorso di directory assoluto, relativo o nullo. Il valore predefinito è `preserve/%Y/%M/%D/`.
* **nomeCartella** Non riuscito: Cartella in cui vengono salvati i file di errore. Questa posizione è sempre relativa alla cartella controllata. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Il valore predefinito è `failure/%Y/%M/%D/`.
* **preserveOnFailure**: Mantieni i file di input in caso di errore durante l&#39;esecuzione dell&#39;operazione su un servizio. Il valore predefinito è vero.
* **overwriteDuplicateFilename**: Se impostato su true, i file nella cartella dei risultati e nella cartella preserve vengono sovrascritti. Se impostato su false, il nome verrà utilizzato per i file e le cartelle con un suffisso di indice numerico. Il valore predefinito è false.

**Definire i valori dei parametri di input**

Quando crei un endpoint di una cartella controllata, devi definire i valori dei parametri di input. In altre parole, devi descrivere i valori di input passati all’operazione richiamata dalla cartella controllata. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di input denominato `InDoc` e il relativo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint di tipo Cartella controllata per questo processo (dopo l&#39;attivazione di un processo, questo diventa un servizio), devi definire il valore del parametro di input.

Per definire i valori dei parametri di input richiesti per un endpoint di una cartella sottoposta a controllo, specificare i seguenti valori:

**Nome** del parametro di input: Nome del parametro di input. Il nome di un valore di input viene specificato in Workbench per un processo. Se il valore di input appartiene a un’operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di input viene specificato nel file component.xml. Ad esempio, il nome del parametro di input per il processo introdotto in questa sezione è `InDoc`.

**Tipo** di mappatura: Utilizzato per configurare i valori di input necessari per richiamare l&#39;operazione del servizio. Esistono due tipi di mapping:

* `Literal`: L’endpoint Cartella controllata utilizza il valore immesso nel campo durante la visualizzazione. Sono supportati tutti i tipi Java di base. Ad esempio, se un’API utilizza input quali String, long, int e Boolean, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.
* `Variable`: Il valore immesso è un pattern di file utilizzato dalla cartella controllata per selezionare l’input. Ad esempio, se selezioni Variabile per il tipo di mappatura e il documento di input deve essere un file PDF, puoi specificare `*.pdf`come valore di mappatura.

**Valore** mappatura: Specifica il valore del tipo di mappatura. Ad esempio, se selezioni un tipo di mappatura `Variable`, puoi specificare `*.pdf` come pattern di file.

**Tipo** di dati: Specifica il tipo di dati dei valori immessi. Ad esempio, il tipo di dati del valore di input del processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Definire un valore del parametro di output**

Quando crei un endpoint di una cartella controllata, devi definire un valore di parametro di output. In altre parole, è necessario descrivere il valore di output restituito dal servizio richiamato dall&#39;endpoint Cartella controllata. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di output denominato `SecuredDoc` e il relativo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint di tipo Cartella controllata per questo processo (dopo l&#39;attivazione di un processo, questo diventa un servizio), devi definire il valore del parametro di output.

Per definire un valore del parametro di output richiesto per un endpoint di una cartella sottoposta a controllo, specificare i seguenti valori:

**Nome** del parametro di output: Nome del parametro di output. Il nome di un valore di output del processo è specificato in Workbench. Se il valore di output appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di output viene specificato nel file component.xml. Ad esempio, il nome del parametro di output per il processo introdotto in questa sezione è `SecuredDoc`.

**Tipo** di mappatura: Utilizzato per configurare l&#39;output del servizio e l&#39;operazione. Sono disponibili le seguenti opzioni:

* Se il servizio restituisce un singolo oggetto (un singolo documento), il pattern è `%F.pdf` e la destinazione di origine è sourcefilename.pdf. Ad esempio, il processo introdotto in questa sezione restituisce un singolo documento. Di conseguenza, il tipo di mappatura può essere definito come `%F.pdf` ( `%F` significa utilizzare il nome file specificato). Il pattern `%E` specifica l’estensione del documento di input.
* Se il servizio restituisce un elenco, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se il servizio restituisce una mappa, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\file1 and Result\sourcefilename\file2. Se la mappa ha più di un oggetto, il pattern è `Result\%F.pdf` e la destinazione di origine è Result\sourcefilename1.pdf (output 1), Result\sourcefilenam2.pdf (output 2) e così via.

**Tipo** di dati: Specifica il tipo di dati del valore restituito. Ad esempio, il tipo di dati del valore restituito del processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Creare un endpoint per cartelle controllate**

Dopo aver impostato gli attributi, i valori di configurazione e i valori dei parametri di input e output dell’endpoint, è necessario creare l’endpoint Cartella controllata.

**Abilitare l’endpoint**

Dopo aver creato un endpoint per cartelle controllate, è necessario abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiungi un endpoint per cartelle controllate utilizzando l’API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungi un endpoint per cartelle controllate utilizzando l&#39;API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Aggiungi un endpoint per cartelle controllate utilizzando l’API Java di AEM Forms:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Imposta gli attributi dell&#39;endpoint della cartella controllata.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specifica il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `WatchedFolder`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `setName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifichi il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che specifichi il nome del servizio.
   * Specificare l&#39;operazione che viene richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. In genere, durante la creazione di un endpoint Cartella di controllo per un servizio creato da un processo creato in Workbench, viene richiamato il nome dell&#39;operazione.

1. Specifica i valori di configurazione.

   Per ogni valore di configurazione da impostare per l’endpoint Cartella controllata, è necessario richiamare il metodo `CreateEndpointInfo` dell’oggetto `setConfigParameterAsText`. Ad esempio, per impostare il valore di configurazione `url`, richiamare il metodo `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e trasmettere i seguenti valori stringa:

   * Valore stringa che specifica il nome del valore di configurazione. Quando si imposta il valore di configurazione `url`, specificare `url`.
   * Valore stringa che specifica il valore di configurazione. Quando imposti il valore di configurazione `url`, specifica il percorso della cartella controllata.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori di configurazione impostati per il servizio EncryptDocument, vedi l&#39;esempio di codice Java situato in [QuickStart: Aggiunta di un endpoint per cartelle controllate tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Definisci i valori dei parametri di input.

   Definire un valore del parametro di input richiamando il metodo `setInputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Valore stringa che specifica il nome del parametro di input. Ad esempio, il nome del parametro di input per il servizio EncryptDocument è `InDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di input. Ad esempio, il tipo di dati del parametro di input `InDoc` è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mapping. Ad esempio, puoi specificare `variable`.
   * Valore stringa che specifica il valore del tipo di mappatura. Ad esempio, è possibile specificare &amp;ast;.pdf come pattern di file.

   >[!NOTE]
   >
   >Richiama il metodo `setInputParameterMapping` per ogni valore del parametro di input da definire. Poiché il processo EncryptDocument dispone di un solo parametro di input, è necessario richiamare questo metodo una volta.

1. Definire un valore del parametro di output.

   Definire un valore del parametro di output richiamando il metodo `setOutputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Valore stringa che specifica il nome del parametro di output. Ad esempio, il nome del parametro di output per il servizio EncryptDocument è `SecuredDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di output. Ad esempio, il tipo di dati del parametro di output `SecuredDoc` è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mapping. Ad esempio, puoi specificare `%F.pdf`.

1. Crea un endpoint per cartelle controllate.

   Creare il punto finale richiamando il metodo `createEndpoint` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta l&#39;endpoint Watched Folder.

1. Attiva l&#39;endpoint.

   Abilita l’endpoint richiamando il metodo `enable` dell’oggetto `EndpointRegistryClient` e passando l’oggetto `Endpoint` restituito dal metodo `createEndpoint` .

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Aggiunta di un endpoint per cartelle controllate tramite l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### File costante dei valori di configurazione delle cartelle controllate {#watched-folder-configuration-values-constant-file}

Avvio rapido [di: L&#39;aggiunta di un endpoint per cartelle controllate tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utilizza un file costante che deve far parte del progetto Java per compilare il quick start. Questo file costante rappresenta i valori di configurazione che devono essere impostati quando si aggiunge un endpoint Watched Folder. Il seguente codice Java rappresenta il file costante.

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

Puoi aggiungere programmaticamente un endpoint e-mail a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint e-mail, gli utenti possono inviare un messaggio e-mail con uno o più file allegati a un account e-mail specifico. Quindi viene richiamata l’operazione di configurazione del servizio e vengono manipolati i file. Dopo aver eseguito l’operazione specificata, il servizio invia un messaggio e-mail al mittente contenente i file modificati come allegati di file.

Ai fini dell&#39;aggiunta programmatica di un endpoint e-mail a un servizio, considera il seguente processo di breve durata denominato *MyApplication\EncryptDocument*. Per informazioni sui processi di breve durata, consulta [Informazioni sui processi AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Questo processo accetta un documento PDF non protetto come valore di input e quindi trasmette il documento PDF non protetto all&#39;operazione `EncryptPDFUsingPassword` del servizio di cifratura. Questo processo crittografa il documento PDF con una password e restituisce il documento PDF crittografato con password come valore di output. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF crittografato con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint e-mail utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per aggiungere un endpoint e-mail a un servizio, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Imposta gli attributi dell’endpoint e-mail.
1. Specifica i valori di configurazione.
1. Definisci i valori dei parametri di input.
1. Definire un valore del parametro di output.
1. Crea l’endpoint e-mail.
1. Attiva l&#39;endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Prima di poter aggiungere programmaticamente un endpoint e-mail, è necessario creare un oggetto `EndpointRegistryClient` .

**Impostare gli attributi dell’endpoint e-mail**

Per creare un endpoint e-mail per un servizio, specifica i seguenti valori:

* **Valore** dell&#39;identificatore del connettore: Specifica il tipo di endpoint creato. Per creare un endpoint e-mail, specifica `Email`.
* **Descrizione**: Specifica una descrizione per l&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Valore** dell&#39;identificatore del servizio: Specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint e-mail al processo introdotto in questa sezione (un processo diventa un servizio quando viene attivato tramite Workbench), specifica `EncryptDocument`.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. In genere, quando si crea un endpoint e-mail per un servizio creato da un processo creato in Workbench, il nome dell’operazione è `invoke`.

**Specificare i valori di configurazione**

È necessario specificare i valori di configurazione per un endpoint e-mail quando si aggiunge programmaticamente un endpoint e-mail a un servizio. Questi valori di configurazione vengono specificati da un amministratore se viene aggiunto un endpoint e-mail tramite la console di amministrazione.

>[!NOTE]
>
>L’account e-mail monitorato è un account speciale utilizzato solo per l’endpoint e-mail. Questo account non è un account e-mail di un utente regolare. L’account e-mail di un utente normale non deve essere configurato come account utilizzato dal provider e-mail, perché il provider e-mail elimina i messaggi e-mail dalla casella in entrata al termine dei messaggi.

I seguenti valori di configurazione vengono impostati quando si aggiunge programmaticamente un endpoint e-mail a un servizio:

* **cronExpression**: Un&#39;espressione cron se l&#39;e-mail deve essere pianificata utilizzando un&#39;espressione cron.
* **repeatCount**: Numero di volte in cui l’endpoint e-mail esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.
* **repeatInterval**: Velocità di scansione in secondi utilizzata dal ricevitore per il controllo della posta in arrivo. Il valore predefinito è 10.
* **startDelay**: Tempo di attesa per l&#39;analisi dopo l&#39;avvio della pianificazione. Il tempo predefinito è 0.
* **batchSize**: Il numero di messaggi e-mail che il ricevitore elabora per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.
* **userName**: Nome utente utilizzato per richiamare un servizio di destinazione da un messaggio e-mail. Il valore predefinito è `SuperAdmin`.
* **domainName**: Un valore di configurazione obbligatorio. Il valore predefinito è `DefaultDom`.
* **domainPattern**: Specifica i pattern di dominio delle e-mail in arrivo accettate dal provider. Ad esempio, se si utilizza `adobe.com`, viene elaborato solo l’e-mail da adobe.com, l’e-mail da altri domini viene ignorata.
* **filePattern**: Specifica i pattern di file allegato in ingresso accettati dal provider. Ciò include i file con estensioni di nome file specifiche (&amp;ast;.dat, &amp;ast;.xml), i file con nomi specifici (dati) e i file con espressioni composite nel nome e nell&#39;estensione (&amp;ast;.[dD][aA]&#39;port&#39;). Il valore predefinito è `*`.
* **recipientSuccfulJob**: Indirizzo e-mail a cui vengono inviati i messaggi per indicare l’esito positivo dei processi. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di lavoro riuscito. Se digiti `sender`, i risultati delle e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica i destinatari aggiuntivi con indirizzi e-mail, ciascuno separato da una virgola. Per disattivare questa opzione, lasciare vuoto questo valore. In alcuni casi, potresti voler attivare un processo e non volere una notifica via e-mail del risultato. Il valore predefinito è `sender`.
* **recipientFailedJob**: Indirizzo e-mail a cui vengono inviati i messaggi per indicare processi non riusciti. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di lavoro non riuscito. Se digiti `sender`, i risultati delle e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica i destinatari aggiuntivi con indirizzi e-mail, ciascuno separato da una virgola. Per disattivare questa opzione, lasciare vuoto questo valore. Il valore predefinito è `sender`.
* **inboxHost**: Nome host della casella in entrata o indirizzo IP da analizzare dal provider di posta elettronica.
* **inboxPort**: La porta utilizzata dal server e-mail. Il valore predefinito per POP3 è 110 e il valore predefinito per IMAP è 143. Se SSL è abilitato, il valore predefinito per POP3 è 995 e il valore predefinito per IMAP è 993.
* **inboxProtocol**: Il protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della casella in entrata. Le opzioni sono `IMAP` o `POP3`. Il server di posta elettronica host della casella in entrata deve supportare questi protocolli.
* **inboxTimeOut**: Timeout in secondi prima che il provider di posta elettronica attenda le risposte della casella in entrata. Il valore predefinito è 60.
* **inboxUser**: Nome utente necessario per accedere all’account e-mail. A seconda del server e-mail e della configurazione, questa può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.
* **inboxPassword**: Password per l’utente della inbox.
* **inboxSSLEnabled**: Imposta questo valore per forzare il provider di posta elettronica a utilizzare SSL durante l’invio di messaggi di notifica di risultati o errori. Assicurati che l&#39;host IMAP o POP3 supporti SSL.
* **smtpHost**: Nome host del server di posta a cui il provider di posta elettronica invia i risultati e i messaggi di errore.
* **smtpPort**: Il valore predefinito per la porta SMTP è 25.
* **smtpUser**: L’account utente del provider di posta elettronica da utilizzare quando invia notifiche e-mail di risultati ed errori.
* **smtpPassword**: Password dell&#39;account SMTP. Alcuni server di posta non richiedono una password SMTP.
* **charSet**: Il set di caratteri utilizzato dal provider di posta elettronica. Il valore predefinito è `UTF-8`.
* **smtpSSLEnabled**: Imposta questo valore per forzare il provider di posta elettronica a utilizzare SSL durante l’invio di messaggi di notifica di risultati o errori. Assicurati che l’host SMTP supporti SSL.
* **failedJobFolder**: Specifica una directory in cui memorizzare i risultati quando il server di posta SMTP non è operativo.
* **asincrono**: Se è impostato su sincrono, vengono elaborati tutti i documenti di input e viene restituita una sola risposta. Se è impostato su asincrono, viene inviata una risposta per ogni documento di input elaborato. Ad esempio, viene creato un endpoint e-mail per il processo introdotto in questo argomento e viene inviato un messaggio e-mail alla casella in entrata dell’endpoint che contiene più documenti PDF non protetti. Quando tutti i documenti PDF sono crittografati con una password e se l’endpoint è configurato come sincrono, viene inviato un singolo messaggio e-mail di risposta con tutti i documenti PDF protetti allegati. Se l’endpoint è configurato come asincrono, viene inviato un messaggio e-mail di risposta separato per ciascun documento PDF protetto. Ogni messaggio e-mail contiene un singolo documento PDF come allegato. Il valore predefinito è asincrono.

**Definire i valori dei parametri di input**

Quando crei un endpoint e-mail, devi definire i valori dei parametri di input. In altre parole, devi descrivere i valori di input passati all’operazione richiamata dall’endpoint e-mail. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di input denominato `InDoc` e il relativo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint e-mail per questo processo (dopo l&#39;attivazione di un processo, questo diventa un servizio), devi definire il valore del parametro di input.

Per definire i valori dei parametri di input richiesti per un endpoint e-mail, specifica i seguenti valori:

**Nome** del parametro di input: Nome del parametro di input. Il nome di un valore di input viene specificato in Workbench per un processo. Se il valore di input appartiene a un’operazione di servizio (un servizio Forms che non è un processo creato in Workbench), il nome di input viene specificato nel file component.xml. Ad esempio, il nome del parametro di input per il processo introdotto in questa sezione è `InDoc`.

**Tipo** di mappatura: Utilizzato per configurare i valori di input necessari per richiamare l&#39;operazione del servizio. Due tipi di mappatura sono i seguenti:

* `Literal`: L’endpoint e-mail utilizza il valore immesso nel campo così come viene visualizzato. Sono supportati tutti i tipi Java di base. Ad esempio, se un’API utilizza input quali String, long, int e Boolean, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.
* `Variable`: Il valore inserito è un pattern di file utilizzato dall’endpoint e-mail per selezionare l’input. Ad esempio, se selezioni Variabile per il tipo di mappatura e il documento di input deve essere un file PDF, puoi specificare `*.pdf` come valore di mappatura.

**Valore** mappatura: Specifica il valore del tipo di mappatura. Ad esempio, se selezioni un tipo di mappatura Variabile, puoi specificare `*.pdf` come pattern di file.

**Tipo** di dati: Specifica il tipo di dati dei valori di input. Ad esempio, il tipo di dati del valore di input del processo introdotto in questa sezione è com.adobe.idp.Document.

**Definire un valore del parametro di output**

Quando crei un endpoint e-mail, devi definire un valore di parametro di output. In altre parole, devi descrivere il valore di output restituito dal servizio richiamato dall’endpoint e-mail. Ad esempio, considera il processo introdotto in questo argomento. Ha un valore di output denominato `SecuredDoc` e il relativo tipo di dati è `com.adobe.idp.Document`. Quando crei un endpoint e-mail per questo processo (dopo l&#39;attivazione di un processo, questo diventa un servizio), devi definire il valore del parametro di output.

Per definire un valore del parametro di output richiesto per un endpoint e-mail, specifica i seguenti valori:

**Nome** del parametro di output: Nome del parametro di output. Il nome di un valore di output del processo è specificato in Workbench. Se il valore di output appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di output viene specificato nel file component.xml. Ad esempio, il nome del parametro di output per il processo introdotto in questa sezione è `SecuredDoc`.

**Tipo** di mappatura: Utilizzato per configurare l&#39;output del servizio e l&#39;operazione. Sono disponibili le seguenti opzioni:

* Se il servizio restituisce un singolo oggetto (un singolo documento), il pattern è `%F.pdf` e la destinazione di origine è sourcefilename.pdf. Ad esempio, il processo introdotto in questa sezione restituisce un singolo documento. Di conseguenza, il tipo di mappatura può essere definito come `%F.pdf` ( `%F` significa utilizzare il nome file specificato). Il pattern `%E` specifica l’estensione del documento di input.
* Se il servizio restituisce un elenco, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se il servizio restituisce una mappa, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\file1 and Result\sourcefilename\file2. Se la mappa ha più di un oggetto, il pattern è `Result\%F.pdf` e la destinazione di origine è Result\sourcefilename1.pdf (output 1), Result\sourcefilenam2.pdf (output 2) e così via.

**Tipo** di dati: Specifica il tipo di dati del valore restituito. Ad esempio, il tipo di dati del valore restituito del processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Creare l’endpoint e-mail**

Dopo aver impostato gli attributi e i valori di configurazione dell’endpoint e-mail e aver definito i valori dei parametri di input e output, devi creare l’endpoint e-mail.

**Abilitare l’endpoint**

Dopo aver creato un endpoint e-mail, devi attivarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiungi un endpoint e-mail utilizzando l’API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungi un endpoint e-mail utilizzando l&#39;API Java {#add-an-email-endpoint-using-the-java-api}

Aggiungi un endpoint e-mail utilizzando l’API Java:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Imposta gli attributi dell’endpoint e-mail.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specifica il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `Email`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `setName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifichi il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che specifichi il nome del servizio.
   * Specificare l&#39;operazione che viene richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. In genere, quando si crea un endpoint e-mail per un servizio creato da un processo creato in Workbench, viene richiamato il nome dell’operazione.

1. Specifica i valori di configurazione.

   Per ogni valore di configurazione da impostare per l’endpoint e-mail, è necessario richiamare il metodo `CreateEndpointInfo` dell’oggetto `setConfigParameterAsText`. Ad esempio, per impostare il valore di configurazione `smtpHost`, richiamare il metodo `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome del valore di configurazione. Quando si imposta il valore di configurazione `smtpHost`, specificare `smtpHost`.
   * Valore stringa che specifica il valore di configurazione. Quando si imposta il valore di configurazione `smtpHost`, specificare un valore stringa che specifichi il nome del server SMTP.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori di configurazione impostati per il servizio EncryptDocument introdotto in questa sezione, vedi l&#39;esempio di codice Java situato in [QuickStart: Aggiunta di un endpoint e-mail utilizzando l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Definisci i valori dei parametri di input.

   Definire un valore del parametro di input richiamando il metodo `setInputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Valore stringa che specifica il nome del parametro di input. Ad esempio, il nome del parametro di input per il servizio EncryptDocument è `InDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di input. Ad esempio, il tipo di dati del parametro di input `InDoc` è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mapping. Ad esempio, puoi specificare `variable`.
   * Valore stringa che specifica il valore del tipo di mappatura. Ad esempio, è possibile specificare &amp;ast;.pdf come pattern di file.

   >[!NOTE]
   >
   >Richiama il metodo `setInputParameterMapping` per ogni valore del parametro di input da definire. Poiché il processo EncryptDocument dispone di un solo parametro di input, è necessario richiamare questo metodo una volta.

1. Definire un valore del parametro di output.

   Definire un valore del parametro di output richiamando il metodo `setOutputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Valore stringa che specifica il nome del parametro di output. Ad esempio, il nome del parametro di output per il servizio EncryptDocument è `SecuredDoc`.
   * Valore stringa che specifica il tipo di dati del parametro di output. Ad esempio, il tipo di dati del parametro di output `SecuredDoc` è `com.adobe.idp.Document`.
   * Valore stringa che specifica il tipo di mapping. Ad esempio, puoi specificare `%F.pdf`.

1. Crea l’endpoint e-mail.

   Creare il punto finale richiamando il metodo `createEndpoint` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta l’endpoint e-mail.

1. Attiva l&#39;endpoint.

   Abilita l’endpoint richiamando il metodo `enable` dell’oggetto `EndpointRegistryClient` e passando l’oggetto `Endpoint` restituito dal metodo `createEndpoint` .

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Aggiunta di un endpoint per cartelle controllate tramite l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### File costante dei valori di configurazione e-mail {#email-configuration-values-constant-file}

Avvio rapido [di: L&#39;aggiunta di un endpoint e-mail tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) utilizza un file costante che deve far parte del progetto Java per compilare il quick start. Questo file costante rappresenta i valori di configurazione che devono essere impostati quando si aggiunge un endpoint e-mail. Il seguente codice Java rappresenta il file costante.

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

Puoi aggiungere programmaticamente un endpoint Remoting a un servizio utilizzando l&#39;API Java di AEM Forms. Aggiungendo un endpoint Remoting, si sta abilitando un&#39;applicazione Flex per richiamare il servizio utilizzando remoting. (Vedere [Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Ai fini dell&#39;aggiunta programmatica di un endpoint Remoting a un servizio, considera il seguente processo di breve durata denominato *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Questo processo accetta un documento PDF non protetto come valore di input e quindi trasmette il documento PDF non protetto all&#39;operazione `EncryptPDFUsingPassword` del servizio di cifratura. Il documento PDF è crittografato con una password e il documento PDF crittografato con password è il valore di output di questo processo. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF crittografato con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

Per illustrare come aggiungere un endpoint Remoting a un servizio, in questa sezione viene aggiunto un endpoint Remoting a un servizio denominato EncryptDocument.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint Remoting utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-4}

Per rimuovere un endpoint da un servizio, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Impostare gli attributi dell&#39;endpoint remoto.
1. Creare un endpoint remoto.
1. Attiva l&#39;endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per aggiungere programmaticamente un endpoint Remoting, è necessario creare un oggetto `EndpointRegistryClient`.

**Impostare gli attributi dell&#39;endpoint remoto**

Per creare un endpoint remoto per un servizio, specificare i seguenti valori:

* **Valore** dell&#39;identificatore del connettore: Specifica il tipo di endpoint creato. Per creare un endpoint Remoting, specificare `Remoting`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Valore** dell&#39;identificatore del servizio: Specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint Remoting al processo introdotto in questa sezione (un processo diventa un servizio quando viene attivato in Workbench), specificare `EncryptDocument`.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. Durante la creazione di un endpoint remoto, specificare un carattere jolly (&amp;ast;).

**Creare un endpoint remoto**

Dopo aver impostato gli attributi dell&#39;endpoint remoto, è possibile creare un endpoint remoto per un servizio.

**Abilitare l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando un endpoint remoto è abilitato, consente a un client Flex di richiamare il servizio.

**Consulta anche**

[Aggiungere un endpoint remoto utilizzando l&#39;API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungi un endpoint remoto utilizzando l&#39;API Java {#add-a-remoting-endpoint-using-the-java-api}

Aggiungi un endpoint remoto utilizzando l&#39;API Java:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare gli attributi dell&#39;endpoint remoto.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specifica il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `Remoting`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `setName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifichi il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che specifichi il nome del servizio.
   * Specificare l&#39;operazione richiamata dal metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passare un valore stringa che specifichi il nome dell&#39;operazione. Per un endpoint remoto, specificare un carattere jolly (&amp;ast;).

1. Creare un endpoint remoto.

   Creare il punto finale richiamando il metodo `createEndpoint` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint Remoting.

1. Attiva l&#39;endpoint.

   Abilita l’endpoint richiamando il metodo `enable` dell’oggetto `EndpointRegistryClient` e passando l’oggetto `Endpoint` restituito dal metodo `createEndpoint` .

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Aggiunta di un endpoint remoto utilizzando l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint TaskManager {#adding-taskmanager-endpoints}

Puoi aggiungere programmaticamente un endpoint TaskManager a un servizio utilizzando l’API Java di AEM Forms. Aggiungendo un endpoint TaskManager a un servizio, è possibile abilitare un utente Workspace a richiamare il servizio. In altre parole, un utente che lavora in Workspace può richiamare un processo con un endpoint TaskManager corrispondente.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint TaskManager utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-5}

Per aggiungere un endpoint TaskManager a un servizio, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Crea una categoria per l’endpoint.
1. Impostare gli attributi dell&#39;endpoint TaskManager.
1. Creare un endpoint TaskManager.
1. Attiva l&#39;endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Prima di poter aggiungere programmaticamente un endpoint TaskManager, è necessario creare un oggetto `EndpointRegistryClient`.

**Crea una categoria per l’endpoint**

Le categorie vengono utilizzate per organizzare i servizi all’interno di Workspace. In altre parole, un utente di Workspace può richiamare un servizio con un endpoint TaskManager selezionando una categoria all’interno di Workspace. Durante la creazione di un endpoint TaskManager, è possibile fare riferimento a una categoria esistente o crearne una nuova a livello di programmazione.

>[!NOTE]
>
>Questa sezione crea una nuova categoria come parte dell&#39;aggiunta di un endpoint TaskManager a un servizio.

**Imposta gli attributi dell’endpoint TaskManager**

Per creare un endpoint TaskManager per un servizio, specificare i seguenti valori:

* **Identificatore** del connettore: Specifica il tipo di endpoint creato. Per creare un endpoint TaskManager, specificare `TaskManagerConnector`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Identificatore** del servizio: Specifica il servizio a cui appartiene l&#39;endpoint.
* **Categoria**: Specifica un valore di identificatore di categoria associato all&#39;endpoint TaskManager.
* **Nome** operazione: In genere, quando si crea un endpoint TaskManager per un servizio creato da un processo creato in Workbench, il nome dell&#39;operazione è  `invoke`.

**Creare un endpoint TaskManager**

Dopo aver impostato gli attributi dell&#39;endpoint TaskManager, è possibile creare un endpoint TaskManager per un servizio.

**Abilitare l’endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l’endpoint è abilitato può essere utilizzato per richiamare il servizio dall’interno di Workspace. Dopo aver abilitato l’endpoint, puoi visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiungere un endpoint TaskManager utilizzando l’API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungi un endpoint TaskManager utilizzando l&#39;API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Aggiungi un endpoint TaskManager utilizzando l&#39;API Java:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Crea una categoria per l’endpoint.

   * Creare un oggetto `CreateEndpointCategoryInfo` utilizzando il relativo costruttore e passando i seguenti valori:

      * Valore stringa che specifica il valore di identificazione della categoria
      * Valore stringa che specifica la descrizione della categoria
   * Creare la categoria richiamando il metodo `createEndpointCategory` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `CreateEndpointCategoryInfo`. Questo metodo restituisce un oggetto `EndpointCategory` che rappresenta la nuova categoria.


1. Impostare gli attributi dell&#39;endpoint TaskManager.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specifica il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `TaskManagerConnector`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `setName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifichi il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che specifichi il nome del servizio.
   * Specificare la categoria a cui appartiene l&#39;endpoint richiamando il metodo `setCategoryId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore stringa che specifica il valore dell&#39;identificatore della categoria. È possibile richiamare il metodo `getId` dell&#39;oggetto `EndpointCategory` per ottenere il valore dell&#39;identificatore di questa categoria.
   * Specificare l&#39;operazione che viene richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. In genere, quando si crea un endpoint `TaskManager` per un servizio creato da un processo creato in Workbench, il nome dell&#39;operazione è `invoke`.

1. Creare un endpoint TaskManager.

   Creare il punto finale richiamando il metodo `createEndpoint` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint TaskManager.

1. Attiva l&#39;endpoint.

   Abilita l’endpoint richiamando il metodo `enable` dell’oggetto `EndpointRegistryClient` e passando l’oggetto `Endpoint` restituito dal metodo `createEndpoint` .

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Aggiunta di un endpoint TaskManager utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modifica degli endpoint {#modifying-endpoints}

Puoi modificare programmaticamente un endpoint esistente utilizzando l’API Java di AEM Forms. Modificando un endpoint, potete modificare il comportamento dell’endpoint. Considera, ad esempio, un endpoint Cartella controllata che specifica una cartella utilizzata come cartella controllata. Puoi modificare programmaticamente i valori di configurazione che appartengono all’endpoint Cartella controllata, in modo che un’altra cartella funzioni come cartella controllata. Per informazioni sui valori di configurazione che appartengono a un endpoint di una cartella controllata, vedere [Aggiunta di endpoint di cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints).

Per illustrare come modificare un endpoint, in questa sezione viene modificato un endpoint di tipo Cartella controllata modificando la cartella che si comporta come cartella controllata.

>[!NOTE]
>
>Non è possibile modificare un endpoint utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-6}

Per modificare un endpoint, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Recupera l’endpoint.
1. Specifica i nuovi valori di configurazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per modificare programmaticamente un endpoint, è necessario creare un oggetto `EndpointRegistryClient` .

**Recupera l’endpoint da modificare**

Prima di poter modificare un endpoint, è necessario recuperarlo. Per recuperare un endpoint, è necessario connettersi come utente in grado di accedere a un endpoint. È consigliabile connettersi come amministratore. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

È possibile recuperare un endpoint recuperando un elenco di endpoint. È quindi possibile eseguire iterazioni nell’elenco, cercando l’endpoint specifico da rimuovere. Ad esempio, è possibile individuare un endpoint determinando il servizio corrispondente all&#39;endpoint e il tipo di endpoint. Quando individua l’endpoint, puoi modificarlo.

**Specificare nuovi valori di configurazione**

Quando modifichi un endpoint, specifica nuovi valori di configurazione. Ad esempio, per modificare un endpoint di una cartella controllata, reimposta tutti i valori di configurazione dell’endpoint della cartella controllata, non solo quelli che desideri modificare. Per informazioni sui valori di configurazione che appartengono a un endpoint di una cartella controllata, vedere [Aggiunta di endpoint di cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Per informazioni sui valori di configurazione che appartengono a un endpoint e-mail, consulta [Aggiunta di endpoint e-mail](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Non è possibile modificare il servizio richiamato dall&#39;endpoint. Se tenti di modificare il servizio, viene generata un’eccezione. Per modificare il servizio associato a un determinato endpoint, rimuovi l&#39;endpoint e creane uno nuovo. (Vedere [Rimozione di endpoint](programmatically-endpoints.md#removing-endpoints).)

**Consulta anche**

[Modifica di un endpoint utilizzando l’API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modifica di un endpoint utilizzando l&#39;API Java {#modifying-an-endpoint-using-the-java-api}

Modificare un endpoint utilizzando l&#39;API Java:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera l’endpoint da modificare.

   * Recupera un elenco di tutti gli endpoint a cui l&#39;utente corrente (specificato nelle proprietà di connessione) può accedere richiamando il metodo `getEndpoints` dell&#39;oggetto `EndpointRegistryClient` e passando un oggetto `PagingFilter` che agisce come filtro. Puoi trasmettere un valore `(PagingFilter)null` per restituire tutti gli endpoint. Questo metodo restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `Endpoint`. Per informazioni su un oggetto `PagingFilter`, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Itera attraverso l&#39;oggetto `java.util.List` per determinare se dispone di endpoint. Se esistono endpoint, ogni elemento è un&#39;istanza `EndPoint`.
   * Determina il servizio che corrisponde a un endpoint richiamando il metodo `getServiceId` dell&#39;oggetto `EndPoint`. Questo metodo restituisce un valore stringa che specifica il nome del servizio.
   * Determinare il tipo di endpoint richiamando il metodo `getConnectorId` dell&#39;oggetto `EndPoint`. Questo metodo restituisce un valore di stringa che specifica il tipo di endpoint. Ad esempio, se l’endpoint è un endpoint di tipo Cartella controllata, questo metodo restituisce `WatchedFolder`.

1. Specifica i nuovi valori di configurazione.

   * Creare un oggetto `ModifyEndpointInfo` richiamando il relativo costruttore.
   * Per ogni valore di configurazione da impostare, richiamare il metodo `ModifyEndpointInfo` dell&#39;oggetto `setConfigParameterAsText`. Ad esempio, per impostare il valore di configurazione dell’URL, richiama il metodo `setConfigParameterAsText` dell’oggetto `ModifyEndpointInfo` e passa i seguenti valori:

      * Valore stringa che specifica il nome del valore di configurazione. Ad esempio, per impostare il valore di configurazione `url`, specificare `url`.
      * Valore stringa che specifica il valore di configurazione. Per definire un valore per il valore di configurazione `url`, specifica il percorso della cartella controllata.
   * Richiamare il metodo `modifyEndpoint` dell&#39;oggetto `EndpointRegistryClient` e passare l&#39;oggetto `ModifyEndpointInfo`.


**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Modifica di un endpoint utilizzando l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rimozione di endpoint {#removing-endpoints}

Puoi rimuovere programmaticamente un endpoint da un servizio utilizzando l&#39;API Java di AEM Forms. Dopo la rimozione di un endpoint, non è possibile richiamare il servizio utilizzando il metodo di chiamata che l&#39;endpoint ha abilitato. Ad esempio, se si rimuove un endpoint SOAP da un servizio, non è possibile richiamare il servizio utilizzando la modalità SOAP.

Per dimostrare come rimuovere un endpoint da un servizio, questa sezione rimuove un endpoint EJB da un servizio denominato *EncryptDocument*.

>[!NOTE]
>
>Non è possibile rimuovere un endpoint utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-7}

Per rimuovere un endpoint da un servizio, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Recupera l’endpoint.
1. Rimuovi l&#39;endpoint.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per rimuovere un endpoint a livello di programmazione, è necessario creare un oggetto `EndpointRegistryClient` .

**Recupera l’endpoint da rimuovere**

Prima di rimuovere un endpoint, è necessario recuperarlo. Per recuperare un endpoint, è necessario connettersi come utente in grado di accedere a un endpoint. È consigliabile connettersi come amministratore. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

È possibile recuperare un endpoint recuperando un elenco di endpoint. È quindi possibile eseguire iterazioni nell’elenco, cercando l’endpoint specifico da rimuovere. Ad esempio, è possibile individuare un endpoint determinando il servizio corrispondente all&#39;endpoint e il tipo di endpoint. Quando si individua l&#39;endpoint, è possibile rimuoverlo.

**Rimuovere l&#39;endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver abilitato l’endpoint, puoi visualizzarlo nella console di amministrazione.

**Consulta anche**

[Rimozione di un endpoint utilizzando l&#39;API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimozione di un endpoint utilizzando l&#39;API Java {#removing-an-endpoint-using-the-java-api}

Rimuovi un endpoint utilizzando l&#39;API Java:

1. Includi file di progetto.

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera l’endpoint da rimuovere.

   * Recupera un elenco di tutti gli endpoint a cui l&#39;utente corrente (specificato nelle proprietà di connessione) ha accesso richiamando il metodo `getEndpoints` dell&#39;oggetto `EndpointRegistryClient` e passando un oggetto `PagingFilter` che agisce come filtro. Puoi passare `(PagingFilter)null` per restituire tutti gli endpoint. Questo metodo restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `Endpoint`.
   * Itera attraverso l&#39;oggetto `java.util.List` per determinare se dispone di endpoint. Se esistono endpoint, ogni elemento è un&#39;istanza `EndPoint`.
   * Determina il servizio che corrisponde a un endpoint richiamando il metodo `getServiceId` dell&#39;oggetto `EndPoint`. Questo metodo restituisce un valore stringa che specifica il nome del servizio.
   * Determinare il tipo di endpoint richiamando il metodo `getConnectorId` dell&#39;oggetto `EndPoint`. Questo metodo restituisce un valore di stringa che specifica il tipo di endpoint. Ad esempio, se l’endpoint è un endpoint EJB, questo metodo restituisce `EJB`.

1. Rimuovi l&#39;endpoint.

   Rimuovere l&#39;endpoint richiamando il metodo `remove` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `EndPoint` che rappresenta l&#39;endpoint da rimuovere.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Rimozione di un endpoint utilizzando l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recupero informazioni sul connettore endpoint {#retrieving-endpoint-connector-information}

Puoi recuperare in modo programmatico informazioni sui connettori endpoint utilizzando l’API di AEM Forms. Un connettore consente a un endpoint di richiamare un servizio utilizzando vari metodi di chiamata. Ad esempio, un connettore per cartelle controllate consente a un endpoint di richiamare un servizio utilizzando cartelle controllate. Recuperando programmaticamente le informazioni sui connettori endpoint, puoi recuperare i valori di configurazione associati a un connettore, ad esempio quali valori di configurazione sono obbligatori e quali facoltativi.

Per dimostrare come recuperare informazioni sui connettori endpoint, questa sezione recupera informazioni su un connettore per cartelle controllate. (Vedere [Aggiunta di endpoint di cartelle controllate](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Non è possibile recuperare informazioni sugli endpoint utilizzando i servizi Web.

>[!NOTE]
>
>Questo argomento utilizza l’ API `ConnectorRegistryClient` per recuperare informazioni sui connettori endpoint. (Consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Riepilogo dei passaggi {#summary_of_steps-8}

Per recuperare le informazioni sul connettore endpoint, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto `ConnectorRegistryClient`.
1. Specifica il tipo di connettore.
1. Recupera i valori di configurazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Se AEM Forms è distribuito su un server applicazioni J2EE supportato che non è JBoss, sostituisci adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, consulta [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client ConnectorRegistry**

Per recuperare in modo programmatico le informazioni sul connettore endpoint, crea un oggetto `ConnectorRegistryClient` .

**Specifica il tipo di connettore**

Specifica il tipo di connettore da cui recuperare le informazioni. Esistono i seguenti tipi di connettori:

* **EJB**: Consente a un&#39;applicazione client di richiamare un servizio utilizzando la modalità EJB.
* **SOAP**: Consente a un&#39;applicazione client di richiamare un servizio utilizzando la modalità SOAP.
* **Cartella** osservata: Consente alle cartelle controllate di richiamare un servizio.
* **E-mail**: Consente ai messaggi e-mail di richiamare un servizio.
* **Remoto**: Consente a un&#39;applicazione client Flex di richiamare un servizio.
* **Connettore** TaskManager: Consente a un utente di Workspace di richiamare un servizio dall’interno di Workspace.

**Recupera i valori di configurazione**

Dopo aver specificato il tipo di connettore, puoi recuperare informazioni sul connettore, ad esempio il valore di configurazione supportato. Ad esempio, per qualsiasi connettore, puoi determinare quali valori di configurazione sono obbligatori e quali sono facoltativi.

**Consulta anche**

[Recupera le informazioni sul connettore endpoint utilizzando l’API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupera le informazioni sul connettore endpoint utilizzando l&#39;API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recupera le informazioni sul connettore endpoint utilizzando l’API Java:

1. Includi file di progetto. .

   Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client ConnectorRegistry.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `ConnectorRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Specifica il tipo di connettore.

   Specificare il tipo di connettore richiamando il metodo `getEndpointDefinition` dell&#39;oggetto `ConnectorRegistryClient` e passando un valore di stringa che specifica il tipo di connettore. Ad esempio, per specificare il tipo di connettore Cartella controllata, passare il valore stringa `WatchedFolder`. Questo metodo restituisce un oggetto `Endpoint` che corrisponde al tipo di connettore.

1. Recupera i valori di configurazione.

   * Recupera i valori di configurazione associati all&#39;interno dell&#39;endpoint richiamando il metodo `getConfigParameters` dell&#39;oggetto `Endpoint`. Questo metodo restituisce una matrice di oggetti `ConfigParameter`.
   * Recupera le informazioni su ciascun valore di configurazione recuperando ogni elemento all’interno dell’array. Ogni elemento è un oggetto `ConfigParameter`. Ad esempio, è possibile determinare se il valore di configurazione è obbligatorio o facoltativo richiamando il metodo `isRequired` dell&#39;oggetto `ConfigParameter`. Se il valore di configurazione è obbligatorio, questo metodo restituisce `true`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Guida introduttiva: Recupero delle informazioni sul connettore endpoint tramite API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
