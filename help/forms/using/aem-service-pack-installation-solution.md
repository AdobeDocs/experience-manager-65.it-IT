---
title: Errore non disponibile del servizio CRX/bundle e Start page dopo l'installazione del service pack 6.5.15.0 più recente
description: Errore non disponibile del servizio CRX/bundle e Start page dopo l'installazione del service pack 6.5.15.0 più recente
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
source-git-commit: e961f0c7107b4eacb0d5e50565cb64f5fa30e265
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---

# Errore non disponibile del servizio dopo l&#39;installazione del service pack AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problema   {#issue}

Dopo aver installato [Service Pack di AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), l’errore si verifica come:
* ERRORE [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException): Impossibile risolvere org.apache.sling.scripting.console

Dopo aver installato AEM service pack 6.5.15.0, il CRX/bundle e la pagina iniziale mostrano errori non disponibili del servizio.

## Si applica a {#applies-to}

Questa soluzione si applica a:
* AEM Forms su tutti i server JEE, eccetto quelli in esecuzione su JBoss EAP 7.4.0

## Soluzione {#solution}

>[!NOTE]
>
>I passaggi per la risoluzione dei problemi sono applicabili a tutti i server delle applicazioni ad eccezione di JBoss EAP 7.4.

Dopo l&#39;installazione [Service Pack di AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), se il CRX/bundle e la pagina iniziale mostrano errori di servizio non disponibili, esegui i seguenti passaggi:

1. Arrestare il server applicazioni.
1. Accedi a `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Individua il `bundle.info` file.
1. Apri `bundle.info` nell&#39;editor di testo formativo e cerca il nome del bundle come `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Nel caso in cui `bundle.info` sotto `bundle52` non contiene il `org.apache.felix.http.bridge` bundle, controlla il numero del bundle in parentesi quadre accanto al `org.apache.felix.http.bridge`. Quindi passa a [root di aem forms]\crx-repository\launchpad\felix\bundle[x] ed esegui i passaggi successivi in questa posizione.

1. Accedi all’URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Cerca `bundle.jar` e rinomina il `bundle.jar` a `bundle.jar.bak`.
1. Copia il `Bundle for AEM 6.5 Forms on JEE Service Pack 15` in questa posizione dal [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Avvia l&#39;application server, attendi che i registri si stabilizzino e controlla lo stato del bundle.
1. Una volta che tutti i bundle sono nello stato attivo, installa il [Frammento per Forms 6.5 AEM su JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) dal `system/console/bundles` e attendere la stabilizzazione del server applicazioni.
1. Arrestare il server applicazioni.
1. Passa a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` ed eliminare `bundle.jar`.
1. Rinomina il `bundle.jar.bak` al `bundle.jar`.
1. Avvia l&#39;application server.