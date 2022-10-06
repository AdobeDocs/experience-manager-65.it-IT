---
title: Guida introduttiva all’API Java
seo-title: Introducing Java API QuickStart
description: Guida introduttiva all’API Java
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

# Guida introduttiva a Java API {#introducing-java-api-quickstart}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Adobe AEM Forms API Quick Start ti consente di accelerare i tuoi sforzi per sviluppare programmi che interagiscono con i servizi AEM Forms. *Guida introduttiva* s sono programmi completi che puoi copiare e incollare nei tuoi progetti e utilizzare come punto di partenza. È possibile eseguire una Avvio rapido per vedere come si comporta e modificarla in base alle proprie esigenze.

Le operazioni AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

Java fortemente tipizzato API Quick Start fornisce un elenco dei file JAR necessari per eseguire l&#39;applicazione Java. La maggior parte dei Java Quick Starts sono applicazioni console eseguite in `main`. Tuttavia, la Guida rapida all’API fortemente tipizzata per Forms Java è implementata come servlet Java che viene eseguito all’interno di un’applicazione web.

L’elenco dei file JAR si trova in una sezione di commento all’inizio della Guida rapida. Ad esempio, il seguente commento si trova in un avvio rapido di Output ed è un tipico elenco di file JAR che si trova in ogni avvio rapido di Java.

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

## Guida rapida a più servizi {#multiple-services-quick-start}

Avvii più rapidi situati in *Programmazione con AEM Forms su JEE* richiamare un servizio specifico per eseguire un&#39;operazione. Tuttavia, alcuni Quick Starts richiamano più servizi AEM Forms per eseguire un determinato flusso di lavoro. Nell’elenco seguente sono riportati gli avvii rapidi Java che richiamano più di un servizio AEM Forms:

[Avvio rapido (modalità SOAP): Trasmissione di un documento situato nell’archivio AEM Forms al servizio Output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (richiama il servizio Repository e Output)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF basato su frammenti tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) (richiama il servizio Assembler e Output)

[Avvio rapido (modalità SOAP): Creazione di documenti PDF con dati XML inviati tramite API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (richiama il servizio Forms, Output e Document Management)

[Avvio rapido (modalità SOAP): Trasmissione di documenti al servizio Forms tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (richiama il servizio Forms e Document Management)

[Avvio rapido (modalità SOAP): Firma digitale di un modulo basato su XFA tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (richiama il servizio Forms e Signature)

[Avvio rapido (modalità SOAP): Gestione di ruoli e autorizzazioni tramite l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) (richiama DirectoryManager e il servizio AuthorizationManager )

[Avvio rapido (modalità SOAP): Trasmissione di documenti al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (richiamare il servizio Output e Document Management)

>[!NOTE]
>
>Quick Start situato in Programmazione con AEM Forms si basa sulla distribuzione di AEM Forms su JBoss® Application Server e sul sistema operativo Microsoft® Windows®. Tuttavia, se utilizzi un altro sistema operativo, ad esempio UNIX®, sostituisci percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Allo stesso modo, se utilizzi un altro server applicativo J2EE, assicurati di specificare proprietà di connessione valide. (Vedi [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La maggior parte dei servizi Web Quick Starts viene scritta in C# e utilizza il framework .NET. Tuttavia, è possibile creare una logica di applicazione client in grado di richiamare i servizi AEM Forms in qualsiasi ambiente di sviluppo che supporti gli standard SOAP. (Vedi [Richiamo di AEM Forms tramite servizi web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
