---
title: Protezione dei documenti con i criteri
seo-title: Protezione dei documenti con i criteri
description: Utilizzare il servizio Document Security per applicare dinamicamente le impostazioni di riservatezza ai documenti Adobe PDF e per mantenere il controllo sui documenti. Il servizio Document Security consente inoltre agli utenti di mantenere il controllo sul modo in cui i destinatari utilizzano il documento PDF protetto tramite criterio.
seo-description: Utilizzare il servizio Document Security per applicare dinamicamente le impostazioni di riservatezza ai documenti Adobe PDF e per mantenere il controllo sui documenti. Il servizio Document Security consente inoltre agli utenti di mantenere il controllo sul modo in cui i destinatari utilizzano il documento PDF protetto tramite criterio.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Developer (Sviluppatore)
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '15559'
ht-degree: 0%

---


# Protezione dei documenti con i criteri {#protecting-documents-with-policies}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Document Security**

Il servizio Document Security consente agli utenti di applicare dinamicamente le impostazioni di riservatezza ai documenti Adobe PDF e di mantenere il controllo sui documenti, indipendentemente dalla loro diffusione.

Il servizio Document Security impedisce che le informazioni si diffondano oltre la portata dell’utente, consentendo agli utenti di mantenere il controllo sul modo in cui i destinatari utilizzano il documento PDF protetto tramite policy. Un utente può specificare chi può aprire un documento, limitare le modalità di utilizzo e monitorare il documento dopo la sua distribuzione. Un utente può anche controllare dinamicamente l&#39;accesso a un documento protetto da policy e può anche revocare dinamicamente l&#39;accesso al documento.

Il servizio Document Security protegge anche altri tipi di file, come i file Microsoft Word (file DOC). È possibile utilizzare l&#39;API client di sicurezza dei documenti per lavorare con questi tipi di file. Sono supportate le seguenti versioni:

* File di Microsoft Office 2003 (file DOC, XLS, PPT)
* File di Microsoft Office 2007 (DOCX, XLSX, file PPTX)
* File Pro/E PTC

Per chiarezza, le due sezioni seguenti illustrano come utilizzare i documenti di Word:

* [Applicazione dei criteri ai documenti di Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Rimozione di criteri dai documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

È possibile eseguire queste operazioni utilizzando il servizio Document Security:

* Creare criteri. Per informazioni, consulta [Creazione di criteri](protecting-documents-policies.md#creating-policies).
* Modificare i criteri. Per informazioni, consulta [Modifica dei criteri](protecting-documents-policies.md#modifying-policies).
* Elimina criteri. Per informazioni, vedere [Eliminazione dei criteri](protecting-documents-policies.md#deleting-policies).
* Applicare criteri ai documenti PDF. Per informazioni, vedere [Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Rimuovere i criteri dai documenti PDF. Per informazioni, vedere [Rimozione di criteri dai documenti PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documenti protetti da policy Inspect. Per informazioni, vedere [Ispezione dei documenti PDF protetti da policy](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revoca l’accesso ai documenti PDF. Per informazioni, vedere [Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents).
* Ripristino dell&#39;accesso ai documenti revocati. Per informazioni, vedere [Ripristino dell&#39;accesso ai documenti revisionati](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Creare filigrane. Per informazioni, vedere [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).
* Cerca eventi. Per informazioni, vedere [Ricerca di eventi](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di criteri {#creating-policies}

Puoi creare criteri in modo programmatico utilizzando l’API Java per la sicurezza dei documenti o l’API del servizio Web. Una *policy* è una raccolta di informazioni che include le impostazioni di protezione dei documenti, gli utenti autorizzati e i diritti di utilizzo. Puoi creare e salvare un numero qualsiasi di criteri, utilizzando le impostazioni di sicurezza appropriate per situazioni e utenti diversi.

I criteri consentono di eseguire le attività seguenti:

* Specificare gli utenti che possono aprire il documento. I destinatari possono appartenere o essere esterni alla tua organizzazione.
* Specifica come i destinatari possono utilizzare il documento. Puoi limitare l’accesso a diverse funzioni di Acrobat e Adobe Reader. Queste funzioni includono la possibilità di stampare e copiare testo, aggiungere firme e aggiungere commenti a un documento.
* Modificare le impostazioni di accesso e protezione in qualsiasi momento, anche dopo la distribuzione del documento protetto tramite criterio.
* Monitora l&#39;utilizzo del documento dopo la distribuzione. È possibile vedere come viene utilizzato il documento e chi lo utilizza. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

### Creazione di un criterio tramite i servizi Web {#creating-a-policy-using-web-services}

Quando crei un criterio utilizzando l’API del servizio Web, fai riferimento a un file XML PDRL (Portable Document Rights Language) esistente che descrive il criterio. Le autorizzazioni dei criteri e l&#39;entità sono definite nel documento PDRL. Il seguente documento XML è un esempio di documento PDRL.

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un criterio, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Imposta gli attributi del criterio.
1. Crea una voce di criterio.
1. Registra il criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-rightsmanagement-client.jar
* namespace.jar (se AEM Forms è implementato su JBoss)
* jaxb-api.jar (se AEM Forms è implementato su JBoss)
* jaxb-impl.jar (se AEM Forms è implementato su JBoss)
* jaxb-libs.jar (se AEM Forms è implementato su JBoss)
* jaxb-xjc.jar (se AEM Forms è implementato su JBoss)
* relaxngDatype.jar (se AEM Forms è implementato su JBoss)
* xsdlib.jar (se AEM Forms è implementato su JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (usa un file JAR diverso se AEM Forms non è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client di sicurezza dei documenti**

Prima di eseguire un&#39;operazione del servizio Document Security, creare un oggetto client del servizio Document Security.

**Impostare gli attributi del criterio**

Per creare un criterio, impostare gli attributi del criterio. Un attributo obbligatorio è il nome del criterio. I nomi dei criteri devono essere univoci per ciascun set di criteri. Un set di criteri è semplicemente una raccolta di criteri. Possono essere presenti due criteri con lo stesso nome se i criteri appartengono a set di criteri separati. Tuttavia, due criteri all&#39;interno di un singolo set di criteri non possono avere lo stesso nome.

Un altro attributo utile da impostare è il periodo di validità. Un periodo di validità è il periodo di tempo durante il quale un documento protetto da policy è accessibile ai destinatari autorizzati. Se non si imposta questo attributo, il criterio è sempre valido.

Un periodo di validità può essere impostato su una delle seguenti opzioni:

* Un numero impostato di giorni in cui il documento è accessibile dal momento in cui viene pubblicato
* Data di fine dopo la quale il documento non è accessibile
* Un intervallo di date specifico per il quale il documento è accessibile
* Sempre valido

È possibile specificare solo una data di inizio, che fa sì che il criterio sia valido dopo la data di inizio. Se specifichi solo una data di fine, il criterio è valido fino alla data di fine. Tuttavia, viene generata un’eccezione se non sono definite sia una data di inizio che una data di fine.

Quando si impostano gli attributi che appartengono a un criterio, è anche possibile impostare le impostazioni di crittografia. Queste impostazioni di crittografia hanno effetto quando il criterio viene applicato a un documento. È possibile specificare i seguenti valori di crittografia:

* **AES256**: Rappresenta l’algoritmo di crittografia AES con una chiave a 256 bit.
* **AES128**: Rappresenta l’algoritmo di crittografia AES con una chiave a 128 bit.
* **NoEncryption:** non rappresenta la crittografia.

Quando si specifica l&#39;opzione `NoEncryption`, non è possibile impostare l&#39;opzione `PlaintextMetadata` su `false`. Se tenti di farlo, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per informazioni su altri attributi che è possibile impostare, consulta la descrizione dell’interfaccia `Policy` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Creare una voce di criterio**

Una voce di criterio associa entità principali, che sono gruppi e utenti, e autorizzazioni a un criterio. Un criterio deve avere almeno una voce di criterio. Si supponga, ad esempio, di eseguire le operazioni seguenti:

* Crea e registra una voce di criterio che consente a un gruppo di visualizzare un documento solo mentre è in linea e non consente ai destinatari di copiarlo.
* Allega l&#39;immissione dei criteri al criterio.
* Proteggi un documento con il criterio utilizzando Acrobat.

Queste azioni consentono ai destinatari di visualizzare il documento solo online e non di copiarlo. Il documento rimane protetto fino a quando la protezione non viene rimossa.

**Registra il criterio**

Prima di poter essere utilizzato, è necessario registrare un nuovo criterio. Dopo aver registrato un criterio, è possibile utilizzarlo per proteggere i documenti.

### Creare un criterio utilizzando l&#39;API Java {#create-a-policy-using-the-java-api}

Crea un criterio utilizzando l’API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Imposta gli attributi del criterio.

   * Creare un oggetto `Policy` richiamando il metodo statico `InfomodelObjectFactory` dell&#39;oggetto `createPolicy`. Questo metodo restituisce un oggetto `Policy`.
   * Impostare l&#39;attributo name del criterio richiamando il metodo `setName` dell&#39;oggetto `Policy` e passando un valore stringa che specifichi il nome del criterio.
   * Impostare la descrizione del criterio richiamando il metodo `setDescription` dell&#39;oggetto `Policy` e passando un valore stringa che specifichi la descrizione del criterio.
   * Impostare il criterio a cui appartiene il nuovo criterio richiamando il metodo `setPolicySetName` dell&#39;oggetto `Policy` e passando un valore stringa che specifichi il nome del set di criteri. (È possibile specificare `null` per questo valore di parametro che determina l&#39;aggiunta del criterio al set di criteri *Criteri personali*.)
   * Crea il periodo di validità del criterio richiamando il metodo statico `createValidityPeriod` dell&#39;oggetto `InfomodelObjectFactory`. Questo metodo restituisce un oggetto `ValidityPeriod`.
   * Impostare il numero di giorni per i quali un documento protetto da policy è accessibile richiamando il metodo `setRelativeExpirationDays` dell&#39;oggetto `ValidityPeriod` e passando un valore intero che specifica il numero di giorni.
   * Impostare il periodo di validità del criterio richiamando il metodo `setValidityPeriod` dell&#39;oggetto `ValidityPeriod` e passando l&#39;oggetto `Policy`.

1. Crea una voce di criterio.

   * Creare una voce di criterio richiamando il metodo statico `createPolicyEntry` dell&#39;oggetto `InfomodelObjectFactory`. Questo metodo restituisce un oggetto `PolicyEntry`.
   * Specifica le autorizzazioni del criterio richiamando il metodo statico `createPermission` dell&#39;oggetto `InfomodelObjectFactory`. Passa un membro dati statico appartenente all’interfaccia `Permission` che rappresenta l’autorizzazione. Questo metodo restituisce un oggetto `Permission`. Ad esempio, per aggiungere l&#39;autorizzazione che consente agli utenti di copiare dati da un documento PDF protetto da policy, passare `Permission.COPY`. (Ripeti questo passaggio per ogni autorizzazione da aggiungere).
   * Aggiungi l’autorizzazione alla voce del criterio richiamando il metodo `addPermission` dell’oggetto `Permission` e passando l’oggetto `PolicyEntry`. (Ripetere questo passaggio per ogni oggetto `Permission` creato).
   * Creare l&#39;entità dei criteri richiamando il metodo statico `createSpecialPrincipal` dell&#39;oggetto `InfomodelObjectFactory`. Passa un membro dati appartenente all&#39;oggetto `InfomodelObjectFactory` che rappresenta l&#39;entità. Questo metodo restituisce un oggetto `Principal`. Ad esempio, per aggiungere l&#39;editore del documento come entità principale, passare `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Aggiungi l&#39;entità alla voce del criterio richiamando il metodo `setPrincipal` dell&#39;oggetto `Principal` e passando l&#39;oggetto `PolicyEntry`.
   * Aggiungi la voce del criterio richiamando il metodo `addPolicyEntry` dell&#39;oggetto `Policy` e passando l&#39;oggetto `PolicyEntry`.

1. Registra il criterio.

   * Creare un oggetto `PolicyManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getPolicyManager`.
   * Registra il criterio richiamando il metodo `registerPolicy` dell&#39;oggetto `PolicyManager` e passando i seguenti valori:

      * L&#39;oggetto `Policy` che rappresenta il criterio da registrare.
   * Valore stringa che rappresenta il set di criteri a cui appartiene il criterio.

   Se per creare l’oggetto `DocumentSecurityClient` si utilizza un account amministratore AEM forms all’interno delle impostazioni di connessione, specificare il nome del set di criteri quando si richiama il metodo `registerPolicy`. Se trasmetti un valore `null` per il set di criteri, il criterio viene creato nel set di criteri *Criteri personali* degli amministratori.

   Se utilizzi un utente Document Security nelle impostazioni di connessione, puoi richiamare il metodo sovraccarico `registerPolicy` che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri personali*. Se non si desidera aggiungere il nuovo criterio al set di criteri, specificare un nome del set di criteri quando si richiama il metodo `registerPolicy`.

   >[!NOTE]
   >
   >Quando crei un criterio, fai riferimento a un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice che utilizzano il servizio Document Security, consulta quanto segue:

* &quot;Avvio rapido (modalità SOAP): Creazione di un criterio tramite l’API Java&quot;

### Crea un criterio utilizzando l&#39;API del servizio Web {#create-a-policy-using-the-web-service-api}

Crea un criterio utilizzando l’API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Imposta gli attributi del criterio.

   * Creare un oggetto `PolicySpec` utilizzando il relativo costruttore.
   * Imposta il nome del criterio assegnando un valore stringa al membro dati `name` dell&#39;oggetto `PolicySpec`.
   * Imposta la descrizione del criterio assegnando un valore stringa al membro dati `description` dell&#39;oggetto `PolicySpec`.
   * Impostare il criterio a cui appartiene il criterio assegnando un valore stringa al membro dati `PolicySpec` dell&#39;oggetto `policySetName`. È necessario specificare un nome di set di criteri esistente. (È possibile specificare `null` per questo valore di parametro che determina l&#39;aggiunta del criterio a *Criteri personali*.)
   * Imposta il periodo di lease offline del criterio assegnando un valore intero al membro dati `PolicySpec` dell&#39;oggetto `offlineLeasePeriod`.
   * Impostare il membro dati `policyXml` dell&#39;oggetto `PolicySpec` con un valore stringa che rappresenta i dati XML PDRL. Per eseguire questa operazione, creare un oggetto .NET `StreamReader` utilizzando il relativo costruttore. Passa la posizione di un file XML PDRL che rappresenta il criterio al costruttore `StreamReader` . Quindi, richiamare il metodo `ReadLine` dell&#39;oggetto `StreamReader` e assegnare il valore restituito a una variabile stringa. Iterare attraverso l&#39;oggetto `StreamReader` fino a quando il metodo `ReadLine` restituisce null. Assegna la variabile stringa al membro dati `policyXml` dell&#39;oggetto `PolicySpec`.

1. Crea una voce di criterio.

   Non è necessario creare una voce di criterio durante la creazione di un criterio utilizzando l&#39;API del servizio Web Document Security. La voce dei criteri è definita nel documento PDRL.

1. Registra il criterio.

   Registra il criterio richiamando il metodo `registerPolicy` dell&#39;oggetto `DocumentSecurityServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `PolicySpec` che rappresenta il criterio da registrare.
   * Valore stringa che rappresenta il set di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;aggiunta del criterio al set di criteri *MyPolices*.

   Se per creare l’oggetto `DocumentSecurityClient` si utilizza un account amministratore AEM forms all’interno delle impostazioni di connessione, specificare il nome del set di criteri quando si richiama il metodo `registerPolicy`.

   Se si utilizza un utente Document SecurityDocument Security all&#39;interno delle impostazioni di connessione, è possibile richiamare il metodo sovraccarico `registerPolicy` che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri personali*. Se non si desidera aggiungere il nuovo criterio al set di criteri, specificare un nome del set di criteri quando si richiama il metodo `registerPolicy`.

   >[!NOTE]
   >
   >Quando crei un criterio e specifichi un set di criteri, assicurati di specificare un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Creazione di un criterio tramite l’API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Creazione di un criterio tramite l’API del servizio Web&quot;

## Modifica dei criteri {#modifying-policies}

Puoi modificare un criterio esistente utilizzando l’API Java per la sicurezza dei documenti o l’API del servizio Web. Per apportare modifiche a un criterio esistente, recuperarlo, modificarlo e quindi aggiornare il criterio sul server. Ad esempio, si supponga di recuperare un criterio esistente e di estenderne il periodo di validità. Prima che la modifica abbia effetto, è necessario aggiornare il criterio.

È possibile modificare un criterio quando i requisiti aziendali cambiano e il criterio non riflette più questi requisiti. Invece di creare un nuovo criterio, puoi semplicemente aggiornare un criterio esistente.

Per modificare gli attributi dei criteri utilizzando un servizio Web (ad esempio, utilizzando le classi proxy Java create con JAX-WS), è necessario assicurarsi che il criterio sia registrato con il servizio Document Security. È quindi possibile fare riferimento al criterio esistente utilizzando il metodo `PolicySpec.getPolicyXml` e modificare gli attributi del criterio utilizzando i metodi applicabili. Ad esempio, puoi modificare il periodo di lease offline richiamando il metodo `PolicySpec.setOfflineLeasePeriod` .

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per modificare un criterio esistente, esegui i seguenti passaggi:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Recupera un criterio esistente.
1. Modificare gli attributi dei criteri.
1. Aggiorna il criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di poter eseguire un&#39;operazione Document Security Service a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un oggetto `RightsManagementClient`. Se si utilizza l&#39;API del servizio Web Document Security, creare un oggetto `RightsManagementServiceService`.

**Recupera un criterio esistente**

È necessario recuperare un criterio esistente per modificarlo. Per recuperare un criterio, specificare il nome e il set di criteri a cui appartiene il criterio. Se si specifica un valore `null` per il nome del set di criteri, il criterio viene recuperato dal set di criteri *Criteri personali*.

**Impostare gli attributi del criterio**

Per modificare un criterio, è necessario modificare il valore degli attributi del criterio. L&#39;unico attributo di criterio che non è possibile modificare è l&#39;attributo name. Ad esempio, per modificare il periodo di leasing offline del criterio, puoi modificare il valore dell’attributo del periodo di leasing offline del criterio.

Quando si modifica il periodo di lease offline di un criterio utilizzando un servizio Web, il campo `offlineLeasePeriod` nell&#39;interfaccia `PolicySpec` viene ignorato. Per aggiornare il periodo di lease offline, modifica l&#39;elemento `OfflineLeasePeriod` nel documento XML PDRL. Quindi fai riferimento al documento PDRL XML aggiornato utilizzando il membro dati `PolicySpec` dell&#39;interfaccia `policyXML`.

>[!NOTE]
>
>Per informazioni su altri attributi che è possibile impostare, consulta la descrizione dell’interfaccia `Policy` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Aggiornare il criterio**

Prima di apportare modifiche a un criterio, è necessario aggiornare il criterio con il servizio Document Security. Le modifiche ai criteri che proteggono i documenti vengono aggiornate al successivo aggiornamento del documento protetto dai criteri con il servizio Document Security.

### Modificare i criteri esistenti utilizzando l&#39;API Java {#modify-existing-policies-using-the-java-api}

Modificare un criterio esistente utilizzando l&#39;API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera un criterio esistente.

   * Creare un oggetto `PolicyManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getPolicyManager`.
   * Creare un oggetto `Policy` che rappresenta il criterio da aggiornare richiamando il metodo `PolicyManager` dell&#39;oggetto `getPolicy` e passando i seguenti valori&quot;

      * Valore stringa che rappresenta il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Valore stringa che rappresenta il nome del criterio.

1. Imposta gli attributi del criterio.

   Modifica gli attributi del criterio per soddisfare i requisiti aziendali. Ad esempio, per modificare il periodo di lease offline del criterio, richiamare il metodo `Policy` dell&#39;oggetto `setOfflineLeasePeriod`.

1. Aggiorna il criterio.

   Aggiornare il criterio richiamando il metodo `updatePolicy` dell&#39;oggetto `PolicyManager`. Passa l&#39;oggetto `Policy` che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere Avvio rapido (modalità SOAP): Modifica di un criterio tramite la sezione API Java .

### Modificare i criteri esistenti utilizzando l&#39;API del servizio Web {#modify-existing-policies-using-the-web-service-api}

Modificare un criterio esistente utilizzando l&#39;API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupera un criterio esistente.

   Creare un oggetto `PolicySpec` che rappresenta il criterio da modificare richiamando il metodo `RightsManagementServiceClient` dell&#39;oggetto `getPolicy` e passando i seguenti valori:

   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Valore stringa che specifica il nome del criterio.

1. Imposta gli attributi del criterio.

   Modifica gli attributi del criterio per soddisfare i requisiti aziendali.

1. Aggiorna il criterio.

   Aggiornare il criterio richiamando il metodo `updatePolicyFromSDK` dell&#39;oggetto `RightsManagementServiceClient` e passando l&#39;oggetto `PolicySpec` che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Modifica di un criterio tramite l’API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Modifica di un criterio tramite l’API del servizio Web&quot;

## Eliminazione dei criteri {#deleting-policies}

Puoi eliminare un criterio esistente utilizzando l’API Java per la sicurezza dei documenti o l’API del servizio Web. Una volta eliminato, un criterio non può più essere utilizzato per proteggere i documenti. Tuttavia, i documenti protetti da policy esistenti che utilizzano il criterio sono ancora protetti. È possibile eliminare un criterio quando uno più recente diventa disponibile.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per eliminare un criterio esistente, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Creare un oggetto API client Document Security.
1. Elimina il criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di poter eseguire un&#39;operazione del servizio Document Security, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un oggetto `RightsManagementClient`. Se si utilizza l&#39;API del servizio Web Document Security, creare un oggetto `RightsManagementServiceService`.

**Elimina il criterio**

Per eliminare un criterio, specificare il criterio da eliminare e il criterio impostato a cui appartiene il criterio. L’utente le cui impostazioni vengono utilizzate per richiamare AEM Forms deve disporre dell’autorizzazione per eliminare il criterio; in caso contrario si verifica un&#39;eccezione. Allo stesso modo, se tenti di eliminare un criterio che non esiste, si verifica un&#39;eccezione.

### Eliminare i criteri utilizzando l&#39;API Java {#delete-policies-using-the-java-api}

Elimina un criterio utilizzando l’API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Elimina il criterio.

   * Creare un oggetto `PolicyManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getPolicyManager`.
   * Elimina il criterio richiamando il metodo `deletePolicy` dell&#39;oggetto `PolicyManager` e passando i seguenti valori:

      * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Valore stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (modalità SOAP): Eliminazione di un criterio tramite l’API Java&quot;

### Eliminare i criteri utilizzando l&#39;API del servizio Web {#delete-policies-using-the-web-service-api}

Eliminare un criterio utilizzando l&#39;API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Elimina il criterio.

   Elimina un criterio richiamando il metodo `deletePolicy` dell&#39;oggetto `RightsManagementServiceClient` e passando i seguenti valori:

   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Valore stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Eliminazione di un criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Eliminazione di un criterio tramite l&#39;API del servizio Web&quot;

## Applicazione dei criteri ai documenti PDF {#applying-policies-to-pdf-documents}

È possibile applicare un criterio a un documento PDF per proteggere il documento. Applicando un criterio a un documento PDF, si limita l&#39;accesso al documento. Non è possibile applicare un criterio a un documento se il documento è già protetto con un criterio.

Quando il documento è aperto, è inoltre possibile limitare l’accesso alle funzioni di Acrobat e Adobe Reader, inclusa la possibilità di stampare e copiare testo, apportare modifiche e aggiungere firme e commenti a un documento. Inoltre, è possibile revocare un documento PDF protetto da policy quando si desidera che gli utenti non accedano più al documento.

È possibile monitorare l&#39;utilizzo di un documento protetto da policy dopo averlo distribuito. In altre parole, puoi vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, puoi scoprire quando qualcuno ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per applicare un criterio a un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Recupera un documento PDF a cui viene applicato un criterio.
1. Applicare un criterio esistente al documento PDF.
1. Salvare il documento PDF protetto tramite criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di eseguire un&#39;operazione del servizio Document Security, creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un oggetto `DocumentSecurityClient`. Se si utilizza l&#39;API del servizio Web Document Security, creare un oggetto `DocumentSecurityServiceService`.

**Recuperare un documento PDF**

È possibile recuperare un documento PDF per applicare un criterio. Dopo aver applicato un criterio al documento PDF, gli utenti vengono soggetti a restrizioni quando utilizzano il documento. Ad esempio, se il criterio non consente l&#39;apertura del documento in modalità non in linea, per aprire il documento gli utenti devono essere in linea.

**Applicare un criterio esistente al documento PDF**

Per applicare un criterio a un documento PDF, fare riferimento a un criterio esistente e specificare il set di criteri a cui appartiene il criterio. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verifica un&#39;eccezione.

**Salvare il documento PDF**

Dopo aver applicato un criterio a un documento PDF, è possibile salvare il documento PDF protetto da criteri come file PDF.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell’accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicare un criterio a un documento PDF utilizzando l&#39;API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Applicare un criterio a un documento PDF utilizzando l’API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Applicare un criterio esistente al documento PDF.

   * Creare un oggetto `DocumentManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getDocumentManager`.
   * Applicare un criterio al documento PDF richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentManager` e passando i seguenti valori:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF a cui viene applicato il criterio.
      * Valore stringa che specifica il nome del documento.
      * Valore stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Valore stringa che specifica il nome del criterio.
      * Valore stringa che rappresenta il nome del dominio User Manager dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro successivo deve essere nullo).
      * Valore stringa che rappresenta il nome canonico dell&#39;utente di user manager che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere `null` (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
      * Un `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni internazionali utilizzate per selezionare il modello di MS Office. Questo valore del parametro è facoltativo e non viene utilizzato per i documenti PDF. Per proteggere un documento PDF, specificare `null`.

      Il metodo `protectDocument` restituisce un oggetto `RMSecureDocumentResult` contenente il documento PDF protetto tramite criterio.


1. Salvare il documento PDF.

   * Richiamare il metodo `getProtectedDoc` dell&#39;oggetto `RMSecureDocumentResult` per ottenere il documento PDF protetto da policy. Questo metodo restituisce un oggetto `com.adobe.idp.Document`.
   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `getProtectedDoc`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (modalità EJB): Applicazione di un criterio a un documento PDF tramite l’API Java&quot;
* &quot;Avvio rapido (modalità SOAP): Applicazione di un criterio a un documento PDF tramite l’API Java&quot;

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applicare un criterio a un documento PDF utilizzando l&#39;API del servizio Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Applicare un criterio a un documento PDF utilizzando l&#39;API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupera un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF a cui viene applicato un criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la dimensione dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Applicare un criterio esistente al documento PDF.

   Applicare un criterio al documento PDF richiamando il metodo `protectDocument` dell&#39;oggetto `RightsManagementServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento PDF a cui viene applicato il criterio.
   * Valore stringa che specifica il nome del documento.
   * Valore stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Valore stringa che specifica il nome del criterio.
   * Valore stringa che rappresenta il nome del dominio User Manager dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro successivo deve essere `null`).
   * Valore stringa che rappresenta il nome canonico dell&#39;utente di user manager che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
   * Un valore `RMLocale` che specifica il valore delle impostazioni internazionali (ad esempio, `RMLocale.en`).
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore del criterio.
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto da policy.
   * Un parametro di output della stringa utilizzato per memorizzare il tipo di MIME (ad esempio, `application/pdf`).

   Il metodo `protectDocument` restituisce un oggetto `BLOB` contenente il documento PDF protetto tramite criterio.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto tramite criterio.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `protectDocument`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Applicazione di un criterio a un documento PDF tramite l’API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Applicazione di un criterio a un documento PDF tramite l’API del servizio Web&quot;

## Rimozione di criteri dai documenti PDF {#removing-policies-from-pdf-documents}

È possibile rimuovere un criterio da un documento protetto da criteri per rimuovere la protezione dal documento. In altre parole, se non si desidera più che il documento sia protetto da una politica. Se si desidera aggiornare un documento protetto da policy con un criterio più recente, invece di rimuovere il criterio e aggiungere il criterio aggiornato, è più efficiente cambiare il criterio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per rimuovere un criterio da un documento PDF protetto da policy, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Creare un oggetto API client Document Security.
1. Recuperare un documento PDF protetto da policy.
1. Rimuovere il criterio dal documento PDF.
1. Salvare il documento PDF non protetto.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di eseguire un&#39;operazione del servizio Document Security, creare un oggetto client del servizio Document Security.

**Recuperare un documento PDF protetto da policy**

È possibile recuperare un documento PDF protetto da policy per rimuovere un criterio. Se si tenta di rimuovere un criterio da un documento PDF non protetto da un criterio, verrà generata un&#39;eccezione.

**Rimuovi il criterio dal documento PDF**

È possibile rimuovere un criterio da un documento PDF protetto da criteri purché nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39;autorizzazione `SWITCH_POLICY` per rimuovere un criterio da un documento PDF. Inoltre, anche l’utente specificato nelle impostazioni di connessione di AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento PDF non protetto**

Dopo la rimozione di un criterio da un documento PDF, è possibile salvare il documento PDF non protetto come file PDF.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Rimuovere un criterio da un documento PDF utilizzando l&#39;API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Rimuovere un criterio da un documento PDF protetto da policy utilizzando l&#39;API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF protetto da policy.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF protetto da policy utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere il criterio dal documento PDF.

   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Rimuovere un criterio dal documento PDF richiamando il metodo `removeSecurity` dell&#39;oggetto `com.adobe.idp.Document` e passando l&#39;oggetto `DocumentManager` contenente il documento PDF protetto tramite criterio. Questo metodo restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeSecurity`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (modalità SOAP): Rimozione di un criterio da un documento PDF tramite l&#39;API Java&quot;

### Rimuovere un criterio utilizzando l&#39;API del servizio Web {#remove-a-policy-using-the-web-service-api}

Rimuovere un criterio da un documento PDF protetto da policy utilizzando l&#39;API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF protetto da policy.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF protetto da criteri da cui viene rimosso il criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere il criterio dal documento PDF.

   Rimuovere il criterio dal documento PDF richiamando il metodo `removePolicySecurity` dell&#39;oggetto `BLOB` e passando l&#39;oggetto `DocumentSecurityServiceClient` contenente il documento PDF protetto tramite criterio. Questo metodo restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removePolicySecurity`. Compilare l’array di byte ottenendo il valore del campo `BLOB` dell’oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Rimozione di un criterio da un documento PDF tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Rimozione di un criterio da un documento PDF tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revoca dell&#39;accesso ai documenti {#revoking-access-to-documents}

È possibile revocare l&#39;accesso a un documento PDF protetto da policy in modo che tutte le copie del documento risultino inaccessibili agli utenti. Quando un utente tenta di aprire un documento PDF revocato, viene reindirizzato a un URL specifico in cui è possibile visualizzare un documento rivisto. L’URL a cui l’utente viene reindirizzato deve essere specificato a livello di programmazione. Quando si revoca l&#39;accesso a un documento, la modifica ha effetto alla successiva sincronizzazione dell&#39;utente con il servizio Document Security aprendo il documento protetto tramite criterio online.

La possibilità di revocare l’accesso a un documento offre ulteriore protezione. Ad esempio, si supponga che sia disponibile una versione più recente di un documento e che non si desideri più che qualcuno visualizzi la versione obsoleta. In questa situazione, l&#39;accesso al documento precedente può essere revocato e nessuno può visualizzare il documento a meno che l&#39;accesso non venga ripristinato.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per revocare un documento protetto da policy, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Recuperare un documento PDF protetto da policy.
1. Revocare il documento protetto da policy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di poter eseguire un&#39;operazione del servizio Document Security, è necessario creare un oggetto client del servizio Document Security.

**Recuperare un documento PDF protetto da policy**

Per revocarlo, è necessario recuperare un documento PDF protetto da policy. Impossibile revocare un documento già revocato o non protetto da policy.

Se si conosce il valore dell&#39;identificatore di licenza del documento protetto tramite criterio, non è necessario recuperare il documento PDF protetto tramite criterio. Tuttavia, nella maggior parte dei casi, per ottenere il valore dell’identificatore di licenza è necessario recuperare il documento PDF.

**Revoca del documento protetto da policy**

Per revocare un documento protetto da policy, specificare l&#39;identificativo della licenza del documento protetto da policy. Inoltre, è possibile specificare l&#39;URL di un documento che l&#39;utente può visualizzare quando tenta di aprire il documento revocato. In altre parole, supponiamo che un documento obsoleto venga revocato. Quando un utente tenta di aprire il documento revocato, vedrà un documento aggiornato invece del documento revocato.

>[!NOTE]
>
>Se si tenta di revocare un documento già revocato, viene generata un&#39;eccezione.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Ripristino dell&#39;accesso ai documenti revisionati](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revoca l’accesso ai documenti utilizzando l’API Java {#revoke-access-to-documents-using-the-java-api}

Revoca l’accesso a un documento PDF protetto da policy utilizzando l’API Document Security (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di sicurezza dei documenti

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF protetto da policy

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF protetto da policy utilizzando il relativo costruttore e passando un valore di stringa che specifichi la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Revoca del documento protetto da policy

   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Recupera il valore dell&#39;identificatore di licenza del documento protetto dai criteri richiamando il metodo `DocumentManager` dell&#39;oggetto `getLicenseId`. Passa l&#39;oggetto `com.adobe.idp.Document` che rappresenta il documento protetto da policy. Questo metodo restituisce un valore stringa che rappresenta il valore dell&#39;identificatore di licenza.
   * Creare un oggetto `LicenseManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getLicenseManager`.
   * Revocare il documento protetto dai criteri richiamando il metodo `revokeLicense` dell&#39;oggetto `LicenseManager` e passando i seguenti valori:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite criterio (specificare il valore restituito del metodo `DocumentManager` dell&#39;oggetto `getLicenseId`).
      * Membro di dati statico dell&#39;interfaccia `License` che specifica il motivo della revoca del documento. Ad esempio, puoi specificare `License.DOCUMENT_REVISED`.
      * Valore `java.net.URL` che specifica la posizione in cui si trova un documento revisionato. Se non desideri reindirizzare un utente a un altro URL, puoi passare `null`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (modalità SOAP): Revoca di un documento tramite l’API Java&quot;

### Revoca l&#39;accesso ai documenti tramite l&#39;API del servizio Web {#revoke-access-to-documents-using-the-web-service-api}

Revoca l’accesso a un documento PDF protetto da policy utilizzando l’API per la sicurezza dei documenti (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di sicurezza dei documenti

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF protetto da policy

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF protetto da policy che viene revocato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto dai criteri da revocare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Revoca del documento protetto da policy

   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto dai criteri richiamando il metodo `getLicenseID` dell&#39;oggetto `DocumentSecurityServiceClient` e passando l&#39;oggetto `BLOB` che rappresenta il documento protetto dai criteri. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore di licenza.
   * Revocare il documento protetto dai criteri richiamando il metodo `revokeLicense` dell&#39;oggetto `DocumentSecurityServiceClient` e passando i seguenti valori:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite criterio (specificare il valore restituito del metodo `DocumentSecurityServiceService` dell&#39;oggetto `getLicenseId`).
      * Membro di dati statico dell&#39; enum `Reason` che specifica il motivo della revoca del documento. Ad esempio, puoi specificare `Reason.DOCUMENT_REVISED`.
      * Valore `string` che specifica la posizione dell&#39;URL in cui si trova un documento revisionato. Se non desideri reindirizzare un utente a un altro URL, puoi passare `null`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Revoca di un documento tramite l’API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Revoca di un documento tramite l’API del servizio Web&quot;

**Consulta anche**

[Rimozione di criteri dai documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ripristino dell&#39;accesso ai documenti revisionati {#reinstating-access-to-revoked-documents}

È possibile ripristinare l’accesso a un documento PDF revocato, in modo che tutte le copie del documento revocato siano accessibili agli utenti. Quando un utente apre un documento ripristinato revocato, può visualizzare il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per ripristinare l’accesso a un documento PDF revocato, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.
1. Ripristina l&#39;accesso al documento PDF revocato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di poter eseguire un&#39;operazione del servizio Document Security, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un oggetto `DocumentSecurityClient`. Se si utilizza l&#39;API del servizio Web Document Security, creare un oggetto `DocumentSecurityServiceService`.

**Recupera l&#39;identificatore di licenza del documento PDF revocato**

Per ripristinare un documento PDF revocato, è necessario recuperare l’identificatore di licenza del documento PDF revocato. Dopo aver ottenuto il valore dell&#39;identificatore di licenza, è possibile ripristinare un documento revocato. Se si tenta di ripristinare un documento non revocato, verrà generata un&#39;eccezione.

**Ripristino dell’accesso al documento PDF revocato**

Per ripristinare l’accesso a un documento PDF revocato, è necessario specificare l’identificatore di licenza del documento revocato. Se si tenta di ripristinare l&#39;accesso a un documento PDF non revocato, verrà generata un&#39;eccezione.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revoca dell’accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Ripristina l&#39;accesso ai documenti revocati utilizzando l&#39;API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Ripristina l’accesso a un documento revocato utilizzando l’API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF revocato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.
   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo `getLicenseId` dell&#39;oggetto `DocumentManager` e passando l&#39;oggetto `com.adobe.idp.Document` che rappresenta il documento revocato. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore di licenza.

1. Ripristina l&#39;accesso al documento PDF revocato.

   * Creare un oggetto `LicenseManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getLicenseManager`.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo `unrevokeLicense` dell&#39;oggetto `LicenseManager` e passando il valore dell&#39;identificatore di licenza del documento revocato.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (modalità SOAP): Ripristino dell’accesso a un documento revocato tramite l’API del servizio Web&quot;

### Ripristino dell&#39;accesso ai documenti revocati tramite l&#39;API del servizio Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Ripristino dell&#39;accesso a un documento revocato tramite l&#39;API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF revocato al quale viene ripristinato l&#39;accesso.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF revocato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Ripristina l&#39;accesso al documento PDF revocato.

   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo `getLicenseID` dell&#39;oggetto `DocumentSecurityServiceClient` e passando l&#39;oggetto `BLOB` che rappresenta il documento revocato. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore di licenza.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo `unrevokeLicense` dell&#39;oggetto `DocumentSecurityServiceClient` e passando un valore di stringa che specifica il valore dell&#39;identificatore di licenza del documento PDF revocato (passare il valore restituito del metodo `DocumentSecurityServiceClient` dell&#39;oggetto `getLicenseId`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Ripristino dell’accesso a un documento revocato tramite l’API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ripristino dell’accesso a un documento revocato tramite l’API del servizio Web&quot;

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ispezione dei documenti PDF protetti da policy {#inspecting-policy-protected-pdf-documents}

È possibile utilizzare l&#39;API del servizio Document Security (Java e il servizio Web) per ispezionare i documenti PDF protetti da policy. L&#39;ispezione dei documenti PDF protetti da policy restituisce informazioni sul documento PDF protetto da policy. Ad esempio, è possibile determinare il criterio utilizzato per proteggere il documento e la data in cui il documento è stato protetto.

Non è possibile eseguire questa operazione se la versione di LiveCycle in uso è 8.x o una versione precedente. In AEM Forms viene aggiunto il supporto per l’ispezione di documenti protetti da policy. Se si tenta di esaminare un documento protetto da policy utilizzando il LiveCycle 8.x (o versione precedente), viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per esaminare un documento PDF protetto da policy, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Recuperare un documento protetto da policy da esaminare.
1. Ottenere informazioni sul documento protetto tramite criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di eseguire un&#39;operazione del servizio Document Security, creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un oggetto `RightsManagementClient`. Se si utilizza l&#39;API del servizio Web Document Security, creare un oggetto `RightsManagementServiceService`.

**Recuperare un documento protetto da policy per ispezionare**

Per esaminare un documento protetto da policy, recuperarlo. Se si tenta di controllare un documento non protetto con un criterio o revocato, viene generata un&#39;eccezione.

**Inspect il documento**

Dopo aver recuperato un documento protetto da policy, è possibile esaminarlo.

**Ottenere informazioni sul documento protetto tramite policy**

Dopo aver esaminato un documento PDF protetto da policy, è possibile ottenere informazioni su di esso. Ad esempio, è possibile determinare il criterio utilizzato per proteggere il documento.

Se si protegge un documento con un criterio che appartiene ai Criteri personali e quindi si chiama `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, viene restituito null.

Se il documento è protetto utilizzando un criterio contenuto in un set di criteri (diverso da Criteri personali), `RMInspectResult.getPolicysetName` e `RMInspectResult.getPolicysetId` restituiscono stringhe valide.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documenti PDF protetti da policy Inspect utilizzando l&#39;API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect è un documento PDF protetto da policy utilizzando l’API del servizio Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, consulta [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento protetto da policy da esaminare.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF protetto da policy utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Inspect il documento.

   * Creare un oggetto `DocumentManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getDocumentManager`.
   * Inspect è il documento protetto da policy richiamando il metodo `LicenseManager` dell&#39;oggetto `inspectDocument`. Passa l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF protetto da policy. Questo metodo restituisce un oggetto `RMInspectResult` contenente informazioni sul documento protetto tramite criterio.

1. Ottenere informazioni sul documento protetto tramite criterio.

   Per ottenere informazioni sul documento protetto tramite criterio, richiamare il metodo appropriato che appartiene all&#39;oggetto `RMInspectResult`. Ad esempio, per recuperare il nome del criterio, richiamare il metodo `RMInspectResult` dell&#39;oggetto `getPolicyName`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (modalità SOAP): Ispezione dei documenti PDF protetti da policy tramite l&#39;API Java&quot;

### Documenti PDF protetti da policy Inspect utilizzando l&#39;API del servizio Web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect è un documento PDF protetto da policy utilizzando l&#39;API del servizio Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento protetto da policy da esaminare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF da esaminare.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Inspect il documento.

   Inspect è il documento protetto da policy richiamando il metodo `RightsManagementServiceClient` dell&#39;oggetto `inspectDocument`. Passa l&#39;oggetto `BLOB` che contiene il documento PDF protetto da policy. Questo metodo restituisce un oggetto `RMInspectResult` contenente informazioni sul documento protetto tramite criterio.

1. Ottenere informazioni sul documento protetto tramite criterio.

   Per ottenere informazioni sul documento protetto tramite criterio, ottenere il valore del campo appropriato che appartiene all&#39;oggetto `RMInspectResult`. Ad esempio, per recuperare il nome del criterio, ottenere il valore del campo `RMInspectResult` dell’oggetto `policyName`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Ispezione dei documenti PDF protetti da policy utilizzando l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ispezione dei documenti PDF protetti da policy utilizzando l&#39;API del servizio Web&quot;

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di filigrane {#creating-watermarks}

Le filigrane consentono di garantire la sicurezza di un documento identificando in modo univoco il documento e controllando la violazione del copyright. Ad esempio, è possibile creare e posizionare una filigrana che indichi Riservato in tutte le pagine di un documento. Una volta creata una filigrana, puoi includerla come parte di un criterio. In altre parole, puoi impostare l’attributo della filigrana del criterio con la filigrana appena creata. Dopo che un criterio contenente una filigrana viene applicato a un documento, la filigrana viene visualizzata nel documento protetto tramite criterio.

>[!NOTE]
>
>Solo gli utenti con privilegi amministrativi di Document Security possono creare filigrane. In altre parole, è necessario specificare tale utente quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per creare una filigrana, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Impostare gli attributi delle filigrane.
1. Registrare la filigrana con il servizio Document Security.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di poter eseguire un&#39;operazione del servizio Document Security, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un oggetto `RightsManagementClient`. Se si utilizza l&#39;API del servizio Web Document Security, creare un oggetto `RightsManagementServiceService`.

**Impostare gli attributi delle filigrane**

Per creare una nuova filigrana, è necessario impostare gli attributi della filigrana. L&#39;attributo name deve sempre essere definito. Oltre all&#39;attributo name, è necessario impostare almeno uno dei seguenti attributi:

* Testo personalizzato
* DateIncluded
* IDutenteIncluso
* NomeUtenteIncluso

Nella tabella seguente sono elencate le coppie chiave-valore richieste per la creazione di una filigrana utilizzando i servizi Web.

<table>
 <thead>
  <tr>
   <th><p>Nome chiave</p></th>
   <th><p>Descrizione</p></th>
   <th><p>Valore</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>Specifica se il nome utente dell'utente che apre il documento fa parte della filigrana.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Specifica se l'identificazione dell'utente che apre il documento fa parte della filigrana.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Specifica se la data corrente fa parte della filigrana.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Se questo valore è true, è necessario specificare il valore del testo personalizzato utilizzando <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Specifica l'opacità della filigrana. Il valore predefinito è 0,5 se non è specificato.</p></td>
   <td><p>Un valore compreso tra 0,0 e 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Specifica la rotazione della filigrana. Il valore predefinito è 0 gradi.</p></td>
   <td><p>Un valore compreso tra 0 e 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Se si specifica questo valore, <code>WaterBackCmd:IS_SIZE_ENABLED</code> deve essere presente e il valore deve essere true. Se questo attributo non viene specificato, il comportamento predefinito è adattato alla pagina.</p></td>
   <td><p>Un valore maggiore di 0.0 e inferiore o uguale a 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Specifica l’allineamento orizzontale della filigrana. Il valore predefinito è center.</p></td>
   <td><p>a sinistra, al centro o a destra</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Specifica l’allineamento verticale della filigrana. Il valore predefinito è center.</p></td>
   <td><p>superiore, centrale o inferiore</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Specifica se la filigrana è di sfondo. Il valore predefinito è false.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True se è specificata una scala personalizzata. Se questo valore è true, è necessario specificare anche SCALE . Se questo valore è false, il valore predefinito è fit to page.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Specifica il testo personalizzato per una filigrana. Se questo valore è presente, anche <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> deve essere presente e impostato su true.</p></td>
   <td><p>True o False</p></td>
  </tr>
 </tbody>
</table>

Tutte le filigrane devono avere uno dei seguenti attributi definiti:

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Tutti gli altri attributi sono facoltativi.

**Registra la filigrana**

Prima di poter essere utilizzato, è necessario registrare una nuova filigrana con il servizio Document Security. Dopo aver registrato una filigrana, puoi utilizzarla all’interno dei criteri.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creare watermark utilizzando l&#39;API Java {#create-watermarks-using-the-java-api}

Crea una filigrana utilizzando l’API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, ad esempio `adobe-rightsmanagement-client.jar`, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare gli attributi della filigrana

   * Creare un oggetto `Watermark` richiamando il metodo statico `InfomodelObjectFactory` dell&#39;oggetto `createWatermark`. Questo metodo restituisce un oggetto `Watermark`.
   * Impostare l&#39;attributo del nome della filigrana richiamando il metodo `setName` dell&#39;oggetto `Watermark` e passando un valore di stringa che specifichi il nome del criterio.
   * Imposta l’attributo di sfondo della filigrana richiamando il metodo `setBackground` dell’oggetto `true` e passando `Watermark`. Impostando questo attributo, la filigrana viene visualizzata sullo sfondo del documento.
   * Imposta l’attributo di testo personalizzato della filigrana richiamando il metodo `setCustomText` dell’oggetto `Watermark` e passando un valore di stringa che rappresenta il testo della filigrana.
   * Impostare l&#39;attributo di opacità della filigrana richiamando il metodo `setOpacity` dell&#39;oggetto `Watermark` e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che la filigrana è completamente trasparente.

1. Registra la filigrana.

   * Creare un oggetto `WatermarkManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getWatermarkManager`. Questo metodo restituisce un oggetto `WatermarkManager`.
   * Registrare la filigrana richiamando il metodo `registerWatermark` dell&#39;oggetto `WatermarkManager` e passando l&#39;oggetto `Watermark` che rappresenta la filigrana da registrare. Questo metodo restituisce un valore di stringa che rappresenta il valore di identificazione della filigrana.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (modalità SOAP): Creazione di una filigrana utilizzando l’API Java&quot;

### Creare watermark utilizzando l&#39;API del servizio Web {#create-watermarks-using-the-web-service-api}

Crea una filigrana utilizzando l’API Document Security (servizio Web):

1. Creare un oggetto API client Document Security.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Impostare gli attributi della filigrana.

   * Creare un oggetto `WatermarkSpec` richiamando il costruttore `WatermarkSpec`.
   * Impostare il nome della filigrana assegnando un valore stringa al membro dati `WatermarkSpec` dell&#39;oggetto `name`.
   * Imposta l’attributo `id` della filigrana assegnando un valore stringa al membro dati `WatermarkSpec` dell’oggetto `id`.
   * Per ogni proprietà watermark da impostare, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` separato.
   * Impostare il valore chiave assegnando un valore al membro dati `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` (ad esempio, `WaterBackCmd:OPACITY)`).
   * Impostare il valore assegnando un valore al membro dati `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` (ad esempio, `.25`).
   * Creare un oggetto `MyArrayOf_xsd_anyType`. Per ciascun oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, richiamare il metodo `MyArrayOf_xsd_anyType` dell&#39;oggetto `Add`. Passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Assegna l&#39;oggetto `MyArrayOf_xsd_anyType` al membro dati `WatermarkSpec` dell&#39;oggetto `values`.

1. Registra la filigrana.

   Registrare la filigrana richiamando il metodo `registerWatermark` dell&#39;oggetto `RightsManagementServiceClient` e passando l&#39;oggetto `WatermarkSpec` che rappresenta la filigrana da registrare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Creazione di una filigrana utilizzando l’API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Creazione di una filigrana utilizzando l’API del servizio Web&quot;

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica delle filigrane {#modifying-watermarks}

Puoi modificare una filigrana esistente utilizzando l’API Java per la sicurezza dei documenti o l’API del servizio Web. Per apportare modifiche a una filigrana esistente, recuperarla, modificarne gli attributi e quindi aggiornarla sul server. Ad esempio, si supponga di recuperare una filigrana e di modificarne l’attributo di opacità. Prima che la modifica abbia effetto, è necessario aggiornare la filigrana.

Quando si modifica una filigrana, la modifica ha effetto sui documenti futuri a cui viene applicata la filigrana. In altre parole, i documenti PDF esistenti che contengono la filigrana non sono interessati.

>[!NOTE]
>
>Solo gli utenti con privilegi amministrativi di Document Security possono modificare i watermark. In altre parole, è necessario specificare tale utente quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-9}

Per modificare una filigrana, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Recupera la filigrana da modificare.
1. Impostare gli attributi delle filigrane.
1. Aggiorna la filigrana.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di poter eseguire un&#39;operazione del servizio Document Security, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un oggetto `DocumentSecurityClient`. Se si utilizza l&#39;API del servizio Web Document Security, creare un oggetto `DocumentSecurityServiceService`.

**Recupera la filigrana da modificare**

Per modificare una filigrana, è necessario recuperare una filigrana esistente. È possibile recuperare una filigrana specificandone il nome o specificandone il valore di identificazione.

**Impostare gli attributi delle filigrane**

Per modificare una filigrana esistente, modificare il valore di uno o più attributi di filigrana. Quando aggiorni in modo programmatico una filigrana utilizzando un servizio Web, è necessario impostare tutti gli attributi originariamente impostati, anche se il valore non cambia. Ad esempio, si supponga di aver impostato i seguenti attributi di filigrana: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` e `WaterBackCmd:SRCTEXT`. Anche se l&#39;unico attributo che si desidera modificare è `WaterBackCmd:OPACITY`, è necessario impostare gli altri valori.

>[!NOTE]
>
>Quando utilizzi l’API Java per modificare una filigrana, non devi specificare tutti gli attributi. Impostare l&#39;attributo della filigrana che si desidera modificare.

>[!NOTE]
>
>Per informazioni sui nomi degli attributi della filigrana, consulta [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).

**Aggiorna la filigrana**

Dopo aver modificato gli attributi di una filigrana, è necessario aggiornare la filigrana.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Creazione di filigrane](protecting-documents-policies.md#creating-watermarks)

### Modificare i watermark utilizzando l&#39;API Java {#modify-watermarks-using-the-java-api}

Modificare una filigrana utilizzando l’API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera la filigrana da modificare.

   Creare un oggetto `WatermarkManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getWatermarkManager` e passare un valore stringa che specifichi il nome della filigrana. Questo metodo restituisce un oggetto `Watermark` che rappresenta la filigrana da modificare.

1. Impostare gli attributi della filigrana.

   Impostare l&#39;attributo di opacità della filigrana richiamando il metodo `setOpacity` dell&#39;oggetto `Watermark` e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che la filigrana è completamente trasparente.

   >[!NOTE]
   >
   >In questo esempio viene modificato solo l&#39;attributo opacity.

1. Aggiorna la filigrana.

   * Aggiornare la filigrana richiamando il metodo `updateWatermark` dell&#39;oggetto `Watermark` e passare l&#39;oggetto `WatermarkManager` il cui attributo è stato modificato.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere Avvio rapido (modalità SOAP): Modifica di una filigrana utilizzando la sezione Java API .

### Modificare i watermark utilizzando l&#39;API del servizio Web {#modify-watermarks-using-the-web-service-api}

Modificare una filigrana utilizzando l&#39;API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupera la filigrana da modificare.

   Recupera la filigrana da modificare richiamando il metodo `getWatermarkByName` dell’oggetto `DocumentSecurityServiceClient`. Passa un valore stringa che specifica il nome della filigrana. Questo metodo restituisce un oggetto `WatermarkSpec` che rappresenta la filigrana da modificare.

1. Impostare gli attributi della filigrana.

   * Per ogni proprietà di filigrana da aggiornare, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` separato.
   * Impostare il valore chiave assegnando un valore al membro dati `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` (ad esempio, `WaterBackCmd:OPACITY)`).
   * Impostare il valore assegnando un valore al membro dati `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` (ad esempio, `.50`).
   * Creare un oggetto `MyArrayOf_xsd_anyType`. Per ciascun oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, richiamare il metodo `MyArrayOf_xsd_anyType` dell&#39;oggetto `Add`. Passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Assegna l&#39;oggetto `MyArrayOf_xsd_anyType` al membro dati `WatermarkSpec` dell&#39;oggetto `values`.

1. Aggiorna la filigrana.

   Aggiornare la filigrana richiamando il metodo `updateWatermark` dell’oggetto `WatermarkSpec` e passando l’oggetto `DocumentSecurityServiceClient` che rappresenta la filigrana da modificare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere la seguente Guida rapida:

* &quot;Avvio rapido (MTOM): Modifica di una filigrana utilizzando l’API del servizio Web&quot;

## Ricerca di eventi {#searching-for-events}

Il servizio di Rights Management tiene traccia delle azioni specifiche che si verificano, ad esempio l&#39;applicazione di un criterio a un documento, l&#39;apertura di un documento protetto da policy e la revoca dell&#39;accesso ai documenti. Il controllo degli eventi deve essere abilitato per il servizio di Rights Management, altrimenti gli eventi non vengono tracciati.

Gli eventi rientrano in una delle seguenti categorie:

* Gli eventi di amministratore sono azioni correlate a un amministratore, ad esempio la creazione di un nuovo account di amministratore.
* Gli eventi del documento sono azioni correlate a un documento, ad esempio la chiusura di un documento protetto da policy.
* Gli eventi dei criteri sono azioni correlate a un criterio, ad esempio la creazione di un nuovo criterio.
* Gli eventi di servizio sono azioni relative al servizio di Rights Management, ad esempio la sincronizzazione con la directory utente.

Puoi cercare eventi specifici utilizzando l’API Java di Rights Management o l’API del servizio Web. Cercando gli eventi, è possibile eseguire attività quali la creazione di un file di registro di determinati eventi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Rights Management, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-10}

Per cercare un evento di Rights Management, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client Rights Management.
1. Specifica l’evento per il quale eseguire la ricerca.
1. Cerca l’evento.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Rights Management**

Prima di poter eseguire un&#39;operazione di servizio di Rights Management a livello di programmazione, è necessario creare un oggetto client di servizio di Rights Management. Se utilizzi l’API Java, crea un oggetto `DocumentSecurityClient`. Se utilizzi l’API del servizio Web di Rights Management, crea un oggetto `DocumentSecurityServiceService` .

**Specifica gli eventi da cercare**

È necessario specificare l’evento da cercare. Ad esempio, è possibile cercare l&#39;evento di creazione del criterio, che si verifica quando viene creato un nuovo criterio.

**Cerca l’evento**

Dopo aver specificato l’evento da cercare, puoi utilizzare l’API Java di Rights Management o l’API del servizio Web di Rights Management per cercare l’evento.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cercare eventi utilizzando l&#39;API Java {#search-for-events-using-the-java-api}

Cerca eventi utilizzando l’API di Rights Management (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Rights Management

   Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Specifica gli eventi da cercare

   * Creare un oggetto `EventManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getEventManager`. Questo metodo restituisce un oggetto `EventManager`.
   * Creare un oggetto `EventSearchFilter` richiamando il relativo costruttore.
   * Specificare l&#39;evento per il quale eseguire la ricerca richiamando il metodo `setEventCode` dell&#39;oggetto `EventSearchFilter` e passando un membro di dati statico appartenente alla classe `EventManager` che rappresenta l&#39;evento per il quale eseguire la ricerca. Ad esempio, per cercare l&#39;evento di creazione dei criteri, passa `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >È possibile definire criteri di ricerca aggiuntivi richiamando i metodi dell&#39;oggetto `EventSearchFilter` . Ad esempio, richiamare il metodo `setUserName` per specificare un utente associato all&#39;evento.

1. Cerca l’evento

   Ricercare l’evento richiamando il metodo `searchForEvents` dell’oggetto `EventManager` e passando l’oggetto `EventSearchFilter` che definisce i criteri di ricerca dell’evento. Questo metodo restituisce una matrice di oggetti `Event`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio di Rights Management, consulta i seguenti Quick Starts:

* &quot;Avvio rapido (SOAP): Ricerca di eventi utilizzando l’API Java&quot;

### Cercare eventi utilizzando l&#39;API del servizio Web {#search-for-events-using-the-web-service-api}

Cerca eventi utilizzando l’API di Rights Management (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Rights Management

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Specifica gli eventi da cercare

   * Creare un oggetto `EventSpec` utilizzando il relativo costruttore.
   * Specifica l&#39;inizio del periodo di tempo durante il quale si è verificato l&#39;evento impostando il membro dati `firstTime.date` dell&#39;oggetto `EventSpec` con l&#39;istanza `DataTime` che rappresenta l&#39;inizio dell&#39;intervallo di date in cui si è verificato l&#39;evento.
   * Assegna il valore `true` al membro dati `EventSpec` dell&#39;oggetto `firstTime.dateSpecified`.
   * Specifica la fine del periodo di tempo durante il quale si è verificato l’evento impostando il membro dati `lastTime.date` dell’oggetto `DataTime` con l’istanza `EventSpec` che rappresenta la fine dell’intervallo di date in cui si è verificato l’evento.
   * Assegna il valore `true` al membro dati `EventSpec` dell&#39;oggetto `lastTime.dateSpecified`.
   * Impostare l&#39;evento da cercare assegnando un valore stringa al membro dati `eventCode` dell&#39;oggetto `EventSpec`. Nella tabella seguente sono elencati i valori numerici che è possibile assegnare a questa proprietà:

   <table>
    <thead>
    <tr>
    <th><p>Tipo evento</p></th>
    <th><p>Valore</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. Cerca l’evento

   Ricercare l’evento richiamando il metodo `searchForEvents` dell’oggetto `DocumentSecurityServiceClient` e passando l’oggetto `EventSpec` che rappresenta l’evento da cercare e il numero massimo di risultati. Questo metodo restituisce un insieme `MyArrayOf_xsd_anyType` in cui ogni elemento è un&#39;istanza `AuditSpec`. Utilizzando un&#39;istanza `AuditSpec`, puoi ottenere informazioni sull&#39;evento, ad esempio l&#39;ora in cui si è verificato. L&#39;istanza `AuditSpec` contiene un membro dati `timestamp` che specifica queste informazioni.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio di Rights Management, consulta i seguenti Quick Starts:

* &quot;Avvio rapido (MTOM): Ricerca di eventi tramite l’API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ricerca di eventi tramite l’API del servizio Web&quot;

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Applicazione dei criteri ai documenti di Word {#applying-policies-to-word-documents}

Oltre ai documenti PDF, il servizio di gestione dei diritti supporta formati di documenti aggiuntivi, come un documento Microsoft Word (file DOC) e altri formati di file Microsoft Office. Ad esempio, è possibile applicare un criterio a un documento Word per proteggerlo. Applicando un criterio a un documento Word, si limita l&#39;accesso al documento. Non è possibile applicare un criterio a un documento se il documento è già protetto con un criterio.

È possibile monitorare l&#39;utilizzo di un documento Word protetto da policy dopo averlo distribuito. In altre parole, puoi vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, puoi scoprire quando qualcuno ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-11}

Per applicare un criterio a un documento Word, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Document Security.
1. Recuperare un documento Word a cui viene applicato un criterio.
1. Applicare un criterio esistente al documento Word.
1. Salvare il documento Word protetto da policy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security, è necessario creare un oggetto client del servizio Document Security.

**Recupera un documento di Word**

È necessario recuperare un documento di Word per applicare un criterio. Dopo aver applicato un criterio al documento Word, gli utenti vengono limitati quando utilizzano il documento. Ad esempio, se il criterio non consente l&#39;apertura del documento in modalità non in linea, per aprire il documento gli utenti devono essere in linea.

**Applicare un criterio esistente al documento Word**

Per applicare un criterio a un documento di Word, è necessario fare riferimento a un criterio esistente e specificare il set di criteri a cui appartiene il criterio. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verifica un&#39;eccezione.

**Salva il documento Word**

Dopo aver applicato un criterio a un documento di Word, è possibile salvare il documento Word protetto da policy come file DOC.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell’accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicare un criterio a un documento Word utilizzando l&#39;API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Applicare un criterio a un documento Word utilizzando l&#39;API Document Security (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento Word.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento Word utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento Word.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Applicare un criterio esistente al documento Word.

   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Applicare un criterio al documento Word richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentManager` e passando i seguenti valori:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento Word a cui viene applicato il criterio.
      * Valore stringa che specifica il nome del documento.
      * Valore stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Valore stringa che specifica il nome del criterio.
      * Valore stringa che rappresenta il nome del dominio User Manager dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro successivo deve essere nullo).
      * Valore stringa che rappresenta il nome canonico dell&#39;utente di user manager che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere `null` (se questo parametro è `null`, il valore del parametro precedente deve essere `null`).
      * Un `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni internazionali utilizzate per selezionare il modello di MS Office. Questo valore del parametro è facoltativo ed è possibile specificare `null`.

      Il metodo `protectDocument` restituisce un oggetto `RMSecureDocumentResult` contenente il documento Word protetto da policy.


1. Salvare il documento Word.

   * Richiamare il metodo `getProtectedDoc` dell&#39;oggetto `RMSecureDocumentResult` per ottenere il documento Word protetto da policy. Questo metodo restituisce un oggetto `com.adobe.idp.Document`.
   * Crea un oggetto `java.io.File` e assicurati che l’estensione del file sia DOC.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `getProtectedDoc`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere la seguente Guida rapida:

* &quot;Avvio rapido (modalità SOAP): Applicazione di un criterio a un documento Word utilizzando l&#39;API Java&quot;

### Applicare un criterio a un documento Word utilizzando l&#39;API del servizio Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Applicare un criterio a un documento Word utilizzando l&#39;API Document Security (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento Word.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento Word a cui viene applicato un criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la dimensione dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Applicare un criterio esistente al documento Word.

   Applicare un criterio al documento Word richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentSecurityServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento Word a cui viene applicato il criterio.
   * Valore stringa che specifica il nome del documento.
   * Valore stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Valore stringa che specifica il nome del criterio.
   * Valore stringa che rappresenta il nome del dominio User Manager dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro successivo deve essere `null`).
   * Valore stringa che rappresenta il nome canonico dell&#39;utente di user manager che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
   * Un valore `RMLocale` che specifica il valore delle impostazioni internazionali (ad esempio, `RMLocale.en`).
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore del criterio.
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto da policy.
   * Un parametro di output della stringa utilizzato per memorizzare il tipo di MIME (ad esempio, `application/doc`).

   Il metodo `protectDocument` restituisce un oggetto `BLOB` contenente il documento Word protetto da policy.

1. Salvare il documento Word.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word protetto dai criteri.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `protectDocument`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file Word richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere la seguente Guida rapida:

* &quot;Avvio rapido (MTOM): Applicazione di un criterio a un documento Word tramite l&#39;API del servizio Web&quot;

## Rimozione di criteri dai documenti di Word {#removing-policies-from-word-documents}

È possibile rimuovere un criterio da un documento Word protetto da criteri per rimuovere la protezione dal documento. In altre parole, se non si desidera più che il documento sia protetto da una politica. Se si desidera aggiornare un documento Word protetto da policy con un criterio più recente, invece di rimuovere il criterio e aggiungere il criterio aggiornato, è più efficiente cambiare il criterio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-12}

Per rimuovere un criterio da un documento Word protetto da policy, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Creare un oggetto API client Document Security.
1. Recuperare un documento Word protetto da policy.
1. Rimuovere il criterio dal documento Word.
1. Salvare i documenti Word non protetti

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client di sicurezza dei documenti**

Prima di eseguire un&#39;operazione del servizio Document Security, creare un oggetto client del servizio Document Security.

**Recuperare un documento Word protetto da policy**

Per rimuovere un criterio, è necessario recuperare un documento Word protetto da policy. Se si tenta di rimuovere un criterio da un documento di Word non protetto da un criterio, verrà generata un&#39;eccezione.

**Rimuovi il criterio dal documento Word**

È possibile rimuovere un criterio da un documento Word protetto da criteri purché nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39;autorizzazione `SWITCH_POLICY` per rimuovere un criterio da un documento di Word. Inoltre, anche l’utente specificato nelle impostazioni di connessione di AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento Word non protetto**

Dopo che il servizio Document Security rimuove un criterio da un documento Word, è possibile salvare il documento Word non protetto come file DOC.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti di Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Rimuovere un criterio da un documento Word utilizzando l&#39;API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Rimuovere un criterio da un documento Word protetto da policy utilizzando l&#39;API Document Security (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di sicurezza dei documenti

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento Word protetto da policy

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento Word protetto da policy utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento Word.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi il criterio dal documento Word

   * Creare un oggetto `DocumentManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getDocumentManager`.
   * Rimuovere un criterio dal documento Word richiamando il metodo `removeSecurity` dell&#39;oggetto `DocumentManager` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento Word protetto da policy. Questo metodo restituisce un oggetto `com.adobe.idp.Document` contenente un documento Word non protetto.

1. Salvare il documento Word non protetto

   * Crea un oggetto `java.io.File` e assicurati che l’estensione del file sia DOC.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeSecurity`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere la seguente Guida rapida:

* &quot;Avvio rapido (modalità SOAP): Rimozione di un criterio da un documento Word utilizzando l&#39;API Java&quot;

### Rimuovere un criterio da un documento Word utilizzando l&#39;API del servizio Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Rimuovere un criterio da un documento Word protetto da policy utilizzando l&#39;API Document Security (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di sicurezza dei documenti

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento Word protetto da policy

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento Word protetto dai criteri da cui viene rimosso il criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovi il criterio dal documento Word

   Rimuovere il criterio dal documento Word richiamando il metodo `removePolicySecurity` dell&#39;oggetto `RightsManagementServiceClient` e passando l&#39;oggetto `BLOB` che contiene il documento Word protetto dal criterio. Questo metodo restituisce un oggetto `BLOB` contenente un documento Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word non protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removePolicySecurity`. Compilare l’array di byte ottenendo il valore del campo `BLOB` dell’oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, vedere la seguente Guida rapida:

* &quot;Avvio rapido (MTOM): Rimozione di un criterio da un documento Word utilizzando l&#39;API del servizio Web&quot;

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
