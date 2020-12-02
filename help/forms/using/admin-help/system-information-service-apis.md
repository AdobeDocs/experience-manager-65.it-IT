---
title: API del servizio informazioni di sistema
seo-title: API del servizio informazioni di sistema
description: Questo documento fornisce informazioni dettagliate sulle API fornite dal servizio informazioni sul sistema.
seo-description: Questo documento fornisce informazioni dettagliate sulle API fornite dal servizio informazioni sul sistema.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---


# API del servizio informazioni di sistema {#system-information-service-apis}

Il servizio informazioni di sistema fornisce un set di REST APIs per recuperare informazioni. La tabella seguente fornisce informazioni dettagliate sulle API:

<table>
 <thead>
  <tr>
   <th><p>Nome</p></th>
   <th><p>URL</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/SystemInfo.properties`</p></td>
   <td><p>Questa API è un wrapper per l'API Java <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a>. Recupera la configurazione dell'ambiente di lavoro corrente. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Recupera tutte le variabili di ambiente del sistema operativo host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Scarica un file zip contenente i registri del server applicazione. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Recupera tutto il contenuto del file config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Recupera i parametri di stato e di configurazione dei servizi AEM moduli.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.criticalDetails</p></td>
   <td><p>Recupera i tempi di attività del server, gli argomenti JVM, la memoria di sistema, la dimensione heap, il nome del sistema operativo, il numero di thread attivi e il numero di thread. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Recupera i valori delle seguenti proprietà:</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDispositionTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Recupera informazioni dettagliate sul database.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Recupera le informazioni sulla versione e sulla licenza dei componenti AEM moduli installati. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Scarica i file di configurazione del server dell'applicazione host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.thread?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.thread?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Recupera il conteggio e la traccia dello stack dei thread attivi. Accetta i seguenti parametri:</p>
    <ul>
     <li><p>iterations= [n]: Specifica il numero di iterazioni. Sostituire n con un numero. </p></li>
     <li><p>Ritardo= [n]: Specifica il numero di millisecondi di attesa prima dell'avvio dell'iterazione successiva. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Questa API è un wrapper per tutte le API del servizio informazioni di sistema. Internamente, esegue tutte le API di informazioni di sistema e scarica le informazioni in formato zip. </p><p><i><strong>nota</strong>: Il SystemInfo.info non fornisce traccia di conteggio e stack dei thread attivi. </i></p></td>
  </tr>
 </tbody>
</table>

