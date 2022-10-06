---
title: Utilizzo dell’archivio AEM Forms
seo-title: Working with AEM Forms Repository
description: Gestisci l'archivio AEM Forms per creare cartelle, scrivere, elencare, leggere, aggiornare e cercare risorse utilizzando l'API Java e l'API Web Service. Inoltre, scopri come creare relazioni tra risorse, bloccare ed eliminare risorse.
seo-description: Manage AEM Forms repository to create folders, write, list, read, update resources, and search resources using the Java API and Web Service API. In addition, learn how to create resource relationships, lock and delete resources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '9117'
ht-degree: 0%

---

# Utilizzo dell’archivio AEM Forms {#working-with-aem-forms-repository}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Repository**

Il servizio Repository fornisce servizi di archiviazione e gestione delle risorse ad AEM Forms. Quando gli sviluppatori creano un *AEM Forms* possono distribuire le risorse nell’archivio anziché nel file system. Le risorse possono includere qualsiasi tipo di materiale collaterale, inclusi moduli XML, PDF forms (inclusi i moduli Acrobat), frammenti di modulo, immagini, profili, criteri, file SWF, file DDX, schemi XML, file WSDL e dati di test.

Ad esempio, considera la seguente applicazione Forms denominata *Applicazioni/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Tenere presente che nella cartella FormsFolder è presente un file denominato Loan.xdp. Per accedere a questa struttura del modulo, specificare il percorso completo (inclusa la versione): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms tramite Workbench, consulta [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Il percorso di una risorsa situata nell’archivio AEM Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>È possibile sfogliare l’archivio AEM Forms utilizzando un browser web. Per sfogliare la directory archivio, immetti il seguente URL in un browser Web `https://[server name]:[server port]/repository`. Puoi verificare i risultati di avvio rapido associati alla sezione Utilizzo dell’archivio AEM Forms utilizzando un browser web. Ad esempio, se aggiungi contenuto all’archivio AEM Forms, puoi visualizzarne il contenuto in un browser web. (Vedi [Avvio rapido (modalità SOAP): Scrittura di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

L’API dell’archivio fornisce una serie di operazioni che è possibile utilizzare per memorizzare e recuperare informazioni dall’archivio. Ad esempio, puoi ottenere un elenco di risorse o recuperare risorse specifiche memorizzate nell’archivio quando una risorsa è necessaria durante l’elaborazione di un’applicazione.

>[!NOTE]
>
>L’API dell’archivio non può essere utilizzata per interagire con Content Services (obsoleto). Per interagire con Content Services (obsoleto), utilizza l’API di gestione dei documenti.

Utilizzando l’API del servizio Repository, puoi eseguire le seguenti attività:

* Creare cartelle. Vedi [Creazione di cartelle](aem-forms-repository.md#creating-folders).
* Scrivi risorse e relative proprietà. Vedi [Scrittura delle risorse](aem-forms-repository.md#writing-resources).
* Elencare risorse in una raccolta specifica o correlate ad altre risorse. Vedi [Elencare risorse](aem-forms-repository.md#listing-resources).
* Leggi le risorse e le relative proprietà. Vedi [Lettura delle risorse](aem-forms-repository.md#reading-resources).
* Aggiorna le risorse e le relative proprietà. Vedi [Aggiornamento delle risorse](aem-forms-repository.md#updating-resources).
* Cerca risorse, inclusa la cronologia, le risorse correlate e le proprietà. Vedi [Ricerca di risorse](aem-forms-repository.md#searching-for-resources).
* Specifica le relazioni tra le risorse. Vedi [Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships).
* Gestisci il controllo dell&#39;accesso alle risorse, compresi il blocco e lo sblocco delle risorse, e la lettura e scrittura degli elenchi di controllo accessi (ACL, Access Control List). Vedi [Blocco delle risorse](aem-forms-repository.md#locking-resources).
* Elimina le risorse e le relative proprietà. Vedi [Eliminazione delle risorse](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Utilizzando l’API dell’archivio, non puoi gestire il controllo dell’accesso alle risorse, cercare risorse o specificare relazioni tra le risorse utilizzando un archivio ECM.

>[!NOTE]
>
>Quando un PDF crittografato viene scritto nell’archivio, non è possibile utilizzare la funzione di estrazione della relazione automatica. In caso contrario, un PDF crittografato può essere memorizzato nell’archivio e successivamente recuperato. Il recuperatore può scegliere di decrittografare il PDF dopo averlo recuperato dall’archivio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di cartelle {#creating-folders}

Le cartelle (raccolte di risorse) vengono utilizzate per memorizzare gli oggetti (file o risorse) nei raggruppamenti organizzati. Le cartelle possono contenere risorse e altre cartelle, dette anche sottocartelle. Le risorse possono essere memorizzate solo in una cartella alla volta.

I file ereditano gli elenchi di controllo di accesso (ACL, Access Control List) dalle cartelle e le sottocartelle ereditano gli ACL dalle cartelle principali. Pertanto, le cartelle principali devono esistere prima di poter creare cartelle secondarie. L’IDE consente di interagire solo a livello di cartella per cartella, non a livello di singolo file. Non è possibile eseguire la versione delle cartelle e non è necessario farlo; una cartella non contiene dati stessi. Si tratta piuttosto solo di un contenitore per risorse che contengono dati. L&#39;ACL predefinito è un&#39;autorizzazione a livello di sistema, il che significa che gli utenti devono avere autorizzazioni a livello di sistema (lettura, scrittura, attraversamento, gestione delle ACL) finché qualcuno non gli dà le autorizzazioni per una particolare cartella. Le ACL funzionano solo nell&#39;IDE.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare una cartella, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea il client di servizio.
1. Crea la cartella.
1. Scrivere la cartella nel repository.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter creare una raccolta di risorse a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Crea la cartella**

Richiama il metodo del servizio Repository per creare la raccolta di risorse e compila la raccolta di risorse con informazioni identificative, tra cui UUID, nome della cartella e descrizione.

**Scrivere la cartella nel repository**

Richiama il metodo del servizio Repository per scrivere la raccolta di risorse, specificando l’URI della cartella target.

**Consulta anche**

[Creare cartelle utilizzando l’API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Creare cartelle utilizzando l’API del servizio Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creare cartelle utilizzando l’API Java {#create-folders-using-the-java-api}

Crea una cartella utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi file di progetto nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Crea la cartella

   Per creare una raccolta di risorse, devi innanzitutto creare una `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` oggetto.

   Richiama il `repositoryInfomodelFactoryBean` dell’oggetto `newResourceCollection` e trasmettere i seguenti parametri:

   * A `com.adobe.repository.infomodel.Id` Identificatore UUID da assegnare alla risorsa.
   * A `com.adobe.repository.infomodel.Lid` Identificatore UUID da assegnare alla risorsa.
   * A `java.lang.String` contenente il nome della raccolta di risorse. Esempio: `FormsFolder`.

   Il metodo restituisce un `com.adobe.repository.infomodel.bean.ResourceCollection` oggetto che rappresenta la nuova cartella.

   Imposta la descrizione della cartella utilizzando la `setDescription` e passare il seguente parametro:

   * A `String` descrive la raccolta di risorse. In questo esempio, `"test Folder"` viene utilizzato `.`


1. Scrivere la cartella nel repository

   Richiama il `ResourceRepositoryClient` dell’oggetto `writeResource` e passa l’URI della cartella e il `ResourceCollection` oggetto. Ad esempio, l’URI della cartella può essere il seguente valore `/Applications/FormsApplication/1.0/`.

   Il metodo restituisce un&#39;istanza della nuova creazione `com.adobe.repository.infomodel.bean.Resource` oggetto. Ad esempio, puoi recuperare il valore dell’identificatore della nuova risorsa richiamando il `com.adobe.repository.infomodel.bean.Resource` dell’oggetto `getId` metodo .

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Avvio rapido (modalità SOAP): Creazione di una cartella tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare cartelle utilizzando l’API del servizio Web {#create-folders-using-the-web-service-api}

Crea una cartella utilizzando l’API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il Repository WSDL utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Crea la cartella

   Crea la cartella utilizzando il costruttore predefinito per `ResourceCollection` e trasmettere i seguenti parametri:

   * Un `Id` che viene creato richiamando il costruttore predefinito per il `Id` e assegnati al `Resource` dell’oggetto `id` campo .
   * Un `Lid` che viene creato richiamando il costruttore predefinito per il `Lid` e assegnati al `Resource` dell’oggetto `lid` campo .
   * Una stringa contenente il nome della raccolta di risorse, assegnata alla `Resource` dell’oggetto `name` campo . Il nome utilizzato in questo esempio è `"testfolder"`.
   * Una stringa contenente la descrizione della raccolta di risorse, assegnata alla `Resource` dell’oggetto `description` campo . La descrizione utilizzata in questo esempio è `"test folder"`.

1. Scrivere la cartella nel repository

   Richiama il `RepositoryServiceService` dell’oggetto `writeResource` e trasmettere i seguenti parametri:

   * Percorso in cui creare la cartella.
   * La `ResourceCollection` oggetto che rappresenta la cartella.
   * Pass `null` per gli altri due parametri.

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Scrittura delle risorse {#writing-resources}

Puoi creare risorse in una determinata posizione nell’archivio. La dimensione naturale del file è soggetta a limitazioni del database e al timeout della sessione. Per la configurazione predefinita, i file sono limitati a 25 MB. Per aumentare o ridurre la dimensione massima del file, è necessario modificare la configurazione del database.

La scrittura di risorse equivale all’archiviazione dei dati nell’archivio. Una volta scritta una risorsa nell’archivio, questa diventa accessibile a tutti i client nell’ecosistema dell’archivio. Quando scrivi risorse nell’archivio, come schemi XML, file XDP e file XSD, i contenuti vengono analizzati in base al tipo MIME. Se il tipo MIME è supportato, il parser determina se esiste una relazione implicita con altri contenuti. Ad esempio, se un foglio di stile CSS ha un URL relativo che fa riferimento a un CSS comune, si prevede di inviare anche il CSS comune nell’archivio. La relazione tra le due risorse viene memorizzata come relazione in sospeso per un periodo non regolabile di 30 giorni. Quando invii il CSS comune all’archivio entro un periodo di 30 giorni, la relazione viene formata.

Quando crei una risorsa, l’elenco di controllo accessi (ACL) viene ereditato dalla cartella principale. La cartella principale dispone di autorizzazioni a livello di sistema fino alla creazione di una risorsa o di una cartella iniziale, in cui alla risorsa o alla cartella vengono assegnate le autorizzazioni ACL predefinite.

Puoi scrivere le risorse in modo programmatico utilizzando l’API Java del servizio Repository o l’API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per scrivere una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Repository.
1. Specifica l’URI della risorsa da leggere.
1. Leggi la risorsa .

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter leggere una risorsa in modo programmatico, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Specifica l’URI della cartella di destinazione per la risorsa**

Crea una stringa contenente l’URI della risorsa da leggere. La sintassi include le barre, come in questo esempio: &quot;/*path*/*cartella*&quot;.

**Creare la risorsa**

Richiama il metodo del servizio Repository per creare la risorsa e compila la risorsa con informazioni identificative, compreso il suo UUID, il nome della risorsa e la descrizione.

**Specifica il contenuto della risorsa**

Richiama il metodo del servizio Repository per creare il contenuto della risorsa e archiviarlo nella risorsa.

**Scrivere la risorsa nella cartella di destinazione**

Richiama il metodo del servizio Repository per scrivere la risorsa, specificando l’URI della cartella di destinazione.

**Consulta anche**

[Scrivere risorse utilizzando l’API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Creazione di risorse tramite l’API del servizio Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Scrivere risorse utilizzando l’API Java {#write-resources-using-the-java-api}

Scrivere una risorsa utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica l’URI della cartella di destinazione per la risorsa

   Specifica l’URI della cartella di destinazione per la risorsa. In questo caso, perché la risorsa denominata `testResource` verranno memorizzati nella cartella denominata `testFolder`, l’URI della cartella è `"/testFolder"`. L’URI viene memorizzato come `java.lang.String` oggetto.

1. Creare la risorsa

   Per creare una risorsa, devi innanzitutto creare una `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` oggetto.

   Richiama il `RepositoryInfomodelFactoryBean` dell’oggetto `newResource` che crea un `com.adobe.repository.infomodel.bean.Resource` oggetto. In questo esempio vengono forniti i seguenti parametri:

   * A `com.adobe.repository.infomodel.Id` che viene creato richiamando il costruttore predefinito per il `Id` classe.
   * A `com.adobe.repository.infomodel.Lid` che viene creato richiamando il costruttore predefinito per il `Lid` classe.
   * A `java.lang.String` contenente il nome file della risorsa.

   Per specificare la descrizione della risorsa, invoca la `Resource` dell’oggetto `setDescription` e passare una stringa contenente la descrizione. In questo esempio, la descrizione è `"test resource"`.

1. Specifica il contenuto della risorsa

   Per creare contenuto per la risorsa, invoca la `RepositoryInfomodelFactoryBean` dell’oggetto `newResourceContent` che restituisce un `com.adobe.repository.infomodel.bean.ResourceContent` oggetto. Aggiungi contenuto a `ResourceContent` oggetto. In questo esempio, questa operazione viene eseguita eseguendo le seguenti attività:

   * Richiamo del `ResourceContent` dell’oggetto `setDataDocument` e la trasmissione di un `com.adobe.idp.Document` oggetto
   * Richiamo del `ResourceContent` dell’oggetto `setSize` e il passaggio delle dimensioni in byte del `Document` oggetto

   Aggiungi il contenuto alla risorsa richiamando il `Resource` dell’oggetto `setContent` e di passare `ResourceContent` oggetto. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Scrivere la risorsa nella cartella di destinazione

   Richiama il `ResourceRepositoryClient` dell’oggetto `writeResource` e passare l&#39;URI della cartella, nonché il `Resource` oggetto.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Avvio rapido (modalità SOAP): Scrittura di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di risorse tramite l’API del servizio Web {#write-resources-using-the-web-service-api}

Scrivere una risorsa utilizzando l’API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il Repository WSDL utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specifica l’URI della cartella di destinazione per la risorsa

   Specifica l’URI della cartella di destinazione per la risorsa. In questo caso, perché la risorsa denominata `testResource` verranno memorizzati nella cartella denominata `testFolder`, l’URI della cartella è `"/testFolder"`. Quando si utilizza un linguaggio conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Creare la risorsa

   Per creare una risorsa, richiamare il costruttore predefinito per `Resource` classe. In questo esempio, le seguenti informazioni vengono memorizzate in `Resource` oggetto:

   * A `com.adobe.repository.infomodel.Id` che viene creato richiamando il costruttore predefinito per il `Id` e assegnati al `Resource` dell’oggetto `id` campo .
   * A `com.adobe.repository.infomodel.Lid` che viene creato richiamando il costruttore predefinito per il `Lid` e assegnati al `Resource` dell’oggetto `lid` campo .
   * Una stringa contenente il nome file della risorsa, che viene assegnata alla `Resource` dell’oggetto `name` campo . Il nome utilizzato in questo esempio è `"testResource"`.
   * Una stringa contenente la descrizione della risorsa, assegnata alla `Resource` dell’oggetto `description` campo . La descrizione utilizzata in questo esempio è `"test resource"`.

1. Specifica il contenuto della risorsa

   Per creare contenuto per la risorsa, invoca il costruttore predefinito per `ResourceContent` classe. Quindi aggiungi il contenuto al `ResourceContent` oggetto. In questo esempio, questa operazione viene eseguita eseguendo le seguenti attività:

   * Assegnazione di un `BLOB` oggetto contenente un documento `ResourceContent` dell’oggetto `dataDocument` campo .
   * Assegnazione delle dimensioni in byte del `BLOB` dell&#39;oggetto `ResourceContent` dell’oggetto `size` campo .

   Aggiungi il contenuto alla risorsa assegnando il `ResourceContent` dell&#39;oggetto `Resource` dell’oggetto `content` campo .

1. Scrivere la risorsa nella cartella di destinazione

   Richiama il `RepositoryServiceService` dell’oggetto `writeResource` e passare l&#39;URI della cartella, nonché il `Resource` oggetto. Pass `null` per gli altri due parametri.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Elencare risorse {#listing-resources}

Puoi individuare le risorse elencando le risorse. Viene eseguita una query sull’archivio per trovare tutte le risorse correlate a una determinata raccolta di risorse.

Una volta organizzate le risorse, è possibile esaminare la struttura creata visualizzando un particolare ramo della struttura, come si farebbe in un sistema operativo.

Le risorse di elenco operano per relazione: Le risorse sono membri di cartelle. L&#39;appartenenza è rappresentata da una relazione di tipo &quot;membro di&quot;. Quando elenchi le risorse in una determinata cartella, esegui una query per individuare le risorse correlate a una determinata cartella dalla relazione &quot;membro di&quot;. Le relazioni sono direzionali: un membro di una relazione ha un&#39;origine che è membro del target. L&#39;origine è la risorsa; la destinazione è la cartella principale.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per elencare le risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea il client di servizio.
1. Specifica il percorso della cartella.
1. Recupera l’elenco delle risorse.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter creare una raccolta di risorse a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Specifica il percorso della cartella**

Crea una stringa contenente il percorso della cartella contenente le risorse. La sintassi include le barre, come in questo esempio: &quot;/*path*/*cartella*&quot;.

**Recupera l’elenco delle risorse**

Richiama il metodo del servizio Repository per recuperare l’elenco delle risorse, specificando il percorso della cartella target.

**Consulta anche**

[Elencare le risorse utilizzando l’API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Elencare risorse tramite l’API del servizio Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Elencare le risorse utilizzando l’API Java {#list-resources-using-the-java-api}

Elencare le risorse utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica il percorso della cartella

   Specifica l’URI della raccolta di risorse da interrogare. In questo caso, il relativo URI è `"/testFolder"`. L’URI viene memorizzato come `java.lang.String` oggetto.

1. Recupera l’elenco delle risorse

   Richiama il `ResourceRepositoryClient` dell’oggetto `listMembers` e passare l&#39;URI della cartella.

   Il metodo restituisce un `java.util.List` di `com.adobe.repository.infomodel.bean.Resource` oggetti che sono la sorgente di un `com.adobe.repository.infomodel.bean.Relation` di tipo `Relation.TYPE_MEMBER_OF` e usa l’URI di raccolta risorse come destinazione. È possibile eseguire iterazioni `List` per recuperare ciascuna delle risorse. In questo esempio vengono visualizzati il nome e la descrizione di ciascuna risorsa.

**Consulta anche**

[Elencare risorse](aem-forms-repository.md#listing-resources).

[Avvio rapido (modalità SOAP): Inserimento di risorse nell’elenco tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Elencare risorse tramite l’API del servizio Web {#list-resources-using-the-web-service-api}

Elencare le risorse utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL dell&#39;archivio.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specifica il percorso della cartella

   Specifica una stringa contenente l’URI della cartella da interrogare. In questo caso, il relativo URI è `"/testFolder"`. Quando si utilizza un linguaggio conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Recupera l’elenco delle risorse

   Richiama il `RepositoryServiceService` dell’oggetto `listMembers` e passa l’URI della cartella come primo parametro. Pass `null` per gli altri due parametri.

   Il metodo restituisce una matrice di oggetti a cui è possibile eseguire il cast `Resource` oggetti. È possibile eseguire iterazioni attraverso l’array di oggetti per recuperare ciascuna delle risorse correlate. In questo esempio vengono visualizzati il nome e la descrizione di ciascuna risorsa.

**Consulta anche**

[Elencare risorse](aem-forms-repository.md#listing-resources).

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Lettura delle risorse {#reading-resources}

Puoi recuperare risorse da una determinata posizione nell’archivio per leggerne il contenuto e i metadati. Il flusso di lavoro è preceduto da un modulo di inizializzazione. Il processo dispone di tutte le autorizzazioni necessarie per leggere il modulo. Il sistema recupera il modulo dati e legge il contenuto dal repository. L’archivio consente l’accesso al contenuto e ai metadati (la possibilità di sapere che la risorsa esiste).

L’archivio dispone dei seguenti quattro tipi di autorizzazioni:

* **traverse**: consente di elencare le risorse; ovvero per leggere i metadati delle risorse, ma non il contenuto delle risorse
* **read**: consente di leggere il contenuto delle risorse
* **scrivere**: consente di scrivere il contenuto delle risorse
* **gestione degli elenchi di controllo accessi (ACL)**: consente di manipolare ACL sulle risorse

Gli utenti possono eseguire i processi solo quando dispongono delle autorizzazioni necessarie per eseguire il processo. Per eseguire la sincronizzazione con l’archivio, gli utenti IDE devono disporre di autorizzazioni di lettura e lettura. Le ACL si applicano solo in fase di progettazione perché il runtime si verifica all&#39;interno del contesto di sistema.

Puoi leggere le risorse in modo programmatico utilizzando l’API Java del servizio Repository o l’API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per leggere una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Repository.
1. Specifica l’URI della risorsa da leggere.
1. Leggi la risorsa .

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter leggere una risorsa in modo programmatico, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Specifica l’URI della risorsa da leggere**

Crea una stringa contenente l’URI della risorsa da leggere. La sintassi include le barre, come in questo esempio: &quot;/*path*/*risorsa*&quot;.

**Leggi la risorsa**

Richiama il metodo del servizio Repository per leggere la risorsa, specificando l&#39;URI.

**Consulta anche**

[Leggi le risorse tramite l’API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lettura delle risorse tramite l’API del servizio Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Leggi le risorse tramite l’API Java {#read-resources-using-the-java-api}

Leggi una risorsa utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica l’URI della risorsa da leggere

   Specifica un valore stringa che rappresenta l’URI della risorsa da recuperare. Ad esempio, supponendo che la risorsa sia denominata *testResource* che si trova in una cartella denominata *testFolder*, specifica `/testFolder/testResource`.

1. Leggi la risorsa

   Richiama il `ResourceRepositoryClient` dell’oggetto `readResource` e passa l’URI della risorsa come parametro. Questo metodo restituisce un `Resource` istanza che rappresenta la risorsa.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Avvio rapido (modalità SOAP): Lettura di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lettura delle risorse tramite l’API del servizio Web {#reading-resources-using-the-web-service-api}

Leggi una risorsa utilizzando l’API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL dell&#39;archivio. (Vedi [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedi [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specifica l’URI della risorsa da leggere

   Specifica una stringa contenente l’URI della risorsa da recuperare. In questo caso, perché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il suo URI è `"/testFolder/testResource"`. Quando si utilizza un linguaggio conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Leggi la risorsa

   Richiama il `RepositoryServiceService` dell’oggetto `readResource` e passa l’URI della risorsa come primo parametro. Pass `null` per gli altri due parametri.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Aggiornamento delle risorse {#updating-resources}

Puoi recuperare e aggiornare il contenuto delle risorse nella directory archivio. Quando aggiorni le risorse, il controllo di accesso a tali risorse rimane invariato tra le versioni. Quando si esegue un aggiornamento, è possibile incrementare la versione principale. Se non scegli di incrementare la versione principale, la versione secondaria viene aggiornata automaticamente.

Quando aggiorni una risorsa, la nuova versione viene creata in base agli attributi di risorsa specificati. Quando aggiorni una risorsa, specifichi due parametri importanti: l’URI di destinazione e un’istanza di risorsa contenente tutti i metadati aggiornati. È importante notare che se non stai modificando un dato attributo (ad esempio, il nome), l&#39;attributo è ancora richiesto nell&#39;istanza passata. Le relazioni create durante l’analisi del contenuto vengono aggiunte alla versione specifica e non vengono portate avanti a meno che non sia specificato.

Ad esempio, se aggiorni un file XDP che contiene riferimenti ad altre risorse, verranno registrati anche tali riferimenti aggiuntivi. Supponiamo che form.xdp versione 1.0 abbia due riferimenti esterni: un logo e un foglio di stile e successivamente si aggiorna form.xdp in modo che ora abbia tre riferimenti: un logo, un foglio di stile e un file di schema. Durante l&#39;aggiornamento, il repository aggiungerà la terza relazione (al file di schema) alla sua tabella di relazione in sospeso. Una volta che il file di schema è presente nell&#39;archivio, la relazione viene formata automaticamente. Tuttavia, se form.xdp versione 2.0 non utilizza più il logo, la versione 2.0 di form.xdp non avrà alcuna relazione con il logo.

Tutte le operazioni di aggiornamento sono atomiche e transazionali. Ad esempio, se due utenti leggono la stessa risorsa ed entrambi decidono di aggiornare la versione 1.0 alla versione 2.0, uno avrà successo e uno di loro avrà esito negativo, verrà mantenuta l’integrità dell’archivio e a entrambi verrà visualizzato un messaggio di conferma del successo o dell’errore. Se la transazione non si esegue il commit, eseguirà il rollback in caso di errore del database e si verificherà il timeout o il rollback a seconda del server dell&#39;applicazione.

Puoi aggiornare programmaticamente le risorse utilizzando l’API Java del servizio Repository o l’API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per aggiornare una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Repository.
1. Recupera la risorsa da aggiornare.
1. Aggiorna la risorsa.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter leggere una risorsa in modo programmatico, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Recupera la risorsa da aggiornare**

Leggi la risorsa . Per ulteriori informazioni, consulta [Lettura delle risorse](aem-forms-repository.md#reading-resources).

**Aggiorna la risorsa**

Imposta le nuove informazioni nella risorsa e richiama il metodo del servizio Repository per aggiornare la risorsa, specificando l’URI, la risorsa aggiornata e la modalità di aggiornamento delle informazioni sulla versione.

**Consulta anche**

[Aggiornare le risorse utilizzando l’API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Aggiornare le risorse utilizzando l’API del servizio Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Aggiornare le risorse utilizzando l’API Java {#update-resources-using-the-java-api}

Aggiornare una risorsa utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Recupera la risorsa da aggiornare

   Specifica l’URI della risorsa da recuperare e leggere. In questo esempio, l’URI della risorsa è `"/testFolder/testResource"`.

1. Aggiorna la risorsa

   Aggiorna `Resource` informazioni sull’oggetto. In questo esempio, per aggiornare la descrizione, richiama il `Resource` dell’oggetto `setDescription` e passare la nuova stringa di descrizione come parametro.

   Quindi invoca il `ServiceClientFactory` dell’oggetto `updateResource` e trasmettere i seguenti parametri:

   * A `java.lang.String` oggetto contenente l’URI della risorsa.
   * La `Resource` oggetto contenente le informazioni aggiornate sulla risorsa.
   * A `boolean` valore che indica se aggiornare la versione principale o secondaria. In questo esempio, un valore di `true` viene trasmesso per indicare che la versione principale deve essere incrementata.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Avvio rapido (modalità SOAP): Aggiornamento di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiornare le risorse utilizzando l’API del servizio Web {#update-resources-using-the-web-service-api}

Aggiornare una risorsa utilizzando l’API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL dell&#39;archivio.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Recupera la risorsa da aggiornare

   Specifica l’URI della risorsa da recuperare e legge la risorsa. In questo esempio, l’URI della risorsa è `"/testFolder/testResource"`. Per ulteriori informazioni, consulta [Lettura delle risorse](aem-forms-repository.md#reading-resources).

1. Aggiorna la risorsa

   Aggiorna `Resource` informazioni sull’oggetto. In questo esempio, per aggiornare la descrizione, assegna un nuovo valore al `Resource` dell’oggetto `description` campo .

1. Richiama il `RepositoryServiceService` dell’oggetto `updateResource` e trasmettere i seguenti parametri:

   * A `System.String` oggetto contenente l’URI della risorsa.
   * La `Resource` oggetto contenente le informazioni aggiornate sulla risorsa.
   * A `boolean` valore che indica se aggiornare la versione principale o secondaria. In questo esempio, un valore di `true` viene trasmesso per indicare che la versione principale deve essere incrementata.
   * Pass `null` per i due parametri rimanenti.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ricerca di risorse {#searching-for-resources}

È possibile creare query utilizzate per cercare risorse nell’archivio, inclusi cronologia, risorse correlate e proprietà.

È possibile recuperare le risorse correlate per determinare le dipendenze tra un modulo e i relativi frammenti. Ad esempio, se si dispone di un modulo è possibile determinare quali frammenti o risorse esterne utilizza. Se disponi di un’immagine, puoi anche scoprire quali moduli utilizzano l’immagine. Puoi anche cercare risorse correlate utilizzando un filtro basato sulle proprietà. Ad esempio, è possibile cercare tutti i moduli che utilizzano un’immagine con un nome specificato o trovare un’immagine utilizzata da un modulo con un nome specifico. Puoi anche eseguire ricerche utilizzando le proprietà delle risorse. Ad esempio, è possibile eseguire una query per trovare tutte le maschere o le risorse il cui nome inizia con una stringa che può includere i caratteri jolly ’%’ e ’_’. Ricorda che le ricerche basate sulle proprietà non sono basate sulle relazioni; tali ricerche si basano sul presupposto che tu disponga di conoscenze specifiche su una determinata risorsa.

**Istruzioni di query**

A *query* contiene una o più istruzioni collegate logicamente con condizioni. A *dichiarazione* è costituito da un operando sinistro, un operatore e un operando destro. Inoltre, puoi specificare l’ordinamento da utilizzare per i risultati della ricerca. La *ordinamento* contiene informazioni equivalenti a un SQL `ORDER BY` ed è composto da elementi che contengono gli attributi su cui si è basata la ricerca, nonché un valore che indica se utilizzare l&#39;ordine crescente o decrescente.

Puoi cercare le risorse in modo programmatico utilizzando l’API Java del servizio Repository. Al momento, non è possibile utilizzare l’API del servizio Web per cercare le risorse.

**Comportamento dell&#39;ordinamento**

L&#39;ordinamento non viene rispettato quando si richiama il `ResourceRepositoryClient` dell’oggetto `searchProperties` e specificando un ordinamento. Ad esempio, supponiamo di creare una risorsa con tre proprietà personalizzate, in cui i nomi degli attributi sono `name`, `secondName`e `asecondName`. Successivamente, crei un elemento di ordinamento sul nome dell&#39;attributo e imposta il `ascending` valore a `true`.

Quindi invoca il `ResourceRepositoryClient` dell’oggetto `searchProperties` e passare l&#39;ordinamento. La ricerca restituisce la risorsa corretta, con le tre proprietà . Tuttavia, le proprietà non vengono ordinate in base al nome dell&#39;attributo. Vengono restituiti nell’ordine in cui sono stati aggiunti: `name`, `secondName`e `asecondName`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per cercare le risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Repository.
1. Specifica la cartella di destinazione per la ricerca.
1. Specifica gli attributi utilizzati nella ricerca.
1. Crea la query utilizzata nella ricerca.
1. Crea l’ordinamento per i risultati della ricerca.
1. Cerca le risorse.
1. Recupera le risorse dal risultato della ricerca.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter leggere una risorsa in modo programmatico, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Specifica la cartella di destinazione per la ricerca**

Crea una stringa contenente il percorso di base da cui eseguire la ricerca. La sintassi include le barre, come in questo esempio: &quot;/*path*/*cartella*&quot;.

**Specifica gli attributi utilizzati nella ricerca**

Puoi basare la ricerca sugli attributi contenuti nelle risorse. Specifica i valori degli attributi su cui eseguire la ricerca.

**Crea la query utilizzata nella ricerca**

Crea una query utilizzando istruzioni e condizioni. Ogni istruzione specifica l&#39;attributo su cui basare la ricerca, la condizione da utilizzare e il valore dell&#39;attributo da utilizzare nella ricerca.

**Creare l’ordinamento dei risultati della ricerca**

L’ordinamento è composto da elementi, ciascuno dei quali contiene uno degli attributi utilizzati nella ricerca e un valore che indica se deve essere utilizzato l’ordine crescente o decrescente.

**Cercare le risorse**

Cerca le risorse utilizzando la cartella, la query e l’ordinamento. Inoltre, indicare la profondità della ricerca e un limite superiore al numero di risultati da restituire.

**Recupera le risorse dal risultato della ricerca**

Itera l’elenco delle risorse restituite ed estrae le informazioni per un’ulteriore elaborazione.

**Consulta anche**

[Cercare risorse utilizzando l’API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Cercare risorse utilizzando l’API Java {#search-for-resources-using-the-java-api}

Cerca una risorsa utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica la cartella di destinazione per la ricerca

   Specificare l&#39;URI del percorso di base da cui eseguire la ricerca. In questo esempio, l’URI della risorsa è `/testFolder`.

1. Specifica gli attributi utilizzati nella ricerca

   Specifica i valori degli attributi su cui eseguire la ricerca. Gli attributi esistono all’interno di un `com.adobe.repository.infomodel.bean.Resource` oggetto. In questo esempio, la ricerca verrà condotta sull&#39;attributo name; pertanto, un `java.lang.String` contenente `Resource` viene utilizzato il nome dell’oggetto, ovvero `testResource` in questo caso.

1. Crea la query utilizzata nella ricerca

   Per creare una query, crea una `com.adobe.repository.query.Query` richiamando il costruttore predefinito per il `Query` e aggiungere istruzioni alla query.

   Per creare un&#39;istruzione, richiamare il costruttore per `com.adobe.repository.query.Query.Statement` e trasmettere i seguenti parametri:

   * Un operando sinistro contenente la costante attributo della risorsa. In questo esempio, poiché il nome della risorsa viene utilizzato come base per la ricerca, il valore statico `Resource.ATTRIBUTE_NAME` viene utilizzato.
   * Operatore che contiene la condizione utilizzata nella ricerca dell’attributo. L&#39;operatore deve essere una delle costanti statiche nel `Query.Statement` classe. In questo esempio, il valore statico `Query.Statement.OPERATOR_BEGINS_WITH` viene utilizzato.
   * Un operando a destra contenente il valore dell&#39;attributo su cui eseguire la ricerca. In questo esempio, l&#39;attributo name, un `String` contenente il valore `"testResource"`, viene utilizzato.

   Specifica lo spazio dei nomi dell&#39;operando di sinistra richiamando il `Query.Statement` dell’oggetto `setNamespace` e il passaggio di uno dei valori statici contenuti nel `com.adobe.repository.infomodel.bean.ResourceProperty` classe. In questo esempio, viene utilizzato `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`.

   Aggiungi ogni istruzione alla query richiamando il `Query` dell’oggetto `addStatement` e di passare `Query.Statement` oggetto.

1. Creare l’ordinamento dei risultati della ricerca

   Per specificare l’ordinamento utilizzato nei risultati della ricerca, crea un `com.adobe.repository.query.sort.SortOrder` richiamando il costruttore predefinito per il `SortOrder` e aggiungere elementi all&#39;ordinamento.

   Per creare un elemento per l&#39;ordinamento, richiamare uno dei costruttori per `com.adobe.repository.query.sort.SortOrder.Element` classe. In questo esempio, poiché il nome della risorsa viene utilizzato come base per la ricerca, il valore statico `Resource.ATTRIBUTE_NAME` viene utilizzato come primo parametro e come ordine crescente (a `boolean` valore `true`) viene specificato come secondo parametro.

   Aggiungi ogni elemento all’ordinamento richiamando il `SortOrder` dell’oggetto `addSortElement` e di passare `SortOrder.Element` oggetto.

1. Cercare le risorse

   Per cercare `resources` in base alle proprietà dell&#39;attributo, richiama il `ResourceRepositoryClient` dell’oggetto `searchProperties` e trasmettere i seguenti parametri:

   * A `String` contenente il percorso base da cui eseguire la ricerca. In questo caso, `"/testFolder"` viene utilizzato.
   * Query utilizzata nella ricerca.
   * Profondità della ricerca. In questo caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` viene utilizzato per indicare che il percorso di base e tutte le relative cartelle devono essere utilizzati.
   * Un `int` valore che indica la prima riga da cui selezionare il set di risultati non di paging. In questo esempio, `0` è specificato.
   * Un `int` valore che indica il numero massimo di risultati da restituire. In questo esempio, `10` è specificato.
   * Ordine utilizzato nella ricerca.

   Il metodo restituisce un `java.util.List` di `Resource` oggetti nell&#39;ordinamento specificato.

1. Recupera le risorse dal risultato della ricerca

   Per recuperare le risorse contenute nel risultato della ricerca, eseguire un&#39;iterazione attraverso `List` e di eseguire il cast di ogni oggetto in un `Resource` per estrarre le informazioni. In questo esempio viene visualizzato il nome di ogni risorsa.

**Consulta anche**

[Ricerca di risorse](aem-forms-repository.md#searching-for-resources)

[Avvio rapido (modalità SOAP): Ricerca di risorse tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creazione di relazioni tra risorse {#creating-resource-relationships}

Puoi specificare le relazioni tra le risorse nella directory archivio. Ci sono tre tipi di relazioni:

* **Dipendenza**: una relazione in cui una risorsa dipende da altre risorse, il che significa che tutte le relative risorse sono necessarie nell’archivio.
* **Appartenenza (file system)**: una relazione in cui una risorsa si trova all&#39;interno di una determinata cartella.
* **Personalizzato**: una relazione specificata tra le risorse. Ad esempio, se una risorsa è stata dichiarata obsoleta e un’altra è stata introdotta nell’archivio, puoi specificare una relazione di sostituzione personalizzata.

Puoi creare relazioni personalizzate. Ad esempio, se si archivia un file HTML nel repository e si utilizza un’immagine, è possibile specificare una relazione personalizzata per correlare il file HTML all’immagine (poiché in genere solo i file XML sono associati alle immagini utilizzando una relazione di dipendenza definita dal repository). Un altro esempio di relazione personalizzata è se desideri creare una visualizzazione diversa dell’archivio con una struttura ad albero a grafico ciclico invece che una struttura ad albero. Puoi definire un grafico circolare insieme a un visualizzatore per attraversare tali relazioni. Infine, puoi indicare che una risorsa sostituisce un’altra risorsa anche se le due risorse sono completamente diverse. In tal caso, puoi definire un tipo di relazione al di fuori dell’intervallo riservato e creare una relazione tra queste due risorse. La tua applicazione sarebbe l&#39;unico cliente in grado di rilevare ed elaborare la relazione e potrebbe essere utilizzato per condurre ricerche su tale relazione.

Puoi specificare a livello di programmazione le relazioni tra le risorse utilizzando l’API Java del servizio archivio o l’API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per specificare una relazione tra due risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Repository.
1. Specifica gli URI delle risorse da correlare.
1. Crea la relazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter leggere una risorsa in modo programmatico, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Specifica gli URI delle risorse da correlare**

Crea stringhe contenenti gli URI della risorsa da correlare. La sintassi include le barre, come in questo esempio: &quot;/*path*/*risorsa*&quot;.

**Creare la relazione**

Richiamare il metodo del servizio Repository per creare e specificare il tipo di relazione.

**Consulta anche**

[Creare risorse sulle relazioni utilizzando l’API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Creare risorse sulle relazioni utilizzando l’API del servizio Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creare risorse sulle relazioni utilizzando l’API Java {#create-relationship-resources-using-the-java-api}

Crea risorse sulle relazioni utilizzando l’API Java del servizio Repository ed esegui le seguenti attività:

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica gli URI delle risorse da correlare

   Specifica gli URI delle risorse da correlare. In questo caso, perché le risorse sono denominate `testResource1` e `testResource2` e si trovano nella cartella denominata `testFolder`, gli URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Gli URI vengono memorizzati come `java.lang.String` oggetti. In questo esempio, le risorse vengono scritte per la prima volta nella directory archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, consulta [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiama il `ResourceRepositoryClient` dell’oggetto `createRelationship` e trasmettere i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Il tipo di relazione, che è una delle costanti statiche nel `com.adobe.repository.infomodel.bean.Relation` classe. In questo esempio, viene stabilita una relazione di dipendenza specificando il valore `Relation.TYPE_DEPENDANT_OF`.
   * A `boolean` valore che indica se la risorsa target viene aggiornata automaticamente nel `com.adobe.repository.infomodel.Id`Identificatore basato su -della nuova risorsa head. In questo esempio, a causa della relazione di dipendenza, il valore `true` è specificato.

   È inoltre possibile recuperare un elenco delle risorse correlate per una determinata risorsa richiamando il `ResourceRepositoryClient` dell’oggetto `getRelated` e passando i seguenti parametri:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio, la risorsa di origine ( `"/testFolder/testResource1"`) è specificato.
   * A `boolean` valore che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché questo è il caso.
   * Il tipo di relazione, che è una delle costanti statiche nel `Relation` classe. In questo esempio, una relazione di dipendenza viene specificata utilizzando lo stesso valore utilizzato in precedenza: `Relation.TYPE_DEPENDANT_OF`.

   La `getRelated` restituisce un `java.util.List` di `Resource` oggetti attraverso i quali è possibile eseguire iterazioni per recuperare ciascuna delle risorse correlate, colmando gli oggetti contenuti nel `List` a `Resource` come fai tu. In questo esempio, `testResource2` nell’elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Avvio rapido (modalità SOAP): Creazione di relazioni tra le risorse tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare risorse sulle relazioni utilizzando l’API del servizio Web {#create-relationship-resources-using-the-web-service-api}

Creare risorse sulle relazioni utilizzando l’API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL dell&#39;archivio.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specifica gli URI delle risorse da correlare

   Specifica gli URI delle risorse da correlare. In questo caso, perché le risorse sono denominate `testResource1` e `testResource2` e si trovano nella cartella denominata `testFolder`, gli URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Quando si utilizza un linguaggio conforme a Microsoft .NET Framework (ad esempio, C#), gli URI vengono memorizzati come `System.String` oggetti. In questo esempio, le risorse vengono scritte per la prima volta nella directory archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, consulta [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiama il `RepositoryServiceService` dell’oggetto `createRelationship` e trasmettere i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Tipo di relazione. In questo esempio, viene stabilita una relazione di dipendenza specificando il valore `3`.
   * A `boolean` valore che indica se è stato specificato il tipo di relazione. In questo esempio, il valore `true` è specificato.
   * A `boolean` valore che indica se la risorsa target viene aggiornata automaticamente nel `Id`Identificatore basato su -della nuova risorsa head. In questo esempio, a causa della relazione di dipendenza, il valore `true` è specificato.
   * A `boolean` valore che indica se l&#39;intestazione di destinazione è stata specificata. In questo esempio, il valore `true` è specificato.
   * Pass `null` per l’ultimo parametro.

   È inoltre possibile recuperare un elenco delle risorse correlate per una determinata risorsa richiamando il `RepositoryServiceService` dell’oggetto `getRelated` e passando i seguenti parametri:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio, la risorsa di origine ( `"/testFolder/testResource1"`) è specificato.
   * A `boolean` valore che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché questo è il caso.
   * A `boolean` valore che indica se la risorsa di origine è stata specificata. In questo esempio, il valore `true` è fornito.
   * Matrice di numeri interi contenente i tipi di relazione. In questo esempio, viene specificata una relazione di dipendenza utilizzando lo stesso valore nell&#39;array utilizzato in precedenza: `3`.
   * Pass `null` per i due parametri rimanenti.

   La `getRelated` restituisce un array di oggetti su cui è possibile eseguire il cast `Resource` oggetti attraverso i quali è possibile eseguire iterazioni per recuperare ciascuna delle risorse correlate. In questo esempio, `testResource2` nell’elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Blocco delle risorse {#locking-resources}

È possibile bloccare una risorsa o un insieme di risorse per l&#39;uso esclusivo da parte di un particolare utente o per uso condiviso tra più di un utente. Un blocco condiviso indica che qualcosa succederà alla risorsa, ma non impedisce a nessun altro di intraprendere azioni con tale risorsa. Un blocco condiviso dovrebbe essere considerato un meccanismo di segnalazione. Un blocco esclusivo significa che l’utente che ha bloccato la risorsa cambierà la risorsa e il blocco assicura che nessun altro possa farlo finché l’utente non avrà più bisogno dell’accesso alla risorsa e non avrà rilasciato il blocco. Se un amministratore del repository sblocca una risorsa, tutti i blocchi esclusivi e condivisi su tale risorsa verranno automaticamente rimossi. Questo tipo di azione è destinato alle situazioni in cui un utente non è più disponibile e non ha sbloccato la risorsa.

Quando una risorsa è bloccata, quando visualizzi la scheda Risorse di Workbench viene visualizzata un’icona a forma di lucchetto, come illustrato di seguito.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Puoi controllare programmaticamente l’accesso alle risorse utilizzando l’API Java del servizio Repository o l’API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per bloccare e sbloccare le risorse, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Repository.
1. Specifica l’URI della risorsa da bloccare.
1. Blocca la risorsa.
1. Recupera i blocchi per la risorsa.
1. Sblocca la risorsa

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter leggere una risorsa in modo programmatico, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Specifica l’URI della risorsa da bloccare**

Crea una stringa contenente l’URI della risorsa da bloccare. La sintassi include le barre, come in questo esempio: &quot;/*path*/*risorsa*&quot;.

**Bloccare la risorsa**

Richiama il metodo del servizio Repository per bloccare la risorsa, specificando l&#39;URI, il tipo di blocco e la profondità di blocco.

**Recupera i blocchi per la risorsa**

Richiama il metodo del servizio Repository per recuperare i blocchi per la risorsa, specificando l’URI.

**Sblocca la risorsa**

Richiama il metodo del servizio Repository per sbloccare la risorsa, specificando l&#39;URI.

**Consulta anche**

[Bloccare le risorse utilizzando l’API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Blocco delle risorse tramite l’API del servizio Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Bloccare le risorse utilizzando l’API Java {#lock-resources-using-the-java-api}

Bloccare le risorse utilizzando l’API del servizio Repository (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica l’URI della risorsa da bloccare

   Specifica l’URI della risorsa da bloccare. In questo caso, perché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il suo URI è `"/testFolder/testResource"`. L’URI viene memorizzato come `java.lang.String` oggetto.

1. Bloccare la risorsa

   Richiama il `ResourceRepositoryClient` dell’oggetto `lockResource` e trasmettere i seguenti parametri:

   * URI della risorsa.
   * L&#39;ambito di blocco. In questo esempio, poiché la risorsa verrà bloccata per uso esclusivo, l’ambito del blocco viene specificato come `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * La profondità di blocco. In questo esempio, poiché il blocco viene applicato solo alla risorsa specifica e nessuno dei relativi membri o elementi secondari, la profondità di blocco viene specificata come `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La versione sovraccaricata del `lockResource` metodo che richiede quattro parametri genera un&#39;eccezione. Assicurati di utilizzare `lockResource` che richiede tre parametri come mostrato in questa procedura dettagliata.

1. Recupera i blocchi per la risorsa

   Richiama il `ResourceRepositoryClient` dell’oggetto `getLocks` e passa l’URI della risorsa come parametro. Il metodo restituisce un elenco di oggetti Lock attraverso i quali è possibile eseguire iterazioni. In questo esempio, il proprietario del blocco, la profondità e l’ambito vengono stampati per ogni oggetto richiamando l’opzione di ogni oggetto Lock `getOwnerUserId`, `getDepth`e `getType` metodi, rispettivamente.

1. Sblocca la risorsa

   Richiama il `ResourceRepositoryClient` dell’oggetto `unlockResource` e passa l’URI della risorsa come parametro. Per ulteriori informazioni, consulta la sezione [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Avvio rapido (modalità SOAP): Blocco di una risorsa tramite API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Blocco delle risorse tramite l’API del servizio Web {#lock-resources-using-the-web-service-api}

Bloccare le risorse utilizzando l’API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il Repository WSDL utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specifica l’URI della risorsa da bloccare

   Specifica una stringa contenente l’URI della risorsa da bloccare. In questo caso, perché la risorsa denominata `testResource` si trova nella cartella `testFolder`, il suo URI è `"/testFolder/testResource"`. Quando si utilizza un linguaggio conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Bloccare la risorsa

   Richiama il `RepositoryServiceService` dell’oggetto `lockResource` e trasmettere i seguenti parametri:

   * URI della risorsa.
   * L&#39;ambito di blocco. In questo esempio, poiché la risorsa verrà bloccata per uso esclusivo, l’ambito del blocco viene specificato come `11`.
   * La profondità di blocco. In questo esempio, poiché il blocco viene applicato solo alla risorsa specifica e nessuno dei relativi membri o elementi secondari, la profondità di blocco viene specificata come `2`.
   * Un `int` valore che indica il numero di secondi fino alla scadenza del blocco. In questo esempio, il valore di `1000` viene utilizzato.
   * Pass `null` per l’ultimo parametro.

1. Recupera i blocchi per la risorsa

   Richiama il `RepositoryServiceService` dell’oggetto `getLocks` e passa l’URI della risorsa come primo parametro e `null` per il secondo parametro. Il metodo restituisce un `object` matrice contenente `Lock` oggetti attraverso i quali è possibile eseguire iterazioni. In questo esempio, il proprietario del blocco, la profondità e l&#39;ambito vengono stampati per ogni oggetto accedendo a ogni `Lock` dell’oggetto `ownerUserId`, `depth`e `type` rispettivamente.

1. Sblocca la risorsa

   Richiama il `RepositoryServiceService` dell’oggetto `unlockResource` e passa l’URI della risorsa come primo parametro e `null` per il secondo parametro.

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Eliminazione delle risorse {#deleting-resources}

Puoi eliminare programmaticamente le risorse da una determinata posizione nell’archivio utilizzando l’API Java (SOAP) del servizio Repository.

Quando elimini una risorsa, l’eliminazione è normalmente permanente, anche se in alcuni casi gli archivi ECM possono memorizzare le versioni della risorsa in base ai loro meccanismi della cronologia. Pertanto, quando elimini una risorsa, è importante essere sicuri che non sarà più necessaria. I motivi comuni per eliminare una risorsa includono la necessità di aumentare lo spazio disponibile nel database. Puoi eliminare una versione di una risorsa, ma in tal caso devi specificare l’identificatore della risorsa e non il relativo identificatore logico (LID) o il relativo percorso. Se elimini una cartella, tutto ciò che si trova in tale cartella, incluse le sottocartelle e le risorse, verrà eliminato automaticamente.

Le risorse correlate non vengono eliminate. Ad esempio, se si dispone di un modulo che utilizza il file logo.gif ed elimini logo.gif, nella tabella delle relazioni in sospeso verrà memorizzata una relazione. In alternativa, in caso di versione obsoleta, imposta lo stato dell’oggetto dell’ultima versione su obsoleto.

Un&#39;operazione di eliminazione non è sicura per le transazioni nei sistemi ECM. Ad esempio, se tenti di eliminare 100 risorse e l’operazione non riesce sulla 50° risorsa, le prime 49 istanze verranno eliminate ma il resto no. In caso contrario, il comportamento predefinito è il rollback (non impegno).

>[!NOTE]
>
>Quando utilizzi `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` metodo con l&#39;archivio ECM (EMC Documentum Content Server e IBM FileNet P8 Content Manager), la transazione non verrà ripristinata se l&#39;eliminazione non riesce per una delle risorse specificate, il che significa che i file che sono stati eliminati non possono essere eliminati.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per eliminare una risorsa, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client del servizio Repository.
1. Specifica l’URI della risorsa da eliminare.
1. Elimina la risorsa.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare il client di servizio**

Prima di poter leggere una risorsa in modo programmatico, è necessario stabilire una connessione e fornire le credenziali. Questa operazione viene eseguita creando un client di servizio.

**Specifica l’URI della risorsa da eliminare**

Crea una stringa contenente l’URI della risorsa da eliminare. La sintassi include le barre, come in questo esempio: &quot;/*path*/*risorsa*&quot;. Se la risorsa da eliminare è una cartella, l’eliminazione sarà ricorsiva.

**Elimina la risorsa**

Richiama il metodo del servizio Repository per eliminare la risorsa, specificando l&#39;URI.

**Consulta anche**

[Eliminare le risorse utilizzando l’API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Eliminare le risorse tramite l’API del servizio Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio archivio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Eliminare le risorse utilizzando l’API Java (SOAP) {#delete-resources-using-the-java-api-soap}

Eliminare una risorsa utilizzando l’API Repository (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare il client di servizio

   Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica l’URI della risorsa da eliminare

   Specifica l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata testResourceToBeDeleted si trova nella cartella denominata testFolder, il relativo URI è `/testFolder/testResourceToBeDeleted`. L’URI viene memorizzato come `java.lang.String` oggetto. In questo esempio, la risorsa viene scritta per la prima volta nella directory archivio e viene recuperato il relativo URI. Per ulteriori informazioni sulla scrittura di una risorsa, consulta [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Elimina la risorsa

   Richiama il `ResourceRepositoryClient` dell’oggetto `deleteResource` e passa l’URI della risorsa come parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Avvio rapido (modalità SOAP): Ricerca di risorse tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminare le risorse tramite l’API del servizio Web {#delete-resources-using-the-web-service-api}

Eliminare una risorsa utilizzando l’API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il Repository WSDL utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client di servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` richiamando il relativo costruttore predefinito. Imposta `Credentials` proprietà che utilizza `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specifica l’URI della risorsa da eliminare

   Specifica l’URI della risorsa da recuperare. In questo caso, perché la risorsa denominata `testResourceToBeDeleted` si trova nella cartella denominata `testFolder`, il suo URI è `"/testFolder/testResourceToBeDeleted"`. In questo esempio, la risorsa viene scritta per la prima volta nella directory archivio e viene recuperato il relativo URI. Per ulteriori informazioni sulla scrittura di una risorsa, consulta [Scrittura delle risorse](aem-forms-repository.md#writing-resources).

1. Elimina la risorsa

   Richiama il `RepositoryServiceService` dell’oggetto `deleteResources` e passare un `System.String` array contenente l’URI della risorsa come primo parametro. Pass `null` per il secondo parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
