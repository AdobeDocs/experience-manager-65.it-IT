---
title: Gestione degli utenti
description: Utilizza l’API User Management per creare applicazioni client in grado di gestire ruoli, autorizzazioni e entità principali (che possono essere utenti o gruppi) e autenticare gli utenti.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '6201'
ht-degree: 0%

---

# Gestione degli utenti {#managing-users}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sulla gestione degli utenti**

È possibile utilizzare l’API User Management per creare applicazioni client in grado di gestire ruoli, autorizzazioni e entità principali (utenti o gruppi) e autenticare gli utenti. L’API User Management è costituita dalle seguenti API di AEM Forms:

* API del servizio Directory Manager
* API del servizio Authentication Manager
* API del servizio Gestione autorizzazioni

Gestione utente consente di assegnare, rimuovere e determinare ruoli e autorizzazioni. Consente inoltre di assegnare, rimuovere ed eseguire query su domini, utenti e gruppi. Infine, puoi utilizzare Gestione utenti per autenticare gli utenti.

In [Aggiunta di utenti](users.md#adding-users) verrà illustrato come aggiungere utenti a livello di programmazione. In questa sezione viene utilizzata l&#39;API del servizio Directory Manager.

In [Eliminazione utenti](users.md#deleting-users) verrà illustrato come eliminare gli utenti a livello di programmazione. In questa sezione viene utilizzata l&#39;API del servizio Directory Manager.

In [Gestione di utenti e gruppi](users.md#managing-users-and-groups) verrà illustrata la differenza tra un utente locale e un utente della directory e verranno forniti esempi di utilizzo delle API Java e dei servizi Web per la gestione programmatica di utenti e gruppi. In questa sezione viene utilizzata l&#39;API del servizio Directory Manager.

In [Gestione di ruoli e autorizzazioni](users.md#managing-roles-and-permissions) verranno fornite informazioni sui ruoli di sistema e sulle autorizzazioni e su ciò che è possibile fare a livello di programmazione per potenziarli. Vengono inoltre forniti esempi di utilizzo delle API Java e dei servizi Web per la gestione di ruoli e autorizzazioni a livello di programmazione. In questa sezione vengono utilizzate sia l&#39;API del servizio Directory Manager che l&#39;API del servizio Gestione autorizzazioni.

In [Autenticazione degli utenti](users.md#authenticating-users) verranno visualizzati esempi di utilizzo delle API Java e dei servizi Web per l&#39;autenticazione a livello di programmazione degli utenti. In questa sezione viene utilizzata l’API del servizio Gestione autorizzazioni.

**Informazioni sul processo di autenticazione**

User Management offre funzionalità di autenticazione integrate e la possibilità di collegarsi al provider di autenticazione personale. Quando User Management riceve una richiesta di autenticazione (ad esempio, un utente tenta di accedere), trasmette le informazioni utente al provider di autenticazione per l’autenticazione. Gestione utenti riceve i risultati dal provider di autenticazione dopo l&#39;autenticazione dell&#39;utente.

Il diagramma seguente mostra l’interazione tra un utente finale che tenta di accedere, User Management e il provider di autenticazione.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

La tabella seguente descrive ogni passaggio del processo di autenticazione.

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
   <td><p>Un utente tenta di accedere a un servizio che richiama Gestione utenti. L'utente specifica un nome utente e una password. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Gestione utenti invia il nome utente, la password e le informazioni di configurazione al provider di autenticazione.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Il provider di autenticazione si connette all'archivio utenti e autentica l'utente.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il provider di autenticazione restituisce i risultati a Gestione utenti.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Gestione utenti consente all’utente di accedere al prodotto o nega l’accesso allo stesso.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se il fuso orario del server è diverso da quello del client, quando si utilizza il WSDL per il servizio AEM Forms Generate PDF su uno stack SOAP nativo utilizzando un client .NET in un cluster Application Server WebSphere, può verificarsi il seguente errore di autenticazione di User Management:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Informazioni sulla gestione delle directory**

Gestione utenti è fornito con un provider di servizi di directory (DirectoryManagerService) che supporta le connessioni alle directory LDAP. Se l&#39;organizzazione utilizza un repository non LDAP per memorizzare i record utente, è possibile creare un provider di servizi di directory personalizzato che funzioni con il repository.

I provider di servizi di directory recuperano i record da un archivio utenti su richiesta di Gestione utenti. Gestione utenti memorizza regolarmente nella cache i record di utenti e gruppi nel database per migliorarne le prestazioni.

Il provider del servizio directory può essere utilizzato per sincronizzare il database di User Management con l&#39;archivio utenti. Questo passaggio assicura che tutte le informazioni della directory utente e tutti i record degli utenti e dei gruppi siano aggiornati.

Inoltre, DirectoryManagerService consente di creare e gestire i domini. I domini definiscono basi utente diverse. Il limite di un dominio viene in genere definito in base alla struttura dell’organizzazione o alla configurazione dell’archivio utenti. I domini User Management forniscono le impostazioni di configurazione utilizzate dai provider di autenticazione e dai provider di servizi directory.

Nel codice XML di configurazione esportato da Gestione utenti, il nodo principale con valore di attributo `Domains` contiene un elemento XML per ogni dominio definito per Gestione utenti. Ciascuno di questi elementi contiene altri elementi che definiscono gli aspetti del dominio associati a specifici fornitori di servizi.

**Informazioni sui valori objectSID**

Quando si utilizza Active Directory, è importante comprendere che un valore `objectSID` non è un attributo univoco tra più domini. Questo valore memorizza l&#39;identificatore di protezione di un oggetto. In un ambiente con più domini (ad esempio, una struttura ad albero di domini) il valore `objectSID` può essere diverso.

Un valore `objectSID` cambierebbe se un oggetto viene spostato da un dominio Active Directory a un altro. Alcuni oggetti hanno lo stesso valore `objectSID` in qualsiasi punto del dominio. Ad esempio, gruppi come BUILTIN\Administrators, BUILTIN\Power Users e così via, avrebbero lo stesso valore `objectSID` indipendentemente dai domini. Questi valori `objectSID` sono noti.

## Aggiunta di utenti {#adding-users}

È possibile utilizzare l’API del servizio Directory Manager (Java e servizio Web) per aggiungere utenti ad AEM Forms a livello di programmazione. Dopo aver aggiunto un utente, è possibile utilizzarlo quando si esegue un&#39;operazione di servizio che richiede un utente. È ad esempio possibile assegnare un&#39;attività al nuovo utente.

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un utente, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Definire le informazioni utente.
1. Aggiungi l’utente ad AEM Forms.
1. Verifica che l’utente sia stato aggiunto.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Creare un client DirectoryManagerService**

Prima di poter eseguire un&#39;operazione del servizio Directory Manager a livello di programmazione, creare un client API del servizio Directory Manager.

**Definisci informazioni utente**

Quando si aggiunge un nuovo utente utilizzando l&#39;API del servizio Directory Manager, definire le informazioni per tale utente. In genere, quando si aggiunge un nuovo utente, vengono definiti i seguenti valori:

* **Nome dominio**: il dominio a cui appartiene l&#39;utente (ad esempio, `DefaultDom`).
* **Valore dell&#39;identificatore utente**: il valore dell&#39;identificatore dell&#39;utente (ad esempio, `wblue`).
* **Tipo di entità**: il tipo di utente (ad esempio, è possibile specificare `USER)`.
* **Nome**: un nome specifico per l&#39;utente (ad esempio, `Wendy`).
* **Cognome**: il cognome dell&#39;utente (ad esempio, `Blue)`.
* **Impostazioni locali**: informazioni sulle impostazioni internazionali per l&#39;utente.

**Aggiungi utente ad AEM Forms**

Dopo aver definito le informazioni utente, puoi aggiungerlo ad AEM Forms. Per aggiungere un utente, richiamare il metodo `createLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient`.

**Verificare che l&#39;utente sia stato aggiunto**

Puoi verificare che l’utente sia stato aggiunto per garantire che non si siano verificati problemi. Individua il nuovo utente utilizzando il valore dell’identificatore utente.

**Consulta anche**

[Aggiungere utenti utilizzando l’API Java](users.md#add-users-using-the-java-api)

[Aggiungere utenti utilizzando l’API del servizio web](users.md#add-users-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Eliminazione di utenti](users.md#deleting-users)

### Aggiungere utenti utilizzando l’API Java {#add-users-using-the-java-api}

Aggiungere utenti utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerServices.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Definire le informazioni utente.

   * Creare un oggetto `UserImpl` utilizzando il relativo costruttore.
   * Impostare il nome del dominio richiamando il metodo `setDomainName` dell&#39;oggetto `UserImpl`. Passa un valore stringa che specifica il nome di dominio.
   * Impostare il tipo di entità richiamando il metodo `setPrincipalType` dell&#39;oggetto `UserImpl`. Passa un valore stringa che specifica il tipo di utente. Ad esempio, è possibile specificare `USER`.
   * Impostare il valore dell&#39;identificatore utente richiamando il metodo `setUserid` dell&#39;oggetto `UserImpl`. Passa un valore stringa che specifica il valore dell&#39;identificatore utente. Ad esempio, è possibile specificare `wblue`.
   * Impostare il nome canonico richiamando il metodo `setCanonicalName` dell&#39;oggetto `UserImpl`. Passa un valore stringa che specifica il nome canonico dell&#39;utente. Ad esempio, è possibile specificare `wblue`.
   * Impostare il nome specificato richiamando il metodo `setGivenName` dell&#39;oggetto `UserImpl`. Passa un valore stringa che specifica il nome dell&#39;utente. Ad esempio, è possibile specificare `Wendy`.
   * Impostare il cognome richiamando il metodo `setFamilyName` dell&#39;oggetto `UserImpl`. Passa un valore stringa che specifica il cognome dell&#39;utente. Ad esempio, è possibile specificare `Blue`.

   >[!NOTE]
   >
   >Richiama un metodo che appartiene all&#39;oggetto `UserImpl` per impostare altri valori. È ad esempio possibile impostare il valore delle impostazioni locali richiamando il metodo `setLocale` dell&#39;oggetto `UserImpl`.

1. Aggiungi l’utente ad AEM Forms.

   Richiama il metodo `createLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient` e passa i seguenti valori:

   * Oggetto `UserImpl` che rappresenta il nuovo utente
   * Valore stringa che rappresenta la password dell&#39;utente

   Il metodo `createLocalUser` restituisce un valore stringa che specifica il valore dell&#39;identificatore utente locale.

1. Verifica che l’utente sia stato aggiunto.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostare il valore dell&#39;identificatore utente richiamando il metodo `setUserId` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiama il metodo `findPrincipals` dell&#39;oggetto `DirectoryManagerServiceClient` e passa l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un&#39;istanza `java.util.List`, in cui ogni elemento è un oggetto `User`. Scorrere l&#39;istanza `java.util.List` per individuare l&#39;utente.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Quick Start (modalità SOAP): aggiunta di utenti utilizzando l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aggiungere utenti utilizzando l’API del servizio web {#add-users-using-the-web-service-api}

Aggiungere utenti utilizzando l&#39;API del servizio Gestione directory (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL per il riferimento del servizio: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client DirectoryManagerService.

   * Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DirectoryManagerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Assicurarsi di specificare `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Definire le informazioni utente.

   * Creare un oggetto `UserImpl` utilizzando il relativo costruttore.
   * Impostare il nome del dominio assegnando un valore stringa al campo `domainName` dell&#39;oggetto `UserImpl`.
   * Impostare il tipo di entità assegnando un valore stringa al campo `principalType` dell&#39;oggetto `UserImpl`. Ad esempio, è possibile specificare `USER`.
   * Impostare il valore dell&#39;identificatore utente assegnando un valore stringa al campo `userid` dell&#39;oggetto `UserImpl`.
   * Impostare il valore del nome canonico assegnando un valore stringa al campo `canonicalName` dell&#39;oggetto `UserImpl`.
   * Impostare il valore del nome specificato assegnando un valore stringa al campo `givenName` dell&#39;oggetto `UserImpl`.
   * Impostare il valore del family name assegnando un valore stringa al campo `familyName` dell&#39;oggetto `UserImpl`.

1. Aggiungi l’utente ad AEM Forms.

   Richiama il metodo `createLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient` e passa i seguenti valori:

   * Oggetto `UserImpl` che rappresenta il nuovo utente
   * Valore stringa che rappresenta la password dell&#39;utente

   Il metodo `createLocalUser` restituisce un valore stringa che specifica il valore dell&#39;identificatore utente locale.

1. Verifica che l’utente sia stato aggiunto.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostare il valore dell&#39;identificatore utente assegnando un valore stringa che rappresenta il valore dell&#39;identificatore utente al campo `userId` dell&#39;oggetto `PrincipalSearchFilter`.
   * Richiama il metodo `findPrincipals` dell&#39;oggetto `DirectoryManagerServiceClient` e passa l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un insieme `MyArrayOfUser`, dove ogni elemento è un oggetto `User`. Scorrere la raccolta `MyArrayOfUser` per individuare l&#39;utente.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminazione di utenti {#deleting-users}

È possibile utilizzare l’API del servizio Directory Manager (Java e servizio Web) per eliminare gli utenti da AEM Forms a livello di programmazione. Dopo aver eliminato un utente, non è più possibile utilizzarlo per eseguire un&#39;operazione di servizio che richiede un utente. Ad esempio, non è possibile assegnare un&#39;attività a un utente eliminato.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per eliminare un utente, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Specificare l&#39;utente da eliminare.
1. Elimina l’utente da AEM Forms.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Creare un client DirectoryManagerService**

Prima di poter eseguire un&#39;operazione API del servizio Directory Manager a livello di programmazione, creare un client del servizio Directory Manager.

**Specificare l&#39;utente da eliminare**

Puoi specificare un utente da eliminare utilizzando il relativo valore di identificatore.

**Elimina utente da AEM Forms**

Per eliminare un utente, richiamare il metodo `deleteLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient`.

**Consulta anche**

[Eliminare gli utenti utilizzando l’API Java](users.md#delete-users-using-the-java-api)

[Eliminare gli utenti utilizzando l’API del servizio web](users.md#delete-users-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di utenti](users.md#adding-users)

### Eliminare gli utenti utilizzando l’API Java {#delete-users-using-the-java-api}

Eliminare gli utenti utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare l&#39;utente da eliminare.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostare il valore dell&#39;identificatore utente richiamando il metodo `setUserId` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiama il metodo `findPrincipals` dell&#39;oggetto `DirectoryManagerServiceClient` e passa l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un&#39;istanza `java.util.List`, in cui ogni elemento è un oggetto `User`. Scorrere l&#39;istanza `java.util.List` per individuare l&#39;utente da eliminare.

1. Elimina l’utente da AEM Forms.

   Richiama il metodo `deleteLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient` e passa il valore del campo `oid` dell&#39;oggetto `User`. Richiama il metodo `getOid` dell&#39;oggetto `User`. Utilizzare l&#39;oggetto `User` recuperato dall&#39;istanza `java.util.List`.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Quick Start (modalità EJB): eliminazione di utenti tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Quick Start (modalità SOAP): eliminazione di utenti tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminare gli utenti utilizzando l’API del servizio web {#delete-users-using-the-web-service-api}

Eliminare gli utenti utilizzando l&#39;API del servizio Directory Manager (servizio Web):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   * Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DirectoryManagerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Assicurarsi di specificare `blob=mtom.`
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Specificare l&#39;utente da eliminare.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostare il valore dell&#39;identificatore utente assegnando un valore stringa al campo `userId` dell&#39;oggetto `PrincipalSearchFilter`.
   * Richiama il metodo `findPrincipals` dell&#39;oggetto `DirectoryManagerServiceClient` e passa l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un insieme `MyArrayOfUser`, dove ogni elemento è un oggetto `User`. Scorrere la raccolta `MyArrayOfUser` per individuare l&#39;utente. L&#39;oggetto `User` recuperato dall&#39;insieme `MyArrayOfUser` viene utilizzato per eliminare l&#39;utente.

1. Elimina l’utente da AEM Forms.

   Eliminare l&#39;utente passando il valore del campo `oid` dell&#39;oggetto `User` al metodo `deleteLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient`.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di gruppi {#creating-groups}

È possibile utilizzare l’API del servizio Directory Manager (Java e servizio Web) per creare in modo programmatico gruppi AEM Forms. Dopo aver creato un gruppo, è possibile utilizzarlo per eseguire un&#39;operazione di servizio che richiede un gruppo. Ad esempio, puoi assegnare un utente al nuovo gruppo. (Vedi [Gestione di utenti e gruppi](users.md#managing-users-and-groups).)

### Riepilogo dei passaggi {#summary_of_steps-2}

Per creare un gruppo, attenersi alla procedura descritta di seguito.

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Determina che il gruppo non esiste.
1. Crea il gruppo.
1. Eseguire un&#39;azione con il gruppo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DirectoryManagerService**

Prima di poter eseguire un&#39;operazione del servizio Directory Manager a livello di programmazione, creare un client API del servizio Directory Manager.

**Determinare se il gruppo esiste**

Quando crei un gruppo, accertati che non esista nello stesso dominio. In altre parole, due gruppi non possono avere lo stesso nome all’interno dello stesso dominio. Per eseguire questa operazione, eseguire una ricerca e filtrare i risultati in base a due valori. Impostare il tipo di entità su `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` per assicurarsi che vengano restituiti solo i gruppi. Inoltre, assicurati di specificare il nome di dominio.

**Crea il gruppo**

Dopo aver determinato che il gruppo non esiste nel dominio, crealo e specifica i seguenti attributi:

* **CommonName**: nome del gruppo.
* **Dominio**: dominio in cui viene aggiunto il gruppo.
* **Descrizione**: descrizione del gruppo.

**Esegui un&#39;azione con il gruppo**

Dopo aver creato un gruppo, potete eseguire un&#39;azione utilizzando il gruppo. Ad esempio, puoi aggiungere un utente al gruppo. Per aggiungere un utente a un gruppo, recupera il valore dell’identificatore univoco sia dell’utente che del gruppo. Trasmettere questi valori al metodo `addPrincipalToLocalGroup`.

**Consulta anche**

[Creare gruppi tramite API Java](users.md#create-groups-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di utenti](users.md#adding-users)

[Eliminazione di utenti](users.md#deleting-users)

### Creare gruppi tramite API Java {#create-groups-using-the-java-api}

Creare un gruppo utilizzando l&#39;API del servizio Directory Manager (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Determinare se il gruppo esiste.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostare il tipo di entità richiamando l&#39;oggetto `setPrincipalType` dell&#39;oggetto `PrincipalSearchFilter`. Passa il valore `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Impostare il dominio richiamando l&#39;oggetto `setSpecificDomainName` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore stringa che specifica il nome di dominio.
   * Per trovare un gruppo, richiamare il metodo `findPrincipals` dell&#39;oggetto `DirectoryManagerServiceClient` (un&#39;entità può essere un gruppo). Passa l&#39;oggetto `PrincipalSearchFilter` che specifica il tipo di entità principale e il nome di dominio. Questo metodo restituisce un&#39;istanza `java.util.List` in cui ogni elemento è un&#39;istanza `Group`. Ogni istanza del gruppo è conforme al filtro specificato mediante l&#39;oggetto `PrincipalSearchFilter`.
   * Scorrere l&#39;istanza `java.util.List`. Per ogni elemento, recupera il nome del gruppo. Verificare che il nome del gruppo non sia uguale al nuovo nome del gruppo.

1. Crea il gruppo.

   * Se il gruppo non esiste, richiamare il metodo `setCommonName` dell&#39;oggetto `Group` e passare un valore stringa che specifichi il nome del gruppo.
   * Richiama il metodo `setDescription` dell&#39;oggetto `Group` e passa un valore stringa che specifica la descrizione del gruppo.
   * Richiama il metodo `setDomainName` dell&#39;oggetto `Group` e passa un valore stringa che specifica il nome di dominio.
   * Richiama il metodo `createLocalGroup` dell&#39;oggetto `DirectoryManagerServiceClient` e passa l&#39;istanza `Group`.

   Il metodo `createLocalUser` restituisce un valore stringa che specifica il valore dell&#39;identificatore utente locale.

1. Eseguire un&#39;azione con il gruppo.

   * Creare un oggetto `PrincipalSearchFilter` utilizzando il relativo costruttore.
   * Impostare il valore dell&#39;identificatore utente richiamando il metodo `setUserId` dell&#39;oggetto `PrincipalSearchFilter`. Passa un valore stringa che rappresenta il valore dell&#39;identificatore utente.
   * Richiama il metodo `findPrincipals` dell&#39;oggetto `DirectoryManagerServiceClient` e passa l&#39;oggetto `PrincipalSearchFilter`. Questo metodo restituisce un&#39;istanza `java.util.List`, in cui ogni elemento è un oggetto `User`. Scorrere l&#39;istanza `java.util.List` per individuare l&#39;utente.
   * Aggiungere un utente al gruppo richiamando il metodo `addPrincipalToLocalGroup` dell&#39;oggetto `DirectoryManagerServiceClient`. Passa il valore restituito del metodo `getOid` dell&#39;oggetto `User`. Passare il valore restituito del metodo `getOid` degli oggetti `Group` (utilizzare l&#39;istanza `Group` che rappresenta il nuovo gruppo).

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestione di utenti e gruppi {#managing-users-and-groups}

Questo argomento descrive come utilizzare (Java) per assegnare, rimuovere ed eseguire query a livello di programmazione su domini, utenti e gruppi.

>[!NOTE]
>
>Durante la configurazione di un dominio, devi impostare l’identificatore univoco per gruppi e utenti. L’attributo scelto non deve essere univoco solo all’interno dell’ambiente LDAP, ma deve anche essere immutabile e non cambierà all’interno della directory. L&#39;attributo deve inoltre essere di tipo stringa semplice (l&#39;unica eccezione attualmente consentita per Active Directory 2000/2003 è `"objectsid"`, che è un valore binario). L&#39;attributo `"GUID"` di Novell eDirectory, ad esempio, non è un tipo di dati stringa semplice e pertanto non funzionerà.

* Per Active Directory, utilizzare `"objectsid"`.
* Per SunOne, utilizzare `"nsuniqueid"`.

>[!NOTE]
>
>La creazione di più utenti e gruppi locali mentre è in corso la sincronizzazione di una directory LDAP non è supportata. Il tentativo di eseguire questo processo può causare errori.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per gestire utenti e gruppi, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DirectoryManagerService.
1. Richiama le operazioni appropriate dell’utente o del gruppo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client DirectoryManagerService**

Prima di poter eseguire un&#39;operazione di servizio di Directory Manager a livello di programmazione, è necessario creare un client di servizio di Directory Manager. Con l&#39;API Java questo viene effettuato creando un oggetto `DirectoryManagerServiceClient`. Con l&#39;API del servizio Web questo viene effettuato creando un oggetto `DirectoryManagerServiceService`.

**Richiama l&#39;utente o il gruppo appropriato**

Dopo aver creato il client del servizio, è possibile richiamare le operazioni di gestione degli utenti o dei gruppi. Il client del servizio consente di assegnare, rimuovere ed eseguire query su domini, utenti e gruppi. Si noti che è possibile aggiungere un&#39;entità di directory o un&#39;entità locale a un gruppo locale, ma non è possibile aggiungere un&#39;entità locale a un gruppo di directory.

**Consulta anche**

[Gestione di utenti e gruppi tramite API Java](users.md#managing-users-and-groups-using-the-java-api)

[Gestione di utenti e gruppi tramite l’API del servizio web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestione di utenti e gruppi tramite API Java {#managing-users-and-groups-using-the-java-api}

Per gestire in modo programmatico utenti, gruppi e domini utilizzando (Java), esegui le seguenti attività:

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java. Per informazioni sul percorso di questi file, vedere [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione. Per informazioni, vedere [Impostazione delle proprietà di connessione ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Richiama le operazioni appropriate dell’utente o del gruppo.

   Per trovare un utente o un gruppo, richiamare uno dei metodi dell&#39;oggetto `DirectoryManagerServiceClient` per trovare le entità (poiché un&#39;entità può essere un utente o un gruppo). Nell&#39;esempio seguente, il metodo `findPrincipals` viene chiamato utilizzando un filtro di ricerca (un oggetto `PrincipalSearchFilter`).

   Poiché in questo caso il valore restituito è un `java.util.List` contenente `Principal` oggetti, scorrere il risultato ed eseguire il cast degli oggetti `Principal` su `User` o `Group`.

   Utilizzando l&#39;oggetto `User` o `Group` risultante (entrambi ereditati dall&#39;interfaccia `Principal`), recuperare le informazioni necessarie nei flussi di lavoro. Ad esempio, la combinazione dei valori del nome di dominio e del nome canonico identifica in modo univoco un’entità principale. Questi vengono recuperati richiamando i metodi `getDomainName` e `getCanonicalName` dell&#39;oggetto `Principal`, rispettivamente.

   Per eliminare un utente locale, richiamare il metodo `deleteLocalUser` dell&#39;oggetto `DirectoryManagerServiceClient` e passare l&#39;identificatore dell&#39;utente.

   Per eliminare un gruppo locale, richiamare il metodo `deleteLocalGroup` dell&#39;oggetto `DirectoryManagerServiceClient` e passare l&#39;identificatore del gruppo.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione di utenti e gruppi tramite l’API del servizio web {#managing-users-and-groups-using-the-web-service-api}

Per gestire in modo programmatico utenti, gruppi e domini tramite l&#39;API del servizio Directory Manager (servizio Web), eseguire le operazioni seguenti:

1. Includi file di progetto.

   * Creare un assembly client Microsoft .NET che utilizza il WSDL di Gestione directory. (Vedi [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).

1. Creare un client DirectoryManagerService.

   Creare un oggetto `DirectoryManagerServiceService` utilizzando il costruttore della classe proxy.

1. Richiama le operazioni appropriate dell’utente o del gruppo.

   Per trovare un utente o un gruppo, richiamare uno dei metodi dell&#39;oggetto `DirectoryManagerServiceService` per trovare le entità (poiché un&#39;entità può essere un utente o un gruppo). Nell&#39;esempio seguente, il metodo `findPrincipalsWithFilter` viene chiamato utilizzando un filtro di ricerca (un oggetto `PrincipalSearchFilter`). Quando si utilizza un oggetto `PrincipalSearchFilter`, le entità locali vengono restituite solo se la proprietà `isLocal` è impostata su `true`. Questo comportamento è diverso da quello che si verificherebbe con l’API Java.

   >[!NOTE]
   >
   >Se nel filtro di ricerca non viene specificato il numero massimo di risultati (tramite il campo `PrincipalSearchFilter.resultsMax`), verrà restituito un massimo di 1000 risultati. Si tratta di un comportamento diverso rispetto a quello che si verifica utilizzando l’API Java, in cui 10 risultati è il massimo predefinito. Inoltre, i metodi di ricerca come `findGroupMembers` non produrranno alcun risultato a meno che nel filtro di ricerca non sia specificato il numero massimo di risultati (ad esempio, tramite il campo `GroupMembershipSearchFilter.resultsMax`). Questo vale per tutti i filtri di ricerca che ereditano dalla classe `GenericSearchFilter`. Per ulteriori informazioni, consulta [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Poiché in questo caso il valore restituito è un `object[]` contenente `Principal` oggetti, scorrere il risultato ed eseguire il cast degli oggetti `Principal` su `User` o `Group`.

   Utilizzando l&#39;oggetto `User` o `Group` risultante (entrambi ereditati dall&#39;interfaccia `Principal`), recuperare le informazioni necessarie nei flussi di lavoro. Ad esempio, la combinazione dei valori del nome di dominio e del nome canonico identifica in modo univoco un’entità principale. Questi vengono recuperati richiamando rispettivamente i campi `domainName` e `canonicalName` dell&#39;oggetto `Principal`.

   Per eliminare un utente locale, richiamare il metodo `deleteLocalUser` dell&#39;oggetto `DirectoryManagerServiceService` e passare l&#39;identificatore dell&#39;utente.

   Per eliminare un gruppo locale, richiamare il metodo `deleteLocalGroup` dell&#39;oggetto `DirectoryManagerServiceService` e passare l&#39;identificatore del gruppo.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Gestione di ruoli e autorizzazioni {#managing-roles-and-permissions}

In questo argomento viene descritto come utilizzare l&#39;API del servizio Gestione autorizzazioni (Java) per assegnare, rimuovere e determinare in modo programmatico ruoli e autorizzazioni.

In AEM Forms, un *ruolo* è un gruppo di autorizzazioni per accedere a una o più risorse a livello di sistema. Queste autorizzazioni vengono create tramite Gestione utenti e vengono applicate dai componenti del servizio. Ad esempio, un amministratore può assegnare il ruolo di &quot;Autore set di criteri&quot; a un gruppo di utenti. Il Rights Management consente quindi agli utenti del gruppo con tale ruolo di creare set di criteri tramite la console di amministrazione.

Esistono due tipi di ruoli: *ruoli predefiniti* e *ruoli personalizzati*. I ruoli predefiniti (*ruoli di sistema)* sono già residenti in AEM Forms. Si presume che i ruoli predefiniti non possano essere eliminati o modificati dall’amministratore e che pertanto non siano modificabili. I ruoli personalizzati creati dall’amministratore, che può successivamente modificarli o eliminarli, sono quindi modificabili.

I ruoli semplificano la gestione delle autorizzazioni. Quando a un utente/gruppo/ruolo viene assegnato un ruolo, a tale utente/gruppo/ruolo viene automaticamente assegnato un insieme di autorizzazioni e tutte le decisioni specifiche relative all&#39;accesso per l&#39;utente/gruppo/ruolo si basano su tale insieme complessivo di autorizzazioni assegnate.

### Riepilogo dei passaggi {#summary_of_steps-4}

Per gestire ruoli e autorizzazioni, attieniti alla seguente procedura:

1. Includi file di progetto.
1. Creare un client AuthorizationManagerService.
1. Richiama le operazioni di ruolo o autorizzazione appropriate.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client AuthorizationManagerService**

Prima di poter eseguire a livello di programmazione un&#39;operazione AuthorizationManagerService di User Management, è necessario creare un client AuthorizationManagerService. Con l&#39;API Java questo viene effettuato creando un oggetto `AuthorizationManagerServiceClient`.

**Richiama il ruolo o le operazioni di autorizzazione appropriate**

Dopo aver creato il client del servizio, è possibile richiamare le operazioni relative al ruolo o alle autorizzazioni. Il client del servizio consente di assegnare, rimuovere e determinare ruoli e autorizzazioni.

**Consulta anche**

[Gestione di ruoli e autorizzazioni tramite API Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Gestione di ruoli e autorizzazioni tramite l’API del servizio web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestione di ruoli e autorizzazioni tramite API Java {#managing-roles-and-permissions-using-the-java-api}

Per gestire ruoli e autorizzazioni tramite l’API del servizio Gestione autorizzazioni (Java), esegui le seguenti attività:

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client AuthorizationManagerService.

   Creare un oggetto `AuthorizationManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama le operazioni di ruolo o autorizzazione appropriate.

   Per assegnare un ruolo a un&#39;entità, richiamare il metodo `assignRole` dell&#39;oggetto `AuthorizationManagerServiceClient` e passare i valori seguenti:

   * Un oggetto `java.lang.String` che contiene l&#39;identificatore del ruolo
   * Matrice di `java.lang.String` oggetti contenente gli identificatori principali.

   Per rimuovere un ruolo da un&#39;entità, richiamare il metodo `unassignRole` dell&#39;oggetto `AuthorizationManagerServiceClient` e passare i valori seguenti:

   * Oggetto `java.lang.String` contenente l&#39;identificatore del ruolo.
   * Matrice di `java.lang.String` oggetti contenente gli identificatori principali.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Quick Start (modalità SOAP): gestione di ruoli e autorizzazioni tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione di ruoli e autorizzazioni tramite l’API del servizio web {#managing-roles-and-permissions-using-the-web-service-api}

Gestisci ruoli e autorizzazioni tramite l’API del servizio Gestione autorizzazioni (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client AuthorizationManagerService.

   * Creare un oggetto `AuthorizationManagerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AuthorizationManagerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AuthorizationManagerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Richiama le operazioni di ruolo o autorizzazione appropriate.

   Per assegnare un ruolo a un&#39;entità, richiamare il metodo `assignRole` dell&#39;oggetto `AuthorizationManagerServiceClient` e passare i valori seguenti:

   * Un oggetto `string` che contiene l&#39;identificatore del ruolo
   * Oggetto `MyArrayOf_xsd_string` contenente gli identificatori principali.

   Per rimuovere un ruolo da un&#39;entità, richiamare il metodo `unassignRole` dell&#39;oggetto `AuthorizationManagerServiceService` e passare i valori seguenti:

   * Oggetto `string` contenente l&#39;identificatore del ruolo.
   * Matrice di `string` oggetti contenente gli identificatori principali.

**Consulta anche**

[Riepilogo dei passaggi](users.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticazione degli utenti {#authenticating-users}

Questo argomento descrive come utilizzare l’API del servizio Authentication Manager (Java) per abilitare le applicazioni client all’autenticazione a livello di programmazione degli utenti.

L&#39;autenticazione utente può essere necessaria per interagire con un database aziendale o altri archivi aziendali che memorizzano dati protetti.

Si consideri, ad esempio, uno scenario in cui un utente immette un nome utente e una password in una pagina Web e invia i valori a un server applicazioni J2EE che ospita Forms. Un’applicazione personalizzata Forms può autenticare l’utente con il servizio Authentication Manager.

Se l&#39;autenticazione ha esito positivo, l&#39;applicazione accede a un database aziendale protetto. In caso contrario, viene inviato all’utente un messaggio che indica che l’utente non è un utente autorizzato.

Il diagramma seguente mostra il flusso logico dell&#39;applicazione.

![au_au_umauth_process](assets/au_au_umauth_process.png)

Nella tabella seguente vengono descritti i passaggi del diagramma

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
   <td><p>L'utente accede a un sito Web e specifica un nome utente e una password. Queste informazioni vengono inviate a un server applicazioni J2EE che ospita AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le credenziali utente vengono autenticate con il servizio Authentication Manager. Se le credenziali utente sono valide, il flusso di lavoro procede al passaggio 3. In caso contrario, viene inviato all’utente un messaggio che indica che l’utente non è un utente autorizzato.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Le informazioni utente e la struttura di un modulo vengono recuperate da un database aziendale protetto. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le informazioni utente vengono unite alla struttura di un modulo e il modulo viene sottoposto a rendering per l’utente. </p></td>
  </tr>
 </tbody>
</table>

### Riepilogo dei passaggi {#summary_of_steps-5}

Per autenticare un utente a livello di programmazione, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client AuthenticationManagerService.
1. Richiama l’operazione di autenticazione.
1. Se necessario, recupera il contesto in modo che l’applicazione client possa inoltrarlo a un altro servizio AEM Forms per l’autenticazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client AuthenticationManagerService**

Prima di poter autenticare un utente a livello di programmazione, è necessario creare un client AuthenticationManagerService. Quando si utilizza l&#39;API Java, creare un oggetto `AuthenticationManagerServiceClient`.

**Richiama operazione di autenticazione**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di autenticazione. Per questa operazione sono necessarie informazioni sull&#39;utente, ad esempio il nome e la password dell&#39;utente. Se l’utente non si autentica, viene generata un’eccezione.

**Recupera il contesto di autenticazione**

Dopo aver autenticato l’utente, puoi creare un contesto basato sull’utente autenticato. Quindi puoi utilizzare il contenuto per richiamare un altro servizio AEM Forms. È ad esempio possibile utilizzare il contesto per creare un `EncryptionServiceClient` e crittografare un documento PDF con una password. Verificare che l&#39;utente autenticato disponga del ruolo denominato `Services User` necessario per richiamare un servizio AEM Forms.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Crittografia di documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autenticazione di un utente tramite API Java {#authenticate-a-user-using-the-java-api}

Autentica un utente tramite Authentication Manager Service API (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar, nel percorso di classe del progetto Java.

1. Creare un client AuthenticationManagerServices.

   Creare un oggetto `AuthenticationManagerServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama l’operazione di autenticazione.

   Richiama il metodo `authenticate` dell&#39;oggetto `AuthenticationManagerServiceClient` e passa i seguenti valori:

   * Oggetto `java.lang.String` contenente il nome dell&#39;utente.
   * Matrice di byte (un oggetto `byte[]`) contenente la password dell&#39;utente. È possibile ottenere l&#39;oggetto `byte[]` richiamando il metodo `getBytes` dell&#39;oggetto `java.lang.String`.

   Il metodo authenticate restituisce un oggetto `AuthResult` contenente informazioni sull&#39;utente autenticato.

1. Recupera il contesto di autenticazione.

   Richiama il metodo `getContext` dell&#39;oggetto `ServiceClientFactory`, che restituirà un oggetto `Context`.

   Quindi richiamare il metodo `initPrincipal` dell&#39;oggetto `Context` e passare `AuthResult`.

### Autenticazione di un utente tramite l’API del servizio web {#authenticate-a-user-using-the-web-service-api}

Autentica un utente tramite l’API del servizio Authentication Manager (servizio web):

1. Includi file di progetto.

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL di Authentication Manager. (Vedi [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. Vedere &quot;Riferimento all&#39;assembly client .NET&quot; in [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Creare un client AuthenticationManagerService.

   Creare un oggetto `AuthenticationManagerServiceService` utilizzando il costruttore della classe proxy.

1. Richiama l’operazione di autenticazione.

   Richiama il metodo `authenticate` dell&#39;oggetto `AuthenticationManagerServiceClient` e passa i seguenti valori:

   * Oggetto `string` contenente il nome dell&#39;utente
   * Matrice di byte (un oggetto `byte[]`) contenente la password dell&#39;utente. È possibile ottenere l&#39;oggetto `byte[]` convertendo un oggetto `string` contenente la password in un array `byte[]` utilizzando la logica illustrata nell&#39;esempio seguente.
   * Il valore restituito sarà un oggetto `AuthResult` che può essere utilizzato per recuperare informazioni sull&#39;utente. Nell&#39;esempio seguente, le informazioni dell&#39;utente vengono recuperate ottenendo prima il campo `authenticatedUser` dell&#39;oggetto `AuthResult` e successivamente i campi `canonicalName` e `domainName` dell&#39;oggetto `User` risultante.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronizzazione degli utenti a livello di programmazione {#programmatically-synchronizing-users}

Puoi sincronizzare gli utenti a livello di programmazione utilizzando l’API User Management. Quando sincronizzi gli utenti, aggiorni AEM Forms con i dati utente presenti nell’archivio utenti. Ad esempio, si supponga di aggiungere nuovi utenti all&#39;archivio utenti. Dopo aver eseguito un&#39;operazione di sincronizzazione, i nuovi utenti diventano utenti di moduli AEM. Inoltre, gli utenti che non si trovano più nel tuo archivio utenti vengono rimossi da AEM Forms.

Il diagramma seguente mostra la sincronizzazione di AEM Forms con un archivio utenti.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

Nella tabella seguente vengono descritti i passaggi del diagramma

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
   <td><p>Un’applicazione client richiede che AEM Forms esegua un’operazione di sincronizzazione.</p></td>
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

Per sincronizzare gli utenti a livello di programmazione, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client UserManagerUtilServiceClient.
1. Specificare il dominio enterprise.
1. Richiama l’operazione di autenticazione.
1. Determinare se l&#39;operazione di sincronizzazione è stata completata

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client UserManagerUtilServiceClientclient**

Prima di poter sincronizzare gli utenti a livello di programmazione, è necessario creare un oggetto `UserManagerUtilServiceClient`.

**Specificare il dominio enterprise**

Prima di eseguire un&#39;operazione di sincronizzazione utilizzando l&#39;API User Management, è necessario specificare il dominio enterprise a cui appartengono gli utenti. È possibile specificare uno o più domini enterprise. Prima di poter eseguire un&#39;operazione di sincronizzazione a livello di programmazione, è necessario impostare un dominio enterprise utilizzando la console di amministrazione. (Vedi [guida per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Richiama operazione di sincronizzazione**

Dopo aver specificato uno o più domini enterprise, è possibile eseguire l&#39;operazione di sincronizzazione. Il tempo necessario per eseguire questa operazione dipende dal numero di record utente presenti nel repository utente.

**Determinare se l&#39;operazione di sincronizzazione è stata completata**

Dopo aver eseguito un&#39;operazione di sincronizzazione a livello di programmazione, è possibile determinare se l&#39;operazione è stata completata.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva API di User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Crittografia di documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronizzazione a livello di codice degli utenti tramite API Java {#programmatically-synchronizing-users-using-the-java-api}

Sincronizzare gli utenti utilizzando l’API User Management (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-usermanager-client.jar e adobe-usermanager-util-client.jar, nel percorso di classe del progetto Java.

1. Creare un client UserManagerUtilServiceClient.

   Creare un oggetto `UserManagerUtilServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare il dominio enterprise.

   * Richiama il metodo `scheduleSynchronization` dell&#39;oggetto `UserManagerUtilServiceClient` per avviare l&#39;operazione di sincronizzazione utente.
   * Creare un&#39;istanza `java.util.Set` utilizzando un costruttore `HashSet`. Assicurarsi di specificare `String` come tipo di dati. Questa istanza di `Java.util.Set` memorizza i nomi di dominio a cui si applica l&#39;operazione di sincronizzazione.
   * Per ogni nome di dominio da aggiungere, richiamare il metodo add dell&#39;oggetto `java.util.Set` e passare il nome di dominio.

1. Richiama l’operazione di sincronizzazione.

   Richiama il metodo `getContext` dell&#39;oggetto `ServiceClientFactory`, che restituirà un oggetto `Context`.

   Quindi richiamare il metodo `initPrincipal` dell&#39;oggetto `Context` e passare `AuthResult`.

**Consulta anche**

[Sincronizzazione degli utenti a livello di programmazione](users.md#programmatically-synchronizing-users)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
