---
title: Utilizzo dell'archivio moduli AEM
seo-title: Utilizzo dell'archivio moduli AEM
description: 'null'
seo-description: 'null'
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Working with AEM Forms Repository {#working-with-aem-forms-repository}

**Informazioni su Repository Service**

Il servizio Repository fornisce servizi di archiviazione e gestione delle risorse ad AEM Forms. Quando gli sviluppatori creano un&#39;applicazione *AEM Forms* , possono distribuire le risorse nell&#39;archivio invece che nel file system. Le risorse possono includere qualsiasi tipo di materiale collaterale, inclusi moduli XML, moduli PDF (inclusi moduli Acrobat), frammenti di modulo, immagini, profili, criteri, file SWF, file DDX, schemi XML, file WSDL e dati di prova.

Ad esempio, consultare la seguente applicazione Forms denominata *Applications/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Tenere presente che nella cartella FormsFolder è presente un file denominato Loan.xdp. Per accedere a questa struttura del modulo, specificare il percorso completo (inclusa la versione): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms utilizzando Workbench, vedere la Guida [di](https://www.adobe.com/go/learn_aemforms_workbench_63)Workbench.

Il percorso di una risorsa situata nell&#39;archivio di AEM Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>È possibile esplorare l&#39;archivio moduli AEM utilizzando un browser Web. Per esplorare la directory archivio, immettete il seguente URL in un browser Web https://[server name]:[server port]/repository. È possibile verificare i risultati di avvio rapido associati alla sezione Utilizzo di AEM Forms Repository utilizzando un browser Web. Ad esempio, se aggiungete contenuto all&#39;archivio moduli di AEM, potete visualizzarne il contenuto in un browser Web. (Vedere Avvio [rapido (modalità SOAP): Scrivere una risorsa utilizzando l&#39;API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)Java.

L&#39;API del repository fornisce una serie di operazioni che è possibile utilizzare per memorizzare e recuperare informazioni dal repository. Ad esempio, è possibile ottenere un elenco di risorse o recuperare risorse specifiche memorizzate nella directory archivio quando una risorsa è necessaria durante l&#39;elaborazione di un&#39;applicazione.

>[!NOTE]
>
>L&#39;API dell&#39;archivio non può essere utilizzata per interagire con Content Services (obsoleto). Per interagire con Content Services (obsoleto), utilizzate Document Management API.

Utilizzando l&#39;API del servizio Repository, potete eseguire le seguenti operazioni:

* Creare cartelle. Consultate [Creazione di cartelle](aem-forms-repository.md#creating-folders).
* Scrivere risorse e relative proprietà. Consulta [Creazione di risorse](aem-forms-repository.md#writing-resources).
* Elenca le risorse in una raccolta specifica o correlate ad altre risorse. Consulta [Elenco delle risorse](aem-forms-repository.md#listing-resources).
* Leggere le risorse e le relative proprietà. Vedere Risorse [di](aem-forms-repository.md#reading-resources)lettura.
* Aggiornare le risorse e le relative proprietà. Consulta [Aggiornamento delle risorse](aem-forms-repository.md#updating-resources).
* Cercare risorse, inclusa la cronologia, le risorse correlate e le proprietà. Consultate [Ricerca di risorse](aem-forms-repository.md#searching-for-resources).
* Specificare le relazioni tra le risorse. Vedere [Creazione di relazioni](aem-forms-repository.md#creating-resource-relationships)con le risorse.
* Gestire il controllo dell&#39;accesso alle risorse, incluso il blocco e lo sblocco delle risorse, nonché la lettura e la scrittura degli elenchi di controllo dell&#39;accesso (ACL). Consultate [Blocco delle risorse](aem-forms-repository.md#locking-resources).
* Eliminare le risorse e le relative proprietà. Vedere [Eliminazione delle risorse](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Utilizzando l&#39;API del repository non è possibile gestire il controllo dell&#39;accesso alle risorse, cercare risorse o specificare relazioni tra risorse utilizzando un repository ECM.

>[!NOTE]
>
>Quando un PDF crittografato viene scritto nell&#39;archivio, non è possibile utilizzare la funzione di estrazione relazione automatica. In caso contrario, un PDF crittografato può essere memorizzato nella directory archivio e successivamente recuperato. Il recuperatore può scegliere di decrittografare il PDF dopo averlo recuperato dalla directory archivio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di cartelle {#creating-folders}

Le cartelle (raccolte di risorse) vengono utilizzate per memorizzare oggetti (file o risorse) in raggruppamenti organizzati. Le cartelle possono contenere risorse e altre cartelle, dette anche sottocartelle. Le risorse possono essere memorizzate in una sola cartella alla volta.

I file ereditano gli elenchi di controllo di accesso (ACL, Access Control List) dalle cartelle e le sottocartelle ereditano gli ACL dalle relative cartelle principali. Pertanto, le cartelle principali devono esistere prima di poter creare cartelle figlie. L’IDE consente di interagire solo a livello di cartella per cartella, non a livello di singolo file. Non è possibile eseguire la versione delle cartelle e non è necessario farlo; una cartella non contiene i dati stessi. ma solo un contenitore per le risorse che contengono dati. L&#39;ACL predefinito è un&#39;autorizzazione a livello di sistema, il che significa che gli utenti devono disporre di autorizzazioni a livello di sistema (lettura, scrittura, lettura, gestione ACL) fino a quando qualcuno non conceda loro le autorizzazioni per una determinata cartella. Gli ACL funzionano solo nell&#39;IDE.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare una cartella, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Create il client del servizio.
1. Create la cartella.
1. Scrivere la cartella nella directory archivio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter creare una raccolta di risorse a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Creare la cartella**

Richiamare il metodo del servizio Repository per creare la raccolta di risorse e compilare la raccolta di risorse con informazioni di identificazione, incluso il relativo UUID, il nome della cartella e la descrizione.

**Scrivere la cartella nella directory archivio**

Richiamare il metodo del servizio Repository per scrivere la raccolta di risorse, specificando l&#39;URI della cartella di destinazione.

**Consulta anche**

[Creare cartelle utilizzando l&#39;API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Creazione di cartelle tramite l&#39;API del servizio Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creare cartelle utilizzando l&#39;API Java {#create-folders-using-the-java-api}

Create una cartella utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file di progetto nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Creare la cartella

   Per creare una raccolta di risorse, è innanzitutto necessario creare un `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` oggetto.

   Richiamare il metodo dell’ `repositoryInfomodelFactoryBean` oggetto `newResourceCollection` e trasmettere i seguenti parametri:

   * Identificatore `com.adobe.repository.infomodel.Id` UUID da assegnare alla risorsa.
   * Identificatore `com.adobe.repository.infomodel.Lid` UUID da assegnare alla risorsa.
   * Un `java.lang.String` contenente il nome della raccolta di risorse. Esempio, `FormsFolder`.
   Il metodo restituisce un `com.adobe.repository.infomodel.bean.ResourceCollection` oggetto che rappresenta la nuova cartella.

   Impostate la descrizione della cartella utilizzando il `setDescription` metodo e passate il seguente parametro:

   * Un oggetto `String` che descrive la raccolta di risorse. In questo esempio `"test Folder"` viene utilizzato `.`


1. Scrivere la cartella nella directory archivio

   Richiamate il metodo dell’ `ResourceRepositoryClient` oggetto `writeResource` e passate l’URI della cartella e dell’ `ResourceCollection` oggetto. Ad esempio, l’URI della cartella può essere il valore seguente `/Applications/FormsApplication/1.0/`.

   Il metodo restituisce un&#39;istanza dell&#39;oggetto appena creato `com.adobe.repository.infomodel.bean.Resource` . È possibile, ad esempio, recuperare il valore identificatore della nuova risorsa richiamando il `com.adobe.repository.infomodel.bean.Resource` metodo dell&#39; `getId` oggetto.

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Avvio rapido (modalità SOAP): Creazione di una cartella mediante l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di cartelle tramite l&#39;API del servizio Web {#create-folders-using-the-web-service-api}

Create una cartella utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto che contiene il nome utente e la password.

1. Creare la cartella

   Create la cartella utilizzando il costruttore predefinito per la `ResourceCollection` classe e trasmettete i seguenti parametri:

   * Un `Id` oggetto, creato richiamando il costruttore predefinito per la `Id` classe e assegnato al campo dell&#39; `Resource` oggetto `id` .
   * Un `Lid` oggetto, creato richiamando il costruttore predefinito per la `Lid` classe e assegnato al campo dell&#39; `Resource` oggetto `lid` .
   * Una stringa contenente il nome della raccolta di risorse, assegnata al campo dell&#39; `Resource` oggetto `name` . Il nome utilizzato in questo esempio è `"testfolder"`.
   * Una stringa contenente la descrizione della raccolta di risorse, assegnata al campo dell&#39; `Resource` oggetto `description` . La descrizione utilizzata in questo esempio è `"test folder"`.

1. Scrivere la cartella nella directory archivio

   Richiama il metodo dell’ `RepositoryServiceService` oggetto `writeResource` e passa i seguenti parametri:

   * Percorso in cui creare la cartella.
   * L&#39; `ResourceCollection` oggetto che rappresenta la cartella.
   * Passa `null` per gli altri due parametri.

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Scrittura delle risorse {#writing-resources}

Potete creare risorse in una determinata posizione nella directory archivio. La dimensione del file naturale è soggetta alle limitazioni del database e al timeout della sessione. Per la configurazione predefinita, i file sono limitati a 25 MB. Per aumentare o ridurre la dimensione massima del file, è necessario modificare la configurazione del database.

La scrittura di risorse equivale alla memorizzazione dei dati nell&#39;archivio. Dopo aver scritto una risorsa nella directory archivio, questa diventa accessibile a tutti i client dell’ecosistema della directory archivio. Quando si scrivono risorse, come schemi XML, file XDP e file XSD, nell&#39;archivio, i contenuti vengono analizzati in base al tipo MIME. Se il tipo MIME è supportato, il parser determina se esiste una relazione implicita con altro contenuto. Ad esempio, se un foglio di stile CSS ha un URL relativo che fa riferimento a un CSS comune, è previsto che invierete anche il CSS comune nell&#39;archivio. La relazione tra le due risorse viene memorizzata come relazione in sospeso per un periodo non regolabile di 30 giorni. Quando inviate il CSS comune alla directory archivio entro 30 giorni, la relazione viene formata.

Quando create una risorsa, l&#39;elenco di controllo di accesso (ACL, Access Control List) viene ereditato dalla cartella principale. La cartella principale dispone di autorizzazioni a livello di sistema fino alla creazione di una risorsa o di una cartella iniziale, al punto in cui alla risorsa o alla cartella vengono assegnate autorizzazioni ACL predefinite.

Potete scrivere le risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per scrivere una risorsa, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificare l&#39;URI della risorsa da leggere.
1. Leggete la risorsa.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare l&#39;URI della cartella di destinazione per la risorsa**

Create una stringa contenente l’URI della risorsa da leggere. La sintassi include le barre, come in questo esempio: &quot;/*path*/*folder*&quot;.

**Creare la risorsa**

Richiama il metodo del servizio Repository per creare la risorsa e compila la risorsa con informazioni identificative, incluso il suo UUID, il nome della risorsa e la descrizione.

**Specificare il contenuto della risorsa**

Richiamare il metodo del servizio Repository per creare il contenuto delle risorse e archiviarlo nella risorsa.

**Scrivere la risorsa nella cartella di destinazione**

Richiamate il metodo del servizio Repository per scrivere la risorsa, specificando l’URI della cartella di destinazione.

**Consulta anche**

[Scrivere risorse tramite l&#39;API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Creazione di risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Scrivere risorse tramite l&#39;API Java {#write-resources-using-the-java-api}

Scrivere una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificare l&#39;URI della cartella di destinazione per la risorsa

   Specificate l’URI della cartella di destinazione per la risorsa. In questo caso, poiché la risorsa denominata `testResource` sarà memorizzata nella cartella denominata `testFolder`, l’URI della cartella è `"/testFolder"`. L&#39;URI è memorizzato come `java.lang.String` oggetto.

1. Creare la risorsa

   Per creare una risorsa, è innanzitutto necessario creare un `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` oggetto.

   Richiama il metodo dell&#39; `RepositoryInfomodelFactoryBean` oggetto `newResource` , che crea un `com.adobe.repository.infomodel.bean.Resource` oggetto. In questo esempio, vengono forniti i seguenti parametri:

   * Un `com.adobe.repository.infomodel.Id` oggetto, creato richiamando il costruttore predefinito per la `Id` classe.
   * Un `com.adobe.repository.infomodel.Lid` oggetto, creato richiamando il costruttore predefinito per la `Lid` classe.
   * Un file `java.lang.String` contenente il nome file della risorsa.
   Per specificare la descrizione della risorsa, richiamare il metodo dell&#39; `Resource` oggetto `setDescription` e passare una stringa contenente la descrizione. In questo esempio, la descrizione è `"test resource"`.

1. Specificare il contenuto della risorsa

   Per creare contenuto per la risorsa, richiamare il metodo dell&#39; `RepositoryInfomodelFactoryBean` oggetto `newResourceContent` , che restituisce un `com.adobe.repository.infomodel.bean.ResourceContent` oggetto. Add content to the `ResourceContent` object. In questo esempio, questo si ottiene eseguendo le seguenti operazioni:

   * Richiamo del metodo dell&#39; `ResourceContent` oggetto `setDataDocument` e passaggio di un `com.adobe.idp.Document` oggetto
   * Richiamo del metodo dell&#39; `ResourceContent` oggetto `setSize` e trasmissione delle dimensioni in byte dell&#39; `Document` oggetto
   Aggiungete il contenuto alla risorsa richiamando il metodo dell&#39; `Resource` oggetto `setContent` e passando l&#39; `ResourceContent` oggetto. Per ulteriori informazioni, consulta [Riferimento](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)API per AEM Forms.

1. Scrivere la risorsa nella cartella di destinazione

   Richiamate il metodo dell’ `ResourceRepositoryClient` oggetto `writeResource` e passate l’URI della cartella, nonché l’ `Resource` oggetto.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Avvio rapido (modalità SOAP): Creazione di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di risorse tramite l&#39;API del servizio Web {#write-resources-using-the-web-service-api}

Scrivere una risorsa utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specificare l&#39;URI della cartella di destinazione per la risorsa

   Specificate l’URI della cartella di destinazione per la risorsa. In questo caso, poiché la risorsa denominata `testResource` sarà memorizzata nella cartella denominata `testFolder`, l’URI della cartella è `"/testFolder"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Creare la risorsa

   Per creare una risorsa, richiamare il costruttore predefinito per la `Resource` classe. In questo esempio, nell&#39; `Resource` oggetto sono memorizzate le informazioni seguenti:

   * Un `com.adobe.repository.infomodel.Id` oggetto, creato richiamando il costruttore predefinito per la `Id` classe e assegnato al campo dell&#39; `Resource` oggetto `id` .
   * Un `com.adobe.repository.infomodel.Lid` oggetto, creato richiamando il costruttore predefinito per la `Lid` classe e assegnato al campo dell&#39; `Resource` oggetto `lid` .
   * Una stringa contenente il nome file della risorsa, assegnato al campo dell&#39; `Resource` oggetto `name` . Il nome utilizzato in questo esempio è `"testResource"`.
   * Una stringa contenente la descrizione della risorsa, assegnata al campo dell&#39; `Resource` oggetto `description` . La descrizione utilizzata in questo esempio è `"test resource"`.

1. Specificare il contenuto della risorsa

   Per creare contenuto per la risorsa, richiamare il costruttore predefinito per la `ResourceContent` classe. Quindi aggiungere il contenuto all&#39; `ResourceContent` oggetto. In questo esempio, questo si ottiene eseguendo le seguenti operazioni:

   * Assegnazione di un `BLOB` oggetto contenente un documento al `ResourceContent` campo dell&#39; `dataDocument` oggetto.
   * Assegnazione delle dimensioni in byte dell&#39; `BLOB` oggetto al campo dell&#39; `ResourceContent` oggetto `size` .
   Aggiungete il contenuto alla risorsa assegnando l&#39; `ResourceContent` oggetto al campo dell&#39; `Resource` oggetto `content` .

1. Scrivere la risorsa nella cartella di destinazione

   Richiamate il metodo dell’ `RepositoryServiceService` oggetto `writeResource` e passate l’URI della cartella, nonché l’ `Resource` oggetto. Passa `null` per gli altri due parametri.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Risorse elenco {#listing-resources}

Potete scoprire le risorse elencando le risorse. Nell&#39;archivio viene eseguita una query per individuare tutte le risorse correlate a una determinata raccolta di risorse.

Una volta organizzate le risorse, potete ispezionare la struttura creata visualizzando un particolare ramo della struttura, come si fa in un sistema operativo.

Le risorse di elenco operano per relazione: le risorse sono membri di cartelle. L&#39;appartenenza è rappresentata da una relazione di tipo &quot;membro di&quot;. Quando si elencano le risorse in una determinata cartella, si esegue una query per individuare le risorse correlate a una determinata cartella dalla relazione &quot;membro di&quot;. Le relazioni sono direzionali: un membro di una relazione ha un&#39;origine che è membro dell&#39;oggetto. L&#39;origine è la risorsa; la destinazione è la cartella principale.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per elencare le risorse, procedere come segue:

1. Includere i file di progetto.
1. Create il client del servizio.
1. Specificate il percorso della cartella.
1. Recuperate l’elenco delle risorse.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter creare una raccolta di risorse a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare il percorso della cartella**

Create una stringa contenente il percorso della cartella contenente le risorse. La sintassi include le barre, come in questo esempio: &quot;/*path*/*folder*&quot;.

**Recuperare l’elenco delle risorse**

Richiamare il metodo del servizio Repository per recuperare l’elenco delle risorse, specificando il percorso della cartella di destinazione.

**Consulta anche**

[Elenca le risorse tramite l&#39;API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Elenca le risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Elenca le risorse tramite l&#39;API Java {#list-resources-using-the-java-api}

Elenca le risorse utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificare il percorso della cartella

   Specificate l&#39;URI della raccolta di risorse da interrogare. In questo caso, l’URI è `"/testFolder"`. L&#39;URI è memorizzato come `java.lang.String` oggetto.

1. Recuperare l’elenco delle risorse

   Richiamate il metodo dell’ `ResourceRepositoryClient` oggetto `listMembers` e passate l’URI della cartella.

   Il metodo restituisce un insieme `java.util.List` di `com.adobe.repository.infomodel.bean.Resource` oggetti che sono l&#39;origine di un `com.adobe.repository.infomodel.bean.Relation` tipo `Relation.TYPE_MEMBER_OF` e che hanno come destinazione l&#39;URI della raccolta di risorse. Potete eseguire un’iterazione `List` per recuperare ciascuna risorsa. In questo esempio vengono visualizzati il nome e la descrizione di ogni risorsa.

**Consulta anche**

[Risorse](aem-forms-repository.md#listing-resources)di elenco.

[Avvio rapido (modalità SOAP): Elencare le risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Elenca le risorse tramite l&#39;API del servizio Web {#list-resources-using-the-web-service-api}

Elenca le risorse utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specificare il percorso della cartella

   Specificate una stringa contenente l’URI della cartella alla quale verrà chiesto di eseguire la query. In questo caso, l’URI è `"/testFolder"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Recuperare l’elenco delle risorse

   Richiamate il metodo dell’ `RepositoryServiceService` oggetto `listMembers` e passate l’URI della cartella come primo parametro. Passa `null` per gli altri due parametri.

   Il metodo restituisce un array di oggetti che è possibile trasmettere agli `Resource` oggetti. È possibile iterare l&#39;array di oggetti per recuperare ciascuna delle risorse correlate. In questo esempio vengono visualizzati il nome e la descrizione di ogni risorsa.

**Consulta anche**

[Risorse](aem-forms-repository.md#listing-resources)di elenco.

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Lettura delle risorse {#reading-resources}

È possibile recuperare risorse da una determinata posizione nella directory archivio per leggerne il contenuto e i metadati. Il flusso di lavoro è preceduto da un modulo di inizializzazione. Il processo dispone di tutte le autorizzazioni necessarie per leggere il modulo. Il sistema recupera il modulo dati e legge il contenuto dalla directory archivio. L’archivio consente l’accesso al contenuto e ai metadati (la possibilità di conoscere l’esistenza della risorsa).

La directory archivio presenta quattro tipi di autorizzazioni:

* **traverse**: consente di elencare le risorse; ovvero per leggere i metadati delle risorse, ma non il contenuto delle risorse
* **read**: consente di leggere il contenuto delle risorse
* **scrivere**: consente di scrivere il contenuto delle risorse
* **gestione degli elenchi di controllo di accesso (ACL)**: consente di manipolare gli ACL sulle risorse

Gli utenti possono eseguire i processi solo quando dispongono dell&#39;autorizzazione per eseguire il processo. Gli utenti IDE devono disporre di autorizzazioni di lettura e lettura da sincronizzare con il repository. Gli ACL si applicano solo in fase di progettazione, perché il runtime si verifica all&#39;interno del contesto del sistema.

Potete leggere le risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per leggere una risorsa, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificare l&#39;URI della risorsa da leggere.
1. Leggete la risorsa.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare l&#39;URI della risorsa da leggere**

Create una stringa contenente l’URI della risorsa da leggere. La sintassi include le barre, come in questo esempio: &quot;/*path*/*resource*&quot;.

**Leggere la risorsa**

Richiamare il metodo del servizio Repository per leggere la risorsa, specificando l&#39;URI.

**Consulta anche**

[Leggere le risorse tramite l&#39;API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lettura delle risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Leggere le risorse tramite l&#39;API Java {#read-resources-using-the-java-api}

Leggere una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificare l&#39;URI della risorsa da leggere

   Specificate un valore di stringa che rappresenta l’URI della risorsa da recuperare. Ad esempio, se la risorsa è denominata *testResource* che si trova in una cartella denominata *testFolder*, specificare `/testFolder/testResource`.

1. Leggere la risorsa

   Richiamate il metodo dell’ `ResourceRepositoryClient` oggetto `readResource` e passate l’URI della risorsa come parametro. Questo metodo restituisce un’ `Resource` istanza che rappresenta la risorsa.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Avvio rapido (modalità SOAP): Lettura di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lettura delle risorse tramite l&#39;API del servizio Web {#reading-resources-using-the-web-service-api}

Leggere una risorsa utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository. (Vedere [Creazione di un assembly client .NET che utilizza la codifica](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)Base64.)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere [Creazione di un assembly client .NET che utilizza la codifica](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)Base64.)

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da leggere

   Specificate una stringa contenente l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResource"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Leggere la risorsa

   Richiamate il metodo dell’ `RepositoryServiceService` oggetto `readResource` e passate l’URI della risorsa come primo parametro. Passa `null` per gli altri due parametri.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Aggiornamento delle risorse {#updating-resources}

È possibile recuperare e aggiornare il contenuto delle risorse nella directory archivio. Quando aggiornate le risorse, il controllo di accesso a tali risorse rimane invariato tra le diverse versioni. Durante l&#39;esecuzione di un aggiornamento, potete scegliere di incrementare la versione principale. Se non si sceglie di incrementare la versione principale, la versione secondaria viene aggiornata automaticamente.

Quando aggiornate una risorsa, la nuova versione viene creata in base agli attributi della risorsa specificati. Quando aggiornate una risorsa, specificate due parametri importanti: l’URI di destinazione e un’istanza di risorsa contenente tutti i metadati aggiornati. È importante notare che se non modificate un dato attributo (ad esempio, il nome), l’attributo è comunque obbligatorio nell’istanza passata. Le relazioni create durante l&#39;analisi del contenuto vengono aggiunte alla versione specifica e non vengono portate avanti a meno che non sia specificato.

Ad esempio, se aggiornate un file XDP che contiene riferimenti ad altre risorse, anche tali riferimenti aggiuntivi verranno registrati. Supponiamo che form.xdp versione 1.0 abbia due riferimenti esterni: un logo e un foglio di stile, quindi si aggiorna form.xdp in modo che ora contenga tre riferimenti: un logo, un foglio di stile e un file di schema. Durante l&#39;aggiornamento, il repository aggiungerà la terza relazione (al file dello schema) alla tabella di relazione in sospeso. Una volta che il file dello schema è presente nella directory archivio, la relazione viene automaticamente formata. Tuttavia, se form.xdp versione 2.0 non utilizza più il logo, form.xdp versione 2.0 non avrà alcuna relazione con il logo.

Tutte le operazioni di aggiornamento sono atomiche e transazionali. Ad esempio, se due utenti leggono la stessa risorsa ed entrambi decidono di aggiornare la versione 1.0 alla versione 2.0, uno di questi avrà successo e uno di loro avrà esito negativo, l&#39;integrità del repository verrà mantenuta e a entrambi verrà visualizzato un messaggio di conferma del successo o dell&#39;errore. Se la transazione non viene confermata, verrà ripristinata in caso di errore del database e si verificherà il timeout o il rollback a seconda del server dell&#39;applicazione.

Potete aggiornare le risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per aggiornare una risorsa, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Recuperate la risorsa da aggiornare.
1. Aggiorna la risorsa.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Recuperare la risorsa da aggiornare**

Leggete la risorsa. Per ulteriori informazioni, vedere [Risorse](aem-forms-repository.md#reading-resources)di lettura.

**Aggiornare la risorsa**

Impostate le nuove informazioni nella risorsa e richiamate il metodo del servizio Repository per aggiornare la risorsa, specificando l’URI, la risorsa aggiornata e la modalità di aggiornamento delle informazioni sulla versione.

**Consulta anche**

[Aggiornare le risorse tramite l&#39;API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Aggiornare le risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Aggiornare le risorse tramite l&#39;API Java {#update-resources-using-the-java-api}

Aggiornare una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Recuperare la risorsa da aggiornare

   Specificate l’URI della risorsa da recuperare e leggere. In questo esempio, l’URI della risorsa è `"/testFolder/testResource"`.

1. Aggiornare la risorsa

   Aggiornare le informazioni dell&#39; `Resource` oggetto. In questo esempio, per aggiornare la descrizione, richiamare il metodo dell&#39; `Resource` oggetto `setDescription` e passare la nuova stringa di descrizione come parametro.

   Quindi richiamate il metodo dell’ `ServiceClientFactory` oggetto `updateResource` e passate i seguenti parametri:

   * Un `java.lang.String` oggetto contenente l&#39;URI della risorsa.
   * L&#39; `Resource` oggetto contenente le informazioni aggiornate sulla risorsa.
   * Un `boolean` valore che indica se aggiornare la versione principale o secondaria. In questo esempio, `true` viene passato un valore di per indicare che la versione principale deve essere incrementata.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Avvio rapido (modalità SOAP): Aggiornamento di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiornare le risorse tramite l&#39;API del servizio Web {#update-resources-using-the-web-service-api}

Aggiornare una risorsa utilizzando l&#39;API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Recuperare la risorsa da aggiornare

   Specificate l’URI della risorsa da recuperare e leggete la risorsa. In questo esempio, l’URI della risorsa è `"/testFolder/testResource"`. Per ulteriori informazioni, vedere [Risorse](aem-forms-repository.md#reading-resources)di lettura.

1. Aggiornare la risorsa

   Aggiornare le informazioni dell&#39; `Resource` oggetto. In questo esempio, per aggiornare la descrizione, assegnare un nuovo valore al campo dell&#39; `Resource` oggetto `description` .

1. Richiamare il metodo dell’ `RepositoryServiceService` oggetto `updateResource` e trasmettere i seguenti parametri:

   * Un `System.String` oggetto contenente l&#39;URI della risorsa.
   * L&#39; `Resource` oggetto contenente le informazioni aggiornate sulla risorsa.
   * Un `boolean` valore che indica se aggiornare la versione principale o secondaria. In questo esempio, `true` viene passato un valore di per indicare che la versione principale deve essere incrementata.
   * Passa `null` per i due parametri rimanenti.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ricerca di risorse {#searching-for-resources}

È possibile creare query utilizzate per cercare risorse nella directory archivio, inclusi cronologia, risorse correlate e proprietà.

È possibile recuperare risorse correlate per determinare le dipendenze tra un modulo e i relativi frammenti. Ad esempio, se si dispone di un modulo è possibile determinare i frammenti o le risorse esterne che utilizza. Se disponete di un’immagine, potete anche scoprire quali moduli utilizzano l’immagine. Potete anche cercare risorse correlate utilizzando il filtro in base alle proprietà. Ad esempio, è possibile cercare tutti i moduli che utilizzano un&#39;immagine con un nome specificato, oppure trovare le immagini utilizzate da un modulo con un nome specificato. È inoltre possibile eseguire ricerche utilizzando le proprietà delle risorse. Ad esempio, è possibile eseguire una query per individuare tutti i moduli o le risorse il cui nome inizia con una stringa specifica che può includere caratteri jolly &quot;%&quot; e &quot;_&quot;. Ricorda che le ricerche basate sulle proprietà non sono basate sulle relazioni; tali ricerche si basano sul presupposto che si disponga di conoscenze specifiche su una determinata risorsa.

**Istruzioni query**

Una *query* contiene una o più istruzioni collegate logicamente con le condizioni. Un&#39; *istruzione* è costituita da un operando sinistro, un operatore e un operando destro. Inoltre, potete specificare l&#39;ordinamento da utilizzare per i risultati della ricerca. L&#39; *ordinamento* contiene informazioni equivalenti a una `ORDER BY` clausola SQL ed è composto da elementi che contengono gli attributi su cui è stata basata la ricerca, nonché un valore che indica se utilizzare l&#39;ordine crescente o decrescente.

È possibile cercare le risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository. Al momento, non è possibile utilizzare l&#39;API del servizio Web per cercare le risorse.

**Comportamento dell&#39;ordinamento**

L&#39;ordinamento non viene rispettato quando si richiama il metodo dell&#39; `ResourceRepositoryClient` oggetto `searchProperties` e si specifica un ordinamento. Ad esempio, si supponga di creare una risorsa con tre proprietà personalizzate, in cui i nomi degli attributi sono `name`, `secondName`e `asecondName`. Quindi create un elemento di ordinamento sul nome dell&#39;attributo e impostate il `ascending` valore su `true`.

Quindi, richiamare il metodo dell’ `ResourceRepositoryClient` oggetto `searchProperties` e trasmettere l’ordine. La ricerca restituisce la risorsa giusta, con le tre proprietà. Tuttavia, le proprietà non sono ordinate per nome di attributo. Vengono restituiti nell&#39;ordine in cui sono stati aggiunti: `name`, `secondName`, e `asecondName`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per cercare risorse, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificate la cartella di destinazione per la ricerca.
1. Specificate gli attributi utilizzati nella ricerca.
1. Create la query utilizzata nella ricerca.
1. Create l’ordinamento per i risultati della ricerca.
1. Cercare le risorse.
1. Recuperate le risorse dal risultato della ricerca.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificate la cartella di destinazione per la ricerca**

Create una stringa contenente il percorso di base da cui eseguire la ricerca. La sintassi include le barre, come in questo esempio: &quot;/*path*/*folder*&quot;.

**Specificare gli attributi utilizzati nella ricerca**

Potete basare la ricerca sugli attributi contenuti nelle risorse. Specificate i valori degli attributi su cui eseguire la ricerca.

**Creare la query utilizzata nella ricerca**

Creare una query utilizzando istruzioni e condizioni. Ogni istruzione specifica l&#39;attributo su cui basare la ricerca, la condizione da utilizzare e il valore dell&#39;attributo da utilizzare nella ricerca.

**Creare l’ordinamento per i risultati della ricerca**

L&#39;ordinamento è composto da elementi, ciascuno dei quali contiene uno degli attributi utilizzati nella ricerca e un valore che indica se deve essere utilizzato l&#39;ordine crescente o decrescente.

**Ricerca delle risorse**

Cercate le risorse utilizzando la cartella, la query e l’ordine. Inoltre, indicare la profondità della ricerca e un limite superiore per il numero di risultati da restituire.

**Recuperare le risorse dal risultato della ricerca**

Scorrete l&#39;elenco di risorse restituito ed estraete le informazioni per un&#39;ulteriore elaborazione.

**Consulta anche**

[Cercare risorse tramite l&#39;API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Cercare risorse tramite l&#39;API Java {#search-for-resources-using-the-java-api}

Cercare una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificate la cartella di destinazione per la ricerca

   Specificare l&#39;URI del percorso di base da cui eseguire la ricerca. In questo esempio, l’URI della risorsa è `/testFolder`.

1. Specificare gli attributi utilizzati nella ricerca

   Specificate i valori per gli attributi su cui eseguire la ricerca. Gli attributi esistono all&#39;interno di un `com.adobe.repository.infomodel.bean.Resource` oggetto. In questo esempio, la ricerca verrà eseguita sull&#39;attributo name; pertanto, viene utilizzato un `java.lang.String` contenitore del nome dell&#39; `Resource` oggetto, in questo `testResource` caso.

1. Creare la query utilizzata nella ricerca

   Per creare una query, creare un `com.adobe.repository.query.Query` oggetto richiamando il costruttore predefinito per la `Query` classe e aggiungendo istruzioni alla query.

   Per creare un&#39;istruzione, richiamare il costruttore per la `com.adobe.repository.query.Query.Statement` classe e trasmettere i seguenti parametri:

   * Un operando a sinistra contenente la costante attributo risorsa. In questo esempio, poiché il nome della risorsa è utilizzato come base per la ricerca, `Resource.ATTRIBUTE_NAME` viene utilizzato il valore statico.
   * Operatore che contiene la condizione utilizzata nella ricerca dell&#39;attributo. L&#39;operatore deve essere una delle costanti statiche della `Query.Statement` classe. In questo esempio viene utilizzato il valore statico `Query.Statement.OPERATOR_BEGINS_WITH` .
   * Un operando a destra contenente il valore dell&#39;attributo su cui eseguire la ricerca. In questo esempio, viene utilizzato l&#39;attributo name, un `String` contenente il valore `"testResource"`.
   Specificare lo spazio dei nomi dell&#39;operando a sinistra richiamando il `Query.Statement` metodo dell&#39;oggetto e passando uno dei valori statici contenuti nella `setNamespace` `com.adobe.repository.infomodel.bean.ResourceProperty` classe. In questo esempio `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` viene utilizzato.

   Aggiungete ogni istruzione alla query richiamando il metodo dell&#39; `Query` oggetto `addStatement` e passando l&#39; `Query.Statement` oggetto.

1. Creare l’ordinamento per i risultati della ricerca

   Per specificare l&#39;ordinamento utilizzato nei risultati della ricerca, create un `com.adobe.repository.query.sort.SortOrder` oggetto richiamando il costruttore predefinito per la `SortOrder` classe e aggiungendo elementi all&#39;ordinamento.

   Per creare un elemento per l&#39;ordinamento, richiamare uno dei costruttori della `com.adobe.repository.query.sort.SortOrder.Element` classe. In questo esempio, poiché il nome della risorsa viene utilizzato come base per la ricerca, il valore statico `Resource.ATTRIBUTE_NAME` viene utilizzato come primo parametro, e l&#39;ordine crescente (un `boolean` valore di `true`) viene specificato come secondo parametro.

   Aggiungete ciascun elemento all&#39;ordinamento richiamando il metodo dell&#39; `SortOrder` oggetto `addSortElement` e passando l&#39; `SortOrder.Element` oggetto.

1. Ricerca delle risorse

   Per eseguire una ricerca `resources` basata sulle proprietà dell&#39;attributo, richiamare il metodo dell&#39; `ResourceRepositoryClient` oggetto `searchProperties` e trasmettere i seguenti parametri:

   * Un `String` contenente il percorso di base da cui eseguire la ricerca. In questo caso `"/testFolder"` viene utilizzato.
   * Query utilizzata nella ricerca.
   * Profondità della ricerca. In questo caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` viene utilizzato per indicare che deve essere utilizzato il percorso di base e tutte le relative cartelle.
   * Un `int` valore che indica la prima riga da cui selezionare il set di risultati non di paging. In questo esempio `0` è specificato.
   * Un `int` valore che indica il numero massimo di risultati da restituire. In questo esempio `10` è specificato.
   * Ordine utilizzato nella ricerca.
   Il metodo restituisce un insieme `java.util.List` di `Resource` oggetti nell&#39;ordinamento specificato.

1. Recuperare le risorse dal risultato della ricerca

   Per recuperare le risorse contenute nel risultato della ricerca, ripetere l&#39;iterazione `List` e unire ciascun oggetto a un `Resource` per estrarne le informazioni. In questo esempio viene visualizzato il nome di ogni risorsa.

**Consulta anche**

[Ricerca di risorse](aem-forms-repository.md#searching-for-resources)

[Avvio rapido (modalità SOAP): Ricerca di risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creazione di relazioni tra risorse {#creating-resource-relationships}

Potete specificare le relazioni tra le risorse nella directory archivio. Esistono tre tipi di relazioni:

* **Dipendenza**: una relazione in cui una risorsa dipende da altre risorse, il che significa che tutte le risorse correlate sono necessarie nella directory archivio.
* **Appartenenza (file system)**: una relazione in cui una risorsa si trova all’interno di una determinata cartella.
* **Personalizzato**: una relazione specificata tra le risorse. Ad esempio, se una risorsa è stata rimossa e un’altra è stata introdotta nella directory archivio, è possibile specificare una relazione sostitutiva specifica.

Potete creare relazioni personalizzate. Ad esempio, se archiviate un file HTML nell&#39;archivio e ne utilizza un&#39;immagine, potete specificare una relazione personalizzata per correlare il file HTML all&#39;immagine (poiché in genere solo i file XML sono associati alle immagini utilizzando una relazione di dipendenza definita dall&#39;archivio). Un altro esempio di relazione personalizzata potrebbe essere se si desidera creare una vista diversa del repository con una struttura grafico ciclica invece di una struttura ad albero. Potete definire un grafico circolare con un visualizzatore per scorrere tali relazioni. Infine, è possibile indicare che una risorsa sostituisce un&#39;altra anche se le due risorse sono completamente diverse. In tal caso, è possibile definire un tipo di relazione al di fuori dell&#39;intervallo riservato e creare una relazione tra le due risorse. L&#39;applicazione sarebbe l&#39;unico client in grado di rilevare ed elaborare la relazione e potrebbe essere utilizzato per eseguire ricerche su tale relazione.

Potete specificare a livello di programmazione le relazioni tra le risorse utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per specificare una relazione tra due risorse, procedere come segue:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificate gli URI delle risorse da correlare.
1. Creare la relazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare gli URI delle risorse da correlare**

Creare stringhe contenenti gli URI della risorsa da correlare. La sintassi include le barre, come in questo esempio: &quot;/*path*/*resource*&quot;.

**Creare la relazione**

Richiamare il metodo del servizio Repository per creare e specificare il tipo di relazione.

**Consulta anche**

[Creazione di risorse sulle relazioni mediante l&#39;API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Creazione di risorse sulle relazioni mediante l&#39;API del servizio Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creazione di risorse sulle relazioni mediante l&#39;API Java {#create-relationship-resources-using-the-java-api}

Create le risorse delle relazioni utilizzando l&#39;API Java del servizio Repository ed eseguite le seguenti operazioni:

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificare gli URI delle risorse da correlare

   Specificate gli URI delle risorse da correlare. In questo caso, poiché le risorse sono denominate `testResource1` e `testResource2` si trovano nella cartella denominata `testFolder`, i relativi URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Gli URI sono memorizzati come `java.lang.String` oggetti. In questo esempio, le risorse vengono scritte per la prima volta nella directory archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, consultate [Creazione di risorse](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiama il metodo dell’ `ResourceRepositoryClient` oggetto `createRelationship` e passa i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Il tipo di relazione, che è una delle costanti statiche della `com.adobe.repository.infomodel.bean.Relation` classe. In questo esempio, una relazione di dipendenza viene stabilita specificando il valore `Relation.TYPE_DEPENDANT_OF`.
   * Un `boolean` valore che indica se la risorsa di destinazione viene aggiornata automaticamente all&#39;identificatore `com.adobe.repository.infomodel.Id`basato sulla nuova risorsa principale. In questo esempio, a causa della relazione di dipendenza, il valore `true` è specificato.
   È inoltre possibile recuperare un elenco delle risorse correlate per una determinata risorsa richiamando il metodo dell’ `ResourceRepositoryClient` oggetto `getRelated` e passando i seguenti parametri:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio viene specificata la risorsa di origine ( `"/testFolder/testResource1"`).
   * Un `boolean` valore che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché è il caso.
   * Il tipo di relazione, che è una delle costanti statiche della `Relation` classe. In questo esempio, una relazione di dipendenza viene specificata utilizzando lo stesso valore utilizzato in precedenza: `Relation.TYPE_DEPENDANT_OF`.
   Il `getRelated` metodo restituisce un `java.util.List` insieme di `Resource` oggetti attraverso i quali è possibile iterare per recuperare ciascuna delle risorse correlate, raggruppando gli oggetti contenuti `List` in `Resource` . In questo esempio `testResource2` è previsto che si trovi nell&#39;elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Avvio rapido (modalità SOAP): Creazione di relazioni tra risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di risorse sulle relazioni mediante l&#39;API del servizio Web {#create-relationship-resources-using-the-web-service-api}

Creare risorse sulle relazioni utilizzando l&#39;API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specificare gli URI delle risorse da correlare

   Specificate gli URI delle risorse da correlare. In questo caso, poiché le risorse sono denominate `testResource1` e `testResource2` si trovano nella cartella denominata `testFolder`, i relativi URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Quando si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), gli URI vengono memorizzati come `System.String` oggetti. In questo esempio, le risorse vengono scritte per la prima volta nella directory archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, consultate [Creazione di risorse](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiama il metodo dell’ `RepositoryServiceService` oggetto `createRelationship` e passa i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Tipo di relazione. In questo esempio, una relazione di dipendenza viene stabilita specificando il valore `3`.
   * Un `boolean` valore che indica se è stato specificato il tipo di relazione. In questo esempio, il valore `true` è specificato.
   * Un `boolean` valore che indica se la risorsa di destinazione viene aggiornata automaticamente all&#39;identificatore `Id`basato sulla nuova risorsa principale. In questo esempio, a causa della relazione di dipendenza, il valore `true` è specificato.
   * Un `boolean` valore che indica se è stata specificata l&#39;intestazione di destinazione. In questo esempio, il valore `true` è specificato.
   * Passa `null` per l&#39;ultimo parametro.
   È inoltre possibile recuperare un elenco delle risorse correlate per una determinata risorsa richiamando il metodo dell’ `RepositoryServiceService` oggetto `getRelated` e passando i seguenti parametri:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio viene specificata la risorsa di origine ( `"/testFolder/testResource1"`).
   * Un `boolean` valore che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché è il caso.
   * Un `boolean` valore che indica se è stata specificata la risorsa di origine. In questo esempio, il valore `true` viene fornito.
   * Un array di numeri interi contenente i tipi di relazione. In questo esempio, una relazione di dipendenza viene specificata utilizzando lo stesso valore nell&#39;array utilizzato in precedenza: `3`.
   * Passa `null` per i due parametri rimanenti.
   Il `getRelated` metodo restituisce un array di oggetti che possono essere inseriti in `Resource` oggetti attraverso i quali è possibile iterare per recuperare ciascuna delle risorse correlate. In questo esempio `testResource2` è previsto che si trovi nell&#39;elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Blocco delle risorse {#locking-resources}

È possibile bloccare una risorsa o un set di risorse da utilizzare esclusivamente da un particolare utente o da un uso condiviso tra più utenti. Un blocco condiviso è un&#39;indicazione che qualcosa accadrà con la risorsa, ma non impedisce ad altri di intraprendere azioni con quella risorsa. Un blocco condiviso dovrebbe essere considerato un meccanismo di segnalazione. Un blocco esclusivo indica che l&#39;utente che ha bloccato la risorsa cambierà la risorsa e il blocco assicura che nessun altro possa farlo finché l&#39;utente non avrà più bisogno dell&#39;accesso alla risorsa e non avrà rilasciato il blocco. Se un amministratore del repository sblocca una risorsa, tutti i blocchi esclusivi e condivisi presenti sulla risorsa verranno automaticamente rimossi. Questo tipo di azione è destinato alle situazioni in cui un utente non è più disponibile e non ha sbloccato la risorsa.

Quando una risorsa è bloccata, quando si visualizza la scheda Risorse in Workbench viene visualizzata un&#39;icona a forma di lucchetto, come illustrato nella figura riportata di seguito.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Potete controllare l&#39;accesso alle risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per bloccare e sbloccare le risorse, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificate l’URI della risorsa da bloccare.
1. Bloccate la risorsa.
1. Recuperare i blocchi per la risorsa.
1. Sblocca risorsa

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare l&#39;URI della risorsa da bloccare**

Create una stringa contenente l’URI della risorsa da bloccare. La sintassi include le barre, come in questo esempio: &quot;/*path*/*resource*&quot;.

**Blocca risorsa**

Richiamare il metodo del servizio Repository per bloccare la risorsa, specificando l’URI, il tipo di blocco e la profondità di blocco.

**Recuperare i blocchi per la risorsa**

Richiamare il metodo del servizio Repository per recuperare i blocchi per la risorsa, specificando l&#39;URI.

**Sblocca risorsa**

Richiamare il metodo del servizio Repository per sbloccare la risorsa, specificando l&#39;URI.

**Consulta anche**

[Blocco delle risorse tramite l&#39;API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Blocco delle risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Blocco delle risorse tramite l&#39;API Java {#lock-resources-using-the-java-api}

Bloccare le risorse utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificare l&#39;URI della risorsa da bloccare

   Specificate l’URI della risorsa da bloccare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResource"`. L&#39;URI è memorizzato come `java.lang.String` oggetto.

1. Blocca risorsa

   Richiama il metodo dell’ `ResourceRepositoryClient` oggetto `lockResource` e passa i seguenti parametri:

   * URI della risorsa.
   * L&#39;ambito di blocco. In questo esempio, poiché la risorsa verrà bloccata per l&#39;uso esclusivo, l&#39;ambito del blocco viene specificato come `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * La profondità di blocco. In questo esempio, poiché il blocco viene applicato solo alla risorsa specifica e nessuno dei relativi membri o elementi secondari, la profondità di blocco viene specificata come `Lock.DEPTH_ZERO`.
   >[!NOTE]
   >
   >La versione sovraccaricata del `lockResource` metodo che richiede quattro parametri genera un&#39;eccezione. Assicurarsi di utilizzare il `lockResource` metodo che richiede tre parametri, come illustrato in questa procedura dettagliata.

1. Recuperare i blocchi per la risorsa

   Richiamate il metodo dell’ `ResourceRepositoryClient` oggetto `getLocks` e passate l’URI della risorsa come parametro. Il metodo restituisce un elenco di oggetti Lock attraverso il quale è possibile eseguire l&#39;iterazione. In questo esempio, il proprietario del blocco, la profondità e l&#39;ambito vengono stampati per ciascun oggetto richiamando rispettivamente i `getOwnerUserId`, `getDepth`e `getType` metodi di ciascun oggetto Lock.

1. Sblocca risorsa

   Richiamate il metodo dell’ `ResourceRepositoryClient` oggetto `unlockResource` e passate l’URI della risorsa come parametro. Per ulteriori informazioni, consulta la Guida di riferimento [alle API per](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Avvio rapido (modalità SOAP): Blocco di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Blocco delle risorse tramite l&#39;API del servizio Web {#lock-resources-using-the-web-service-api}

Bloccare le risorse utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da bloccare

   Specificate una stringa contenente l’URI della risorsa da bloccare. In questo caso, poiché la risorsa denominata `testResource` è nella cartella `testFolder`, il relativo URI è `"/testFolder/testResource"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un `System.String` oggetto.

1. Blocca risorsa

   Richiama il metodo dell’ `RepositoryServiceService` oggetto `lockResource` e passa i seguenti parametri:

   * URI della risorsa.
   * L&#39;ambito di blocco. In questo esempio, poiché la risorsa verrà bloccata per l&#39;uso esclusivo, l&#39;ambito del blocco viene specificato come `11`.
   * La profondità di blocco. In questo esempio, poiché il blocco viene applicato solo alla risorsa specifica e nessuno dei relativi membri o elementi secondari, la profondità di blocco viene specificata come `2`.
   * Un `int` valore che indica il numero di secondi prima della scadenza del blocco. In questo esempio, `1000` viene utilizzato il valore di.
   * Passa `null` per l&#39;ultimo parametro.

1. Recuperare i blocchi per la risorsa

   Richiamate il metodo dell’ `RepositoryServiceService` oggetto `getLocks` e passate l’URI della risorsa come primo parametro e `null` per il secondo parametro. Il metodo restituisce una `object` matrice contenente `Lock` oggetti attraverso i quali è possibile iterare. In questo esempio, il proprietario del blocco, la profondità e l&#39;ambito vengono stampati per ciascun oggetto accedendo rispettivamente ai campi `Lock` , `ownerUserId`e `depth``type` ai campi di ciascun oggetto.

1. Sblocca risorsa

   Richiamate il metodo dell’ `RepositoryServiceService` oggetto `unlockResource` e passate l’URI della risorsa come primo parametro e `null` per il secondo parametro.

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Eliminazione delle risorse {#deleting-resources}

È possibile eliminare programmaticamente le risorse da una determinata posizione nell&#39;archivio utilizzando l&#39;API Java (SOAP) del servizio Repository.

Quando si elimina una risorsa, l&#39;eliminazione è in genere permanente, anche se in alcuni casi i repository ECM possono memorizzare le versioni della risorsa in base ai meccanismi della cronologia. Pertanto, quando si elimina una risorsa, è importante essere certi di non averne più bisogno. I motivi comuni per eliminare una risorsa includono la necessità di aumentare lo spazio disponibile nel database. È possibile eliminare una versione di una risorsa, ma in questo caso è necessario specificare l&#39;identificatore della risorsa e non il relativo identificatore logico (LID) o percorso. Se eliminate una cartella, tutti gli elementi in essa contenuti, comprese le sottocartelle e le risorse, verranno eliminati automaticamente.

Le risorse correlate non vengono eliminate. Ad esempio, se si dispone di un modulo che utilizza il file logo.gif ed eliminate logo.gif, nella tabella delle relazioni in sospeso verrà memorizzata una relazione. In alternativa, per la versione obsoleta imposta lo stato dell’oggetto dell’ultima versione su obsoleto.

Un&#39;operazione di eliminazione non è sicura per le transazioni nei sistemi ECM. Ad esempio, se tentate di eliminare 100 risorse e l&#39;operazione ha esito negativo sulla 50° risorsa, le prime 49 istanze verranno eliminate ma il resto non verrà eliminato. In caso contrario, il comportamento predefinito è rollback (non impegno).

>[!NOTE]
>
>Se si utilizza il `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` metodo con il repository ECM (EMC Documentum Content Server e IBM FileNet P8 Content Manager), la transazione non verrà ripristinata se l&#39;eliminazione non riesce per una delle risorse specificate, il che significa che i file che sono stati eliminati non possono essere eliminati.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per eliminare una risorsa, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificate l’URI della risorsa da eliminare.
1. Eliminare la risorsa.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare l&#39;URI della risorsa da eliminare**

Create una stringa contenente l’URI della risorsa da eliminare. La sintassi include le barre, come in questo esempio: &quot;/*path*/*resource*&quot;. Se la risorsa da eliminare è una cartella, l’eliminazione sarà ricorsiva.

**Eliminare la risorsa**

Richiamare il metodo del servizio Repository per eliminare la risorsa, specificando l&#39;URI.

**Consulta anche**

[Eliminare le risorse tramite l&#39;API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Eliminare le risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Eliminare risorse tramite Java API(SOAP) {#delete-resources-using-the-java-api-soap}

Eliminate una risorsa utilizzando l&#39;API Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un `ResourceRepositoryClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificare l&#39;URI della risorsa da eliminare

   Specificate l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata testResourceToBeDeleted si trova nella cartella denominata testFolder, il relativo URI è `/testFolder/testResourceToBeDeleted`. L&#39;URI è memorizzato come `java.lang.String` oggetto. In questo esempio, la risorsa viene scritta per la prima volta nella directory archivio e viene recuperato il relativo URI. Per ulteriori informazioni sulla scrittura di una risorsa, consultate [Creazione di risorse](aem-forms-repository.md#writing-resources).

1. Eliminare la risorsa

   Richiamate il metodo dell’ `ResourceRepositoryClient` oggetto `deleteResource` e passate l’URI della risorsa come parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Avvio rapido (modalità SOAP): Ricerca di risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminare le risorse tramite l&#39;API del servizio Web {#delete-resources-using-the-web-service-api}

Eliminate una risorsa utilizzando l&#39;API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `RepositoryServiceService` oggetto richiamando il relativo costruttore predefinito. Impostate la relativa `Credentials` proprietà utilizzando un `System.Net.NetworkCredential` oggetto contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da eliminare

   Specificate l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata `testResourceToBeDeleted` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResourceToBeDeleted"`. In questo esempio, la risorsa viene scritta per la prima volta nella directory archivio e viene recuperato il relativo URI. Per ulteriori informazioni sulla scrittura di una risorsa, consultate [Creazione di risorse](aem-forms-repository.md#writing-resources).

1. Eliminare la risorsa

   Richiamate il metodo dell’ `RepositoryServiceService` oggetto `deleteResources` e passate un `System.String` array contenente l’URI della risorsa come primo parametro. Passa `null` per il secondo parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
