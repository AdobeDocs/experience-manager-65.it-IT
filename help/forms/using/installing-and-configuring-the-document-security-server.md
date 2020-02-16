---
title: Installazione e configurazione del server di protezione del documento
seo-title: Installazione e configurazione del server di protezione del documento
description: 'La protezione dei documenti consente di distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere ai documenti protetti. '
seo-description: 'La protezione dei documenti consente di distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere ai documenti protetti. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Installazione e configurazione del server di protezione del documento {#installing-and-configuring-the-document-security-server}

La protezione dei documenti consente di distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere ai documenti protetti.

La protezione dei documenti Adobe Experience Manager Forms garantisce che i documenti vengano utilizzati solo dagli utenti autorizzati. La protezione dei documenti consente di distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. I formati di file supportati includono file Adobe PDF (Portable Document Format) e Microsoft Word, Excel e PowerPoint.

È possibile proteggere i documenti utilizzando i criteri. Le impostazioni di riservatezza specificate in un criterio determinano in che modo il destinatario può utilizzare il documento a cui si applica il criterio. Ad esempio, è possibile specificare se i destinatari possono stampare o copiare il testo, modificare il testo o aggiungere firme e commenti ai documenti protetti.

I criteri sono memorizzati in Document Security Server; i criteri vengono applicati ai documenti tramite l&#39;applicazione client. Quando applicate un criterio a un documento, le impostazioni di riservatezza specificate nel criterio proteggono le informazioni contenute nel documento. Potete distribuire il documento protetto tramite criterio ai destinatari autorizzati dal criterio.

Document Security fornisce inoltre client, visualizzatori e indicizzatori per proteggere i documenti, visualizzare i documenti protetti e indicizzare i documenti protetti. Per informazioni dettagliate sulla protezione dei documenti, vedere [Informazioni sulla protezione](/help/forms/using/admin-help/document-security.md)dei documenti.

## Topologia di distribuzione {#deployment-topology}

La funzionalità di protezione dei documenti è disponibile solo in AEM Forms su JEE. È necessaria una singola istanza di AEM Forms su JEE. Se necessario, potete anche creare un cluster o una farm di server AEM Forms. La topologia seguente è una topologia indicativa per eseguire la funzionalità di protezione del documento. Per informazioni dettagliate sulla topologia, consultate Topologie di [architettura e distribuzione per AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

Il diagramma seguente mostra l&#39;architettura tipica di AEM Forms Document Security:

![](do-not-localize/document-security-typical-environment.png)

## Installazione di AEM Forms su JEE {#installing-aem-forms-on-jee}

Per installare e configurare AEM Forms su JEE, effettuate le seguenti operazioni:

1. Scaricate il programma di installazione AEM 6.5 Forms on JEE dal sito Web delle licenze [Adobe (LWS)](https://licensing.adobe.com/). Per scaricare il programma di installazione è necessario un contratto di manutenzione e assistenza valido.
1. Leggi il documento [Moduli](/help/forms/using/aem-forms-jee-supported-platforms.md) AEM su piattaforme supportate JEE e assicurati che il software, l&#39;hardware, i sistemi operativi, il server applicazioni, i database, i JDK e altre infrastrutture siano pronti per installare AEM Forms su JEE.
1. (Solo installazioni non chiavi in mano) Leggi la [sezione Preparazione all’installazione del singolo server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) AEM Forms o [Preparazione all’installazione del cluster](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) di server AEM Forms e prepara il tuo ambiente per installare e configurare AEM Forms su JEE.
1. A seconda dell’ambiente e del server applicazioni, scegliete uno dei documenti seguenti e seguite le istruzioni per completare l’installazione

   * [Installazione e implementazione di AEM Forms su JEE tramite chiavi in mano JBoss](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Installazione e implementazione di AEM Forms su JEE per JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Installazione e implementazione di AEM Forms su JEE per WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Installazione e implementazione di AEM Forms su JEE per WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configurazione di AEM Forms su JEE nel cluster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configurazione di AEM Forms su JEE nel cluster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configurazione di AEM Forms su JEE nel cluster WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)
   >[!NOTE]
   >
   >Nella schermata di selezione dei moduli di AEM Forms su JEE, selezionate l&#39;opzione Document Security. L&#39;opzione Document Security non richiede la selezione di altri moduli.

## Passaggi successivi {#next-steps}

* [Configurare le opzioni client e server](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Creazione e gestione dei criteri](/help/forms/using/admin-help/creating-policies.md)
* [Creazione e gestione di set di criteri](/help/forms/using/admin-help/creating-policy-sets.md)
