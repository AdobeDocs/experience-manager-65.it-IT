---
title: Installazione e configurazione del server di protezione dei documenti
seo-title: Installazione e configurazione del server di protezione dei documenti
description: 'Utilizzare la protezione dei documenti per distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere a documenti protetti. '
seo-description: 'Utilizzare la protezione dei documenti per distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere a documenti protetti. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
role: Admin
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Installazione e configurazione del server di protezione dei documenti {#installing-and-configuring-the-document-security-server}

Utilizzare la protezione dei documenti per distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere a documenti protetti.

La protezione dei documenti Adobe Experience Manager Forms garantisce che solo gli utenti autorizzati possano utilizzare i documenti. Utilizzando la protezione dei documenti, è possibile distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. I formati di file supportati includono file PDF (Adobe Portable Document Format) e Microsoft Word, Excel e PowerPoint.

È possibile proteggere i documenti utilizzando i criteri. Le impostazioni di riservatezza specificate in un criterio determinano in che modo un destinatario può utilizzare un documento a cui applicare il criterio. Ad esempio, è possibile specificare se i destinatari possono stampare o copiare testo, modificare testo o aggiungere firme e commenti ai documenti protetti.

I criteri sono memorizzati sul server di sicurezza dei documenti; i criteri vengono applicati ai documenti tramite l&#39;applicazione client. Quando si applica un criterio a un documento, le impostazioni di riservatezza specificate nel criterio proteggono le informazioni contenute nel documento. Puoi distribuire il documento protetto tramite criterio ai destinatari autorizzati dal criterio.

La sicurezza dei documenti fornisce inoltre client, visualizzatori e indicizzatori per proteggere i documenti, visualizzare documenti protetti e indicizzare documenti protetti. Per informazioni dettagliate sulla protezione dei documenti, vedere [informazioni sulla protezione dei documenti](/help/forms/using/admin-help/document-security.md).

## Topologia di distribuzione  {#deployment-topology}

La funzionalità di sicurezza dei documenti è disponibile solo in AEM Forms su JEE. È necessaria una singola istanza di AEM Forms su JEE. Se necessario, puoi anche creare un cluster o una farm di server AEM Forms. La topologia seguente è indicativa per eseguire la funzionalità di protezione del documento. Per informazioni dettagliate sulla topologia, consulta [Architettura e topologie di distribuzione per AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

Il diagramma seguente illustra l’architettura tipica di AEM Forms Document Security:

![](do-not-localize/document-security-typical-environment.png)

## Installazione di AEM Forms in JEE {#installing-aem-forms-on-jee}

Esegui i seguenti passaggi per installare e configurare AEM Forms su JEE:

1. Scarica il programma di installazione di Forms 6.5 AEM su JEE dal [sito Web di licenze di Adobe (LWS)](https://licensing.adobe.com/). Per scaricare il programma di installazione è necessario un contratto di manutenzione e supporto valido.
1. Leggi il documento [AEM Forms sulle piattaforme supportate JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) e assicurati che il software, l&#39;hardware, i sistemi operativi, il server applicazioni, i database, i JDK e altre infrastrutture siano pronti per installare AEM Forms su JEE.
1. (Solo installazioni non chiavi in mano) Leggi la sezione [Preparazione all&#39;installazione del singolo server AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) o [Preparazione all&#39;installazione del cluster di server AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) e prepara il tuo ambiente per installare e configurare AEM Forms su JEE.
1. A seconda dell&#39;ambiente e del server applicazioni, scegli uno dei seguenti documenti e segui le istruzioni per completare l&#39;installazione

   * [Installazione e distribuzione di AEM Forms su JEE tramite chiavi in mano JBoss](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Installazione e distribuzione di AEM Forms su JEE per JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Installazione e distribuzione di AEM Forms su JEE per WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Installazione e distribuzione di AEM Forms su JEE per WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configurazione di AEM Forms su JEE nel cluster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configurazione di AEM Forms su JEE nel cluster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configurazione di AEM Forms su JEE nel cluster WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >Nella schermata di selezione del modulo di AEM Forms su JEE configuration manager, seleziona l’opzione Document Security. L&#39;opzione Sicurezza documento non richiede la selezione di altri moduli.

## Passaggi successivi {#next-steps}

* [Configurare le opzioni client e server](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Creazione e gestione dei criteri](/help/forms/using/admin-help/creating-policies.md)
* [Creazione e gestione dei set di criteri](/help/forms/using/admin-help/creating-policy-sets.md)
