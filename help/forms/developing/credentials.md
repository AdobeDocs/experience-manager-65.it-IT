---
title: Utilizzo delle credenziali
seo-title: Utilizzo delle credenziali
description: Importa le credenziali in AEM Forms utilizzando l'API di Trust Manager e l'API Java. Inoltre, scopri come eliminare le credenziali utilizzando l’API di Trust Manager e l’API Java.
seo-description: Importa le credenziali in AEM Forms utilizzando l'API di Trust Manager e l'API Java. Inoltre, scopri come eliminare le credenziali utilizzando l’API di Trust Manager e l’API Java.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# Utilizzo delle credenziali {#working-with-credentials}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio credenziali**

Una credenziale contiene le informazioni di chiave privata necessarie per firmare o identificare i documenti. Un certificato è un&#39;informazione a chiave pubblica configurata per l&#39;attendibilità. AEM Forms utilizza certificati e credenziali per diversi scopi:

* Le estensioni Acrobat Reader DC utilizzano una credenziale per abilitare i diritti di utilizzo di Adobe Reader nei documenti PDF. (Vedere [Applicazione dei diritti di utilizzo ai documenti PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* Il servizio Firma accede a certificati e credenziali durante l’esecuzione di operazioni quali la firma digitale di documenti PDF. (Consultare [Firma digitale di documenti PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

È possibile interagire in modo programmatico con il servizio Credenziali utilizzando l&#39;API Java di Trust Manager. È possibile eseguire le seguenti attività:

* [Importazione delle credenziali tramite l’API di Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Eliminazione delle credenziali tramite l&#39;API di Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>È inoltre possibile importare ed eliminare i certificati utilizzando la console di amministrazione. (Consultare [guida all&#39;amministrazione.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importazione delle credenziali tramite l’API di Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

È possibile importare una credenziale in AEM Forms a livello di programmazione utilizzando l’API di Trust Manager. Ad esempio, è possibile importare una credenziale utilizzata per firmare un documento PDF. (Consultare [Firma digitale di documenti PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Quando si importa una credenziale, è necessario specificare un alias per la credenziale. L’alias viene utilizzato per eseguire un’operazione Forms che richiede una credenziale. Una volta importate, le credenziali possono essere visualizzate nella console di amministrazione, come illustrato di seguito. L&#39;alias della credenziale è *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Non è possibile importare una credenziale in AEM Forms utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary-of-steps}

Per importare una credenziale in AEM Forms, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client di servizio delle credenziali.
1. Fai riferimento alla credenziale.
1. Esegui l’operazione di importazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di servizio delle credenziali**

Prima di importare una credenziale in AEM Forms a livello di programmazione, crea un client di servizio delle credenziali. Per informazioni, vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Riferimento alla credenziale**

Fai riferimento a una credenziale da importare in AEM Forms. L&#39;avvio rapido associato a questa sezione fa riferimento a un file P12 che si trova nel file system.

**Esegui l’operazione di importazione**

Dopo aver fatto riferimento alla credenziale, importala in AEM Forms. Se la credenziale non viene importata correttamente, viene generata un&#39;eccezione. Quando si importa una credenziale, è necessario specificare un alias per la credenziale.

**Consulta anche**

[Importare credenziali tramite l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio credenziali](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Eliminazione delle credenziali tramite l&#39;API di Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importare le credenziali utilizzando l&#39;API Java {#import-credentials-using-the-java-api}

Importare una credenziale in AEM Forms utilizzando l’API di Trust Manager (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-truststore-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di servizio delle credenziali

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `CredentialServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento alla credenziale

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione della credenziale.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza le credenziali utilizzando il costruttore `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene la credenziale al costruttore.

1. Esegui l’operazione di importazione

   * Creare un array di stringhe contenente un elemento. Assegna il valore `truststore.usage.type.sign` all’elemento.
   * Richiama il metodo `importCredential` dell&#39;oggetto `CredentialServiceClient` e passa i seguenti valori:

      * Valore stringa che specifica il valore di alias della credenziale.
      * L&#39;istanza `com.adobe.idp.Document` che memorizza le credenziali.
      * Valore stringa che specifica la password associata alla credenziale.
      * Array di stringhe contenente il valore di utilizzo. Ad esempio, è possibile specificare questo valore `truststore.usage.type.sign`. Per importare una credenziale di estensione del Reader, specifica `truststore.usage.type.lcre`.

**Consulta anche**

[Importazione delle credenziali tramite l’API di Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Avvio rapido (modalità SOAP): Importazione di credenziali tramite l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminazione delle credenziali tramite l&#39;API di Trust Manager {#deleting-credentials-by-using-the-trust-manager-api}

È possibile eliminare in modo programmatico una credenziale utilizzando l&#39;API di Trust Manager. Quando si elimina una credenziale, è necessario specificare un alias corrispondente alla credenziale. Una volta eliminata, non è possibile utilizzare una credenziale per eseguire un&#39;operazione.

>[!NOTE]
>
>Non è possibile eliminare una credenziale in AEM Forms utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per eliminare una credenziale, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client di servizio delle credenziali.
1. Esegui l’operazione di eliminazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di servizio delle credenziali**

Prima di poter eliminare in modo programmatico una credenziale, crea un client del servizio di integrazione dei dati . Quando crei un client di servizio, definisci le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Esegui l’operazione di eliminazione**

Per eliminare una credenziale, specifica l’alias corrispondente alla credenziale. Se si specifica un alias che non esiste, viene generata un&#39;eccezione.

**Consulta anche**

[Importare credenziali tramite l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importare credenziali tramite l’API Java](credentials.md#import-credentials-using-the-java-api)

### Eliminazione delle credenziali tramite l&#39;API Java {#deleting-credentials-using-the-java-api}

Eliminare una credenziale da AEM Forms utilizzando l’API di Trust Manager (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-truststore-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di servizio delle credenziali

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `CredentialServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Esegui l’operazione di eliminazione

   Richiama il metodo `deleteCredential` dell&#39;oggetto `CredentialServiceClient` e passa un valore stringa che specifica il valore dell&#39;alias.

**Consulta anche**

[Eliminazione delle credenziali tramite l&#39;API di Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Avvio rapido (modalità SOAP): Eliminazione delle credenziali tramite l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
