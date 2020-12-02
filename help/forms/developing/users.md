---
title: Gestione degli utenti
seo-title: Gestione degli utenti
description: 'null'
seo-description: 'null'
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '6191'
ht-degree: 0%

---


# Gestione degli utenti {#managing-users}

**Gestione utente**

Potete utilizzare l&#39;API di gestione utente per creare applicazioni client in grado di gestire ruoli, autorizzazioni e entità (che possono essere utenti o gruppi), nonché di autenticare gli utenti. L&#39;API di gestione utente è costituita dalle seguenti  API AEM Forms:

* API del servizio Directory Manager
* API del servizio Authentication Manager
* API del servizio Gestione autorizzazioni

Gestione utente consente di assegnare, rimuovere e determinare ruoli e autorizzazioni. Consente inoltre di assegnare, rimuovere ed eseguire query su domini, utenti e gruppi. Infine, potete utilizzare Gestione utente per autenticare gli utenti.

In [Aggiunta di utenti](users.md#adding-users) comprenderete come aggiungere utenti a livello di programmazione. Questa sezione utilizza l&#39;API del servizio Directory Manager.

In [Eliminazione di utenti](users.md#deleting-users) sarà possibile comprendere come eliminare gli utenti a livello di programmazione. Questa sezione utilizza l&#39;API del servizio Directory Manager.

In [Gestione di utenti e gruppi](users.md#managing-users-and-groups) comprenderete la differenza tra un utente locale e un utente di directory e vedrete alcuni esempi di utilizzo delle API Java e dei servizi Web per gestire gli utenti e i gruppi a livello di programmazione. Questa sezione utilizza l&#39;API del servizio Directory Manager.

In [Gestione di ruoli e autorizzazioni](users.md#managing-roles-and-permissions) verranno illustrati i ruoli e le autorizzazioni del sistema e le azioni che è possibile eseguire a livello di programmazione per incrementarli, nonché esempi di come utilizzare le API Java e dei servizi Web per gestire in modo programmatico ruoli e autorizzazioni. In questa sezione vengono utilizzate sia l&#39;API del servizio Directory Manager che l&#39;API del servizio Gestione autorizzazioni.

In [Autenticazione utenti](users.md#authenticating-users) sono disponibili alcuni esempi sull&#39;utilizzo delle API Java e dei servizi Web per l&#39;autenticazione programmatica degli utenti. In questa sezione viene utilizzata l’API del servizio Gestione autorizzazioni.

**Informazioni sul processo di autenticazione**

Gestione utente fornisce funzionalità di autenticazione integrate e consente di connettersi con il proprio provider di autenticazione. Quando User Management riceve una richiesta di autenticazione (ad esempio, un utente tenta di eseguire l&#39;accesso), trasmette le informazioni utente al provider di autenticazione per l&#39;autenticazione. Gestione utente riceve i risultati dal provider di autenticazione dopo l&#39;autenticazione dell&#39;utente.

Nel diagramma seguente è illustrata l&#39;interazione tra un utente finale che tenta di eseguire l&#39;accesso, Gestione utente e il provider di autenticazione.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

La tabella seguente descrive ogni fase del processo di autenticazione.

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un utente tenta di accedere a un servizio che richiama Gestione utente. L'utente specifica un nome utente e una password. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Gestione utente invia al provider di autenticazione il nome utente e la password, nonché le informazioni di configurazione.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Il provider di autenticazione si connette all'archivio utenti e autentica l'utente.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il provider di autenticazione restituisce i risultati a Gestione utente.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Gestione utente consente all'utente di effettuare l'accesso o nega l'accesso al prodotto.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se il fuso orario del server è diverso dal fuso orario del client, quando si utilizza il WSDL per il servizio AEM Forms Generate PDF  su uno stack SOAP nativo utilizzando un client .NET su un cluster di server applicazioni WebSphere, potrebbe verificarsi il seguente errore di autenticazione di gestione utente:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Informazioni sulla gestione delle directory**

User Management viene fornito con un provider di servizi di directory (DirectoryManagerService) che supporta le connessioni alle directory LDAP. Se l’organizzazione utilizza un archivio non LDAP per memorizzare i record utente, potete creare un provider di servizi di directory personalizzato che collabori con il repository.

I fornitori di servizi di directory recuperano i record da un archivio utenti su richiesta di Gestione utente. Gestione utenti memorizza regolarmente nella cache i record di utenti e gruppi presenti nel database per migliorare le prestazioni.

Il provider del servizio di directory può essere utilizzato per sincronizzare il database Gestione utente con lo store utente. Questo passaggio assicura che tutte le informazioni sulla directory utente e tutti i record utente e gruppo siano aggiornati.

Inoltre, DirectoryManagerService consente di creare e gestire i domini. I domini definiscono diverse basi utente. Il limite di un dominio viene generalmente definito in base alla struttura dell’organizzazione o alla configurazione dell’archivio utenti. I domini di gestione utenti forniscono le impostazioni di configurazione utilizzate dai provider di autenticazione e dai fornitori di servizi di directory.

Nel file XML di configurazione esportato da User Management, il nodo principale con il valore dell&#39;attributo `Domains` contiene un elemento XML per ciascun dominio definito per User Management. Ciascuno di questi elementi contiene altri elementi che definiscono gli aspetti del dominio associato a fornitori di servizi specifici.

**Informazioni sui valori objectSID**

Quando si utilizza Active Directory, è importante comprendere che un valore `objectSID` non è un attributo univoco tra più domini. Questo valore memorizza l&#39;identificatore di protezione di un oggetto. In un ambiente con più domini (ad esempio, una struttura ad albero di domini) il valore `objectSID` può essere diverso.

Un valore `objectSID` cambierebbe se un oggetto venisse spostato da un dominio Active Directory a un altro. Alcuni oggetti hanno lo stesso valore `objectSID` ovunque nel dominio. Ad esempio, gruppi come BUILTIN\Administrators, BUILTIN\Power Users e così via avranno lo stesso valore `objectSID` indipendentemente dai domini. Questi valori `objectSID` sono noti.

## Aggiunta di utenti {#adding-users}

È possibile utilizzare l&#39;API del servizio Directory Manager (Java e il servizio Web) per aggiungere gli utenti a  AEM Forms a livello di programmazione. Dopo aver aggiunto un utente, potete utilizzarlo quando eseguite un&#39;operazione di servizio che richiede un utente. Ad esempio, potete assegnare un’attività al nuovo utente.

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un utente, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client DirectoryManagerService.
1. Definite le informazioni utente.
1. Aggiungete l&#39;utente a  AEM Forms.
1. Verificare che l&#39;utente sia aggiunto.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione del servizio Directory Manager in modo programmatico, creare un client API Directory Manager Service.

**Definizione delle informazioni utente**

Quando aggiungete un nuovo utente utilizzando l&#39;API di Directory Manager Service, definite le informazioni per tale utente. In genere, quando si aggiunge un nuovo utente, vengono definiti i seguenti valori:

* **Nome** dominio: Il dominio a cui appartiene l&#39;utente (ad esempio,  `DefaultDom`).
* **Valore** identificatore utente: Il valore identificativo dell’utente (ad esempio,  `wblue`).
* **Tipo** principale: Il tipo di utente (ad esempio, potete specificare  `USER)`.
* **Nome**: Un nome specifico per l’utente (ad esempio,  `Wendy`).
* **Cognome**: Nome della famiglia dell’utente (ad esempio,  `Blue)`.
* **Impostazioni internazionali**: Informazioni sulle impostazioni internazionali per l’utente.

**Aggiungere l&#39;utente a  AEM Forms**

Dopo aver definito le informazioni utente, potete aggiungere l’utente a  AEM Forms. Per aggiungere un utente, richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `createLocalUser`.

**Verificare che l&#39;utente sia stato aggiunto**

Potete verificare che l&#39;utente sia stato aggiunto per assicurarsi che non si siano verificati problemi. Individuate il nuovo utente utilizzando il valore dell&#39;identificatore utente.

**Consulta anche**

[Aggiunta di utenti tramite l&#39;API Java](users.md#add-users-using-the-java-api)

[Aggiunta di utenti tramite l&#39;API del servizio Web](users.md#add-users-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Eliminazione degli utenti](users.md#deleting-users)

### Aggiunta di utenti tramite Java API {#add-users-using-the-java-api}

Aggiungete utenti utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerServices.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Definite le informazioni utente.

   * Creare un oggetto `UserImpl` utilizzando il relativo costruttore.
   * Impostate il nome demain richiamando il metodo `UserImpl` dell&#39;oggetto `setDomainName`. Passa un valore di stringa che specifica il nome del dominio.
   * Impostare il tipo di entità richiamando il metodo `UserImpl` dell&#39;oggetto `setPrincipalType`. Passa un valore di stringa che specifica il tipo di utente. Ad esempio, è possibile specificare `USER`.
   * Impostate il valore dell&#39;identificatore utente richiamando il metodo `setUserid` dell&#39;oggetto `UserImpl`. Passa un valore di stringa che specifica il valore dell&#39;identificatore utente. Ad esempio, è possibile specificare `wblue`.
   * Impostare il nome canonico richiamando il metodo `UserImpl` dell&#39;oggetto `setCanonicalName`. Passa un valore di stringa che specifica il nome canonico dell&#39;utente. Ad esempio, è possibile specificare `wblue`.
   * Impostare il nome specificato richiamando il metodo `UserImpl` dell&#39;oggetto `setGivenName`. Passa un valore di stringa che specifica il nome specificato dall&#39;utente. Ad esempio, è possibile specificare `Wendy`.
   * Impostare il nome della famiglia richiamando il metodo `UserImpl` dell&#39;oggetto `setFamilyName`. Passa un valore di stringa che specifica il nome della famiglia dell&#39;utente. Ad esempio, è possibile specificare `Blue`.

   >[!NOTE]
   >
   >Richiamare un metodo che appartiene all&#39;oggetto `UserImpl` per impostare altri valori. Ad esempio, è possibile impostare il valore delle impostazioni internazionali richiamando il metodo `UserImpl` dell&#39;oggetto `setLocale`.

1. Aggiungete l&#39;utente a  AEM Forms.

   Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `createLocalUser` e trasmettere i seguenti valori:

   * L&#39;oggetto `UserImpl` che rappresenta il nuovo utente
   * Una stringa che rappresenta la password dell&#39;utente

   Il metodo `createLocalUser` restituisce un valore di stringa che specifica il valore dell&#39;identificatore utente locale.

1. Verificate che l&#39;utente sia stato aggiunto.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostate il valore dell&#39;identificatore utente richiamando il metodo `setUserId` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore di stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `findPrincipals` e passare l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un&#39;istanza `java.util.List`, in cui ogni elemento è un oggetto `User`. Iterate l&#39;istanza `java.util.List` per individuare l&#39;utente.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Aggiunta di utenti tramite l&#39;API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiunta di utenti tramite l&#39;API del servizio Web {#add-users-using-the-web-service-api}

Aggiungete utenti utilizzando l&#39;API del servizio Directory Manager (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicuratevi di utilizzare la seguente definizione WSDL per il riferimento al servizio: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client DirectoryManagerService.

   * Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DirectoryManagerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio. Assicurarsi di specificare `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Definite le informazioni utente.

   * Creare un oggetto `UserImpl` utilizzando il relativo costruttore.
   * Impostate il nome demain assegnando un valore stringa al campo `UserImpl` dell&#39;oggetto `domainName`.
   * Impostare il tipo di entità assegnando un valore di stringa al campo `UserImpl` dell&#39;oggetto `principalType`. Ad esempio, è possibile specificare `USER`.
   * Impostate il valore dell&#39;identificatore utente assegnando un valore stringa al campo `UserImpl` dell&#39;oggetto `userid`.
   * Impostare il valore del nome canonico assegnando un valore stringa al campo `UserImpl` dell&#39;oggetto `canonicalName`.
   * Impostare il valore del nome specificato assegnando un valore stringa al campo `UserImpl` dell&#39;oggetto `givenName`.
   * Impostare il valore del nome della famiglia assegnando un valore stringa al campo `UserImpl` dell&#39;oggetto `familyName`.

1. Aggiungete l&#39;utente a  AEM Forms.

   Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `createLocalUser` e trasmettere i seguenti valori:

   * L&#39;oggetto `UserImpl` che rappresenta il nuovo utente
   * Una stringa che rappresenta la password dell&#39;utente

   Il metodo `createLocalUser` restituisce un valore di stringa che specifica il valore dell&#39;identificatore utente locale.

1. Verificate che l&#39;utente sia stato aggiunto.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostate il valore dell&#39;identificatore utente dell&#39;utente assegnando un valore stringa che rappresenta il valore dell&#39;identificatore utente al campo `PrincipalSearchFilter` dell&#39;oggetto `userId`.
   * Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `findPrincipals` e passare l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un oggetto raccolta `MyArrayOfUser`, in cui ogni elemento è un oggetto `User`. Iterate la raccolta `MyArrayOfUser` per individuare l&#39;utente.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminazione di utenti {#deleting-users}

È possibile utilizzare l&#39;API del servizio Directory Manager (Java e il servizio Web) per eliminare programmaticamente gli utenti da  AEM Forms. Dopo l&#39;eliminazione di un utente, l&#39;utente non può più essere utilizzato per eseguire un&#39;operazione di servizio che richiede un utente. Ad esempio, non potete assegnare un’attività a un utente eliminato.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per eliminare un utente, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client DirectoryManagerService.
1. Specificate l’utente da eliminare.
1. Eliminate l’utente da  AEM Forms.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione API di Directory Manager Service a livello di programmazione, creare un client del servizio Directory Manager.

**Specificare l&#39;utente da eliminare**

Potete specificare un utente da eliminare utilizzando il valore dell&#39;identificatore dell&#39;utente.

**Eliminare l’utente da  AEM Forms**

Per eliminare un utente, richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `deleteLocalUser`.

**Consulta anche**

[Eliminare gli utenti tramite l&#39;API Java](users.md#delete-users-using-the-java-api)

[Eliminare gli utenti tramite l&#39;API del servizio Web](users.md#delete-users-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di utenti](users.md#adding-users)

### Eliminare gli utenti mediante l&#39;API Java {#delete-users-using-the-java-api}

Eliminare gli utenti utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificate l’utente da eliminare.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostate il valore dell&#39;identificatore utente richiamando il metodo `setUserId` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore di stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `findPrincipals` e passare l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un&#39;istanza `java.util.List`, in cui ogni elemento è un oggetto `User`. Iterate l&#39;istanza `java.util.List` per individuare l&#39;utente da eliminare.

1. Eliminate l’utente da  AEM Forms.

   Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `deleteLocalUser` e passare il valore del campo `User` dell&#39;oggetto `oid`. Richiamare il metodo `User` dell&#39;oggetto `getOid`. Utilizzare l&#39;oggetto `User` recuperato dall&#39;istanza `java.util.List`.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Avvio rapido (modalità EJB): Eliminazione di utenti tramite l&#39;API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Avvio rapido (modalità SOAP): Eliminazione di utenti tramite l&#39;API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminare gli utenti mediante l&#39;API del servizio Web {#delete-users-using-the-web-service-api}

Eliminare gli utenti utilizzando l&#39;API del servizio Directory Manager (servizio Web):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   * Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DirectoryManagerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio. Assicurarsi di specificare `blob=mtom.`
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Specificate l’utente da eliminare.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostate il valore dell&#39;identificatore utente assegnando un valore stringa al campo `PrincipalSearchFilter` dell&#39;oggetto `userId`.
   * Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `findPrincipals` e passare l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un oggetto raccolta `MyArrayOfUser`, in cui ogni elemento è un oggetto `User`. Iterate la raccolta `MyArrayOfUser` per individuare l&#39;utente. L&#39;oggetto `User` recuperato dall&#39;oggetto dell&#39;insieme `MyArrayOfUser` viene utilizzato per eliminare l&#39;utente.

1. Eliminate l’utente da  AEM Forms.

   Eliminare l&#39;utente passando il valore del campo `User` dell&#39;oggetto `oid` al metodo `DirectoryManagerServiceClient` dell&#39;oggetto `deleteLocalUser`.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di gruppi {#creating-groups}

È possibile utilizzare l&#39;API del servizio Directory Manager (Java e il servizio Web) per creare  gruppi AEM Forms a livello di programmazione. Dopo aver creato un gruppo, potete utilizzarlo per eseguire un&#39;operazione di servizio che richiede un gruppo. Ad esempio, potete assegnare un utente al nuovo gruppo. (Vedere [Gestione di utenti e gruppi](users.md#managing-users-and-groups).)

### Riepilogo dei passaggi {#summary_of_steps-2}

Per creare un gruppo, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client DirectoryManagerService.
1. Determinare che il gruppo non esiste.
1. Create il gruppo.
1. Eseguire un&#39;azione con il gruppo.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione del servizio Directory Manager in modo programmatico, creare un client API Directory Manager Service.

**Determinare se il gruppo esiste**

Quando create un gruppo, accertatevi che il gruppo non esista nello stesso dominio. In altre parole, due gruppi non possono avere lo stesso nome all&#39;interno dello stesso dominio. Per eseguire questa operazione, eseguire una ricerca e filtrare i risultati della ricerca in base a due valori. Impostate il tipo di entità su `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` per garantire che vengano restituiti solo i gruppi. Inoltre, specificate il nome di dominio.

**Creare il gruppo**

Dopo aver stabilito che il gruppo non esiste nel dominio, create il gruppo e specificate i seguenti attributi:

* **CommonName**: Nome del gruppo.
* **Dominio**: Il dominio in cui viene aggiunto il gruppo.
* **Descrizione**: Descrizione del gruppo.

**Eseguire un&#39;azione con il gruppo**

Dopo aver creato un gruppo, potete eseguire un’azione utilizzando il gruppo. Ad esempio, potete aggiungere un utente al gruppo. Per aggiungere un utente a un gruppo, recuperate il valore dell’identificatore univoco sia dell’utente che del gruppo. Passa questi valori al metodo `addPrincipalToLocalGroup`.

**Consulta anche**

[Creazione di gruppi tramite l&#39;API Java](users.md#create-groups-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di utenti](users.md#adding-users)

[Eliminazione degli utenti](users.md#deleting-users)

### Creare gruppi utilizzando l&#39;API Java {#create-groups-using-the-java-api}

Create un gruppo utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Determinate se il gruppo esiste.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostare il tipo di entità richiamando l&#39;oggetto `PrincipalSearchFilter` dell&#39;oggetto `setPrincipalType`. Passare il valore `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Impostare il dominio richiamando l&#39;oggetto `setSpecificDomainName` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore di stringa che specifica il nome del dominio.
   * Per trovare un gruppo, richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `findPrincipals` (un&#39;entità può essere un gruppo). Passa l&#39;oggetto `PrincipalSearchFilter` che specifica il tipo di entità e il nome di dominio. Questo metodo restituisce un&#39;istanza `java.util.List` in cui ogni elemento è un&#39;istanza `Group`. Ogni istanza di gruppo è conforme al filtro specificato utilizzando l&#39;oggetto `PrincipalSearchFilter`.
   * Iterate l&#39;istanza `java.util.List`. Per ciascun elemento, recuperate il nome del gruppo. Verificate che il nome del gruppo non corrisponda al nuovo nome del gruppo.

1. Create il gruppo.

   * Se il gruppo non esiste, richiamare il metodo `setCommonName` dell&#39;oggetto `Group` e passare un valore di stringa che specifica il nome del gruppo.
   * Richiamare il metodo `Group` dell&#39;oggetto `setDescription` e passare un valore di stringa che specifica la descrizione del gruppo.
   * Richiamare il metodo `Group` dell&#39;oggetto `setDomainName` e passare un valore di stringa che specifica il nome del dominio.
   * Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `createLocalGroup` e passare l&#39;istanza `Group`.

   Il metodo `createLocalUser` restituisce un valore di stringa che specifica il valore dell&#39;identificatore utente locale.

1. Eseguire un&#39;azione con il gruppo.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostate il valore dell&#39;identificatore utente richiamando il metodo `setUserId` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore di stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiamare il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `findPrincipals` e passare l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un&#39;istanza `java.util.List`, in cui ogni elemento è un oggetto `User`. Iterate l&#39;istanza `java.util.List` per individuare l&#39;utente.
   * Aggiungete un utente al gruppo richiamando il metodo `DirectoryManagerServiceClient` dell&#39;oggetto `addPrincipalToLocalGroup`. Passare il valore restituito dal metodo `User` dell&#39;oggetto `getOid`. Passare il valore restituito dal metodo `Group` degli oggetti `getOid` (utilizzare l&#39;istanza `Group` che rappresenta il nuovo gruppo).

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestione di utenti e gruppi {#managing-users-and-groups}

Questo argomento descrive come utilizzare (Java) per assegnare, rimuovere ed eseguire query a livello di programmazione a domini, utenti e gruppi.

>[!NOTE]
>
>Quando configurate un dominio, dovete impostare l&#39;identificatore univoco per gruppi e utenti. L’attributo selezionato non deve essere univoco nell’ambiente LDAP, ma deve anche essere immutabile e non deve essere modificato all’interno della directory. Questo attributo deve anche essere di tipo dati stringa semplice (l&#39;unica eccezione attualmente consentita per Active Directory 2000/2003 è `"objectsid"`, che è un valore binario). L&#39;attributo Novell eDirectory `"GUID"`, ad esempio, non è un tipo di dati stringa semplice e pertanto non funziona.

* Per Active Directory, utilizzare `"objectsid"`.
* Per SunOne, utilizzare `"nsuniqueid"`.

>[!NOTE]
>
>La creazione di più utenti e gruppi locali mentre è in corso la sincronizzazione di una directory LDAP non è supportata. Il tentativo di eseguire questo processo potrebbe causare errori.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per gestire utenti e gruppi, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client DirectoryManagerService.
1. Richiama le operazioni utente o gruppo appropriate.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione del servizio Directory Manager in modo programmatico, è necessario creare un client del servizio Directory Manager. Con l&#39;API Java questo si ottiene creando un oggetto `DirectoryManagerServiceClient`. Con l&#39;API del servizio Web ciò viene ottenuto creando un oggetto `DirectoryManagerServiceService`.

**Richiama le operazioni utente o gruppo appropriate**

Dopo aver creato il client del servizio, potete richiamare le operazioni di gestione utente o gruppo. Il client del servizio consente di assegnare, rimuovere ed eseguire query su domini, utenti e gruppi. È possibile aggiungere un&#39;entità directory o locale a un gruppo locale, ma non è possibile aggiungere un&#39;entità locale a un gruppo di directory.

**Consulta anche**

[Gestione di utenti e gruppi tramite l&#39;API Java](users.md#managing-users-and-groups-using-the-java-api)

[Gestione di utenti e gruppi tramite l&#39;API del servizio Web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestione di utenti e gruppi mediante l&#39;API Java {#managing-users-and-groups-using-the-java-api}

Per gestire gli utenti, i gruppi e i domini a livello di programmazione utilizzando (Java), effettua le seguenti operazioni:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-usermanager-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione. Per informazioni, vedere [Impostazione delle proprietà di connessione ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Richiama le operazioni utente o gruppo appropriate.

   Per trovare un utente o un gruppo, invocate uno dei metodi dell&#39;oggetto `DirectoryManagerServiceClient` per trovare le entità (poiché un&#39;entità può essere un utente o un gruppo). Nell&#39;esempio seguente, il metodo `findPrincipals` viene chiamato utilizzando un filtro di ricerca (un oggetto `PrincipalSearchFilter`).

   Poiché in questo caso il valore restituito è un `java.util.List` contenente oggetti `Principal`, è possibile iterare il risultato e proiettare gli oggetti `Principal` su oggetti `User` o `Group`.

   Utilizzando l&#39;oggetto `User` o `Group` risultante (entrambi ereditati dall&#39;interfaccia `Principal`), recuperare le informazioni necessarie nei flussi di lavoro. Ad esempio, il nome di dominio e i valori del nome canonico, in combinazione, identificano in modo univoco un&#39;entità. Tali metodi vengono recuperati richiamando, rispettivamente, i metodi `Principal` dell&#39;oggetto `getDomainName` e `getCanonicalName`.

   Per eliminare un utente locale, richiamare il metodo `deleteLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient` e passare l&#39;identificatore dell&#39;utente.

   Per eliminare un gruppo locale, richiamate il metodo `deleteLocalGroup` dell&#39;oggetto `DirectoryManagerServiceClient` e passate l&#39;identificatore del gruppo.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione di utenti e gruppi tramite l&#39;API del servizio Web {#managing-users-and-groups-using-the-web-service-api}

Per gestire in modo programmatico utenti, gruppi e domini tramite l&#39;API del servizio Directory Manager (servizio Web), eseguire le operazioni seguenti:

1. Includere i file di progetto.

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL di Directory Manager. (Vedere [Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceService` utilizzando il costruttore della classe proxy.

1. Richiama le operazioni utente o gruppo appropriate.

   Per trovare un utente o un gruppo, invocate uno dei metodi dell&#39;oggetto `DirectoryManagerServiceService` per trovare le entità (poiché un&#39;entità può essere un utente o un gruppo). Nell&#39;esempio seguente, il metodo `findPrincipalsWithFilter` viene chiamato utilizzando un filtro di ricerca (un oggetto `PrincipalSearchFilter`). Quando si utilizza un oggetto `PrincipalSearchFilter`, le entità locali vengono restituite solo se la proprietà `isLocal` è impostata su `true`. Questo comportamento è diverso da quello che si verificherebbe con l&#39;API Java.

   >[!NOTE]
   >
   >Se il numero massimo di risultati non viene specificato nel filtro di ricerca (tramite il campo `PrincipalSearchFilter.resultsMax`), verrà restituito un massimo di 1000 risultati. Questo comportamento è diverso da quello che si verifica utilizzando l&#39;API Java, in cui 10 risultati è il massimo predefinito. Inoltre, i metodi di ricerca come `findGroupMembers` non produrranno alcun risultato a meno che il numero massimo di risultati non sia specificato nel filtro di ricerca (ad esempio, attraverso il campo `GroupMembershipSearchFilter.resultsMax`). Ciò vale per tutti i filtri di ricerca che ereditano dalla classe `GenericSearchFilter`. Per ulteriori informazioni, vedere [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Poiché in questo caso il valore restituito è un `object[]` contenente oggetti `Principal`, ripetere il risultato e proiettare gli oggetti `Principal` in oggetti `User` o `Group`.

   Utilizzando l&#39;oggetto `User` o `Group` risultante (entrambi ereditati dall&#39;interfaccia `Principal`), recuperare le informazioni necessarie nei flussi di lavoro. Ad esempio, il nome di dominio e i valori del nome canonico, in combinazione, identificano in modo univoco un&#39;entità. Per recuperarli, è necessario richiamare i campi `Principal` `domainName` e `canonicalName` dell&#39;oggetto, rispettivamente.

   Per eliminare un utente locale, richiamare il metodo `deleteLocalUser` dell&#39;oggetto `DirectoryManagerServiceService` e passare l&#39;identificatore dell&#39;utente.

   Per eliminare un gruppo locale, richiamate il metodo `deleteLocalGroup` dell&#39;oggetto `DirectoryManagerServiceService` e passate l&#39;identificatore del gruppo.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Gestione di ruoli e autorizzazioni {#managing-roles-and-permissions}

In questo argomento viene descritto come utilizzare l’API di Gestione autorizzazioni (Java) per assegnare, rimuovere e determinare in modo programmatico ruoli e autorizzazioni.

In  AEM Forms, un *ruolo* è un gruppo di autorizzazioni per accedere a una o più risorse a livello di sistema. Queste autorizzazioni vengono create tramite Gestione utente e vengono applicate dai componenti del servizio. Ad esempio, un amministratore potrebbe assegnare il ruolo di autore del set di criteri a un gruppo di utenti. Questo Rights Management consente agli utenti di quel gruppo con tale ruolo di creare set di criteri tramite la console di amministrazione.

Esistono due tipi di ruoli: *ruoli predefiniti* e *ruoli personalizzati*. I ruoli predefiniti (*ruoli di sistema)* sono già residenti in  AEM Forms. Si presume che i ruoli predefiniti non possano essere eliminati o modificati dall&#39;amministratore e che pertanto siano immutabili. I ruoli personalizzati creati dall&#39;amministratore, che possono successivamente modificarli o eliminarli, sono pertanto modificabili.

I ruoli semplificano la gestione delle autorizzazioni. Quando un ruolo viene assegnato a un&#39;entità, un set di autorizzazioni viene automaticamente assegnato a tale entità e tutte le decisioni relative all&#39;accesso specifiche per l&#39;entità si basano su tale insieme complessivo di autorizzazioni assegnate.

### Riepilogo dei passaggi {#summary_of_steps-4}

Per gestire ruoli e autorizzazioni, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un client AuthorizationManagerService.
1. Richiama le operazioni di ruolo o autorizzazione appropriate.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un client AuthorizationManagerService**

Prima di poter eseguire un&#39;operazione di User Management AuthorizationManagerService a livello di programmazione, è necessario creare un client AuthorizationManagerService. Con l&#39;API Java questo si ottiene creando un oggetto `AuthorizationManagerServiceClient`.

**Richiama le operazioni di ruolo o autorizzazione appropriate**

Dopo aver creato il client del servizio, potete richiamare le operazioni di ruolo o autorizzazione. Il client del servizio consente di assegnare, rimuovere e determinare ruoli e autorizzazioni.

**Consulta anche**

[Gestione di ruoli e autorizzazioni tramite l&#39;API Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Gestione di ruoli e autorizzazioni tramite l&#39;API del servizio Web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestione di ruoli e autorizzazioni mediante l&#39;API Java {#managing-roles-and-permissions-using-the-java-api}

Per gestire ruoli e autorizzazioni utilizzando l’API di Gestione autorizzazioni (Java), eseguite le seguenti operazioni:

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client AuthorizationManagerService.

   Creare un oggetto `AuthorizationManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama le operazioni di ruolo o autorizzazione appropriate.

   Per assegnare un ruolo a un&#39;entità, richiamare il metodo `AuthorizationManagerServiceClient` dell&#39;oggetto &lt;a1/> e passare i seguenti valori:`assignRole`

   * Un oggetto `java.lang.String` che contiene l&#39;identificatore del ruolo
   * Un array di oggetti `java.lang.String` contenenti gli identificatori principali.

   Per rimuovere un ruolo da un&#39;entità, richiamare il metodo `AuthorizationManagerServiceClient` dell&#39;oggetto &lt;a1/> e passare i seguenti valori:`unassignRole`

   * Un oggetto `java.lang.String` che contiene l&#39;identificatore del ruolo.
   * Un array di oggetti `java.lang.String` contenenti gli identificatori principali.


**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Gestione di ruoli e autorizzazioni tramite l&#39;API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione di ruoli e autorizzazioni tramite l&#39;API del servizio Web {#managing-roles-and-permissions-using-the-web-service-api}

Gestire ruoli e autorizzazioni utilizzando l’API del servizio Gestione autorizzazioni (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client AuthorizationManagerService.

   * Creare un oggetto `AuthorizationManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AuthorizationManagerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AuthorizationManagerServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Richiama le operazioni di ruolo o autorizzazione appropriate.

   Per assegnare un ruolo a un&#39;entità, richiamare il metodo `AuthorizationManagerServiceClient` dell&#39;oggetto &lt;a1/> e passare i seguenti valori:`assignRole`

   * Un oggetto `string` che contiene l&#39;identificatore del ruolo
   * Un oggetto `MyArrayOf_xsd_string` che contiene gli identificatori principali.

   Per rimuovere un ruolo da un&#39;entità, richiamare il metodo `AuthorizationManagerServiceService` dell&#39;oggetto &lt;a1/> e passare i seguenti valori:`unassignRole`

   * Un oggetto `string` che contiene l&#39;identificatore del ruolo.
   * Un array di oggetti `string` contenenti gli identificatori principali.


**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticazione utenti {#authenticating-users}

Questo argomento descrive come utilizzare l&#39;API Authentication Manager Service (Java) per abilitare le applicazioni client ad autenticare gli utenti a livello di programmazione.

L&#39;autenticazione dell&#39;utente può essere necessaria per interagire con un database aziendale o altri repository aziendali in cui sono memorizzati i dati protetti.

Considerate, ad esempio, uno scenario in cui un utente immette un nome utente e una password in una pagina Web e invia i valori a un server applicazione J2EE in cui è installato Forms. Un&#39;applicazione personalizzata Forms può autenticare l&#39;utente con il servizio Authentication Manager.

Se l&#39;autenticazione ha esito positivo, l&#39;applicazione accede a un database enterprise protetto. In caso contrario, all&#39;utente viene inviato un messaggio in cui si attesta che l&#39;utente non è un utente autorizzato.

Il diagramma seguente mostra il flusso logico dell&#39;applicazione.

![au_au_umauth_process](assets/au_au_umauth_process.png)

La tabella seguente descrive i passaggi descritti in questo diagramma

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>3</p></td>
   <td><p>L'utente accede a un sito Web e specifica un nome utente e una password. Queste informazioni vengono inviate a un server applicazione J2EE che ospita  AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le credenziali utente sono autenticate con il servizio Authentication Manager. Se le credenziali utente sono valide, il flusso di lavoro procede al passaggio 3. In caso contrario, all'utente viene inviato un messaggio in cui si attesta che l'utente non è un utente autorizzato.</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>Le informazioni utente e una struttura del modulo vengono recuperate da un database enterprise protetto. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le informazioni utente vengono unite a una struttura del modulo e il modulo viene rappresentato all'utente. </p></td>
  </tr>
 </tbody>
</table>

### Riepilogo dei passaggi {#summary_of_steps-5}

Per autenticare un utente a livello di programmazione, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Create un client AuthenticationManagerService.
1. Richiama l&#39;operazione di autenticazione.
1. Se necessario, recuperate il contesto in modo che l&#39;applicazione client possa inoltrarlo a un altro servizio AEM Forms  per l&#39;autenticazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un client AuthenticationManagerService**

Prima di poter autenticare un utente a livello di programmazione, è necessario creare un client AuthenticationManagerService. Quando utilizzate l&#39;API Java, create un oggetto `AuthenticationManagerServiceClient`.

**Richiamo dell&#39;operazione di autenticazione**

Dopo aver creato il client del servizio, potete richiamare l&#39;operazione di autenticazione. Questa operazione richiede informazioni sull’utente, ad esempio il nome e la password dell’utente. Se l&#39;utente non esegue l&#39;autenticazione, viene generata un&#39;eccezione.

**Recuperare il contesto di autenticazione**

Dopo aver autenticato l&#39;utente, puoi creare un contesto basato sull&#39;utente autenticato. Potete quindi utilizzare il contenuto per richiamare un altro  servizi AEM Forms. Ad esempio, è possibile utilizzare il contesto per creare un documento `EncryptionServiceClient` e cifrare un documento PDF con una password. Verificare che l&#39;utente autenticato abbia il ruolo `Services User` richiesto per richiamare un servizio AEM Forms .

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Cifratura di documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autenticazione di un utente tramite l&#39;API Java {#authenticate-a-user-using-the-java-api}

Eseguire l&#39;autenticazione di un utente mediante l&#39;API Authentication Manager Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client AuthenticationManagerServices.

   Creare un oggetto `AuthenticationManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama l&#39;operazione di autenticazione.

   Richiamare il metodo `AuthenticationManagerServiceClient` dell&#39;oggetto `authenticate` e trasmettere i seguenti valori:

   * Un oggetto `java.lang.String` che contiene il nome dell&#39;utente.
   * Un array di byte (un oggetto `byte[]`) contenente la password dell&#39;utente. È possibile ottenere l&#39;oggetto `byte[]` richiamando il metodo `java.lang.String` dell&#39;oggetto `getBytes`.

   Il metodo authenticate restituisce un oggetto `AuthResult` che contiene informazioni sull&#39;utente autenticato.

1. Recuperare il contesto di autenticazione.

   Richiamare il metodo `ServiceClientFactory` dell&#39;oggetto `getContext`, che restituirà un oggetto `Context`.

   Quindi, richiamare il metodo `Context` dell&#39;oggetto `initPrincipal` e passare il `AuthResult`.

### Autenticazione di un utente tramite l&#39;API del servizio Web {#authenticate-a-user-using-the-web-service-api}

Autenticazione di un utente tramite l&#39;API Authentication Manager Service (servizio Web):

1. Includere i file di progetto.

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL di Authentication Manager. (Vedere [Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere &quot;Riferimento all&#39;assembly del client .NET&quot; in [Chiamata  AEM Forms tramite codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Create un client AuthenticationManagerService.

   Creare un oggetto `AuthenticationManagerServiceService` utilizzando il costruttore della classe proxy.

1. Richiama l&#39;operazione di autenticazione.

   Richiamare il metodo `AuthenticationManagerServiceClient` dell&#39;oggetto `authenticate` e trasmettere i seguenti valori:

   * Un oggetto `string` che contiene il nome dell&#39;utente
   * Un array di byte (un oggetto `byte[]`) contenente la password dell&#39;utente. È possibile ottenere l&#39;oggetto `byte[]` convertendo un oggetto `string` contenente la password in un array `byte[]` utilizzando la logica illustrata nell&#39;esempio seguente.
   * Il valore restituito sarà un oggetto `AuthResult`, che può essere utilizzato per recuperare informazioni sull&#39;utente. Nell&#39;esempio seguente, le informazioni dell&#39;utente vengono recuperate prima ottenendo il campo `AuthResult` dell&#39;oggetto `authenticatedUser` e successivamente ottenendo i campi `User` e `canonicalName` dell&#39;oggetto risultante.`domainName`

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronizzazione programmatica degli utenti {#programmatically-synchronizing-users}

Potete sincronizzare gli utenti a livello di programmazione utilizzando l&#39;API di gestione utente. Quando sincronizzate gli utenti, state aggiornando  AEM Forms con i dati utente presenti nell&#39;archivio degli utenti. Ad esempio, si supponga di aggiungere nuovi utenti al repository degli utenti. Dopo aver eseguito un&#39;operazione di sincronizzazione, i nuovi utenti diventano utenti AEM moduli. Inoltre, gli utenti che non si trovano più nel repository degli utenti vengono rimossi da  AEM Forms.

Il diagramma seguente mostra  sincronizzazione di AEM Forms con un repository utente.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

La tabella seguente descrive i passaggi descritti in questo diagramma

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un'applicazione client richiede che  AEM Forms esegua un'operazione di sincronizzazione.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p> AEM Forms esegue un'operazione di sincronizzazione.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Le informazioni utente vengono aggiornate.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Un utente può visualizzare le informazioni aggiornate sull’utente. </p></td>
  </tr>
 </tbody>
</table>

### Riepilogo dei passaggi {#summary_of_steps-6}

Per sincronizzare gli utenti a livello di programmazione, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client UserManagerUtilServiceClient.
1. Specificate il dominio enterprise.
1. Richiama l&#39;operazione di autenticazione.
1. Determinare se l’operazione di sincronizzazione è completa

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un client UserManagerUtilServiceClient**

Prima di poter sincronizzare gli utenti a livello di programmazione, è necessario creare un oggetto `UserManagerUtilServiceClient`.

**Specificare il dominio enterprise**

Prima di eseguire un&#39;operazione di sincronizzazione utilizzando l&#39;API di gestione utente, specificate il dominio Enterprise a cui appartengono gli utenti. Puoi specificare uno o più domini enterprise. Prima di poter eseguire un&#39;operazione di sincronizzazione a livello di programmazione, è necessario impostare un dominio Enterprise utilizzando la console di amministrazione. (Vedere [guida di amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Richiamo dell’operazione di sincronizzazione**

Dopo aver specificato uno o più domini Enterprise, potete eseguire l&#39;operazione di sincronizzazione. Il tempo necessario per eseguire questa operazione dipende dal numero di record utente presenti nell&#39;archivio utenti.

**Determinare se l’operazione di sincronizzazione è completa**

Dopo aver eseguito un&#39;operazione di sincronizzazione a livello di programmazione, è possibile determinare se l&#39;operazione è stata completata.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Cifratura di documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronizzazione programmatica degli utenti tramite Java API {#programmatically-synchronizing-users-using-the-java-api}

Sincronizzate gli utenti mediante l’API di gestione utente (Java):

1. Includere i file di progetto.

   Includete file JAR client, come adobe-usermanager-client.jar e adobe-usermanager-util-client.jar, nel percorso di classe del progetto Java.

1. Creare un client UserManagerUtilServiceClient.

   Creare un oggetto `UserManagerUtilServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificate il dominio enterprise.

   * Richiamare il metodo `UserManagerUtilServiceClient` dell&#39;oggetto `scheduleSynchronization` per avviare l&#39;operazione di sincronizzazione dell&#39;utente.
   * Create un&#39;istanza `java.util.Set` utilizzando un costruttore `HashSet`. Assicurarsi di specificare `String` come tipo di dati. Questa istanza `Java.util.Set` memorizza i nomi di dominio a cui si applica l&#39;operazione di sincronizzazione.
   * Per ciascun nome di dominio da aggiungere, richiamare il metodo add dell&#39;oggetto `java.util.Set` e passare il nome di dominio.

1. Richiama l’operazione di sincronizzazione.

   Richiamare il metodo `ServiceClientFactory` dell&#39;oggetto `getContext`, che restituirà un oggetto `Context`.

   Quindi, richiamare il metodo `Context` dell&#39;oggetto `initPrincipal` e passare il `AuthResult`.

**Consulta anche**

[Sincronizzazione programmatica degli utenti](users.md#programmatically-synchronizing-users)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
