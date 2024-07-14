---
title: Utilizzo dell’archivio di AEM Forms
description: Gestisci l’archivio AEM Forms per creare cartelle, scrivere, elencare, leggere, aggiornare e cercare risorse utilizzando l’API Java e l’API del servizio web. Inoltre, scopri come creare relazioni tra risorse, bloccare ed eliminare risorse.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '9036'
ht-degree: 0%

---

# Utilizzo dell’archivio di AEM Forms {#working-with-aem-forms-repository}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio archivio**

Il servizio Archivio fornisce ad AEM Forms servizi di archiviazione e gestione delle risorse. Quando gli sviluppatori creano un&#39;applicazione *AEM Forms*, possono distribuire le risorse nell&#39;archivio anziché nel file system. Le risorse possono includere qualsiasi tipo di materiale collaterale, tra cui moduli XML, PDF forms (inclusi i moduli Acrobat), frammenti di moduli, immagini, profili, criteri, file SWF, file DDX, schemi XML, file WSDL e dati di test.

Consideriamo ad esempio la seguente applicazione Forms denominata *Applications/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

In FormsFolder è presente un file denominato Loan.xdp. Per accedere a questa struttura di modulo, specificare il percorso completo (inclusa la versione): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms tramite Workbench, vedere la [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Il percorso di una risorsa nell’archivio AEM Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Puoi sfogliare l’archivio di AEM Forms utilizzando un browser web. Per sfogliare il repository, immettere l&#39;URL seguente in un browser Web `https://[server name]:[server port]/repository`. Puoi verificare i risultati della procedura di avvio rapido associati alla sezione Utilizzo dell’archivio di AEM Forms utilizzando un browser web. Ad esempio, se aggiungi contenuto all’archivio di AEM Forms, puoi visualizzarlo in un browser web. (Vedere [Guida rapida (modalità SOAP): Scrittura di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

L’API dell’archivio fornisce diverse operazioni che è possibile utilizzare per memorizzare e recuperare informazioni dall’archivio. Ad esempio, puoi ottenere un elenco di risorse o recuperare risorse specifiche memorizzate nell’archivio quando una risorsa è necessaria per l’elaborazione di un’applicazione.

>[!NOTE]
>
>Impossibile utilizzare l’API dell’archivio per interagire con Content Services (obsoleto). Per interagire con Content Services (obsoleto), utilizza l’API Document Management.

Utilizzando l’API del servizio Archivio, puoi eseguire le seguenti attività:

* Creare cartelle. Vedere [Creazione di cartelle](aem-forms-repository.md#creating-folders).
* Scrivi le risorse e le relative proprietà. Consulta [Scrittura delle risorse](aem-forms-repository.md#writing-resources).
* Elencare le risorse in una determinata raccolta o correlate ad altre risorse. Vedi [Elenco delle risorse](aem-forms-repository.md#listing-resources).
* Leggi le risorse e le relative proprietà. Consulta [Lettura delle risorse](aem-forms-repository.md#reading-resources).
* Aggiornare le risorse e le relative proprietà. Vedi [Aggiornamento risorse](aem-forms-repository.md#updating-resources).
* Cerca le risorse, inclusa la cronologia, le risorse correlate e le proprietà. Vedi [Ricerca delle risorse](aem-forms-repository.md#searching-for-resources).
* Specificare le relazioni tra le risorse. Vedere [Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships).
* Consente di gestire il controllo dell&#39;accesso alle risorse, incluso il blocco e lo sblocco delle risorse, nonché la lettura e la scrittura di elenchi di controllo di accesso (ACL). Vedi [Blocco delle risorse](aem-forms-repository.md#locking-resources).
* Elimina le risorse e le relative proprietà. Vedi [Eliminazione delle risorse](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Utilizzando l&#39;API del repository, non è possibile gestire il controllo dell&#39;accesso alle risorse, cercare risorse o specificare relazioni tra risorse utilizzando un repository ECM.

>[!NOTE]
>
>Quando un PDF crittografato viene scritto nel repository, non è possibile utilizzare la funzione di estrazione automatica delle relazioni. In caso contrario, un PDF crittografato può essere archiviato nell’archivio e successivamente recuperato. Il modulo di recupero può scegliere di decrittografare il PDF dopo averlo recuperato dall’archivio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di cartelle {#creating-folders}

Le cartelle (raccolte di risorse) vengono utilizzate per memorizzare gli oggetti (file o risorse) in raggruppamenti organizzati. Le cartelle possono contenere risorse e altre cartelle, note anche come sottocartelle. Le risorse possono essere archiviate in una sola cartella alla volta.

I file ereditano gli elenchi di controllo di accesso (ACL) dalle cartelle, mentre le sottocartelle ereditano gli ACL dalle cartelle padre. Pertanto, le cartelle principali devono esistere prima di poter creare le cartelle secondarie. L&#39;IDE consente di interagire solo cartella per cartella e non file per file. Non è possibile creare una versione delle cartelle e non è necessario farlo; una cartella non contiene dati. È invece solo un contenitore per le risorse che contengono dati. L&#39;ACL predefinito è un&#39;autorizzazione a livello di sistema, il che significa che gli utenti devono disporre di autorizzazioni a livello di sistema (lettura, scrittura, spostamento e gestione degli ACL) fino a quando qualcuno non assegna loro le autorizzazioni per una particolare cartella. Gli ACL funzionano solo nell’IDE.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare una cartella, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare il client del servizio.
1. Crea la cartella.
1. Scrivere la cartella nel repository.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter creare una raccolta di risorse a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Crea la cartella**

Richiama il metodo del servizio Archivio per creare la raccolta di risorse e popolarla con informazioni di identificazione, tra cui UUID, nome della cartella e descrizione.

**Scrivere la cartella nel repository**

Richiama il metodo del servizio Repository per scrivere la raccolta di risorse, specificando l’URI della cartella di destinazione.

**Consulta anche**

[Creare cartelle utilizzando l’API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Creare cartelle utilizzando l’API del servizio web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creare cartelle utilizzando l’API Java {#create-folders-using-the-java-api}

Crea una cartella utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi i file di progetto nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Creare la cartella

   Per creare una raccolta di risorse, è innanzitutto necessario creare un oggetto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Richiama il metodo `newResourceCollection` dell&#39;oggetto `repositoryInfomodelFactoryBean` e passa i seguenti parametri:

   * Identificatore UUID `com.adobe.repository.infomodel.Id` da assegnare alla risorsa.
   * Identificatore UUID `com.adobe.repository.infomodel.Lid` da assegnare alla risorsa.
   * `java.lang.String` contenente il nome della raccolta di risorse. Esempio: `FormsFolder`.

   Il metodo restituisce un oggetto `com.adobe.repository.infomodel.bean.ResourceCollection` che rappresenta la nuova cartella.

   Impostare la descrizione della cartella utilizzando il metodo `setDescription` e passare il seguente parametro:

   * `String` che descrive la raccolta di risorse. In questo esempio, `"test Folder"` è utilizzato `.`

1. Scrivere la cartella nel repository

   Richiama il metodo `writeResource` dell&#39;oggetto `ResourceRepositoryClient` e passa l&#39;URI della cartella e dell&#39;oggetto `ResourceCollection`. Ad esempio, l&#39;URI della cartella può essere il seguente valore `/Applications/FormsApplication/1.0/`.

   Il metodo restituisce un&#39;istanza dell&#39;oggetto `com.adobe.repository.infomodel.bean.Resource` appena creato. È possibile, ad esempio, recuperare il valore dell&#39;identificatore della nuova risorsa richiamando il metodo `getId` dell&#39;oggetto `com.adobe.repository.infomodel.bean.Resource`.

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Quick Start (modalità SOAP): creazione di una cartella utilizzando l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare cartelle utilizzando l’API del servizio web {#create-folders-using-the-web-service-api}

Crea una cartella utilizzando l’API del servizio Archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del repository utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Creare la cartella

   Creare la cartella utilizzando il costruttore predefinito per la classe `ResourceCollection` e passare i seguenti parametri:

   * Oggetto `Id` creato richiamando il costruttore predefinito per la classe `Id` e assegnato al campo `id` dell&#39;oggetto `Resource`.
   * Oggetto `Lid` creato richiamando il costruttore predefinito per la classe `Lid` e assegnato al campo `lid` dell&#39;oggetto `Resource`.
   * Stringa contenente il nome della raccolta di risorse, assegnata al campo `name` dell&#39;oggetto `Resource`. Il nome utilizzato in questo esempio è `"testfolder"`.
   * Stringa contenente la descrizione della raccolta di risorse, assegnata al campo `description` dell&#39;oggetto `Resource`. La descrizione utilizzata in questo esempio è `"test folder"`.

1. Scrivere la cartella nel repository

   Richiama il metodo `writeResource` dell&#39;oggetto `RepositoryServiceService` e passa i seguenti parametri:

   * Percorso in cui creare la cartella.
   * Oggetto `ResourceCollection` che rappresenta la cartella.
   * Passa `null` per gli altri due parametri.

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Scrittura delle risorse {#writing-resources}

Puoi creare le risorse in una determinata posizione nell’archivio. La dimensione naturale del file è soggetta alle limitazioni del database e al timeout della sessione. Per la configurazione predefinita, i file sono limitati a 25 MB. Per aumentare o ridurre la dimensione massima del file, è necessario modificare la configurazione del database.

La scrittura delle risorse equivale all’archiviazione dei dati nell’archivio. Una volta scritta una risorsa nell’archivio, questa diventa accessibile a tutti i client nell’ecosistema dell’archivio. Quando si scrivono nel repository risorse quali schemi XML, file XDP e file XSD, il contenuto viene analizzato in base al tipo MIME. Se il tipo MIME è supportato, il parser determina se esiste una relazione implicita con altri contenuti. Ad esempio, se un foglio di stile CSS ha un URL relativo che fa riferimento a un CSS comune, è previsto che invierai anche il CSS comune nell’archivio. La relazione tra le due risorse viene memorizzata come relazione in sospeso per un periodo non regolabile di 30 giorni. Quando invii il CSS comune all’archivio entro il periodo di 30 giorni, viene creata la relazione.

Quando si crea una risorsa, l&#39;elenco di controllo di accesso (ACL) viene ereditato dalla cartella padre. La cartella principale dispone di autorizzazioni a livello di sistema fino alla creazione di una risorsa o cartella iniziale. A questo punto alla risorsa o alla cartella vengono assegnate le autorizzazioni ACL predefinite.

Puoi scrivere le risorse a livello di programmazione utilizzando il servizio Archivio API Java o API del servizio web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per scrivere una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Archivio.
1. Specifica l’URI della risorsa da leggere.
1. Leggi la risorsa.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Specificare l&#39;URI della cartella di destinazione per la risorsa**

Crea una stringa contenente l’URI della risorsa da leggere. La sintassi include barre, come in questo esempio: &quot;/*percorso*/*cartella*&quot;.

**Crea la risorsa**

Richiama il metodo del servizio Archivio per creare la risorsa e compilarla con le informazioni di identificazione, tra cui UUID, nome e descrizione.

**Specificare il contenuto della risorsa**

Richiama il metodo del servizio Archivio per creare il contenuto della risorsa e archiviarlo nella risorsa.

**Scrivere la risorsa nella cartella di destinazione**

Richiama il metodo del servizio Archivio per scrivere la risorsa, specificando l’URI della cartella di destinazione.

**Consulta anche**

[Scrivere risorse utilizzando l’API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Scrivere risorse utilizzando l’API del servizio web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Scrivere risorse utilizzando l’API Java {#write-resources-using-the-java-api}

Scrivere una risorsa utilizzando l’API del servizio Archivio (Java):

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specifica l’URI della cartella di destinazione per la risorsa

   Specifica l’URI della cartella di destinazione per la risorsa. In questo caso, poiché la risorsa denominata `testResource` verrà archiviata nella cartella denominata `testFolder`, l&#39;URI della cartella è `"/testFolder"`. L&#39;URI viene archiviato come oggetto `java.lang.String`.

1. Creare la risorsa

   Per creare una risorsa, è innanzitutto necessario creare un oggetto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Richiama il metodo `newResource` dell&#39;oggetto `RepositoryInfomodelFactoryBean`, che crea un oggetto `com.adobe.repository.infomodel.bean.Resource`. In questo esempio, vengono forniti i seguenti parametri:

   * Oggetto `com.adobe.repository.infomodel.Id` creato richiamando il costruttore predefinito per la classe `Id`.
   * Oggetto `com.adobe.repository.infomodel.Lid` creato richiamando il costruttore predefinito per la classe `Lid`.
   * `java.lang.String` contenente il nome file della risorsa.

   Per specificare la descrizione della risorsa, richiamare il metodo `setDescription` dell&#39;oggetto `Resource` e passare una stringa contenente la descrizione. In questo esempio, la descrizione è `"test resource"`.

1. Specificare il contenuto della risorsa

   Per creare contenuto per la risorsa, richiamare il metodo `newResourceContent` dell&#39;oggetto `RepositoryInfomodelFactoryBean`, che restituisce un oggetto `com.adobe.repository.infomodel.bean.ResourceContent`. Aggiungi contenuto all&#39;oggetto `ResourceContent`. In questo esempio, questo viene eseguito eseguendo le seguenti attività:

   * Richiamare il metodo `setDataDocument` dell&#39;oggetto `ResourceContent` e passare un oggetto `com.adobe.idp.Document`
   * Richiamare il metodo `setSize` dell&#39;oggetto `ResourceContent` e passare le dimensioni in byte dell&#39;oggetto `Document`

   Aggiungere il contenuto alla risorsa richiamando il metodo `setContent` dell&#39;oggetto `Resource` e passando nell&#39;oggetto `ResourceContent`. Per ulteriori informazioni, consulta [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Scrivi la risorsa nella cartella di destinazione

   Richiama il metodo `writeResource` dell&#39;oggetto `ResourceRepositoryClient` e passa l&#39;URI della cartella e l&#39;oggetto `Resource`.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Quick Start (modalità SOAP): scrittura di una risorsa utilizzando l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Scrivere risorse utilizzando l’API del servizio web {#write-resources-using-the-web-service-api}

Scrivere una risorsa utilizzando l’API del servizio Archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del repository utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specifica l’URI della cartella di destinazione per la risorsa

   Specifica l’URI della cartella di destinazione per la risorsa. In questo caso, poiché la risorsa denominata `testResource` verrà archiviata nella cartella denominata `testFolder`, l&#39;URI della cartella è `"/testFolder"`. Quando si utilizza un linguaggio compatibile con Microsoft .NET Framework, ad esempio C#, archiviare l&#39;URI in un oggetto `System.String`.

1. Creare la risorsa

   Per creare una risorsa, richiamare il costruttore predefinito per la classe `Resource`. In questo esempio, nell&#39;oggetto `Resource` sono memorizzate le seguenti informazioni:

   * Oggetto `com.adobe.repository.infomodel.Id` creato richiamando il costruttore predefinito per la classe `Id` e assegnato al campo `id` dell&#39;oggetto `Resource`.
   * Oggetto `com.adobe.repository.infomodel.Lid` creato richiamando il costruttore predefinito per la classe `Lid` e assegnato al campo `lid` dell&#39;oggetto `Resource`.
   * Stringa contenente il nome file della risorsa, assegnato al campo `name` dell&#39;oggetto `Resource`. Il nome utilizzato in questo esempio è `"testResource"`.
   * Stringa contenente la descrizione della risorsa, assegnata al campo `description` dell&#39;oggetto `Resource`. La descrizione utilizzata in questo esempio è `"test resource"`.

1. Specificare il contenuto della risorsa

   Per creare contenuto per la risorsa, richiamare il costruttore predefinito per la classe `ResourceContent`. Aggiungere quindi il contenuto all&#39;oggetto `ResourceContent`. In questo esempio, questo viene eseguito eseguendo le seguenti attività:

   * Assegnazione di un oggetto `BLOB` contenente un documento al campo `dataDocument` dell&#39;oggetto `ResourceContent`.
   * Assegnazione della dimensione in byte dell&#39;oggetto `BLOB` al campo `size` dell&#39;oggetto `ResourceContent`.

   Aggiungere il contenuto alla risorsa assegnando l&#39;oggetto `ResourceContent` al campo `content` dell&#39;oggetto `Resource`.

1. Scrivi la risorsa nella cartella di destinazione

   Richiama il metodo `writeResource` dell&#39;oggetto `RepositoryServiceService` e passa l&#39;URI della cartella e l&#39;oggetto `Resource`. Passa `null` per gli altri due parametri.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Elenco delle risorse {#listing-resources}

Puoi scoprire le risorse elencandole. Viene eseguita una query sull’archivio per trovare tutte le risorse correlate a una determinata raccolta di risorse.

Una volta organizzate le risorse, è possibile ispezionare la struttura creata visualizzando un particolare ramo della struttura, come si farebbe in un sistema operativo.

Le risorse dell’elenco operano in base alla relazione: le risorse sono membri delle cartelle. L’appartenenza è rappresentata da una relazione di tipo &quot;member of&quot;. Quando si elencano risorse in una determinata cartella, si esegue una query per individuare le risorse correlate a una determinata cartella tramite la relazione &quot;membro di&quot;. Le relazioni sono direzionali: un membro di una relazione ha un&#39;origine che è un membro della destinazione. L&#39;origine è la risorsa. La destinazione è la cartella padre.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per elencare le risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare il client del servizio.
1. Specifica il percorso della cartella.
1. Recupera l’elenco delle risorse.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter creare una raccolta di risorse a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Specificare il percorso della cartella**

Crea una stringa contenente il percorso della cartella contenente le risorse. La sintassi include barre, come in questo esempio: &quot;/*percorso*/*cartella*&quot;.

**Recupera l&#39;elenco delle risorse**

Richiama il metodo del servizio Archivio per recuperare l’elenco delle risorse, specificando il percorso della cartella di destinazione.

**Consulta anche**

[Elencare le risorse utilizzando l’API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Elencare le risorse utilizzando l’API del servizio web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Elencare le risorse utilizzando l’API Java {#list-resources-using-the-java-api}

Elencare le risorse utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare il percorso della cartella

   Specificare l&#39;URI della raccolta di risorse di cui eseguire la query. In questo caso, l&#39;URI è `"/testFolder"`. L&#39;URI viene archiviato come oggetto `java.lang.String`.

1. Recuperare l’elenco delle risorse

   Richiama il metodo `listMembers` dell&#39;oggetto `ResourceRepositoryClient` e passa l&#39;URI della cartella.

   Il metodo restituisce `java.util.List` di `com.adobe.repository.infomodel.bean.Resource` oggetti che sono l&#39;origine di `com.adobe.repository.infomodel.bean.Relation` di tipo `Relation.TYPE_MEMBER_OF` e che hanno come destinazione l&#39;URI della raccolta di risorse. È possibile eseguire iterazioni in `List` per recuperare ogni risorsa. In questo esempio vengono visualizzati il nome e la descrizione di ogni risorsa.

**Consulta anche**

[Elenco delle risorse](aem-forms-repository.md#listing-resources).

[Quick Start (modalità SOAP): elenco delle risorse utilizzando l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Elencare le risorse utilizzando l’API del servizio web {#list-resources-using-the-web-service-api}

Elencare le risorse utilizzando l’API del servizio Archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare il percorso della cartella

   Specificare una stringa contenente l&#39;URI della cartella da interrogare. In questo caso, l&#39;URI è `"/testFolder"`. Quando si utilizza un linguaggio conforme a Microsoft .NET Framework (ad esempio, C#), archiviare l&#39;URI in un oggetto `System.String`.

1. Recuperare l’elenco delle risorse

   Richiama il metodo `listMembers` dell&#39;oggetto `RepositoryServiceService` e passa l&#39;URI della cartella come primo parametro. Passa `null` per gli altri due parametri.

   Il metodo restituisce un array di oggetti che è possibile eseguire il cast a `Resource` oggetti. È possibile scorrere l&#39;array di oggetti per recuperare ciascuna delle risorse correlate. In questo esempio vengono visualizzati il nome e la descrizione di ogni risorsa.

**Consulta anche**

[Elenco delle risorse](aem-forms-repository.md#listing-resources).

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Lettura delle risorse {#reading-resources}

Puoi recuperare le risorse da una determinata posizione nell’archivio per leggerne il contenuto e i metadati. Il flusso di lavoro è front-end da un modulo di inizializzazione. Il processo dispone di tutte le autorizzazioni necessarie per leggere il modulo. Il sistema recupera il form di dati e legge il contenuto dal repository. L’archivio consente l’accesso al contenuto e ai metadati (la capacità persino di sapere che la risorsa esiste).

L’archivio dispone dei seguenti quattro tipi di autorizzazioni:

* **attraversare**: consente di elencare le risorse, ovvero di leggere i metadati delle risorse ma non il contenuto delle risorse
* **read**: consente di leggere il contenuto delle risorse
* **scrittura**: consente di scrivere il contenuto delle risorse
* **gestione degli elenchi di controllo di accesso (ACL)**: consente di manipolare gli ACL sulle risorse

Gli utenti possono eseguire i processi solo se dispongono dell&#39;autorizzazione per eseguire il processo. Gli utenti IDE devono disporre di autorizzazioni di lettura e navigazione per la sincronizzazione con l’archivio. Gli ACL vengono applicati solo in fase di progettazione poiché il runtime si verifica all&#39;interno del contesto di sistema.

Puoi leggere le risorse a livello di programmazione utilizzando l’API Java del servizio Archivio o l’API del servizio web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per leggere una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Archivio.
1. Specifica l’URI della risorsa da leggere.
1. Leggi la risorsa.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Specificare l&#39;URI della risorsa da leggere**

Crea una stringa contenente l’URI della risorsa da leggere. La sintassi include barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;.

**Leggi la risorsa**

Richiama il metodo del servizio Archivio per leggere la risorsa, specificando l’URI.

**Consulta anche**

[Lettura delle risorse tramite API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lettura delle risorse tramite l’API del servizio web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Lettura delle risorse tramite API Java {#read-resources-using-the-java-api}

Leggi una risorsa utilizzando l’API del servizio Archivio (Java):

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specifica l’URI della risorsa da leggere

   Specifica un valore stringa che rappresenta l’URI della risorsa da recuperare. Se ad esempio la risorsa è denominata *testResource* in una cartella denominata *testFolder*, specificare `/testFolder/testResource`.

1. Leggi la risorsa

   Richiama il metodo `readResource` dell&#39;oggetto `ResourceRepositoryClient` e passa l&#39;URI della risorsa come parametro. Questo metodo restituisce un&#39;istanza `Resource` che rappresenta la risorsa.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Guida rapida (modalità SOAP): lettura di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lettura delle risorse tramite l’API del servizio web {#reading-resources-using-the-web-service-api}

Leggi una risorsa utilizzando l’API del servizio Archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del repository. Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).
   * Fare riferimento all&#39;assembly client Microsoft .NET. Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specifica l’URI della risorsa da leggere

   Specifica una stringa contenente l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResource"`. Quando si utilizza un linguaggio compatibile con Microsoft .NET Framework, ad esempio C#, archiviare l&#39;URI in un oggetto `System.String`.

1. Leggi la risorsa

   Richiama il metodo `readResource` dell&#39;oggetto `RepositoryServiceService` e passa l&#39;URI della risorsa come primo parametro. Passa `null` per gli altri due parametri.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Aggiornamento delle risorse {#updating-resources}

Puoi recuperare e aggiornare il contenuto delle risorse nell’archivio. Quando si aggiornano le risorse, il controllo di accesso a tali risorse rimane invariato tra le versioni. Quando si esegue un aggiornamento, è possibile incrementare la versione principale. Se non scegli di incrementare la versione principale, la versione secondaria viene aggiornata automaticamente.

Quando aggiorni una risorsa, la nuova versione viene creata in base agli attributi di risorsa specificati. Quando aggiorni una risorsa, specifichi due parametri importanti: l’URI di destinazione e un’istanza della risorsa contenente tutti i metadati aggiornati. È importante notare che se non stai modificando un dato attributo (ad esempio, il nome), l’attributo è ancora necessario nell’istanza trasmessa. Le relazioni create durante l’analisi del contenuto vengono aggiunte alla versione specifica e non vengono portate avanti a meno che non sia specificato diversamente.

Ad esempio, se aggiorni un file XDP che contiene riferimenti ad altre risorse, anche questi riferimenti aggiuntivi verranno registrati. Si supponga che la versione 1.0 di form.xdp disponga di due riferimenti esterni: un logo e un foglio di stile e che successivamente venga aggiornato form.xdp in modo che ora disponga di tre riferimenti: un logo, un foglio di stile e un file di schema. Durante l’aggiornamento, l’archivio aggiungerà la terza relazione (al file di schema) alla tabella delle relazioni in sospeso. Una volta che il file di schema è presente nell’archivio, la relazione viene formata automaticamente. Tuttavia, se la versione 2.0 di form.xdp non utilizza più il logo, la versione 2.0 di form.xdp non avrà una relazione con il logo.

Tutte le operazioni di aggiornamento sono atomiche e transazionali. Ad esempio, se due utenti leggono la stessa risorsa ed entrambi decidono di aggiornare la versione 1.0 alla versione 2.0, uno di loro avrà esito positivo e uno di loro avrà esito negativo, l’integrità dell’archivio verrà mantenuta ed entrambi riceveranno un messaggio di conferma del completamento o del fallimento. Se la transazione non viene eseguita, verrà eseguito il rollback in caso di errore del database e verrà eseguito il timeout o il rollback a seconda del server applicazioni.

Puoi aggiornare le risorse a livello di programmazione utilizzando l’API Java del servizio Archivio o l’API del servizio web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per aggiornare una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Archivio.
1. Recupera la risorsa da aggiornare.
1. Aggiorna la risorsa.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Recupera la risorsa da aggiornare**

Leggi la risorsa. Per ulteriori informazioni, vedere [Lettura delle risorse](aem-forms-repository.md#reading-resources).

**Aggiorna la risorsa**

Imposta le nuove informazioni nella risorsa e richiama il metodo del servizio Archivio per aggiornare la risorsa, specificando l’URI, la risorsa aggiornata e la modalità di aggiornamento delle informazioni sulla versione.

**Consulta anche**

[Aggiornare le risorse utilizzando l’API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Aggiornare le risorse utilizzando l’API del servizio web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Aggiornare le risorse utilizzando l’API Java {#update-resources-using-the-java-api}

Aggiornare una risorsa utilizzando l’API del servizio Archivio (Java):

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recupera la risorsa da aggiornare

   Specifica l’URI della risorsa da recuperare e leggere. In questo esempio, l&#39;URI della risorsa è `"/testFolder/testResource"`.

1. Aggiornare la risorsa

   Aggiornare le informazioni dell&#39;oggetto `Resource`. In questo esempio, per aggiornare la descrizione, richiamare il metodo `setDescription` dell&#39;oggetto `Resource` e passare la nuova stringa di descrizione come parametro.

   Quindi richiamare il metodo `updateResource` dell&#39;oggetto `ServiceClientFactory` e passare i seguenti parametri:

   * Oggetto `java.lang.String` contenente l&#39;URI della risorsa.
   * Oggetto `Resource` contenente le informazioni aggiornate sulla risorsa.
   * Valore `boolean` che indica se aggiornare la versione principale o secondaria. In questo esempio, viene passato il valore `true` per indicare che la versione principale deve essere incrementata.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Quick Start (modalità SOAP): aggiornamento di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiornare le risorse utilizzando l’API del servizio web {#update-resources-using-the-web-service-api}

Aggiornare una risorsa utilizzando l’API dell’archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Recupera la risorsa da aggiornare

   Specifica l’URI della risorsa da recuperare e leggi la risorsa. In questo esempio, l&#39;URI della risorsa è `"/testFolder/testResource"`. Per ulteriori informazioni, vedere [Lettura delle risorse](aem-forms-repository.md#reading-resources).

1. Aggiornare la risorsa

   Aggiornare le informazioni dell&#39;oggetto `Resource`. In questo esempio, per aggiornare la descrizione, assegnare un nuovo valore al campo `description` dell&#39;oggetto `Resource`.

1. Richiama il metodo `updateResource` dell&#39;oggetto `RepositoryServiceService` e passa i seguenti parametri:

   * Oggetto `System.String` contenente l&#39;URI della risorsa.
   * Oggetto `Resource` contenente le informazioni aggiornate sulla risorsa.
   * Valore `boolean` che indica se aggiornare la versione principale o secondaria. In questo esempio, viene passato il valore `true` per indicare che la versione principale deve essere incrementata.
   * Passa `null` per i due parametri rimanenti.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ricerca di risorse {#searching-for-resources}

È possibile creare query utilizzate per cercare risorse nell’archivio, inclusa la cronologia, le risorse correlate e le proprietà.

È possibile recuperare le risorse correlate per determinare le dipendenze tra un modulo e i relativi frammenti. Ad esempio, se disponi di un modulo puoi determinare quali frammenti o risorse esterne utilizza. Se si dispone di un&#39;immagine, è inoltre possibile individuare i moduli che la utilizzano. Puoi anche cercare risorse correlate utilizzando filtri basati sulle proprietà. È possibile, ad esempio, cercare tutti i moduli che utilizzano un&#39;immagine con un nome specificato o trovare qualsiasi immagine utilizzata da un modulo con un nome specificato. Puoi anche eseguire ricerche utilizzando le proprietà della risorsa. È ad esempio possibile eseguire una query per trovare tutti i moduli o le risorse il cui nome inizia con una determinata stringa che può includere i caratteri jolly &quot;%&quot; e &quot;_&quot;. Ricorda che le ricerche basate sulle proprietà non si basano su relazioni; tali ricerche si basano sul presupposto che si disponga di conoscenze specifiche su una determinata risorsa.

**Istruzioni query**

Una *query* contiene una o più istruzioni unite in modo logico con condizioni. Un&#39;istruzione *statement* è costituita da un operando sinistro, un operatore e un operando destro. È inoltre possibile specificare l&#39;ordinamento da utilizzare per i risultati della ricerca. L&#39;*ordinamento* contiene informazioni equivalenti a una clausola SQL `ORDER BY` ed è costituito da elementi che contengono gli attributi su cui è basata la ricerca e da un valore che indica se deve essere utilizzato l&#39;ordine crescente o decrescente.

Puoi cercare le risorse a livello di programmazione utilizzando il servizio Archivio API Java. Al momento, non è possibile utilizzare l’API del servizio web per cercare le risorse.

**Comportamento ordinamento**

L&#39;ordinamento non viene rispettato quando si richiama il metodo `searchProperties` dell&#39;oggetto `ResourceRepositoryClient` e si specifica un ordinamento. Si supponga, ad esempio, di creare una risorsa con tre proprietà personalizzate, i cui nomi di attributo sono `name`, `secondName` e `asecondName`. Successivamente si crea un elemento di ordinamento sul nome dell&#39;attributo e si imposta il valore `ascending` su `true`.

Quindi si richiama il metodo `searchProperties` dell&#39;oggetto `ResourceRepositoryClient` e si passa l&#39;ordinamento. La ricerca restituisce la risorsa corretta, con le tre proprietà. Tuttavia, le proprietà non sono ordinate per nome di attributo. Vengono restituiti nell&#39;ordine in cui sono stati aggiunti: `name`, `secondName` e `asecondName`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per cercare le risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Archivio.
1. Specificare la cartella di destinazione per la ricerca.
1. Specifica gli attributi utilizzati nella ricerca.
1. Crea la query utilizzata nella ricerca.
1. Crea l’ordinamento per i risultati della ricerca.
1. Cerca le risorse.
1. Recupera le risorse dal risultato della ricerca.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Specificare la cartella di destinazione per la ricerca**

Creare una stringa contenente il percorso di base da cui eseguire la ricerca. La sintassi include barre, come in questo esempio: &quot;/*percorso*/*cartella*&quot;.

**Specificare gli attributi utilizzati nella ricerca**

Puoi basare la ricerca sugli attributi contenuti nelle risorse. Specificare i valori degli attributi su cui eseguire la ricerca.

**Crea la query utilizzata nella ricerca**

Creare una query utilizzando istruzioni e condizioni. Ogni istruzione specifica l’attributo su cui basare la ricerca, la condizione da utilizzare e il valore dell’attributo da utilizzare nella ricerca.

**Crea l&#39;ordinamento per i risultati della ricerca**

L’ordinamento è costituito da elementi, ciascuno dei quali contiene uno degli attributi utilizzati nella ricerca e un valore che indica se deve essere utilizzato l’ordine crescente o decrescente.

**Cerca le risorse**

Cerca le risorse utilizzando la cartella, la query e l’ordinamento. Inoltre, indica la profondità della ricerca e un limite superiore al numero di risultati da restituire.

**Recupera le risorse dal risultato della ricerca**

Scorrere l&#39;elenco di risorse restituito ed estrarre le informazioni per l&#39;ulteriore elaborazione.

**Consulta anche**

[Cercare risorse utilizzando l’API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Cercare risorse utilizzando l’API Java {#search-for-resources-using-the-java-api}

Cerca una risorsa utilizzando l’API del servizio Archivio (Java):

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare la cartella di destinazione per la ricerca

   Specificare l&#39;URI del percorso di base da cui eseguire la ricerca. In questo esempio, l&#39;URI della risorsa è `/testFolder`.

1. Specificare gli attributi utilizzati nella ricerca

   Specificare i valori per gli attributi su cui eseguire la ricerca. Gli attributi esistono in un oggetto `com.adobe.repository.infomodel.bean.Resource`. In questo esempio, la ricerca verrà eseguita sull&#39;attributo name; pertanto, viene utilizzato un `java.lang.String` contenente il nome dell&#39;oggetto `Resource`, che in questo caso è `testResource`.

1. Crea la query utilizzata nella ricerca

   Per creare una query, creare un oggetto `com.adobe.repository.query.Query` richiamando il costruttore predefinito per la classe `Query` e aggiungere istruzioni alla query.

   Per creare un&#39;istruzione, richiamare il costruttore per la classe `com.adobe.repository.query.Query.Statement` e passare i seguenti parametri:

   * Operando sinistro contenente la costante dell&#39;attributo della risorsa. In questo esempio, poiché il nome della risorsa viene utilizzato come base per la ricerca, viene utilizzato il valore statico `Resource.ATTRIBUTE_NAME`.
   * Operatore contenente la condizione utilizzata nella ricerca dell&#39;attributo. L&#39;operatore deve essere una delle costanti statiche nella classe `Query.Statement`. In questo esempio viene utilizzato il valore statico `Query.Statement.OPERATOR_BEGINS_WITH`.
   * Operando destro contenente il valore di attributo su cui eseguire la ricerca. In questo esempio, viene utilizzato l&#39;attributo name, un `String` contenente il valore `"testResource"`.

   Specificare lo spazio dei nomi dell&#39;operando sinistro richiamando il metodo `setNamespace` dell&#39;oggetto `Query.Statement` e passando uno dei valori statici contenuti nella classe `com.adobe.repository.infomodel.bean.ResourceProperty`. In questo esempio, viene utilizzato `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`.

   Aggiungere ogni istruzione alla query richiamando il metodo `addStatement` dell&#39;oggetto `Query` e passando l&#39;oggetto `Query.Statement`.

1. Creare l’ordinamento per i risultati della ricerca

   Per specificare l&#39;ordinamento utilizzato nei risultati della ricerca, creare un oggetto `com.adobe.repository.query.sort.SortOrder` richiamando il costruttore predefinito per la classe `SortOrder` e aggiungere elementi all&#39;ordinamento.

   Per creare un elemento per l&#39;ordinamento, richiamare uno dei costruttori per la classe `com.adobe.repository.query.sort.SortOrder.Element`. In questo esempio, poiché il nome della risorsa viene utilizzato come base per la ricerca, il valore statico `Resource.ATTRIBUTE_NAME` viene utilizzato come primo parametro e l&#39;ordine crescente (un valore `boolean` di `true`) viene specificato come secondo parametro.

   Aggiungere ogni elemento al criterio di ordinamento richiamando il metodo `addSortElement` dell&#39;oggetto `SortOrder` e passando nell&#39;oggetto `SortOrder.Element`.

1. Cercare le risorse

   Per cercare `resources` in base alle proprietà dell&#39;attributo, richiamare il metodo `searchProperties` dell&#39;oggetto `ResourceRepositoryClient` e passare i seguenti parametri:

   * Un `String` contenente il percorso di base da cui eseguire la ricerca. In questo caso, viene utilizzato `"/testFolder"`.
   * Query utilizzata nella ricerca.
   * Profondità della ricerca. In questo caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` viene utilizzato per indicare che devono essere utilizzati il percorso di base e tutte le relative cartelle.
   * Valore `int` che indica la prima riga dalla quale selezionare il set di risultati non di paging. In questo esempio, è specificato `0`.
   * Valore `int` che indica il numero massimo di risultati da restituire. In questo esempio, è specificato `10`.
   * Ordinamento utilizzato nella ricerca.

   Il metodo restituisce `java.util.List` di `Resource` oggetti nell&#39;ordinamento specificato.

1. Recuperare le risorse dal risultato della ricerca

   Per recuperare le risorse contenute nel risultato della ricerca, scorrere l&#39;iterazione di `List` ed eseguire il cast di ogni oggetto in un `Resource` per estrarre le informazioni. In questo esempio viene visualizzato il nome di ogni risorsa.

**Consulta anche**

[Ricerca di risorse](aem-forms-repository.md#searching-for-resources)

[Quick Start (modalità SOAP): ricerca di risorse tramite API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creazione di relazioni tra risorse {#creating-resource-relationships}

Puoi specificare le relazioni tra le risorse nell’archivio. Esistono tre tipi di relazioni:

* **Dipendenza**: una relazione in cui una risorsa dipende da altre risorse, il che significa che tutte le risorse correlate sono necessarie nel repository.
* **Appartenenza (file system)**: una relazione in cui una risorsa si trova all&#39;interno di una determinata cartella.
* **Personalizzato**: relazione specificata tra le risorse. Ad esempio, se una risorsa è stata dichiarata obsoleta e un’altra risorsa è stata introdotta nell’archivio, puoi specificare una tua relazione di sostituzione.

Puoi creare relazioni personalizzate. Se, ad esempio, si memorizza un file HTML nel repository e viene utilizzata un&#39;immagine, è possibile specificare una relazione personalizzata per correlare il file HTML con l&#39;immagine (in genere solo i file XML vengono associati alle immagini mediante una relazione di dipendenza definita nel repository). Un altro esempio di relazione personalizzata potrebbe essere la creazione di una vista diversa dell’archivio con una struttura a grafo ciclica anziché ad albero. Puoi definire un grafico circolare insieme a un visualizzatore per analizzare tali relazioni. Infine, puoi indicare che una risorsa sostituisce un’altra anche se le due risorse sono completamente diverse. In tal caso, puoi definire un tipo di relazione al di fuori dell’intervallo riservato e creare una relazione tra queste due risorse. L&#39;applicazione è l&#39;unico client in grado di rilevare ed elaborare la relazione e può essere utilizzata per eseguire ricerche su tale relazione.

Puoi specificare in modo programmatico le relazioni tra le risorse utilizzando l’API Java o l’API del servizio web Repository.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per specificare una relazione tra due risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Archivio.
1. Specifica gli URI delle risorse da correlare.
1. Crea la relazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Specificare gli URI delle risorse da correlare**

Crea stringhe contenenti gli URI della risorsa da correlare. La sintassi include barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;.

**Crea la relazione**

Richiama il metodo del servizio Archivio per creare e specificare il tipo di relazione.

**Consulta anche**

[Creare risorse di relazione tramite API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Creare risorse di relazione tramite l’API del servizio web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creare risorse di relazione tramite API Java {#create-relationship-resources-using-the-java-api}

Crea risorse di relazione utilizzando l’API Java del servizio Repository, esegui le seguenti attività:

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare gli URI delle risorse da correlare

   Specifica gli URI delle risorse da correlare. In questo caso, poiché le risorse sono denominate `testResource1` e `testResource2` e si trovano nella cartella denominata `testFolder`, i relativi URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Gli URI vengono archiviati come oggetti `java.lang.String`. In questo esempio, le risorse vengono prima scritte nell’archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiama il metodo `createRelationship` dell&#39;oggetto `ResourceRepositoryClient` e passa i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Tipo di relazione, che è una delle costanti statiche nella classe `com.adobe.repository.infomodel.bean.Relation`. In questo esempio viene stabilita una relazione di dipendenza specificando il valore `Relation.TYPE_DEPENDANT_OF`.
   * Valore `boolean` che indica se la risorsa di destinazione viene aggiornata automaticamente all&#39;identificatore basato su `com.adobe.repository.infomodel.Id` della nuova risorsa head. In questo esempio, a causa della relazione di dipendenza, viene specificato il valore `true`.

   È inoltre possibile recuperare un elenco di risorse correlate per una determinata risorsa richiamando il metodo `getRelated` dell&#39;oggetto `ResourceRepositoryClient` e passando i parametri seguenti:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio viene specificata la risorsa di origine ( `"/testFolder/testResource1"`).
   * Valore `boolean` che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché questo è il caso.
   * Tipo di relazione, che è una delle costanti statiche nella classe `Relation`. In questo esempio viene specificata una relazione di dipendenza utilizzando lo stesso valore utilizzato in precedenza: `Relation.TYPE_DEPENDANT_OF`.

   Il metodo `getRelated` restituisce un oggetto `java.util.List` di `Resource` tramite il quale è possibile eseguire l&#39;iterazione per recuperare ciascuna delle risorse correlate, eseguendo il cast degli oggetti contenuti in `List` in `Resource`. In questo esempio, `testResource2` dovrebbe essere nell&#39;elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Guida rapida (modalità SOAP): creazione di relazioni tra le risorse tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare risorse di relazione tramite l’API del servizio web {#create-relationship-resources-using-the-web-service-api}

Crea risorse di relazione utilizzando l’API dell’archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare gli URI delle risorse da correlare

   Specifica gli URI delle risorse da correlare. In questo caso, poiché le risorse sono denominate `testResource1` e `testResource2` e si trovano nella cartella denominata `testFolder`, i relativi URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Quando si utilizza un linguaggio compatibile con Microsoft .NET Framework (ad esempio, C#), gli URI vengono archiviati come oggetti `System.String`. In questo esempio, le risorse vengono prima scritte nell’archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiama il metodo `createRelationship` dell&#39;oggetto `RepositoryServiceService` e passa i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Tipo di relazione. In questo esempio viene stabilita una relazione di dipendenza specificando il valore `3`.
   * Valore `boolean` che indica se è stato specificato il tipo di relazione. In questo esempio viene specificato il valore `true`.
   * Valore `boolean` che indica se la risorsa di destinazione viene aggiornata automaticamente all&#39;identificatore basato su `Id` della nuova risorsa head. In questo esempio, a causa della relazione di dipendenza, viene specificato il valore `true`.
   * Valore `boolean` che indica se è stata specificata l&#39;intestazione di destinazione. In questo esempio viene specificato il valore `true`.
   * Passa `null` per l&#39;ultimo parametro.

   È inoltre possibile recuperare un elenco di risorse correlate per una determinata risorsa richiamando il metodo `getRelated` dell&#39;oggetto `RepositoryServiceService` e passando i parametri seguenti:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio viene specificata la risorsa di origine ( `"/testFolder/testResource1"`).
   * Valore `boolean` che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché questo è il caso.
   * Valore `boolean` che indica se la risorsa di origine è stata specificata. In questo esempio, viene fornito il valore `true`.
   * Matrice di numeri interi contenente i tipi di relazione. In questo esempio viene specificata una relazione di dipendenza utilizzando lo stesso valore nell&#39;array utilizzato in precedenza: `3`.
   * Passa `null` per i due parametri rimanenti.

   Il metodo `getRelated` restituisce un array di oggetti che è possibile eseguire il cast in `Resource` oggetti tramite i quali è possibile eseguire iterazioni per recuperare ciascuna delle risorse correlate. In questo esempio, `testResource2` dovrebbe essere nell&#39;elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Blocco delle risorse {#locking-resources}

Puoi bloccare una risorsa o un set di risorse per un utilizzo esclusivo da parte di un particolare utente o per un utilizzo condiviso tra più utenti. Un blocco condiviso indica che qualcosa si verifica con la risorsa, ma non impedisce a nessun altro di intraprendere azioni con tale risorsa. Una serratura condivisa deve essere considerata un meccanismo di segnalazione. Un blocco esclusivo indica che l’utente che ha bloccato la risorsa cambierà la risorsa e assicura che nessun altro possa farlo finché l’utente non avrà più bisogno di accedere alla risorsa e avrà rilasciato il blocco. Se un amministratore del repository sblocca una risorsa, tutti i blocchi esclusivi e condivisi della risorsa verranno rimossi automaticamente. Questo tipo di azione è destinato alle situazioni in cui un utente non è più disponibile e non ha sbloccato la risorsa.

Quando una risorsa è bloccata, viene visualizzata un&#39;icona di blocco quando si visualizza la scheda Risorse in Workbench, come illustrato nella figura seguente.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Puoi controllare l’accesso alle risorse a livello di programmazione utilizzando l’API Java o l’API del servizio web Repository.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per bloccare e sbloccare le risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Archivio.
1. Specificare l&#39;URI della risorsa da bloccare.
1. Blocca la risorsa.
1. Recupera i blocchi per la risorsa.
1. Sblocca la risorsa

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Specificare l&#39;URI della risorsa da bloccare**

Crea una stringa contenente l’URI della risorsa da bloccare. La sintassi include barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;.

**Blocca la risorsa**

Richiama il metodo del servizio Archivio per bloccare la risorsa, specificando l’URI, il tipo di blocco e la profondità di blocco.

**Recupera i blocchi per la risorsa**

Richiama il metodo del servizio Archivio per recuperare i blocchi per la risorsa, specificando l’URI.

**Sblocca la risorsa**

Richiama il metodo del servizio Archivio per sbloccare la risorsa, specificando l’URI.

**Consulta anche**

[Bloccare le risorse utilizzando l’API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Bloccare le risorse utilizzando l’API del servizio web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Bloccare le risorse utilizzando l’API Java {#lock-resources-using-the-java-api}

Blocca le risorse utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare l&#39;URI della risorsa da bloccare

   Specificare l&#39;URI della risorsa da bloccare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResource"`. L&#39;URI viene archiviato come oggetto `java.lang.String`.

1. Blocca la risorsa

   Richiama il metodo `lockResource` dell&#39;oggetto `ResourceRepositoryClient` e passa i seguenti parametri:

   * URI della risorsa.
   * Ambito del blocco. In questo esempio, poiché la risorsa verrà bloccata per l&#39;utilizzo esclusivo, l&#39;ambito di blocco è specificato come `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * Profondità del blocco. In questo esempio, poiché il blocco verrà applicato solo alla risorsa specifica e a nessuno dei relativi membri o figli, la profondità del blocco è specificata come `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La versione di overload del metodo `lockResource` che richiede quattro parametri genera un&#39;eccezione. Assicurarsi di utilizzare il metodo `lockResource` che richiede tre parametri, come illustrato in questa procedura dettagliata.

1. Recupera i blocchi per la risorsa

   Richiama il metodo `getLocks` dell&#39;oggetto `ResourceRepositoryClient` e passa l&#39;URI della risorsa come parametro. Il metodo restituisce un elenco di oggetti Lock attraverso i quali è possibile eseguire un&#39;iterazione. In questo esempio, il proprietario del blocco, la profondità e l&#39;ambito vengono stampati per ogni oggetto richiamando i metodi `getOwnerUserId`, `getDepth` e `getType` di ogni oggetto Lock, rispettivamente.

1. Sblocca la risorsa

   Richiama il metodo `unlockResource` dell&#39;oggetto `ResourceRepositoryClient` e passa l&#39;URI della risorsa come parametro. Per ulteriori informazioni, vedere [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Quick Start (modalità SOAP): blocco di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Bloccare le risorse utilizzando l’API del servizio web {#lock-resources-using-the-web-service-api}

Blocca le risorse utilizzando l’API del servizio Archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da bloccare

   Specificare una stringa contenente l&#39;URI della risorsa da bloccare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella `testFolder`, il relativo URI è `"/testFolder/testResource"`. Quando si utilizza un linguaggio compatibile con Microsoft .NET Framework, ad esempio C#, archiviare l&#39;URI in un oggetto `System.String`.

1. Blocca la risorsa

   Richiama il metodo `lockResource` dell&#39;oggetto `RepositoryServiceService` e passa i seguenti parametri:

   * URI della risorsa.
   * Ambito del blocco. In questo esempio, poiché la risorsa verrà bloccata per l&#39;utilizzo esclusivo, l&#39;ambito di blocco è specificato come `11`.
   * Profondità del blocco. In questo esempio, poiché il blocco verrà applicato solo alla risorsa specifica e a nessuno dei relativi membri o figli, la profondità del blocco è specificata come `2`.
   * Valore `int` che indica il numero di secondi trascorsi fino alla scadenza del blocco. In questo esempio viene utilizzato il valore di `1000`.
   * Passa `null` per l&#39;ultimo parametro.

1. Recupera i blocchi per la risorsa

   Richiama il metodo `getLocks` dell&#39;oggetto `RepositoryServiceService` e passa l&#39;URI della risorsa come primo parametro e `null` come secondo parametro. Il metodo restituisce un array `object` contenente `Lock` oggetti tramite i quali è possibile eseguire l&#39;iterazione. In questo esempio, il proprietario del blocco, la profondità e l&#39;ambito vengono stampati per ogni oggetto accedendo rispettivamente ai campi `ownerUserId`, `depth` e `type` di ogni oggetto `Lock`.

1. Sblocca la risorsa

   Richiama il metodo `unlockResource` dell&#39;oggetto `RepositoryServiceService` e passa l&#39;URI della risorsa come primo parametro e `null` come secondo parametro.

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Eliminazione delle risorse {#deleting-resources}

Puoi eliminare programmaticamente le risorse da una determinata posizione nell’archivio utilizzando il servizio Archivio Java API (SOAP).

Quando si elimina una risorsa, l&#39;eliminazione è in genere permanente, anche se in alcuni casi gli archivi ECM possono memorizzare le versioni della risorsa in base ai rispettivi meccanismi di cronologia. Pertanto, durante l’eliminazione di una risorsa, è importante assicurarsi di non averne più bisogno. I motivi comuni per l’eliminazione di una risorsa includono la necessità di aumentare lo spazio disponibile nel database. È possibile eliminare una versione di una risorsa, ma in tal caso è necessario specificare l&#39;identificatore della risorsa e non il relativo identificatore logico (LID) o percorso. Se elimini una cartella, tutti gli elementi in essa contenuti, incluse le sottocartelle e le risorse, verranno eliminati automaticamente.

Le risorse correlate non vengono eliminate. Se ad esempio si dispone di un modulo che utilizza il file logo.gif ed si elimina logo.gif, nella tabella delle relazioni in sospeso verrà memorizzata una relazione. In alternativa, per rendere obsoleta la versione, imposta lo stato oggetto della versione più recente su obsoleto.

Un&#39;operazione di eliminazione non è sicura per le transazioni nei sistemi ECM. Ad esempio, se tenti di eliminare 100 risorse e l’operazione non riesce sulla 50a risorsa, le prime 49 istanze verranno eliminate, ma le altre no. In caso contrario, il comportamento predefinito è il rollback (non impegno).

>[!NOTE]
>
>Quando si utilizza il metodo `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` con il repository ECM (EMC Documentum Content Server e IBM FileNet P8 Content Manager), non viene eseguito il rollback della transazione se l&#39;eliminazione non riesce per una delle risorse specificate, pertanto non è possibile annullare l&#39;eliminazione dei file eliminati.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per eliminare una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Archivio.
1. Specifica l’URI della risorsa da eliminare.
1. Elimina la risorsa.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Crea il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tale scopo, è necessario creare un client di servizio.

**Specificare l&#39;URI della risorsa da eliminare**

Crea una stringa contenente l’URI della risorsa da eliminare. La sintassi include barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;. Se la risorsa da eliminare è una cartella, l’eliminazione sarà ricorsiva.

**Elimina la risorsa**

Richiama il metodo del servizio Archivio per eliminare la risorsa, specificando l’URI.

**Consulta anche**

[Eliminare le risorse utilizzando l’API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Eliminare le risorse utilizzando l’API del servizio web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Eliminare le risorse utilizzando Java API (SOAP) {#delete-resources-using-the-java-api-soap}

Eliminare una risorsa utilizzando l’API dell’archivio (Java):

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare l&#39;URI della risorsa da eliminare

   Specifica l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata testResourceToBeDeleted si trova nella cartella denominata testFolder, l&#39;URI corrispondente è `/testFolder/testResourceToBeDeleted`. L&#39;URI viene archiviato come oggetto `java.lang.String`. In questo esempio, la risorsa viene prima scritta nell’archivio e il relativo URI viene recuperato. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Elimina la risorsa

   Richiama il metodo `deleteResource` dell&#39;oggetto `ResourceRepositoryClient` e passa l&#39;URI della risorsa come parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Quick Start (modalità SOAP): ricerca di risorse tramite API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminare le risorse utilizzando l’API del servizio web {#delete-resources-using-the-web-service-api}

Elimina una risorsa utilizzando l’API dell’archivio (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostare la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da eliminare

   Specifica l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata `testResourceToBeDeleted` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResourceToBeDeleted"`. In questo esempio, la risorsa viene prima scritta nell’archivio e il relativo URI viene recuperato. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Elimina la risorsa

   Richiama il metodo `deleteResources` dell&#39;oggetto `RepositoryServiceService` e passa una matrice `System.String` contenente l&#39;URI della risorsa come primo parametro. Passa `null` per il secondo parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
