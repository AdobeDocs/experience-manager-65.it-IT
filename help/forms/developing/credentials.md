---
title: Utilizzo delle credenziali
seo-title: Utilizzo delle credenziali
description: 'null'
seo-description: 'null'
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 0%

---


# Utilizzo delle credenziali {#working-with-credentials}

**Informazioni sul servizio credenziali**

Una credenziale contiene le informazioni di chiave privata necessarie per firmare o identificare i documenti. Un certificato è un&#39;informazione di chiave pubblica configurata per l&#39;attendibilità.  AEM Forms utilizza certificati e credenziali per diversi scopi:

* Le estensioni Acrobat Reader DC utilizzano una credenziale per abilitare  diritti di utilizzo Adobe Reader nei documenti PDF. (Vedere [Applicazione dei diritti di utilizzo ai documenti PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* Il servizio Signature accede a certificati e credenziali durante l&#39;esecuzione di operazioni quali la firma digitale di documenti PDF. (Vedere [Firma digitale di documenti PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

È possibile interagire in modo programmatico con il servizio Credential utilizzando l&#39;API Java di Trust Manager. È possibile effettuare le seguenti operazioni:

* [Importazione di credenziali tramite l&#39;API di Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Eliminazione delle credenziali tramite l&#39;API di Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>È inoltre possibile importare ed eliminare i certificati utilizzando la console di amministrazione. (Vedere [guida di amministrazione.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importazione di credenziali tramite l&#39;API di Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

È possibile importare una credenziale in  AEM Forms a livello di programmazione utilizzando l&#39;API di Trust Manager. Ad esempio, è possibile importare una credenziale utilizzata per firmare un documento PDF. (Vedere [Firma digitale di documenti PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Quando importate una credenziale, specificate un alias per la credenziale. L&#39;alias viene utilizzato per eseguire un&#39;operazione Forms che richiede una credenziale. Una volta importata, una credenziale può essere visualizzata nella console di amministrazione, come illustrato nella figura seguente. Tenere presente che l&#39;alias della credenziale è *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Non è possibile importare una credenziale in  AEM Forms utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary-of-steps}

Per importare una credenziale in  AEM Forms, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio delle credenziali.
1. Fare riferimento alla credenziale.
1. Eseguire l’operazione di importazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di servizio credenziali**

Prima di importare una credenziale in  AEM Forms a livello di programmazione, creare un client di servizi credenziale. Per informazioni, vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Riferimento alla credenziale**

Fate riferimento a una credenziale da importare in  AEM Forms. L&#39;avvio rapido associato a questa sezione fa riferimento a un file P12 che si trova nel file system.

**Eseguire l&#39;operazione di importazione**

Dopo aver fatto riferimento alla credenziale, importate la credenziale in  AEM Forms. Se la credenziale non viene importata correttamente, viene generata un&#39;eccezione. Quando importate una credenziale, specificate un alias per la credenziale.

**Consulta anche**

[Importare le credenziali tramite l&#39;API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio credenziali](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Eliminazione delle credenziali tramite l&#39;API di Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importare le credenziali tramite l&#39;API Java {#import-credentials-using-the-java-api}

Importare una credenziale in  AEM Forms utilizzando l&#39;API Trust Manager (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-trust-store-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di servizio credenziali

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `CredentialServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento alla credenziale

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione della credenziale.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza le credenziali utilizzando il costruttore `com.adobe.idp.Document`. Passare l&#39;oggetto `java.io.FileInputStream` che contiene la credenziale al costruttore.

1. Eseguire l&#39;operazione di importazione

   * Creare una matrice di stringhe contenente un elemento. Assegnare il valore `truststore.usage.type.sign` all&#39;elemento.
   * Richiamare il metodo `CredentialServiceClient` dell&#39;oggetto `importCredential` e trasmettere i seguenti valori:

      * Un valore di stringa che specifica il valore alias per la credenziale.
      * L&#39;istanza `com.adobe.idp.Document` che memorizza la credenziale.
      * Valore stringa che specifica la password associata alla credenziale.
      * La matrice stringa che contiene il valore di utilizzo. Ad esempio, è possibile specificare questo valore `truststore.usage.type.sign`. Per importare una credenziale di estensione Reader, specificate `truststore.usage.type.lcre`.

**Consulta anche**

[Importazione di credenziali tramite l&#39;API di Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Avvio rapido (modalità SOAP): Importazione di credenziali tramite l&#39;API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminazione delle credenziali tramite l&#39;API di Trust Manager {#deleting-credentials-by-using-the-trust-manager-api}

È possibile eliminare una credenziale a livello di programmazione utilizzando l&#39;API di Trust Manager. Quando eliminate una credenziale, specificate un alias corrispondente alla credenziale. Una volta eliminata, non è possibile utilizzare una credenziale per eseguire un&#39;operazione.

>[!NOTE]
>
>Non è possibile eliminare una credenziale in  AEM Forms utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per eliminare una credenziale, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio delle credenziali.
1. Eseguire l&#39;operazione di eliminazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di servizio credenziali**

Prima di eliminare una credenziale a livello di programmazione, creare un client di servizi di integrazione dati. Quando create un client di servizi, definite le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Eseguire l&#39;operazione di eliminazione**

Per eliminare una credenziale, specificare l&#39;alias corrispondente alla credenziale. Se si specifica un alias che non esiste, viene generata un&#39;eccezione.

**Consulta anche**

[Importare le credenziali tramite l&#39;API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importare le credenziali tramite l&#39;API Java](credentials.md#import-credentials-using-the-java-api)

### Eliminazione delle credenziali tramite l&#39;API Java {#deleting-credentials-using-the-java-api}

Eliminate una credenziale da  AEM Forms utilizzando l&#39;API Trust Manager (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-trust-store-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di servizio credenziali

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `CredentialServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Eseguire l&#39;operazione di eliminazione

   Richiamare il metodo `CredentialServiceClient` dell&#39;oggetto `deleteCredential` e passare un valore di stringa che specifica il valore alias.

**Consulta anche**

[Eliminazione delle credenziali tramite l&#39;API di Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Avvio rapido (modalità SOAP): Eliminazione delle credenziali tramite l&#39;API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
