---
title: Introduzione a Java API QuickStart
seo-title: Introducing Java API QuickStart
description: Introduzione a Java API QuickStart
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Introduzione a Java API Quick Start {#introducing-java-api-quickstart}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Adobe La Guida introduttiva alle API di AEM Forms può aiutarti ad accelerare gli sforzi per sviluppare programmi che interagiscono con i servizi di AEM Forms. *Guida rapida* s sono programmi completi che puoi copiare e incollare nei tuoi progetti e utilizzare come punto di partenza. Puoi eseguire una Guida rapida per vedere come si comporta e modificarla in base alle tue esigenze.

Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

La Guida introduttiva dell’API fortemente tipizzata Java fornisce un elenco dei file JAR necessari per eseguire l’applicazione Java. La maggior parte dei Quick Start Java sono applicazioni console eseguite in `main`. Tuttavia, Quick Start per API Java fortemente tipizzata di Forms è implementato come servlet Java eseguito all’interno di un’applicazione web.

L’elenco dei file JAR si trova in una sezione di commenti all’inizio della Guida introduttiva. Ad esempio, il seguente commento si trova in un avvio rapido di output ed è un tipico elenco di file JAR trovato in ogni avvio rapido Java.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## Guida introduttiva a più servizi {#multiple-services-quick-start}

La maggior parte degli avvii rapidi si trova in *Programmazione con AEM Forms su JEE* richiama un servizio specifico per eseguire un’operazione. Tuttavia, alcuni Quick Starts richiamano più servizi AEM Forms per eseguire un determinato flusso di lavoro. L’elenco seguente fornisce avvii rapidi Java che richiamano più di un servizio AEM Forms:

[Guida rapida (modalità SOAP): passaggio di un documento che si trova nel repository di AEM Forms al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (richiama il servizio Archivio e output)

[Guida rapida (modalità SOAP): creazione di un documento PDF basato su frammenti tramite API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) (richiama il servizio Assemblatore e output)

[Guida rapida (modalità SOAP): creazione di documenti PDF con dati XML inviati tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (richiama il servizio Forms, Output e Document Management)

[Quick Start (modalità SOAP): passaggio di documenti al servizio Forms utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (richiama il servizio Forms e Document Management)

[Quick Start (modalità SOAP): firma digitale di un modulo basato su XFA tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (richiama il servizio Forms e Signature)

[Quick Start (modalità SOAP): gestione di ruoli e autorizzazioni tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) (richiama il servizio DirectoryManager e AuthorizationManager )

[Quick Start (modalità SOAP): trasferimento di documenti al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (richiama il servizio di gestione documenti e output)

>[!NOTE]
>
>La Guida introduttiva alla programmazione con AEM Forms si basa sulla distribuzione di AEM Forms su JBoss® Application Server e sul sistema operativo Microsoft® Windows®. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX®, sostituire i percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La maggior parte dei servizi Web Quick Starts sono scritti in C# e utilizzano .NET Framework. Tuttavia, è possibile creare una logica dell’applicazione client in grado di richiamare i servizi AEM Forms in qualsiasi ambiente di sviluppo che supporti gli standard SOAP. (vedere [Richiamare AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
