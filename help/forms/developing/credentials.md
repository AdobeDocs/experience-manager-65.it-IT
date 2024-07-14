---
title: Utilizzo delle credenziali
description: Importa le credenziali in AEM Forms utilizzando l’API di Trust Manager e l’API Java. Inoltre, scopri come eliminare le credenziali utilizzando l’API di Trust Manager e l’API Java.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---

# Utilizzo delle credenziali {#working-with-credentials}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio credenziali**

Una credenziale contiene le informazioni sulla chiave privata necessarie per la firma o l&#39;identificazione dei documenti. Un certificato è costituito da informazioni sulla chiave pubblica configurate per l&#39;attendibilità. AEM Forms utilizza certificati e credenziali per diversi scopi:

* Le estensioni Acrobat Reader DC utilizzano una credenziale per abilitare i diritti di utilizzo di Adobe Reader nei documenti PDF. (Vedi [Applicazione dei diritti di utilizzo ai documenti di PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* Il servizio di firma accede a certificati e credenziali durante l&#39;esecuzione di operazioni quali la firma digitale di documenti PDF. (Vedi [Documenti PDF Con Firma Digitale](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

È possibile interagire in modo programmatico con il servizio Credential utilizzando l’API Java di Trust Manager. Puoi eseguire le seguenti attività:

* [Importazione delle credenziali tramite l&#39;API di Gestione trust](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Eliminazione delle credenziali tramite l’API di Gestione trust](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>È inoltre possibile importare ed eliminare certificati utilizzando la console di amministrazione. (Vedi [guida per l&#39;amministrazione.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importazione delle credenziali tramite l&#39;API di Gestione trust {#importing-credentials-by-using-the-trust-manager-api}

È possibile importare in modo programmatico una credenziale in AEM Forms utilizzando l’API di Trust Manager. È ad esempio possibile importare le credenziali utilizzate per firmare un documento PDF. (Vedi [Documenti Di PDF Con Firma Digitale](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Quando si importa una credenziale, è necessario specificare un alias per la credenziale. L&#39;alias viene utilizzato per eseguire un&#39;operazione Forms che richiede una credenziale. Una volta importata, è possibile visualizzare una credenziale nella console di amministrazione, come illustrato nella figura seguente. L&#39;alias per le credenziali è *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Non è possibile importare credenziali in AEM Forms utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary-of-steps}

Per importare una credenziale in AEM Forms, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio delle credenziali.
1. Fai riferimento alle credenziali.
1. Eseguire l&#39;operazione di importazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client del servizio credenziali**

Prima di importare a livello di programmazione una credenziale in AEM Forms, creare un client del servizio delle credenziali. Per informazioni, vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Fai riferimento alle credenziali**

Fai riferimento a una credenziale da importare in AEM Forms. L&#39;avvio rapido associato a questa sezione fa riferimento a un file P12 nel file system.

**Operazione di importazione**

Dopo aver fatto riferimento alle credenziali, importale in AEM Forms. Se le credenziali non vengono importate correttamente, viene generata un&#39;eccezione. Quando si importa una credenziale, è necessario specificare un alias per la credenziale.

**Consulta anche**

[Importare le credenziali tramite API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio credenziali](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Eliminazione delle credenziali tramite l’API di Gestione trust](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importare le credenziali tramite API Java {#import-credentials-using-the-java-api}

Importa una credenziale in AEM Forms utilizzando l’API di Trust Manager (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-truststore-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio delle credenziali

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `CredentialServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento alle credenziali

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione delle credenziali.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza le credenziali utilizzando il costruttore `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene le credenziali al costruttore.

1. Eseguire l&#39;operazione di importazione

   * Creare una matrice di stringhe contenente un elemento. Assegnare il valore `truststore.usage.type.sign` all&#39;elemento.
   * Richiama il metodo `importCredential` dell&#39;oggetto `CredentialServiceClient` e passa i seguenti valori:

      * Valore stringa che specifica il valore alias per le credenziali.
      * L&#39;istanza `com.adobe.idp.Document` che memorizza le credenziali.
      * Valore stringa che specifica la password associata alle credenziali.
      * Matrice di stringhe contenente il valore di utilizzo. È ad esempio possibile specificare il valore `truststore.usage.type.sign`. Per importare le credenziali di un&#39;estensione di Reader, specificare `truststore.usage.type.lcre`.

**Consulta anche**

[Importazione delle credenziali tramite l&#39;API di Gestione trust](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Quick Start (modalità SOAP): importazione delle credenziali tramite l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminazione delle credenziali tramite l’API di Gestione trust {#deleting-credentials-by-using-the-trust-manager-api}

È possibile eliminare le credenziali a livello di programmazione utilizzando l&#39;API di Gestione fonti attendibili. Quando si elimina una credenziale, si specifica un alias corrispondente alla credenziale. Una volta eliminate, non è possibile utilizzare le credenziali per eseguire un&#39;operazione.

>[!NOTE]
>
>Non è possibile eliminare una credenziale in AEM Forms utilizzando i servizi Web.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per eliminare una credenziale, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio delle credenziali.
1. Eseguire l&#39;operazione di eliminazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client del servizio credenziali**

Prima di eliminare programmaticamente una credenziale, creare un client del servizio di integrazione dati. Quando si crea un client di servizio, vengono definite le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Operazione di eliminazione**

Per eliminare una credenziale, specificare l&#39;alias corrispondente alla credenziale. Se si specifica un alias che non esiste, viene generata un&#39;eccezione.

**Consulta anche**

[Importare le credenziali tramite API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importare le credenziali tramite API Java](credentials.md#import-credentials-using-the-java-api)

### Eliminazione delle credenziali tramite API Java {#deleting-credentials-using-the-java-api}

Eliminare una credenziale da AEM Forms utilizzando l’API di gestione del trust (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-truststore-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio delle credenziali

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `CredentialServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Eseguire l&#39;operazione di eliminazione

   Richiama il metodo `deleteCredential` dell&#39;oggetto `CredentialServiceClient` e passa un valore stringa che specifica il valore alias.

**Consulta anche**

[Eliminazione delle credenziali tramite l’API di Gestione trust](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Quick Start (modalità SOAP): eliminazione delle credenziali tramite l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
