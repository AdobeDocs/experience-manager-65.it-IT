---
title: Gestione degli utenti
seo-title: Managing Users
description: Utilizza l'API User Management per creare applicazioni client in grado di gestire ruoli, autorizzazioni e entità principali (che possono essere utenti o gruppi), nonché di autenticare gli utenti.
seo-description: Use the User Management API to create client applications that can manage roles, permissions, and principals (which can be users or groups), as well as authenticate users.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '6228'
ht-degree: 0%

---

# Gestione degli utenti {#managing-users}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sulla gestione degli utenti**

Puoi utilizzare l&#39;API User Management per creare applicazioni client in grado di gestire ruoli, autorizzazioni e entità principali (che possono essere utenti o gruppi), nonché autenticare gli utenti. L’API di gestione utenti è costituita dalle seguenti API AEM Forms:

* API del servizio Directory Manager
* API del servizio Authentication Manager
* API del servizio Gestione autorizzazioni

Gestione utente consente di assegnare, rimuovere e determinare ruoli e autorizzazioni. Consente inoltre di assegnare, rimuovere ed eseguire query su domini, utenti e gruppi. Infine, puoi utilizzare Gestione utente per autenticare gli utenti.

In [Aggiunta di utenti](users.md#adding-users) comprenderai come aggiungere gli utenti a livello di programmazione. In questa sezione viene utilizzata l&#39;API del servizio Directory Manager.

In [Eliminazione degli utenti](users.md#deleting-users) comprenderai come eliminare programmaticamente gli utenti. In questa sezione viene utilizzata l&#39;API del servizio Directory Manager.

In [Gestione di utenti e gruppi](users.md#managing-users-and-groups) comprenderai la differenza tra un utente locale e un utente di directory e vedrai esempi di utilizzo delle API di Java e servizi web per gestire in modo programmatico utenti e gruppi. In questa sezione viene utilizzata l&#39;API del servizio Directory Manager.

In [Gestione di ruoli e autorizzazioni](users.md#managing-roles-and-permissions) scopri i ruoli e le autorizzazioni del sistema e cosa puoi fare a livello di programmazione per incrementarli, nonché come utilizzare le API dei servizi web e Java per gestire in modo programmatico ruoli e autorizzazioni. In questa sezione vengono utilizzate sia l&#39;API del servizio Directory Manager che l&#39;API del servizio Gestione autorizzazioni.

In [Autenticazione degli utenti](users.md#authenticating-users) vedrai esempi di utilizzo delle API Java e dei servizi web per l’autenticazione programmatica degli utenti. In questa sezione viene utilizzata l’API del servizio Gestione autorizzazioni.

**Informazioni sul processo di autenticazione**

User Management fornisce funzionalità di autenticazione integrate e consente anche di connettersi con il provider di autenticazione. Quando User Management riceve una richiesta di autenticazione (ad esempio, un utente tenta di accedere), trasmette le informazioni utente al provider di autenticazione per l&#39;autenticazione. User Management riceve i risultati dal provider di autenticazione dopo l&#39;autenticazione dell&#39;utente.

Il diagramma seguente mostra l’interazione tra un utente finale che tenta di accedere, Gestione utente e il provider di autenticazione.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

La tabella seguente descrive ogni fase del processo di autenticazione.

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
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
   <td><p>User Management invia al provider di autenticazione il nome utente e la password, nonché le informazioni di configurazione.</p></td>
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
   <td><p>Gestione utente consente all’utente di accedere al prodotto o nega l’accesso al prodotto.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se il fuso orario del server è diverso dal fuso orario client, durante il consumo del servizio WSDL per AEM Forms Generate PDF su uno stack SOAP nativo utilizzando un client .NET su un cluster WebSphere Application Server, potrebbe verificarsi il seguente errore di autenticazione di User Management:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Informazioni sulla gestione delle directory**

User Management viene fornito con un provider di servizi directory (DirectoryManagerService) che supporta le connessioni alle directory LDAP. Se la tua organizzazione utilizza un archivio non LDAP per memorizzare i record utente, puoi creare un provider di servizi di directory che funziona con il tuo archivio.

I provider di servizi di directory recuperano i record da un archivio utenti su richiesta di Gestione utente. Gestione utente memorizza regolarmente nella cache i record di utenti e gruppi nel database per migliorare le prestazioni.

Il provider di servizi di directory può essere utilizzato per sincronizzare il database User Management con l&#39;archivio utenti. Questo passaggio assicura che tutte le informazioni sulla directory utente e tutti i record utente e gruppo siano aggiornati.

Inoltre, DirectoryManagerService consente di creare e gestire i domini. I domini definiscono diverse basi utente. Il limite di un dominio viene generalmente definito in base alla struttura dell’organizzazione o alla configurazione dell’archivio utenti. I domini di gestione utente forniscono impostazioni di configurazione utilizzate dai provider di autenticazione e dai fornitori di servizi di directory.

Nell&#39;XML di configurazione esportato da User Management, il nodo principale che ha il valore dell&#39;attributo di `Domains` contiene un elemento XML per ogni dominio definito per Gestione utente. Ciascuno di questi elementi contiene altri elementi che definiscono gli aspetti del dominio associato a specifici fornitori di servizi.

**Informazioni sui valori objectSID**

Quando si utilizza Active Directory, è importante comprendere che un `objectSID` Il valore non è un attributo univoco per più domini. Questo valore memorizza l&#39;identificatore di sicurezza di un oggetto. In un ambiente con più domini (ad esempio, una struttura ad albero di domini) il `objectSID` può essere diverso.

Un `objectSID` Se un oggetto viene spostato da un dominio Active Directory a un altro, il valore viene modificato. Alcuni oggetti hanno lo stesso `objectSID` in qualsiasi punto del dominio. Ad esempio, gruppi come BUILTIN\Administrators, BUILTIN\Power Users e così via avranno lo stesso `objectSID` indipendentemente dai domini. Tali `objectSID` i valori sono noti.

## Aggiunta di utenti {#adding-users}

È possibile utilizzare l&#39;API del servizio Directory Manager (Java e servizio Web) per aggiungere gli utenti a AEM Forms in modo programmatico. Dopo aver aggiunto un utente, puoi utilizzarlo quando esegui un&#39;operazione di servizio che richiede un utente. Ad esempio, è possibile assegnare un’attività al nuovo utente.

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un utente, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Definisci le informazioni utente.
1. Aggiungi l’utente ad AEM Forms.
1. Verifica che l’utente sia aggiunto.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione di servizio di Gestione directory a livello di programmazione, creare un client API di Gestione directory.

**Definire le informazioni utente**

Quando si aggiunge un nuovo utente utilizzando l&#39;API del servizio Directory Manager, definire le informazioni per tale utente. In genere, quando si aggiunge un nuovo utente, vengono definiti i seguenti valori:

* **Nome di dominio**: Il dominio a cui appartiene l’utente (ad esempio, `DefaultDom`).
* **Valore identificativo utente**: Il valore dell&#39;identificatore dell&#39;utente (ad esempio, `wblue`).
* **Tipo principale**: Il tipo di utente (ad esempio, puoi specificare `USER)`.
* **Nome assegnato**: Un nome specifico per l’utente (ad esempio, `Wendy`).
* **Cognome**: Il cognome dell’utente (ad esempio, `Blue)`.
* **Impostazioni internazionali**: Informazioni sulle impostazioni internazionali per l’utente.

**Aggiungi l’utente ad AEM Forms**

Dopo aver definito le informazioni utente, puoi aggiungere l’utente ad AEM Forms. Per aggiungere un utente, richiama il `DirectoryManagerServiceClient` dell’oggetto `createLocalUser` metodo .

**Verifica che l’utente sia stato aggiunto**

Puoi verificare che l’utente sia stato aggiunto per assicurarti che non si siano verificati problemi. Individua il nuovo utente utilizzando il valore dell&#39;identificatore utente.

**Consulta anche**

[Aggiungere utenti tramite l’API Java](users.md#add-users-using-the-java-api)

[Aggiungere utenti tramite l’API del servizio Web](users.md#add-users-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Eliminazione degli utenti](users.md#deleting-users)

### Aggiungere utenti tramite l’API Java {#add-users-using-the-java-api}

Aggiungi gli utenti utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerServices.

   Crea un `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Definisci le informazioni utente.

   * Crea un `UserImpl` utilizzando il relativo costruttore.
   * Imposta il nome del demain richiamando il `UserImpl` dell’oggetto `setDomainName` metodo . Passa un valore stringa che specifica il nome di dominio.
   * Imposta il tipo di entità richiamando il `UserImpl` dell’oggetto `setPrincipalType` metodo . Passa un valore stringa che specifica il tipo di utente. Ad esempio, puoi specificare `USER`.
   * Imposta il valore dell&#39;identificatore utente richiamando il `UserImpl` dell’oggetto `setUserid` metodo . Passa un valore stringa che specifica il valore dell&#39;identificatore utente. Ad esempio, puoi specificare `wblue`.
   * Imposta il nome canonico richiamando il `UserImpl` dell’oggetto `setCanonicalName` metodo . Passa un valore stringa che specifica il nome canonico dell&#39;utente. Ad esempio, puoi specificare `wblue`.
   * Imposta il nome specificato richiamando il `UserImpl` dell’oggetto `setGivenName` metodo . Passa un valore di stringa che specifica il nome specificato dall&#39;utente. Ad esempio, puoi specificare `Wendy`.
   * Imposta il nome della famiglia richiamando il `UserImpl` dell’oggetto `setFamilyName` metodo . Passa un valore stringa che specifica il nome della famiglia dell&#39;utente. Ad esempio, puoi specificare `Blue`.

   >[!NOTE]
   >
   >Richiama di un metodo che appartiene al `UserImpl` per impostare altri valori. Ad esempio, puoi impostare il valore delle impostazioni internazionali richiamando il `UserImpl` dell’oggetto `setLocale` metodo .

1. Aggiungi l’utente ad AEM Forms.

   Richiama il `DirectoryManagerServiceClient` dell’oggetto `createLocalUser` e passare i seguenti valori:

   * La `UserImpl` oggetto che rappresenta il nuovo utente
   * Valore stringa che rappresenta la password dell&#39;utente

   La `createLocalUser` restituisce un valore di stringa che specifica il valore dell&#39;identificatore utente locale.

1. Verifica che l’utente sia stato aggiunto.

   * Crea un `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Imposta il valore dell&#39;identificatore utente richiamando il `PrincipalSearchFilter` dell’oggetto `setUserId` metodo . Passa un valore stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiama il `DirectoryManagerServiceClient` dell’oggetto `findPrincipals` e passare il `PrincipalSearchFilter` oggetto. Questo metodo restituisce un `java.util.List` istanza, dove ogni elemento è un `User` oggetto. Itera attraverso il `java.util.List` istanza per individuare l&#39;utente.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Aggiunta di utenti tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere utenti tramite l’API del servizio Web {#add-users-using-the-web-service-api}

Aggiungere utenti utilizzando l&#39;API del servizio Directory Manager (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL per il riferimento al servizio: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client DirectoryManagerService.

   * Crea un `DirectoryManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `DirectoryManagerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Assicurati di specificare `?blob=mtom`.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `DirectoryManagerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Definisci le informazioni utente.

   * Crea un `UserImpl` utilizzando il relativo costruttore.
   * Imposta il nome della richiesta assegnando un valore stringa al `UserImpl` dell’oggetto `domainName` campo .
   * Imposta il tipo principale assegnando un valore stringa al `UserImpl` dell’oggetto `principalType` campo . Ad esempio, puoi specificare `USER`.
   * Imposta il valore dell&#39;identificatore utente assegnando un valore stringa al `UserImpl` dell’oggetto `userid` campo .
   * Imposta il valore del nome canonico assegnando un valore stringa al `UserImpl` dell’oggetto `canonicalName` campo .
   * Imposta il valore del nome specificato assegnando un valore stringa al `UserImpl` dell’oggetto `givenName` campo .
   * Imposta il valore del nome della famiglia assegnando un valore stringa al `UserImpl` dell’oggetto `familyName` campo .

1. Aggiungi l’utente ad AEM Forms.

   Richiama il `DirectoryManagerServiceClient` dell’oggetto `createLocalUser` e passare i seguenti valori:

   * La `UserImpl` oggetto che rappresenta il nuovo utente
   * Valore stringa che rappresenta la password dell&#39;utente

   La `createLocalUser` restituisce un valore di stringa che specifica il valore dell&#39;identificatore utente locale.

1. Verifica che l’utente sia stato aggiunto.

   * Crea un `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Imposta il valore dell&#39;identificatore utente assegnando un valore stringa che rappresenta il valore dell&#39;identificatore utente al `PrincipalSearchFilter` dell’oggetto `userId` campo .
   * Richiama il `DirectoryManagerServiceClient` dell’oggetto `findPrincipals` e passare il `PrincipalSearchFilter` oggetto. Questo metodo restituisce un `MyArrayOfUser` oggetto raccolta, in cui ogni elemento è un `User` oggetto. Itera attraverso il `MyArrayOfUser` raccolta per individuare l&#39;utente.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminazione degli utenti {#deleting-users}

È possibile utilizzare l&#39;API del servizio Directory Manager (Java e servizio Web) per eliminare programmaticamente gli utenti da AEM Forms. Dopo aver eliminato un utente, non può più essere utilizzato per eseguire un&#39;operazione di servizio che richiede un utente. Ad esempio, non è possibile assegnare un’attività a un utente eliminato.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per eliminare un utente, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Specifica l’utente da eliminare.
1. Elimina l’utente da AEM Forms.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione API di Directory Manager Service a livello di programmazione, creare un client di servizio di Directory Manager.

**Specificare l&#39;utente da eliminare**

Puoi specificare un utente da eliminare utilizzando il valore dell’identificatore dell’utente.

**Eliminare l’utente da AEM Forms**

Per eliminare un utente, richiama il `DirectoryManagerServiceClient` dell’oggetto `deleteLocalUser` metodo .

**Consulta anche**

[Eliminare gli utenti tramite l’API Java](users.md#delete-users-using-the-java-api)

[Eliminare gli utenti tramite l’API del servizio Web](users.md#delete-users-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di utenti](users.md#adding-users)

### Eliminare gli utenti tramite l’API Java {#delete-users-using-the-java-api}

Eliminare gli utenti utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   Crea un `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica l’utente da eliminare.

   * Crea un `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Imposta il valore dell&#39;identificatore utente richiamando il `PrincipalSearchFilter` dell’oggetto `setUserId` metodo . Passa un valore stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiama il `DirectoryManagerServiceClient` dell’oggetto `findPrincipals` e passare il `PrincipalSearchFilter` oggetto. Questo metodo restituisce un `java.util.List` istanza, dove ogni elemento è un `User` oggetto. Itera attraverso il `java.util.List` istanza per individuare l&#39;utente da eliminare.

1. Elimina l’utente da AEM Forms.

   Richiama il `DirectoryManagerServiceClient` dell’oggetto `deleteLocalUser` e passare il valore del `User` dell’oggetto `oid` campo . Richiama il `User` dell’oggetto `getOid` metodo . Utilizza la `User` oggetto recuperato dal `java.util.List` istanza.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Avvio rapido (modalità EJB): Eliminazione di utenti tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Avvio rapido (modalità SOAP): Eliminazione di utenti tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminare gli utenti tramite l’API del servizio Web {#delete-users-using-the-web-service-api}

Eliminare gli utenti utilizzando l&#39;API del servizio Directory Manager (servizio Web):

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   * Crea un `DirectoryManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `DirectoryManagerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Assicurati di specificare `blob=mtom.`
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `DirectoryManagerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Specifica l’utente da eliminare.

   * Crea un `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Imposta il valore dell&#39;identificatore utente assegnando un valore stringa al `PrincipalSearchFilter` dell’oggetto `userId` campo .
   * Richiama il `DirectoryManagerServiceClient` dell’oggetto `findPrincipals` e passare il `PrincipalSearchFilter` oggetto. Questo metodo restituisce un `MyArrayOfUser` oggetto raccolta, in cui ogni elemento è un `User` oggetto. Itera attraverso il `MyArrayOfUser` raccolta per individuare l&#39;utente. La `User` oggetto recuperato dal `MyArrayOfUser` l&#39;oggetto collection viene utilizzato per eliminare l&#39;utente.

1. Elimina l’utente da AEM Forms.

   Elimina l&#39;utente passando il `User` dell’oggetto `oid` valore del campo nel `DirectoryManagerServiceClient` dell’oggetto `deleteLocalUser` metodo .

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di gruppi {#creating-groups}

È possibile utilizzare l&#39;API del servizio Directory Manager (Java e servizio Web) per creare in modo programmatico gruppi AEM Forms. Dopo aver creato un gruppo, è possibile utilizzare tale gruppo per eseguire un&#39;operazione di servizio che richiede un gruppo. Ad esempio, puoi assegnare un utente al nuovo gruppo. (Vedi [Gestione di utenti e gruppi](users.md#managing-users-and-groups).)

### Riepilogo dei passaggi {#summary_of_steps-2}

Per creare un gruppo, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Determinare che il gruppo non esiste.
1. Crea il gruppo.
1. Esegui un&#39;azione con il gruppo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione di servizio di Gestione directory a livello di programmazione, creare un client API di Gestione directory.

**Determinare se il gruppo esiste**

Quando crei un gruppo, assicurati che il gruppo non esista nello stesso dominio. Due gruppi non possono quindi avere lo stesso nome all&#39;interno dello stesso dominio. Per eseguire questa operazione, eseguire una ricerca e filtrare i risultati della ricerca in base a due valori. Imposta il tipo di entità su `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` per garantire che vengano restituiti solo i gruppi. Inoltre, accertati di specificare il nome di dominio.

**Crea il gruppo**

Dopo aver determinato che il gruppo non esiste nel dominio, crea il gruppo e specifica i seguenti attributi:

* **NomeComune**: Nome del gruppo.
* **Dominio**: Dominio in cui viene aggiunto il gruppo.
* **Descrizione**: Descrizione del gruppo.

**Esegui un&#39;azione con il gruppo**

Dopo aver creato un gruppo, è possibile eseguire un&#39;azione utilizzando il gruppo . Ad esempio, puoi aggiungere un utente al gruppo. Per aggiungere un utente a un gruppo, recupera il valore dell&#39;identificatore univoco sia dell&#39;utente che del gruppo. Passa questi valori al `addPrincipalToLocalGroup` metodo .

**Consulta anche**

[Creare gruppi utilizzando l’API Java](users.md#create-groups-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di utenti](users.md#adding-users)

[Eliminazione degli utenti](users.md#deleting-users)

### Creare gruppi utilizzando l’API Java {#create-groups-using-the-java-api}

Creare un gruppo utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   Crea un `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Determina se il gruppo esiste.

   * Crea un `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Imposta il tipo di entità richiamando il `PrincipalSearchFilter` dell’oggetto `setPrincipalType` oggetto. Passa il valore `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Imposta il dominio richiamando il `PrincipalSearchFilter` dell’oggetto `setSpecificDomainName` oggetto. Passa un valore stringa che specifica il nome di dominio.
   * Per trovare un gruppo, invoca il `DirectoryManagerServiceClient` dell’oggetto `findPrincipals` (un&#39;entità principale può essere un gruppo). Passa la `PrincipalSearchFilter` oggetto che specifica il tipo principale e il nome di dominio. Questo metodo restituisce un `java.util.List` istanza in cui ogni elemento è un `Group` istanza. Ogni istanza di gruppo è conforme al filtro specificato utilizzando il `PrincipalSearchFilter` oggetto.
   * Itera attraverso il `java.util.List` istanza. Per ogni elemento, recupera il nome del gruppo. Assicurati che il nome del gruppo non sia uguale al nuovo nome del gruppo.

1. Crea il gruppo.

   * Se il gruppo non esiste, richiama il `Group` dell’oggetto `setCommonName` e passare un valore stringa che specifica il nome del gruppo.
   * Richiama il `Group` dell’oggetto `setDescription` e passare un valore stringa che specifica la descrizione del gruppo.
   * Richiama il `Group` dell’oggetto `setDomainName` e passare un valore stringa che specifica il nome di dominio.
   * Richiama il `DirectoryManagerServiceClient` dell’oggetto `createLocalGroup` e passare il `Group` istanza.

   La `createLocalUser` restituisce un valore di stringa che specifica il valore dell&#39;identificatore utente locale.

1. Esegui un&#39;azione con il gruppo.

   * Crea un `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Imposta il valore dell&#39;identificatore utente richiamando il `PrincipalSearchFilter` dell’oggetto `setUserId` metodo . Passa un valore stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiama il `DirectoryManagerServiceClient` dell’oggetto `findPrincipals` e passare il `PrincipalSearchFilter` oggetto. Questo metodo restituisce un `java.util.List` istanza, dove ogni elemento è un `User` oggetto. Itera attraverso il `java.util.List` istanza per individuare l&#39;utente.
   * Aggiungi un utente al gruppo richiamando il `DirectoryManagerServiceClient` dell’oggetto `addPrincipalToLocalGroup` metodo . Passa il valore restituito di `User` dell’oggetto `getOid` metodo . Passa il valore restituito di `Group` degli oggetti `getOid` (utilizzare `Group` che rappresenta il nuovo gruppo).

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestione di utenti e gruppi {#managing-users-and-groups}

Questo argomento descrive come utilizzare (Java) per assegnare, rimuovere ed eseguire query a livello di programmazione su domini, utenti e gruppi.

>[!NOTE]
>
>Durante la configurazione di un dominio, devi impostare l’identificatore univoco per gruppi e utenti. L&#39;attributo scelto non deve essere solo univoco all&#39;interno dell&#39;ambiente LDAP, ma deve anche essere immutabile e non potrà essere modificato all&#39;interno della directory. Questo attributo deve anche essere di tipo dati stringa semplice (l&#39;unica eccezione attualmente consentita per Active Directory 2000/2003 è `"objectsid"`, che è un valore binario). Attributo Novell eDirectory `"GUID"`, ad esempio, non è un tipo di dati stringa semplice e pertanto non funziona.

* Per Active Directory, utilizzare `"objectsid"`.
* Per SunOne, utilizzare `"nsuniqueid"`.

>[!NOTE]
>
>La creazione di più utenti e gruppi locali mentre è in corso la sincronizzazione di una directory LDAP non è supportata. Il tentativo di questo processo può causare errori.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per gestire utenti e gruppi, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Richiama le operazioni utente o di gruppo appropriate.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client DirectoryManagerService**

Prima di eseguire un&#39;operazione di servizio di Gestione directory a livello di programmazione, è necessario creare un client di servizio di Gestione directory. Con l’API Java questa operazione viene eseguita creando un `DirectoryManagerServiceClient` oggetto. Con l’API del servizio Web questo viene realizzato creando un `DirectoryManagerServiceService` oggetto.

**Richiamare le operazioni utente o di gruppo appropriate**

Dopo aver creato il client di servizio, puoi richiamare le operazioni di gestione dell&#39;utente o del gruppo. Il client di servizi ti consente di assegnare, rimuovere ed eseguire query su domini, utenti e gruppi. Si noti che è possibile aggiungere un&#39;entità directory o un&#39;entità locale a un gruppo locale, ma non è possibile aggiungere un&#39;entità locale a un gruppo di directory.

**Consulta anche**

[Gestione di utenti e gruppi tramite l’API Java](users.md#managing-users-and-groups-using-the-java-api)

[Gestione di utenti e gruppi tramite l’API del servizio Web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestione di utenti e gruppi tramite l’API Java {#managing-users-and-groups-using-the-java-api}

Per gestire in modo programmatico utenti, gruppi e domini utilizzando (Java), esegui le seguenti attività:

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un client DirectoryManagerService.

   Crea un `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione. Per informazioni, consulta [Impostazione delle proprietà di connessione ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Richiama le operazioni utente o di gruppo appropriate.

   Per trovare un utente o un gruppo, richiamare una delle `DirectoryManagerServiceClient` metodi dell&#39;oggetto per la ricerca di entità principali (poiché un&#39;entità può essere un utente o un gruppo). Nell’esempio seguente, la `findPrincipals` viene chiamato utilizzando un filtro di ricerca (a `PrincipalSearchFilter` oggetto).

   Poiché in questo caso il valore restituito è un `java.util.List` contenente `Principal` oggetti, eseguire iterazioni nel risultato e creare il cast `Principal` oggetti `User` o `Group` oggetti.

   Utilizzo del risultato `User` o `Group` (che ereditano entrambi dal `Principal` , recupera le informazioni necessarie nei flussi di lavoro. Ad esempio, i valori del nome di dominio e del nome canonico, in combinazione, identificano in modo univoco un&#39;entità principale. Questi vengono recuperati richiamando il `Principal` dell’oggetto `getDomainName` e `getCanonicalName` metodi, rispettivamente.

   Per eliminare un utente locale, richiama il `DirectoryManagerServiceClient` dell’oggetto `deleteLocalUser` e passa l&#39;identificatore dell&#39;utente.

   Per eliminare un gruppo locale, richiamare `DirectoryManagerServiceClient` dell’oggetto `deleteLocalGroup` e passare l&#39;identificatore del gruppo.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione di utenti e gruppi tramite l’API del servizio Web {#managing-users-and-groups-using-the-web-service-api}

Per gestire in modo programmatico utenti, gruppi e domini utilizzando l&#39;API del servizio Directory Manager (servizio Web), eseguire le operazioni seguenti:

1. Includi file di progetto.

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL di Directory Manager. (Vedi [Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedi [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creare un client DirectoryManagerService.

   Crea un `DirectoryManagerServiceService` utilizzando il costruttore della classe proxy.

1. Richiama le operazioni utente o di gruppo appropriate.

   Per trovare un utente o un gruppo, richiamare una delle `DirectoryManagerServiceService` metodi dell&#39;oggetto per la ricerca di entità principali (poiché un&#39;entità può essere un utente o un gruppo). Nell’esempio seguente, la `findPrincipalsWithFilter` viene chiamato utilizzando un filtro di ricerca (a `PrincipalSearchFilter` oggetto). Quando si utilizza un `PrincipalSearchFilter` oggetto , le entità locali vengono restituite solo se la `isLocal` è impostata su `true`. Questo comportamento è diverso da quello che si verificherebbe con l’API Java.

   >[!NOTE]
   >
   >Se il numero massimo di risultati non è specificato nel filtro di ricerca (tramite `PrincipalSearchFilter.resultsMax` (campo), verrà restituito un massimo di 1000 risultati. Si tratta di un comportamento diverso rispetto a quello che si verifica utilizzando l’API Java, in cui 10 risultati sono il massimo predefinito. Inoltre, i metodi di ricerca come `findGroupMembers` non produrrà alcun risultato a meno che il numero massimo di risultati non sia specificato nel filtro di ricerca (ad esempio, attraverso `GroupMembershipSearchFilter.resultsMax` (campo). Questo vale per tutti i filtri di ricerca che ereditano dal `GenericSearchFilter` classe. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Poiché in questo caso il valore restituito è un valore `object[]` contenente `Principal` oggetti, eseguire iterazioni nel risultato e creare il cast `Principal` oggetti `User` o `Group` oggetti.

   Utilizzo del risultato `User` o `Group` (che ereditano entrambi dal `Principal` , recupera le informazioni necessarie nei flussi di lavoro. Ad esempio, i valori del nome di dominio e del nome canonico, in combinazione, identificano in modo univoco un&#39;entità principale. Questi vengono recuperati richiamando il `Principal` dell’oggetto `domainName` e `canonicalName` rispettivamente.

   Per eliminare un utente locale, richiama il `DirectoryManagerServiceService` dell’oggetto `deleteLocalUser` e passa l&#39;identificatore dell&#39;utente.

   Per eliminare un gruppo locale, richiamare `DirectoryManagerServiceService` dell’oggetto `deleteLocalGroup` e passare l&#39;identificatore del gruppo.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Gestione di ruoli e autorizzazioni {#managing-roles-and-permissions}

Questo argomento descrive come utilizzare l’API del servizio Gestione autorizzazioni (Java) per assegnare, rimuovere e determinare in modo programmatico ruoli e autorizzazioni.

In AEM Forms, un *ruolo* è un gruppo di autorizzazioni per accedere a una o più risorse a livello di sistema. Queste autorizzazioni vengono create tramite Gestione utente e vengono applicate dai componenti del servizio. Ad esempio, un amministratore può assegnare il ruolo di &quot;Autore set di criteri&quot; a un gruppo di utenti. Il Rights Management consente quindi agli utenti di quel gruppo con quel ruolo di creare set di criteri tramite la console di amministrazione.

Esistono due tipi di ruoli: *ruoli predefiniti* e *ruoli personalizzati*. Ruoli predefiniti (*ruoli di sistema)* sono già residenti in AEM Forms. Si presume che i ruoli predefiniti non possano essere eliminati o modificati dall’amministratore e che pertanto non siano modificabili. I ruoli personalizzati creati dall’amministratore, che possono successivamente modificarli o eliminarli, sono pertanto modificabili.

I ruoli semplificano la gestione delle autorizzazioni. Quando un ruolo viene assegnato a un&#39;entità principale, a tale entità viene automaticamente assegnato un set di autorizzazioni e tutte le decisioni specifiche relative all&#39;accesso per l&#39;entità si basano su quel set complessivo di autorizzazioni assegnate.

### Riepilogo dei passaggi {#summary_of_steps-4}

Per gestire ruoli e autorizzazioni, esegui i seguenti passaggi:

1. Includi file di progetto.
1. Creare un client AuthorizationManagerService.
1. Richiama le operazioni di ruolo o autorizzazione appropriate.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client AuthorizationManagerService**

Prima di poter eseguire un&#39;operazione Gestione utente AuthorizationManagerService a livello di programmazione, è necessario creare un client AuthorizationManagerService. Con l’API Java questa operazione viene eseguita creando un’ `AuthorizationManagerServiceClient` oggetto.

**Richiamare le operazioni di ruolo o autorizzazione appropriate**

Dopo aver creato il client di servizio, puoi richiamare le operazioni relative al ruolo o alle autorizzazioni. Il client di servizi consente di assegnare, rimuovere e determinare ruoli e autorizzazioni.

**Consulta anche**

[Gestione di ruoli e autorizzazioni tramite l’API Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Gestione di ruoli e autorizzazioni tramite l’API del servizio Web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestione di ruoli e autorizzazioni tramite l’API Java {#managing-roles-and-permissions-using-the-java-api}

Per gestire ruoli e autorizzazioni utilizzando l’API del servizio Gestione autorizzazioni (Java), esegui le seguenti attività:

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client AuthorizationManagerService.

   Crea un `AuthorizationManagerServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiama le operazioni di ruolo o autorizzazione appropriate.

   Per assegnare un ruolo a un&#39;entità, richiamare l&#39; `AuthorizationManagerServiceClient` dell’oggetto `assignRole` e passare i seguenti valori:

   * A `java.lang.String` oggetto contenente l&#39;identificatore del ruolo
   * Matrice di `java.lang.String` oggetti contenenti gli identificatori principali.

   Per rimuovere un ruolo da un&#39;entità, richiamare l&#39; `AuthorizationManagerServiceClient` dell’oggetto `unassignRole` e passare i seguenti valori:

   * A `java.lang.String` oggetto contenente l&#39;identificatore del ruolo.
   * Matrice di `java.lang.String` oggetti contenenti gli identificatori principali.


**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Gestione di ruoli e autorizzazioni tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione di ruoli e autorizzazioni tramite l’API del servizio Web {#managing-roles-and-permissions-using-the-web-service-api}

Gestisci ruoli e autorizzazioni utilizzando l’API del servizio Gestione autorizzazioni (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client AuthorizationManagerService.

   * Crea un `AuthorizationManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `AuthorizationManagerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `AuthorizationManagerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Richiama le operazioni di ruolo o autorizzazione appropriate.

   Per assegnare un ruolo a un&#39;entità, richiamare l&#39; `AuthorizationManagerServiceClient` dell’oggetto `assignRole` e passare i seguenti valori:

   * A `string` oggetto contenente l&#39;identificatore del ruolo
   * A `MyArrayOf_xsd_string` oggetto contenente gli identificatori principali.

   Per rimuovere un ruolo da un&#39;entità, richiamare l&#39; `AuthorizationManagerServiceService` dell’oggetto `unassignRole` e passare i seguenti valori:

   * A `string` oggetto contenente l&#39;identificatore del ruolo.
   * Matrice di `string` oggetti contenenti gli identificatori principali.


**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticazione degli utenti {#authenticating-users}

In questo argomento viene descritto come utilizzare l’API del servizio Authentication Manager (Java) per consentire alle applicazioni client di eseguire l’autenticazione programmatica degli utenti.

L&#39;autenticazione utente può essere necessaria per interagire con un database aziendale o altri archivi aziendali in cui sono archiviati dati protetti.

Considera, ad esempio, uno scenario in cui un utente immette un nome utente e una password in una pagina web e invia i valori a un server applicativo J2EE che ospita Forms. Un&#39;applicazione personalizzata Forms può autenticare l&#39;utente con il servizio Authentication Manager.

Se l&#39;autenticazione ha esito positivo, l&#39;applicazione accede a un database aziendale protetto. In caso contrario, all’utente viene inviato un messaggio in cui si informa che l’utente non è un utente autorizzato.

Il diagramma seguente mostra il flusso logico dell’applicazione.

![au_au_umauth_process](assets/au_au_umauth_process.png)

La tabella seguente descrive i passaggi descritti in questo diagramma

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>L'utente accede a un sito Web e specifica un nome utente e una password. Queste informazioni vengono inviate a un server applicativo J2EE che ospita AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le credenziali utente sono autenticate con il servizio Authentication Manager. Se le credenziali utente sono valide, il flusso di lavoro procede al passaggio 3. In caso contrario, all’utente viene inviato un messaggio in cui si informa che l’utente non è un utente autorizzato.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Le informazioni utente e una struttura del modulo vengono recuperate da un database aziendale protetto. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le informazioni utente vengono unite a una struttura del modulo e il modulo viene sottoposto a rendering per l’utente. </p></td>
  </tr>
 </tbody>
</table>

### Riepilogo dei passaggi {#summary_of_steps-5}

Per autenticare un utente a livello di programmazione, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client AuthenticationManagerService.
1. Richiama l&#39;operazione di autenticazione.
1. Se necessario, recupera il contesto in modo che l’applicazione client possa inoltrarlo a un altro servizio AEM Forms per l’autenticazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client AuthenticationManagerService**

Prima di poter autenticare un utente a livello di programmazione, è necessario creare un client AuthenticationManagerService. Quando utilizzi l’API Java, crea un `AuthenticationManagerServiceClient` oggetto.

**Richiamare l’operazione di autenticazione**

Dopo aver creato il client di servizio, puoi richiamare l’operazione di autenticazione. Questa operazione richiederà informazioni sull’utente, ad esempio il nome e la password dell’utente. Se l&#39;utente non si autentica, viene generata un&#39;eccezione.

**Recupera il contesto di autenticazione**

Dopo aver autenticato l&#39;utente, puoi creare un contesto basato sull&#39;utente autenticato. Puoi quindi utilizzare il contenuto per richiamare un altro servizio AEM Forms. Ad esempio, puoi utilizzare il contesto per creare un `EncryptionServiceClient` e crittografare un documento PDF con una password. Assicurati che l&#39;utente autenticato abbia il ruolo denominato `Services User` necessaria per richiamare un servizio AEM Forms.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Crittografia dei documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autenticazione di un utente tramite l’API Java {#authenticate-a-user-using-the-java-api}

Autentica un utente utilizzando l’API del servizio Authentication Manager (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client AuthenticationManagerServices.

   Crea un `AuthenticationManagerServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiama l&#39;operazione di autenticazione.

   Richiama il `AuthenticationManagerServiceClient` dell’oggetto `authenticate` e passare i seguenti valori:

   * A `java.lang.String` oggetto contenente il nome dell&#39;utente.
   * Matrice di byte (a `byte[]` ) contenente la password dell&#39;utente. È possibile ottenere `byte[]` richiamando l&#39;oggetto `java.lang.String` dell’oggetto `getBytes` metodo .

   Il metodo authenticate restituisce un `AuthResult` oggetto , che contiene informazioni sull&#39;utente autenticato.

1. Recupera il contesto di autenticazione.

   Richiama il `ServiceClientFactory` dell’oggetto `getContext` che restituirà un `Context` oggetto.

   Quindi invoca il `Context` dell’oggetto `initPrincipal` e passare il `AuthResult`.

### Autenticazione di un utente tramite l’API del servizio Web {#authenticate-a-user-using-the-web-service-api}

Autentica un utente utilizzando l’API del servizio Authentication Manager (servizio Web):

1. Includi file di progetto.

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL di Authentication Manager. (Vedi [Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere &quot;Riferimento all&#39;assembly client .NET&quot; in [Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Crea un client AuthenticationManagerService.

   Crea un `AuthenticationManagerServiceService` utilizzando il costruttore della classe proxy.

1. Richiama l&#39;operazione di autenticazione.

   Richiama il `AuthenticationManagerServiceClient` dell’oggetto `authenticate` e passare i seguenti valori:

   * A `string` oggetto contenente il nome dell&#39;utente
   * Matrice di byte (a `byte[]` ) contenente la password dell&#39;utente. È possibile ottenere `byte[]` conversione di un oggetto `string` oggetto contenente la password di un `byte[]` utilizzando la logica mostrata nell’esempio seguente.
   * Il valore restituito sarà un `AuthResult` oggetto , che può essere utilizzato per recuperare informazioni sull&#39;utente. Nell’esempio seguente, le informazioni dell’utente vengono recuperate ottenendo prima il `AuthResult` dell’oggetto `authenticatedUser` e successivamente ottenere il risultato `User` dell’oggetto `canonicalName` e `domainName` campi.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronizzazione programmatica degli utenti {#programmatically-synchronizing-users}

Puoi sincronizzare gli utenti in modo programmatico utilizzando l&#39;API User Management. Quando sincronizzi gli utenti, stai aggiornando AEM Forms con i dati utente che si trovano nel tuo archivio utenti. Ad esempio, si supponga di aggiungere nuovi utenti all’archivio utenti. Dopo aver eseguito un’operazione di sincronizzazione, i nuovi utenti diventano utenti di moduli AEM. Inoltre, gli utenti che non si trovano più nel tuo archivio utenti vengono rimossi da AEM Forms.

Il diagramma seguente mostra la sincronizzazione di AEM Forms con un archivio utenti.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

La tabella seguente descrive i passaggi descritti in questo diagramma

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un'applicazione client richiede che AEM Forms esegua un'operazione di sincronizzazione.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms esegue un’operazione di sincronizzazione.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Le informazioni utente vengono aggiornate.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Un utente è in grado di visualizzare le informazioni utente aggiornate. </p></td>
  </tr>
 </tbody>
</table>

### Riepilogo dei passaggi {#summary_of_steps-6}

Per sincronizzare programmaticamente gli utenti, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client UserManagerUtilServiceClient.
1. Specifica il dominio enterprise.
1. Richiama l&#39;operazione di autenticazione.
1. Determinare se l’operazione di sincronizzazione è completa

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Crea un client UserManagerUtilServiceClient**

Prima di poter sincronizzare programmaticamente gli utenti, devi creare un `UserManagerUtilServiceClient` oggetto.

**Specificare il dominio enterprise**

Prima di eseguire un’operazione di sincronizzazione utilizzando l’API User Management, specificare il dominio enterprise a cui appartengono gli utenti. Puoi specificare uno o più domini enterprise. Prima di eseguire un’operazione di sincronizzazione a livello di programmazione, è necessario impostare un dominio enterprise utilizzando la console di amministrazione. (Vedi [aiuto amministrativo](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Richiamare l’operazione di sincronizzazione**

Dopo aver specificato uno o più domini enterprise, è possibile eseguire l&#39;operazione di sincronizzazione. Il tempo necessario per eseguire questa operazione dipende dal numero di record utente che si trovano nell’archivio degli utenti.

**Determinare se l’operazione di sincronizzazione è completa**

Dopo aver eseguito un’operazione di sincronizzazione a livello di programmazione, puoi determinare se l’operazione è completa.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Crittografia dei documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronizzazione programmatica degli utenti tramite l’API Java {#programmatically-synchronizing-users-using-the-java-api}

Sincronizza gli utenti utilizzando l&#39;API User Management (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-usermanager-client.jar e adobe-usermanager-util-client.jar, nel percorso di classe del progetto Java.

1. Creare un client UserManagerUtilServiceClient.

   Crea un `UserManagerUtilServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Specifica il dominio enterprise.

   * Richiama il `UserManagerUtilServiceClient` dell’oggetto `scheduleSynchronization` per avviare l&#39;operazione di sincronizzazione utente.
   * Crea un `java.util.Set` tramite un `HashSet` costruttore. Assicurati di specificare `String` come tipo di dati. Questo `Java.util.Set` instance memorizza i nomi di dominio a cui si applica l&#39;operazione di sincronizzazione.
   * Per ogni nome di dominio da aggiungere, invoca la `java.util.Set` metodo add dell&#39;oggetto e passare il nome di dominio.

1. Richiama l&#39;operazione di sincronizzazione.

   Richiama il `ServiceClientFactory` dell’oggetto `getContext` che restituirà un `Context` oggetto.

   Quindi invoca il `Context` dell’oggetto `initPrincipal` e passare il `AuthResult`.

**Consulta anche**

[Sincronizzazione programmatica degli utenti](users.md#programmatically-synchronizing-users)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
