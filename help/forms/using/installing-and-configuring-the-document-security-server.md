---
title: Installazione e configurazione del server di Document Security
description: Utilizza Document Security per distribuire in modo sicuro le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere ai documenti protetti.
contentOwner: khsingh
role: Admin
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication,Document Security
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: aa28c6c8-3ede-445b-a351-eeb0c9f9aec4
    internal-label: Interactive Communication
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 14%
---
# Installazione e configurazione del server di Document Security {#installing-and-configuring-the-document-security-server}

Utilizza Document Security per distribuire in modo sicuro le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere ai documenti protetti.

La funzione di protezione dei documenti di Adobe Experience Manager Forms garantisce che solo gli utenti autorizzati possano utilizzare i documenti. Grazie alla protezione dei documenti è possibile distribuire in modo sicuro le informazioni salvate in un formato supportato. I formati di file supportati sono Adobe Portable Document Format (PDF) e Microsoft Word, Excel e PowerPoint.

È possibile proteggere i documenti utilizzando i criteri. Le impostazioni di riservatezza specificate in una policy determinano il modo in cui un destinatario può utilizzare un documento al quale si applica la policy. È ad esempio possibile specificare se i destinatari possono stampare o copiare testo, modificarlo o aggiungere firme e commenti ai documenti protetti.

Le policy vengono memorizzate nel server di Document Security e applicate ai documenti tramite l’applicazione client. Le informazioni contenute in un documento a cui è stato applicato un criterio, sono protette dalle relative impostazioni di riservatezza definite nel criterio stesso. Puoi distribuire il documento protetto da criterio ai destinatari autorizzati dal criterio stesso.

Document Security fornisce inoltre a client, visualizzatori e indicizzatori la protezione dei documenti, la visualizzazione dei documenti protetti e l’indicizzazione dei documenti protetti. Per informazioni dettagliate sulla protezione dei documenti, consulta [informazioni sulla protezione dei documenti](/help/forms/using/admin-help/document-security.md).

## Topologia di distribuzione  {#deployment-topology}

La funzionalità di protezione dei documenti è disponibile solo in AEM Forms su JEE. È necessaria una singola istanza di AEM Forms su JEE. Se necessario, puoi anche creare un cluster o una farm di server AEM Forms. La topologia seguente è indicativa per l’esecuzione della funzionalità di protezione dei documenti. Per informazioni dettagliate sulla topologia, vedere [Architettura e topologie di distribuzione per AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![Topologia del server di protezione dei documenti](do-not-localize/document-security-server_topology.png)

Il diagramma seguente mostra l’architettura tipica di AEM Forms Document Security:

![Ambiente tipico di Document Security](do-not-localize/document-security-typical-environment.png)

## Installazione di AEM Forms su JEE {#installing-aem-forms-on-jee}

Per installare e configurare AEM Forms su JEE, effettua le seguenti operazioni:

1. Scarica il programma di installazione di AEM 6.5 Forms su JEE dal [sito Web Adobe Licensing (LWS)](https://licensing.adobe.com/). Per scaricare il programma di installazione è necessario un contratto valido di manutenzione e supporto.
1. Leggi il documento [AEM Forms sulle piattaforme supportate da JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) e assicurati che il software, l&#39;hardware, i sistemi operativi, il server applicazioni, i database, i JDK e l&#39;altra infrastruttura siano pronti per installare AEM Forms su JEE.
1. (Solo installazioni non chiavi in mano) Leggi [Preparazione all&#39;installazione di AEM Forms single server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) o [Preparazione all&#39;installazione del cluster di server AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) e prepara l&#39;ambiente per installare e configurare AEM Forms su JEE.
1. A seconda dell&#39;ambiente e del server applicazioni in uso, scegliere uno dei seguenti documenti e seguire le istruzioni per completare l&#39;installazione

   * [Installazione e distribuzione di AEM Forms su JEE utilizzando JBoss turnkey](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Installazione e distribuzione di AEM Forms su JEE per JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Installazione e distribuzione di AEM Forms su JEE per WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Installazione e distribuzione di AEM Forms su JEE per WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configurazione di AEM Forms su JEE nel cluster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configurazione di AEM Forms su JEE nel cluster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configurazione di AEM Forms su JEE nel cluster WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >Nella schermata di selezione del modulo di AEM Forms su JEE configuration manager, seleziona l’opzione Document Security. L’opzione Document Security non richiede la selezione di alcun altro modulo.

## Passaggi successivi {#next-steps}

* [Configurare le opzioni client e server](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Creare e gestire le policy](/help/forms/using/admin-help/creating-policies.md)
* [Creare e gestire set di criteri](/help/forms/using/admin-help/creating-policy-sets.md)
