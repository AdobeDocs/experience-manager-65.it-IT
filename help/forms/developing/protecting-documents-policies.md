---
title: Protezione dei documenti con i criteri
seo-title: Protezione dei documenti con i criteri
description: Il servizio Document Security consente di applicare in modo dinamico le impostazioni per la salvaguardia della riservatezza  documenti Adobe PDF e di mantenere il controllo sui documenti. Il servizio Document Security consente inoltre agli utenti di controllare in che modo i destinatari utilizzano il documento PDF protetto tramite criterio.
seo-description: Il servizio Document Security consente di applicare in modo dinamico le impostazioni per la salvaguardia della riservatezza  documenti Adobe PDF e di mantenere il controllo sui documenti. Il servizio Document Security consente inoltre agli utenti di controllare in che modo i destinatari utilizzano il documento PDF protetto tramite criterio.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '15558'
ht-degree: 0%

---


# Protezione dei documenti con criteri {#protecting-documents-with-policies}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

**Informazioni su Document Security Service**

Il servizio Document Security consente agli utenti di applicare dinamicamente le impostazioni di riservatezza ai documenti  Adobe PDF e di mantenere il controllo sui documenti, indipendentemente dalla loro diffusione.

Il servizio Document Security impedisce che le informazioni si diffondano oltre la portata dell&#39;utente consentendo agli utenti di mantenere il controllo sul modo in cui i destinatari utilizzano il documento PDF protetto tramite criterio. Un utente può specificare chi può aprire un documento, limitare il suo utilizzo e monitorare il documento dopo averlo distribuito. Un utente può inoltre controllare in modo dinamico l&#39;accesso a un documento protetto tramite criterio e può revocare l&#39;accesso al documento anche in modo dinamico.

Il servizio Document Security protegge anche altri tipi di file come i file Microsoft Word (file DOC). Potete utilizzare l&#39;API client di Document Security per lavorare con questi tipi di file. Sono supportate le versioni seguenti:

* File di Microsoft Office 2003 (file DOC, XLS, PPT)
* File di Microsoft Office 2007 (DOCX, XLSX, PPTX)
* PTC Pro/E, file

Per maggiore chiarezza, nelle due sezioni seguenti viene illustrato come utilizzare i documenti Word:

* [Applicazione dei criteri ai documenti Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Rimozione di criteri dai documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Potete eseguire le seguenti attività utilizzando il servizio Document Security:

* Creare criteri. Per informazioni, vedere [Creazione di criteri](protecting-documents-policies.md#creating-policies).
* Modificare i criteri. Per informazioni, vedere [Modifica dei criteri](protecting-documents-policies.md#modifying-policies).
* Eliminare i criteri. Per informazioni, vedere [Eliminazione dei criteri](protecting-documents-policies.md#deleting-policies).
* Applicare criteri ai documenti PDF. Per ulteriori informazioni, vedere [Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Rimuovere i criteri dai documenti PDF. Per ulteriori informazioni, vedere [Rimozione di criteri dai documenti PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
*  documenti protetti tramite criterio Inspect. Per ulteriori informazioni, vedere [Analisi dei documenti PDF protetti tramite criterio](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revoca l&#39;accesso ai documenti PDF. Per informazioni, vedere [Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents).
* Ripristinare l&#39;accesso ai documenti revocati. Per ulteriori informazioni, vedere [Ripristino dell&#39;accesso ai documenti revisionati](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Creare filigrane. Per informazioni, vedere [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).
* Cercare gli eventi. Per informazioni, vedere [Ricerca di eventi](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di criteri {#creating-policies}

Potete creare criteri a livello di programmazione utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Una *policy* è una raccolta di informazioni che include le impostazioni di protezione dei documenti, gli utenti autorizzati e i diritti di utilizzo. Potete creare e salvare un numero qualsiasi di criteri, utilizzando le impostazioni di protezione appropriate per situazioni e utenti diversi.

I criteri consentono di eseguire le operazioni seguenti:

* Specificate gli utenti che possono aprire il documento. I destinatari possono appartenere o essere esterni all&#39;organizzazione.
* Specificare il modo in cui i destinatari possono utilizzare il documento. Potete limitare l&#39;accesso a  diverse funzioni di Acrobat e  Adobe Reader. Queste funzioni includono la possibilità di stampare e copiare il testo, aggiungere firme e aggiungere commenti a un documento.
* Modificate le impostazioni di accesso e protezione in qualsiasi momento, anche dopo la distribuzione del documento protetto tramite criterio.
* Monitorare l’uso del documento dopo averlo distribuito. È possibile vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

### Creazione di un criterio tramite i servizi Web {#creating-a-policy-using-web-services}

Quando create un criterio utilizzando l&#39;API del servizio Web, fate riferimento a un file XML PDF (Portable Document Rights Language) esistente che descrive il criterio. Le autorizzazioni per i criteri e l&#39;entità sono definite nel documento PDRL. Il seguente documento XML è un esempio di documento PDRL.

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
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un criterio, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Impostate gli attributi del criterio.
1. Creare una voce del criterio.
1. Registra il criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-rightsmanagement-client.jar
* namespace.jar (se  AEM Forms è distribuito su JBoss)
* jaxb-api.jar (se  AEM Forms è distribuito su JBoss)
* jaxb-impl.jar (se  AEM Forms è distribuito su JBoss)
* jaxb-libs.jar (se  AEM Forms è distribuito su JBoss)
* jaxb-xjc.jar (se  AEM Forms è distribuito su JBoss)
* relaxngData.jar (se  AEM Forms è distribuito su JBoss)
* xsdlib.jar (se  AEM Forms è distribuito su JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilizzate un file JAR diverso se  AEM Forms non è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client Document Security**

Prima di eseguire un&#39;operazione del servizio Document Security a livello di programmazione, create un oggetto client del servizio Document Security.

**Impostare gli attributi del criterio**

Per creare un criterio, impostate gli attributi del criterio. Un attributo obbligatorio è il nome del criterio. I nomi dei criteri devono essere univoci per ciascun set di criteri. Un set di criteri è semplicemente una raccolta di criteri. Possono essere presenti due criteri con lo stesso nome se i criteri appartengono a set di criteri separati. Tuttavia, due criteri all&#39;interno di un singolo set di criteri non possono avere lo stesso nome.

Un altro attributo utile da impostare è il periodo di validità. Un periodo di validità è il periodo di tempo durante il quale un documento protetto tramite criterio è accessibile ai destinatari autorizzati. Se non impostate questo attributo, il criterio è sempre valido.

Un periodo di validità può essere impostato su una delle seguenti opzioni:

* Numero impostato di giorni in cui il documento è accessibile a partire dal momento in cui viene pubblicato
* Una data di fine dopo la quale il documento non è accessibile
* Un intervallo di date specifico per il quale il documento è accessibile
* Always valid

È possibile specificare solo una data di inizio, che determina la validità del criterio dopo la data di inizio. Se si specifica solo una data di fine, il criterio è valido fino alla data di fine. Tuttavia, viene generata un&#39;eccezione se non sono definite sia una data di inizio che una data di fine.

Quando impostate gli attributi che appartengono a un criterio, potete anche impostare le impostazioni di cifratura. Queste impostazioni di cifratura hanno effetto quando il criterio viene applicato a un documento. È possibile specificare i seguenti valori di cifratura:

* **AES256**: Rappresenta l’algoritmo di cifratura AES con una chiave a 256 bit.
* **AES128**: Rappresenta l’algoritmo di cifratura AES con una chiave a 128 bit.
* **NoEncryption:** Non rappresenta la cifratura.

Quando si specifica l&#39;opzione `NoEncryption`, non è possibile impostare l&#39;opzione `PlaintextMetadata` su `false`. Se tentate di farlo, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per informazioni su altri attributi che è possibile impostare, vedete la descrizione dell&#39;interfaccia `Policy` in [ AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Creare una voce di criterio**

Una voce di criterio associa entità, che sono gruppi e utenti, e autorizzazioni a un criterio. Un criterio deve avere almeno una voce del criterio. Si supponga, ad esempio, di eseguire le seguenti operazioni:

* Create e registrate una voce del criterio che consente a un gruppo di visualizzare solo un documento mentre è in linea e impedisce ai destinatari di copiarlo.
* Associate l&#39;immissione dei criteri al criterio.
* Proteggere un documento con il criterio utilizzando  Acrobat.

Queste azioni consentono ai destinatari di visualizzare il documento solo online e non di copiarlo. Il documento rimane protetto finché non viene rimossa la protezione.

**Registrazione del criterio**

Per poter utilizzare un nuovo criterio, è necessario registrarlo. Dopo aver registrato un criterio, potete utilizzarlo per proteggere i documenti.

### Creare un criterio utilizzando l&#39;API Java {#create-a-policy-using-the-java-api}

Create un criterio utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostate gli attributi del criterio.

   * Creare un oggetto `Policy` richiamando il metodo statico `InfomodelObjectFactory` dell&#39;oggetto `createPolicy`. Questo metodo restituisce un oggetto `Policy`.
   * Impostate l&#39;attributo nome del criterio richiamando il metodo `setName` dell&#39;oggetto `Policy` e passando un valore di stringa che specifica il nome del criterio.
   * Impostate la descrizione del criterio richiamando il metodo `setDescription` dell&#39;oggetto `Policy` e passando un valore di stringa che specifica la descrizione del criterio.
   * Impostare il set di criteri a cui appartiene il nuovo criterio richiamando il metodo `setPolicySetName` dell&#39;oggetto `Policy` e passando un valore di stringa che specifica il nome del set di criteri. (È possibile specificare `null` per questo valore di parametro che determina l&#39;aggiunta del criterio al set di criteri *My Policies*.)
   * Creare il periodo di validità del criterio richiamando il metodo statico `InfomodelObjectFactory` dell&#39;oggetto `createValidityPeriod`. Questo metodo restituisce un oggetto `ValidityPeriod`.
   * Impostare il numero di giorni per i quali un documento protetto tramite criterio è accessibile richiamando il metodo `ValidityPeriod` dell&#39;oggetto `setRelativeExpirationDays` e passando un valore intero che specifica il numero di giorni.
   * Impostare il periodo di validità del criterio richiamando il metodo `setValidityPeriod` dell&#39;oggetto `ValidityPeriod` e passando l&#39;oggetto `Policy`.

1. Creare una voce del criterio.

   * Creare una voce di criterio richiamando il metodo statico `createPolicyEntry` dell&#39;oggetto `InfomodelObjectFactory`. Questo metodo restituisce un oggetto `PolicyEntry`.
   * Specificare le autorizzazioni del criterio richiamando il metodo statico `InfomodelObjectFactory` dell&#39;oggetto `createPermission`. Passa un membro di dati statici appartenente all&#39;interfaccia `Permission` che rappresenta l&#39;autorizzazione. Questo metodo restituisce un oggetto `Permission`. Ad esempio, per aggiungere l&#39;autorizzazione che consente agli utenti di copiare dati da un documento PDF protetto tramite criterio, passare `Permission.COPY`. Ripetete questo passaggio per ogni autorizzazione da aggiungere.
   * Aggiungete l&#39;autorizzazione alla voce del criterio richiamando il metodo `addPermission` dell&#39;oggetto `Permission` e passando l&#39;oggetto `PolicyEntry`. (Ripetere questo passaggio per ogni oggetto `Permission` creato).
   * Creare l&#39;entità del criterio richiamando il metodo statico `createSpecialPrincipal` dell&#39;oggetto `InfomodelObjectFactory`. Passa un membro di dati appartenente all&#39;oggetto `InfomodelObjectFactory` che rappresenta l&#39;entità. Questo metodo restituisce un oggetto `Principal`. Ad esempio, per aggiungere l&#39;editore del documento come entità, passare `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Aggiungete l&#39;entità alla voce del criterio richiamando il metodo `setPrincipal` dell&#39;oggetto `Principal` e passando l&#39;oggetto `PolicyEntry`.
   * Aggiungete la voce del criterio richiamando il metodo `addPolicyEntry` dell&#39;oggetto `PolicyEntry` e passando l&#39;oggetto `Policy`.

1. Registra il criterio.

   * Creare un oggetto `PolicyManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getPolicyManager`.
   * Registra il criterio richiamando il metodo `PolicyManager` dell&#39;oggetto `registerPolicy` e passando i seguenti valori:

      * L&#39;oggetto `Policy` che rappresenta il criterio da registrare.
   * Una stringa che rappresenta il set di criteri a cui appartiene il criterio.

   Se nelle impostazioni di connessione si utilizza un account amministratore di moduli AEM per creare l&#39;oggetto `DocumentSecurityClient`, specificare il nome del set di criteri quando si richiama il metodo `registerPolicy`. Se si passa un valore `null` per il set di criteri, il criterio viene creato nel set di criteri *Criteri personali* degli amministratori.

   Se utilizzate un utente di Document Security nelle impostazioni di connessione, potete richiamare il metodo sovraccarico `registerPolicy` che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri personali*. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome di set di criteri quando si richiama il metodo `registerPolicy`.

   >[!NOTE]
   >
   >Quando create un criterio, fate riferimento a un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice che utilizzano il servizio Document Security, consultate quanto segue:

* &quot;Avvio rapido (modalità SOAP): Creazione di un criterio tramite l&#39;API Java&quot;

### Creare un criterio utilizzando l&#39;API del servizio Web {#create-a-policy-using-the-web-service-api}

Create un criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Impostate gli attributi del criterio.

   * Creare un oggetto `PolicySpec` utilizzando il relativo costruttore.
   * Impostate il nome del criterio assegnando un valore stringa al membro di dati `PolicySpec` dell&#39;oggetto `name`.
   * Impostate la descrizione del criterio assegnando un valore stringa al membro di dati `PolicySpec` dell&#39;oggetto `description`.
   * Impostare il criterio a cui apparterrà il criterio assegnando un valore stringa al membro di dati `PolicySpec` dell&#39;oggetto `policySetName`. È necessario specificare un nome di set di criteri esistente. (È possibile specificare `null` per questo valore di parametro che determina l&#39;aggiunta del criterio a *My Policies*.)
   * Impostare il periodo di tempo consentito per il criterio offline assegnando un valore intero al membro di dati `PolicySpec` dell&#39;oggetto `offlineLeasePeriod`.
   * Impostare il membro di dati `PolicySpec` dell&#39;oggetto `policyXml` con un valore di stringa che rappresenta i dati XML PDRL. Per eseguire questa operazione, creare un oggetto .NET `StreamReader` utilizzando il relativo costruttore. Trasmettere la posizione di un file PDRL XML che rappresenta il criterio al costruttore `StreamReader`. Quindi, richiamare il metodo `StreamReader` dell&#39;oggetto `ReadLine` e assegnare il valore restituito a una variabile di stringa. Iterate l&#39;oggetto `StreamReader` fino a quando il metodo `ReadLine` restituisce null. Assegnare la variabile stringa al membro di dati `PolicySpec` dell&#39;oggetto `policyXml`.

1. Creare una voce del criterio.

   Non è necessario creare una voce del criterio al momento della creazione di un criterio tramite l&#39;API del servizio Web di Document Security. La voce del criterio è definita nel documento PDF.

1. Registra il criterio.

   Registra il criterio richiamando il metodo `DocumentSecurityServiceClient` dell&#39;oggetto `registerPolicy` e passando i seguenti valori:

   * L&#39;oggetto `PolicySpec` che rappresenta il criterio da registrare.
   * Una stringa che rappresenta il set di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;aggiunta del criterio al set di criteri *MyPolices*.

   Se per creare l&#39;oggetto `DocumentSecurityClient` si utilizza un account amministratore di moduli AEM all&#39;interno delle impostazioni di connessione, specificare il nome del set di criteri quando si richiama il metodo `registerPolicy`.

   Se utilizzate un utente Document Security all&#39;interno delle impostazioni di connessione, potete richiamare il metodo sovraccarico `registerPolicy` che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri personali*. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome di set di criteri quando si richiama il metodo `registerPolicy`.

   >[!NOTE]
   >
   >Quando create un criterio e specificate un set di criteri, accertatevi di specificare un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Creazione di un criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Creazione di un criterio tramite l&#39;API del servizio Web&quot;

## Modifica dei criteri {#modifying-policies}

Potete modificare un criterio esistente utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Per apportare modifiche a un criterio esistente, è necessario recuperarlo, modificarlo e quindi aggiornare il criterio sul server. Ad esempio, si supponga di recuperare un criterio esistente e di estenderne il periodo di validità. Prima che la modifica abbia effetto, è necessario aggiornare il criterio.

Potete modificare un criterio quando i requisiti aziendali cambiano e il criterio non riflette più tali requisiti. Invece di creare un nuovo criterio, potete semplicemente aggiornare un criterio esistente.

Per modificare gli attributi del criterio utilizzando un servizio Web (ad esempio, utilizzando classi proxy Java create con JAX-WS), è necessario verificare che il criterio sia registrato con il servizio Document Security. Potete quindi fare riferimento al criterio esistente utilizzando il metodo `PolicySpec.getPolicyXml` e modificare gli attributi del criterio utilizzando i metodi applicabili. Ad esempio, potete modificare il periodo di tempo consentito per l&#39;utilizzo non in linea richiamando il metodo `PolicySpec.setOfflineLeasePeriod`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per modificare un criterio esistente, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare un criterio esistente.
1. Modificare gli attributi dei criteri.
1. Aggiornare il criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione Document Security Service a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un oggetto `RightsManagementClient`. Se utilizzate l&#39;API del servizio Web di Document Security, create un oggetto `RightsManagementServiceService`.

**Recuperare un criterio esistente**

È necessario recuperare un criterio esistente per modificarlo. Per recuperare un criterio, specificate il nome del criterio e il set al quale il criterio appartiene. Se si specifica un valore `null` per il nome del set di criteri, il criterio viene recuperato dal set di criteri *Criteri personali*.

**Impostare gli attributi del criterio**

Per modificare un criterio, modificate il valore degli attributi del criterio. L&#39;unico attributo di criterio che non potete modificare è l&#39;attributo name. Ad esempio, per modificare il periodo di tempo consentito dal criterio per l&#39;utilizzo non in linea, potete modificare il valore dell&#39;attributo del periodo consentito non in linea del criterio.

Quando si modifica il periodo di tempo consentito per un criterio offline utilizzando un servizio Web, il campo `offlineLeasePeriod` nell&#39;interfaccia `PolicySpec` viene ignorato. Per aggiornare il periodo di tempo consentito per l&#39;utilizzo non in linea, modificare l&#39;elemento `OfflineLeasePeriod` nel documento XML PDRL. Fare quindi riferimento al documento PDF XML aggiornato utilizzando il membro di dati `policyXML` dell&#39;interfaccia `PolicySpec`.

>[!NOTE]
>
>Per informazioni su altri attributi che è possibile impostare, vedete la descrizione dell&#39;interfaccia `Policy` in [ AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Aggiornare il criterio**

Prima che le modifiche apportate a un criterio vengano applicate, è necessario aggiornare il criterio con il servizio Document Security. Le modifiche ai criteri di protezione dei documenti vengono aggiornate al successivo aggiornamento della sincronizzazione del documento protetto tramite criterio con il servizio Document Security.

### Modificare i criteri esistenti utilizzando l&#39;API Java {#modify-existing-policies-using-the-java-api}

Modificate un criterio esistente utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un criterio esistente.

   * Creare un oggetto `PolicyManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getPolicyManager`.
   * Creare un oggetto `Policy` che rappresenti il criterio da aggiornare richiamando il metodo `PolicyManager` dell&#39;oggetto `getPolicy` e passando i seguenti valori&quot;

      * Una stringa che rappresenta il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Una stringa che rappresenta il nome del criterio.

1. Impostate gli attributi del criterio.

   Modificate gli attributi del criterio per soddisfare i requisiti aziendali. Ad esempio, per modificare il periodo di tempo consentito dal criterio per l&#39;utilizzo offline, richiamare il metodo `Policy` dell&#39;oggetto `setOfflineLeasePeriod`.

1. Aggiornare il criterio.

   Aggiornare il criterio richiamando il metodo `PolicyManager` dell&#39;oggetto `updatePolicy`. Passa l&#39;oggetto `Policy` che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate Avvio rapido (modalità SOAP): Modifica di un criterio tramite la sezione Java API.

### Modificare i criteri esistenti utilizzando l&#39;API del servizio Web {#modify-existing-policies-using-the-web-service-api}

Modificate un criterio esistente utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un criterio esistente.

   Creare un oggetto `PolicySpec` che rappresenti il criterio da modificare richiamando il metodo `RightsManagementServiceClient` dell&#39;oggetto `getPolicy` e passando i seguenti valori:

   * Una stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Un valore di stringa che specifica il nome del criterio.

1. Impostate gli attributi del criterio.

   Modificate gli attributi del criterio per soddisfare i requisiti aziendali.

1. Aggiornare il criterio.

   Aggiornare il criterio richiamando il metodo `updatePolicyFromSDK` dell&#39;oggetto `PolicySpec` e passando l&#39;oggetto `RightsManagementServiceClient` che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Modifica di un criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Modifica di un criterio tramite l&#39;API del servizio Web&quot;

## Eliminazione dei criteri {#deleting-policies}

Potete eliminare un criterio esistente utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Una volta eliminato, un criterio non può più essere utilizzato per proteggere i documenti. Tuttavia, i documenti protetti tramite criterio esistenti che utilizzano il criterio sono ancora protetti. Potete eliminare un criterio quando diventa disponibile un criterio più recente.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per eliminare un criterio esistente, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Creare un oggetto Document Security Client API.
1. Eliminate il criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un oggetto `RightsManagementClient`. Se utilizzate l&#39;API del servizio Web di Document Security, create un oggetto `RightsManagementServiceService`.

**Eliminare il criterio**

Per eliminare un criterio, è necessario specificare il criterio da eliminare e il set al quale il criterio appartiene. L&#39;utente le cui impostazioni sono utilizzate per richiamare  AEM Forms deve disporre dell&#39;autorizzazione per eliminare il criterio; in caso contrario si verifica un&#39;eccezione. Analogamente, se si tenta di eliminare un criterio che non esiste, si verifica un&#39;eccezione.

### Eliminare i criteri utilizzando l&#39;API Java {#delete-policies-using-the-java-api}

Eliminate un criterio utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Eliminate il criterio.

   * Creare un oggetto `PolicyManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getPolicyManager`.
   * Eliminate il criterio richiamando il metodo `PolicyManager` dell&#39;oggetto `deletePolicy` e passando i seguenti valori:

      * Una stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Un valore di stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Eliminazione di un criterio tramite l&#39;API Java&quot;

### Eliminare i criteri utilizzando l&#39;API del servizio Web {#delete-policies-using-the-web-service-api}

Eliminate un criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Eliminate il criterio.

   Per eliminare un criterio, richiamate il metodo `RightsManagementServiceClient` dell&#39;oggetto `deletePolicy` e passate i seguenti valori:

   * Una stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Un valore di stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Eliminazione di un criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Eliminazione di un criterio tramite l&#39;API del servizio Web&quot;

## Applicazione dei criteri ai documenti PDF {#applying-policies-to-pdf-documents}

È possibile applicare un criterio a un documento PDF per proteggere il documento. Applicando un criterio a un documento PDF, è possibile limitare l&#39;accesso al documento. Non è possibile applicare un criterio a un documento se il documento è già protetto con un criterio.

Mentre il documento è aperto, è inoltre possibile limitare l&#39;accesso alle  funzioni di Acrobat e  Adobe Reader, inclusa la possibilità di stampare e copiare il testo, apportare modifiche e aggiungere firme e commenti a un documento. Inoltre, è possibile revocare un documento PDF protetto tramite criterio quando non si desidera più che gli utenti accedano al documento.

È possibile monitorare l&#39;utilizzo di un documento protetto tramite criterio dopo averlo distribuito. In altre parole, potete vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per applicare un criterio a un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare un documento PDF a cui viene applicato un criterio.
1. Applicare un criterio esistente al documento PDF.
1. Salvate il documento PDF protetto tramite criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di eseguire un&#39;operazione del servizio Document Security a livello di programmazione, create un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un oggetto `DocumentSecurityClient`. Se utilizzate l&#39;API del servizio Web di Document Security, create un oggetto `DocumentSecurityServiceService`.

**Recupero di un documento PDF**

È possibile recuperare un documento PDF per applicare un criterio. Dopo aver applicato un criterio al documento PDF, gli utenti possono utilizzare il documento con restrizioni. Ad esempio, se il criterio non consente l&#39;apertura del documento offline, gli utenti devono essere online per aprire il documento.

**Applicare un criterio esistente al documento PDF**

Per applicare un criterio a un documento PDF, fare riferimento a un criterio esistente e specificare a quale set di criteri appartiene il criterio. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verifica un&#39;eccezione.

**Salvare il documento PDF**

Dopo che il servizio Document Security ha applicato un criterio a un documento PDF, potete salvare il documento PDF protetto tramite criterio come file PDF.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicazione di un criterio a un documento PDF tramite l&#39;API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Applicare un criterio a un documento PDF utilizzando l&#39;API Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Applicare un criterio esistente al documento PDF.

   * Creare un oggetto `DocumentManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getDocumentManager`.
   * Applicare un criterio al documento PDF richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentManager` e passando i seguenti valori:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF a cui viene applicato il criterio.
      * Una stringa che specifica il nome del documento.
      * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Una stringa che specifica il nome del criterio.
      * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore successivo del parametro deve essere null).
      * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere `null` (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
      * Un `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni internazionali utilizzate per selezionare il modello di MS Office. Questo valore del parametro è facoltativo e non viene utilizzato per i documenti PDF. Per proteggere un documento PDF, specificare `null`.

      Il metodo `protectDocument` restituisce un oggetto `RMSecureDocumentResult` contenente il documento PDF protetto tramite criterio.


1. Salvare il documento PDF.

   * Richiamare il metodo `RMSecureDocumentResult` dell&#39;oggetto `getProtectedDoc` per ottenere il documento PDF protetto tramite criterio. Questo metodo restituisce un oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `java.io.File` e assicurarsi che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document` (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `getProtectedDoc`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità EJB): Applicazione di un criterio a un documento PDF tramite l&#39;API Java&quot;
* &quot;Avvio rapido (modalità SOAP): Applicazione di un criterio a un documento PDF tramite l&#39;API Java&quot;

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applicazione di un criterio a un documento PDF tramite l&#39;API del servizio Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Applicare un criterio a un documento PDF utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF a cui viene applicato un criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la dimensione dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Applicare un criterio esistente al documento PDF.

   Applicare un criterio al documento PDF richiamando il metodo `protectDocument` dell&#39;oggetto `RightsManagementServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento PDF a cui viene applicato il criterio.
   * Una stringa che specifica il nome del documento.
   * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Una stringa che specifica il nome del criterio.
   * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore successivo del parametro deve essere `null`).
   * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
   * Un valore `RMLocale` che specifica il valore delle impostazioni internazionali (ad esempio, `RMLocale.en`).
   * Un parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore del criterio.
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite criterio.
   * Un parametro di output della stringa utilizzato per memorizzare il tipo mime (ad esempio, `application/pdf`).

   Il metodo `protectDocument` restituisce un oggetto `BLOB` contenente il documento PDF protetto tramite criterio.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto tramite criterio.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `protectDocument`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Applicazione di un criterio a un documento PDF tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Applicazione di un criterio a un documento PDF tramite l&#39;API del servizio Web&quot;

## Rimozione di criteri dai documenti PDF {#removing-policies-from-pdf-documents}

È possibile rimuovere un criterio da un documento protetto tramite criterio per rimuovere la protezione dal documento. Se non si desidera più che il documento sia protetto tramite un criterio. Se desiderate aggiornare un documento protetto tramite criterio con un criterio più recente, invece di rimuovere il criterio e aggiungere il criterio aggiornato, è più efficiente cambiare il criterio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per rimuovere un criterio da un documento PDF protetto tramite criterio, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Creare un oggetto Document Security Client API.
1. Recuperare un documento PDF protetto tramite criterio.
1. Rimuovere il criterio dal documento PDF.
1. Salvare il documento PDF non protetto.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di eseguire un&#39;operazione del servizio Document Security a livello di programmazione, create un oggetto client del servizio Document Security.

**Recuperare un documento PDF protetto tramite criterio**

È possibile recuperare un documento PDF protetto tramite criterio per rimuovere un criterio. Se tentate di rimuovere un criterio da un documento PDF non protetto da un criterio, causerete un&#39;eccezione.

**Rimuovere il criterio dal documento PDF**

È possibile rimuovere un criterio da un documento PDF protetto tramite criterio a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39;autorizzazione `SWITCH_POLICY` per rimuovere un criterio da un documento PDF. Inoltre, anche l&#39;utente specificato nelle impostazioni di connessione di AEM Forms  deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento PDF non protetto**

Dopo che il servizio Document Security ha rimosso un criterio da un documento PDF, potete salvare il documento PDF non protetto come file PDF.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Rimuovere un criterio da un documento PDF utilizzando l&#39;API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Rimuovere un criterio da un documento PDF protetto tramite criterio utilizzando l&#39;API Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF protetto tramite criterio.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF protetto tramite criterio utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere il criterio dal documento PDF.

   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Rimuovere un criterio dal documento PDF richiamando il metodo `removeSecurity` dell&#39;oggetto `com.adobe.idp.Document` e passando l&#39;oggetto `DocumentManager` che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un oggetto `java.io.File` e assicurarsi che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document` (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeSecurity`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Rimozione di un criterio da un documento PDF tramite l&#39;API Java&quot;

### Rimozione di un criterio tramite l&#39;API del servizio Web {#remove-a-policy-using-the-web-service-api}

Rimuovere un criterio da un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF protetto tramite criterio.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF protetto tramite criterio dal quale viene rimosso il criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere il criterio dal documento PDF.

   Rimuovere il criterio dal documento PDF richiamando il metodo `removePolicySecurity` dell&#39;oggetto `BLOB` e passando l&#39;oggetto `DocumentSecurityServiceClient` che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removePolicySecurity`. Compilare l&#39;array di byte ottenendo il valore del campo `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Rimozione di un criterio da un documento PDF tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Rimozione di un criterio da un documento PDF tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revoca dell&#39;accesso ai documenti {#revoking-access-to-documents}

È possibile revocare l&#39;accesso a un documento PDF protetto tramite criterio in modo che tutte le copie del documento non siano accessibili agli utenti. Quando un utente tenta di aprire un documento PDF revocato, viene reindirizzato a un URL specificato in cui è possibile visualizzare un documento modificato. È necessario specificare a livello di programmazione l&#39;URL al quale l&#39;utente viene reindirizzato. Quando revocate l&#39;accesso a un documento, la modifica ha effetto alla successiva sincronizzazione dell&#39;utente con il servizio Document Security aprendo il documento protetto tramite criterio online.

La capacità di revocare l&#39;accesso a un documento offre ulteriore protezione. Ad esempio, si supponga che sia disponibile una versione più recente di un documento e che non si desideri più che qualcuno visualizzi la versione obsoleta. In questa situazione, l&#39;accesso al documento precedente può essere revocato e nessuno può visualizzare il documento a meno che l&#39;accesso non venga ripristinato.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per revocare un documento protetto tramite criterio, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare un documento PDF protetto tramite criterio.
1. Revoca del documento protetto tramite criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security.

**Recuperare un documento PDF protetto tramite criterio**

È necessario recuperare un documento PDF protetto tramite criterio per revocarlo. Non è possibile revocare un documento già revocato o non protetto tramite criterio.

Se si conosce il valore dell&#39;identificatore di licenza del documento protetto tramite criterio, non è necessario recuperare il documento PDF protetto tramite criterio. Tuttavia, nella maggior parte dei casi, è necessario recuperare il documento PDF per ottenere il valore dell&#39;identificatore di licenza.

**Revoca del documento protetto tramite criterio**

Per revocare un documento protetto tramite criterio, specificate l&#39;identificatore di licenza del documento protetto tramite criterio. Inoltre, è possibile specificare l&#39;URL di un documento che l&#39;utente può visualizzare quando cerca di aprire il documento revocato. Si supponga quindi che venga revocato un documento obsoleto. Quando un utente tenta di aprire il documento revocato, visualizzerà un documento aggiornato invece del documento revocato.

>[!NOTE]
>
>Se si tenta di revocare un documento già revocato, viene generata un&#39;eccezione.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Ripristino dell&#39;accesso ai documenti revocati](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revoca l&#39;accesso ai documenti tramite l&#39;API Java {#revoke-access-to-documents-using-the-java-api}

Revocare l&#39;accesso a un documento PDF protetto tramite criterio utilizzando l&#39;API Document Security (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF protetto tramite criterio

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF protetto tramite criterio utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Revoca del documento protetto tramite criterio

   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite criterio richiamando il metodo `DocumentManager` dell&#39;oggetto `getLicenseId`. Passa l&#39;oggetto `com.adobe.idp.Document` che rappresenta il documento protetto tramite criterio. Questo metodo restituisce un valore di stringa che rappresenta il valore dell’identificatore di licenza.
   * Creare un oggetto `LicenseManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getLicenseManager`.
   * Revocare il documento protetto tramite criterio richiamando il metodo `revokeLicense` dell&#39;oggetto e passando i seguenti valori:`LicenseManager`

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite criterio (specificare il valore restituito dal metodo `DocumentManager` dell&#39;oggetto `getLicenseId`).
      * Un membro di dati statici dell&#39;interfaccia `License` che specifica il motivo della revoca del documento. Ad esempio, è possibile specificare `License.DOCUMENT_REVISED`.
      * Un valore `java.net.URL` che specifica la posizione in cui si trova un documento modificato. Se non si desidera reindirizzare un utente a un altro URL, è possibile passare `null`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Revoca di un documento tramite l&#39;API Java&quot;

### Revoca l&#39;accesso ai documenti tramite l&#39;API del servizio Web {#revoke-access-to-documents-using-the-web-service-api}

Revocare l&#39;accesso a un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto API client Document Security

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF protetto tramite criterio

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF protetto tramite criterio revocato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta il percorso del file del documento PDF protetto tramite criterio da revocare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Revoca del documento protetto tramite criterio

   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite criterio richiamando il metodo `getLicenseID` dell&#39;oggetto `BLOB` e passando l&#39;oggetto `DocumentSecurityServiceClient` che rappresenta il documento protetto tramite criterio. Questo metodo restituisce un valore di stringa che rappresenta l’identificatore della licenza.
   * Revocare il documento protetto tramite criterio richiamando il metodo `revokeLicense` dell&#39;oggetto e passando i seguenti valori:`DocumentSecurityServiceClient`

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite criterio (specificare il valore restituito dal metodo `DocumentSecurityServiceService` dell&#39;oggetto `getLicenseId`).
      * Un membro di dati statici dell&#39;enum `Reason` che specifica il motivo della revoca del documento. Ad esempio, è possibile specificare `Reason.DOCUMENT_REVISED`.
      * Un valore `string` che specifica la posizione dell&#39;URL in cui si trova il documento rivisto. Se non si desidera reindirizzare un utente a un altro URL, è possibile passare `null`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Revoca di un documento tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Revoca di un documento tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Rimozione di criteri dai documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ripristino dell&#39;accesso ai documenti revisionati {#reinstating-access-to-revoked-documents}

È possibile ripristinare l&#39;accesso a un documento PDF revocato, in modo che tutte le copie del documento revocato siano accessibili agli utenti. Quando un utente apre un documento ripristinato revocato, può visualizzare il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per ripristinare l&#39;accesso a un documento PDF revocato, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.
1. Ripristinare l&#39;accesso al documento PDF revocato.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un oggetto `DocumentSecurityClient`. Se utilizzate l&#39;API del servizio Web di Document Security, create un oggetto `DocumentSecurityServiceService`.

**Recuperare l&#39;identificatore di licenza del documento PDF revocato**

Per ripristinare un documento PDF revocato, è necessario recuperare l’identificatore di licenza del documento PDF revocato. Dopo aver ottenuto il valore dell&#39;identificatore di licenza, potete ripristinare un documento revocato. Se si tenta di ripristinare un documento che non viene revocato, verrà generata un&#39;eccezione.

**Ripristino dell&#39;accesso al documento PDF revocato**

Per ripristinare l&#39;accesso a un documento PDF revocato, è necessario specificare l&#39;identificatore di licenza del documento revocato. Se si tenta di ripristinare l&#39;accesso a un documento PDF non revocato, si verificherà un&#39;eccezione.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Ripristino dell&#39;accesso ai documenti revocati tramite l&#39;API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Ripristinate l&#39;accesso a un documento revocato utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF revocato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.
   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo `getLicenseId` dell&#39;oggetto `com.adobe.idp.Document` e passando l&#39;oggetto `DocumentManager` che rappresenta il documento revocato. Questo metodo restituisce un valore di stringa che rappresenta l’identificatore della licenza.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Creare un oggetto `LicenseManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getLicenseManager`.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo `unrevokeLicense` dell&#39;oggetto `LicenseManager` e passando il valore dell&#39;identificatore di licenza del documento revocato.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Ripristino dell&#39;accesso a un documento revocato tramite l&#39;API del servizio Web&quot;

### Ripristino dell&#39;accesso ai documenti revocati tramite l&#39;API del servizio Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Ripristinate l&#39;accesso a un documento revocato utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF revocato al quale viene ripristinato l&#39;accesso.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta il percorso del file del documento PDF revocato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo `getLicenseID` dell&#39;oggetto `BLOB` e passando l&#39;oggetto `DocumentSecurityServiceClient` che rappresenta il documento revocato. Questo metodo restituisce un valore di stringa che rappresenta l’identificatore della licenza.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo `unrevokeLicense` dell&#39;oggetto `DocumentSecurityServiceClient` e passando un valore di stringa che specifica il valore dell&#39;identificatore di licenza del documento PDF revocato (passare il valore restituito dal metodo `DocumentSecurityServiceClient` dell&#39;oggetto `getLicenseId`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Ripristino dell&#39;accesso a un documento revocato tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ripristino dell&#39;accesso a un documento revocato tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica dei documenti PDF protetti tramite criterio {#inspecting-policy-protected-pdf-documents}

Potete utilizzare l&#39;API di Document Security Service (Java e il servizio Web) per ispezionare i documenti PDF protetti tramite criterio. L&#39;ispezione dei documenti PDF protetti tramite criterio restituisce informazioni sul documento PDF protetto tramite criterio. È possibile, ad esempio, determinare il criterio utilizzato per proteggere il documento e la data in cui il documento è stato protetto.

Non potete eseguire questa operazione se la versione dell&#39;LiveCycle in uso è 8.x o precedente. In  AEM Forms viene aggiunto il supporto per l&#39;ispezione di documenti protetti tramite criterio. Se tentate di ispezionare un documento protetto tramite criterio utilizzando l&#39;LiveCycle 8.x (o versioni precedenti), viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per esaminare un documento PDF protetto tramite criterio, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare un documento protetto tramite criterio da esaminare.
1. Ottenete informazioni sul documento protetto tramite criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di eseguire un&#39;operazione del servizio Document Security a livello di programmazione, create un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un oggetto `RightsManagementClient`. Se utilizzate l&#39;API del servizio Web di Document Security, create un oggetto `RightsManagementServiceService`.

**Recuperare un documento protetto tramite criterio da esaminare**

Per esaminare un documento protetto tramite criterio, recuperatelo. Se tentate di ispezionare un documento non protetto con un criterio o revocato, viene generata un&#39;eccezione.

**Inspect il documento**

Dopo aver recuperato un documento protetto tramite criterio, potete controllarlo.

**Ottenere informazioni sul documento protetto tramite criterio**

Dopo aver esaminato un documento PDF protetto tramite criterio, potete ottenere informazioni su di esso. Ad esempio, è possibile determinare il criterio utilizzato per proteggere il documento.

Se si protegge un documento con un criterio che appartiene a Criteri personali e quindi si chiama `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, viene restituito null.

Se il documento è protetto tramite un criterio contenuto in un set di criteri (diverso da Criteri personali), `RMInspectResult.getPolicysetName` e `RMInspectResult.getPolicysetId` restituiscono stringhe valide.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

###  documenti PDF protetti tramite criterio Inspect utilizzando l&#39;API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

 ad Inspect un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento protetto tramite criterio da esaminare.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF protetto tramite criterio utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1.  Inspect il documento.

   * Creare un oggetto `DocumentManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getDocumentManager`.
   *  Inspect al documento protetto tramite criterio richiamando il metodo `LicenseManager` dell&#39;oggetto `inspectDocument`. Passa l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un oggetto `RMInspectResult` che contiene informazioni sul documento protetto tramite criterio.

1. Ottenete informazioni sul documento protetto tramite criterio.

   Per ottenere informazioni sul documento protetto tramite criterio, richiamare il metodo appropriato che appartiene all&#39;oggetto `RMInspectResult`. Ad esempio, per recuperare il nome del criterio, richiamare il metodo `RMInspectResult` dell&#39;oggetto `getPolicyName`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Ispezione dei documenti PDF protetti tramite criterio tramite l&#39;API Java&quot;

###  documenti PDF protetti tramite criterio Inspect utilizzando l&#39;API del servizio Web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

 ad Inspect un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento protetto tramite criterio da esaminare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF da esaminare.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Trasmettere l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1.  Inspect il documento.

    Inspect al documento protetto tramite criterio richiamando il metodo `RightsManagementServiceClient` dell&#39;oggetto `inspectDocument`. Passa l&#39;oggetto `BLOB` che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un oggetto `RMInspectResult` che contiene informazioni sul documento protetto tramite criterio.

1. Ottenete informazioni sul documento protetto tramite criterio.

   Per ottenere informazioni sul documento protetto tramite criterio, ottenere il valore del campo appropriato che appartiene all&#39;oggetto `RMInspectResult`. Ad esempio, per recuperare il nome del criterio, ottenere il valore del campo `RMInspectResult` dell&#39;oggetto `policyName`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Ispezione dei documenti PDF protetti tramite criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ispezione dei documenti PDF protetti tramite criterio tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di filigrane {#creating-watermarks}

Le filigrane garantiscono la sicurezza di un documento identificando in modo univoco il documento e controllando la violazione del copyright. Ad esempio, è possibile creare e inserire una filigrana con l&#39;indicazione Riservato su tutte le pagine di un documento. Dopo la creazione di una filigrana, potete includerla come parte di un criterio. In altre parole, potete impostare l&#39;attributo della filigrana del criterio con la filigrana appena creata. Dopo che un criterio contenente una filigrana è stato applicato a un documento, la filigrana viene visualizzata nel documento protetto tramite criterio.

>[!NOTE]
>
>Le filigrane possono essere create solo dagli utenti con privilegi di amministratore Document Security. In altre parole, è necessario specificare tale utente quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per creare una filigrana, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Impostare gli attributi delle filigrane.
1. Registra la filigrana con il servizio Document Security.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un oggetto `RightsManagementClient`. Se utilizzate l&#39;API del servizio Web di Document Security, create un oggetto `RightsManagementServiceService`.

**Impostare gli attributi delle filigrane**

Per creare una nuova filigrana, è necessario impostare gli attributi della filigrana. L&#39;attributo name deve sempre essere definito. Oltre all&#39;attributo name, è necessario impostare almeno uno dei seguenti attributi:

* Testo personalizzato
* DateIncluso
* UserIdInclused
* NomeUtenteIncluso

Nella tabella seguente sono elencate le coppie chiave-valore richieste per la creazione di una filigrana tramite i servizi Web.

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
   <td><p>Se questo valore è true, il valore del testo personalizzato deve essere specificato utilizzando <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Specifica l’opacità della filigrana. Il valore predefinito è 0,5 se non è specificato.</p></td>
   <td><p>Un valore compreso tra 0,0 e 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Specifica la rotazione della filigrana. Il valore predefinito è 0 gradi.</p></td>
   <td><p>Un valore compreso tra 0 e 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Se questo valore viene specificato, <code>WaterBackCmd:IS_SIZE_ENABLED</code> deve essere presente e il valore deve essere true. Se questo attributo non è specificato, il comportamento predefinito è adatto alla pagina.</p></td>
   <td><p>Un valore maggiore di 0.0 e inferiore o uguale a 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Specifica l'allineamento orizzontale della filigrana. Il valore predefinito è center.</p></td>
   <td><p>a sinistra, al centro o a destra</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Specifica l'allineamento verticale della filigrana. Il valore predefinito è center.</p></td>
   <td><p>top, center o bottom</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Specifica se la filigrana è uno sfondo. Il valore predefinito è false.</p></td>
   <td><p>True o False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True se viene specificata una scala personalizzata. Se questo valore è true, è necessario specificare anche SCALE. Se questo valore è false, il valore predefinito è adatto alla pagina.</p></td>
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

**Registrazione della filigrana**

Prima di poter essere utilizzata, è necessario registrare una nuova filigrana con il servizio Document Security. Dopo aver registrato una filigrana, è possibile utilizzarla all&#39;interno dei criteri.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creare filigrane utilizzando l&#39;API Java {#create-watermarks-using-the-java-api}

Create una filigrana utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete i file JAR client, ad esempio `adobe-rightsmanagement-client.jar`, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare gli attributi della filigrana

   * Creare un oggetto `Watermark` richiamando il metodo statico `InfomodelObjectFactory` dell&#39;oggetto `createWatermark`. Questo metodo restituisce un oggetto `Watermark`.
   * Impostate l&#39;attributo nome della filigrana richiamando il metodo `setName` dell&#39;oggetto `Watermark` e passando un valore di stringa che specifica il nome del criterio.
   * Impostare l&#39;attributo di sfondo della filigrana richiamando il metodo `setBackground` dell&#39;oggetto `true` e passando `Watermark`. Impostando questo attributo, la filigrana viene visualizzata sullo sfondo del documento.
   * Impostare l&#39;attributo di testo personalizzato della filigrana richiamando il metodo `setCustomText` dell&#39;oggetto `Watermark` e passando un valore di stringa che rappresenta il testo della filigrana.
   * Impostare l&#39;attributo di opacità della filigrana richiamando il metodo `setOpacity` dell&#39;oggetto `Watermark` e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che la filigrana è completamente trasparente.

1. Registra la filigrana.

   * Creare un oggetto `WatermarkManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getWatermarkManager`. Questo metodo restituisce un oggetto `WatermarkManager`.
   * Registrare la filigrana richiamando il metodo `registerWatermark` dell&#39;oggetto `Watermark` e passando l&#39;oggetto `WatermarkManager` che rappresenta la filigrana da registrare. Questo metodo restituisce un valore di stringa che rappresenta il valore di identificazione della filigrana.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Creazione di una filigrana mediante l&#39;API Java&quot;

### Creare filigrane utilizzando l&#39;API del servizio Web {#create-watermarks-using-the-web-service-api}

Create una filigrana utilizzando l&#39;API di Document Security (servizio Web):

1. Creare un oggetto Document Security Client API.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Impostate gli attributi della filigrana.

   * Creare un oggetto `WatermarkSpec` richiamando il costruttore `WatermarkSpec`.
   * Impostare il nome della filigrana assegnando un valore stringa al membro di dati `WatermarkSpec` dell&#39;oggetto `name`.
   * Impostare l&#39;attributo della filigrana `id` assegnando un valore stringa al membro di dati `WatermarkSpec` dell&#39;oggetto `id`.
   * Per ogni proprietà della filigrana da impostare, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` separato.
   * Impostare il valore chiave assegnando un valore al membro di dati `key` dell&#39;oggetto `WaterBackCmd:OPACITY)` (ad esempio, `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Impostare il valore assegnando un valore al membro di dati `value` dell&#39;oggetto `.25` (ad esempio, `MyMapOf_xsd_string_To_xsd_anyType_Item`).
   * Creare un oggetto `MyArrayOf_xsd_anyType`. Per ciascun oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, richiamare il metodo `MyArrayOf_xsd_anyType` dell&#39;oggetto `Add`. Passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare l&#39;oggetto `MyArrayOf_xsd_anyType` al membro di dati `WatermarkSpec` dell&#39;oggetto `values`.

1. Registra la filigrana.

   Registrare la filigrana richiamando il metodo `registerWatermark` dell&#39;oggetto `WatermarkSpec` e passando l&#39;oggetto `RightsManagementServiceClient` che rappresenta la filigrana da registrare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Creazione di una filigrana mediante l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Creazione di una filigrana mediante l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica delle filigrane {#modifying-watermarks}

Potete modificare una filigrana esistente utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Per apportare modifiche a una filigrana esistente, recuperarla, modificarne gli attributi e quindi aggiornarla sul server. Ad esempio, supponete di recuperare una filigrana e modificarne l’attributo di opacità. Prima che la modifica abbia effetto, è necessario aggiornare la filigrana.

Quando modificate una filigrana, la modifica ha effetto sui documenti futuri a cui è stata applicata la filigrana. In altre parole, i documenti PDF esistenti contenenti la filigrana non vengono modificati.

>[!NOTE]
>
>Le filigrane possono essere modificate solo dagli utenti con diritti di amministratore di Document Security. In altre parole, è necessario specificare tale utente quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-9}

Per modificare una filigrana, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperate la filigrana da modificare.
1. Impostare gli attributi delle filigrane.
1. Aggiorna la filigrana.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un oggetto `DocumentSecurityClient`. Se utilizzate l&#39;API del servizio Web di Document Security, create un oggetto `DocumentSecurityServiceService`.

**Recuperare la filigrana da modificare**

Per modificare una filigrana, è necessario recuperare una filigrana esistente. È possibile recuperare una filigrana specificandone il nome o il valore identificativo.

**Impostare gli attributi delle filigrane**

Per modificare una filigrana esistente, modificate il valore di uno o più attributi della filigrana. Quando si aggiorna una filigrana a livello di programmazione utilizzando un servizio Web, è necessario impostare tutti gli attributi impostati originariamente, anche se il valore non cambia. Ad esempio, si supponga che siano impostati i seguenti attributi di filigrana: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` e `WaterBackCmd:SRCTEXT`. Anche se l&#39;unico attributo che si desidera modificare è `WaterBackCmd:OPACITY`, è necessario impostare anche gli altri valori.

>[!NOTE]
>
>Quando utilizzate l&#39;API Java per modificare una filigrana, non è necessario specificare tutti gli attributi. Impostate l’attributo della filigrana da modificare.

>[!NOTE]
>
>Per informazioni sui nomi degli attributi delle filigrane, vedere [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).

**Aggiornare la filigrana**

Dopo aver modificato gli attributi di una filigrana, è necessario aggiornare la filigrana.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Creazione di filigrane](protecting-documents-policies.md#creating-watermarks)

### Modificare le filigrane utilizzando l&#39;API Java {#modify-watermarks-using-the-java-api}

Modificare una filigrana utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperate la filigrana da modificare.

   Creare un oggetto `WatermarkManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getWatermarkManager` e passando un valore di stringa che specifica il nome della filigrana. Questo metodo restituisce un oggetto `Watermark` che rappresenta la filigrana da modificare.

1. Impostate gli attributi della filigrana.

   Impostare l&#39;attributo di opacità della filigrana richiamando il metodo `setOpacity` dell&#39;oggetto `Watermark` e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che la filigrana è completamente trasparente.

   >[!NOTE]
   >
   >In questo esempio viene modificato solo l’attributo opacità.

1. Aggiorna la filigrana.

   * Aggiornare la filigrana richiamando il metodo `updateWatermark` dell&#39;oggetto `Watermark` e passando l&#39;oggetto `WatermarkManager` il cui attributo è stato modificato.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate Avvio rapido (modalità SOAP): Modifica di una filigrana tramite la sezione Java API.

### Modificare le filigrane utilizzando l&#39;API del servizio Web {#modify-watermarks-using-the-web-service-api}

Modificare una filigrana utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperate la filigrana da modificare.

   Recuperare la filigrana da modificare richiamando il metodo `getWatermarkByName` dell&#39;oggetto `DocumentSecurityServiceClient`. Passa un valore di stringa che specifica il nome della filigrana. Questo metodo restituisce un oggetto `WatermarkSpec` che rappresenta la filigrana da modificare.

1. Impostate gli attributi della filigrana.

   * Per ogni proprietà della filigrana da aggiornare, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` separato.
   * Impostare il valore chiave assegnando un valore al membro di dati `key` dell&#39;oggetto `WaterBackCmd:OPACITY)` (ad esempio, `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Impostare il valore assegnando un valore al membro di dati `value` dell&#39;oggetto `.50` (ad esempio, `MyMapOf_xsd_string_To_xsd_anyType_Item`).
   * Creare un oggetto `MyArrayOf_xsd_anyType`. Per ciascun oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`, richiamare il metodo `MyArrayOf_xsd_anyType` dell&#39;oggetto `Add`. Passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare l&#39;oggetto `MyArrayOf_xsd_anyType` al membro di dati `WatermarkSpec` dell&#39;oggetto `values`.

1. Aggiorna la filigrana.

   Aggiornare la filigrana richiamando il metodo `updateWatermark` dell&#39;oggetto `WatermarkSpec` e passando l&#39;oggetto `DocumentSecurityServiceClient` che rappresenta la filigrana da modificare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (MTOM): Modifica di una filigrana mediante l&#39;API del servizio Web&quot;

## Ricerca di eventi {#searching-for-events}

Il servizio Rights Management tiene traccia delle azioni specifiche eseguite, ad esempio l&#39;applicazione di un criterio a un documento, l&#39;apertura di un documento protetto tramite criterio e la revoca dell&#39;accesso ai documenti. Il controllo degli eventi deve essere abilitato per il servizio di Rights Management o gli eventi non vengono tracciati.

Gli eventi rientrano in una delle seguenti categorie:

* Gli eventi di amministratore sono azioni correlate a un amministratore, ad esempio la creazione di un nuovo account di amministratore.
* Gli eventi del documento sono azioni correlate a un documento, ad esempio la chiusura di un documento protetto tramite criterio.
* Gli eventi dei criteri sono azioni correlate a un criterio, ad esempio la creazione di un nuovo criterio.
* Gli eventi di servizio sono azioni correlate al servizio di Rights Management, ad esempio la sincronizzazione con la directory utente.

Potete cercare eventi specifici utilizzando l&#39;API Java di Rights Management o l&#39;API del servizio Web. Cercando gli eventi, è possibile eseguire attività quali la creazione di un file di registro di determinati eventi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di Rights Management, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-10}

Per cercare un evento di Rights Management, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client API Rights Management.
1. Specificate l&#39;evento per il quale eseguire la ricerca.
1. Cercate l’evento.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Rights Management**

Prima di eseguire un&#39;operazione di servizio Rights Management a livello di programmazione, è necessario creare un oggetto client di servizio Rights Management. Se utilizzate l&#39;API Java, create un oggetto `DocumentSecurityClient`. Se utilizzate l&#39;API del servizio Web di Rights Management, create un oggetto `DocumentSecurityServiceService`.

**Specificare gli eventi da cercare**

È necessario specificare l&#39;evento da cercare. Ad esempio, è possibile cercare l&#39;evento policy create, che si verifica quando viene creato un nuovo criterio.

**Ricerca dell’evento**

Dopo aver specificato l&#39;evento da cercare, potete utilizzare l&#39;API Java di Rights Management o l&#39;API del servizio Web di Rights Management per cercare l&#39;evento.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cercare eventi utilizzando l&#39;API Java {#search-for-events-using-the-java-api}

Cercare eventi utilizzando l&#39;API Rights Management (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Rights Management

   Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Specificare gli eventi da cercare

   * Creare un oggetto `EventManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getEventManager`. Questo metodo restituisce un oggetto `EventManager`.
   * Creare un oggetto `EventSearchFilter` richiamandone il costruttore.
   * Specificare l&#39;evento per il quale eseguire la ricerca richiamando il metodo `setEventCode` dell&#39;oggetto e passando un membro di dati statico appartenente alla classe `EventManager` che rappresenta l&#39;evento per il quale eseguire la ricerca. `EventSearchFilter` Ad esempio, per cercare l&#39;evento di creazione del criterio, passare `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >È possibile definire criteri di ricerca aggiuntivi richiamando i metodi dell&#39;oggetto `EventSearchFilter`. Ad esempio, invocate il metodo `setUserName` per specificare un utente associato all&#39;evento.

1. Ricerca dell’evento

   Cercare l&#39;evento richiamando il metodo `searchForEvents` dell&#39;oggetto `EventSearchFilter` e passando l&#39;oggetto `EventManager` che definisce i criteri di ricerca dell&#39;evento. Questo metodo restituisce un array di oggetti `Event`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio di Rights Management, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (SOAP): Ricerca di eventi tramite l&#39;API Java&quot;

### Cercare eventi utilizzando l&#39;API del servizio Web {#search-for-events-using-the-web-service-api}

Cercare eventi utilizzando l&#39;API Rights Management (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto API client Rights Management

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Specificare gli eventi da cercare

   * Creare un oggetto `EventSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;inizio del periodo di tempo durante il quale si è verificato l&#39;evento impostando il membro di dati `firstTime.date` dell&#39;oggetto `DataTime` con l&#39;istanza `EventSpec` che rappresenta l&#39;inizio dell&#39;intervallo di date in cui si è verificato l&#39;evento.
   * Assegnare il valore `true` al membro di dati `EventSpec` dell&#39;oggetto `firstTime.dateSpecified`.
   * Specificare la fine del periodo di tempo durante il quale si è verificato l&#39;evento impostando il membro di dati `lastTime.date` dell&#39;oggetto `DataTime` con l&#39;istanza `EventSpec` che rappresenta la fine dell&#39;intervallo di date in cui si è verificato l&#39;evento.
   * Assegnare il valore `true` al membro di dati `EventSpec` dell&#39;oggetto `lastTime.dateSpecified`.
   * Impostare l&#39;evento da cercare assegnando un valore stringa al membro di dati `eventCode` dell&#39;oggetto `EventSpec`. Nella tabella seguente sono elencati i valori numerici che è possibile assegnare a questa proprietà:

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

1. Ricerca dell’evento

   Cercare l&#39;evento richiamando il metodo `DocumentSecurityServiceClient` dell&#39;oggetto `searchForEvents` e passando l&#39;oggetto `EventSpec` che rappresenta l&#39;evento per il quale eseguire la ricerca e il numero massimo di risultati. Questo metodo restituisce un insieme `MyArrayOf_xsd_anyType` in cui ogni elemento è un&#39;istanza `AuditSpec`. Utilizzando un&#39;istanza `AuditSpec`, potete ottenere informazioni sull&#39;evento, ad esempio l&#39;ora in cui si è verificato. L&#39;istanza `AuditSpec` contiene un membro di dati `timestamp` che specifica queste informazioni.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio di Rights Management, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Ricerca di eventi tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ricerca di eventi tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Applicazione dei criteri ai documenti di Word {#applying-policies-to-word-documents}

Oltre ai documenti PDF, il servizio Rights Management supporta anche formati di documenti aggiuntivi, ad esempio documenti Microsoft Word (DOC) e altri formati di file Microsoft Office. Ad esempio, è possibile applicare un criterio a un documento Word per proteggerlo. Applicando un criterio a un documento Word, si limita l&#39;accesso al documento. Non è possibile applicare un criterio a un documento se il documento è già protetto con un criterio.

È possibile monitorare l&#39;utilizzo di un documento Word protetto tramite criterio dopo averlo distribuito. In altre parole, potete vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-11}

Per applicare un criterio a un documento di Word, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare un documento Word a cui viene applicato un criterio.
1. Applicare un criterio esistente al documento Word.
1. Salvare il documento Word protetto tramite criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security.

**Recupero di un documento di Word**

Per applicare un criterio è necessario recuperare un documento Word. Dopo aver applicato un criterio al documento Word, gli utenti possono utilizzare il documento con restrizioni. Ad esempio, se il criterio non consente l&#39;apertura del documento offline, gli utenti devono essere online per aprire il documento.

**Applicare un criterio esistente al documento Word**

Per applicare un criterio a un documento Word, è necessario fare riferimento a un criterio esistente e specificare a quale set di criteri appartiene il criterio. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verifica un&#39;eccezione.

**Salvare il documento di Word**

Dopo che il servizio Document Security applica un criterio a un documento Word, potete salvare il documento Word protetto tramite criterio come file DOC.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicare un criterio a un documento Word utilizzando l&#39;API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Applicate un criterio a un documento Word utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocumentSecurityClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento Word.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento Word utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento Word.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Applicare un criterio esistente al documento Word.

   * Creare un oggetto `DocumentManager` richiamando il metodo `DocumentSecurityClient` dell&#39;oggetto `getDocumentManager`.
   * Applicare un criterio al documento Word richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentManager` e passando i seguenti valori:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento Word a cui viene applicato il criterio.
      * Una stringa che specifica il nome del documento.
      * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
      * Una stringa che specifica il nome del criterio.
      * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore successivo del parametro deve essere null).
      * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere `null` (se questo parametro è `null`, il valore del parametro precedente deve essere `null`).
      * Un `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni internazionali utilizzate per selezionare il modello di MS Office. Questo valore del parametro è facoltativo ed è possibile specificare `null`.

      Il metodo `protectDocument` restituisce un oggetto `RMSecureDocumentResult` contenente il documento Word protetto tramite criterio.


1. Salvare il documento Word.

   * Richiamare il metodo `RMSecureDocumentResult` dell&#39;oggetto `getProtectedDoc` per ottenere il documento Word protetto tramite criterio. Questo metodo restituisce un oggetto `com.adobe.idp.Document`.
   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del file sia DOC.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document` (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `getProtectedDoc`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Applicazione di un criterio a un documento Word tramite l&#39;API Java&quot;

### Applicazione di un criterio a un documento Word tramite l&#39;API del servizio Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Applicare un criterio a un documento Word utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un oggetto `DocumentSecurityServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DocumentSecurityServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento Word.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento Word a cui viene applicato un criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di Word e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la dimensione dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Applicare un criterio esistente al documento Word.

   Applicare un criterio al documento Word richiamando il metodo `protectDocument` dell&#39;oggetto `DocumentSecurityServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento Word a cui viene applicato il criterio.
   * Una stringa che specifica il nome del documento.
   * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. È possibile specificare un valore `null` che determina l&#39;utilizzo del set di criteri `MyPolicies`.
   * Una stringa che specifica il nome del criterio.
   * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore successivo del parametro deve essere `null`).
   * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
   * Un valore `RMLocale` che specifica il valore delle impostazioni internazionali (ad esempio, `RMLocale.en`).
   * Un parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore del criterio.
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite criterio.
   * Un parametro di output della stringa utilizzato per memorizzare il tipo mime (ad esempio, `application/doc`).

   Il metodo `protectDocument` restituisce un oggetto `BLOB` contenente il documento Word protetto tramite criterio.

1. Salvare il documento Word.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word protetto tramite criterio.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `protectDocument`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file Word richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (MTOM): Applicazione di un criterio a un documento Word tramite l&#39;API del servizio Web&quot;

## Rimozione di criteri dai documenti di Word {#removing-policies-from-word-documents}

È possibile rimuovere un criterio da un documento Word protetto tramite criterio per rimuovere la protezione dal documento. Se non si desidera più che il documento sia protetto tramite un criterio. Se si desidera aggiornare un documento Word protetto tramite criterio con un criterio più recente, invece di rimuovere il criterio e aggiungere il criterio aggiornato, è più efficiente cambiare il criterio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-12}

Per rimuovere un criterio da un documento Word protetto tramite criterio, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Creare un oggetto Document Security Client API.
1. Recuperare un documento Word protetto tramite criterio.
1. Rimuovere il criterio dal documento Word.
1. Salvare i documenti Word non protetti.s

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di eseguire un&#39;operazione del servizio Document Security a livello di programmazione, create un oggetto client del servizio Document Security.

**Recupero di un documento Word protetto tramite criterio**

Per rimuovere un criterio è necessario recuperare un documento Word protetto tramite criterio. Se tentate di rimuovere un criterio da un documento di Word che non è protetto da un criterio, causerete un&#39;eccezione.

**Rimuovere il criterio dal documento Word**

È possibile rimuovere un criterio da un documento Word protetto tramite criterio a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39;autorizzazione `SWITCH_POLICY` per rimuovere un criterio da un documento Word. Inoltre, anche l&#39;utente specificato nelle impostazioni di connessione di AEM Forms  deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento Word non protetto**

Dopo che il servizio Document Security rimuove un criterio da un documento Word, potete salvare il documento Word non protetto come file DOC.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Rimozione di un criterio da un documento Word tramite l&#39;API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Rimuovete un criterio da un documento Word protetto tramite criterio utilizzando l&#39;API di Document Security (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `RightsManagementClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupero di un documento Word protetto tramite criterio

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento Word protetto tramite criterio utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento Word.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere il criterio dal documento Word

   * Creare un oggetto `DocumentManager` richiamando il metodo `RightsManagementClient` dell&#39;oggetto `getDocumentManager`.
   * Rimuovere un criterio dal documento Word richiamando il metodo `removeSecurity` dell&#39;oggetto `com.adobe.idp.Document` e passando l&#39;oggetto `DocumentManager` che contiene il documento Word protetto tramite criterio. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che contiene un documento Word non protetto.

1. Salvare il documento Word non protetto

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del file sia DOC.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document` (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeSecurity`).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Rimozione di un criterio da un documento Word tramite l&#39;API Java&quot;

### Rimozione di un criterio da un documento di Word utilizzando l&#39;API del servizio Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Rimuovete un criterio da un documento Word protetto tramite criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto API client Document Security

   * Creare un oggetto `RightsManagementServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `RightsManagementServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `RightsManagementServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupero di un documento Word protetto tramite criterio

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento Word protetto tramite criterio dal quale viene rimosso il criterio.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di Word e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere il criterio dal documento Word

   Rimuovere il criterio dal documento Word richiamando il metodo `removePolicySecurity` dell&#39;oggetto `BLOB` e passando l&#39;oggetto `RightsManagementServiceClient` che contiene il documento Word protetto tramite criterio. Questo metodo restituisce un oggetto `BLOB` che contiene un documento Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word non protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removePolicySecurity`. Compilare l&#39;array di byte ottenendo il valore del campo `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (MTOM): Rimozione di un criterio da un documento Word tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
