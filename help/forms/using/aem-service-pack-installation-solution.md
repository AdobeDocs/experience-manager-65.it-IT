---
title: Errori di servizio CRX/bundle e Start page non disponibili dopo l’installazione del service pack 6.5.15.0 più recente
description: Errori di servizio CRX/bundle e Start page non disponibili dopo l’installazione del service pack 6.5.15.0 più recente
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---

# Errore di servizio non disponibile dopo l’installazione del service pack AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problema   {#issue}

Dopo aver installato il [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), l&#39;errore si verifica come segue:
* ERRORE [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: impossibile risolvere org.apache.sling.scripting.console

Dopo aver installato il service pack AEM 6.5.15.0, il CRX/bundle e la pagina iniziale mostrano gli errori di servizio non disponibile.

## Applicabile a {#applies-to}

Questa soluzione si applica a:
* AEM Forms su tutti i server JEE eccetto quelli in esecuzione su JBoss EAP 7.4.0

## Soluzione {#solution}

>[!NOTE]
>
>I passaggi per la risoluzione dei problemi sono applicabili a tutti i server applicazioni ad eccezione di JBoss EAP 7.4.

Dopo aver installato [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), se CRX/bundle e la pagina iniziale mostrano errori di servizio non disponibili, effettuare le seguenti operazioni:

1. Arrestare il server applicazioni.
1. Accedi a `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Individuare il file `bundle.info`.
1. Apri il file `bundle.info` nell&#39;editor di testo ant e cerca il nome del bundle come `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Se `bundle.info` in `bundle52` non contiene il bundle `org.apache.felix.http.bridge`, controlla il numero del bundle tra parentesi quadre accanto a `org.apache.felix.http.bridge`. Passa quindi alla [directory principale di aem-forms]\crx-repository\launchpad\felix\bundle[x] ed esegui i passaggi successivi in questa posizione.

1. Passare all&#39;URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Cercare `bundle.jar` e rinominare `bundle.jar` in `bundle.jar.bak`.
1. Copia `Bundle for AEM 6.5 Forms on JEE Service Pack 15` in questa posizione dalla [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Avvia il server applicazioni, attendi che i registri si stabilizzino e verifichi lo stato del bundle.
1. Una volta che tutti i bundle sono nello stato attivo, installa il [Frammento per AEM 6.5 Forms su JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) da `system/console/bundles` e attendi la stabilizzazione del server applicazioni.
1. Arrestare il server applicazioni.
1. Passare a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` ed eliminare `bundle.jar`.
1. Rinomina `bundle.jar.bak` in `bundle.jar`.
1. Avviare il server applicazioni.
