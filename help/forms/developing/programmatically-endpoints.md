---
title: Gestione programmatica degli endpoint
seo-title: Gestione programmatica degli endpoint
description: Utilizzate il servizio Endpoint Registry per aggiungere endpoint EJB, aggiungere endpoint SOAP, aggiungere endpoint di cartelle esaminate, aggiungere endpoint e-mail, aggiungere endpoint Remoting, aggiungere endpoint Task Manager, modificare endpoint, rimuovere endpoint e recuperare informazioni sul connettore endpoint.
seo-description: Utilizzate il servizio Endpoint Registry per aggiungere endpoint EJB, aggiungere endpoint SOAP, aggiungere endpoint di cartelle esaminate, aggiungere endpoint e-mail, aggiungere endpoint Remoting, aggiungere endpoint Task Manager, modificare endpoint, rimuovere endpoint e recuperare informazioni sul connettore endpoint.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '10863'
ht-degree: 1%

---


# Gestione programmatica degli endpoint {#programmatically-managing-endpoints}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

**Informazioni su Endpoint Registry Service**

Il servizio del Registro di sistema degli endpoint consente di gestire gli endpoint a livello di programmazione. Ad esempio, potete aggiungere i seguenti tipi di endpoint a un servizio:

* EJB
* SOAP
* Cartella esaminata
* E-mail
* (Obsoleto per AEM moduli) Remoting
* Task Manager

>[!NOTE]
>
>SOAP, EJB e (obsoleto per i moduli AEM su JEE) Gli endpoint di promemoria vengono creati automaticamente per ciascun servizio attivato. Gli endpoint SOAP ed EJB consentono SOAP ed EJB per tutte le operazioni di servizio.

Un endpoint remoto consente ai client Flex di richiamare le operazioni sul servizio AEM Forms  a cui viene aggiunto l&#39;endpoint. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare le operazioni sul servizio appropriato.

Gli endpoint E-mail, Task Manager e Cartella esaminata mostrano solo un&#39;operazione specifica del servizio. L&#39;aggiunta di questi endpoint richiede un secondo passaggio di configurazione per selezionare un metodo da richiamare, impostare i parametri di configurazione e specificare le mappature dei parametri di input e output.

È possibile organizzare gli endpoint di TaskManager in gruppi denominati *categorie*. Queste categorie vengono quindi esposte a Workspace tramite TaskManager, con gli utenti finali che visualizzano gli endpoint di TaskManager man mano che vengono classificati. In Workspace, gli utenti finali visualizzano queste categorie nel riquadro di navigazione. Gli endpoint all&#39;interno di ciascuna categoria vengono visualizzati come schede di processo nella pagina Processi iniziali di Workspace.

È possibile eseguire le seguenti attività utilizzando il servizio del Registro di sistema di Endpoint:

* Aggiungete gli endpoint EJB. (Vedere [Aggiunta di endpoint EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Aggiungere endpoint SOAP. (Vedere [Aggiunta di endpoint SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Aggiungi endpoint cartella esaminata (vedere [Aggiunta di endpoint cartella esaminata](programmatically-endpoints.md#adding-watched-folder-endpoints)).
* Aggiungi endpoint e-mail. (Vedere [Aggiunta di endpoint e-mail](programmatically-endpoints.md#adding-email-endpoints).)
* Aggiungi endpoint di tipo promemoria. (Vedere [Aggiunta di endpoint remoti](programmatically-endpoints.md#adding-remoting-endpoints).)
* Aggiungere endpoint TaskManager (vedere [Aggiunta di endpoint TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints)).
* Modificare gli endpoint (vedere [Modifica di endpoint](programmatically-endpoints.md#modifying-endpoints)).
* Rimuovere gli endpoint (vedere [Rimozione di endpoint](programmatically-endpoints.md#removing-endpoints)).
* Recuperare le informazioni sul connettore endpoint (vedere [Recupero delle informazioni sul connettore endpoint](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Aggiunta di endpoint EJB {#adding-ejb-endpoints}

Puoi aggiungere a livello di programmazione un endpoint EJB a un servizio utilizzando l&#39;API Java di AEM Forms . Aggiungendo un endpoint EJB a un servizio, si sta abilitando un&#39;applicazione client per richiamare il servizio utilizzando la modalità EJB. In altre parole, quando si impostano le proprietà di connessione necessarie per richiamare  AEM Forms, è possibile selezionare la modalità EJB. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Non è possibile aggiungere un endpoint EJB utilizzando i servizi Web.

>[!NOTE]
>
>In genere, un endpoint EJB viene aggiunto a un servizio per impostazione predefinita. Tuttavia, un endpoint EJB può essere aggiunto a un processo distribuito a livello di programmazione o quando un endpoint EJB è stato rimosso e deve essere aggiunto di nuovo.

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un endpoint EJB a un servizio, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistry Client`.
1. Impostate gli attributi dell’endpoint EJB.
1. Create un endpoint EJB.
1. Abilitate l’endpoint.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Prima di poter aggiungere un endpoint EJB a livello di programmazione, è necessario creare un oggetto `EndpointRegistryClient`.

**Impostazione degli attributi dell’endpoint EJB**

Per creare un endpoint EJB per un servizio, specificate i seguenti valori:

* **Identificatore** del connettore: Specifica il tipo di endpoint da creare. Per creare un endpoint EJB, specificate `EJB`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Identificatore** servizio: Specifica il servizio a cui appartiene l&#39;endpoint.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. Quando create un endpoint EJB, specificate un carattere jolly ( `*`). Tuttavia, se si desidera specificare un&#39;operazione specifica invece di richiamare tutte le operazioni del servizio, specificare il nome dell&#39;operazione anziché utilizzare il carattere jolly ( `*`).

**Creare un endpoint EJB**

Dopo aver impostato gli attributi dell&#39;endpoint EJB, potete creare un endpoint EJB per un servizio.

**Abilitare l&#39;endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Dopo aver abilitato l&#39;endpoint, può essere utilizzato per richiamare il servizio. Dopo aver attivato l’endpoint, potete visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiunta di un endpoint EJB tramite l&#39;API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiunta di un endpoint EJB mediante l&#39;API Java {#adding-an-ejb-endpoint-using-the-java-api}

Aggiungete un endpoint EJB utilizzando l&#39;API Java:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java. (

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostate gli attributi dell’endpoint EJB.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specificare il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `EJB`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore di stringa che specifica il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passare un valore di stringa che specifica il nome dell&#39;operazione. Per gli endpoint SOAP ed EJB, specificate un carattere jolly ( `*`) che implica tutte le operazioni.

1. Create un endpoint EJB.

   Creare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint EJB.

1. Abilitate l’endpoint.

   Abilitare l&#39;endpoint richiamando il metodo di abilitazione dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `Endpoint` restituito dal metodo `createEndpoint`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Aggiunta di un endpoint EJB tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint SOAP {#adding-soap-endpoints}

È possibile aggiungere a livello di programmazione un endpoint SOAP a un servizio utilizzando l&#39;API Java di AEM Forms . Aggiungendo un endpoint SOAP, si abilita un&#39;applicazione client per richiamare il servizio utilizzando la modalità SOAP. In altre parole, quando si impostano le proprietà di connessione necessarie per richiamare  AEM Forms, è possibile selezionare la modalità SOAP.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint SOAP utilizzando i servizi Web.

>[!NOTE]
>
>In genere, un endpoint SOAP viene aggiunto a un servizio per impostazione predefinita, tuttavia, un endpoint SOAP può essere aggiunto a un processo distribuito a livello di programmazione o quando un endpoint SOAP è stato rimosso e deve essere aggiunto di nuovo.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per aggiungere un endpoint SOAP a un servizio, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Impostate gli attributi dell&#39;endpoint SOAP.
1. Creare un endpoint SOAP.
1. Abilitate l’endpoint.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Questi file JAR sono necessari per creare un endpoint SOAP. Tuttavia, è necessario aggiungere file JAR se si utilizza l&#39;endpoint SOAP per richiamare il servizio. Per informazioni su  file AEM Forms JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per aggiungere a livello di programmazione un endpoint SOAP a un servizio, è necessario creare un oggetto `EndpointRegistryClient`.

**Imposta attributi endpoint SOAP**

Per aggiungere un endpoint SOAP a un servizio, specificate i seguenti valori:

* **Valore** identificatore connettore: Specifica il tipo di endpoint da creare. Per creare un endpoint SOAP, specificare `SOAP`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Valore** ID servizio: Specifica il servizio a cui appartiene l&#39;endpoint.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. Quando create un endpoint SOAP, specificate un carattere jolly ( `*`). Tuttavia, se si desidera specificare un&#39;operazione specifica invece di richiamare tutte le operazioni del servizio, specificare il nome dell&#39;operazione anziché utilizzare il carattere jolly ( `*`).

**Creare un endpoint SOAP**

Dopo aver impostato gli attributi dell&#39;endpoint SOAP, potete creare un endpoint SOAP.

**Abilitare l&#39;endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l&#39;endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver attivato l’endpoint, potete visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiunta di un endpoint SOAP tramite l&#39;API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiunta di un endpoint SOAP utilizzando l&#39;API Java {#add-a-soap-endpoint-using-the-java-api}

Aggiungete un endpoint SOAP a un servizio utilizzando l&#39;API Java:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostate gli attributi dell&#39;endpoint SOAP.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specificare il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `SOAP`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore di stringa che specifica il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. Per gli endpoint SOAP ed EJB, specificate un carattere jolly ( `*`) che implica tutte le operazioni.

1. Creare un endpoint SOAP.

   Creare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint SOAP.

1. Abilitate l’endpoint.

   Abilitare l&#39;endpoint richiamando il metodo di abilitazione dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `Endpoint` restituito dal metodo `createEndpoint`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Aggiunta di un endpoint SOAP tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint cartella esaminata {#adding-watched-folder-endpoints}

È possibile aggiungere a livello di programmazione un endpoint di cartelle esaminate a un servizio utilizzando l&#39;API Java di AEM Forms . Aggiungendo un endpoint cartella esaminata, gli utenti possono inserire un file (ad esempio un file PDF) in una cartella. Quando il file viene inserito nella cartella, viene richiamato il servizio configurato e manipolato il file. Dopo che il servizio ha eseguito l&#39;operazione specificata, salva il file modificato in una cartella di output specificata. Una cartella esaminata è configurata per essere analizzata a un intervallo di frequenza fissa o con una pianificazione cron, ad esempio ogni lunedì, mercoledì e venerdì a mezzogiorno.

Per aggiungere in modo programmatico un endpoint di cartelle esaminate a un servizio, prendere in considerazione il seguente processo di breve durata denominato *EncryptDocument*. (Vedere [Informazioni  processi AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Questo processo accetta un documento PDF non protetto come valore di input, quindi passa il documento PDF non protetto all&#39;operazione `EncryptPDFUsingPassword` del servizio di cifratura. Il documento PDF è crittografato con una password e il documento PDF crittografato con password è il valore di output di questo processo. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint cartella esaminata utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-2}

Per aggiungere a un servizio un endpoint della cartella esaminata, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Impostate gli attributi endpoint cartella esaminata.
1. Specificate i valori di configurazione.
1. Definire i valori dei parametri di input.
1. Definire un valore di parametro di output.
1. Crea un endpoint cartella esaminata.
1. Abilitate l’endpoint.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per aggiungere a livello di programmazione un endpoint cartella esaminata, è necessario creare un oggetto `EndpointRegistryClient`.

**Imposta attributi endpoint cartella esaminata**

Per creare un endpoint della cartella esaminata per un servizio, specificate i seguenti valori:

* **Identificatore** del connettore: Specifica il tipo di endpoint creato. Per creare un endpoint cartella esaminata, specificate `WatchedFolder`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Identificatore** servizio: Specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint cartella esaminata al processo introdotto in questa sezione (un processo diventa un servizio quando attivato tramite Workbench), specificare `EncryptDocument`.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. In genere, durante la creazione di un endpoint di tipo cartella esaminata per un servizio originato da un processo creato in Workbench, il nome dell&#39;operazione è `invoke`.

**Specificare i valori di configurazione**

È necessario specificare i valori di configurazione per un endpoint di una cartella esaminata quando si aggiunge a livello di programmazione un endpoint di una cartella esaminata a un servizio. Questi valori di configurazione vengono specificati da un amministratore se un endpoint della cartella esaminata viene aggiunto utilizzando la console di amministrazione.

L&#39;elenco seguente specifica i valori di configurazione impostati durante l&#39;aggiunta a livello di programmazione di un endpoint di una cartella esaminata a un servizio:

* **url**: Specifica il percorso della cartella esaminata. In un ambiente cluster, questo valore deve puntare a una cartella di rete condivisa accessibile da ogni computer del cluster.
* **asincrono**: Identifica il tipo di chiamata come asincrono o sincrono. I processi transitori e sincroni possono essere invocati solo in modo sincrono. Il valore predefinito è true. È consigliabile l&#39;impostazione asincrona.
* **cronExpression**: Utilizzato da quarzo per pianificare il polling della directory di input. Per informazioni dettagliate sulla configurazione dell&#39;espressione cron, vedere [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html).
* **purgeDuration**: Si tratta di un attributo obbligatorio. I file e le cartelle nella cartella dei risultati vengono eliminati quando sono più vecchi di questo valore. Questo valore viene misurato in giorni. Questo attributo è utile per evitare che la cartella dei risultati diventi piena. Un valore pari a -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
* **repeatInterval**: L’intervallo, in secondi, per la scansione della cartella esaminata per l’input. A meno che non sia abilitata la limitazione, questo valore deve essere maggiore del tempo necessario per elaborare un processo medio; in caso contrario, il sistema potrebbe sovraccaricarsi. Il valore predefinito è 5.
* **repeatCount**: Il numero di volte in cui una cartella esaminata esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.
* **throttleOn**: Limita il numero di processi delle cartelle esaminate che possono essere elaborati in un dato momento. Il numero massimo di processi è determinato dal valore batchSize.
* **userName**: Nome utente utilizzato per richiamare un servizio di destinazione dalla cartella esaminata. Questo valore è obbligatorio. Il valore predefinito è SuperAdmin.
* **domainName**: Il dominio dell’utente. Questo valore è obbligatorio. Il valore predefinito è DefaultDom.
* **batchSize**: Numero di file o cartelle da raccogliere per scansione. utilizzare questo valore per evitare un sovraccarico del sistema; la scansione di troppi file alla volta può causare un arresto anomalo. Il valore predefinito è 2.
* **waitTime**: Tempo, in millisecondi, di attesa prima della scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 36.000.000 millisecondi (un&#39;ora) e il file è stato creato un minuto fa, questo file viene recuperato dopo che sono passati 59 o più minuti. Questo attributo è utile per garantire che un file o una cartella venga copiato completamente nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il file richiede dieci minuti per il download, impostare il tempo di attesa su 10&amp;ast;60 &amp;ast;1000 millisecondi. Questa impostazione impedisce alla cartella esaminata di eseguire la scansione del file se non è stato in attesa per dieci minuti. Il valore predefinito è 0.
* **excludeFilePattern**: Il pattern utilizzato da una cartella esaminata per determinare quali file e cartelle acquisire. I file o le cartelle con questo pattern non verranno analizzati per l&#39;elaborazione. Questa impostazione è utile quando l’input è una cartella che contiene più file. Il contenuto della cartella può essere copiato in una cartella con un nome che verrà scelto dalla cartella esaminata. Questo passaggio impedisce alla cartella esaminata di raccogliere una cartella da elaborare prima che la cartella venga completamente copiata nella cartella di input. Ad esempio, se il valore excludeFilePattern è `data*`, tutti i file e le cartelle che corrispondono a `data*` non vengono prelevati. Sono inclusi file e cartelle denominati `data1`, `data2` e così via. Inoltre, il pattern può essere completato con pattern di caratteri jolly per specificare i pattern di file. La cartella esaminata modifica l&#39;espressione regolare per supportare i pattern con caratteri jolly quali `*.*` e `*.pdf`. Questi pattern carattere jolly non sono supportati dalle espressioni regolari.
* **includeFilePattern**: Il pattern utilizzato dalla cartella esaminata per determinare quali cartelle e file acquisire e acquisire. Ad esempio, se questo valore è `*`, vengono prelevati tutti i file e le cartelle che corrispondono a `input*`. Sono inclusi file e cartelle denominati `input1`, `input2` e così via. Il valore predefinito è `*`. Questo valore indica tutti i file e le cartelle. Inoltre, il pattern può essere completato con pattern di caratteri jolly per specificare i pattern di file. La cartella esaminata modifica l&#39;espressione regolare per supportare i pattern con caratteri jolly quali `*.*` e `*.pdf`. Questi pattern carattere jolly non sono supportati dalle espressioni regolari. Questo valore è obbligatorio.
* **resultFolderName**: La cartella in cui sono memorizzati i risultati salvati. Questo percorso può essere assoluto o relativo. Se i risultati non vengono visualizzati in questa cartella, controllare la cartella degli errori. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Il valore predefinito è `result/%Y/%M/%D/`. Si tratta della cartella dei risultati all’interno della cartella esaminata.
* **preserveFolderName**: Posizione in cui vengono memorizzati i file dopo l&#39;esito positivo della scansione e del prelievo. Questa posizione può essere assoluta, relativa o null. Il valore predefinito è `preserve/%Y/%M/%D/`.
* **failureFolderName**: La cartella in cui vengono salvati i file di errore. Questo percorso è sempre relativo alla cartella esaminata. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Il valore predefinito è `failure/%Y/%M/%D/`.
* **preserveOnFailed**: Mantieni i file di input in caso di mancata esecuzione dell&#39;operazione su un servizio. Il valore predefinito è true.
* **overwriteDuplicateFilename**: Se è impostato su true, i file nella cartella dei risultati e nella cartella preserve vengono sovrascritti. Se è impostata su false, per il nome vengono utilizzati file e cartelle con un suffisso indice numerico. Il valore predefinito è false.

**Definire i valori dei parametri di input**

Quando si crea un endpoint della cartella esaminata, è necessario definire i valori dei parametri di input. È quindi necessario descrivere i valori di input passati all&#39;operazione richiamata dalla cartella esaminata. Ad esempio, prendete in considerazione il processo introdotto in questo argomento. Il valore immesso è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Quando create un endpoint della cartella esaminata per questo processo (dopo che un processo è stato attivato, diventa un servizio), dovete definire il valore del parametro di input.

Per definire i valori dei parametri di input richiesti per l’endpoint di una cartella esaminata, specificate i seguenti valori:

**Nome** del parametro di input: Nome del parametro di input. Il nome di un valore di input è specificato in Workbench per un processo. Se il valore di input appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di input è specificato nel file component.xml. Ad esempio, il nome del parametro di input per il processo introdotto in questa sezione è `InDoc`.

**Tipo** mapping: Utilizzato per configurare i valori di input necessari per richiamare l&#39;operazione del servizio. Esistono due tipi di mapping:

* `Literal`: L’endpoint Cartella osservata utilizza il valore immesso nel campo così come viene visualizzato. Sono supportati tutti i tipi Java di base. Ad esempio, se un&#39;API utilizza input quali String, long, int e Boolean, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.
* `Variable`: Il valore immesso è un pattern di file utilizzato dalla cartella esaminata per selezionare l&#39;input. Ad esempio, se si seleziona Variabile per il tipo di mappatura e il documento di input deve essere un file PDF, è possibile specificare `*.pdf`come valore di mappatura.

**Valore** mappatura: Specifica il valore del tipo di mappatura. Ad esempio, se si seleziona un tipo di mappatura `Variable`, è possibile specificare `*.pdf` come pattern di file.

**Tipo** di dati: Specifica il tipo di dati dei valori di input. Ad esempio, il tipo di dati del valore immesso del processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Definire un valore di parametro di output**

Quando create un endpoint cartella esaminata, dovete definire un valore di parametro di output. È quindi necessario descrivere il valore di output restituito dal servizio richiamato dall&#39;endpoint Cartella osservata. Ad esempio, prendete in considerazione il processo introdotto in questo argomento. Ha un valore di output denominato `SecuredDoc` e il relativo tipo di dati è `com.adobe.idp.Document`. Quando create un endpoint della cartella esaminata per questo processo (dopo che un processo è attivato, diventa un servizio), dovete definire il valore del parametro di output.

Per definire un valore del parametro di output richiesto per un endpoint di una cartella esaminata, specificate i seguenti valori:

**Nome** del parametro di output: Nome del parametro di output. Il nome di un valore di output del processo è specificato in Workbench. Se il valore di output appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di output è specificato nel file component.xml. Ad esempio, il nome del parametro di output per il processo introdotto in questa sezione è `SecuredDoc`.

**Tipo** mapping: Utilizzato per configurare l&#39;output del servizio e l&#39;operazione. Sono disponibili le seguenti opzioni:

* Se il servizio restituisce un singolo oggetto (un singolo documento), il pattern è `%F.pdf` e la destinazione di origine è sourcefilename.pdf. Ad esempio, il processo introdotto in questa sezione restituisce un singolo documento. Di conseguenza, il tipo di mappatura può essere definito come `%F.pdf` ( `%F` significa utilizzare il nome file specificato). Il pattern `%E` specifica l&#39;estensione del documento di input.
* Se il servizio restituisce un elenco, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se il servizio restituisce una mappa, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\file1 and Result\sourcefilename\file2. Se la mappa ha più di un oggetto, il pattern è `Result\%F.pdf` e la destinazione di origine è Result\sourcefilename1.pdf (output 1), Result\sourcefilenam2.pdf (output 2) e così via.

**Tipo** di dati: Specifica il tipo di dati del valore restituito. Ad esempio, il tipo di dati del valore restituito dal processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Creare un endpoint cartella esaminata**

Dopo aver impostato gli attributi dell’endpoint, i valori di configurazione e i valori dei parametri di input e output, dovete creare l’endpoint della cartella esaminata.

**Abilitare l&#39;endpoint**

Dopo aver creato un endpoint cartella esaminata, è necessario attivarlo. Quando l&#39;endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver attivato l’endpoint, potete visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiunta di un endpoint cartella esaminata tramite l&#39;API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiunta di un endpoint cartella esaminata tramite l&#39;API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Aggiungete un endpoint della cartella esaminata utilizzando l&#39;API Java di AEM Forms :

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostate gli attributi endpoint cartella esaminata.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specificare il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `WatchedFolder`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore di stringa che specifica il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. In genere, durante la creazione di un endpoint di tipo Cartella esaminata per un servizio originato da un processo creato in Workbench, viene richiamato il nome dell&#39;operazione.

1. Specificate i valori di configurazione.

   Per ogni valore di configurazione da impostare per l&#39;endpoint della cartella esaminata, è necessario richiamare il metodo `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText`. Ad esempio, per impostare il valore di configurazione `url`, richiamare il metodo `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e passare i seguenti valori stringa:

   * Un valore di stringa che specifica il nome del valore di configurazione. Quando si imposta il valore di configurazione `url`, specificare `url`.
   * Un valore di stringa che specifica il valore del valore di configurazione. Quando si imposta il valore di configurazione `url`, specificare il percorso della cartella esaminata.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori di configurazione impostati per il servizio EncryptDocument, vedere l&#39;esempio di codice Java disponibile in [QuickStart: Aggiunta di un endpoint cartella esaminata tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Definire i valori dei parametri di input.

   Definire un valore del parametro di input richiamando il metodo `setInputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Un valore di stringa che specifica il nome del parametro di input. Ad esempio, il nome del parametro di input per il servizio EncryptDocument è `InDoc`.
   * Una stringa che specifica il tipo di dati del parametro di input. Ad esempio, il tipo di dati del parametro di input `InDoc` è `com.adobe.idp.Document`.
   * Un valore di stringa che specifica il tipo di mapping. Ad esempio, è possibile specificare `variable`.
   * Un valore di stringa che specifica il valore del tipo di mappatura. Ad esempio, è possibile specificare &amp;ast;.pdf come pattern di file.

   >[!NOTE]
   >
   >Richiama il metodo `setInputParameterMapping` per ogni valore del parametro di input da definire. Poiché il processo EncryptDocument ha un solo parametro di input, è necessario richiamare questo metodo una volta.

1. Definire un valore di parametro di output.

   Definire un valore del parametro di output richiamando il metodo `setOutputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Un valore di stringa che specifica il nome del parametro di output. Ad esempio, il nome del parametro di output per il servizio EncryptDocument è `SecuredDoc`.
   * Una stringa che specifica il tipo di dati del parametro di output. Ad esempio, il tipo di dati del parametro di output `SecuredDoc` è `com.adobe.idp.Document`.
   * Un valore di stringa che specifica il tipo di mapping. Ad esempio, è possibile specificare `%F.pdf`.

1. Crea un endpoint cartella esaminata.

   Creare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta l&#39;endpoint cartella esaminata.

1. Abilitate l’endpoint.

   Abilitare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `enable` e passando l&#39;oggetto `Endpoint` restituito dal metodo `createEndpoint`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Aggiunta di un endpoint cartella esaminata tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### File costante dei valori di configurazione delle cartelle esaminate {#watched-folder-configuration-values-constant-file}

Avvio rapido di [avvio rapido: L&#39;aggiunta di un endpoint di cartelle esaminate tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utilizza un file costante che deve far parte del progetto Java per compilare il rapido avvio. Questo file costante rappresenta i valori di configurazione che devono essere impostati quando si aggiunge un endpoint cartella esaminata. Il seguente codice Java rappresenta il file costante.

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

Puoi aggiungere un endpoint e-mail a un servizio a livello di programmazione utilizzando l&#39;API Java di AEM Forms . Aggiungendo un endpoint e-mail, gli utenti possono inviare un messaggio e-mail contenente uno o più file allegati a un account e-mail specificato. Quindi, viene richiamata l’operazione di configurazione del servizio e vengono modificati i file. Dopo che il servizio ha eseguito l&#39;operazione specificata, invia un messaggio e-mail al mittente con i file modificati come allegati di file.

Ai fini dell&#39;aggiunta programmatica di un endpoint e-mail a un servizio, tenere in considerazione il seguente processo di breve durata denominato *MyApplication\EncryptDocument*. Per informazioni sui processi di breve durata, vedere [Informazioni  processi AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Questo processo accetta un documento PDF non protetto come valore di input, quindi passa il documento PDF non protetto all&#39;operazione `EncryptPDFUsingPassword` del servizio di cifratura. In questo modo il documento PDF viene crittografato con una password e il documento PDF crittografato con password viene restituito come valore di output. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

>[!NOTE]
>
>Non potete aggiungere un endpoint e-mail utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per aggiungere un endpoint e-mail a un servizio, eseguite le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Impostate gli attributi dell’endpoint e-mail.
1. Specificate i valori di configurazione.
1. Definire i valori dei parametri di input.
1. Definire un valore di parametro di output.
1. Create l’endpoint e-mail.
1. Abilitate l’endpoint.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Prima di poter aggiungere un endpoint e-mail a livello di programmazione, è necessario creare un oggetto `EndpointRegistryClient`.

**Impostare gli attributi dell’endpoint e-mail**

Per creare un endpoint e-mail per un servizio, specificate i seguenti valori:

* **Valore** identificatore connettore: Specifica il tipo di endpoint creato. Per creare un endpoint e-mail, specificate `Email`.
* **Descrizione**: Specifica una descrizione per l&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Valore** ID servizio: Specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint e-mail al processo introdotto in questa sezione (un processo diventa un servizio quando attivato tramite Workbench), specificare `EncryptDocument`.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. In genere, durante la creazione di un endpoint e-mail per un servizio originato da un processo creato in Workbench, il nome dell&#39;operazione è `invoke`.

**Specificare i valori di configurazione**

È necessario specificare i valori di configurazione per un endpoint e-mail quando si aggiunge programmaticamente un endpoint e-mail a un servizio. Questi valori di configurazione vengono specificati da un amministratore se un endpoint e-mail viene aggiunto utilizzando la console di amministrazione.

>[!NOTE]
>
>L&#39;account e-mail monitorato è un account speciale utilizzato solo per l&#39;endpoint e-mail. Questo account non è un account e-mail di un utente normale. Un account e-mail di un utente normale non deve essere configurato come account utilizzato dal provider e-mail, perché il provider e-mail elimina i messaggi e-mail dalla inbox al termine dei messaggi.

I seguenti valori di configurazione vengono impostati quando si aggiunge a livello di programmazione un endpoint e-mail a un servizio:

* **cronExpression**: Un&#39;espressione cron se l&#39;e-mail deve essere pianificata utilizzando un&#39;espressione cron.
* **repeatCount**: Numero di volte in cui l’endpoint e-mail esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.
* **repeatInterval**: Frequenza di scansione in secondi utilizzata dal ricevitore per verificare la posta in arrivo. Il valore predefinito è 10.
* **startDelay**: Tempo di attesa per l&#39;analisi dopo l&#39;avvio del pianificatore. Il valore predefinito è 0.
* **batchSize**: Il numero di messaggi e-mail che il ricevitore elabora per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.
* **userName**: Nome utente utilizzato per richiamare un servizio di destinazione dall’e-mail. Il valore predefinito è `SuperAdmin`.
* **domainName**: Un valore di configurazione obbligatorio. Il valore predefinito è `DefaultDom`.
* **domainPattern**: Specifica i pattern di dominio dell&#39;e-mail in arrivo che il provider accetta. Ad esempio, se si utilizza `adobe.com`, vengono elaborati solo i messaggi e-mail provenienti da adobe.com, mentre quelli provenienti da altri domini vengono ignorati.
* **filePattern**: Specifica i pattern di allegati che il provider accetta. Questo include file con estensioni di nomi file specifiche (&amp;ast;.dat, &amp;ast;.xml), file con nomi specifici (dati) e file con espressioni composite nel nome e nell&#39;estensione (&amp;ast;.[dD][aA]&#39;port&#39;). Il valore predefinito è `*`.
* **receiveSuccfulJob**: Indirizzo e-mail cui vengono inviati i messaggi per indicare l’esito positivo dei processi. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di processo riuscito. Se digitate `sender`, i risultati dell&#39;e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specificate altri destinatari con indirizzi e-mail, separati da una virgola. Per disattivare questa opzione, lasciate vuoto questo valore. In alcuni casi, potrebbe essere utile attivare un processo e non si desidera inviare una notifica via e-mail del risultato. Il valore predefinito è `sender`.
* **receiveFailedJob**: Indirizzo e-mail cui vengono inviati i messaggi per indicare che i processi non sono riusciti. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di processo non riuscito. Se digitate `sender`, i risultati dell&#39;e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specificate altri destinatari con indirizzi e-mail, separati da una virgola. Per disattivare questa opzione, lasciate vuoto questo valore. Il valore predefinito è `sender`.
* **inboxHost**: Il nome host della inbox o l&#39;indirizzo IP per il provider di posta elettronica da analizzare.
* **inboxPort**: La porta utilizzata dal server e-mail. Il valore predefinito per POP3 è 110 e il valore predefinito per IMAP è 143. Se SSL è abilitato, il valore predefinito per POP3 è 995 e il valore predefinito per IMAP è 993.
* **inboxProtocol**: Il protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della inbox. Le opzioni sono `IMAP` o `POP3`. Il server di posta elettronica dell&#39;host della inbox deve supportare questi protocolli.
* **inboxTimeOut**: Timeout in secondi per il provider di posta elettronica di attendere le risposte della inbox. Il valore predefinito è 60.
* **inboxUser**: Nome utente necessario per accedere all’account e-mail. A seconda del server e-mail e della configurazione, questa potrebbe essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.
* **inboxPassword**: La password per l’utente della inbox.
* **inboxSSLEnabled**: Impostate questo valore per obbligare il provider di posta elettronica a utilizzare SSL per inviare messaggi di notifica di risultati o errori. Assicurarsi che l&#39;host IMAP o POP3 supporti SSL.
* **smtpHost**: Il nome host del server di posta elettronica a cui il provider invia i risultati e i messaggi di errore.
* **smtpPort**: Il valore predefinito per la porta SMTP è 25.
* **smtpUser**: L’account utente del provider di posta elettronica da utilizzare per l’invio di notifiche e-mail di risultati ed errori.
* **smtpPassword**: La password dell&#39;account SMTP. Alcuni server di posta elettronica non richiedono una password SMTP.
* **charSet**: Set di caratteri utilizzato dal provider di posta elettronica. Il valore predefinito è `UTF-8`.
* **smtpSSLEnabled**: Impostate questo valore per obbligare il provider di posta elettronica a utilizzare SSL per inviare messaggi di notifica di risultati o errori. Verificate che l&#39;host SMTP supporti SSL.
* **failJobFolder**: Specifica una directory in cui memorizzare i risultati quando il server di posta SMTP non è operativo.
* **asincrono**: Quando è impostato su sincrono, tutti i documenti di input vengono elaborati e viene restituita una sola risposta. Se impostato su asincrono, viene inviata una risposta per ciascun documento di input elaborato. Ad esempio, viene creato un endpoint e-mail per il processo introdotto in questo argomento e viene inviato un messaggio e-mail alla inbox dell&#39;endpoint che contiene più documenti PDF non protetti. Quando tutti i documenti PDF sono crittografati con una password e se l&#39;endpoint è configurato come sincrono, viene inviato un singolo messaggio e-mail di risposta con tutti i documenti PDF protetti collegati. Se l&#39;endpoint è configurato come asincrono, viene inviato un messaggio e-mail di risposta separato per ciascun documento PDF protetto. Ciascun messaggio e-mail contiene un singolo documento PDF come allegato. Il valore predefinito è asincrono.

**Definire i valori dei parametri di input**

Quando create un endpoint e-mail, dovete definire i valori dei parametri di input. In altre parole, devi descrivere i valori di input passati all&#39;operazione richiamata dall&#39;endpoint e-mail. Ad esempio, prendete in considerazione il processo introdotto in questo argomento. Il valore immesso è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Quando create un endpoint e-mail per questo processo (dopo che un processo viene attivato, diventa un servizio), dovete definire il valore del parametro di input.

Per definire i valori dei parametri di input richiesti per un endpoint e-mail, specificate i seguenti valori:

**Nome** del parametro di input: Nome del parametro di input. Il nome di un valore di input è specificato in Workbench per un processo. Se il valore di input appartiene a un&#39;operazione di servizio (un servizio Forms che non è un processo creato in Workbench), il nome di input è specificato nel file component.xml. Ad esempio, il nome del parametro di input per il processo introdotto in questa sezione è `InDoc`.

**Tipo** mapping: Utilizzato per configurare i valori di input necessari per richiamare l&#39;operazione del servizio. Due tipi di mapping sono i seguenti:

* `Literal`: L&#39;endpoint e-mail utilizza il valore immesso nel campo così come viene visualizzato. Sono supportati tutti i tipi Java di base. Ad esempio, se un&#39;API utilizza input quali String, long, int e Boolean, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.
* `Variable`: Il valore immesso è un pattern di file utilizzato dall&#39;endpoint e-mail per selezionare l&#39;input. Ad esempio, se si seleziona Variabile per il tipo di mappatura e il documento di input deve essere un file PDF, è possibile specificare `*.pdf` come valore di mappatura.

**Valore** mappatura: Specifica il valore del tipo di mappatura. Ad esempio, se si seleziona un tipo di mappatura della variabile, è possibile specificare `*.pdf` come pattern di file.

**Tipo** di dati: Specifica il tipo di dati dei valori di input. Ad esempio, il tipo di dati del valore di input del processo introdotto in questa sezione è com.adobe.idp.Document.

**Definire un valore di parametro di output**

Quando create un endpoint e-mail, dovete definire un valore di parametro di output. Ovvero, devi descrivere il valore di output restituito dal servizio richiamato dall&#39;endpoint e-mail. Ad esempio, prendete in considerazione il processo introdotto in questo argomento. Ha un valore di output denominato `SecuredDoc` e il relativo tipo di dati è `com.adobe.idp.Document`. Quando create un endpoint e-mail per questo processo (dopo che un processo viene attivato, diventa un servizio), dovete definire il valore del parametro di output.

Per definire un valore del parametro di output richiesto per un endpoint e-mail, specificate i seguenti valori:

**Nome** del parametro di output: Nome del parametro di output. Il nome di un valore di output del processo è specificato in Workbench. Se il valore di output appartiene a un&#39;operazione di servizio (un servizio che non è un processo creato in Workbench), il nome di output è specificato nel file component.xml. Ad esempio, il nome del parametro di output per il processo introdotto in questa sezione è `SecuredDoc`.

**Tipo** mapping: Utilizzato per configurare l&#39;output del servizio e l&#39;operazione. Sono disponibili le seguenti opzioni:

* Se il servizio restituisce un singolo oggetto (un singolo documento), il pattern è `%F.pdf` e la destinazione di origine è sourcefilename.pdf. Ad esempio, il processo introdotto in questa sezione restituisce un singolo documento. Di conseguenza, il tipo di mappatura può essere definito come `%F.pdf` ( `%F` significa utilizzare il nome file specificato). Il pattern `%E` specifica l&#39;estensione del documento di input.
* Se il servizio restituisce un elenco, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se il servizio restituisce una mappa, il pattern è `Result\%F\` e la destinazione di origine è Result\sourcefilename\file1 and Result\sourcefilename\file2. Se la mappa ha più di un oggetto, il pattern è `Result\%F.pdf` e la destinazione di origine è Result\sourcefilename1.pdf (output 1), Result\sourcefilenam2.pdf (output 2) e così via.

**Tipo** di dati: Specifica il tipo di dati del valore restituito. Ad esempio, il tipo di dati del valore restituito dal processo introdotto in questa sezione è `com.adobe.idp.Document`.

**Creare l’endpoint e-mail**

Dopo aver impostato gli attributi dell’endpoint e i valori di configurazione e aver definito i valori dei parametri di input e output, dovete creare l’endpoint e-mail.

**Abilitare l&#39;endpoint**

Dopo aver creato un endpoint e-mail, è necessario attivarlo. Quando l&#39;endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver attivato l’endpoint, potete visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiunta di un endpoint e-mail tramite l&#39;API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiunta di un endpoint e-mail mediante l&#39;API Java {#add-an-email-endpoint-using-the-java-api}

Aggiungete un endpoint e-mail utilizzando l&#39;API Java:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostate gli attributi dell’endpoint e-mail.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specificare il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `Email`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore di stringa che specifica il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. In genere, quando si crea un endpoint e-mail per un servizio originato da un processo creato in Workbench, viene richiamato il nome dell&#39;operazione.

1. Specificate i valori di configurazione.

   Per ogni valore di configurazione da impostare per l&#39;endpoint e-mail, è necessario richiamare il metodo `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText`. Ad esempio, per impostare il valore di configurazione `smtpHost`, richiamare il metodo `CreateEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e passare i seguenti valori:

   * Un valore di stringa che specifica il nome del valore di configurazione. Quando si imposta il valore di configurazione `smtpHost`, specificare `smtpHost`.
   * Un valore di stringa che specifica il valore del valore di configurazione. Quando si imposta il valore di configurazione `smtpHost`, specificare un valore di stringa che specifica il nome del server SMTP.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori di configurazione impostati per il servizio EncryptDocument introdotto in questa sezione, vedere l&#39;esempio di codice Java disponibile in [QuickStart: Aggiunta di un endpoint e-mail mediante l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Definire i valori dei parametri di input.

   Definire un valore del parametro di input richiamando il metodo `setInputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Un valore di stringa che specifica il nome del parametro di input. Ad esempio, il nome del parametro di input per il servizio EncryptDocument è `InDoc`.
   * Una stringa che specifica il tipo di dati del parametro di input. Ad esempio, il tipo di dati del parametro di input `InDoc` è `com.adobe.idp.Document`.
   * Un valore di stringa che specifica il tipo di mapping. Ad esempio, è possibile specificare `variable`.
   * Un valore di stringa che specifica il valore del tipo di mappatura. Ad esempio, è possibile specificare &amp;ast;.pdf come pattern di file.

   >[!NOTE]
   >
   >Richiama il metodo `setInputParameterMapping` per ogni valore del parametro di input da definire. Poiché il processo EncryptDocument ha un solo parametro di input, è necessario richiamare questo metodo una volta.

1. Definire un valore di parametro di output.

   Definire un valore del parametro di output richiamando il metodo `setOutputParameterMapping` dell&#39;oggetto `CreateEndpointInfo` e passando i seguenti valori:

   * Un valore di stringa che specifica il nome del parametro di output. Ad esempio, il nome del parametro di output per il servizio EncryptDocument è `SecuredDoc`.
   * Una stringa che specifica il tipo di dati del parametro di output. Ad esempio, il tipo di dati del parametro di output `SecuredDoc` è `com.adobe.idp.Document`.
   * Un valore di stringa che specifica il tipo di mapping. Ad esempio, è possibile specificare `%F.pdf`.

1. Create l’endpoint e-mail.

   Creare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta l&#39;endpoint e-mail.

1. Abilitate l’endpoint.

   Abilitare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `enable` e passando l&#39;oggetto `Endpoint` restituito dal metodo `createEndpoint`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Aggiunta di un endpoint cartella esaminata tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### File costante valori di configurazione e-mail {#email-configuration-values-constant-file}

Avvio rapido di [avvio rapido: L&#39;aggiunta di un endpoint e-mail tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) utilizza un file costante che deve far parte del progetto Java per compilare il rapido avvio. Questo file costante rappresenta i valori di configurazione che devono essere impostati quando si aggiunge un endpoint e-mail. Il seguente codice Java rappresenta il file costante.

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

Puoi aggiungere un endpoint remoto a un servizio a livello di programmazione utilizzando l&#39;API Java di AEM Forms . Aggiungendo un endpoint remoto, si sta abilitando un&#39;applicazione Flex per richiamare il servizio utilizzando la rimozione. (Vedere [Chiamata  AEM Forms tramite (obsoleto per AEM moduli)  AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Ai fini dell&#39;aggiunta programmatica di un endpoint Remoting a un servizio, tenere in considerazione il seguente processo di breve durata denominato *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Questo processo accetta un documento PDF non protetto come valore di input, quindi passa il documento PDF non protetto all&#39;operazione `EncryptPDFUsingPassword` del servizio di cifratura. Il documento PDF è crittografato con una password e il documento PDF crittografato con password è il valore di output di questo processo. Il nome del valore di input (il documento PDF non protetto) è `InDoc` e il tipo di dati è `com.adobe.idp.Document`. Il nome del valore di output (il documento PDF con password) è `SecuredDoc` e il tipo di dati è `com.adobe.idp.Document`.

Per dimostrare come aggiungere un endpoint remoto a un servizio, in questa sezione viene aggiunto un endpoint remoto a un servizio denominato EncryptDocument.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint remoto utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-4}

Per rimuovere un endpoint da un servizio, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Impostate gli attributi dell&#39;endpoint remoto.
1. Creare un endpoint remoto.
1. Abilitate l’endpoint.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per aggiungere un endpoint remoto a livello di programmazione, è necessario creare un oggetto `EndpointRegistryClient`.

**Impostazione degli attributi endpoint remoto**

Per creare un endpoint remoto per un servizio, specificate i seguenti valori:

* **Valore** identificatore connettore: Specifica il tipo di endpoint creato. Per creare un endpoint remoto, specificare `Remoting`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Valore** ID servizio: Specifica il servizio a cui appartiene l&#39;endpoint. Ad esempio, per aggiungere un endpoint remoto al processo introdotto in questa sezione (un processo diventa un servizio quando viene attivato in Workbench), specificare `EncryptDocument`.
* **Nome** operazione: Specifica il nome dell&#39;operazione richiamata utilizzando l&#39;endpoint. Quando create un endpoint remoto, specificate un carattere jolly (&amp;ast;).

**Creare un endpoint remoto**

Dopo aver impostato gli attributi dell&#39;endpoint remoto, potete creare un endpoint remoto per un servizio.

**Abilitare l&#39;endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando un endpoint remoto è abilitato, consente a un client Flex di richiamare il servizio.

**Consulta anche**

[Aggiunta di un endpoint remoto tramite l&#39;API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere un endpoint remoto utilizzando l&#39;API Java {#add-a-remoting-endpoint-using-the-java-api}

Aggiungete un endpoint remoto utilizzando l&#39;API Java:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostate gli attributi dell&#39;endpoint remoto.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specificare il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `Remoting`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore di stringa che specifica il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome del servizio.
   * Specificare l&#39;operazione richiamata dal metodo `CreateEndpointInfo` dell&#39;oggetto `setOperationName` e passare un valore di stringa che specifica il nome dell&#39;operazione. Per un endpoint remoto, specificate un carattere jolly (&amp;ast;).

1. Creare un endpoint remoto.

   Creare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint remoto.

1. Abilitate l’endpoint.

   Abilitare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `enable` e passando l&#39;oggetto `Endpoint` restituito dal metodo `createEndpoint`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Aggiunta di un endpoint remoto tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Aggiunta di endpoint TaskManager {#adding-taskmanager-endpoints}

È possibile aggiungere a livello di programmazione un endpoint TaskManager a un servizio utilizzando l&#39;API Java AEM Forms . Aggiungendo un endpoint di TaskManager a un servizio, l&#39;utente di Workspace può richiamare il servizio. In altre parole, un utente che lavora in Workspace può richiamare un processo con un endpoint TaskManager corrispondente.

>[!NOTE]
>
>Non è possibile aggiungere un endpoint TaskManager utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-5}

Per aggiungere un endpoint TaskManager a un servizio, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Create una categoria per l&#39;endpoint.
1. Impostate gli attributi endpoint TaskManager.
1. Creare un endpoint TaskManager.
1. Abilitate l’endpoint.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Prima di poter aggiungere un endpoint TaskManager a livello di programmazione, è necessario creare un oggetto `EndpointRegistryClient`.

**Creare una categoria per l&#39;endpoint**

Le categorie vengono utilizzate per organizzare i servizi all&#39;interno di Workspace. In altre parole, un utente di Workspace può richiamare un servizio che dispone di un endpoint TaskManager selezionando una categoria all&#39;interno di Workspace. Quando si crea un endpoint TaskManager, è possibile fare riferimento a una categoria esistente o creare una nuova categoria a livello di programmazione.

>[!NOTE]
>
>Questa sezione crea una nuova categoria come parte dell&#39;aggiunta di un endpoint TaskManager a un servizio.

**Imposta attributi endpoint TaskManager**

Per creare un endpoint TaskManager per un servizio, specificare i valori seguenti:

* **Identificatore** del connettore: Specifica il tipo di endpoint creato. Per creare un endpoint TaskManager, specificare `TaskManagerConnector`.
* **Descrizione**: Specifica la descrizione dell&#39;endpoint.
* **Nome**: Specifica il nome dell&#39;endpoint.
* **Identificatore** servizio: Specifica il servizio a cui appartiene l&#39;endpoint.
* **Categoria**: Specifica un valore di identificatore di categoria associato all&#39;endpoint TaskManager.
* **Nome** operazione: In genere, durante la creazione di un endpoint TaskManager per un servizio originato da un processo creato in Workbench, il nome dell&#39;operazione è  `invoke`.

**Creare un endpoint TaskManager**

Dopo aver impostato gli attributi endpoint TaskManager, è possibile creare un endpoint TaskManager per un servizio.

**Abilitare l&#39;endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l’endpoint è abilitato, può essere utilizzato per richiamare il servizio dall’interno di Workspace. Dopo aver attivato l’endpoint, potete visualizzarlo nella console di amministrazione.

**Consulta anche**

[Aggiunta di un endpoint TaskManager tramite l&#39;API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere un endpoint TaskManager utilizzando l&#39;API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Aggiungete un endpoint TaskManager utilizzando l&#39;API Java:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Create una categoria per l&#39;endpoint.

   * Creare un oggetto `CreateEndpointCategoryInfo` utilizzando il relativo costruttore e passando i seguenti valori:

      * Un valore di stringa che specifica il valore di identificatore della categoria
      * Un valore di stringa che specifica la descrizione della categoria
   * Creare la categoria richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `createEndpointCategory` e passando l&#39;oggetto `CreateEndpointCategoryInfo`. Questo metodo restituisce un oggetto `EndpointCategory` che rappresenta la nuova categoria.


1. Impostate gli attributi endpoint TaskManager.

   * Creare un oggetto `CreateEndpointInfo` utilizzando il relativo costruttore.
   * Specificare il valore dell&#39;identificatore del connettore richiamando il metodo `setConnectorId` dell&#39;oggetto `CreateEndpointInfo` e passando il valore della stringa `TaskManagerConnector`.
   * Specificare la descrizione dell&#39;endpoint richiamando il metodo `setDescription` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che descrive l&#39;endpoint.
   * Specificare il nome dell&#39;endpoint richiamando il metodo `CreateEndpointInfo` dell&#39;oggetto `setName` e passando un valore di stringa che specifica il nome.
   * Specificare il servizio a cui appartiene l&#39;endpoint richiamando il metodo `setServiceId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome del servizio.
   * Specificare la categoria a cui appartiene l&#39;endpoint richiamando il metodo `setCategoryId` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il valore dell&#39;identificatore della categoria. È possibile richiamare il metodo `EndpointCategory` dell&#39;oggetto `getId` per ottenere il valore dell&#39;identificatore di questa categoria.
   * Specificare l&#39;operazione richiamata richiamando il metodo `setOperationName` dell&#39;oggetto `CreateEndpointInfo` e passando un valore di stringa che specifica il nome dell&#39;operazione. In genere, durante la creazione di un endpoint `TaskManager` per un servizio originato da un processo creato in Workbench, il nome dell&#39;operazione è `invoke`.

1. Creare un endpoint TaskManager.

   Creare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `createEndpoint` e passando l&#39;oggetto `CreateEndpointInfo`. Questo metodo restituisce un oggetto `Endpoint` che rappresenta il nuovo endpoint TaskManager.

1. Abilitate l’endpoint.

   Abilitare l&#39;endpoint richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `enable` e passando l&#39;oggetto `Endpoint` restituito dal metodo `createEndpoint`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Aggiunta di un endpoint TaskManager tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modifica di endpoint {#modifying-endpoints}

Potete modificare a livello di programmazione un endpoint esistente utilizzando l&#39;API Java di AEM Forms . Modificando un endpoint, potete modificare il comportamento dell&#39;endpoint. Considerate, ad esempio, un endpoint cartella esaminata che specifica una cartella utilizzata come cartella esaminata. È possibile modificare a livello di programmazione i valori di configurazione che appartengono all’endpoint della cartella esaminata, in modo che un’altra cartella funzioni come cartella esaminata. Per informazioni sui valori di configurazione che appartengono a un endpoint di una cartella esaminata, vedere [Aggiunta di endpoint cartella esaminata](programmatically-endpoints.md#adding-watched-folder-endpoints).

Per dimostrare come modificare un endpoint, in questa sezione viene modificato un endpoint cartella esaminata modificando la cartella che si comporta come cartella esaminata.

>[!NOTE]
>
>Non è possibile modificare un endpoint utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-6}

Per modificare un endpoint, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Recuperate l’endpoint.
1. Specificate nuovi valori di configurazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per modificare un endpoint a livello di programmazione, è necessario creare un oggetto `EndpointRegistryClient`.

**Recuperare l’endpoint da modificare**

Prima di poter modificare un endpoint, è necessario recuperarlo. Per recuperare un endpoint, è necessario connettersi come utente che può accedere a un endpoint. È consigliabile connettersi come amministratore. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

È possibile recuperare un endpoint recuperando un elenco di endpoint. Potete quindi eseguire un&#39;iterazione nell&#39;elenco, cercando l&#39;endpoint specifico da rimuovere. Ad esempio, potete individuare un endpoint determinando il servizio che corrisponde all&#39;endpoint e il tipo di endpoint. Quando si individua l’endpoint, è possibile modificarlo.

**Specificare nuovi valori di configurazione**

Quando modificate un endpoint, specificate nuovi valori di configurazione. Ad esempio, per modificare un endpoint cartella esaminata, reimpostare tutti i valori di configurazione dell&#39;endpoint cartella esaminata, non solo quelli che si desidera modificare. Per informazioni sui valori di configurazione che appartengono a un endpoint di una cartella esaminata, vedere [Aggiunta di endpoint cartella esaminata](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Per informazioni sui valori di configurazione che appartengono a un endpoint e-mail, vedere [Aggiunta di endpoint e-mail](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Non è possibile modificare il servizio richiamato dall&#39;endpoint. Se tentate di modificare il servizio, viene generata un&#39;eccezione. Per modificare il servizio associato a un determinato endpoint, rimuovete l&#39;endpoint e createne uno nuovo. (Vedere [Rimozione di endpoint](programmatically-endpoints.md#removing-endpoints).)

**Consulta anche**

[Modifica di un endpoint tramite l&#39;API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modifica di un endpoint utilizzando l&#39;API Java {#modifying-an-endpoint-using-the-java-api}

Modificate un endpoint utilizzando l&#39;API Java:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperate l’endpoint da modificare.

   * Recuperare un elenco di tutti gli endpoint a cui l&#39;utente corrente (specificato nelle proprietà di connessione) può accedere richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `getEndpoints` e passando un oggetto `PagingFilter` che funge da filtro. Potete passare un valore `(PagingFilter)null` per restituire tutti gli endpoint. Questo metodo restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `Endpoint`. Per informazioni su un oggetto `PagingFilter`, vedere [ AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Iterate l&#39;oggetto `java.util.List` per determinare se contiene endpoint. Se esistono endpoint, ogni elemento è un&#39;istanza `EndPoint`.
   * Determinare il servizio che corrisponde a un endpoint richiamando il metodo `EndPoint` dell&#39;oggetto `getServiceId`. Questo metodo restituisce un valore di stringa che specifica il nome del servizio.
   * Determinare il tipo di endpoint richiamando il metodo `EndPoint` dell&#39;oggetto `getConnectorId`. Questo metodo restituisce un valore di stringa che specifica il tipo di endpoint. Ad esempio, se l&#39;endpoint è un endpoint cartella esaminata, questo metodo restituisce `WatchedFolder`.

1. Specificate nuovi valori di configurazione.

   * Creare un oggetto `ModifyEndpointInfo` richiamandone il costruttore.
   * Per ogni valore di configurazione da impostare, richiamare il metodo `ModifyEndpointInfo` dell&#39;oggetto `setConfigParameterAsText`. Ad esempio, per impostare il valore di configurazione dell&#39;URL, richiamare il metodo `ModifyEndpointInfo` dell&#39;oggetto `setConfigParameterAsText` e passare i seguenti valori:

      * Un valore di stringa che specifica il nome del valore di configurazione. Ad esempio, per impostare il valore di configurazione `url`, specificare `url`.
      * Un valore di stringa che specifica il valore del valore di configurazione. Per definire un valore per il valore di configurazione `url`, specificate il percorso della cartella esaminata.
   * Richiamare il metodo `EndpointRegistryClient` dell&#39;oggetto `modifyEndpoint` e passare l&#39;oggetto `ModifyEndpointInfo`.


**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Modifica di un endpoint tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rimozione di endpoint {#removing-endpoints}

Puoi rimuovere programmaticamente un endpoint da un servizio utilizzando l&#39;API Java di AEM Forms . Dopo aver rimosso un endpoint, il servizio non può essere invocato utilizzando il metodo di chiamata abilitato dall&#39;endpoint. Ad esempio, se si rimuove un endpoint SOAP da un servizio, non è possibile richiamare il servizio utilizzando la modalità SOAP.

Per dimostrare come rimuovere un endpoint da un servizio, questa sezione rimuove un endpoint EJB da un servizio denominato *EncryptDocument*.

>[!NOTE]
>
>Non è possibile rimuovere un endpoint utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-7}

Per rimuovere un endpoint da un servizio, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `EndpointRegistryClient`.
1. Recuperate l’endpoint.
1. Rimuovere l&#39;endpoint.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client EndpointRegistry**

Per rimuovere un endpoint a livello di programmazione, è necessario creare un oggetto `EndpointRegistryClient`.

**Recuperare l’endpoint da rimuovere**

Prima di rimuovere un endpoint, è necessario recuperarlo. Per recuperare un endpoint, è necessario connettersi come utente che può accedere a un endpoint. È consigliabile connettersi come amministratore. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

È possibile recuperare un endpoint recuperando un elenco di endpoint. Potete quindi eseguire un&#39;iterazione nell&#39;elenco, cercando l&#39;endpoint specifico da rimuovere. Ad esempio, potete individuare un endpoint determinando il servizio che corrisponde all&#39;endpoint e il tipo di endpoint. Quando individuate l’endpoint, potete rimuoverlo.

**Rimuovere l&#39;endpoint**

Dopo aver creato un nuovo endpoint, è necessario abilitarlo. Quando l&#39;endpoint è abilitato, può essere utilizzato per richiamare il servizio. Dopo aver attivato l’endpoint, potete visualizzarlo nella console di amministrazione.

**Consulta anche**

[Rimozione di un endpoint tramite l&#39;API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimozione di un endpoint utilizzando l&#39;API Java {#removing-an-endpoint-using-the-java-api}

Rimuovete un endpoint utilizzando l&#39;API Java:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client EndpointRegistry.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EndpointRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperate l’endpoint da rimuovere.

   * Recuperare un elenco di tutti gli endpoint a cui l&#39;utente corrente (specificato nelle proprietà di connessione) ha accesso richiamando il metodo `EndpointRegistryClient` dell&#39;oggetto `getEndpoints` e passando un oggetto `PagingFilter` che funge da filtro. Potete passare `(PagingFilter)null` per restituire tutti gli endpoint. Questo metodo restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `Endpoint`.
   * Iterate l&#39;oggetto `java.util.List` per determinare se contiene endpoint. Se esistono endpoint, ogni elemento è un&#39;istanza `EndPoint`.
   * Determinare il servizio che corrisponde a un endpoint richiamando il metodo `EndPoint` dell&#39;oggetto `getServiceId`. Questo metodo restituisce un valore di stringa che specifica il nome del servizio.
   * Determinare il tipo di endpoint richiamando il metodo `EndPoint` dell&#39;oggetto `getConnectorId`. Questo metodo restituisce un valore di stringa che specifica il tipo di endpoint. Ad esempio, se l&#39;endpoint è un endpoint EJB, questo metodo restituisce `EJB`.

1. Rimuovere l&#39;endpoint.

   Rimuovere l&#39;endpoint richiamando il metodo `remove` dell&#39;oggetto `EndpointRegistryClient` e passando l&#39;oggetto `EndPoint` che rappresenta l&#39;endpoint da rimuovere.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Rimozione di un endpoint tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recupero delle informazioni sul connettore endpoint {#retrieving-endpoint-connector-information}

Potete recuperare informazioni sui connettori endpoint a livello di programmazione utilizzando l&#39;API AEM Forms . Un connettore consente a un endpoint di richiamare un servizio utilizzando vari metodi di chiamata. Ad esempio, un connettore per cartelle esaminate consente a un endpoint di richiamare un servizio utilizzando le cartelle esaminate. Tramite il recupero programmatico delle informazioni sui connettori endpoint, è possibile recuperare i valori di configurazione associati a un connettore, ad esempio quali valori di configurazione sono obbligatori e quali facoltativi.

Per dimostrare come recuperare informazioni sui connettori endpoint, questa sezione recupera informazioni su un connettore per cartelle esaminate. (Vedere [Aggiunta di endpoint cartella osservata](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Non è possibile recuperare informazioni sugli endpoint utilizzando i servizi Web.

>[!NOTE]
>
>In questo argomento viene utilizzata l&#39;API `ConnectorRegistryClient` per recuperare informazioni sui connettori endpoint. (Vedere [ AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Riepilogo dei passaggi {#summary_of_steps-8}

Per recuperare le informazioni sul connettore endpoint, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto `ConnectorRegistryClient`.
1. Specificare il tipo di connettore.
1. Recuperare i valori di configurazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Se  AEM Forms è distribuito su un server applicazione J2EE supportato che non è JBoss, sostituite adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazione J2EE in cui  AEM Forms è distribuito. Per informazioni sulla posizione di tutti  file AEM Forms JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto ConnectorRegistry Client**

Per recuperare le informazioni sul connettore dell&#39;endpoint a livello di programmazione, creare un oggetto `ConnectorRegistryClient`.

**Specificare il tipo di connettore**

Specificare il tipo di connettore da cui recuperare le informazioni. Esistono i seguenti tipi di connettori:

* **EJB**: Consente a un&#39;applicazione client di richiamare un servizio utilizzando la modalità EJB.
* **SOAP**: Abilita un&#39;applicazione client a richiamare un servizio utilizzando la modalità SOAP.
* **Cartella** esaminata: Consente alle cartelle esaminate di richiamare un servizio.
* **E-mail**: Consente ai messaggi e-mail di richiamare un servizio.
* **Remoto**: Abilita un&#39;applicazione client Flex a richiamare un servizio.
* **TaskManagerConnector**: Consente a un utente di Workspace di richiamare un servizio dall’interno di Workspace.

**Recuperare i valori di configurazione**

Dopo aver specificato il tipo di connettore, è possibile recuperare informazioni sul connettore, ad esempio il valore di configurazione supportato. Ad esempio, per qualsiasi connettore, è possibile determinare quali valori di configurazione sono obbligatori e quali sono facoltativi.

**Consulta anche**

[Recuperare le informazioni sul connettore dell&#39;endpoint utilizzando l&#39;API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare le informazioni sul connettore endpoint utilizzando l&#39;API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recuperate le informazioni sul connettore endpoint utilizzando l&#39;API Java:

1. Includere i file di progetto. .

   Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto ConnectorRegistry Client.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `ConnectorRegistryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Specificare il tipo di connettore.

   Specificare il tipo di connettore richiamando il metodo `ConnectorRegistryClient` dell&#39;oggetto `getEndpointDefinition` e passando un valore di stringa che specifica il tipo di connettore. Ad esempio, per specificare il tipo di connettore per cartelle esaminate, passare il valore stringa `WatchedFolder`. Questo metodo restituisce un oggetto `Endpoint` che corrisponde al tipo di connettore.

1. Recuperare i valori di configurazione.

   * Recuperare i valori di configurazione associati all&#39;interno dell&#39;endpoint richiamando il metodo `Endpoint` dell&#39;oggetto `getConfigParameters`. Questo metodo restituisce un array di oggetti `ConfigParameter`.
   * Recuperate informazioni su ciascun valore di configurazione recuperando ogni elemento all&#39;interno dell&#39;array. Ciascun elemento è un oggetto `ConfigParameter`. È possibile, ad esempio, determinare se il valore di configurazione è obbligatorio o facoltativo richiamando il metodo `ConfigParameter` dell&#39;oggetto `isRequired`. Se il valore di configurazione è obbligatorio, questo metodo restituisce `true`.

**Consulta anche**

[Riepilogo dei passaggi](programmatically-endpoints.md#summary-of-steps)

[Avvio rapido: Recupero delle informazioni sul connettore endpoint tramite l&#39;API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
