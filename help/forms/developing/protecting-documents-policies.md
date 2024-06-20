---
title: Protezione di documenti con criteri
description: Utilizza il servizio Document Security per applicare dinamicamente le impostazioni di riservatezza ai documenti di Adobe PDF e mantenere il controllo su di essi. Il servizio Document Security consente inoltre agli utenti di mantenere il controllo sul modo in cui i destinatari utilizzano il documento PDF protetto tramite policy.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '15394'
ht-degree: 0%

---

# Protezione di documenti con criteri {#protecting-documents-with-policies}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

**Informazioni sul servizio Document Security**

Il servizio Document Security consente agli utenti di applicare dinamicamente le impostazioni di riservatezza ai documenti di Adobe PDF e di mantenere il controllo su di essi, indipendentemente dalla loro diffusione.

Il servizio Document Security impedisce la diffusione di informazioni al di fuori della portata dell’utente, consentendo agli utenti di mantenere il controllo sul modo in cui i destinatari utilizzano il documento PDF protetto tramite policy. Un utente può specificare chi può aprire un documento, limitare le modalità di utilizzo e monitorare il documento dopo la distribuzione. Un utente può inoltre controllare in modo dinamico l’accesso a un documento protetto tramite policy e può persino revocare in modo dinamico l’accesso al documento.

Il servizio Document Security protegge anche altri tipi di file, come i file Word di Microsoft (file DOC). Per utilizzare questi tipi di file è possibile utilizzare l’API client di Document Security. Sono supportate le seguenti versioni:

* File di Microsoft Office 2003 (file DOC, XLS, PPT)
* File di Microsoft Office 2007 (file DOCX, XLSX, PPTX)
* File PTC Pro/E

Per maggiore chiarezza, nelle due sezioni seguenti viene illustrato come utilizzare i documenti di Word:

* [Applicazione di criteri ai documenti di Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Rimozione di criteri da documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Puoi eseguire queste attività utilizzando il servizio Document Security:

* Creare criteri. Per informazioni, consulta [Creazione di criteri](protecting-documents-policies.md#creating-policies).
* Modificare i criteri. Per informazioni, consulta [Modifica dei criteri](protecting-documents-policies.md#modifying-policies).
* Elimina criteri. Per informazioni, consulta [Eliminazione dei criteri](protecting-documents-policies.md#deleting-policies).
* Applicare policy ai documenti PDF. Per informazioni, consulta [Applicazione delle policy ai documenti di PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Rimuovere i criteri dai documenti di PDF. Per informazioni, consulta [Rimozione di criteri dai documenti di PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documenti protetti tramite policy di Inspect. Per informazioni, consulta [Verifica dei documenti di PDF protetti tramite policy](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revoca dell&#39;accesso ai documenti di PDF. Per informazioni, consulta [Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents).
* Ripristinare l&#39;accesso ai documenti revocati. Per informazioni, consulta [Ripristino dell’accesso ai documenti revocati](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Creare filigrane. Per informazioni, consulta [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).
* Cerca gli eventi. Per informazioni, consulta [Ricerca di eventi](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di criteri {#creating-policies}

Puoi creare policy a livello di programmazione utilizzando l’API Java di Document Security o l’API di servizio web. A *policy* è una raccolta di informazioni che includono impostazioni di protezione dei documenti, utenti autorizzati e diritti di utilizzo. È possibile creare e salvare un numero qualsiasi di criteri, utilizzando le impostazioni di protezione appropriate per situazioni e utenti diversi.

I criteri consentono di eseguire le seguenti attività:

* Specificare gli utenti autorizzati ad aprire il documento. I destinatari possono appartenere o essere esterni alla tua organizzazione.
* Specificare come i destinatari possono utilizzare il documento. Puoi limitare l’accesso a diverse funzioni di Acrobat e Adobe Reader. Queste funzionalità includono la possibilità di stampare e copiare testo, aggiungere firme e aggiungere commenti a un documento.
* Modificare le impostazioni di accesso e protezione in qualsiasi momento, anche dopo la distribuzione del documento protetto tramite policy.
* Monitorare l&#39;utilizzo del documento dopo averlo distribuito. È possibile vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

### Creazione di una policy tramite servizi web {#creating-a-policy-using-web-services}

Quando si crea una policy utilizzando l’API del servizio Web, fare riferimento a un file XML Portable Document Rights Language (PDRL) esistente che descrive la policy. Le autorizzazioni dei criteri e l&#39;entità principale sono definite nel documento PDRL. Il seguente documento XML è un esempio di documento PDRL.

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un criterio, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Impostare gli attributi del criterio.
1. Crea una voce criterio.
1. Registra il criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-rightsmanagement-client.jar
* namespace.jar (se AEM Forms è distribuito su JBoss)
* jaxb-api.jar (se AEM Forms è distribuito su JBoss)
* jaxb-impl.jar (se AEM Forms è distribuito su JBoss)
* jaxb-libs.jar (se AEM Forms è distribuito su JBoss)
* jaxb-xjc.jar (se AEM Forms è distribuito su JBoss)
* relaxDatatype.jar (se AEM Forms è distribuito su JBoss)
* xsdlib.jar (se AEM Forms è distribuito su JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilizza un file JAR diverso se AEM Forms non è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security.

**Impostare gli attributi del criterio**

Per creare un criterio, impostare gli attributi del criterio. Un attributo obbligatorio è il nome del criterio. I nomi dei criteri devono essere univoci per ogni set di criteri. Un set di criteri è semplicemente una raccolta di criteri. Se i criteri appartengono a set di criteri separati, è possibile che siano presenti due criteri con lo stesso nome. Tuttavia, due criteri all&#39;interno di un singolo set di criteri non possono avere lo stesso nome.

Un altro attributo utile da impostare è il periodo di validità. Un periodo di validità è il periodo di tempo durante il quale un documento protetto tramite policy è accessibile ai destinatari autorizzati. Se non si imposta questo attributo, il criterio è sempre valido.

Un periodo di validità può essere impostato su una delle seguenti opzioni:

* Un numero di giorni impostato per l&#39;accesso al documento dal momento in cui il documento viene pubblicato
* Data di fine dopo la quale il documento non è accessibile
* Un intervallo di date specifico per il quale il documento è accessibile
* Sempre valido

È possibile specificare solo una data di inizio, che determina la validità del criterio dopo la data di inizio. Se specifichi solo una data di fine, il criterio è valido fino alla data di fine. Tuttavia, viene generata un’eccezione se non sono definite sia una data di inizio che una data di fine.

Quando si impostano gli attributi che appartengono a un criterio, è inoltre possibile impostare le impostazioni di crittografia. Queste impostazioni di crittografia hanno effetto quando la policy viene applicata a un documento. È possibile specificare i seguenti valori di crittografia:

* **AES256**: rappresenta l’algoritmo di crittografia AES con una chiave a 256 bit.
* **AES128**: rappresenta l’algoritmo di crittografia AES con una chiave a 128 bit.
* **Nessuna crittografia:** Non rappresenta alcuna crittografia.

Quando si specifica `NoEncryption` , non è possibile impostare `PlaintextMetadata` opzione per `false`. Se tenti di farlo, viene generata un’eccezione.

>[!NOTE]
>
>Per informazioni sugli altri attributi che è possibile impostare, vedere `Policy` descrizione dell’interfaccia in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Creare una voce criterio**

Una voce criterio consente di associare entità, ovvero gruppi e utenti, e autorizzazioni a un criterio. Un criterio deve avere almeno una voce di criterio. Si supponga, ad esempio, di eseguire i task riportati di seguito.

* Creare e registrare una voce di criterio che consente a un gruppo di visualizzare un documento solo mentre è online e impedisce ai destinatari di copiarlo.
* Allega la voce del criterio al criterio.
* Proteggi un documento con la policy utilizzando Acrobat.

Di conseguenza, i destinatari possono solo visualizzare il documento online e non possono copiarlo. Il documento rimane protetto finché non viene rimossa la protezione.

**Registra la policy**

È necessario registrare un nuovo criterio prima di poterlo utilizzare. Dopo aver registrato una policy, è possibile utilizzarla per proteggere i documenti.

### Creare un criterio utilizzando l’API Java {#create-a-policy-using-the-java-api}

Crea una policy utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocumentSecurityClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Impostare gli attributi del criterio.

   * Creare un `Policy` oggetto richiamando il `InfomodelObjectFactory` statico dell&#39;oggetto `createPolicy` metodo. Questo metodo restituisce un `Policy` oggetto.
   * Impostare l&#39;attributo name del criterio richiamando `Policy` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome del criterio.
   * Impostare la descrizione del criterio richiamando `Policy` dell&#39;oggetto `setDescription` e passando un valore stringa che specifica la descrizione del criterio.
   * Specificare il set di criteri a cui appartiene il nuovo criterio richiamando `Policy` dell&#39;oggetto `setPolicySetName` e passando un valore stringa che specifica il nome del set di criteri. (È possibile specificare `null` per questo valore di parametro che determina l’aggiunta del criterio a *I Miei Criteri* set di criteri.)
   * Creare il periodo di validità del criterio richiamando `InfomodelObjectFactory` statico dell&#39;oggetto `createValidityPeriod` metodo. Questo metodo restituisce un `ValidityPeriod` oggetto.
   * Impostare il numero di giorni per i quali un documento protetto tramite policy è accessibile richiamando `ValidityPeriod` dell&#39;oggetto `setRelativeExpirationDays` e viene passato un valore intero che specifica il numero di giorni.
   * Impostare il periodo di validità del criterio richiamando `Policy` dell&#39;oggetto `setValidityPeriod` e passando il `ValidityPeriod` oggetto.

1. Crea una voce criterio.

   * Creare una voce di criterio richiamando `InfomodelObjectFactory` statico dell&#39;oggetto `createPolicyEntry` metodo. Questo metodo restituisce un `PolicyEntry` oggetto.
   * Specificare le autorizzazioni del criterio richiamando `InfomodelObjectFactory` statico dell&#39;oggetto `createPermission` metodo. Trasmettere un membro dati statico che appartiene al `Permission` interfaccia che rappresenta l’autorizzazione. Questo metodo restituisce un `Permission` oggetto. Ad esempio, per aggiungere l’autorizzazione che consente agli utenti di copiare i dati da un documento PDF protetto tramite policy, passa `Permission.COPY`. (Ripeti questo passaggio per ogni autorizzazione da aggiungere).
   * Aggiungere l’autorizzazione alla voce del criterio richiamando `PolicyEntry` dell&#39;oggetto `addPermission` e passando il `Permission` oggetto. (Ripeti questo passaggio per ogni `Permission` oggetto creato).
   * Creare l’entità criterio richiamando `InfomodelObjectFactory` statico dell&#39;oggetto `createSpecialPrincipal` metodo. Trasmettere un membro dati che appartiene al `InfomodelObjectFactory` oggetto che rappresenta l&#39;entità principale. Questo metodo restituisce un `Principal` oggetto. Ad esempio, per aggiungere l&#39;editore del documento come entità principale, passare `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Aggiungere l&#39;entità alla voce del criterio richiamando `PolicyEntry` dell&#39;oggetto `setPrincipal`e passando il `Principal` oggetto.
   * Aggiungere la voce del criterio richiamando `Policy` dell&#39;oggetto `addPolicyEntry` e passando il `PolicyEntry` oggetto.

1. Registra il criterio.

   * Creare un `PolicyManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getPolicyManager` metodo.
   * Registra il criterio richiamando `PolicyManager` dell&#39;oggetto `registerPolicy` e fornendo i seguenti valori:

      * Il `Policy` oggetto che rappresenta il criterio da registrare.

   * Valore stringa che rappresenta il set di criteri a cui appartiene il criterio.

   Se si utilizza un account amministratore di AEM forms nelle impostazioni di connessione per creare `DocumentSecurityClient` , quindi specificare il nome del set di criteri quando si richiama `registerPolicy` metodo. Se si supera un `null` per il set di criteri, il criterio viene creato negli amministratori *I Miei Criteri* set di criteri.

   Se utilizzi un utente di Document Security nelle impostazioni di connessione, puoi richiamare l’utente sovraccaricato `registerPolicy` metodo che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *I Miei Criteri*. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome per il set di criteri quando si richiama `registerPolicy` metodo.

   >[!NOTE]
   >
   >Quando crei un criterio, fai riferimento a un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice con il servizio Document Security, consulta:

* &quot;Guida rapida (modalità SOAP): creazione di una policy tramite API Java&quot;

### Creare un criterio utilizzando l’API del servizio web {#create-a-policy-using-the-web-service-api}

Crea una policy utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `DocumentSecurityServiceClient` utilizzando il costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Impostare gli attributi del criterio.

   * Creare un `PolicySpec` mediante il costruttore.
   * Impostare il nome del criterio assegnando un valore stringa al `PolicySpec` dell&#39;oggetto `name` membro dati.
   * Impostare la descrizione del criterio assegnando un valore stringa al `PolicySpec` dell&#39;oggetto `description` membro dati.
   * Specificare il set di criteri a cui appartiene il criterio assegnando un valore stringa al `PolicySpec` dell&#39;oggetto `policySetName` membro dati. Specificare un nome di set di criteri esistente. (È possibile specificare `null` per questo valore di parametro che determina l’aggiunta del criterio a *I Miei Criteri*.)
   * Impostare il periodo di lease non in linea del criterio assegnando un valore intero al `PolicySpec` dell&#39;oggetto `offlineLeasePeriod` membro dati.
   * Imposta il `PolicySpec` dell&#39;oggetto `policyXml` membro dati con un valore stringa che rappresenta i dati XML PDRL. Per eseguire questa operazione, creare una .NET `StreamReader` mediante il costruttore. Passa la posizione di un file XML PDRL che rappresenta il criterio a `StreamReader` costruttore. Quindi, richiama `StreamReader` dell&#39;oggetto `ReadLine` e assegna il valore restituito a una variabile stringa. Effettua iterazione attraverso `StreamReader` oggetto fino al `ReadLine` il metodo restituisce null. Assegna la variabile stringa a `PolicySpec` dell&#39;oggetto `policyXml` membro dati.

1. Crea una voce criterio.

   Non è necessario creare una voce policy durante la creazione di una policy utilizzando l’API del servizio web di Document Security. La voce del criterio è definita nel documento PDRL.

1. Registra il criterio.

   Registra il criterio richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `registerPolicy` e fornendo i seguenti valori:

   * Il `PolicySpec` oggetto che rappresenta il criterio da registrare.
   * Valore stringa che rappresenta il set di criteri a cui appartiene il criterio. È possibile specificare un `null` valore che determina l’aggiunta del criterio al *MyPolicy* set di criteri.

   Se si utilizza un account amministratore di AEM forms nelle impostazioni di connessione per creare `DocumentSecurityClient` oggetto, specificare il nome del set di criteri quando si richiama `registerPolicy` metodo.

   Se utilizzi un utente di Document Security nelle impostazioni di connessione, puoi richiamare l’utente sovraccaricato `registerPolicy` metodo che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *I Miei Criteri*. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome per il set di criteri quando si richiama `registerPolicy` metodo.

   >[!NOTE]
   >
   >Quando crei un criterio e specifichi un set di criteri, accertati di specificare un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): creazione di un criterio utilizzando l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): creazione di un criterio utilizzando l’API del servizio web&quot;

## Modifica dei criteri {#modifying-policies}

Puoi modificare una policy esistente utilizzando l’API Java di Document Security o l’API di servizio web. Per modificare un criterio esistente, recuperarlo, modificarlo e quindi aggiornare il criterio sul server. Si supponga, ad esempio, di recuperare un criterio esistente e di estenderne il periodo di validità. Prima che la modifica entri in vigore, devi aggiornare il criterio.

È possibile modificare un criterio quando cambiano i requisiti aziendali e il criterio non riflette più questi requisiti. Invece di creare un criterio, puoi semplicemente aggiornare un criterio esistente.

Per modificare gli attributi dei criteri utilizzando un servizio web (ad esempio, utilizzando le classi proxy Java create con JAX-WS), è necessario assicurarsi che i criteri siano registrati nel servizio Document Security. È quindi possibile fare riferimento al criterio esistente utilizzando `PolicySpec.getPolicyXml` e modificare gli attributi dei criteri utilizzando i metodi applicabili. Ad esempio, puoi modificare il periodo di lease offline richiamando il `PolicySpec.setOfflineLeasePeriod` metodo.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per modificare un criterio esistente, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recupera un criterio esistente.
1. Modificare gli attributi dei criteri.
1. Aggiorna il criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione Document Security Service a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un’ `RightsManagementClient` oggetto. Se utilizzi l’API del servizio web Document Security, crea un’ `RightsManagementServiceService` oggetto.

**Recuperare un criterio esistente**

Recuperare un criterio esistente per modificarlo. Per recuperare un criterio, specificare il nome del criterio e il set di criteri a cui appartiene il criterio. Se si specifica un `null` per il nome del set di criteri, il criterio viene recuperato dal *I Miei Criteri* set di criteri.

**Impostare gli attributi del criterio**

Per modificare un criterio, è necessario modificare il valore degli attributi del criterio. L’unico attributo del criterio che non può essere modificato è l’attributo name. Ad esempio, per modificare il periodo di lease offline del criterio, è possibile modificare il valore dell&#39;attributo del periodo di lease offline del criterio.

Quando si modifica il periodo di lease offline di un criterio utilizzando un servizio web, il `offlineLeasePeriod` campo sul `PolicySpec` viene ignorata. Per aggiornare il periodo di lease offline, modifica `OfflineLeasePeriod` nel documento PDRL XML. Quindi, fare riferimento al documento XML PDRL aggiornato utilizzando `PolicySpec` dell&#39;interfaccia `policyXML` membro dati.

>[!NOTE]
>
>Per informazioni sugli altri attributi che è possibile impostare, vedere `Policy` descrizione dell’interfaccia in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Aggiornare il criterio**

Prima di poter applicare le modifiche apportate a una policy, è necessario aggiornarla con il servizio Document Security. Le modifiche alle policy che proteggono i documenti vengono aggiornate alla successiva sincronizzazione del documento protetto con il servizio Document Security.

### Modificare i criteri esistenti utilizzando l’API Java {#modify-existing-policies-using-the-java-api}

Modifica una policy esistente utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `RightsManagementClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recupera un criterio esistente.

   * Creare un `PolicyManager` oggetto richiamando il `RightsManagementClient` dell&#39;oggetto `getPolicyManager` metodo.
   * Creare un `Policy` oggetto che rappresenta il criterio da aggiornare richiamando `PolicyManager` dell&#39;oggetto `getPolicy` e fornendo i seguenti valori&quot;

      * Valore stringa che rappresenta il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che comporta la `MyPolicies` set di criteri in uso.
      * Valore stringa che rappresenta il nome del criterio.

1. Impostare gli attributi del criterio.

   Modifica gli attributi della policy per soddisfare i requisiti aziendali. Ad esempio, per modificare il periodo di lease offline del criterio, richiama `Policy` dell&#39;oggetto `setOfflineLeasePeriod` metodo.

1. Aggiorna il criterio.

   Aggiorna il criterio richiamando `PolicyManager` dell&#39;oggetto `updatePolicy` metodo. Passa il `Policy` oggetto che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Guida rapida (modalità SOAP): modificare una policy utilizzando l’API Java.

### Modificare i criteri esistenti utilizzando l’API del servizio web {#modify-existing-policies-using-the-web-service-api}

Modifica una policy esistente utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `RightsManagementServiceClient` utilizzando il costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera un criterio esistente.

   Creare un `PolicySpec` oggetto che rappresenta il criterio da modificare richiamando `RightsManagementServiceClient` dell&#39;oggetto `getPolicy` e fornendo i seguenti valori:

   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che comporta la `MyPolicies` set di criteri in uso.
   * Valore stringa che specifica il nome del criterio.

1. Impostare gli attributi del criterio.

   Modifica gli attributi della policy per soddisfare i requisiti aziendali.

1. Aggiorna il criterio.

   Aggiorna il criterio richiamando `RightsManagementServiceClient` dell&#39;oggetto `updatePolicyFromSDK` e passando il `PolicySpec` oggetto che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): modifica di un criterio tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): modifica di un criterio tramite l’API del servizio web&quot;

## Eliminazione dei criteri {#deleting-policies}

Puoi eliminare una policy esistente utilizzando l’API Java di Document Security o l’API di servizio web. Una volta eliminata, una policy non può più essere utilizzata per proteggere i documenti. Tuttavia, i documenti protetti tramite policy esistenti che utilizzano la policy sono ancora protetti. È possibile eliminare un criterio quando ne diventa disponibile uno più recente.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per eliminare un criterio esistente, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Crea un oggetto API client di Document Security.
1. Elimina il criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un’ `RightsManagementClient` oggetto. Se utilizzi l’API del servizio web Document Security, crea un’ `RightsManagementServiceService` oggetto.

**Elimina il criterio**

Per eliminare un criterio, specificare il criterio da eliminare e il set di criteri a cui appartiene il criterio. L’utente le cui impostazioni vengono utilizzate per richiamare AEM Forms deve disporre dell’autorizzazione per eliminare il criterio; in caso contrario, si verifica un’eccezione. Analogamente, se si tenta di eliminare un criterio inesistente, si verifica un&#39;eccezione.

### Eliminare i criteri utilizzando l’API Java {#delete-policies-using-the-java-api}

Elimina una policy utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `RightsManagementClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Elimina il criterio.

   * Creare un `PolicyManager` oggetto richiamando il `RightsManagementClient` dell&#39;oggetto `getPolicyManager` metodo.
   * Elimina il criterio richiamando `PolicyManager` dell&#39;oggetto `deletePolicy` e fornendo i seguenti valori:

      * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che comporta la `MyPolicies` set di criteri in uso.
      * Valore stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): eliminazione di un criterio utilizzando l’API Java&quot;

### Eliminare i criteri utilizzando l’API del servizio web {#delete-policies-using-the-web-service-api}

Elimina una policy utilizzando l’API di Document Security (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `RightsManagementServiceClient` utilizzando il costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Elimina il criterio.

   Eliminare un criterio richiamando `RightsManagementServiceClient` dell&#39;oggetto `deletePolicy` e fornendo i seguenti valori:

   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che comporta la `MyPolicies` set di criteri in uso.
   * Valore stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): eliminazione di un criterio tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): eliminazione di un criterio tramite l’API del servizio web&quot;

## Applicazione delle policy ai documenti di PDF {#applying-policies-to-pdf-documents}

È possibile applicare una policy a un documento PDF per proteggere il documento. Applicando una policy a un documento PDF, si limita l’accesso al documento. Non è possibile applicare una policy a un documento se il documento è già protetto con una policy.

Quando il documento è aperto, è inoltre possibile limitare l&#39;accesso alle funzioni di Acrobat e Adobe Reader, inclusa la possibilità di stampare e copiare testo, apportare modifiche e aggiungere firme e commenti a un documento. Inoltre, è possibile revocare un documento PDF protetto tramite policy quando non si desidera più che gli utenti accedano al documento.

È possibile monitorare l’utilizzo di un documento protetto tramite policy dopo averlo distribuito. In altre parole, è possibile vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile scoprire quando qualcuno ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per applicare una policy a un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperare un documento PDF a cui è applicato un criterio.
1. Applica una policy esistente al documento PDF.
1. Salva il documento PDF protetto tramite policy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un’ `DocumentSecurityClient` oggetto. Se utilizzi l’API del servizio web Document Security, crea un’ `DocumentSecurityServiceService` oggetto.

**Recuperare un documento PDF**

È possibile recuperare un documento PDF per applicare una policy. Dopo aver applicato una policy al documento PDF, gli utenti vengono limitati quando utilizzano il documento. Se, ad esempio, la policy non consente l&#39;apertura del documento in modalità non in linea, gli utenti devono essere in linea per aprire il documento.

**Applicare una policy esistente al documento PDF**

Per applicare una policy a un documento PDF, fai riferimento a una policy esistente e specifica a quale set di policy appartiene la policy. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verificherà un&#39;eccezione.

**Salva il documento PDF**

Dopo che il servizio Document Security ha applicato una policy a un documento PDF PDF, puoi salvarlo come file PDF.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicare una policy a un documento PDF utilizzando l’API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Applica una policy a un documento PDF utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `RightsManagementClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Applica una policy esistente al documento PDF.

   * Creare un `DocumentManager` oggetto richiamando il `RightsManagementClient` dell&#39;oggetto `getDocumentManager` metodo.
   * Applicare una policy al documento PDF richiamando `DocumentManager` dell&#39;oggetto `protectDocument` e fornendo i seguenti valori:

      * Il `com.adobe.idp.Document` oggetto che contiene il documento PDF a cui viene applicato il criterio.
      * Valore stringa che specifica il nome del documento.
      * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un `null` valore che risulta in `MyPolicies` set di criteri in uso.
      * Valore stringa che specifica il nome del criterio.
      * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere null).
      * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere `null` (se questo parametro è null, il valore del parametro precedente deve essere `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta la lingua utilizzata per selezionare il modello di MS Office. Questo valore di parametro è facoltativo e non viene utilizzato per i documenti PDF. Per proteggere un documento PDF, specifica `null`.

     Il `protectDocument` il metodo restituisce un `RMSecureDocumentResult` oggetto contenente il documento PDF protetto tramite policy.

1. Salvare il documento PDF.

   * Richiama `RMSecureDocumentResult` dell&#39;oggetto `getProtectedDoc` metodo per ottenere il documento PDF protetto tramite policy. Questo metodo restituisce un `com.adobe.idp.Document` oggetto.
   * Creare un `java.io.File` e accertati che l’estensione del file sia PDF.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file (assicurati di utilizzare il `Document` oggetto restituito da `getProtectedDoc` metodo).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità EJB): applicazione di una policy a un documento PDF tramite l’API Java&quot;
* &quot;Guida rapida (modalità SOAP): applicazione di una policy a un documento PDF tramite l’API Java&quot;

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applicare una policy a un documento PDF utilizzando l’API del servizio web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Applicare una policy a un documento PDF utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `RightsManagementServiceClient` utilizzando il costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF a cui viene applicato un criterio.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. Determinare la dimensione dell&#39;array di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Applica una policy esistente al documento PDF.

   Applicare una policy al documento PDF richiamando `RightsManagementServiceClient` dell&#39;oggetto `protectDocument` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che contiene il documento PDF a cui viene applicato il criterio.
   * Valore stringa che specifica il nome del documento.
   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un `null` valore che risulta in `MyPolicies` set di criteri in uso.
   * Valore stringa che specifica il nome del criterio.
   * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere `null`).
   * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro precedente deve essere `null`).
   * A `RMLocale` valore che specifica il valore locale (ad esempio, `RMLocale.en`).
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore dei criteri.
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite policy.
   * Un parametro di output stringa utilizzato per memorizzare il tipo mime (ad esempio, `application/pdf`).

   Il `protectDocument` il metodo restituisce un `BLOB` oggetto contenente il documento PDF protetto tramite policy.

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto tramite policy.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `protectDocument` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): applicazione di una policy a un documento PDF tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): applicazione di una policy a un documento PDF tramite l’API del servizio web&quot;

## Rimozione di criteri dai documenti di PDF {#removing-policies-from-pdf-documents}

È possibile rimuovere una policy da un documento protetto tramite policy per rimuovere la protezione dal documento. In altre parole, se non desideri più che il documento sia protetto da una policy. Se si desidera aggiornare un documento protetto tramite policy con una policy più recente, invece di rimuovere la policy e aggiungere la policy aggiornata, è più efficiente cambiare la policy.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per rimuovere una policy da un documento PDF protetto tramite policy, attenersi alla seguente procedura:

1. Includi file di progetto
1. Crea un oggetto API client di Document Security.
1. Recuperare un documento PDF protetto tramite policy.
1. Rimuovi il criterio dal documento PDF.
1. Salvare il documento PDF non protetto.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security.

**Recuperare un documento PDF protetto tramite policy**

Per rimuovere una policy, è possibile recuperare un documento PDF protetto tramite policy. Se tenti di rimuovere una policy da un documento PDF non protetto da una policy, viene generata un’eccezione.

**Rimuovi il criterio dal documento PDF**

È possibile rimuovere una policy da un documento PDF protetto tramite policy a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere `SWITCH_POLICY` autorizzazione a rimuovere una policy da un documento PDF. Inoltre, anche l’utente specificato nelle impostazioni di connessione di AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salva il documento PDF non protetto**

Dopo che il servizio Document Security ha rimosso una policy da un documento PDF, puoi salvare il documento PDF non protetto come file PDF.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione delle policy ai documenti di PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Rimuovere una policy da un documento PDF utilizzando l’API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Rimuovi una policy da un documento PDF protetto tramite policy utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocumentSecurityClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF protetto tramite policy.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF protetto tramite policy utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Rimuovi il criterio dal documento PDF.

   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager` metodo.
   * Rimuovere una policy dal documento PDF richiamando `DocumentManager` dell&#39;oggetto `removeSecurity` e passando il `com.adobe.idp.Document` oggetto contenente il documento PDF protetto tramite policy. Questo metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un `java.io.File` e accertati che l’estensione del file sia PDF.
   * Richiama `Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file (assicurati di utilizzare il `Document` oggetto restituito da `removeSecurity` metodo).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): rimozione di una policy da un documento PDF tramite l’API Java&quot;

### Rimuovere un criterio utilizzando l’API del servizio web {#remove-a-policy-using-the-web-service-api}

Rimuovi una policy da un documento PDF protetto tramite policy utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `DocumentSecurityServiceClient` utilizzando il costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF protetto tramite policy.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento PDF protetto tramite policy da cui viene rimossa la policy.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Rimuovi il criterio dal documento PDF.

   Rimuovere la policy dal documento PDF richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `removePolicySecurity` e passando il `BLOB` oggetto contenente il documento PDF protetto tramite policy. Questo metodo restituisce un `BLOB` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `removePolicySecurity` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` campo.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): rimozione di una policy da un documento PDF tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): rimozione di una policy da un documento PDF tramite l’API del servizio web&quot;

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revoca dell&#39;accesso ai documenti {#revoking-access-to-documents}

È possibile revocare l’accesso a un documento di PDF protetto tramite policy in modo che tutte le copie del documento siano inaccessibili agli utenti. Quando un utente cerca di aprire un documento PDF revocato, viene reindirizzato a un URL specificato in cui è possibile visualizzare un documento revisionato. L&#39;URL a cui l&#39;utente viene reindirizzato deve essere specificato a livello di programmazione. Quando revochi l’accesso a un documento, la modifica entra in vigore alla successiva sincronizzazione dell’utente con il servizio Document Security, quando il documento protetto tramite policy viene aperto online.

La possibilità di revocare l&#39;accesso a un documento offre una protezione aggiuntiva. Si supponga, ad esempio, che sia disponibile una versione più recente di un documento e che non si desideri più visualizzare la versione obsoleta. In questo caso, è possibile revocare l&#39;accesso al documento precedente e non è possibile visualizzare il documento a meno che non venga ripristinato l&#39;accesso.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per revocare un documento protetto tramite policy, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperare un documento PDF protetto tramite policy.
1. Revoca del documento protetto tramite policy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security.

**Recuperare un documento PDF protetto tramite policy**

Recupera un documento PDF protetto tramite policy per revocarlo. Non è possibile revocare un documento già revocato o non protetto tramite policy.

Se si conosce il valore dell&#39;identificatore di licenza del documento protetto tramite policy, non è necessario recuperare il documento PDF protetto tramite policy. Tuttavia, nella maggior parte dei casi è necessario recuperare il documento PDF per ottenere il valore dell&#39;identificatore della licenza.

**Revoca del documento protetto tramite policy**

Per revocare un documento protetto tramite policy, specifica l’identificatore di licenza del documento protetto tramite policy. È inoltre possibile specificare l&#39;URL di un documento che l&#39;utente può visualizzare quando tenta di aprire il documento revocato. In altre parole, si supponga che un documento non aggiornato venga revocato. Quando un utente cerca di aprire il documento revocato, visualizza un documento aggiornato invece del documento revocato.

>[!NOTE]
>
>Se si tenta di revocare un documento già revocato, viene generata un&#39;eccezione.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione delle policy ai documenti di PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Ripristino dell’accesso ai documenti revocati](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revocare l’accesso ai documenti utilizzando l’API Java {#revoke-access-to-documents-using-the-java-api}

Revoca dell’accesso a un documento PDF protetto tramite policy utilizzando Document Security API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Document Security

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocumentSecurityClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF protetto tramite policy

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF protetto tramite policy utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Revoca del documento protetto tramite policy

   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager` metodo.
   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite policy richiamando `DocumentManager` dell&#39;oggetto `getLicenseId` metodo. Passa il `com.adobe.idp.Document` oggetto che rappresenta il documento protetto tramite policy. Questo metodo restituisce un valore stringa che rappresenta il valore dell&#39;identificatore di licenza.
   * Creare un `LicenseManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getLicenseManager` metodo.
   * Revoca del documento protetto tramite policy richiamando `LicenseManager` dell&#39;oggetto `revokeLicense` e fornendo i seguenti valori:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite policy (specificare il valore restituito del `DocumentManager` dell&#39;oggetto `getLicenseId` metodo).
      * Un membro dati statico del `License` interfaccia che specifica il motivo della revoca del documento. Ad esempio, puoi specificare `License.DOCUMENT_REVISED`.
      * A `java.net.URL` valore che specifica la posizione in cui si trova un documento revisionato. Se non desideri reindirizzare un utente a un altro URL, puoi passare `null`.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): revoca di un documento tramite API Java&quot;

### Revoca dell’accesso ai documenti tramite l’API del servizio web {#revoke-access-to-documents-using-the-web-service-api}

Revoca dell’accesso a un documento PDF protetto tramite policy utilizzando Document Security API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di Document Security

   * Creare un `DocumentSecurityServiceClient` utilizzando il costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF protetto tramite policy

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF protetto tramite policy revocato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto tramite policy da revocare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Revoca del documento protetto tramite policy

   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite policy richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `getLicenseID` e passando il `BLOB` oggetto che rappresenta il documento protetto tramite policy. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore della licenza.
   * Revoca del documento protetto tramite policy richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `revokeLicense` e fornendo i seguenti valori:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite policy (specificare il valore restituito del `DocumentSecurityServiceService` dell&#39;oggetto `getLicenseId` metodo).
      * Un membro dati statico del `Reason` enum che specifica il motivo della revoca del documento. Ad esempio, puoi specificare `Reason.DOCUMENT_REVISED`.
      * A `string` valore che specifica la posizione URL in cui si trova un documento revisionato. Se non desideri reindirizzare un utente a un altro URL, puoi passare `null`.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): revoca di un documento tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): revoca di un documento tramite l’API del servizio web&quot;

**Consulta anche**

[Rimozione di criteri da documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ripristino dell’accesso ai documenti revocati {#reinstating-access-to-revoked-documents}

È possibile ripristinare l&#39;accesso a un documento di PDF revocato, in modo che tutte le copie del documento revocato siano accessibili agli utenti. Quando un utente apre un documento ripristinato che è stato revocato, può visualizzare il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per ripristinare l&#39;accesso a un documento di PDF revocato, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.
1. Ripristinare l&#39;accesso al documento PDF revocato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un’ `DocumentSecurityClient` oggetto. Se utilizzi l’API del servizio web Document Security, crea un’ `DocumentSecurityServiceService` oggetto.

**Recuperare l&#39;identificatore di licenza del documento di PDF revocato**

Recuperare l&#39;identificatore di licenza del documento PDF revocato per ripristinare un documento PDF revocato. Dopo aver ottenuto il valore dell&#39;identificatore di licenza, è possibile ripristinare un documento revocato. Se si tenta di ripristinare un documento non revocato, verrà generata un&#39;eccezione.

**Ripristina l&#39;accesso al documento di PDF revocato**

Per ripristinare l&#39;accesso a un documento PDF revocato, è necessario specificare l&#39;identificatore della licenza del documento revocato. Se si tenta di ripristinare l&#39;accesso a un documento di PDF non revocato, verrà generata un&#39;eccezione.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione delle policy ai documenti di PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Ripristinare l’accesso ai documenti revocati utilizzando l’API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Ripristinare l’accesso a un documento revocato utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocumentSecurityClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF revocato tramite il costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.
   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager` metodo.
   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando `DocumentManager` dell&#39;oggetto `getLicenseId` e passando il `com.adobe.idp.Document` oggetto che rappresenta il documento revocato. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore della licenza.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Creare un `LicenseManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getLicenseManager` metodo.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando `LicenseManager` dell&#39;oggetto `unrevokeLicense` e passando il valore dell&#39;identificatore di licenza del documento revocato.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): ripristino dell’accesso a un documento revocato tramite l’API del servizio web&quot;

### Ripristinare l’accesso ai documenti revocati tramite l’API del servizio web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Ripristinare l’accesso a un documento revocato utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `DocumentSecurityServiceClient` utilizzando il costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF revocato a cui viene ripristinato l&#39;accesso.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF revocato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `getLicenseID` e passando il `BLOB` oggetto che rappresenta il documento revocato. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore della licenza.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `unrevokeLicense` e passando un valore stringa che specifica il valore dell&#39;identificatore di licenza del documento PDF revocato (passare il valore restituito del `DocumentSecurityServiceClient` dell&#39;oggetto `getLicenseId` metodo).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): ripristino dell’accesso a un documento revocato tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): ripristino dell’accesso a un documento revocato tramite l’API del servizio web&quot;

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica dei documenti di PDF protetti tramite policy {#inspecting-policy-protected-pdf-documents}

Puoi usare l’API Document Security Service (Java e servizio web) per esaminare i documenti PDF protetti tramite policy. L’ispezione dei documenti di PDF protetti tramite policy restituisce informazioni sul documento di PDF protetto tramite policy. È possibile, ad esempio, determinare la policy utilizzata per proteggere il documento e la data in cui è stato protetto.

Non è possibile eseguire questa attività se la versione del LiveCycle in uso è 8.x o precedente. In AEM Forms è stato aggiunto il supporto per l’ispezione di documenti protetti tramite policy. Se si tenta di esaminare un documento protetto tramite policy utilizzando LiveCycle 8.x (o versioni precedenti), viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per esaminare un documento PDF protetto tramite policy, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperare un documento protetto tramite policy da esaminare.
1. Ottenere informazioni sul documento protetto tramite policy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un’ `RightsManagementClient` oggetto. Se utilizzi l’API del servizio web Document Security, crea un’ `RightsManagementServiceService` oggetto.

**Recuperare un documento protetto tramite policy da esaminare**

Per esaminare un documento protetto tramite policy, recuperalo. Se si tenta di ispezionare un documento non protetto con una policy o revocato, viene generata un&#39;eccezione.

**Inspect il documento**

Dopo aver recuperato un documento protetto tramite policy, è possibile esaminarlo.

**Ottenere informazioni sul documento protetto tramite policy**

Dopo aver esaminato un documento PDF protetto tramite policy, puoi ottenere informazioni al riguardo. È ad esempio possibile determinare il criterio utilizzato per proteggere il documento.

Se proteggi un documento con una policy che appartiene a I miei criteri e poi richiami `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, viene restituito null.

Se il documento è protetto utilizzando un criterio contenuto in un set di criteri (diverso da Criteri personali), `RMInspectResult.getPolicysetName` e `RMInspectResult.getPolicysetId` restituisce stringhe valide.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documenti di Inspect Policy Protected PDF tramite l’API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect è un documento PDF protetto tramite policy utilizzando Document Security Service API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedere [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un `RightsManagementClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare un documento protetto tramite policy da esaminare.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF protetto tramite policy utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Inspect il documento.

   * Creare un `DocumentManager` oggetto richiamando il `RightsManagementClient` dell&#39;oggetto `getDocumentManager` metodo.
   * Inspect il documento protetto tramite policy richiamando `LicenseManager` dell&#39;oggetto `inspectDocument` metodo. Passa il `com.adobe.idp.Document` oggetto contenente il documento PDF protetto tramite policy. Questo metodo restituisce un `RMInspectResult` oggetto contenente informazioni sul documento protetto tramite policy.

1. Ottenere informazioni sul documento protetto tramite policy.

   Per ottenere informazioni sul documento protetto tramite policy, richiama il metodo appropriato a cui appartiene `RMInspectResult` oggetto. Ad esempio, per recuperare il nome del criterio, richiama `RMInspectResult` dell&#39;oggetto `getPolicyName` metodo.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): ispezione dei documenti PDF protetti tramite policy tramite l’API Java&quot;

### Documenti di Inspect Policy Protected PDF che utilizzano l’API del servizio web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect è un documento PDF protetto tramite policy utilizzando l’API Document Security Service (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `RightsManagementServiceClient` utilizzando il costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento protetto tramite policy da esaminare.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF da verificare.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso per la lettura.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Inspect il documento.

   Inspect il documento protetto tramite policy richiamando `RightsManagementServiceClient` dell&#39;oggetto `inspectDocument` metodo. Passa il `BLOB` oggetto contenente il documento PDF protetto tramite policy. Questo metodo restituisce un `RMInspectResult` oggetto contenente informazioni sul documento protetto tramite policy.

1. Ottenere informazioni sul documento protetto tramite policy.

   Per ottenere informazioni sul documento protetto tramite policy, ottieni il valore del campo appropriato che appartiene al `RMInspectResult` oggetto. Ad esempio, per recuperare il nome del criterio, ottieni il valore del `RMInspectResult` dell&#39;oggetto `policyName` campo.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): controllo dei documenti PDF protetti tramite policy tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): controllo dei documenti PDF protetti tramite policy tramite l’API del servizio web&quot;

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di filigrane {#creating-watermarks}

Le filigrane contribuiscono a garantire la sicurezza di un documento identificandolo in modo univoco e controllando la violazione del copyright. Ad esempio, è possibile creare e inserire una filigrana che indichi Riservato su tutte le pagine di un documento. Dopo aver creato una filigrana, puoi includerla come parte di una policy. In altre parole, è possibile impostare l’attributo della filigrana del criterio con la filigrana appena creata. Dopo aver applicato a un documento una policy contenente una filigrana, questa viene visualizzata nel documento protetto tramite policy.

>[!NOTE]
>
>Solo gli utenti con privilegi amministrativi di Document Security possono creare filigrane. In altre parole, è necessario specificare un utente di questo tipo quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per creare una filigrana, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Impostare gli attributi delle filigrane.
1. Registra la filigrana presso il servizio Document Security.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un’ `RightsManagementClient` oggetto. Se utilizzi l’API del servizio web Document Security, crea un’ `RightsManagementServiceService` oggetto.

**Impostare gli attributi delle filigrane**

Per creare una filigrana, è necessario impostare gli attributi della filigrana. L’attributo name deve sempre essere definito. Oltre all&#39;attributo name, è necessario impostare almeno uno dei seguenti attributi:

* Testo personalizzato
* DateIncluded
* UserIdIncluded
* UserNameIncluded

Nella tabella seguente sono elencate le coppie chiave-valore necessarie per la creazione di una filigrana tramite i servizi Web.

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
   <td><p>Vero o Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Specifica se l'identificazione dell'utente che apre il documento fa parte della filigrana.</p></td>
   <td><p>Vero o Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Specifica se la data corrente fa parte della filigrana.</p></td>
   <td><p>Vero o Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Se questo valore è true, il valore del testo personalizzato deve essere specificato utilizzando <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>Vero o Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Specifica l'opacità della filigrana. Il valore predefinito è 0,5 se non specificato.</p></td>
   <td><p>Un valore compreso tra 0,0 e 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Specifica la rotazione della filigrana. Il valore predefinito è 0 gradi.</p></td>
   <td><p>Un valore compreso tra 0 e 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Se questo valore è specificato, allora <code>WaterBackCmd:IS_SIZE_ENABLED</code> deve essere presente e il valore deve essere true. Se questo attributo non è specificato, il comportamento predefinito è Adatta alla pagina.</p></td>
   <td><p>Un valore maggiore di 0,0 e minore o uguale a 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Specifica l'allineamento orizzontale della filigrana. Il valore predefinito è center.</p></td>
   <td><p>a sinistra, al centro o a destra</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Specifica l'allineamento verticale della filigrana. Il valore predefinito è center.</p></td>
   <td><p>superiore, centrale o inferiore</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Specifica se la filigrana è uno sfondo. Il valore predefinito è false.</p></td>
   <td><p>Vero o Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True se viene specificata una scala personalizzata. Se questo valore è true, è necessario specificare anche SCALE. Se questo valore è false, l’impostazione predefinita è adatta alla pagina.</p></td>
   <td><p>Vero o Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Specifica il testo personalizzato per una filigrana. Se questo valore è presente, allora <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> deve essere presente e impostato su true.</p></td>
   <td><p>Vero o Falso</p></td>
  </tr>
 </tbody>
</table>

Per tutte le filigrane deve essere definito uno dei seguenti attributi:

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Tutti gli altri attributi sono facoltativi.

**Registrare la filigrana**

Prima di poter essere utilizzata, una nuova filigrana deve essere registrata presso il servizio Document Security. Dopo aver registrato una filigrana, puoi utilizzarla all’interno dei criteri.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione delle policy ai documenti di PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creare filigrane utilizzando l’API Java {#create-watermarks-using-the-java-api}

Crea una filigrana utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi file JAR client, ad esempio `adobe-rightsmanagement-client.jar`, nel percorso della classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `RightsManagementClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Imposta attributi filigrana

   * Creare un `Watermark` oggetto richiamando il `InfomodelObjectFactory` statico dell&#39;oggetto `createWatermark` metodo. Questo metodo restituisce un `Watermark` oggetto.
   * Impostare l&#39;attributo del nome della filigrana richiamando `Watermark` dell&#39;oggetto `setName` e passando un valore stringa che specifica il nome del criterio.
   * Impostare l&#39;attributo di sfondo della filigrana richiamando `Watermark` dell&#39;oggetto `setBackground` metodo e passaggio `true`. Impostando questo attributo, la filigrana viene visualizzata sullo sfondo del documento.
   * Impostare l&#39;attributo di testo personalizzato della filigrana richiamando `Watermark` dell&#39;oggetto `setCustomText` e passando un valore stringa che rappresenta il testo della filigrana.
   * Impostare l&#39;attributo di opacità della filigrana richiamando `Watermark` dell&#39;oggetto `setOpacity` e viene passato un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che è completamente trasparente.

1. Registrare la filigrana.

   * Creare un `WatermarkManager` oggetto richiamando il `RightsManagementClient` dell&#39;oggetto `getWatermarkManager` metodo. Questo metodo restituisce un `WatermarkManager` oggetto.
   * Registrare la filigrana richiamando `WatermarkManager` dell&#39;oggetto `registerWatermark` e passando il `Watermark` oggetto che rappresenta la filigrana da registrare. Questo metodo restituisce un valore stringa che rappresenta il valore di identificazione della filigrana.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): creazione di una filigrana tramite l’API Java&quot;

### Creare filigrane utilizzando l’API del servizio web {#create-watermarks-using-the-web-service-api}

Crea una filigrana utilizzando Document Security API (servizio web):

1. Crea un oggetto API client di Document Security.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `RightsManagementServiceClient` utilizzando il costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Impostare gli attributi della filigrana.

   * Creare un `WatermarkSpec` oggetto richiamando il `WatermarkSpec` costruttore.
   * Impostare il nome della filigrana assegnando un valore stringa al `WatermarkSpec` dell&#39;oggetto `name` membro dati.
   * Impostare la filigrana `id` mediante l&#39;assegnazione di un valore stringa al `WatermarkSpec` dell&#39;oggetto `id` membro dati.
   * Per ogni proprietà filigrana da impostare, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Imposta il valore chiave assegnando un valore alla `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` membro dati (ad esempio, `WaterBackCmd:OPACITY)`.
   * Imposta il valore assegnando un valore a `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` membro dati (ad esempio, `.25`).
   * Creare un `MyArrayOf_xsd_anyType` oggetto. Per ogni `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto, richiamare `MyArrayOf_xsd_anyType` dell&#39;oggetto `Add` metodo. Passa il `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna la `MyArrayOf_xsd_anyType` oggetto al `WatermarkSpec` dell&#39;oggetto `values` membro dati.

1. Registrare la filigrana.

   Registrare la filigrana richiamando `RightsManagementServiceClient` dell&#39;oggetto `registerWatermark` e passando il `WatermarkSpec` oggetto che rappresenta la filigrana da registrare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): creazione di una filigrana tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): creazione di una filigrana tramite l’API del servizio web&quot;

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica delle filigrane {#modifying-watermarks}

Puoi modificare una filigrana esistente utilizzando l’API Java di Document Security o l’API di servizio web. Per modificare una filigrana esistente, recuperarla, modificarne gli attributi e quindi aggiornarla sul server. Si supponga, ad esempio, di recuperare una filigrana e di modificarne l&#39;attributo di opacità. Prima di applicare la modifica, è necessario aggiornare la filigrana.

Quando si modifica una filigrana, la modifica ha effetto sui documenti futuri a cui è applicata la filigrana. In altre parole, i documenti PDF esistenti che contengono la filigrana non vengono interessati.

>[!NOTE]
>
>Solo gli utenti con privilegi amministrativi di Document Security possono modificare le filigrane. In altre parole, è necessario specificare un utente di questo tipo quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-9}

Per modificare una filigrana, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperate la filigrana da modificare.
1. Impostare gli attributi delle filigrane.
1. Aggiorna la filigrana.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzi l’API Java, crea un’ `DocumentSecurityClient` oggetto. Se utilizzi l’API del servizio web Document Security, crea un’ `DocumentSecurityServiceService` oggetto.

**Recupera la filigrana da modificare**

Per modificare una filigrana, è necessario recuperarne una esistente. È possibile recuperare una filigrana specificandone il nome o specificandone il valore di identificatore.

**Impostare gli attributi delle filigrane**

Per modificare una filigrana esistente, modificare il valore di uno o più attributi della filigrana. Quando si aggiorna una filigrana a livello di programmazione utilizzando un servizio Web, è necessario impostare tutti gli attributi impostati in origine, anche se il valore non cambia. Ad esempio, si supponga di impostare i seguenti attributi di filigrana: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`, e `WaterBackCmd:SRCTEXT`. Anche se l’unico attributo che desideri modificare è `WaterBackCmd:OPACITY`, è necessario impostare correttamente gli altri valori.

>[!NOTE]
>
>Quando si utilizza l’API Java per modificare una filigrana, non è necessario specificare tutti gli attributi. Impostare l&#39;attributo della filigrana che si desidera modificare.

>[!NOTE]
>
>Per informazioni sui nomi degli attributi della filigrana, vedere [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).

**Aggiorna filigrana**

Dopo aver modificato gli attributi di una filigrana, è necessario aggiornarla.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Creazione di filigrane](protecting-documents-policies.md#creating-watermarks)

### Modificare le filigrane utilizzando l’API Java {#modify-watermarks-using-the-java-api}

Modifica una filigrana utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocumentSecurityClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperate la filigrana da modificare.

   Creare un `WatermarkManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getWatermarkManager` e passa un valore stringa che specifica il nome della filigrana. Questo metodo restituisce un `Watermark` oggetto che rappresenta la filigrana da modificare.

1. Impostare gli attributi della filigrana.

   Impostare l&#39;attributo di opacità della filigrana richiamando `Watermark` dell&#39;oggetto `setOpacity` e viene passato un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che è completamente trasparente.

   >[!NOTE]
   >
   >In questo esempio viene modificato solo l&#39;attributo di opacità.

1. Aggiorna la filigrana.

   * Aggiornare la filigrana richiamando `WatermarkManager` dell&#39;oggetto `updateWatermark` e trasmettere il `Watermark` oggetto il cui attributo è stato modificato.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Guida rapida (modalità SOAP): modifica di una filigrana tramite API Java.

### Modificare le filigrane utilizzando l’API del servizio web {#modify-watermarks-using-the-web-service-api}

Modifica una filigrana utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `DocumentSecurityServiceClient` utilizzando il costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperate la filigrana da modificare.

   Recuperare la filigrana da modificare richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `getWatermarkByName` metodo. Passa un valore stringa che specifica il nome della filigrana. Questo metodo restituisce un `WatermarkSpec` oggetto che rappresenta la filigrana da modificare.

1. Impostare gli attributi della filigrana.

   * Per ogni proprietà filigrana da aggiornare, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Imposta il valore chiave assegnando un valore alla `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` membro dati (ad esempio, `WaterBackCmd:OPACITY)`.
   * Imposta il valore assegnando un valore a `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` membro dati (ad esempio, `.50`).
   * Creare un `MyArrayOf_xsd_anyType` oggetto. Per ogni `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto, richiamare `MyArrayOf_xsd_anyType` dell&#39;oggetto `Add` metodo. Passa il `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna la `MyArrayOf_xsd_anyType` oggetto al `WatermarkSpec` dell&#39;oggetto `values` membro dati.

1. Aggiorna la filigrana.

   Aggiornare la filigrana richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `updateWatermark` e passando il `WatermarkSpec` oggetto che rappresenta la filigrana da modificare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (MTOM): modifica di una filigrana tramite l’API del servizio web&quot;

## Ricerca di eventi {#searching-for-events}

Il servizio di Rights Management tiene traccia di azioni specifiche nel momento in cui si verificano, ad esempio l’applicazione di una policy a un documento, l’apertura di un documento protetto tramite policy e la revoca dell’accesso ai documenti. Il controllo degli eventi deve essere abilitato per il servizio di Rights Management oppure non è possibile tenere traccia degli eventi.

Gli eventi rientrano in una delle seguenti categorie:

* Gli eventi di amministratore sono azioni correlate a un amministratore, ad esempio la creazione di un account amministratore.
* Gli eventi documento sono azioni correlate a un documento, ad esempio la chiusura di un documento protetto tramite policy.
* Gli eventi dei criteri sono azioni correlate a un criterio, ad esempio la creazione di un criterio.
* Gli eventi di servizio sono azioni correlate al servizio di Rights Management, ad esempio la sincronizzazione con la directory utente.

Puoi cercare eventi specifici utilizzando l’API Java di Rights Management o l’API di servizio web. La ricerca di eventi consente di eseguire attività quali la creazione di un file di registro di determinati eventi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di Rights Management, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-10}

Per cercare un evento di Rights Management, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Rights Management.
1. Specifica l’evento per il quale eseguire la ricerca.
1. Cerca l’evento.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creazione di un oggetto API client di Rights Management**

Prima di poter eseguire un&#39;operazione del servizio di Rights Management a livello di programmazione, è necessario creare un oggetto client del servizio di Rights Management. Se utilizzi l’API Java, crea un’ `DocumentSecurityClient` oggetto. Se utilizzi l’API del servizio Web Rights Management, crea un’ `DocumentSecurityServiceService` oggetto.

**Specificare gli eventi da cercare**

Specifica l’evento da cercare. Ad esempio, è possibile cercare l’evento di creazione del criterio, che si verifica quando viene creato un nuovo criterio.

**Cerca l’evento**

Dopo aver specificato l’evento da cercare, puoi utilizzare l’API Java di Rights Management o l’API del servizio web di Rights Management per cercare l’evento.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cercare gli eventi utilizzando l’API Java {#search-for-events-using-the-java-api}

Cerca gli eventi utilizzando l’API di Rights Management (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creazione di un oggetto API client di Rights Management

   Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene proprietà di connessione.

1. Specificare gli eventi da cercare

   * Creare un `EventManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getEventManager` metodo. Questo metodo restituisce un `EventManager` oggetto.
   * Creare un `EventSearchFilter` richiamando il relativo costruttore.
   * Specifica l’evento per il quale eseguire la ricerca richiamando `EventSearchFilter` dell&#39;oggetto `setEventCode` e il passaggio di un membro dati statico che appartiene al `EventManager` classe che rappresenta l’evento per il quale eseguire la ricerca. Ad esempio, per cercare l’evento di creazione del criterio, passa `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >È possibile definire criteri di ricerca aggiuntivi richiamando `EventSearchFilter` metodi a oggetti. Ad esempio, richiama il `setUserName` per specificare un utente associato all&#39;evento.

1. Cerca l’evento

   Cercare l&#39;evento richiamando `EventManager` dell&#39;oggetto `searchForEvents` e passando il `EventSearchFilter` oggetto che definisce i criteri di ricerca dell&#39;evento. Questo metodo restituisce un array di `Event` oggetti.

**Esempi di codice**

Per esempi di codice relativi all&#39;utilizzo del servizio di Rights Management, vedere la Guida introduttiva seguente:

* &quot;Guida rapida (SOAP): ricerca di eventi tramite l’API Java&quot;

### Cercare gli eventi utilizzando l’API del servizio web {#search-for-events-using-the-web-service-api}

Cerca gli eventi utilizzando l’API di Rights Management (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creazione di un oggetto API client di Rights Management

   * Creare un `DocumentSecurityServiceClient` utilizzando il costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Specificare gli eventi da cercare

   * Creare un `EventSpec` mediante il costruttore.
   * Specificare l&#39;inizio del periodo di tempo durante il quale si è verificato l&#39;evento impostando `EventSpec` dell&#39;oggetto `firstTime.date` membro dati con `DataTime` istanza che rappresenta l’inizio dell’intervallo di date in cui si è verificato l’evento.
   * Assegna il valore `true` al `EventSpec` dell&#39;oggetto `firstTime.dateSpecified` membro dati.
   * Specificare la fine del periodo di tempo durante il quale si è verificato l&#39;evento impostando `EventSpec` dell&#39;oggetto `lastTime.date` membro dati con `DataTime` istanza che rappresenta la fine dell’intervallo di date in cui si è verificato l’evento.
   * Assegna il valore `true` al `EventSpec` dell&#39;oggetto `lastTime.dateSpecified` membro dati.
   * Imposta l’evento da cercare assegnando un valore stringa alla `EventSpec` dell&#39;oggetto `eventCode` membro dati. Nella tabella seguente sono elencati i valori numerici che è possibile assegnare a questa proprietà:

   <table>
    <thead>
    <tr>
    <th><p>Tipo di evento</p></th>
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

   Cercare l&#39;evento richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `searchForEvents` e passando il `EventSpec` oggetto che rappresenta l’evento per il quale eseguire la ricerca e il numero massimo di risultati. Questo metodo restituisce un `MyArrayOf_xsd_anyType` raccolta in cui ogni elemento è un `AuditSpec` dell&#39;istanza. Utilizzo di un `AuditSpec` dell&#39;evento, ad esempio l&#39;ora in cui si è verificato. Il `AuditSpec` l’istanza contiene un `timestamp` membro dati che specifica queste informazioni.

**Esempi di codice**

Per esempi di codice relativi all&#39;utilizzo del servizio di Rights Management, vedere la Guida introduttiva seguente:

* &quot;Guida rapida (MTOM): ricerca di eventi tramite l’API del servizio web&quot;
* &quot;Quick Start (SwaRef): ricerca di eventi tramite l’API del servizio web&quot;

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Applicazione di criteri ai documenti di Word {#applying-policies-to-word-documents}

Oltre ai documenti PDF, il servizio Rights Management supporta formati di documento aggiuntivi, ad esempio un documento di Microsoft Word (file DOC) e altri formati di file di Microsoft Office. È ad esempio possibile applicare una policy a un documento di Word per proteggerlo. Applicando una policy a un documento di Word, si limita l&#39;accesso al documento. Non è possibile applicare una policy a un documento se il documento è già protetto con una policy.

È possibile monitorare l&#39;utilizzo di un documento Word protetto tramite policy dopo averlo distribuito. In altre parole, è possibile vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile scoprire quando qualcuno ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-11}

Per applicare una policy a un documento di Word, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperare un documento di Word a cui è applicato un criterio.
1. Applicare una policy esistente al documento di Word.
1. Salvare il documento Word protetto tramite policy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security.

**Recuperare un documento di Word**

Recuperare un documento di Word per applicare una policy. Dopo aver applicato una policy al documento di Word, gli utenti saranno soggetti a restrizioni quando utilizzano il documento. Se, ad esempio, la policy non consente l&#39;apertura del documento in modalità non in linea, gli utenti devono essere in linea per aprire il documento.

**Applicare una policy esistente al documento di Word**

Per applicare un criterio a un documento di Word, è necessario fare riferimento a un criterio esistente e specificare il set di criteri a cui appartiene il criterio. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verificherà un&#39;eccezione.

**Salvare il documento di Word**

Dopo che il servizio Document Security ha applicato una policy a un documento di Word, è possibile salvarlo come file DOC.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicare una policy a un documento Word utilizzando l’API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Applicare una policy a un documento di Word utilizzando l’API Document Security (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocumentSecurityClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare un documento di Word.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento di Word utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento di Word.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Applicare una policy esistente al documento di Word.

   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager` metodo.
   * Applicare una policy al documento di Word richiamando `DocumentManager` dell&#39;oggetto `protectDocument` e fornendo i seguenti valori:

      * Il `com.adobe.idp.Document` oggetto che contiene il documento di Word a cui viene applicato il criterio.
      * Valore stringa che specifica il nome del documento.
      * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un `null` valore che risulta in `MyPolicies` set di criteri in uso.
      * Valore stringa che specifica il nome del criterio.
      * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere null).
      * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere `null` (se questo parametro è `null`, il valore del parametro precedente deve essere `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta la lingua utilizzata per selezionare il modello di MS Office. Il valore di questo parametro è facoltativo ed è possibile specificare `null`.

     Il `protectDocument` il metodo restituisce un `RMSecureDocumentResult` oggetto che contiene il documento Word protetto tramite policy.

1. Salvare il documento di Word.

   * Richiama `RMSecureDocumentResult` dell&#39;oggetto `getProtectedDoc` per ottenere il documento Word protetto tramite policy. Questo metodo restituisce un `com.adobe.idp.Document` oggetto.
   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia DOC.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file (assicurati di utilizzare il `Document` oggetto restituito da `getProtectedDoc` metodo).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (modalità SOAP): applicazione di una policy a un documento Word tramite l’API Java&quot;

### Applicare una policy a un documento Word utilizzando l’API del servizio web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Applicare una policy a un documento di Word utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un `DocumentSecurityServiceClient` utilizzando il costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento di Word.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento di Word a cui viene applicato un criterio.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di Word e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. Determinare la dimensione dell&#39;array di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Applicare una policy esistente al documento di Word.

   Applicare una policy al documento di Word richiamando `DocumentSecurityServiceClient` dell&#39;oggetto `protectDocument` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che contiene il documento di Word a cui viene applicato il criterio.
   * Valore stringa che specifica il nome del documento.
   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un `null` valore che risulta in `MyPolicies` set di criteri in uso.
   * Valore stringa che specifica il nome del criterio.
   * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere `null`).
   * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro precedente deve essere `null`).
   * A `RMLocale` valore che specifica il valore locale (ad esempio, `RMLocale.en`).
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore dei criteri.
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite policy.
   * Un parametro di output stringa utilizzato per memorizzare il tipo mime (ad esempio, `application/doc`).

   Il `protectDocument` il metodo restituisce un `BLOB` oggetto che contiene il documento Word protetto tramite policy.

1. Salvare il documento di Word.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento Word protetto tramite policy.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `protectDocument` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file di Word richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (MTOM): applicazione di una policy a un documento Word tramite l’API del servizio web&quot;

## Rimozione di criteri da documenti di Word {#removing-policies-from-word-documents}

È possibile rimuovere una policy da un documento Word protetto tramite policy per rimuovere la protezione dal documento. In altre parole, se non desideri più che il documento sia protetto da una policy. Se si desidera aggiornare un documento Word protetto tramite policy con una policy più recente, invece di rimuovere la policy e aggiungere la policy aggiornata, è più efficiente cambiare la policy.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-12}

Per rimuovere una policy da un documento Word protetto tramite policy, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Crea un oggetto API client di Document Security.
1. Recuperare un documento Word protetto tramite policy.
1. Rimuovere la policy dal documento di Word.
1. Salva i documenti Word non protetti

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security.

**Recuperare un documento Word protetto tramite policy**

Recuperare un documento Word protetto tramite policy per rimuovere una policy. Se si tenta di rimuovere una policy da un documento di Word non protetto da una policy, verrà generata un&#39;eccezione.

**Rimuovere la policy dal documento di Word**

È possibile rimuovere una policy da un documento Word protetto tramite policy a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere `SWITCH_POLICY` autorizzazione per rimuovere una policy da un documento di Word. Inoltre, anche l’utente specificato nelle impostazioni di connessione di AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento Word non protetto**

Dopo che il servizio Document Security ha rimosso una policy da un documento Word, puoi salvare il documento Word non protetto come file DOC.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione di criteri ai documenti di Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Rimuovere una policy da un documento Word utilizzando l’API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Rimuovi una policy da un documento Word protetto tramite policy utilizzando Document Security API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Document Security

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `RightsManagementClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare un documento Word protetto tramite policy

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento Word protetto tramite policy utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento Word.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Rimuovere la policy dal documento di Word

   * Creare un `DocumentManager` oggetto richiamando il `RightsManagementClient` dell&#39;oggetto `getDocumentManager` metodo.
   * Rimuovere una policy dal documento di Word richiamando `DocumentManager` dell&#39;oggetto `removeSecurity` e passando il `com.adobe.idp.Document` oggetto che contiene il documento Word protetto tramite policy. Questo metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento di Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia DOC.
   * Richiama `Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file (assicurati di utilizzare il `Document` oggetto restituito da `removeSecurity` metodo).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (modalità SOAP): rimozione di una policy da un documento Word tramite l’API Java&quot;

### Rimuovere una policy da un documento di Word utilizzando l’API del servizio web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Rimuovi una policy da un documento Word protetto tramite policy utilizzando Document Security API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di Document Security

   * Creare un `RightsManagementServiceClient` utilizzando il costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento Word protetto tramite policy

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` viene utilizzato per memorizzare il documento Word protetto tramite policy da cui viene rimossa la policy.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di Word e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Rimuovere la policy dal documento di Word

   Rimuovere la policy dal documento di Word richiamando `RightsManagementServiceClient` dell&#39;oggetto `removePolicySecurity` e passando il `BLOB` oggetto che contiene il documento Word protetto tramite policy. Questo metodo restituisce un `BLOB` oggetto contenente un documento di Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di Word non protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `removePolicySecurity` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` campo.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (MTOM): rimozione di una policy da un documento Word tramite l’API del servizio web&quot;

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
