---
title: Errori di servizio CRX/bundle e Start page non disponibili dopo l’installazione del service pack 6.5.15.0 più recente
description: Errori di servizio CRX/bundle e Start page non disponibili dopo l’installazione del service pack 6.5.15.0 più recente
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---

# Errore di servizio non disponibile dopo l’installazione del service pack AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problema   {#issue}

Dopo aver installato [Service Pack di AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), l’errore si verifica come:
* ERRORE [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: impossibile risolvere org.apache.sling.scripting.console

Dopo aver installato il service pack AEM 6.5.15.0, CRX/bundle e la pagina iniziale mostrano gli errori di servizio non disponibili.

## Applicabile a {#applies-to}

Questa soluzione si applica a:
* AEM Forms su tutti i server JEE eccetto quelli in esecuzione su JBoss EAP 7.4.0

## Soluzione {#solution}

>[!NOTE]
>
>I passaggi per la risoluzione dei problemi sono applicabili a tutti i server applicazioni ad eccezione di JBoss EAP 7.4.

Dopo l’installazione [Service Pack di AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), se CRX/bundle e la pagina iniziale mostrano errori di servizio non disponibile, effettua le seguenti operazioni:

1. Arrestare il server applicazioni.
1. Accedi a `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Individua il `bundle.info` file.
1. Apri `bundle.info` nell’editor di testo ant e cerca il nome del bundle come `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Se il valore `bundle.info` in `bundle52` non contiene `org.apache.felix.http.bridge` il numero del bundle tra parentesi quadre accanto al simbolo `org.apache.felix.http.bridge`. Quindi vai a [directory principale di aem-forms]\crx-repository\launchpad\felix\bundle[x] ed eseguire i passaggi successivi in questa posizione.

1. Passa a URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Cerca `bundle.jar` e rinominare `bundle.jar` a `bundle.jar.bak`.
1. Copia il `Bundle for AEM 6.5 Forms on JEE Service Pack 15` in questa posizione da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Avvia il server applicazioni, attendi che i registri si stabilizzino e verifichi lo stato del bundle.
1. Una volta che tutti i bundle sono in stato attivo, installa [Frammento per AEM 6.5 Forms su JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) dal `system/console/bundles` e attendere che il server applicazioni si stabilizzi.
1. Arrestare il server applicazioni.
1. Accedi a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` ed elimina `bundle.jar`.
1. Rinomina il `bundle.jar.bak` al `bundle.jar`.
1. Avviare il server applicazioni.
