---
title: Utilizzo di  archivio AEM Forms
seo-title: Utilizzo di  archivio AEM Forms
description: 'null'
seo-description: 'null'
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '9076'
ht-degree: 0%

---


# Utilizzo  repository AEM Forms {#working-with-aem-forms-repository}

**Informazioni su Repository Service**

Il servizio Repository fornisce servizi di archiviazione e gestione delle risorse per  AEM Forms. Quando gli sviluppatori creano un&#39;applicazione *AEM Forms*, possono distribuire le risorse nella directory archivio invece che nel file system. Le risorse possono includere qualsiasi tipo di materiale collaterale, inclusi moduli XML, PDF forms (inclusi  moduli Acrobat), frammenti di modulo, immagini, profili, criteri, file SWF, file DDX, schemi XML, file WSDL e dati di prova.

Ad esempio, prendere in considerazione la seguente applicazione Forms denominata *Applicazioni/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Tenere presente che nella cartella FormsFolder è presente un file denominato Loan.xdp. Per accedere a questa struttura del modulo, è necessario specificare il percorso completo (inclusa la versione): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms utilizzando Workbench, vedere la Guida di Workbench [Guida](https://www.adobe.com/go/learn_aemforms_workbench_63).

Il percorso di una risorsa che si trova nell&#39;archivio di AEM Forms  è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>È possibile esplorare  archivio AEM Forms utilizzando un browser Web. Per esplorare la directory archivio, immettete il seguente URL in un browser Web `https://[server name]:[server port]/repository`. È possibile verificare i risultati di avvio rapido associati alla sezione Utilizzo  repository di AEM Forms utilizzando un browser Web. Ad esempio, se aggiungete contenuto all&#39;archivio AEM Forms , potete visualizzarne il contenuto in un browser Web. (Vedere [Avvio rapido (modalità SOAP): Scrittura di una risorsa mediante l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).

L&#39;API del repository fornisce una serie di operazioni che è possibile utilizzare per memorizzare e recuperare informazioni dal repository. Ad esempio, è possibile ottenere un elenco di risorse o recuperare risorse specifiche memorizzate nella directory archivio quando una risorsa è necessaria durante l&#39;elaborazione di un&#39;applicazione.

>[!NOTE]
>
>L&#39;API dell&#39;archivio non può essere utilizzata per interagire con Content Services (obsoleto). Per interagire con Content Services (obsoleto), utilizzate Document Management API.

Utilizzando l&#39;API del servizio Repository, potete eseguire le seguenti operazioni:

* Creare cartelle. Vedere [Creazione di cartelle](aem-forms-repository.md#creating-folders).
* Scrivere le risorse e le relative proprietà. Vedere [Risorse di scrittura](aem-forms-repository.md#writing-resources).
* Elenca le risorse in una raccolta specifica o correlate ad altre risorse. Vedere [Risorse di elenco](aem-forms-repository.md#listing-resources).
* Leggere le risorse e le relative proprietà. Vedere [Risorse di lettura](aem-forms-repository.md#reading-resources).
* Aggiornare le risorse e le relative proprietà. Vedere [Aggiornamento delle risorse](aem-forms-repository.md#updating-resources).
* Cercare risorse, inclusa la cronologia, le risorse correlate e le proprietà. Vedere [Ricerca di risorse](aem-forms-repository.md#searching-for-resources).
* Specificare le relazioni tra le risorse. Vedere [Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships).
* Gestire il controllo dell&#39;accesso alle risorse, incluso il blocco e lo sblocco delle risorse, nonché la lettura e la scrittura degli elenchi di controllo dell&#39;accesso (ACL). Vedere [Risorse di blocco](aem-forms-repository.md#locking-resources).
* Eliminare le risorse e le relative proprietà. Vedere [Eliminazione delle risorse](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Utilizzando l&#39;API del repository non è possibile gestire il controllo dell&#39;accesso alle risorse, cercare risorse o specificare relazioni tra risorse utilizzando un repository ECM.

>[!NOTE]
>
>Quando un PDF crittografato viene scritto nell&#39;archivio, non è possibile utilizzare la funzione di estrazione relazione automatica. In caso contrario, un PDF crittografato può essere memorizzato nella directory archivio e successivamente recuperato. Il recuperatore può scegliere di decrittografare il PDF dopo averlo recuperato dalla directory archivio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di cartelle {#creating-folders}

Le cartelle (raccolte di risorse) vengono utilizzate per memorizzare oggetti (file o risorse) in raggruppamenti organizzati. Le cartelle possono contenere risorse e altre cartelle, dette anche sottocartelle. Le risorse possono essere memorizzate in una sola cartella alla volta.

I file ereditano gli elenchi di controllo di accesso (ACL, Access Control List) dalle cartelle e le sottocartelle ereditano gli ACL dalle relative cartelle principali. Pertanto, le cartelle principali devono esistere prima di poter creare cartelle figlie. L’IDE consente di interagire solo a livello di cartella per cartella, non a livello di singolo file. Non è possibile eseguire la versione delle cartelle e non è necessario farlo; una cartella non contiene i dati stessi. ma solo un contenitore per le risorse che contengono dati. L&#39;ACL predefinito è un&#39;autorizzazione a livello di sistema, il che significa che gli utenti devono disporre di autorizzazioni a livello di sistema (lettura, scrittura, lettura, gestione ACL) fino a quando qualcuno non conceda loro le autorizzazioni per una determinata cartella. Gli ACL funzionano solo nell&#39;IDE.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Richiamare il metodo del servizio Repository per creare la raccolta di risorse e compilare la raccolta di risorse con le informazioni di identificazione, incluso il relativo UUID, il nome della cartella e la descrizione.

**Scrivere la cartella nella directory archivio**

Richiamare il metodo del servizio Repository per scrivere la raccolta di risorse, specificando l&#39;URI della cartella di destinazione.

**Consulta anche**

[Creare cartelle utilizzando l&#39;API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Creazione di cartelle tramite l&#39;API del servizio Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creare cartelle utilizzando l&#39;API Java {#create-folders-using-the-java-api}

Create una cartella utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file di progetto nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Creare la cartella

   Per creare una raccolta di risorse, è innanzitutto necessario creare un oggetto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Richiamare il metodo `repositoryInfomodelFactoryBean` dell&#39;oggetto `newResourceCollection` e trasmettere i seguenti parametri:

   * Un identificatore UUID `com.adobe.repository.infomodel.Id` da assegnare alla risorsa.
   * Un identificatore UUID `com.adobe.repository.infomodel.Lid` da assegnare alla risorsa.
   * Un `java.lang.String` contenente il nome della raccolta di risorse. Esempio, `FormsFolder`.

   Il metodo restituisce un oggetto `com.adobe.repository.infomodel.bean.ResourceCollection` che rappresenta la nuova cartella.

   Impostate la descrizione della cartella utilizzando il metodo `setDescription` e passate il seguente parametro:

   * Un `String` che descrive la raccolta di risorse. In questo esempio, viene utilizzato `"test Folder"``.`


1. Scrivere la cartella nella directory archivio

   Richiamare il metodo `ResourceRepositoryClient` dell&#39;oggetto `writeResource` e trasmettere l&#39;URI della cartella e l&#39;oggetto `ResourceCollection`. Ad esempio, l&#39;URI della cartella può essere il seguente valore `/Applications/FormsApplication/1.0/`.

   Il metodo restituisce un&#39;istanza dell&#39;oggetto `com.adobe.repository.infomodel.bean.Resource` appena creato. È possibile, ad esempio, recuperare il valore identificatore della nuova risorsa richiamando il metodo `com.adobe.repository.infomodel.bean.Resource` dell&#39;oggetto `getId`.

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Avvio rapido (modalità SOAP): Creazione di una cartella mediante l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare cartelle utilizzando l&#39;API del servizio Web {#create-folders-using-the-web-service-api}

Create una cartella utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` che contiene il nome utente e la password.

1. Creare la cartella

   Create la cartella utilizzando il costruttore predefinito per la classe `ResourceCollection` e trasmettete i seguenti parametri:

   * Un oggetto `Id`, creato richiamando il costruttore predefinito per la classe `Id` e assegnato al campo `Resource` dell&#39;oggetto `id`.
   * Un oggetto `Lid`, creato richiamando il costruttore predefinito per la classe `Lid` e assegnato al campo `Resource` dell&#39;oggetto `lid`.
   * Una stringa contenente il nome della raccolta di risorse, assegnata al campo `Resource` dell&#39;oggetto `name`. Il nome utilizzato in questo esempio è `"testfolder"`.
   * Una stringa contenente la descrizione della raccolta di risorse, assegnata al campo `Resource` dell&#39;oggetto `description`. La descrizione utilizzata in questo esempio è `"test folder"`.

1. Scrivere la cartella nella directory archivio

   Richiamare il metodo `RepositoryServiceService` dell&#39;oggetto `writeResource` e trasmettere i seguenti parametri:

   * Percorso in cui creare la cartella.
   * L&#39;oggetto `ResourceCollection` che rappresenta la cartella.
   * Passare `null` per gli altri due parametri.

**Consulta anche**

[Creazione di cartelle](aem-forms-repository.md#creating-folders)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Risorse di scrittura {#writing-resources}

Potete creare risorse in una determinata posizione nella directory archivio. La dimensione del file naturale è soggetta alle limitazioni del database e al timeout della sessione. Per la configurazione predefinita, i file sono limitati a 25 MB. Per aumentare o ridurre la dimensione massima del file, è necessario modificare la configurazione del database.

La scrittura di risorse equivale alla memorizzazione dei dati nell&#39;archivio. Dopo aver scritto una risorsa nella directory archivio, questa diventa accessibile a tutti i client dell’ecosistema della directory archivio. Quando si scrivono risorse, come schemi XML, file XDP e file XSD, nell&#39;archivio, i contenuti vengono analizzati in base al tipo MIME. Se il tipo MIME è supportato, il parser determina se esiste una relazione implicita con altro contenuto. Ad esempio, se un foglio di stile CSS ha un URL relativo che fa riferimento a un CSS comune, è previsto che invierete anche il CSS comune nell&#39;archivio. La relazione tra le due risorse viene memorizzata come relazione in sospeso per un periodo non regolabile di 30 giorni. Quando inviate il CSS comune alla directory archivio entro 30 giorni, la relazione viene formata.

Quando create una risorsa, l&#39;elenco di controllo di accesso (ACL, Access Control List) viene ereditato dalla cartella principale. La cartella principale dispone di autorizzazioni a livello di sistema fino alla creazione di una risorsa o di una cartella iniziale, al punto in cui alla risorsa o alla cartella vengono assegnate autorizzazioni ACL predefinite.

Potete scrivere le risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per scrivere una risorsa, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificate l’URI della risorsa da leggere.
1. Leggete la risorsa.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare l&#39;URI della cartella di destinazione per la risorsa**

Create una stringa contenente l’URI della risorsa da leggere. La sintassi include le barre, come in questo esempio: &quot;/*percorso*/*cartella*&quot;.

**Creare la risorsa**

Richiama il metodo del servizio Repository per creare la risorsa e compila la risorsa con informazioni identificative, incluso il suo UUID, il nome della risorsa e la descrizione.

**Specificare il contenuto della risorsa**

Richiamare il metodo del servizio Repository per creare il contenuto delle risorse e archiviarlo nella risorsa.

**Scrivere la risorsa nella cartella di destinazione**

Richiamate il metodo del servizio Repository per scrivere la risorsa, specificando l’URI della cartella di destinazione.

**Consulta anche**

[Scrivere risorse tramite l&#39;API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Creazione di risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creazione di risorse tramite Java API {#write-resources-using-the-java-api}

Scrivere una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare l&#39;URI della cartella di destinazione per la risorsa

   Specificate l’URI della cartella di destinazione per la risorsa. In questo caso, poiché la risorsa denominata `testResource` verrà memorizzata nella cartella denominata `testFolder`, l&#39;URI della cartella è `"/testFolder"`. L&#39;URI è memorizzato come oggetto `java.lang.String`.

1. Creare la risorsa

   Per creare una risorsa, è innanzitutto necessario creare un oggetto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Richiamare il metodo `RepositoryInfomodelFactoryBean` dell&#39;oggetto `newResource`, che crea un oggetto `com.adobe.repository.infomodel.bean.Resource`. In questo esempio, vengono forniti i seguenti parametri:

   * Un oggetto `com.adobe.repository.infomodel.Id`, creato richiamando il costruttore predefinito per la classe `Id`.
   * Un oggetto `com.adobe.repository.infomodel.Lid`, creato richiamando il costruttore predefinito per la classe `Lid`.
   * Un `java.lang.String` contenente il nome file della risorsa.

   Per specificare la descrizione della risorsa, richiamare il metodo `setDescription` dell&#39;oggetto `Resource` e passare una stringa contenente la descrizione. In questo esempio, la descrizione è `"test resource"`.

1. Specificare il contenuto della risorsa

   Per creare contenuto per la risorsa, richiamare il metodo `RepositoryInfomodelFactoryBean` dell&#39;oggetto `newResourceContent`, che restituisce un oggetto &lt;a2/>. `com.adobe.repository.infomodel.bean.ResourceContent` Aggiungere contenuto all&#39;oggetto `ResourceContent`. In questo esempio, questo si ottiene eseguendo le seguenti operazioni:

   * Chiamata del metodo `ResourceContent` dell&#39;oggetto `setDataDocument` e trasmissione di un oggetto `com.adobe.idp.Document`
   * Chiamata del metodo `ResourceContent` dell&#39;oggetto `setSize` e trasmissione delle dimensioni in byte dell&#39;oggetto `Document`

   Aggiungete il contenuto alla risorsa richiamando il metodo `Resource` dell&#39;oggetto `setContent` e passando l&#39;oggetto &lt;a2/>. `ResourceContent` Per ulteriori informazioni, vedere [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Scrivere la risorsa nella cartella di destinazione

   Richiamare il metodo `ResourceRepositoryClient` dell&#39;oggetto `writeResource` e trasmettere l&#39;URI della cartella, nonché l&#39;oggetto `Resource`.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Avvio rapido (modalità SOAP): Creazione di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di risorse tramite l&#39;API del servizio Web {#write-resources-using-the-web-service-api}

Scrivere una risorsa utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare l&#39;URI della cartella di destinazione per la risorsa

   Specificate l’URI della cartella di destinazione per la risorsa. In questo caso, poiché la risorsa denominata `testResource` verrà memorizzata nella cartella denominata `testFolder`, l&#39;URI della cartella è `"/testFolder"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un oggetto `System.String`.

1. Creare la risorsa

   Per creare una risorsa, richiamare il costruttore predefinito per la classe `Resource`. In questo esempio, nell&#39;oggetto `Resource` sono memorizzate le informazioni seguenti:

   * Un oggetto `com.adobe.repository.infomodel.Id`, creato richiamando il costruttore predefinito per la classe `Id` e assegnato al campo `Resource` dell&#39;oggetto `id`.
   * Un oggetto `com.adobe.repository.infomodel.Lid`, creato richiamando il costruttore predefinito per la classe `Lid` e assegnato al campo `Resource` dell&#39;oggetto `lid`.
   * Una stringa che contiene il nome file della risorsa, assegnato al campo `Resource` dell&#39;oggetto `name`. Il nome utilizzato in questo esempio è `"testResource"`.
   * Una stringa contenente la descrizione della risorsa, assegnata al campo `Resource` dell&#39;oggetto `description`. La descrizione utilizzata in questo esempio è `"test resource"`.

1. Specificare il contenuto della risorsa

   Per creare contenuto per la risorsa, richiamare il costruttore predefinito per la classe `ResourceContent`. Quindi aggiungere il contenuto all&#39;oggetto `ResourceContent`. In questo esempio, questo si ottiene eseguendo le seguenti operazioni:

   * Assegnazione di un oggetto `BLOB` contenente un documento al campo `ResourceContent` dell&#39;oggetto `dataDocument`.
   * Assegnazione delle dimensioni in byte dell&#39;oggetto `BLOB` al campo `ResourceContent` dell&#39;oggetto `size`.

   Aggiungete il contenuto alla risorsa assegnando l&#39;oggetto `ResourceContent` al campo `Resource` dell&#39;oggetto `content`.

1. Scrivere la risorsa nella cartella di destinazione

   Richiamare il metodo `RepositoryServiceService` dell&#39;oggetto `writeResource` e trasmettere l&#39;URI della cartella, nonché l&#39;oggetto `Resource`. Passare `null` per gli altri due parametri.

**Consulta anche**

[Scrittura delle risorse](aem-forms-repository.md#writing-resources)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Risorse di elenco {#listing-resources}

Potete scoprire le risorse elencando le risorse. Nell&#39;archivio viene eseguita una query per individuare tutte le risorse correlate a una determinata raccolta di risorse.

Una volta organizzate le risorse, potete ispezionare la struttura creata visualizzando un particolare ramo della struttura, come si fa in un sistema operativo.

Le risorse di elenco operano per relazione: le risorse sono membri di cartelle. L&#39;appartenenza è rappresentata da una relazione di tipo &quot;membro di&quot;. Quando si elencano le risorse in una determinata cartella, si esegue una query per individuare le risorse correlate a una determinata cartella dalla relazione &quot;membro di&quot;. Le relazioni sono direzionali: un membro di una relazione ha un&#39;origine che è membro dell&#39;oggetto. L&#39;origine è la risorsa; la destinazione è la cartella principale.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Create una stringa contenente il percorso della cartella contenente le risorse. La sintassi include le barre, come in questo esempio: &quot;/*percorso*/*cartella*&quot;.

**Recuperare l’elenco delle risorse**

Richiamare il metodo del servizio Repository per recuperare l’elenco delle risorse, specificando il percorso della cartella di destinazione.

**Consulta anche**

[Elenca le risorse tramite l&#39;API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Elenca le risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Elenca le risorse tramite l&#39;API Java {#list-resources-using-the-java-api}

Elenca le risorse utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare il percorso della cartella

   Specificate l&#39;URI della raccolta di risorse da interrogare. In questo caso, l&#39;URI è `"/testFolder"`. L&#39;URI è memorizzato come oggetto `java.lang.String`.

1. Recuperare l’elenco delle risorse

   Richiamare il metodo `ResourceRepositoryClient` dell&#39;oggetto `listMembers` e trasmettere l&#39;URI della cartella.

   Il metodo restituisce un `java.util.List` di `com.adobe.repository.infomodel.bean.Resource` oggetti che costituiscono l&#39;origine di un `com.adobe.repository.infomodel.bean.Relation` di tipo `Relation.TYPE_MEMBER_OF` e che hanno come destinazione l&#39;URI di raccolta delle risorse. Potete eseguire un&#39;iterazione su questa `List` per recuperare ciascuna delle risorse. In questo esempio vengono visualizzati il nome e la descrizione di ogni risorsa.

**Consulta anche**

[Risorse](aem-forms-repository.md#listing-resources) di elenco.

[Avvio rapido (modalità SOAP): Elencare le risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Elenca le risorse utilizzando l&#39;API del servizio Web {#list-resources-using-the-web-service-api}

Elenca le risorse utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare il percorso della cartella

   Specificate una stringa contenente l’URI della cartella alla quale verrà chiesto di eseguire la query. In questo caso, l&#39;URI è `"/testFolder"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un oggetto `System.String`.

1. Recuperare l’elenco delle risorse

   Richiamate il metodo `RepositoryServiceService` dell&#39;oggetto `listMembers` e passate l&#39;URI della cartella come primo parametro. Passare `null` per gli altri due parametri.

   Il metodo restituisce un array di oggetti che possono essere inseriti in oggetti `Resource`. È possibile iterare l&#39;array di oggetti per recuperare ciascuna delle risorse correlate. In questo esempio vengono visualizzati il nome e la descrizione di ogni risorsa.

**Consulta anche**

[Risorse](aem-forms-repository.md#listing-resources) di elenco.

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Risorse di lettura {#reading-resources}

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
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per leggere una risorsa, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Repository.
1. Specificate l’URI della risorsa da leggere.
1. Leggete la risorsa.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare il client del servizio**

Prima di poter leggere una risorsa a livello di programmazione, è necessario stabilire una connessione e fornire le credenziali. A tal fine, create un client di servizi.

**Specificare l&#39;URI della risorsa da leggere**

Create una stringa contenente l’URI della risorsa da leggere. La sintassi include le barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;.

**Leggere la risorsa**

Richiamare il metodo del servizio Repository per leggere la risorsa, specificando l&#39;URI.

**Consulta anche**

[Leggere le risorse tramite l&#39;API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lettura delle risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Leggi le risorse tramite l&#39;API Java {#read-resources-using-the-java-api}

Leggere una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare l&#39;URI della risorsa da leggere

   Specificate un valore di stringa che rappresenta l’URI della risorsa da recuperare. Ad esempio, se la risorsa è denominata *testResource* che si trova in una cartella denominata *testFolder*, specificare `/testFolder/testResource`.

1. Leggere la risorsa

   Richiamate il metodo `ResourceRepositoryClient` dell&#39;oggetto `readResource` e passate l&#39;URI della risorsa come parametro. Questo metodo restituisce un&#39;istanza `Resource` che rappresenta la risorsa.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Avvio rapido (modalità SOAP): Lettura di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lettura delle risorse tramite l&#39;API del servizio Web {#reading-resources-using-the-web-service-api}

Leggere una risorsa utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository. (Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da leggere

   Specificate una stringa contenente l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResource"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un oggetto `System.String`.

1. Leggere la risorsa

   Richiamate il metodo `RepositoryServiceService` dell&#39;oggetto `readResource` e passate l&#39;URI della risorsa come primo parametro. Passare `null` per gli altri due parametri.

**Consulta anche**

[Lettura delle risorse](aem-forms-repository.md#reading-resources)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Aggiornamento delle risorse {#updating-resources}

È possibile recuperare e aggiornare il contenuto delle risorse nella directory archivio. Quando aggiornate le risorse, il controllo di accesso a tali risorse rimane invariato tra le diverse versioni. Durante l&#39;esecuzione di un aggiornamento, potete scegliere di incrementare la versione principale. Se non si sceglie di incrementare la versione principale, la versione secondaria viene aggiornata automaticamente.

Quando aggiornate una risorsa, la nuova versione viene creata in base agli attributi della risorsa specificati. Quando aggiornate una risorsa, specificate due parametri importanti: l’URI di destinazione e un’istanza di risorsa contenente tutti i metadati aggiornati. È importante notare che se non modificate un dato attributo (ad esempio, il nome), l’attributo è comunque obbligatorio nell’istanza passata. Le relazioni create durante l&#39;analisi del contenuto vengono aggiunte alla versione specifica e non vengono portate avanti a meno che non sia specificato.

Ad esempio, se aggiornate un file XDP che contiene riferimenti ad altre risorse, anche tali riferimenti aggiuntivi verranno registrati. Supponiamo che form.xdp versione 1.0 abbia due riferimenti esterni: un logo e un foglio di stile, quindi si aggiorna form.xdp in modo che ora contenga tre riferimenti: un logo, un foglio di stile e un file di schema. Durante l&#39;aggiornamento, il repository aggiungerà la terza relazione (al file dello schema) alla tabella di relazione in sospeso. Una volta che il file dello schema è presente nella directory archivio, la relazione viene automaticamente formata. Tuttavia, se form.xdp versione 2.0 non utilizza più il logo, form.xdp versione 2.0 non avrà alcuna relazione con il logo.

Tutte le operazioni di aggiornamento sono atomiche e transazionali. Ad esempio, se due utenti leggono la stessa risorsa ed entrambi decidono di aggiornare la versione 1.0 alla versione 2.0, uno di questi avrà successo e uno di loro avrà esito negativo, l&#39;integrità del repository verrà mantenuta e a entrambi verrà visualizzato un messaggio di conferma del successo o dell&#39;errore. Se la transazione non viene confermata, verrà ripristinata in caso di errore del database e si verificherà il timeout o il rollback a seconda del server dell&#39;applicazione.

Potete aggiornare le risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Leggete la risorsa. Per ulteriori informazioni, vedere [Risorse di lettura](aem-forms-repository.md#reading-resources).

**Aggiornare la risorsa**

Impostate le nuove informazioni nella risorsa e richiamate il metodo del servizio Repository per aggiornare la risorsa, specificando l’URI, la risorsa aggiornata e la modalità di aggiornamento delle informazioni sulla versione.

**Consulta anche**

[Aggiornare le risorse tramite l&#39;API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Aggiornare le risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Aggiornare le risorse utilizzando l&#39;API Java {#update-resources-using-the-java-api}

Aggiornare una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recuperare la risorsa da aggiornare

   Specificate l’URI della risorsa da recuperare e leggere. In questo esempio, l&#39;URI della risorsa è `"/testFolder/testResource"`.

1. Aggiornare la risorsa

   Aggiornare le informazioni dell&#39;oggetto `Resource`. In questo esempio, per aggiornare la descrizione, richiamare il metodo `Resource` dell&#39;oggetto &lt;a1/> e passare la nuova stringa di descrizione come parametro.`setDescription`

   Quindi, richiamare il metodo `ServiceClientFactory` dell&#39;oggetto `updateResource` e trasmettere i seguenti parametri:

   * Un oggetto `java.lang.String` contenente l&#39;URI della risorsa.
   * L&#39;oggetto `Resource` contenente le informazioni aggiornate sulla risorsa.
   * Un valore `boolean` che indica se aggiornare la versione principale o secondaria. In questo esempio, viene passato un valore di `true` per indicare che la versione principale deve essere incrementata.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Avvio rapido (modalità SOAP): Aggiornamento di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiornare le risorse utilizzando l&#39;API del servizio Web {#update-resources-using-the-web-service-api}

Aggiornare una risorsa utilizzando l&#39;API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Recuperare la risorsa da aggiornare

   Specificate l’URI della risorsa da recuperare e leggete la risorsa. In questo esempio, l&#39;URI della risorsa è `"/testFolder/testResource"`. Per ulteriori informazioni, vedere [Risorse di lettura](aem-forms-repository.md#reading-resources).

1. Aggiornare la risorsa

   Aggiornare le informazioni dell&#39;oggetto `Resource`. In questo esempio, per aggiornare la descrizione, assegnare un nuovo valore al campo `Resource` dell&#39;oggetto `description`.

1. Richiamare il metodo `RepositoryServiceService` dell&#39;oggetto `updateResource` e trasmettere i seguenti parametri:

   * Un oggetto `System.String` contenente l&#39;URI della risorsa.
   * L&#39;oggetto `Resource` contenente le informazioni aggiornate sulla risorsa.
   * Un valore `boolean` che indica se aggiornare la versione principale o secondaria. In questo esempio, viene passato un valore di `true` per indicare che la versione principale deve essere incrementata.
   * Passa `null` per i due parametri rimanenti.

**Consulta anche**

[Aggiornamento delle risorse](aem-forms-repository.md#updating-resources)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ricerca di risorse {#searching-for-resources}

È possibile creare query utilizzate per cercare risorse nella directory archivio, inclusi cronologia, risorse correlate e proprietà.

È possibile recuperare risorse correlate per determinare le dipendenze tra un modulo e i relativi frammenti. Ad esempio, se si dispone di un modulo è possibile determinare i frammenti o le risorse esterne che utilizza. Se disponete di un’immagine, potete anche scoprire quali moduli utilizzano l’immagine. Potete anche cercare risorse correlate utilizzando il filtro in base alle proprietà. Ad esempio, è possibile cercare tutti i moduli che utilizzano un&#39;immagine con un nome specificato, oppure trovare le immagini utilizzate da un modulo con un nome specificato. È inoltre possibile eseguire ricerche utilizzando le proprietà delle risorse. Ad esempio, è possibile eseguire una query per individuare tutti i moduli o le risorse il cui nome inizia con una stringa specifica che può includere caratteri jolly &quot;%&quot; e &quot;_&quot;. Ricorda che le ricerche basate sulle proprietà non sono basate sulle relazioni; tali ricerche si basano sul presupposto che si disponga di conoscenze specifiche su una determinata risorsa.

**Istruzioni query**

Una *query* contiene una o più istruzioni collegate logicamente con le condizioni. Una *istruzione* è costituita da un operando a sinistra, un operatore e un operando a destra. Inoltre, potete specificare l&#39;ordinamento da utilizzare per i risultati della ricerca. L&#39; *ordinamento* contiene informazioni equivalenti a una clausola SQL `ORDER BY` ed è composto da elementi che contengono gli attributi su cui è stata basata la ricerca, nonché un valore che indica se è necessario utilizzare l&#39;ordine crescente o decrescente.

È possibile cercare le risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository. Al momento, non è possibile utilizzare l&#39;API del servizio Web per cercare le risorse.

**Comportamento dell&#39;ordinamento**

L&#39;ordinamento non viene rispettato quando si richiama il metodo `searchProperties` dell&#39;oggetto `ResourceRepositoryClient` e si specifica un ordinamento. Ad esempio, si supponga di creare una risorsa con tre proprietà personalizzate, dove i nomi degli attributi sono `name`, `secondName` e `asecondName`. Quindi create un elemento di ordinamento sul nome dell&#39;attributo e impostate il valore `ascending` su `true`.

Quindi si richiama il metodo `ResourceRepositoryClient` dell&#39;oggetto `searchProperties` e si passa all&#39;ordinamento. La ricerca restituisce la risorsa giusta, con le tre proprietà. Tuttavia, le proprietà non sono ordinate in base al nome dell&#39;attributo. Vengono restituiti nell&#39;ordine in cui sono stati aggiunti: `name`, `secondName` e `asecondName`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Create una stringa contenente il percorso di base da cui eseguire la ricerca. La sintassi include le barre, come in questo esempio: &quot;/*percorso*/*cartella*&quot;.

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

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Cercare risorse utilizzando l&#39;API Java {#search-for-resources-using-the-java-api}

Cercare una risorsa utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificate la cartella di destinazione per la ricerca

   Specificare l&#39;URI del percorso di base da cui eseguire la ricerca. In questo esempio, l&#39;URI della risorsa è `/testFolder`.

1. Specificare gli attributi utilizzati nella ricerca

   Specificate i valori per gli attributi su cui eseguire la ricerca. Gli attributi esistono all&#39;interno di un oggetto `com.adobe.repository.infomodel.bean.Resource`. In questo esempio, la ricerca verrà eseguita sull&#39;attributo name; pertanto, viene utilizzato un `java.lang.String` contenente il nome dell&#39;oggetto `Resource`, che in questo caso è `testResource`.

1. Creare la query utilizzata nella ricerca

   Per creare una query, creare un oggetto `com.adobe.repository.query.Query` richiamando il costruttore predefinito per la classe `Query` e aggiungendo istruzioni alla query.

   Per creare un&#39;istruzione, richiamare il costruttore per la classe `com.adobe.repository.query.Query.Statement` e trasmettere i seguenti parametri:

   * Un operando a sinistra contenente la costante attributo risorsa. In questo esempio, poiché il nome della risorsa è utilizzato come base per la ricerca, viene utilizzato il valore statico `Resource.ATTRIBUTE_NAME`.
   * Operatore che contiene la condizione utilizzata nella ricerca dell&#39;attributo. L&#39;operatore deve essere una delle costanti statiche nella classe `Query.Statement`. In questo esempio viene utilizzato il valore statico `Query.Statement.OPERATOR_BEGINS_WITH`.
   * Un operando a destra contenente il valore dell&#39;attributo su cui eseguire la ricerca. In questo esempio, viene utilizzato l&#39;attributo name, un `String` contenente il valore `"testResource"`.

   Specificare lo spazio dei nomi dell&#39;operando sinistro richiamando il metodo `Query.Statement` dell&#39;oggetto `setNamespace` e passando uno dei valori statici contenuti nella classe &lt;a2/>. `com.adobe.repository.infomodel.bean.ResourceProperty` In questo esempio viene utilizzato `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`.

   Aggiungete ogni istruzione alla query richiamando il metodo `Query` dell&#39;oggetto `addStatement` e passando l&#39;oggetto &lt;a2/>.`Query.Statement`

1. Creare l’ordinamento per i risultati della ricerca

   Per specificare l&#39;ordinamento utilizzato nei risultati della ricerca, create un oggetto `com.adobe.repository.query.sort.SortOrder` richiamando il costruttore predefinito per la classe `SortOrder` e aggiungendo elementi all&#39;ordinamento.

   Per creare un elemento per l&#39;ordinamento, richiamare uno dei costruttori per la classe `com.adobe.repository.query.sort.SortOrder.Element`. In questo esempio, poiché il nome della risorsa è utilizzato come base per la ricerca, il valore statico `Resource.ATTRIBUTE_NAME` viene utilizzato come primo parametro, mentre l&#39;ordine crescente (un valore `boolean` di `true`) viene specificato come secondo parametro.

   Aggiungete ciascun elemento all&#39;ordinamento richiamando il metodo `SortOrder` dell&#39;oggetto `addSortElement` e passando l&#39;oggetto &lt;a2/>.`SortOrder.Element`

1. Ricerca delle risorse

   Per cercare `resources` in base alle proprietà dell&#39;attributo, richiamare il metodo `ResourceRepositoryClient` dell&#39;oggetto `searchProperties` e trasmettere i seguenti parametri:

   * Un `String` contenente il percorso di base da cui eseguire la ricerca. In questo caso, viene utilizzato `"/testFolder"`.
   * Query utilizzata nella ricerca.
   * Profondità della ricerca. In questo caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` viene utilizzato per indicare che deve essere utilizzato il percorso di base e tutte le relative cartelle.
   * Un valore `int` che indica la prima riga da cui selezionare il set di risultati non di paging. In questo esempio, è specificato `0`.
   * Un valore `int` che indica il numero massimo di risultati da restituire. In questo esempio, è specificato `10`.
   * Ordine utilizzato nella ricerca.

   Il metodo restituisce un `java.util.List` di `Resource` oggetti nell&#39;ordine specificato.

1. Recuperare le risorse dal risultato della ricerca

   Per recuperare le risorse contenute nel risultato della ricerca, ripetere l&#39;iterazione attraverso `List` e inserire ciascun oggetto in un `Resource` per estrarne le informazioni. In questo esempio viene visualizzato il nome di ogni risorsa.

**Consulta anche**

[Ricerca di risorse](aem-forms-repository.md#searching-for-resources)

[Avvio rapido (modalità SOAP): Ricerca di risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

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
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Creare stringhe contenenti gli URI della risorsa da correlare. La sintassi include le barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;.

**Creare la relazione**

Richiamare il metodo del servizio Repository per creare e specificare il tipo di relazione.

**Consulta anche**

[Creazione di risorse sulle relazioni mediante l&#39;API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Creazione di risorse sulle relazioni mediante l&#39;API del servizio Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creare risorse sulle relazioni utilizzando l&#39;API Java {#create-relationship-resources-using-the-java-api}

Create le risorse delle relazioni utilizzando l&#39;API Java del servizio Repository ed eseguite le seguenti operazioni:

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare gli URI delle risorse da correlare

   Specificate gli URI delle risorse da correlare. In questo caso, poiché le risorse sono denominate `testResource1` e `testResource2` e si trovano nella cartella denominata `testFolder`, i relativi URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Gli URI sono memorizzati come oggetti `java.lang.String`. In questo esempio, le risorse vengono scritte per la prima volta nella directory archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Risorse di scrittura](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiamare il metodo `ResourceRepositoryClient` dell&#39;oggetto `createRelationship` e trasmettere i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Il tipo di relazione, che è una delle costanti statiche nella classe `com.adobe.repository.infomodel.bean.Relation`. In questo esempio, una relazione di dipendenza viene stabilita specificando il valore `Relation.TYPE_DEPENDANT_OF`.
   * Un valore `boolean` che indica se la risorsa di destinazione viene aggiornata automaticamente all&#39;identificatore basato su `com.adobe.repository.infomodel.Id` della nuova risorsa principale. In questo esempio, a causa della relazione di dipendenza, viene specificato il valore `true`.

   È inoltre possibile recuperare un elenco delle risorse correlate per una determinata risorsa richiamando il metodo `ResourceRepositoryClient` dell&#39;oggetto `getRelated` e passando i seguenti parametri:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio viene specificata la risorsa di origine ( `"/testFolder/testResource1"`).
   * Un valore `boolean` che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché è il caso.
   * Il tipo di relazione, che è una delle costanti statiche nella classe `Relation`. In questo esempio, una relazione di dipendenza viene specificata utilizzando lo stesso valore utilizzato in precedenza: `Relation.TYPE_DEPENDANT_OF`.

   Il metodo `getRelated` restituisce `java.util.List` di oggetti `Resource` attraverso i quali è possibile iterare per recuperare ciascuna delle risorse correlate, raggruppando gli oggetti contenuti in `List` in `Resource` così come si fa. In questo esempio, `testResource2` deve essere incluso nell&#39;elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Avvio rapido (modalità SOAP): Creazione di relazioni tra le risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di risorse sulle relazioni mediante l&#39;API del servizio Web {#create-relationship-resources-using-the-web-service-api}

Creare risorse sulle relazioni utilizzando l&#39;API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare gli URI delle risorse da correlare

   Specificate gli URI delle risorse da correlare. In questo caso, poiché le risorse sono denominate `testResource1` e `testResource2` e si trovano nella cartella denominata `testFolder`, i relativi URI sono `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Quando si utilizza un linguaggio conforme a Microsoft .NET Framework (ad esempio, C#), gli URI vengono memorizzati come oggetti `System.String`. In questo esempio, le risorse vengono scritte per la prima volta nella directory archivio e i relativi URI vengono recuperati. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Risorse di scrittura](aem-forms-repository.md#writing-resources).

1. Creare la relazione

   Richiamare il metodo `RepositoryServiceService` dell&#39;oggetto `createRelationship` e trasmettere i seguenti parametri:

   * URI della risorsa di origine.
   * URI della risorsa di destinazione.
   * Tipo di relazione. In questo esempio, una relazione di dipendenza viene stabilita specificando il valore `3`.
   * Un valore `boolean` che indica se è stato specificato il tipo di relazione. In questo esempio, il valore `true` è specificato.
   * Un valore `boolean` che indica se la risorsa di destinazione viene aggiornata automaticamente all&#39;identificatore basato su `Id` della nuova risorsa principale. In questo esempio, a causa della relazione di dipendenza, viene specificato il valore `true`.
   * Un valore `boolean` che indica se è stata specificata l&#39;intestazione di destinazione. In questo esempio, il valore `true` è specificato.
   * Passa `null` per l&#39;ultimo parametro.

   È inoltre possibile recuperare un elenco delle risorse correlate per una determinata risorsa richiamando il metodo `RepositoryServiceService` dell&#39;oggetto `getRelated` e passando i seguenti parametri:

   * URI della risorsa per la quale recuperare le risorse correlate. In questo esempio viene specificata la risorsa di origine ( `"/testFolder/testResource1"`).
   * Un valore `boolean` che indica se la risorsa specificata è la risorsa di origine nella relazione. In questo esempio, il valore `true` è specificato perché è il caso.
   * Un valore `boolean` che indica se la risorsa di origine è stata specificata. In questo esempio, viene fornito il valore `true`.
   * Un array di numeri interi contenente i tipi di relazione. In questo esempio, una relazione di dipendenza viene specificata utilizzando lo stesso valore nell&#39;array utilizzato in precedenza: `3`.
   * Passa `null` per i due parametri rimanenti.

   Il metodo `getRelated` restituisce un array di oggetti che possono essere inseriti in oggetti `Resource` attraverso i quali è possibile iterare per recuperare ciascuna delle risorse correlate. In questo esempio, `testResource2` deve essere incluso nell&#39;elenco delle risorse restituite.

**Consulta anche**

[Creazione di relazioni tra risorse](aem-forms-repository.md#creating-resource-relationships)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Blocco delle risorse {#locking-resources}

È possibile bloccare una risorsa o un set di risorse da utilizzare esclusivamente da un particolare utente o da un uso condiviso tra più utenti. Un blocco condiviso è un&#39;indicazione che qualcosa accadrà con la risorsa, ma non impedisce a nessun altro di intraprendere azioni con quella risorsa. Un blocco condiviso dovrebbe essere considerato un meccanismo di segnalazione. Un blocco esclusivo indica che l&#39;utente che ha bloccato la risorsa cambierà la risorsa e il blocco assicura che nessun altro possa farlo finché l&#39;utente non avrà più bisogno dell&#39;accesso alla risorsa e non avrà rilasciato il blocco. Se un amministratore del repository sblocca una risorsa, tutti i blocchi esclusivi e condivisi presenti sulla risorsa verranno automaticamente rimossi. Questo tipo di azione è destinato alle situazioni in cui un utente non è più disponibile e non ha sbloccato la risorsa.

Quando una risorsa è bloccata, quando si visualizza la scheda Risorse in Workbench viene visualizzata un&#39;icona a forma di lucchetto, come illustrato nella figura riportata di seguito.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Potete controllare l&#39;accesso alle risorse a livello di programmazione utilizzando l&#39;API Java del servizio Repository o l&#39;API del servizio Web.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Create una stringa contenente l’URI della risorsa da bloccare. La sintassi include le barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;.

**Blocca risorsa**

Richiamare il metodo del servizio Repository per bloccare la risorsa, specificando l’URI, il tipo di blocco e la profondità di blocco.

**Recuperare i blocchi per la risorsa**

Richiamare il metodo del servizio Repository per recuperare i blocchi per la risorsa, specificando l&#39;URI.

**Sblocca risorsa**

Richiamare il metodo del servizio Repository per sbloccare la risorsa, specificando l&#39;URI.

**Consulta anche**

[Blocco delle risorse tramite l&#39;API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Blocco delle risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Blocco delle risorse tramite l&#39;API Java {#lock-resources-using-the-java-api}

Bloccare le risorse utilizzando l&#39;API del servizio Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare l&#39;URI della risorsa da bloccare

   Specificate l’URI della risorsa da bloccare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResource"`. L&#39;URI è memorizzato come oggetto `java.lang.String`.

1. Blocca risorsa

   Richiamare il metodo `ResourceRepositoryClient` dell&#39;oggetto `lockResource` e trasmettere i seguenti parametri:

   * URI della risorsa.
   * L&#39;ambito di blocco. In questo esempio, poiché la risorsa verrà bloccata per l&#39;uso esclusivo, l&#39;ambito del blocco viene specificato come `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * La profondità di blocco. In questo esempio, poiché il blocco viene applicato solo alla risorsa in questione e nessuno dei relativi membri o elementi secondari, la profondità di blocco è specificata come `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La versione sovraccaricata del metodo `lockResource` che richiede quattro parametri genera un&#39;eccezione. Assicurarsi di utilizzare il metodo `lockResource` che richiede tre parametri, come illustrato in questa procedura dettagliata.

1. Recuperare i blocchi per la risorsa

   Richiamate il metodo `ResourceRepositoryClient` dell&#39;oggetto `getLocks` e passate l&#39;URI della risorsa come parametro. Il metodo restituisce un elenco di oggetti Lock attraverso il quale è possibile eseguire l&#39;iterazione. In questo esempio, il proprietario del blocco, la profondità e l&#39;ambito vengono stampati per ciascun oggetto richiamando rispettivamente i metodi `getOwnerUserId`, `getDepth` e `getType` di ciascun oggetto Lock.

1. Sblocca risorsa

   Richiamate il metodo `ResourceRepositoryClient` dell&#39;oggetto `unlockResource` e passate l&#39;URI della risorsa come parametro. Per ulteriori informazioni, vedere [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Avvio rapido (modalità SOAP): Blocco di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Blocco delle risorse tramite l&#39;API del servizio Web {#lock-resources-using-the-web-service-api}

Bloccare le risorse utilizzando l&#39;API del servizio Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da bloccare

   Specificate una stringa contenente l’URI della risorsa da bloccare. In questo caso, poiché la risorsa denominata `testResource` si trova nella cartella `testFolder`, il relativo URI è `"/testFolder/testResource"`. Se si utilizza una lingua conforme a Microsoft .NET Framework (ad esempio, C#), memorizzare l&#39;URI in un oggetto `System.String`.

1. Blocca risorsa

   Richiamare il metodo `RepositoryServiceService` dell&#39;oggetto `lockResource` e trasmettere i seguenti parametri:

   * URI della risorsa.
   * L&#39;ambito di blocco. In questo esempio, poiché la risorsa verrà bloccata per l&#39;uso esclusivo, l&#39;ambito del blocco viene specificato come `11`.
   * La profondità di blocco. In questo esempio, poiché il blocco viene applicato solo alla risorsa in questione e nessuno dei relativi membri o elementi secondari, la profondità di blocco è specificata come `2`.
   * Un valore `int` che indica il numero di secondi fino alla scadenza del blocco. In questo esempio viene utilizzato il valore di `1000`.
   * Passa `null` per l&#39;ultimo parametro.

1. Recuperare i blocchi per la risorsa

   Richiamate il metodo `RepositoryServiceService` dell&#39;oggetto `getLocks` e passate l&#39;URI della risorsa come primo parametro e `null` come secondo parametro. Il metodo restituisce un array `object` contenente oggetti `Lock` attraverso i quali è possibile iterare. In questo esempio, il proprietario del blocco, la profondità e l&#39;ambito vengono stampati per ciascun oggetto accedendo rispettivamente ai campi `Lock` dell&#39;oggetto `ownerUserId`, `depth` e `type`.

1. Sblocca risorsa

   Richiamate il metodo `RepositoryServiceService` dell&#39;oggetto `unlockResource` e passate l&#39;URI della risorsa come primo parametro e `null` come secondo parametro.

**Consulta anche**

[Blocco delle risorse](aem-forms-repository.md#locking-resources)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Eliminazione delle risorse {#deleting-resources}

È possibile eliminare programmaticamente le risorse da una determinata posizione nell&#39;archivio utilizzando l&#39;API Java (SOAP) del servizio Repository.

Quando si elimina una risorsa, l&#39;eliminazione è in genere permanente, anche se in alcuni casi i repository ECM possono memorizzare le versioni della risorsa in base ai meccanismi della cronologia. Pertanto, quando si elimina una risorsa, è importante essere certi di non averne più bisogno. I motivi comuni per eliminare una risorsa includono la necessità di aumentare lo spazio disponibile nel database. È possibile eliminare una versione di una risorsa, ma in questo caso è necessario specificare l&#39;identificatore della risorsa e non il relativo identificatore logico (LID) o percorso. Se eliminate una cartella, tutti gli elementi in essa contenuti, comprese le sottocartelle e le risorse, verranno eliminati automaticamente.

Le risorse correlate non vengono eliminate. Ad esempio, se si dispone di un modulo che utilizza il file logo.gif ed eliminate logo.gif, nella tabella delle relazioni in sospeso verrà memorizzata una relazione. In alternativa, per l&#39;eliminazione della versione, imposta lo stato dell&#39;oggetto dell&#39;ultima versione su obsoleto.

Un&#39;operazione di eliminazione non è sicura per le transazioni nei sistemi ECM. Ad esempio, se tentate di eliminare 100 risorse e l&#39;operazione ha esito negativo sulla 50° risorsa, le prime 49 istanze verranno eliminate ma il resto non verrà eliminato. In caso contrario, il comportamento predefinito è rollback (non impegno).

>[!NOTE]
>
>Se si utilizza il metodo `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` con l&#39;archivio ECM (EMC Documentum Content Server e IBM FileNet P8 Content Manager), la transazione non verrà ripristinata se l&#39;eliminazione non riesce per una delle risorse specificate, il che significa che i file che sono stati eliminati non possono essere eliminati.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Repository, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Create una stringa contenente l’URI della risorsa da eliminare. La sintassi include le barre, come in questo esempio: &quot;/*percorso*/*risorsa*&quot;. Se la risorsa da eliminare è una cartella, l’eliminazione sarà ricorsiva.

**Eliminare la risorsa**

Richiamare il metodo del servizio Repository per eliminare la risorsa, specificando l&#39;URI.

**Consulta anche**

[Eliminare le risorse tramite l&#39;API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Eliminare le risorse tramite l&#39;API del servizio Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio repository](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Eliminare le risorse utilizzando l&#39;API Java(SOAP) {#delete-resources-using-the-java-api-soap}

Eliminate una risorsa utilizzando l&#39;API Repository (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare il client del servizio

   Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare l&#39;URI della risorsa da eliminare

   Specificate l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata testResourceToBeDeleted si trova nella cartella denominata testFolder, il relativo URI è `/testFolder/testResourceToBeDeleted`. L&#39;URI è memorizzato come oggetto `java.lang.String`. In questo esempio, la risorsa viene scritta per la prima volta nella directory archivio e viene recuperato il relativo URI. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Risorse di scrittura](aem-forms-repository.md#writing-resources).

1. Eliminare la risorsa

   Richiamate il metodo `ResourceRepositoryClient` dell&#39;oggetto `deleteResource` e passate l&#39;URI della risorsa come parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Avvio rapido (modalità SOAP): Ricerca di risorse tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminare le risorse tramite l&#39;API del servizio Web {#delete-resources-using-the-web-service-api}

Eliminate una risorsa utilizzando l&#39;API Repository (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del repository utilizzando Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare il client del servizio

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `RepositoryServiceService` richiamando il relativo costruttore predefinito. Impostate la relativa proprietà `Credentials` utilizzando un oggetto `System.Net.NetworkCredential` contenente il nome utente e la password.

1. Specificare l&#39;URI della risorsa da eliminare

   Specificate l’URI della risorsa da recuperare. In questo caso, poiché la risorsa denominata `testResourceToBeDeleted` si trova nella cartella denominata `testFolder`, il relativo URI è `"/testFolder/testResourceToBeDeleted"`. In questo esempio, la risorsa viene scritta per la prima volta nella directory archivio e viene recuperato il relativo URI. Per ulteriori informazioni sulla scrittura di una risorsa, vedere [Risorse di scrittura](aem-forms-repository.md#writing-resources).

1. Eliminare la risorsa

   Richiamare il metodo `RepositoryServiceService` dell&#39;oggetto `deleteResources` e passare una matrice `System.String` contenente l&#39;URI della risorsa come primo parametro. Passa `null` per il secondo parametro.

**Consulta anche**

[Eliminazione delle risorse](aem-forms-repository.md#deleting-resources)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
