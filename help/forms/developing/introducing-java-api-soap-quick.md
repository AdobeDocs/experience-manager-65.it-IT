---
title: Introduzione a Java API QuickStart
seo-title: Introduzione a Java API QuickStart
description: Introduzione a Java API QuickStart
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---


# Introduzione a Java API Quick Start {#introducing-java-api-quickstart}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

 Adobe  AEM Forms API Quick Start consente di accelerare i vostri sforzi per sviluppare programmi che interagiscono con  servizi AEM Forms. *Gli* avvii rapidi sono programmi completi che puoi copiare e incollare nei tuoi progetti e utilizzare come punto di partenza. Potete eseguire una Avvio rapido per vedere come si comporta e modificarla in base alle vostre esigenze.

 le operazioni AEM Forms possono essere eseguite utilizzando l&#39;API  fortemente tipizzata da AEM Forms e la modalità di connessione deve essere impostata su SOAP.

Java fortemente tipizzato API Quick Start fornisce un elenco di file JAR necessari per eseguire l&#39;applicazione Java. La maggior parte delle avvii rapidi Java è un&#39;applicazione console eseguita all&#39;interno di `main`. Tuttavia, la Guida rapida API fortemente tipizzata in Forms Java è implementata come servlet Java che viene eseguito all&#39;interno di un&#39;applicazione Web.

L’elenco dei file JAR si trova in una sezione di commenti all’inizio della Avvio rapido. Ad esempio, il commento seguente si trova in un avvio rapido di Output ed è un tipico elenco di file JAR trovato in ciascuna Avvio rapido di Java.

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

## Avvio rapido di più servizi {#multiple-services-quick-start}

La maggior parte delle soluzioni di avvio rapido disponibili in *Programmazione con  AEM Forms su JEE* richiama un servizio specifico per eseguire un&#39;operazione. Tuttavia, alcuni avvii rapidi richiamano più servizi AEM Forms  per eseguire un determinato flusso di lavoro. Nell&#39;elenco seguente sono riportati gli avvii rapidi Java che richiamano più di un servizio AEM Forms :

[Avvio rapido (modalità SOAP): Trasmissione di un documento situato nell&#39;archivio AEM Forms  al servizio Output tramite l&#39;API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)  Java (richiama il servizio Repository e Output)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF basato su frammenti tramite l&#39;API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)  Java (richiama il servizio Assembler e Output)

[Avvio rapido (modalità SOAP): Creazione di documenti PDF con dati XML inviati tramite l&#39;API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)  Java (richiama il servizio Forms, Output e Document Management)

[Avvio rapido (modalità SOAP): Invio di documenti al servizio Forms tramite l&#39;API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)  Java (richiama il servizio Forms e Document Management)

[Avvio rapido (modalità SOAP): Firma digitale di un modulo basato su XFA tramite l&#39;API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)  Java (richiama il servizio Forms e Firma)

[Avvio rapido (modalità SOAP): Gestione di ruoli e autorizzazioni mediante l&#39;API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)  Java (richiama DirectoryManager e il servizio AuthorizationManager)

[Avvio rapido (modalità SOAP): Trasmissione di documenti al servizio di output tramite l&#39;API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)  Java (invocate il servizio Output e Gestione documenti)

>[!NOTE]
>
>La sezione Avvio rapido nella programmazione con  AEM Forms si basa su  AEM Forms implementato in JBoss® Application Server e nel sistema operativo Microsoft® Windows®. Tuttavia, se si utilizza un altro sistema operativo, come UNIX®, sostituire percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Allo stesso modo, se utilizzate un altro server applicazione J2EE, accertatevi di specificare proprietà di connessione valide. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La maggior parte dei servizi Web Quick Starts è scritta in C# e utilizza .NET framework. Tuttavia, è possibile creare logica dell&#39;applicazione client in grado di richiamare  servizi AEM Forms in qualsiasi ambiente di sviluppo che supporti gli standard SOAP. (Vedere [Chiamata  AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

