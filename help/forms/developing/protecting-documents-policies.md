---
title: Protezione dei documenti con i criteri
seo-title: Protezione dei documenti con i criteri
description: 'null'
seo-description: 'null'
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '15466'
ht-degree: 0%

---


# Protezione dei documenti con i criteri {#protecting-documents-with-policies}

**Informazioni su Document Security Service**

Il servizio Document Security consente agli utenti di applicare in modo dinamico le impostazioni per la salvaguardia della riservatezza ai documenti Adobe PDF e di mantenere il controllo sui documenti, indipendentemente dalla loro diffusione.

Il servizio Document Security impedisce che le informazioni si diffondano oltre la portata dell&#39;utente consentendo agli utenti di mantenere il controllo sul modo in cui i destinatari utilizzano il documento PDF protetto tramite criterio. Un utente può specificare chi può aprire un documento, limitare il suo utilizzo e monitorare il documento dopo averlo distribuito. Un utente può inoltre controllare in modo dinamico l&#39;accesso a un documento protetto tramite criterio e può revocare l&#39;accesso al documento anche in modo dinamico.

Il servizio Document Security protegge anche altri tipi di file come i file Microsoft Word (file DOC). Potete utilizzare l&#39;API client di Document Security per lavorare con questi tipi di file. Sono supportate le versioni seguenti:

* File di Microsoft Office 2003 (DOC, XLS, PPT)
* File di Microsoft Office 2007 (DOCX, XLSX, PPTX)
* PTC Pro/E, file

Per maggiore chiarezza, nelle due sezioni seguenti viene illustrato come utilizzare i documenti Word:

* [Applicazione dei criteri ai documenti Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Rimozione di criteri dai documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Potete eseguire le seguenti attività utilizzando il servizio Document Security:

* Creare criteri. Per ulteriori informazioni, vedere [Creazione di criteri](protecting-documents-policies.md#creating-policies).
* Modificare i criteri. Per ulteriori informazioni, vedere [Modifica dei criteri](protecting-documents-policies.md#modifying-policies).
* Eliminare i criteri. Per informazioni, vedere [Eliminazione dei criteri](protecting-documents-policies.md#deleting-policies).
* Applicare criteri ai documenti PDF. Per ulteriori informazioni, vedere [Applicazione dei criteri ai documenti](protecting-documents-policies.md#applying-policies-to-pdf-documents)PDF.
* Rimuovere i criteri dai documenti PDF. Per ulteriori informazioni, vedere [Rimozione di criteri dai documenti](protecting-documents-policies.md#removing-policies-from-pdf-documents)PDF.
* Ispezionare i documenti protetti tramite criterio. Per ulteriori informazioni, vedere [Analisi dei documenti](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)PDF protetti tramite criterio.
* Revoca l&#39;accesso ai documenti PDF. Per ulteriori informazioni, vedere [Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents).
* Ripristinare l&#39;accesso ai documenti revocati. Per ulteriori informazioni, vedere [Ripristino dell&#39;accesso ai documenti](protecting-documents-policies.md#reinstating-access-to-revoked-documents)revocati.
* Creare filigrane. Per informazioni, consultate [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).
* Cercare gli eventi. Per ulteriori informazioni, vedere [Ricerca di eventi](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di criteri {#creating-policies}

Potete creare criteri a livello di programmazione utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Un *criterio* è una raccolta di informazioni che include le impostazioni di protezione dei documenti, gli utenti autorizzati e i diritti di utilizzo. Potete creare e salvare un numero qualsiasi di criteri, utilizzando le impostazioni di protezione appropriate per situazioni e utenti diversi.

I criteri consentono di eseguire le operazioni seguenti:

* Specificate gli utenti che possono aprire il documento. I destinatari possono appartenere o essere esterni all&#39;organizzazione.
* Specificare il modo in cui i destinatari possono utilizzare il documento. È possibile limitare l’accesso a diverse funzioni di Acrobat e Adobe Reader. Queste funzioni includono la possibilità di stampare e copiare il testo, aggiungere firme e aggiungere commenti a un documento.
* Modificate le impostazioni di accesso e protezione in qualsiasi momento, anche dopo la distribuzione del documento protetto tramite criterio.
* Monitorare l’uso del documento dopo averlo distribuito. È possibile vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

### Creazione di un criterio tramite i servizi Web {#creating-a-policy-using-web-services}

Quando create un criterio utilizzando l&#39;API del servizio Web, fate riferimento a un file XML PDF (Portable Document Rights Language) esistente che descrive il criterio. Le autorizzazioni dei criteri e l&#39;entità sono definite nel documento PDRL. Il seguente documento XML è un esempio di documento PDRL.

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
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* namespace.jar (se AEM Forms è distribuito su JBoss)
* jaxb-api.jar (se AEM Forms sono distribuiti su JBoss)
* jaxb-impl.jar (se i AEM Forms sono distribuiti su JBoss)
* jaxb-libs.jar (se AEM Forms è distribuito su JBoss)
* jaxb-xjc.jar (se i AEM Forms sono distribuiti su JBoss)
* relaxngDataType.jar (se i AEM Forms sono distribuiti su JBoss)
* xsdlib.jar (se AEM Forms sono distribuiti su JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilizzate un file JAR diverso se i AEM Forms non sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

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

Quando specificate l’ `NoEncryption` opzione, non potete impostare l’ `PlaintextMetadata` opzione su `false`. Se tentate di farlo, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per informazioni su altri attributi che potete impostare, consultate la descrizione dell&#39; `Policy` interfaccia in Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Creare una voce di criterio**

Una voce di criterio associa entità, che sono gruppi e utenti, e autorizzazioni a un criterio. Un criterio deve avere almeno una voce del criterio. Si supponga, ad esempio, di eseguire le seguenti operazioni:

* Create e registrate una voce del criterio che consente a un gruppo di visualizzare solo un documento mentre è in linea e impedisce ai destinatari di copiarlo.
* Associate l&#39;immissione dei criteri al criterio.
* Proteggere un documento con il criterio utilizzando Acrobat.

Queste azioni consentono ai destinatari di visualizzare il documento solo online e non di copiarlo. Il documento rimane protetto finché non viene rimossa la protezione.

**Registrazione del criterio**

Per poter utilizzare un nuovo criterio, è necessario registrarlo. Dopo aver registrato un criterio, potete utilizzarlo per proteggere i documenti.

### Creazione di un criterio tramite l&#39;API Java {#create-a-policy-using-the-java-api}

Create un criterio utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Impostate gli attributi del criterio.

   * Creare un `Policy` oggetto richiamando il `InfomodelObjectFactory` metodo statico dell&#39;oggetto `createPolicy` . Questo metodo restituisce un `Policy` oggetto.
   * Impostate l&#39;attributo nome del criterio richiamando il metodo dell&#39; `Policy` `setName` oggetto e passando un valore di stringa che specifica il nome del criterio.
   * Impostate la descrizione del criterio richiamando il metodo dell&#39; `Policy` oggetto `setDescription` e passando un valore di stringa che specifica la descrizione del criterio.
   * Impostare il set di criteri a cui appartiene il nuovo criterio richiamando il metodo dell&#39; `Policy` `setPolicySetName` oggetto e passando un valore di stringa che specifica il nome del set di criteri. (È possibile specificare `null` per questo valore di parametro che determina l&#39;aggiunta del criterio al set di criteri *Criteri* personali.)
   * Creare il periodo di validità del criterio richiamando il `InfomodelObjectFactory` metodo statico dell&#39;oggetto `createValidityPeriod` . Questo metodo restituisce un `ValidityPeriod` oggetto.
   * Impostare il numero di giorni per i quali un documento protetto tramite criterio è accessibile richiamando il metodo dell&#39; `ValidityPeriod` `setRelativeExpirationDays` oggetto e passando un valore intero che specifica il numero di giorni.
   * Impostare il periodo di validità del criterio richiamando il metodo dell&#39; `Policy` oggetto `setValidityPeriod` e passando l&#39; `ValidityPeriod` oggetto.

1. Creare una voce del criterio.

   * Creare una voce del criterio richiamando il `InfomodelObjectFactory` metodo statico dell&#39;oggetto `createPolicyEntry` . Questo metodo restituisce un `PolicyEntry` oggetto.
   * Specificate le autorizzazioni del criterio richiamando il `InfomodelObjectFactory` metodo statico dell&#39;oggetto `createPermission` . Passa un membro di dati statici appartenente all&#39; `Permission` interfaccia che rappresenta l&#39;autorizzazione. Questo metodo restituisce un `Permission` oggetto. Ad esempio, per aggiungere l&#39;autorizzazione che consente agli utenti di copiare dati da un documento PDF protetto tramite criterio, passare `Permission.COPY`. Ripetete questo passaggio per ogni autorizzazione da aggiungere.
   * Aggiungete l&#39;autorizzazione alla voce del criterio richiamando il metodo dell&#39; `PolicyEntry` oggetto `addPermission` e passando l&#39; `Permission` oggetto. Ripetete questo passaggio per ogni `Permission` oggetto creato.
   * Creare l&#39;entità del criterio richiamando il `InfomodelObjectFactory` metodo statico dell&#39;oggetto `createSpecialPrincipal` . Passa un membro di dati appartenente all&#39; `InfomodelObjectFactory` oggetto che rappresenta l&#39;entità. Questo metodo restituisce un `Principal` oggetto. Ad esempio, per aggiungere come entità l’editore del documento, passare `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Aggiungete l&#39;entità alla voce del criterio richiamando il `PolicyEntry` metodo dell&#39;oggetto e passando l&#39; `setPrincipal``Principal` oggetto.
   * Aggiungete la voce del criterio al criterio richiamando il metodo dell&#39; `Policy` oggetto `addPolicyEntry` e passando l&#39; `PolicyEntry` oggetto.

1. Registra il criterio.

   * Creare un `PolicyManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getPolicyManager` oggetto.
   * Registrare il criterio richiamando il metodo dell&#39; `PolicyManager` oggetto `registerPolicy` e passando i seguenti valori:

      * L&#39; `Policy` oggetto che rappresenta il criterio da registrare.
   * Una stringa che rappresenta il set di criteri a cui appartiene il criterio.

   Se per creare l&#39; `DocumentSecurityClient` oggetto si utilizza un account amministratore di moduli AEM all&#39;interno delle impostazioni di connessione, è necessario specificare il nome del set di criteri quando si richiama il `registerPolicy` metodo. Se passate un `null` valore per il set di criteri, il criterio viene creato nel set di criteri *Criteri* personali degli amministratori.

   Se utilizzate un utente di Document Security all&#39;interno delle impostazioni di connessione, potete richiamare il `registerPolicy` metodo sovraccarico che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri* personali. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome di set di criteri quando si richiama il `registerPolicy` metodo.

   >[!NOTE]
   >
   >Quando create un criterio, fate riferimento a un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice che utilizzano il servizio Document Security, consultate quanto segue:

* &quot;Avvio rapido (modalità SOAP): Creazione di un criterio tramite l&#39;API Java&quot;

### Creazione di un criterio tramite l&#39;API del servizio Web {#create-a-policy-using-the-web-service-api}

Create un criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `DocumentSecurityServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Impostate gli attributi del criterio.

   * Creare un `PolicySpec` oggetto utilizzando il relativo costruttore.
   * Impostate il nome del criterio assegnando un valore stringa al membro dati dell&#39; `PolicySpec` oggetto `name` .
   * Impostare la descrizione del criterio assegnando un valore stringa al membro dati dell&#39; `PolicySpec` oggetto `description` .
   * Impostare l&#39;insieme di criteri a cui apparterrà il criterio assegnando un valore di stringa al membro `PolicySpec` dati dell&#39; `policySetName` oggetto. È necessario specificare un nome di set di criteri esistente. (È possibile specificare `null` per questo valore di parametro che determina l&#39;aggiunta del criterio ai criteri *personali*.)
   * Impostate il periodo di tempo consentito per il criterio offline assegnando un valore intero al membro `PolicySpec` dati dell&#39; `offlineLeasePeriod` oggetto.
   * Impostare il membro dati dell&#39; `PolicySpec` oggetto `policyXml` con un valore di stringa che rappresenta i dati XML PDRL. Per eseguire questa operazione, creare un oggetto .NET `StreamReader` utilizzando il relativo costruttore. Trasmettere la posizione di un file PDRL XML che rappresenta il criterio al `StreamReader` costruttore. Quindi, richiamare il metodo dell&#39; `StreamReader` oggetto `ReadLine` e assegnare il valore restituito a una variabile di stringa. Eseguire un&#39;iterazione sull&#39; `StreamReader` oggetto finché il `ReadLine` metodo restituisce null. Assegnare la variabile stringa al membro dati dell&#39; `PolicySpec` oggetto `policyXml` .

1. Creare una voce del criterio.

   Non è necessario creare una voce del criterio al momento della creazione di un criterio tramite l&#39;API del servizio Web di Document Security. La voce del criterio è definita nel documento PDF.

1. Registra il criterio.

   Registrare il criterio richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `registerPolicy` e passando i seguenti valori:

   * L&#39; `PolicySpec` oggetto che rappresenta il criterio da registrare.
   * Una stringa che rappresenta il set di criteri a cui appartiene il criterio. È possibile specificare un `null` valore che determina l&#39;aggiunta del criterio al set di criteri *MyPolices* .

   Se per creare l&#39; `DocumentSecurityClient` oggetto si utilizza un account amministratore di moduli AEM all&#39;interno delle impostazioni di connessione, specificare il nome del set di criteri quando si richiama il `registerPolicy` metodo.

   Se utilizzate un utente Document Security all&#39;interno delle impostazioni di connessione, potete richiamare il `registerPolicy` metodo sovraccarico che accetta solo il criterio. In altre parole, non è necessario specificare il nome del set di criteri. Tuttavia, il criterio viene aggiunto al set di criteri denominato *Criteri* personali. Se non si desidera aggiungere il nuovo criterio a questo set di criteri, specificare un nome di set di criteri quando si richiama il `registerPolicy` metodo.

   >[!NOTE]
   >
   >Quando create un criterio e specificate un set di criteri, accertatevi di specificare un set di criteri esistente. Se si specifica un set di criteri che non esiste, viene generata un&#39;eccezione.

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Creazione di un criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Creazione di un criterio tramite l&#39;API del servizio Web&quot;

## Modifica dei criteri {#modifying-policies}

Potete modificare un criterio esistente utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Per apportare modifiche a un criterio esistente, è necessario recuperarlo, modificarlo e quindi aggiornare il criterio sul server. Ad esempio, si supponga di recuperare un criterio esistente e di estenderne il periodo di validità. Prima che la modifica abbia effetto, è necessario aggiornare il criterio.

Potete modificare un criterio quando i requisiti aziendali cambiano e il criterio non riflette più tali requisiti. Invece di creare un nuovo criterio, potete semplicemente aggiornare un criterio esistente.

Per modificare gli attributi del criterio utilizzando un servizio Web (ad esempio, utilizzando classi proxy Java create con JAX-WS), è necessario verificare che il criterio sia registrato con il servizio Document Security. È quindi possibile fare riferimento al criterio esistente utilizzando il `PolicySpec.getPolicyXml` metodo e modificare gli attributi del criterio utilizzando i metodi applicabili. Ad esempio, potete modificare il periodo di tempo consentito per l&#39;utilizzo non in linea richiamando il `PolicySpec.setOfflineLeasePeriod` metodo.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire un&#39;operazione Document Security Service a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un `RightsManagementClient` oggetto. Se utilizzate l&#39;API del servizio Web di Document Security, create un `RightsManagementServiceService` oggetto.

**Recuperare un criterio esistente**

È necessario recuperare un criterio esistente per modificarlo. Per recuperare un criterio, specificate il nome del criterio e il set al quale il criterio appartiene. Se si specifica un `null` valore per il nome del set di criteri, il criterio viene recuperato dal set di criteri *Criteri* personali.

**Impostare gli attributi del criterio**

Per modificare un criterio, modificate il valore degli attributi del criterio. L&#39;unico attributo di criterio che non potete modificare è l&#39;attributo name. Ad esempio, per modificare il periodo di tempo consentito dal criterio per l&#39;utilizzo non in linea, potete modificare il valore dell&#39;attributo del periodo consentito non in linea del criterio.

Quando si modifica il periodo di tempo consentito per un criterio offline utilizzando un servizio Web, il `offlineLeasePeriod` campo nell&#39; `PolicySpec` interfaccia viene ignorato. Per aggiornare il periodo di tempo consentito per l&#39;utilizzo non in linea, modificare l&#39; `OfflineLeasePeriod` elemento nel documento XML PDRL. Quindi, fare riferimento al documento PDF XML aggiornato utilizzando il membro dati dell&#39; `PolicySpec` interfaccia `policyXML` .

>[!NOTE]
>
>Per informazioni su altri attributi che potete impostare, consultate la descrizione dell&#39; `Policy` interfaccia in Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Aggiornare il criterio**

Prima che le modifiche apportate a un criterio vengano applicate, è necessario aggiornare il criterio con il servizio Document Security. Le modifiche ai criteri di protezione dei documenti vengono aggiornate al successivo aggiornamento della sincronizzazione del documento protetto tramite criterio con il servizio Document Security.

### Modificare i criteri esistenti utilizzando l&#39;API Java {#modify-existing-policies-using-the-java-api}

Modificate un criterio esistente utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `RightsManagementClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un criterio esistente.

   * Creare un `PolicyManager` oggetto richiamando il `RightsManagementClient` metodo dell&#39; `getPolicyManager` oggetto.
   * Creare un oggetto `Policy` che rappresenti il criterio da aggiornare richiamando il metodo dell&#39; `PolicyManager` oggetto `getPolicy` e passando i seguenti valori&quot;

      * Una stringa che rappresenta il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che il set di criteri venga utilizzato `MyPolicies` .
      * Una stringa che rappresenta il nome del criterio.

1. Impostate gli attributi del criterio.

   Modificate gli attributi del criterio per soddisfare i requisiti aziendali. Ad esempio, per modificare il periodo di tempo consentito dal criterio offline, richiamare il `Policy` metodo dell&#39;oggetto `setOfflineLeasePeriod` .

1. Aggiornare il criterio.

   Aggiornare il criterio richiamando il metodo dell&#39; `PolicyManager` oggetto `updatePolicy` . Passa l&#39; `Policy` oggetto che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate Avvio rapido (modalità SOAP): Modifica di un criterio tramite la sezione Java API.

### Modifica dei criteri esistenti tramite l&#39;API del servizio Web {#modify-existing-policies-using-the-web-service-api}

Modificate un criterio esistente utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `RightsManagementServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un criterio esistente.

   Creare un `PolicySpec` oggetto che rappresenti il criterio da modificare richiamando il metodo dell&#39; `RightsManagementServiceClient` oggetto `getPolicy` e passando i seguenti valori:

   * Una stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che il set di criteri venga utilizzato `MyPolicies` .
   * Un valore di stringa che specifica il nome del criterio.

1. Impostate gli attributi del criterio.

   Modificate gli attributi del criterio per soddisfare i requisiti aziendali.

1. Aggiornare il criterio.

   Aggiornare il criterio richiamando il metodo dell&#39; `RightsManagementServiceClient` oggetto `updatePolicyFromSDK` e passando l&#39; `PolicySpec` oggetto che rappresenta il criterio da aggiornare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Modifica di un criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Modifica di un criterio tramite l&#39;API del servizio Web&quot;

## Eliminazione dei criteri {#deleting-policies}

Potete eliminare un criterio esistente utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Una volta eliminato, un criterio non può più essere utilizzato per proteggere i documenti. Tuttavia, i documenti protetti tramite criterio esistenti che utilizzano il criterio sono ancora protetti. Potete eliminare un criterio quando diventa disponibile un criterio più recente.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per eliminare un criterio esistente, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Creare un oggetto Document Security Client API.
1. Eliminate il criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un `RightsManagementClient` oggetto. Se utilizzate l&#39;API del servizio Web di Document Security, create un `RightsManagementServiceService` oggetto.

**Eliminare il criterio**

Per eliminare un criterio, è necessario specificare il criterio da eliminare e il set al quale il criterio appartiene. L&#39;utente le cui impostazioni sono utilizzate per richiamare AEM Forms deve disporre dell&#39;autorizzazione per eliminare il criterio; in caso contrario si verifica un&#39;eccezione. Analogamente, se si tenta di eliminare un criterio che non esiste, si verifica un&#39;eccezione.

### Eliminare i criteri tramite l&#39;API Java {#delete-policies-using-the-java-api}

Eliminate un criterio utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `RightsManagementClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Eliminate il criterio.

   * Creare un `PolicyManager` oggetto richiamando il `RightsManagementClient` metodo dell&#39; `getPolicyManager` oggetto.
   * Eliminare il criterio richiamando il metodo dell&#39; `PolicyManager` oggetto `deletePolicy` e passando i seguenti valori:

      * Una stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che il set di criteri venga utilizzato `MyPolicies` .
      * Un valore di stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Eliminazione di un criterio tramite l&#39;API Java&quot;

### Eliminare i criteri tramite l&#39;API del servizio Web {#delete-policies-using-the-web-service-api}

Eliminate un criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `RightsManagementServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Eliminate il criterio.

   Per eliminare un criterio, richiamate il metodo dell&#39; `RightsManagementServiceClient` oggetto `deletePolicy` e passate i seguenti valori:

   * Una stringa che specifica il nome del set di criteri a cui appartiene il criterio. È possibile specificare `null` che il set di criteri venga utilizzato `MyPolicies` .
   * Un valore di stringa che specifica il nome del criterio da eliminare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Eliminazione di un criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Eliminazione di un criterio tramite l&#39;API del servizio Web&quot;

## Applicazione dei criteri ai documenti PDF {#applying-policies-to-pdf-documents}

È possibile applicare un criterio a un documento PDF per proteggere il documento. Applicando un criterio a un documento PDF, è possibile limitare l&#39;accesso al documento. Non è possibile applicare un criterio a un documento se il documento è già protetto con un criterio.

Mentre il documento è aperto, è inoltre possibile limitare l&#39;accesso alle funzioni di Acrobat e Adobe Reader, compresa la possibilità di stampare e copiare il testo, apportare modifiche e aggiungere firme e commenti a un documento. Inoltre, è possibile revocare un documento PDF protetto tramite criterio quando non si desidera più che gli utenti accedano al documento.

È possibile monitorare l&#39;utilizzo di un documento protetto tramite criterio dopo averlo distribuito. In altre parole, potete vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di eseguire un&#39;operazione del servizio Document Security a livello di programmazione, create un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un `DocumentSecurityClient` oggetto. Se utilizzate l&#39;API del servizio Web di Document Security, create un `DocumentSecurityServiceService` oggetto.

**Recupero di un documento PDF**

È possibile recuperare un documento PDF per applicare un criterio. Dopo aver applicato un criterio al documento PDF, gli utenti possono utilizzare il documento con restrizioni. Ad esempio, se il criterio non consente l&#39;apertura del documento offline, gli utenti devono essere online per aprire il documento.

**Applicare un criterio esistente al documento PDF**

Per applicare un criterio a un documento PDF, fare riferimento a un criterio esistente e specificare a quale set di criteri appartiene il criterio. L&#39;utente che sta impostando le proprietà di connessione deve avere accesso al criterio specificato. In caso contrario, si verifica un&#39;eccezione.

**Salvare il documento PDF**

Dopo che il servizio Document Security ha applicato un criterio a un documento PDF, potete salvare il documento PDF protetto tramite criterio come file PDF.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicazione di un criterio a un documento PDF tramite l&#39;API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Applicare un criterio a un documento PDF utilizzando l&#39;API Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `RightsManagementClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Applicare un criterio esistente al documento PDF.

   * Creare un `DocumentManager` oggetto richiamando il `RightsManagementClient` metodo dell&#39; `getDocumentManager` oggetto.
   * Applicare un criterio al documento PDF richiamando il metodo dell&#39; `DocumentManager` oggetto `protectDocument` e passando i seguenti valori:

      * L&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF a cui viene applicato il criterio.
      * Una stringa che specifica il nome del documento.
      * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. Potete specificare un `null` valore che determina l&#39;utilizzo del set di `MyPolicies` criteri.
      * Una stringa che specifica il nome del criterio.
      * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore successivo del parametro deve essere null).
      * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere `null` (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
      * Un `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni internazionali utilizzate per selezionare il modello di MS Office. Questo valore del parametro è facoltativo e non viene utilizzato per i documenti PDF. Per proteggere un documento PDF, specificare `null`.

      Il `protectDocument` metodo restituisce un `RMSecureDocumentResult` oggetto che contiene il documento PDF protetto tramite criterio.


1. Salvare il documento PDF.

   * Richiamare il metodo dell&#39; `RMSecureDocumentResult` oggetto `getProtectedDoc` per ottenere il documento PDF protetto tramite criterio. Questo metodo restituisce un `com.adobe.idp.Document` oggetto.
   * Creare un `java.io.File` oggetto e assicurarsi che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `getProtectedDoc` metodo).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità EJB): Applicazione di un criterio a un documento PDF tramite l&#39;API Java&quot;
* &quot;Avvio rapido (modalità SOAP): Applicazione di un criterio a un documento PDF tramite l&#39;API Java&quot;

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applicazione di un criterio a un documento PDF tramite l&#39;API del servizio Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Applicare un criterio a un documento PDF utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `RightsManagementServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Trasmettere un valore di stringa che specifica il WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF a cui è applicato un criterio.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. Determinare la dimensione dell&#39;array di byte ottenendo la `System.IO.FileStream` proprietà dell&#39; `Length` oggetto.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Applicare un criterio esistente al documento PDF.

   Applicare un criterio al documento PDF richiamando il metodo dell&#39; `RightsManagementServiceClient` oggetto `protectDocument` e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene il documento PDF a cui viene applicato il criterio.
   * Una stringa che specifica il nome del documento.
   * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. Potete specificare un `null` valore che determina l&#39;utilizzo del set di `MyPolicies` criteri.
   * Una stringa che specifica il nome del criterio.
   * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro successivo deve essere `null`).
   * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
   * Un `RMLocale` valore che specifica il valore delle impostazioni internazionali (ad esempio, `RMLocale.en`).
   * Un parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore del criterio.
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite criterio.
   * Un parametro di output della stringa utilizzato per memorizzare il tipo mime (ad esempio, `application/pdf`).

   Il `protectDocument` metodo restituisce un `BLOB` oggetto che contiene il documento PDF protetto tramite criterio.

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto tramite criterio.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `protectDocument` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Applicazione di un criterio a un documento PDF tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Applicazione di un criterio a un documento PDF tramite l&#39;API del servizio Web&quot;

## Rimozione di criteri dai documenti PDF {#removing-policies-from-pdf-documents}

È possibile rimuovere un criterio da un documento protetto tramite criterio per rimuovere la protezione dal documento. Se non si desidera più che il documento sia protetto tramite un criterio. Se desiderate aggiornare un documento protetto tramite criterio con un criterio più recente, invece di rimuovere il criterio e aggiungere il criterio aggiornato, è più efficiente cambiare il criterio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

È possibile rimuovere un criterio da un documento PDF protetto tramite criterio a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39; `SWITCH_POLICY` autorizzazione per rimuovere un criterio da un documento PDF. Inoltre, anche l&#39;utente specificato nelle impostazioni di connessione AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento PDF non protetto**

Dopo che il servizio Document Security ha rimosso un criterio da un documento PDF, potete salvare il documento PDF non protetto come file PDF.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Rimozione di un criterio da un documento PDF tramite l&#39;API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Rimuovere un criterio da un documento PDF protetto tramite criterio utilizzando l&#39;API Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF protetto tramite criterio.

   * Creare un `java.io.FileInputStream` oggetto che rappresenti il documento PDF protetto tramite criterio utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Rimuovere il criterio dal documento PDF.

   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getDocumentManager` oggetto.
   * Rimuovere un criterio dal documento PDF richiamando il `DocumentManager` metodo dell&#39; `removeSecurity` oggetto e passando l&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che contiene un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un `java.io.File` oggetto e assicurarsi che l&#39;estensione del file sia PDF.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `removeSecurity` metodo).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Rimozione di un criterio da un documento PDF tramite l&#39;API Java&quot;

### Rimozione di un criterio tramite l&#39;API del servizio Web {#remove-a-policy-using-the-web-service-api}

Rimuovere un criterio da un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `DocumentSecurityServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF protetto tramite criterio.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF protetto tramite criterio da cui viene rimosso il criterio.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Rimuovere il criterio dal documento PDF.

   Rimuovere il criterio dal documento PDF richiamando il `DocumentSecurityServiceClient` metodo dell&#39; `removePolicySecurity` oggetto e passando l&#39; `BLOB` oggetto che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un `BLOB` oggetto che contiene un documento PDF non protetto.

1. Salvare il documento PDF non protetto.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `removePolicySecurity` metodo. Compilare l&#39;array di byte ottenendo il valore del campo dell&#39; `BLOB` oggetto `MTOM` .
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Rimozione di un criterio da un documento PDF tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Rimozione di un criterio da un documento PDF tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revoca dell&#39;accesso ai documenti {#revoking-access-to-documents}

È possibile revocare l&#39;accesso a un documento PDF protetto tramite criterio in modo che tutte le copie del documento non siano accessibili agli utenti. Quando un utente tenta di aprire un documento PDF revocato, viene reindirizzato a un URL specificato in cui è possibile visualizzare un documento modificato. È necessario specificare a livello di programmazione l&#39;URL al quale l&#39;utente viene reindirizzato. Quando revocate l&#39;accesso a un documento, la modifica ha effetto alla successiva sincronizzazione dell&#39;utente con il servizio Document Security aprendo il documento protetto tramite criterio online.

La capacità di revocare l&#39;accesso a un documento offre ulteriore protezione. Ad esempio, si supponga che sia disponibile una versione più recente di un documento e che non si desideri più che qualcuno visualizzi la versione obsoleta. In questa situazione, l&#39;accesso al documento precedente può essere revocato e nessuno può visualizzare il documento a meno che l&#39;accesso non venga ripristinato.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Ripristino dell&#39;accesso ai documenti revocati](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revoca l&#39;accesso ai documenti tramite l&#39;API Java {#revoke-access-to-documents-using-the-java-api}

Revocare l&#39;accesso a un documento PDF protetto tramite criterio utilizzando l&#39;API Document Security (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF protetto tramite criterio

   * Creare un `java.io.FileInputStream` oggetto che rappresenti il documento PDF protetto tramite criterio utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Revoca del documento protetto tramite criterio

   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getDocumentManager` oggetto.
   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite criterio richiamando il `DocumentManager` metodo dell&#39; `getLicenseId` oggetto. Passa l&#39; `com.adobe.idp.Document` oggetto che rappresenta il documento protetto tramite criterio. Questo metodo restituisce un valore di stringa che rappresenta il valore dell’identificatore di licenza.
   * Creare un `LicenseManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getLicenseManager` oggetto.
   * Revocare il documento protetto tramite criterio richiamando il metodo dell&#39; `LicenseManager` oggetto `revokeLicense` e passando i seguenti valori:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite criterio (specificare il valore restituito dal `DocumentManager` metodo dell&#39; `getLicenseId` oggetto).
      * Un membro di dati statici dell&#39; `License` interfaccia che specifica il motivo della revoca del documento. For example, you can specify `License.DOCUMENT_REVISED`.
      * Un `java.net.URL` valore che specifica la posizione in cui si trova il documento rivisto. Se non desiderate reindirizzare un utente a un altro URL, potete passare `null`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Revoca di un documento tramite l&#39;API Java&quot;

### Revoca dell&#39;accesso ai documenti tramite l&#39;API del servizio Web {#revoke-access-to-documents-using-the-web-service-api}

Revocare l&#39;accesso a un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto API client Document Security

   * Creare un `DocumentSecurityServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento PDF protetto tramite criterio

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF protetto tramite criterio revocato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto tramite criterio da revocare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Revoca del documento protetto tramite criterio

   * Recuperare il valore dell&#39;identificatore di licenza del documento protetto tramite criterio richiamando il `DocumentSecurityServiceClient` metodo dell&#39; `getLicenseID` oggetto e passando l&#39; `BLOB` oggetto che rappresenta il documento protetto tramite criterio. Questo metodo restituisce un valore di stringa che rappresenta l’identificatore della licenza.
   * Revocare il documento protetto tramite criterio richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `revokeLicense` e passando i seguenti valori:

      * Valore stringa che specifica il valore dell&#39;identificatore di licenza del documento protetto tramite criterio (specificare il valore restituito dal `DocumentSecurityServiceService` metodo dell&#39; `getLicenseId` oggetto).
      * Un membro di dati statici dell&#39; `Reason` enum che specifica il motivo della revoca del documento. For example, you can specify `Reason.DOCUMENT_REVISED`.
      * Un `string` valore che specifica la posizione dell&#39;URL in cui si trova il documento rivisto. Se non desiderate reindirizzare un utente a un altro URL, potete passare `null`.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Revoca di un documento tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Revoca di un documento tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Rimozione di criteri dai documenti di Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ripristino dell&#39;accesso ai documenti revocati {#reinstating-access-to-revoked-documents}

È possibile ripristinare l&#39;accesso a un documento PDF revocato, in modo che tutte le copie del documento revocato siano accessibili agli utenti. Quando un utente apre un documento ripristinato revocato, può visualizzare il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per ripristinare l&#39;accesso a un documento PDF revocato, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.
1. Ripristinare l&#39;accesso al documento PDF revocato.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un `DocumentSecurityClient` oggetto. Se utilizzate l&#39;API del servizio Web di Document Security, create un `DocumentSecurityServiceService` oggetto.

**Recuperare l&#39;identificatore di licenza del documento PDF revocato**

Per ripristinare un documento PDF revocato, è necessario recuperare l’identificatore di licenza del documento PDF revocato. Dopo aver ottenuto il valore dell&#39;identificatore di licenza, potete ripristinare un documento revocato. Se si tenta di ripristinare un documento che non viene revocato, verrà generata un&#39;eccezione.

**Ripristino dell&#39;accesso al documento PDF revocato**

Per ripristinare l&#39;accesso a un documento PDF revocato, è necessario specificare l&#39;identificatore di licenza del documento revocato. Se si tenta di ripristinare l&#39;accesso a un documento PDF non revocato, si verificherà un&#39;eccezione.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Ripristino dell&#39;accesso ai documenti revocati tramite l&#39;API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Ripristinate l&#39;accesso a un documento revocato utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF revocato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.
   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getDocumentManager` oggetto.
   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo dell&#39; `DocumentManager` oggetto `getLicenseId` e passando l&#39; `com.adobe.idp.Document` oggetto che rappresenta il documento revocato. Questo metodo restituisce un valore di stringa che rappresenta l’identificatore della licenza.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Creare un `LicenseManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getLicenseManager` oggetto.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo dell&#39; `LicenseManager` oggetto `unrevokeLicense` e passando il valore dell&#39;identificatore di licenza del documento revocato.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Ripristino dell&#39;accesso a un documento revocato tramite l&#39;API del servizio Web&quot;

### Ripristino dell&#39;accesso ai documenti revocati tramite l&#39;API del servizio Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Ripristinate l&#39;accesso a un documento revocato utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `DocumentSecurityServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare l&#39;identificatore di licenza del documento PDF revocato.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF revocato al quale viene ripristinato l&#39;accesso.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta il percorso del file del documento PDF revocato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Ripristinare l&#39;accesso al documento PDF revocato.

   * Recuperare il valore dell&#39;identificatore di licenza del documento revocato richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `getLicenseID` e passando l&#39; `BLOB` oggetto che rappresenta il documento revocato. Questo metodo restituisce un valore di stringa che rappresenta l’identificatore della licenza.
   * Ripristinare l&#39;accesso al documento PDF revocato richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `unrevokeLicense` e passando un valore stringa che specifica il valore dell&#39;identificatore di licenza del documento PDF revocato (passare il valore restituito dal metodo dell&#39; `DocumentSecurityServiceClient` oggetto `getLicenseId` ).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Ripristino dell&#39;accesso a un documento revocato tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ripristino dell&#39;accesso a un documento revocato tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica dei documenti PDF protetti tramite criterio {#inspecting-policy-protected-pdf-documents}

Potete utilizzare l&#39;API di Document Security Service (Java e il servizio Web) per ispezionare i documenti PDF protetti tramite criterio. L&#39;ispezione dei documenti PDF protetti tramite criterio restituisce informazioni sul documento PDF protetto tramite criterio. È possibile, ad esempio, determinare il criterio utilizzato per proteggere il documento e la data in cui il documento è stato protetto.

Non è possibile eseguire questa operazione se la versione di LiveCycle in uso è 8.x o precedente. Il supporto per l&#39;ispezione di documenti protetti tramite criterio è aggiunto nei AEM Forms. Se si tenta di esaminare un documento protetto tramite criterio utilizzando LiveCycle 8.x (o versioni precedenti), viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per esaminare un documento PDF protetto tramite criterio, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Recuperare un documento protetto tramite criterio da esaminare.
1. Ottenete informazioni sul documento protetto tramite criterio.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di eseguire un&#39;operazione del servizio Document Security a livello di programmazione, create un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un `RightsManagementClient` oggetto. Se utilizzate l&#39;API del servizio Web di Document Security, create un `RightsManagementServiceService` oggetto.

**Recuperare un documento protetto tramite criterio da esaminare**

Per esaminare un documento protetto tramite criterio, recuperatelo. Se tentate di ispezionare un documento non protetto con un criterio o revocato, viene generata un&#39;eccezione.

**Ispezionare il documento**

Dopo aver recuperato un documento protetto tramite criterio, potete controllarlo.

**Ottenere informazioni sul documento protetto tramite criterio**

Dopo aver esaminato un documento PDF protetto tramite criterio, potete ottenere informazioni su di esso. Ad esempio, è possibile determinare il criterio utilizzato per proteggere il documento.

Se si protegge un documento con un criterio che appartiene a Criteri personali e quindi si chiama `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, viene restituito null.

Se il documento è protetto tramite un criterio contenuto in un set di criteri (diverso da Criteri personali), `RMInspectResult.getPolicysetName` e `RMInspectResult.getPolicysetId` restituiscono stringhe valide.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspect Policy Protected PDF Documents using Java API {#inspect-policy-protected-pdf-documents-using-the-java-api}

Esaminate un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
   * Creare un `RightsManagementClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un documento protetto tramite criterio da esaminare.

   * Creare un `java.io.FileInputStream` oggetto che rappresenti il documento PDF protetto tramite criterio utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Esaminare il documento.

   * Creare un `DocumentManager` oggetto richiamando il `RightsManagementClient` metodo dell&#39; `getDocumentManager` oggetto.
   * Esaminare il documento protetto tramite criterio richiamando il `LicenseManager` metodo dell&#39; `inspectDocument` . Passa l&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un `RMInspectResult` oggetto che contiene informazioni sul documento protetto tramite criterio.

1. Ottenete informazioni sul documento protetto tramite criterio.

   Per ottenere informazioni sul documento protetto tramite criterio, richiamare il metodo appropriato che appartiene all&#39; `RMInspectResult` oggetto. Ad esempio, per recuperare il nome del criterio, richiamare il `RMInspectResult` metodo dell&#39; `getPolicyName` oggetto.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Ispezione dei documenti PDF protetti tramite criterio tramite l&#39;API Java&quot;

### Inspect Policy Protected PDF Documents using the web service API {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Esaminate un documento PDF protetto tramite criterio utilizzando l&#39;API di Document Security Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `RightsManagementServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento protetto tramite criterio da esaminare.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF da esaminare.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Trasmettere l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Esaminare il documento.

   Esaminare il documento protetto tramite criterio richiamando il `RightsManagementServiceClient` metodo dell&#39; `inspectDocument` . Passa l&#39; `BLOB` oggetto che contiene il documento PDF protetto tramite criterio. Questo metodo restituisce un `RMInspectResult` oggetto che contiene informazioni sul documento protetto tramite criterio.

1. Ottenete informazioni sul documento protetto tramite criterio.

   Per ottenere informazioni sul documento protetto tramite criterio, ottenere il valore del campo appropriato che appartiene all&#39; `RMInspectResult` oggetto. Ad esempio, per recuperare il nome del criterio, ottenere il valore del campo dell&#39; `RMInspectResult` oggetto `policyName` .

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Ispezione dei documenti PDF protetti tramite criterio tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ispezione dei documenti PDF protetti tramite criterio tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di filigrane {#creating-watermarks}

Le filigrane garantiscono la sicurezza di un documento identificando in modo univoco il documento e controllando la violazione del copyright. Ad esempio, è possibile creare e inserire una filigrana con l&#39;indicazione Riservato su tutte le pagine di un documento. Dopo la creazione di una filigrana, potete includerla come parte di un criterio. In altre parole, potete impostare l&#39;attributo della filigrana del criterio con la filigrana appena creata. Dopo che un criterio contenente una filigrana è stato applicato a un documento, la filigrana viene visualizzata nel documento protetto tramite criterio.

>[!NOTE]
>
>Le filigrane possono essere create solo dagli utenti con privilegi di amministratore Document Security. In altre parole, è necessario specificare tale utente quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per creare una filigrana, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Document Security Client API.
1. Impostare gli attributi delle filigrane.
1. Registra la filigrana con il servizio Document Security.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Document Security**

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un `RightsManagementClient` oggetto. Se utilizzate l&#39;API del servizio Web di Document Security, create un `RightsManagementServiceService` oggetto.

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
   <td><p>Se questo valore è specificato, <code>WaterBackCmd:IS_SIZE_ENABLED</code> deve essere presente e il valore deve essere true. Se questo attributo non è specificato, il comportamento predefinito è adatto alla pagina.</p></td>
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
   <td><p>Specifica il testo personalizzato per una filigrana. Se questo valore è presente, <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> deve essere presente e impostato su true.</p></td>
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

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creare filigrane tramite l&#39;API Java {#create-watermarks-using-the-java-api}

Create una filigrana utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio `adobe-rightsmanagement-client.jar`, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `RightsManagementClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Impostare gli attributi della filigrana

   * Creare un `Watermark` oggetto richiamando il `InfomodelObjectFactory` metodo statico dell&#39;oggetto `createWatermark` . Questo metodo restituisce un `Watermark` oggetto.
   * Impostate l&#39;attributo nome della filigrana richiamando il metodo dell&#39; `Watermark` `setName` oggetto e passando un valore di stringa che specifica il nome del criterio.
   * Impostare l&#39;attributo di sfondo della filigrana richiamando il metodo dell&#39; `Watermark` oggetto `setBackground` e passando `true`. Impostando questo attributo, la filigrana viene visualizzata sullo sfondo del documento.
   * Impostare l&#39;attributo di testo personalizzato della filigrana richiamando il metodo dell&#39; `Watermark` oggetto `setCustomText` e passando un valore di stringa che rappresenta il testo della filigrana.
   * Impostare l&#39;attributo di opacità della filigrana richiamando il metodo dell&#39; `Watermark` `setOpacity` oggetto e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che la filigrana è completamente trasparente.

1. Registra la filigrana.

   * Creare un `WatermarkManager` oggetto richiamando il `RightsManagementClient` metodo dell&#39; `getWatermarkManager` oggetto. Questo metodo restituisce un `WatermarkManager` oggetto.
   * Registrare la filigrana richiamando il metodo dell&#39; `WatermarkManager` oggetto `registerWatermark` e passando l&#39;oggetto `Watermark` che rappresenta la filigrana da registrare. Questo metodo restituisce un valore di stringa che rappresenta il valore di identificazione della filigrana.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Creazione di una filigrana mediante l&#39;API Java&quot;

### Creare filigrane mediante l&#39;API del servizio Web {#create-watermarks-using-the-web-service-api}

Create una filigrana utilizzando l&#39;API di Document Security (servizio Web):

1. Creare un oggetto Document Security Client API.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `RightsManagementServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Impostate gli attributi della filigrana.

   * Creare un `WatermarkSpec` oggetto richiamando il `WatermarkSpec` costruttore.
   * Impostare il nome della filigrana assegnando un valore di stringa al membro dati dell&#39; `WatermarkSpec` oggetto `name` .
   * Impostare l&#39;attributo della `id` filigrana assegnando un valore di stringa al membro di dati dell&#39; `WatermarkSpec` oggetto `id` .
   * Per ogni proprietà della filigrana da impostare, creare un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto separato.
   * Impostare il valore chiave assegnando un valore al membro `MyMapOf_xsd_string_To_xsd_anyType_Item` dati dell&#39; `key` oggetto (ad esempio, `WaterBackCmd:OPACITY)`).
   * Impostare il valore assegnando un valore al membro `MyMapOf_xsd_string_To_xsd_anyType_Item` dati dell&#39;oggetto (ad esempio, `value` `.25`).
   * Create a `MyArrayOf_xsd_anyType` object. Per ciascun `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto, richiamare il `MyArrayOf_xsd_anyType` metodo dell&#39; `Add` . Passate l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegnare l&#39; `MyArrayOf_xsd_anyType` oggetto al membro dati dell&#39; `WatermarkSpec` oggetto `values` .

1. Registra la filigrana.

   Registrare la filigrana richiamando il metodo dell&#39; `RightsManagementServiceClient` oggetto `registerWatermark` e passando l&#39;oggetto `WatermarkSpec` che rappresenta la filigrana da registrare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate i seguenti esempi di avvio rapido:

* &quot;Avvio rapido (MTOM): Creazione di una filigrana mediante l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Creazione di una filigrana mediante l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica delle filigrane {#modifying-watermarks}

Potete modificare una filigrana esistente utilizzando l&#39;API Java di Document Security o l&#39;API del servizio Web. Per apportare modifiche a una filigrana esistente, recuperarla, modificarne gli attributi e quindi aggiornarla sul server. Ad esempio, supponete di recuperare una filigrana e modificarne l’attributo di opacità. Prima che la modifica abbia effetto, è necessario aggiornare la filigrana.

Quando modificate una filigrana, la modifica ha effetto sui documenti futuri a cui è stata applicata la filigrana. In altre parole, i documenti PDF esistenti contenenti la filigrana non vengono modificati.

>[!NOTE]
>
>Le filigrane possono essere modificate solo dagli utenti con diritti di amministratore di Document Security. In altre parole, è necessario specificare tale utente quando si definiscono le impostazioni di connessione necessarie per creare un oggetto client del servizio Document Security.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire un&#39;operazione del servizio Document Security a livello di programmazione, è necessario creare un oggetto client del servizio Document Security. Se utilizzate l&#39;API Java, create un `DocumentSecurityClient` oggetto. Se utilizzate l&#39;API del servizio Web di Document Security, create un `DocumentSecurityServiceService` oggetto.

**Recuperare la filigrana da modificare**

Per modificare una filigrana, è necessario recuperare una filigrana esistente. È possibile recuperare una filigrana specificandone il nome o il valore identificativo.

**Impostare gli attributi delle filigrane**

Per modificare una filigrana esistente, modificate il valore di uno o più attributi della filigrana. Quando si aggiorna una filigrana a livello di programmazione utilizzando un servizio Web, è necessario impostare tutti gli attributi impostati originariamente, anche se il valore non cambia. Ad esempio, si supponga che siano impostati i seguenti attributi di filigrana: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`, e `WaterBackCmd:SRCTEXT`. Anche se l&#39;unico attributo che si desidera modificare è `WaterBackCmd:OPACITY`, è necessario impostare gli altri valori.

>[!NOTE]
>
>Quando utilizzate l&#39;API Java per modificare una filigrana, non è necessario specificare tutti gli attributi. Impostate l’attributo della filigrana da modificare.

>[!NOTE]
>
>Per informazioni sui nomi degli attributi delle filigrane, consultate [Creazione di filigrane](protecting-documents-policies.md#creating-watermarks).

**Aggiornare la filigrana**

Dopo aver modificato gli attributi di una filigrana, è necessario aggiornare la filigrana.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Creazione di filigrane](protecting-documents-policies.md#creating-watermarks)

### Modificare le filigrane mediante l&#39;API Java {#modify-watermarks-using-the-java-api}

Modificare una filigrana utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperate la filigrana da modificare.

   Creare un `WatermarkManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getWatermarkManager` oggetto e passando un valore di stringa che specifica il nome della filigrana. Questo metodo restituisce un `Watermark` oggetto che rappresenta la filigrana da modificare.

1. Impostate gli attributi della filigrana.

   Impostare l&#39;attributo di opacità della filigrana richiamando il metodo dell&#39; `Watermark` `setOpacity` oggetto e passando un valore intero che specifica il livello di opacità. Il valore 100 indica che la filigrana è completamente opaca e il valore 0 indica che la filigrana è completamente trasparente.

   >[!NOTE]
   >
   >In questo esempio viene modificato solo l’attributo opacità.

1. Aggiorna la filigrana.

   * Aggiornare la filigrana richiamando il metodo dell&#39; `WatermarkManager` oggetto `updateWatermark` `Watermark` e passando l&#39;oggetto il cui attributo è stato modificato.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate Avvio rapido (modalità SOAP): Modifica di una filigrana tramite la sezione Java API.

### Modificare le filigrane mediante l&#39;API del servizio Web {#modify-watermarks-using-the-web-service-api}

Modificare una filigrana utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `DocumentSecurityServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperate la filigrana da modificare.

   Recuperare la filigrana da modificare richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `getWatermarkByName` . Passa un valore di stringa che specifica il nome della filigrana. Questo metodo restituisce un `WatermarkSpec` oggetto che rappresenta la filigrana da modificare.

1. Impostate gli attributi della filigrana.

   * Per ogni proprietà della filigrana da aggiornare, creare un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto separato.
   * Impostare il valore chiave assegnando un valore al membro `MyMapOf_xsd_string_To_xsd_anyType_Item` dati dell&#39; `key` oggetto (ad esempio, `WaterBackCmd:OPACITY)`).
   * Impostare il valore assegnando un valore al membro `MyMapOf_xsd_string_To_xsd_anyType_Item` dati dell&#39;oggetto (ad esempio, `value` `.50`).
   * Create a `MyArrayOf_xsd_anyType` object. Per ciascun `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto, richiamare il `MyArrayOf_xsd_anyType` metodo dell&#39; `Add` . Passate l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegnare l&#39; `MyArrayOf_xsd_anyType` oggetto al membro dati dell&#39; `WatermarkSpec` oggetto `values` .

1. Aggiorna la filigrana.

   Aggiornare la filigrana richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `updateWatermark` e passando l&#39; `WatermarkSpec` oggetto che rappresenta la filigrana da modificare.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (MTOM): Modifica di una filigrana mediante l&#39;API del servizio Web&quot;

## Ricerca di eventi {#searching-for-events}

Il servizio Rights Management tiene traccia delle azioni specifiche eseguite, ad esempio l&#39;applicazione di un criterio a un documento, l&#39;apertura di un documento protetto tramite criterio e la revoca dell&#39;accesso ai documenti. Il controllo degli eventi deve essere abilitato per il servizio Rights Management, altrimenti gli eventi non vengono tracciati.

Gli eventi rientrano in una delle seguenti categorie:

* Gli eventi di amministratore sono azioni correlate a un amministratore, ad esempio la creazione di un nuovo account di amministratore.
* Gli eventi del documento sono azioni correlate a un documento, ad esempio la chiusura di un documento protetto tramite criterio.
* Gli eventi dei criteri sono azioni correlate a un criterio, ad esempio la creazione di un nuovo criterio.
* Gli eventi di servizio sono azioni relative al servizio Rights Management, ad esempio la sincronizzazione con la directory dell&#39;utente.

Potete cercare eventi specifici utilizzando l&#39;API Java di Rights Management o l&#39;API del servizio Web. Cercando gli eventi, è possibile eseguire attività quali la creazione di un file di registro di determinati eventi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Rights Management, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-10}

Per cercare un evento Rights Management, effettuate le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Rights Management Client API.
1. Specificate l&#39;evento per il quale eseguire la ricerca.
1. Cercate l’evento.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Rights Management Client API**

Prima di poter eseguire un&#39;operazione del servizio Rights Management in modo programmatico, dovete creare un oggetto client del servizio Rights Management. Se utilizzate l&#39;API Java, create un `DocumentSecurityClient` oggetto. Se utilizzate l&#39;API del servizio Web Rights Management, create un `DocumentSecurityServiceService` oggetto.

**Specificare gli eventi da cercare**

È necessario specificare l&#39;evento da cercare. Ad esempio, è possibile cercare l&#39;evento policy create, che si verifica quando viene creato un nuovo criterio.

**Ricerca dell’evento**

Dopo aver specificato l&#39;evento da cercare, potete utilizzare l&#39;API Java di Rights Management o l&#39;API del servizio Web di Rights Management per cercare l&#39;evento.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cercare eventi utilizzando l&#39;API Java {#search-for-events-using-the-java-api}

Cercate gli eventi utilizzando l&#39;API Rights Management (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Rights Management Client API

   Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Specificare gli eventi da cercare

   * Creare un `EventManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getEventManager` oggetto. Questo metodo restituisce un `EventManager` oggetto.
   * Creare un `EventSearchFilter` oggetto richiamandone il costruttore.
   * Specificare l&#39;evento per il quale eseguire la ricerca richiamando il metodo dell&#39; `EventSearchFilter` oggetto `setEventCode` e passando un membro di dati statici appartenente alla `EventManager` classe che rappresenta l&#39;evento per il quale eseguire la ricerca. Ad esempio, per cercare l&#39;evento di creazione del criterio, passare `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >È possibile definire criteri di ricerca aggiuntivi richiamando metodi `EventSearchFilter` oggetto. Ad esempio, richiamare il `setUserName` metodo per specificare un utente associato all&#39;evento.

1. Ricerca dell’evento

   Cercare l&#39;evento richiamando il metodo dell&#39; `EventManager` oggetto `searchForEvents` e passando l&#39;oggetto `EventSearchFilter` che definisce i criteri di ricerca dell&#39;evento. Questo metodo restituisce un array di `Event` oggetti.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Rights Management, consultate le seguenti Guide rapide:

* &quot;Avvio rapido (SOAP): Ricerca di eventi tramite l&#39;API Java&quot;

### Cercare eventi utilizzando l&#39;API del servizio Web {#search-for-events-using-the-web-service-api}

Cercare gli eventi utilizzando l&#39;API Rights Management (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Rights Management Client API

   * Creare un `DocumentSecurityServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Specificare gli eventi da cercare

   * Creare un `EventSpec` oggetto utilizzando il relativo costruttore.
   * Specificare l&#39;inizio del periodo di tempo durante il quale si è verificato l&#39;evento impostando il membro `EventSpec` dati dell&#39;oggetto con `firstTime.date` `DataTime` l&#39;istanza che rappresenta l&#39;inizio dell&#39;intervallo di date in cui si è verificato l&#39;evento.
   * Assegnare il valore `true` al membro dati dell&#39; `EventSpec` oggetto `firstTime.dateSpecified` .
   * Specificare la fine del periodo di tempo durante il quale si è verificato l&#39;evento impostando il membro `EventSpec` dati dell&#39;oggetto con `lastTime.date` `DataTime` l&#39;istanza che rappresenta la fine dell&#39;intervallo di date in cui si è verificato l&#39;evento.
   * Assegnare il valore `true` al membro dati dell&#39; `EventSpec` oggetto `lastTime.dateSpecified` .
   * Impostare l&#39;evento da cercare assegnando un valore stringa al membro dati dell&#39; `EventSpec` oggetto `eventCode` . Nella tabella seguente sono elencati i valori numerici che è possibile assegnare a questa proprietà:

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

   Cercare l&#39;evento richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `searchForEvents` e passando l&#39;oggetto `EventSpec` che rappresenta l&#39;evento per il quale eseguire la ricerca e il numero massimo di risultati. Questo metodo restituisce una `MyArrayOf_xsd_anyType` raccolta in cui ogni elemento è un&#39; `AuditSpec` istanza. Utilizzando un&#39; `AuditSpec` istanza, potete ottenere informazioni sull&#39;evento, ad esempio l&#39;ora in cui si è verificato. L&#39; `AuditSpec` istanza contiene un membro `timestamp` dati che specifica queste informazioni.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Rights Management, consultate le seguenti Guide rapide:

* &quot;Avvio rapido (MTOM): Ricerca di eventi tramite l&#39;API del servizio Web&quot;
* &quot;Avvio rapido (SwaRef): Ricerca di eventi tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Applicazione dei criteri ai documenti Word {#applying-policies-to-word-documents}

Oltre ai documenti PDF, il servizio Rights Management supporta anche formati di documenti aggiuntivi, ad esempio documenti Microsoft Word (DOC) e altri formati di file Microsoft Office. Ad esempio, è possibile applicare un criterio a un documento Word per proteggerlo. Applicando un criterio a un documento Word, si limita l&#39;accesso al documento. Non è possibile applicare un criterio a un documento se il documento è già protetto con un criterio.

È possibile monitorare l&#39;utilizzo di un documento Word protetto tramite criterio dopo averlo distribuito. In altre parole, potete vedere come viene utilizzato il documento e chi lo sta utilizzando. Ad esempio, è possibile verificare quando un utente ha aperto il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revoca dell&#39;accesso ai documenti](protecting-documents-policies.md#revoking-access-to-documents)

### Applicazione di un criterio a un documento Word tramite l&#39;API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Applicate un criterio a un documento Word utilizzando l&#39;API di Document Security (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Document Security Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `DocumentSecurityClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un documento Word.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento Word utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento Word.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Applicare un criterio esistente al documento Word.

   * Creare un `DocumentManager` oggetto richiamando il `DocumentSecurityClient` metodo dell&#39; `getDocumentManager` oggetto.
   * Applicare un criterio al documento Word richiamando il metodo dell&#39; `DocumentManager` oggetto `protectDocument` e passando i seguenti valori:

      * L&#39; `com.adobe.idp.Document` oggetto che contiene il documento Word a cui viene applicato il criterio.
      * Una stringa che specifica il nome del documento.
      * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. Potete specificare un `null` valore che determina l&#39;utilizzo del set di `MyPolicies` criteri.
      * Una stringa che specifica il nome del criterio.
      * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore successivo del parametro deve essere null).
      * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere `null` (se questo parametro è `null`, il valore del parametro precedente deve essere `null`).
      * Un `com.adobe.livecycle.rightsmanagement.Locale` che rappresenta le impostazioni internazionali utilizzate per selezionare il modello di MS Office. Questo valore del parametro è facoltativo ed è possibile specificarlo `null`.

      Il `protectDocument` metodo restituisce un `RMSecureDocumentResult` oggetto che contiene il documento Word protetto tramite criterio.


1. Salvare il documento Word.

   * Richiamare il metodo dell&#39; `RMSecureDocumentResult` oggetto `getProtectedDoc` per ottenere il documento Word protetto tramite criterio. Questo metodo restituisce un `com.adobe.idp.Document` oggetto.
   * Creare un `java.io.File` oggetto e assicurarsi che l&#39;estensione del file sia DOC.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `getProtectedDoc` metodo).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Applicazione di un criterio a un documento Word tramite l&#39;API Java&quot;

### Applicazione di un criterio a un documento Word tramite l&#39;API del servizio Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Applicare un criterio a un documento Word utilizzando l&#39;API di Document Security (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto Document Security Client API.

   * Creare un `DocumentSecurityServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `DocumentSecurityServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperare un documento Word.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento Word a cui è applicato un criterio.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di Word e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. Determinare la dimensione dell&#39;array di byte ottenendo la `System.IO.FileStream` proprietà dell&#39; `Length` oggetto.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Applicare un criterio esistente al documento Word.

   Applicare un criterio al documento Word richiamando il metodo dell&#39; `DocumentSecurityServiceClient` oggetto `protectDocument` e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene il documento Word a cui viene applicato il criterio.
   * Una stringa che specifica il nome del documento.
   * Un valore di stringa che specifica il nome dell&#39;insieme di criteri a cui appartiene il criterio. Potete specificare un `null` valore che determina l&#39;utilizzo del set di `MyPolicies` criteri.
   * Una stringa che specifica il nome del criterio.
   * Una stringa che rappresenta il nome del dominio di gestione utenti dell&#39;utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro successivo deve essere `null`).
   * Una stringa che rappresenta il nome del nome canonico dell&#39;utente manager utente che è l&#39;editore del documento. Questo valore del parametro è facoltativo e può essere nullo (se questo parametro è nullo, il valore del parametro precedente deve essere `null`).
   * Un `RMLocale` valore che specifica il valore delle impostazioni internazionali (ad esempio, `RMLocale.en`).
   * Un parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore del criterio.
   * Parametro di output della stringa utilizzato per memorizzare il valore dell&#39;identificatore protetto tramite criterio.
   * Un parametro di output della stringa utilizzato per memorizzare il tipo mime (ad esempio, `application/doc`).

   Il `protectDocument` metodo restituisce un `BLOB` oggetto che contiene il documento Word protetto tramite criterio.

1. Salvare il documento Word.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word protetto tramite criterio.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `protectDocument` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file Word richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (MTOM): Applicazione di un criterio a un documento Word tramite l&#39;API del servizio Web&quot;

## Rimozione di criteri dai documenti di Word {#removing-policies-from-word-documents}

È possibile rimuovere un criterio da un documento Word protetto tramite criterio per rimuovere la protezione dal documento. Se non si desidera più che il documento sia protetto tramite un criterio. Se si desidera aggiornare un documento Word protetto tramite criterio con un criterio più recente, invece di rimuovere il criterio e aggiungere il criterio aggiornato, è più efficiente cambiare il criterio.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Document Security, consultate Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

È possibile rimuovere un criterio da un documento Word protetto tramite criterio a condizione che nelle impostazioni di connessione sia specificato un amministratore. In caso contrario, il criterio utilizzato per proteggere un documento deve contenere l&#39; `SWITCH_POLICY` autorizzazione per rimuovere un criterio da un documento Word. Inoltre, anche l&#39;utente specificato nelle impostazioni di connessione AEM Forms deve disporre di tale autorizzazione. In caso contrario, viene generata un&#39;eccezione.

**Salvare il documento Word non protetto**

Dopo che il servizio Document Security rimuove un criterio da un documento Word, potete salvare il documento Word non protetto come file DOC.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Applicazione dei criteri ai documenti Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Rimozione di un criterio da un documento Word tramite l&#39;API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Rimuovete un criterio da un documento Word protetto tramite criterio utilizzando l&#39;API di Document Security (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-rightsmanagement-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Document Security

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `RightsManagementClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recupero di un documento Word protetto tramite criterio

   * Creare un `java.io.FileInputStream` oggetto che rappresenti il documento Word protetto tramite criterio utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento Word.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Rimuovere il criterio dal documento Word

   * Creare un `DocumentManager` oggetto richiamando il `RightsManagementClient` metodo dell&#39; `getDocumentManager` oggetto.
   * Rimuovere un criterio dal documento Word richiamando il `DocumentManager` metodo dell&#39; `removeSecurity` oggetto e passando l&#39; `com.adobe.idp.Document` oggetto che contiene il documento Word protetto tramite criterio. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che contiene un documento Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un `java.io.File` oggetto e assicurarsi che l&#39;estensione del file sia DOC.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `removeSecurity` metodo).

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (modalità SOAP): Rimozione di un criterio da un documento Word tramite l&#39;API Java&quot;

### Rimozione di un criterio da un documento Word tramite l&#39;API del servizio Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Rimuovete un criterio da un documento Word protetto tramite criterio utilizzando l&#39;API di Document Security (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un oggetto API client Document Security

   * Creare un `RightsManagementServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `RightsManagementServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `RightsManagementServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupero di un documento Word protetto tramite criterio

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento Word protetto tramite criterio dal quale viene rimosso il criterio.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di Word e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Rimuovere il criterio dal documento Word

   Rimuovere il criterio dal documento Word richiamando il `RightsManagementServiceClient` metodo dell&#39; `removePolicySecurity` oggetto e passando l&#39; `BLOB` oggetto che contiene il documento Word protetto tramite criterio. Questo metodo restituisce un `BLOB` oggetto che contiene un documento Word non protetto.

1. Salvare il documento Word non protetto

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento Word non protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `removePolicySecurity` metodo. Compilare l&#39;array di byte ottenendo il valore del campo dell&#39; `BLOB` oggetto `MTOM` .
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.

**Esempi di codice**

Per esempi di codice che utilizzano il servizio Document Security, consultate la seguente sezione Avvio rapido:

* &quot;Avvio rapido (MTOM): Rimozione di un criterio da un documento Word tramite l&#39;API del servizio Web&quot;

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
