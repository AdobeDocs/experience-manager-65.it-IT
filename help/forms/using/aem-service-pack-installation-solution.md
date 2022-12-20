---
title: Errore non disponibile del servizio CRX/bundle e Start page dopo l'installazione del service pack 6.5.15.0 più recente
description: Errore non disponibile del servizio CRX/bundle e Start page dopo l'installazione del service pack 6.5.15.0 più recente
source-git-commit: 4e4dca8ae8ed49c5b81934f22572c84938f4f676
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 2%

---


# Errori di servizio non disponibili dopo l&#39;installazione del service pack AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problema   {#issue}

Dopo aver installato [Service Pack di AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), l’errore si verifica come:
* ERRORE [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException): Impossibile risolvere org.apache.sling.scripting.console

Dopo aver installato AEM service pack 6.5.15.0, il CRX/bundle e la pagina iniziale mostrano errori non disponibili del servizio.

## Soluzione {#solution}

>[!NOTE]
>
>I passaggi per la risoluzione dei problemi sono applicabili a tutti i server applicazioni ad eccezione di JBoss EAP 7.4.

Dopo l&#39;installazione [Service Pack di AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), se il CRX/bundle e la pagina iniziale mostrano errori di servizio non disponibili, esegui i seguenti passaggi:

1. Arrestare l&#39;Application Server.
1. Accedi a `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Individua il `bundle.info` file.
1. Apri `bundle.info` nell&#39;editor di testo formativo e cerca il nome del bundle come `org.apache.felix.http.bridge`.

>[!NOTE]
>
>Nel caso in cui `bundle.info` sotto `bundle52` non contiene il `org.apache.felix.http.bridge` bundle, controlla il numero del bundle in parentesi quadre accanto al `org.apache.felix.http.bridge`. Quindi passa a [root di aem forms]\crx-repository\launchpad\felix\bundle[x] ed esegui i passaggi successivi in questa posizione.

1. Accedi all’URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Cerca `bundle.jar` e rinomina il `bundle.jar` a `bundle.jar.bak`.
1. Copia `bundle.jar` in questa posizione dal [Distribuzione di software](https://jira.corp.adobe.com/secure/attachment/9402702/bundle.jar).
1. Avvia l&#39;Application Server, attendi che i registri si stabilizzino e controlla lo stato del bundle.
1. Una volta che tutti i bundle sono nello stato attivato, installa il `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` frammento servlet dal `system/console/bundles` scaricato da [Distribuzione di software.](https://jira.corp.adobe.com/secure/attachment/9396977/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)
1. Di nuovo, attendere che Application Server si stabilizzi.
1. Arrestare l&#39;Application Server.
1. Passa a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` ed eliminare `bundle.jar`.
1. Rinomina il `bundle.jar.bak` al `bundle.jar`.
1. Avviare l&#39;Application Server.

## Si applica a {#applies-to}

Questa soluzione si applica a:
* AEM Forms su tutti i server JEE, eccetto quelli in esecuzione su JBoss EAP 7.4.0
