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
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '15394'
ht-degree: 0%

---

# Protezione di documenti con criteri {#protecting-documents-with-policies}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

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

* Creare criteri. Per informazioni, vedere [Creazione di criteri](protecting-documents-policies.md#creating-policies).
* Modificare i criteri. Per informazioni, vedere [Modifica dei criteri](protecting-documents-policies.md#modifying-policies).
* Elimina criteri. Per informazioni, vedere [Eliminazione dei criteri](protecting-documents-policies.md#deleting-policies).
* Applicare policy ai documenti PDF. Per informazioni, vedere [Applicazione dei criteri ai documenti di PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Rimuovere i criteri dai documenti di PDF. Per informazioni, vedere [Rimozione dei criteri dai documenti di PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documenti protetti tramite policy di Inspect. Per informazioni, vedere [Verifica dei documenti di PDF protetti dai criteri](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revoca dell&#39;accesso ai documenti di PDF. Per informazioni, vedere [Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents).
* Ripristinare l&#39;accesso ai documenti revocati. Per informazioni, vedere [Ripristino dell&#39;accesso ai documenti revocati](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Creare filigrane. Per informazioni, vedere [Creazione delle filigrane](protecting-documents-policies.md#creating-watermarks).
* Cerca gli eventi. Per informazioni, vedere [Ricerca di eventi](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di criteri {#creating-policies}

Puoi creare policy a livello di programmazione utilizzando l’API Java di Document Security o l’API di servizio web. Un *criterio* è una raccolta di informazioni che include impostazioni di protezione dei documenti, utenti autorizzati e diritti di utilizzo. È possibile creare e salvare un numero qualsiasi di criteri, utilizzando le impostazioni di protezione appropriate per situazioni e utenti diversi.

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security.

**Imposta gli attributi del criterio**

Per creare un criterio, impostare gli attributi del criterio. Un attributo obbligatorio è il nome del criterio. I nomi dei criteri devono essere univoci per ogni set di criteri. Un set di criteri è semplicemente una raccolta di criteri. Se i criteri appartengono a set di criteri separati, è possibile che siano presenti due criteri con lo stesso nome. Tuttavia, due criteri all&#39;interno di un singolo set di criteri non possono avere lo stesso nome.

Un altro attributo utile da impostare è il periodo di validità. Un periodo di validità è il periodo di tempo durante il quale un documento protetto tramite policy è accessibile ai destinatari autorizzati. Se non si imposta questo attributo, il criterio è sempre valido.

Un periodo di validità può essere impostato su una delle seguenti opzioni:

* Un numero di giorni impostato per l&#39;accesso al documento dal momento in cui il documento viene pubblicato
* Data di fine dopo la quale il documento non è accessibile
* Un intervallo di date specifico per il quale il documento è accessibile
* Sempre valido

È possibile specificare solo una data di inizio, che determina la validità del criterio dopo la data di inizio. Se specifichi solo una data di fine, il criterio è valido fino alla data di fine. Tuttavia, viene generata un’eccezione se non sono definite sia una data di inizio che una data di fine.

Quando si impostano gli attributi che appartengono a un criterio, è inoltre possibile impostare le impostazioni di crittografia. Queste impostazioni di crittografia hanno effetto quando la policy viene applicata a un documento. È possibile specificare i seguenti valori di crittografia:

* **AES256**: rappresenta l&#39;algoritmo di crittografia AES con una chiave a 256 bit.
* **AES128**: rappresenta l&#39;algoritmo di crittografia AES con una chiave a 128 bit.
* **NoEncryption:** non rappresenta alcuna crittografia.

Quando si specifica l&#39;opzione `NoEncryption`, non è possibile impostare l&#39;opzione `PlaintextMetadata` su `false`. Se tenti di farlo, viene generata un’eccezione.

>[!NOTE]
>
>Per informazioni sugli altri attributi che è possibile impostare, vedere la descrizione dell&#39;interfaccia `Policy` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crea una voce di criterio**

Una voce criterio consente di associare entità, ovvero gruppi e utenti, e autorizzazioni a un criterio. Un criterio deve avere almeno una voce di criterio. Si supponga, ad esempio, di eseguire i task riportati di seguito.

* Creare e registrare una voce di criterio che consente a un gruppo di visualizzare un documento solo mentre è online e impedisce ai destinatari di copiarlo.
* Allega la voce del criterio al criterio.
* Proteggi un documento con la policy utilizzando Acrobat.

Di conseguenza, i destinatari possono solo visualizzare il documento online e non possono copiarlo. Il documento rimane protetto finché non viene rimossa la protezione.

**Registra il criterio**

È necessario registrare un nuovo criterio prima di poterlo utilizzare. Dopo aver registrato una policy, è possibile utilizzarla per proteggere i documenti.

### Creare un criterio utilizzando l’API Java {#create-a-policy-using-the-java-api}

Crea una policy utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare gli attributi del criterio.

   * Creare un oggetto `Policy` richiamando il metodo `createPolicy` statico dell&#39;oggetto `InfomodelObjectFactory`. Questo metodo restituisce un oggetto `Policy`.
   * Impostare l&#39;attributo name del criterio richiamando il metodo `setName` dell&#39;oggetto `Policy` e passando un valore stringa che specifica il nome del criterio.
   * Impostare la descrizione del criterio richiamando il metodo `setDescription` dell&#39;oggetto `Policy` e passando un valore stringa che specifica la descrizione del criterio.
   * Specificare il set di criteri a cui appartiene il nuovo criterio richiamando il metodo `setPolicySetName` dell&#39;oggetto `Policy` e passando un valore stringa che specifica il nome del set di criteri. È possibile specificare `null` per il valore di questo parametro che determina l&#39;aggiunta del criterio al set di criteri *Criteri personali*.
   * Creare il periodo di validità del criterio richiamando il metodo `createValidityPeriod` statico dell&#39;oggetto `InfomodelObjectFactory`. Questo metodo restituisce un oggetto `ValidityPeriod`.
   * Impostare il numero di giorni per i quali un documento protetto tramite policy è accessibile richiamando il metodo `setRelativeExpirationDays` dell&#39;oggetto `ValidityPeriod` e passando un valore intero che specifica il numero di giorni.
   * Impostare il periodo di validità del criterio richiamando il metodo `setValidityPeriod` dell&#39;oggetto `Policy` e passando l&#39;oggetto `ValidityPeriod`.

1. Crea una voce criterio.

   * Creare una voce dei criteri richiamando il metodo `createPolicyEntry` statico dell&#39;oggetto `InfomodelObjectFactory`. Questo metodo restituisce un oggetto `PolicyEntry`.
   * Specificare le autorizzazioni del criterio richiamando il metodo `createPermission` statico dell&#39;oggetto `InfomodelObjectFactory`. Passa un membro dati statico che appartiene all&#39;interfaccia `Permission` che rappresenta l&#39;autorizzazione. Questo metodo restituisce un oggetto `Permission`. Per aggiungere ad esempio l&#39;autorizzazione che consente agli utenti di copiare dati da un documento PDF protetto tramite policy, passare `Permission.COPY`. (Ripeti questo passaggio per ogni autorizzazione da aggiungere).
   * Aggiungere l&#39;autorizzazione alla voce dei criteri richiamando il metodo `addPermission` dell&#39;oggetto `PolicyEntry` e passando l&#39;oggetto `Permission`. Ripetere questo passaggio per ogni oggetto `Permission` creato.
   * Creare l&#39;entità criterio richiamando il metodo `createSpecialPrincipal` statico dell&#39;oggetto `InfomodelObjectFactory`. Passare un membro dati appartenente all&#39;oggetto `InfomodelObjectFactory` che rappresenta l&#39;entità. Questo metodo restituisce un oggetto `Principal`. Ad esempio, per aggiungere l&#39;editore del documento come entità principale, passare `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Aggiungere l&#39;entità alla voce dei criteri richiamando il metodo `setPrincipal` dell&#39;oggetto `PolicyEntry` e passando l&#39;oggetto `Principal`.
   * Aggiungere la voce del criterio richiamando il metodo `addPolicyEntry` dell&#39;oggetto `Policy` e passando l&#39;oggetto `PolicyEntry`.

1. Registra il criterio.

   * Creare un oggetto `PolicyManager` richiamando il metodo `getPolicyManager` dell&#39;oggetto `DocumentSecurityClient`.
   * Registrare il criterio richiamando il metodo `registerPolicy` dell&#39;oggetto `PolicyManager` e passando i valori seguenti:

      * Oggetto `Policy` che rappresenta il criterio da registrare.

   * Valore stringa che rappresenta il set di criteri a cui appartiene il criterio.

   Se si utilizza un account amministratore di AEM forms nelle impostazioni di connessione per creare l&#39;oggetto `DocumentSecurityClient`, specificare il nome del set di criteri quando si richiama il metodo `registerPolicy`. Se si passa un valore `null` per il set di criteri, il criterio verrà creato nel set di criteri *Criteri personali* degli amministratori.

   Se utilizzi un utente di Document Security nelle impostazioni di connessione, puoi richiamare il metodo `registerPolicy` sovraccarico che accetta solo i criteri. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri personali*. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome per il set di criteri quando si richiama il metodo `registerPolicy`.

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Impostare gli attributi del criterio.

   * Creare un oggetto `PolicySpec` utilizzando il relativo costruttore.
   * Impostare il nome del criterio assegnando un valore stringa al membro dati `name` dell&#39;oggetto `PolicySpec`.
   * Impostare la descrizione del criterio assegnando un valore stringa al membro dati `description` dell&#39;oggetto `PolicySpec`.
   * Specificare il set di criteri a cui appartiene il criterio assegnando un valore stringa al membro dati `policySetName` dell&#39;oggetto `PolicySpec`. Specificare un nome di set di criteri esistente. È possibile specificare `null` per il valore di questo parametro che determina l&#39;aggiunta del criterio a *Criteri personali*.
   * Impostare il periodo di lease offline del criterio assegnando un valore intero al membro dati `offlineLeasePeriod` dell&#39;oggetto `PolicySpec`.
   * Impostare il membro dati `policyXml` dell&#39;oggetto `PolicySpec` con un valore stringa che rappresenta i dati XML PDRL. Per eseguire questa attività, creare un oggetto .NET `StreamReader` utilizzando il relativo costruttore. Passare la posizione di un file XML PDRL che rappresenta il criterio al costruttore `StreamReader`. Quindi, richiamare il metodo `ReadLine` dell&#39;oggetto `StreamReader` e assegnare il valore restituito a una variabile stringa. Scorrere l&#39;oggetto `StreamReader` fino a quando il metodo `ReadLine` non restituisce null. Assegnare la variabile stringa al membro dati `policyXml` dell&#39;oggetto `PolicySpec`.

1. Crea una voce criterio.

   Non è necessario creare una voce policy durante la creazione di una policy utilizzando l’API del servizio web di Document Security. La voce del criterio è definita nel documento PDRL.

1. Registra il criterio.

   Registrare il criterio richiamando il metodo `registerPolicy` dell&#39;oggetto `DocumentSecurityServiceClient` e passando i valori seguenti:

   * Oggetto `PolicySpec` che rappresenta il criterio da registrare.
   * Valore stringa che rappresenta il set di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;aggiunta del criterio al set di criteri *MyPolicy*.

   Se si utilizza un account amministratore di AEM forms nelle impostazioni di connessione per creare l&#39;oggetto `DocumentSecurityClient`, specificare il nome del set di criteri quando si richiama il metodo `registerPolicy`.

   Se utilizzi un utente di Document SecurityDocument Security nelle impostazioni di connessione, puoi richiamare il metodo `registerPolicy` sovraccarico che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri personali*. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome per il set di criteri quando si richiama il metodo `registerPolicy`.

   >[!NOTE]
   >
   >Quando crei un criterio e specifichi un set di criteri, accertati di specificare un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): creazione di un criterio utilizzando l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): creazione di un criterio utilizzando l’API del servizio web&quot;

## Modifica dei criteri {#modifying-policies}

Puoi modificare una policy esistente utilizzando l’API Java di Document Security o l’API di servizio web. Per modificare un criterio esistente, recuperarlo, modificarlo e quindi aggiornare il criterio sul server. Si supponga, ad esempio, di recuperare un criterio esistente e di estenderne il periodo di validità. Prima che la modifica entri in vigore, devi aggiornare il criterio.

È possibile modificare un criterio quando cambiano i requisiti aziendali e il criterio non riflette più questi requisiti. Invece di creare un criterio, puoi semplicemente aggiornare un criterio esistente.

Per modificare gli attributi dei criteri utilizzando un servizio web (ad esempio, utilizzando le classi proxy Java create con JAX-WS), è necessario assicurarsi che i criteri siano registrati nel servizio Document Security. È quindi possibile fare riferimento al criterio esistente utilizzando il metodo `PolicySpec.getPolicyXml` e modificare gli attributi del criterio utilizzando i metodi applicabili. Ad esempio, è possibile modificare il periodo di lease offline richiamando il metodo `PolicySpec.setOfflineLeasePeriod`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire un’operazione Document Security Service a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se si utilizza l&#39;API Java, creare un oggetto `RightsManagementClient`. Se utilizzi l’API del servizio web Document Security, crea un oggetto `RightsManagementServiceService`.

**Recupera un criterio esistente**

Recuperare un criterio esistente per modificarlo. Per recuperare un criterio, specificare il nome del criterio e il set di criteri a cui appartiene il criterio. Se si specifica un valore `null` per il nome del set di criteri, il criterio verrà recuperato dal set di criteri *Criteri personali*.

**Imposta gli attributi del criterio**

Per modificare un criterio, è necessario modificare il valore degli attributi del criterio. L’unico attributo del criterio che non può essere modificato è l’attributo name. Ad esempio, per modificare il periodo di lease offline del criterio, è possibile modificare il valore dell&#39;attributo del periodo di lease offline del criterio.

Quando si modifica il periodo di lease offline di un criterio utilizzando un servizio Web, il campo `offlineLeasePeriod` nell&#39;interfaccia `PolicySpec` viene ignorato. Per aggiornare il periodo di lease offline, modificare l&#39;elemento `OfflineLeasePeriod` nel documento XML PDRL. Fare quindi riferimento al documento XML PDRL aggiornato utilizzando il membro dati `policyXML` dell&#39;interfaccia `PolicySpec`.

>[!NOTE]
>
>Per informazioni sugli altri attributi che è possibile impostare, vedere la descrizione dell&#39;interfaccia `Policy` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Aggiorna il criterio**

Prima di poter applicare le modifiche apportate a una policy, è necessario aggiornarla con il servizio Document Security. Le modifiche alle policy che proteggono i documenti vengono aggiornate alla successiva sincronizzazione del documento protetto con il servizio Document Security.

### Modificare i criteri esistenti utilizzando l’API Java {#modify-existing-policies-using-the-java-api}

Modifica una policy esistente utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera un criterio esistente.

   * Creare un oggetto `PolicyManager` richiamando il metodo `getPolicyManager` dell&#39;oggetto `RightsManagementClient`.
   * Creare un oggetto `Policy` che rappresenta il criterio da aggiornare richiamando il metodo `getPolicy` dell&#39;oggetto `PolicyManager` e passando i valori seguenti&quot;

      * Valore stringa che rappresenta il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Valore stringa che rappresenta il nome del criterio.

1. Impostare gli attributi del criterio.

   Modifica gli attributi della policy per soddisfare i requisiti aziendali. Ad esempio, per modificare il periodo di lease offline del criterio, richiamare il metodo `setOfflineLeasePeriod` dell&#39;oggetto `Policy`.

1. Aggiorna il criterio.

   Aggiornare il criterio richiamando il metodo `updatePolicy` dell&#39;oggetto `PolicyManager`. Passa l&#39;oggetto `Policy` che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Guida rapida (modalità SOAP): modificare una policy utilizzando l’API Java.

### Modificare i criteri esistenti utilizzando l’API del servizio web {#modify-existing-policies-using-the-web-service-api}

Modifica una policy esistente utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera un criterio esistente.

   Creare un oggetto `PolicySpec` che rappresenta il criterio da modificare richiamando il metodo `getPolicy` dell&#39;oggetto `RightsManagementServiceClient` e passando i valori seguenti:

   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Valore stringa che specifica il nome del criterio.

1. Impostare gli attributi del criterio.

   Modifica gli attributi della policy per soddisfare i requisiti aziendali.

1. Aggiorna il criterio.

   Aggiornare il criterio richiamando il metodo `updatePolicyFromSDK` dell&#39;oggetto `RightsManagementServiceClient` e passando l&#39;oggetto `PolicySpec` che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): modifica di un criterio tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): modifica di un criterio tramite l’API del servizio web&quot;

## Eliminazione dei criteri {#deleting-policies}

Puoi eliminare una policy esistente utilizzando l’API Java di Document Security o l’API di servizio web. Una volta eliminata, una policy non può più essere utilizzata per proteggere i documenti. Tuttavia, i documenti protetti tramite policy esistenti che utilizzano la policy sono ancora protetti. È possibile eliminare un criterio quando ne diventa disponibile uno più recente.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per eliminare un criterio esistente, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Crea un oggetto API client di Document Security.
1. Elimina il criterio.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se si utilizza l&#39;API Java, creare un oggetto `RightsManagementClient`. Se utilizzi l’API del servizio web Document Security, crea un oggetto `RightsManagementServiceService`.

**Elimina il criterio**

Per eliminare un criterio, specificare il criterio da eliminare e il set di criteri a cui appartiene il criterio. L’utente le cui impostazioni vengono utilizzate per richiamare AEM Forms deve disporre dell’autorizzazione per eliminare il criterio; in caso contrario, si verifica un’eccezione. Analogamente, se si tenta di eliminare un criterio inesistente, si verifica un&#39;eccezione.

### Eliminare i criteri utilizzando l’API Java {#delete-policies-using-the-java-api}

Elimina una policy utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Elimina il criterio.

   * Creare un oggetto `PolicyManager` richiamando il metodo `getPolicyManager` dell&#39;oggetto `RightsManagementClient`.
   * Eliminare il criterio richiamando il metodo `deletePolicy` dell&#39;oggetto `PolicyManager` e passando i valori seguenti:

      * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Elimina il criterio.

   Eliminare un criterio richiamando il metodo `deletePolicy` dell&#39;oggetto `RightsManagementServiceClient` e passando i valori seguenti:

   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security. Se si utilizza l&#39;API Java, creare un oggetto `DocumentSecurityClient`. Se utilizzi l’API del servizio web Document Security, crea un oggetto `DocumentSecurityServiceService`.

**Recuperare un documento PDF**

È possibile recuperare un documento PDF per applicare una policy. Dopo aver applicato una policy al documento PDF, gli utenti vengono limitati quando utilizzano il documento. Se, ad esempio, la policy non consente l&#39;apertura del documento in modalità non in linea, gli utenti devono essere in linea per aprire il documento.

**Applica un criterio esistente al documento PDF**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Applica una policy esistente al documento PDF.

   * Creare un oggetto `DocumentManager` richiamando il metodo `getDocumentManager` dell&#39;oggetto `RightsManagementClient`.
   * Applicare una policy al documento PDF richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentManager` e passando i valori seguenti:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF a cui viene applicato il criterio.
      * Valore stringa che specifica il nome del documento.
      * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Valore stringa che specifica il nome del criterio.
      * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere null).
      * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore del parametro è facoltativo e può essere `null` (se il parametro è null, il valore del parametro precedente deve essere `null`).
      * `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni locali utilizzate per la selezione del modello di MS Office. Questo valore di parametro è facoltativo e non viene utilizzato per i documenti PDF. Per proteggere un documento PDF, specificare `null`.

     Il metodo `protectDocument` restituisce un oggetto `RMSecureDocumentResult` contenente il documento PDF protetto tramite policy.

1. Salvare il documento PDF.

   * Richiama il metodo `getProtectedDoc` dell&#39;oggetto `RMSecureDocumentResult` per ottenere il documento PDF protetto tramite policy. Questo metodo restituisce un oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `java.io.File` e assicurarsi che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `getProtectedDoc`).

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Trasmettere un valore stringa che specifica il WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF a cui viene applicato un criterio.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la dimensione della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Applica una policy esistente al documento PDF.

   Applicare una policy al documento PDF richiamando il metodo `protectDocument` dell&#39;oggetto `RightsManagementServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene il documento PDF a cui viene applicato il criterio.
   * Valore stringa che specifica il nome del documento.
   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Valore stringa che specifica il nome del criterio.
   * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere `null`).
   * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore del parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro precedente deve essere `null`).
   * Valore `RMLocale` che specifica il valore delle impostazioni locali, ad esempio `RMLocale.en`.
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore dei criteri.
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite policy.
   * Parametro di output stringa utilizzato per memorizzare il tipo MIME (ad esempio, `application/pdf`).

   Il metodo `protectDocument` restituisce un oggetto `BLOB` contenente il documento PDF protetto tramite policy.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto tramite policy.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `protectDocument`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (MTOM): applicazione di una policy a un documento PDF tramite l’API del servizio web&quot;
* &quot;Guida rapida (SwaRef): applicazione di una policy a un documento PDF tramite l’API del servizio web&quot;

## Rimozione di criteri dai documenti di PDF {#removing-policies-from-pdf-documents}

È possibile rimuovere una policy da un documento protetto tramite policy per rimuovere la protezione dal documento. In altre parole, se non desideri più che il documento sia protetto da una policy. Se si desidera aggiornare un documento protetto tramite policy con una policy più recente, invece di rimuovere la policy e aggiungere la policy aggiornata, è più efficiente cambiare la policy.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

È possibile rimuovere una policy da un documento PDF protetto tramite policy a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39;autorizzazione `SWITCH_POLICY` per rimuovere un criterio da un documento PDF. Inoltre, anche l’utente specificato nelle impostazioni di connessione di AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento di PDF non protetto**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF protetto tramite policy.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF protetto tramite policy utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi il criterio dal documento PDF.

   * Creare un oggetto `DocumentManager` richiamando il metodo `getDocumentManager` dell&#39;oggetto `DocumentSecurityClient`.
   * Rimuovere un criterio dal documento PDF richiamando il metodo `removeSecurity` dell&#39;oggetto `DocumentManager` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF protetto tramite criteri. Questo metodo restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un oggetto `java.io.File` e assicurarsi che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeSecurity`).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): rimozione di una policy da un documento PDF tramite l’API Java&quot;

### Rimuovere un criterio utilizzando l’API del servizio web {#remove-a-policy-using-the-web-service-api}

Rimuovi una policy da un documento PDF protetto tramite policy utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF protetto tramite policy.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento PDF protetto tramite policy da cui viene rimosso il criterio.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Rimuovi il criterio dal documento PDF.

   Rimuovere il criterio dal documento PDF richiamando il metodo `removePolicySecurity` dell&#39;oggetto `DocumentSecurityServiceClient` e passando l&#39;oggetto `BLOB` che contiene il documento PDF protetto tramite criteri. Questo metodo restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removePolicySecurity`. Compilare la matrice di byte ottenendo il valore del campo `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF protetto tramite policy

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF protetto tramite policy utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Revoca del documento protetto tramite policy

   * Creare un oggetto `DocumentManager` richiamando il metodo `getDocumentManager` dell&#39;oggetto `DocumentSecurityClient`.
   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite policy richiamando il metodo `getLicenseId` dell&#39;oggetto `DocumentManager`. Passa l&#39;oggetto `com.adobe.idp.Document` che rappresenta il documento protetto tramite policy. Questo metodo restituisce un valore stringa che rappresenta il valore dell&#39;identificatore di licenza.
   * Creare un oggetto `LicenseManager` richiamando il metodo `getLicenseManager` dell&#39;oggetto `DocumentSecurityClient`.
   * Revocare il documento protetto tramite policy richiamando il metodo `revokeLicense` dell&#39;oggetto `LicenseManager` e passando i valori seguenti:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite policy (specificare il valore restituito del metodo `getLicenseId` dell&#39;oggetto `DocumentManager`).
      * Membro dati statico dell&#39;interfaccia `License` che specifica il motivo della revoca del documento. Ad esempio, è possibile specificare `License.DOCUMENT_REVISED`.
      * Valore `java.net.URL` che specifica il percorso in cui si trova un documento revisionato. Se non desideri reindirizzare un utente a un altro URL, puoi passare `null`.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): revoca di un documento tramite API Java&quot;

### Revoca dell’accesso ai documenti tramite l’API del servizio web {#revoke-access-to-documents-using-the-web-service-api}

Revoca dell’accesso a un documento PDF protetto tramite policy utilizzando Document Security API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di Document Security

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF protetto tramite policy

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare un documento PDF protetto tramite policy revocato.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto tramite policy da revocare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Revoca del documento protetto tramite policy

   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite policy richiamando il metodo `getLicenseID` dell&#39;oggetto `DocumentSecurityServiceClient` e passando l&#39;oggetto `BLOB` che rappresenta il documento protetto tramite policy. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore della licenza.
   * Revocare il documento protetto tramite policy richiamando il metodo `revokeLicense` dell&#39;oggetto `DocumentSecurityServiceClient` e passando i valori seguenti:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite policy (specificare il valore restituito del metodo `getLicenseId` dell&#39;oggetto `DocumentSecurityServiceService`).
      * Membro dati statico dell&#39;enumerazione `Reason` che specifica il motivo della revoca del documento. Ad esempio, è possibile specificare `Reason.DOCUMENT_REVISED`.
      * Valore `string` che specifica la posizione URL in cui si trova un documento revisionato. Se non desideri reindirizzare un utente a un altro URL, puoi passare `null`.

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per ripristinare l&#39;accesso a un documento di PDF revocato, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.
1. Ripristinare l&#39;accesso al documento PDF revocato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se si utilizza l&#39;API Java, creare un oggetto `DocumentSecurityClient`. Se utilizzi l’API del servizio web Document Security, crea un oggetto `DocumentSecurityServiceService`.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF revocato utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.
   * Creare un oggetto `DocumentManager` richiamando il metodo `getDocumentManager` dell&#39;oggetto `DocumentSecurityClient`.
   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo `getLicenseId` dell&#39;oggetto `DocumentManager` e passando l&#39;oggetto `com.adobe.idp.Document` che rappresenta il documento revocato. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore della licenza.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Creare un oggetto `LicenseManager` richiamando il metodo `getLicenseManager` dell&#39;oggetto `DocumentSecurityClient`.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo `unrevokeLicense` dell&#39;oggetto `LicenseManager` e passando il valore dell&#39;identificatore di licenza del documento revocato.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): ripristino dell’accesso a un documento revocato tramite l’API del servizio web&quot;

### Ripristinare l’accesso ai documenti revocati tramite l’API del servizio web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Ripristinare l’accesso a un documento revocato utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare un documento PDF revocato a cui viene ripristinato l&#39;accesso.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF revocato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo `getLicenseID` dell&#39;oggetto `DocumentSecurityServiceClient` e passando l&#39;oggetto `BLOB` che rappresenta il documento revocato. Questo metodo restituisce un valore stringa che rappresenta l&#39;identificatore della licenza.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo `unrevokeLicense` dell&#39;oggetto `DocumentSecurityServiceClient` e passando un valore stringa che specifica il valore dell&#39;identificatore di licenza del documento PDF revocato (passare il valore restituito del metodo `getLicenseId` dell&#39;oggetto `DocumentSecurityServiceClient`).

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per esaminare un documento PDF protetto tramite policy, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Recuperare un documento protetto tramite policy da esaminare.
1. Ottenere informazioni sul documento protetto tramite policy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, crea un oggetto client del servizio Document Security. Se si utilizza l&#39;API Java, creare un oggetto `RightsManagementClient`. Se utilizzi l’API del servizio web Document Security, crea un oggetto `RightsManagementServiceService`.

**Recuperare un documento protetto tramite policy da ispezionare**

Per esaminare un documento protetto tramite policy, recuperalo. Se si tenta di ispezionare un documento non protetto con una policy o revocato, viene generata un&#39;eccezione.

**Inspect il documento**

Dopo aver recuperato un documento protetto tramite policy, è possibile esaminarlo.

**Ottieni informazioni sul documento protetto tramite policy**

Dopo aver esaminato un documento PDF protetto tramite policy, puoi ottenere informazioni al riguardo. È ad esempio possibile determinare il criterio utilizzato per proteggere il documento.

Se si protegge un documento con un criterio che appartiene a Criteri utente e si chiama `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, verrà restituito null.

Se il documento è protetto utilizzando un criterio contenuto in un set di criteri (diverso da Criteri personali), `RMInspectResult.getPolicysetName` e `RMInspectResult.getPolicysetId` restituiscono stringhe valide.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documenti di Inspect Policy Protected PDF tramite l’API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect è un documento PDF protetto tramite policy utilizzando Document Security Service API (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java. Per informazioni sul percorso di questi file, vedere [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento protetto tramite policy da esaminare.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF protetto tramite policy utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Inspect il documento.

   * Creare un oggetto `DocumentManager` richiamando il metodo `getDocumentManager` dell&#39;oggetto `RightsManagementClient`.
   * Inspect ha protetto il documento tramite policy richiamando il metodo `inspectDocument` dell&#39;oggetto `LicenseManager`. Passa l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF protetto tramite policy. Questo metodo restituisce un oggetto `RMInspectResult` contenente informazioni sul documento protetto tramite policy.

1. Ottenere informazioni sul documento protetto tramite policy.

   Per ottenere informazioni sul documento protetto tramite policy, richiamare il metodo appropriato che appartiene all&#39;oggetto `RMInspectResult`. Ad esempio, per recuperare il nome del criterio, richiamare il metodo `getPolicyName` dell&#39;oggetto `RMInspectResult`.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): ispezione dei documenti PDF protetti tramite policy tramite l’API Java&quot;

### Documenti di Inspect Policy Protected PDF che utilizzano l’API del servizio web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect è un documento PDF protetto tramite policy utilizzando l’API Document Security Service (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento protetto tramite policy da esaminare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF da verificare.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso per la lettura.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Inspect il documento.

   Inspect ha protetto il documento tramite policy richiamando il metodo `inspectDocument` dell&#39;oggetto `RightsManagementServiceClient`. Passa l&#39;oggetto `BLOB` che contiene il documento PDF protetto tramite policy. Questo metodo restituisce un oggetto `RMInspectResult` contenente informazioni sul documento protetto tramite policy.

1. Ottenere informazioni sul documento protetto tramite policy.

   Per ottenere informazioni sul documento protetto tramite policy, ottenere il valore del campo appropriato che appartiene all&#39;oggetto `RMInspectResult`. Ad esempio, per recuperare il nome del criterio, ottenere il valore del campo `policyName` dell&#39;oggetto `RMInspectResult`.

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per creare una filigrana, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Document Security.
1. Impostare gli attributi delle filigrane.
1. Registra la filigrana presso il servizio Document Security.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Document Security**

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se si utilizza l&#39;API Java, creare un oggetto `RightsManagementClient`. Se utilizzi l’API del servizio web Document Security, crea un oggetto `RightsManagementServiceService`.

**Imposta gli attributi delle filigrane**

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
   <td><p>Se questo valore è specificato, <code>WaterBackCmd:IS_SIZE_ENABLED</code> deve essere presente e il valore deve essere true. Se questo attributo non è specificato, il comportamento predefinito è Adatta alla pagina.</p></td>
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
   <td><p>Specifica il testo personalizzato per una filigrana. Se questo valore è presente, anche <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> deve essere presente e impostato su true.</p></td>
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

**Registra filigrana**

Prima di poter essere utilizzata, una nuova filigrana deve essere registrata presso il servizio Document Security. Dopo aver registrato una filigrana, puoi utilizzarla all’interno dei criteri.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione delle policy ai documenti di PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creare filigrane utilizzando l’API Java {#create-watermarks-using-the-java-api}

Crea una filigrana utilizzando Document Security API (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio `adobe-rightsmanagement-client.jar`, nel percorso di classe del progetto Java.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Imposta attributi filigrana

   * Creare un oggetto `Watermark` richiamando il metodo `createWatermark` statico dell&#39;oggetto `InfomodelObjectFactory`. Questo metodo restituisce un oggetto `Watermark`.
   * Impostare l&#39;attributo name della filigrana richiamando il metodo `setName` dell&#39;oggetto `Watermark` e passando un valore stringa che specifica il nome del criterio.
   * Impostare l&#39;attributo background della filigrana richiamando il metodo `setBackground` dell&#39;oggetto `Watermark` e passando `true`. Impostando questo attributo, la filigrana viene visualizzata sullo sfondo del documento.
   * Impostare l&#39;attributo di testo personalizzato della filigrana richiamando il metodo `setCustomText` dell&#39;oggetto `Watermark` e passando un valore stringa che rappresenta il testo della filigrana.
   * Impostare l&#39;attributo di opacità della filigrana richiamando il metodo `setOpacity` dell&#39;oggetto `Watermark` e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che è completamente trasparente.

1. Registrare la filigrana.

   * Creare un oggetto `WatermarkManager` richiamando il metodo `getWatermarkManager` dell&#39;oggetto `RightsManagementClient`. Questo metodo restituisce un oggetto `WatermarkManager`.
   * Registrare la filigrana richiamando il metodo `registerWatermark` dell&#39;oggetto `WatermarkManager` e passando l&#39;oggetto `Watermark` che rappresenta la filigrana da registrare. Questo metodo restituisce un valore stringa che rappresenta il valore di identificazione della filigrana.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Quick Starts (Avvio rapido) seguente:

* &quot;Guida rapida (modalità SOAP): creazione di una filigrana tramite l’API Java&quot;

### Creare filigrane utilizzando l’API del servizio web {#create-watermarks-using-the-web-service-api}

Crea una filigrana utilizzando Document Security API (servizio web):

1. Crea un oggetto API client di Document Security.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Impostare gli attributi della filigrana.

   * Creare un oggetto `WatermarkSpec` richiamando il costruttore `WatermarkSpec`.
   * Impostare il nome della filigrana assegnando un valore stringa al membro dati `name` dell&#39;oggetto `WatermarkSpec`.
   * Impostare l&#39;attributo `id` della filigrana assegnando un valore stringa al membro dati `id` dell&#39;oggetto `WatermarkSpec`.
   * Per ogni proprietà filigrana da impostare, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` separato.
   * Impostare il valore chiave assegnando un valore al membro dati `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` (ad esempio, `WaterBackCmd:OPACITY)`.
   * Impostare il valore assegnando un valore al membro dati `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, ad esempio `.25`.
   * Creare un oggetto `MyArrayOf_xsd_anyType`. Per ogni oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, richiamare il metodo `Add` dell&#39;oggetto `MyArrayOf_xsd_anyType`. Passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare l&#39;oggetto `MyArrayOf_xsd_anyType` al membro dati `values` dell&#39;oggetto `WatermarkSpec`.

1. Registrare la filigrana.

   Registrare la filigrana richiamando il metodo `registerWatermark` dell&#39;oggetto `RightsManagementServiceClient` e passando l&#39;oggetto `WatermarkSpec` che rappresenta la filigrana da registrare.

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire un’operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se si utilizza l&#39;API Java, creare un oggetto `DocumentSecurityClient`. Se utilizzi l’API del servizio web Document Security, crea un oggetto `DocumentSecurityServiceService`.

**Recupera la filigrana da modificare**

Per modificare una filigrana, è necessario recuperarne una esistente. È possibile recuperare una filigrana specificandone il nome o specificandone il valore di identificatore.

**Imposta gli attributi delle filigrane**

Per modificare una filigrana esistente, modificare il valore di uno o più attributi della filigrana. Quando si aggiorna una filigrana a livello di programmazione utilizzando un servizio Web, è necessario impostare tutti gli attributi impostati in origine, anche se il valore non cambia. Si supponga, ad esempio, che siano impostati i seguenti attributi di filigrana: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` e `WaterBackCmd:SRCTEXT`. Sebbene l&#39;unico attributo che si desidera modificare sia `WaterBackCmd:OPACITY`, è necessario impostare gli altri valori in modo corretto.

>[!NOTE]
>
>Quando si utilizza l’API Java per modificare una filigrana, non è necessario specificare tutti gli attributi. Impostare l&#39;attributo della filigrana che si desidera modificare.

>[!NOTE]
>
>Per informazioni sui nomi degli attributi della filigrana, vedere [Creazione delle filigrane](protecting-documents-policies.md#creating-watermarks).

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperate la filigrana da modificare.

   Creare un oggetto `WatermarkManager` richiamando il metodo `getWatermarkManager` dell&#39;oggetto `DocumentSecurityClient` e passare un valore stringa che specifichi il nome della filigrana. Questo metodo restituisce un oggetto `Watermark` che rappresenta la filigrana da modificare.

1. Impostare gli attributi della filigrana.

   Impostare l&#39;attributo di opacità della filigrana richiamando il metodo `setOpacity` dell&#39;oggetto `Watermark` e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che è completamente trasparente.

   >[!NOTE]
   >
   >In questo esempio viene modificato solo l&#39;attributo di opacità.

1. Aggiorna la filigrana.

   * Aggiornare la filigrana richiamando il metodo `updateWatermark` dell&#39;oggetto `WatermarkManager` e passare l&#39;oggetto `Watermark` il cui attributo è stato modificato.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la sezione Guida rapida (modalità SOAP): modifica di una filigrana tramite API Java.

### Modificare le filigrane utilizzando l’API del servizio web {#modify-watermarks-using-the-web-service-api}

Modifica una filigrana utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperate la filigrana da modificare.

   Recuperare la filigrana da modificare richiamando il metodo `getWatermarkByName` dell&#39;oggetto `DocumentSecurityServiceClient`. Passa un valore stringa che specifica il nome della filigrana. Questo metodo restituisce un oggetto `WatermarkSpec` che rappresenta la filigrana da modificare.

1. Impostare gli attributi della filigrana.

   * Per ogni proprietà filigrana da aggiornare, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` separato.
   * Impostare il valore chiave assegnando un valore al membro dati `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` (ad esempio, `WaterBackCmd:OPACITY)`.
   * Impostare il valore assegnando un valore al membro dati `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, ad esempio `.50`.
   * Creare un oggetto `MyArrayOf_xsd_anyType`. Per ogni oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, richiamare il metodo `Add` dell&#39;oggetto `MyArrayOf_xsd_anyType`. Passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare l&#39;oggetto `MyArrayOf_xsd_anyType` al membro dati `values` dell&#39;oggetto `WatermarkSpec`.

1. Aggiorna la filigrana.

   Aggiornare la filigrana richiamando il metodo `updateWatermark` dell&#39;oggetto `DocumentSecurityServiceClient` e passando l&#39;oggetto `WatermarkSpec` che rappresenta la filigrana da modificare.

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
>Per ulteriori informazioni sul servizio di Rights Management, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-10}

Per cercare un evento di Rights Management, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Rights Management.
1. Specifica l’evento per il quale eseguire la ricerca.
1. Cerca l’evento.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Crea un oggetto API client di Rights Management**

Prima di poter eseguire un&#39;operazione del servizio di Rights Management a livello di programmazione, è necessario creare un oggetto client del servizio di Rights Management. Se si utilizza l&#39;API Java, creare un oggetto `DocumentSecurityClient`. Se si utilizza l&#39;API del servizio Web di Rights Management, creare un oggetto `DocumentSecurityServiceService`.

**Specificare gli eventi da cercare**

Specifica l’evento da cercare. Ad esempio, è possibile cercare l’evento di creazione del criterio, che si verifica quando viene creato un nuovo criterio.

**Cerca evento**

Dopo aver specificato l’evento da cercare, puoi utilizzare l’API Java di Rights Management o l’API del servizio web di Rights Management per cercare l’evento.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cercare gli eventi utilizzando l’API Java {#search-for-events-using-the-java-api}

Cerca gli eventi utilizzando l’API di Rights Management (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creazione di un oggetto API client di Rights Management

   Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare gli eventi da cercare

   * Creare un oggetto `EventManager` richiamando il metodo `getEventManager` dell&#39;oggetto `DocumentSecurityClient`. Questo metodo restituisce un oggetto `EventManager`.
   * Creare un oggetto `EventSearchFilter` richiamando il relativo costruttore.
   * Specificare l&#39;evento per il quale eseguire la ricerca richiamando il metodo `setEventCode` dell&#39;oggetto `EventSearchFilter` e passando un membro dati statico appartenente alla classe `EventManager` che rappresenta l&#39;evento per il quale eseguire la ricerca. Ad esempio, per cercare l&#39;evento di creazione dei criteri, passare `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >È possibile definire ulteriori criteri di ricerca richiamando `EventSearchFilter` metodi di oggetto. Ad esempio, richiamare il metodo `setUserName` per specificare un utente associato all&#39;evento.

1. Cerca l’evento

   Cercare l&#39;evento richiamando il metodo `searchForEvents` dell&#39;oggetto `EventManager` e passando l&#39;oggetto `EventSearchFilter` che definisce i criteri di ricerca dell&#39;evento. Questo metodo restituisce una matrice di `Event` oggetti.

**Esempi di codice**

Per esempi di codice relativi all&#39;utilizzo del servizio di Rights Management, vedere la Guida introduttiva seguente:

* &quot;Guida rapida (SOAP): ricerca di eventi tramite l’API Java&quot;

### Cercare gli eventi utilizzando l’API del servizio web {#search-for-events-using-the-web-service-api}

Cerca gli eventi utilizzando l’API di Rights Management (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creazione di un oggetto API client di Rights Management

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Specificare gli eventi da cercare

   * Creare un oggetto `EventSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;inizio del periodo di tempo durante il quale si è verificato l&#39;evento impostando il membro dati `firstTime.date` dell&#39;oggetto `EventSpec` con istanza `DataTime` che rappresenta l&#39;inizio dell&#39;intervallo di date in cui si è verificato l&#39;evento.
   * Assegnare il valore `true` al membro dati `firstTime.dateSpecified` dell&#39;oggetto `EventSpec`.
   * Specificare la fine del periodo di tempo durante il quale si è verificato l&#39;evento impostando il membro dati `lastTime.date` dell&#39;oggetto `EventSpec` con istanza `DataTime` che rappresenta la fine dell&#39;intervallo di date in cui si è verificato l&#39;evento.
   * Assegnare il valore `true` al membro dati `lastTime.dateSpecified` dell&#39;oggetto `EventSpec`.
   * Impostare l&#39;evento da cercare assegnando un valore stringa al membro dati `eventCode` dell&#39;oggetto `EventSpec`. Nella tabella seguente sono elencati i valori numerici che è possibile assegnare a questa proprietà:

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

   Cercare l&#39;evento richiamando il metodo `searchForEvents` dell&#39;oggetto `DocumentSecurityServiceClient` e passando l&#39;oggetto `EventSpec` che rappresenta l&#39;evento per il quale eseguire la ricerca e il numero massimo di risultati. Questo metodo restituisce un insieme `MyArrayOf_xsd_anyType` in cui ogni elemento è un&#39;istanza `AuditSpec`. Utilizzando un&#39;istanza di `AuditSpec`, è possibile ottenere informazioni sull&#39;evento, ad esempio l&#39;ora in cui si è verificato. L&#39;istanza `AuditSpec` contiene un membro dati `timestamp` che specifica queste informazioni.

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
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Applicare un criterio esistente al documento di Word**

Per applicare un criterio a un documento di Word, è necessario fare riferimento a un criterio esistente e specificare il set di criteri a cui appartiene il criterio. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verificherà un&#39;eccezione.

**Salva documento di Word**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento di Word.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento di Word utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento di Word.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Applicare una policy esistente al documento di Word.

   * Creare un oggetto `DocumentManager` richiamando il metodo `getDocumentManager` dell&#39;oggetto `DocumentSecurityClient`.
   * Applicare una policy al documento di Word richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentManager` e passando i valori seguenti:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento di Word a cui viene applicato il criterio.
      * Valore stringa che specifica il nome del documento.
      * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Valore stringa che specifica il nome del criterio.
      * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere null).
      * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore del parametro è facoltativo e può essere `null` (se il parametro è `null`, il valore del parametro precedente deve essere `null`).
      * `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni locali utilizzate per la selezione del modello di MS Office. Il valore di questo parametro è facoltativo ed è possibile specificare `null`.

     Il metodo `protectDocument` restituisce un oggetto `RMSecureDocumentResult` che contiene il documento Word protetto tramite policy.

1. Salvare il documento di Word.

   * Richiama il metodo `getProtectedDoc` dell&#39;oggetto `RMSecureDocumentResult` per ottenere il documento Word protetto tramite policy. Questo metodo restituisce un oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `java.io.File` e assicurarsi che l&#39;estensione del file sia DOC.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `getProtectedDoc`).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (modalità SOAP): applicazione di una policy a un documento Word tramite l’API Java&quot;

### Applicare una policy a un documento Word utilizzando l’API del servizio web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Applicare una policy a un documento di Word utilizzando Document Security API (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto API client di Document Security.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento di Word.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento di Word a cui è applicato un criterio.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento di Word e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la dimensione della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Applicare una policy esistente al documento di Word.

   Applicare una policy al documento di Word richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentSecurityServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene il documento di Word a cui viene applicato il criterio.
   * Valore stringa che specifica il nome del documento.
   * Valore stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Valore stringa che specifica il nome del criterio.
   * Valore string che rappresenta il nome del dominio del gestore utenti dell&#39;utente che è l&#39;autore del documento. Il valore di questo parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro successivo deve essere `null`).
   * Valore stringa che rappresenta il nome canonico dell&#39;utente responsabile dell&#39;utente che è l&#39;autore del documento. Il valore del parametro è facoltativo e può essere null (se il parametro è null, il valore del parametro precedente deve essere `null`).
   * Valore `RMLocale` che specifica il valore delle impostazioni locali, ad esempio `RMLocale.en`.
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore dei criteri.
   * Parametro di output stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite policy.
   * Parametro di output stringa utilizzato per memorizzare il tipo MIME (ad esempio, `application/doc`).

   Il metodo `protectDocument` restituisce un oggetto `BLOB` che contiene il documento Word protetto tramite policy.

1. Salvare il documento di Word.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento Word protetto tramite policy.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `protectDocument`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file di Word richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (MTOM): applicazione di una policy a un documento Word tramite l’API del servizio web&quot;

## Rimozione di criteri da documenti di Word {#removing-policies-from-word-documents}

È possibile rimuovere una policy da un documento Word protetto tramite policy per rimuovere la protezione dal documento. In altre parole, se non desideri più che il documento sia protetto da una policy. Se si desidera aggiornare un documento Word protetto tramite policy con una policy più recente, invece di rimuovere la policy e aggiungere la policy aggiornata, è più efficiente cambiare la policy.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consulta [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Rimuovi il criterio dal documento di Word**

È possibile rimuovere una policy da un documento Word protetto tramite policy a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39;autorizzazione `SWITCH_POLICY` per rimuovere un criterio da un documento di Word. Inoltre, anche l’utente specificato nelle impostazioni di connessione di AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento Word protetto tramite policy

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento Word protetto tramite policy utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento Word.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere la policy dal documento di Word

   * Creare un oggetto `DocumentManager` richiamando il metodo `getDocumentManager` dell&#39;oggetto `RightsManagementClient`.
   * Rimuovere una policy dal documento di Word richiamando il metodo `removeSecurity` dell&#39;oggetto `DocumentManager` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento di Word protetto tramite policy. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che contiene un documento di Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un oggetto `java.io.File` e assicurarsi che l&#39;estensione del file sia DOC.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeSecurity`).

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (modalità SOAP): rimozione di una policy da un documento Word tramite l’API Java&quot;

### Rimuovere una policy da un documento di Word utilizzando l’API del servizio web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Rimuovi una policy da un documento Word protetto tramite policy utilizzando Document Security API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di Document Security

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento Word protetto tramite policy

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento Word protetto tramite policy da cui viene rimossa la policy.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento di Word e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Rimuovere la policy dal documento di Word

   Rimuovere la policy dal documento di Word richiamando il metodo `removePolicySecurity` dell&#39;oggetto `RightsManagementServiceClient` e passando l&#39;oggetto `BLOB` che contiene il documento di Word protetto tramite policy. Questo metodo restituisce un oggetto `BLOB` che contiene un documento di Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento di Word non protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removePolicySecurity`. Compilare la matrice di byte ottenendo il valore del campo `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Esempi di codice**

Per esempi di codice con il servizio Document Security, consulta la Guida introduttiva seguente:

* &quot;Guida rapida (MTOM): rimozione di una policy da un documento Word tramite l’API del servizio web&quot;

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
