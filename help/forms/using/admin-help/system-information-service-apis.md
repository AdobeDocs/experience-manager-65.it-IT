---
title: API di System Information Service
description: Questo documento fornisce informazioni dettagliate sulle API fornite dal servizio informazioni di sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# API di System Information Service {#system-information-service-apis}

Il servizio informazioni di sistema fornisce un set di API REST per recuperare informazioni. La tabella seguente fornisce informazioni dettagliate sulle API:

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
   <td><p>https://'[server]:[porta]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>Questa API è un wrapper per <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> API Java. Recupera la configurazione dell’ambiente di lavoro corrente. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Recupera tutte le variabili di ambiente del sistema operativo host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Scarica un file zip contenente i registri del server applicazioni. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Recupera tutto il contenuto del file config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Recupera lo stato e i parametri di configurazione dei servizi moduli AEM.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.italDetails</p></td>
   <td><p>Recupera il tempo di attività del server, gli argomenti JVM, la memoria di sistema, la dimensione heap, il nome del sistema operativo, il numero di thread attivi e il numero di thread. </p></td>
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
     <li><p>DefaultDocumentDisposingTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>FileConfigurazioneServiziDati </p></li>
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
   <td><p>Recupera le informazioni sulla versione e sulla licenza dei componenti AEM forms installati. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Scarica i file di configurazione del server applicazioni host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Recupera il conteggio e la traccia dello stack dei thread attivi. Accetta i seguenti parametri:</p>
    <ul>
     <li><p>iterations= [n]: specifica il numero di iterazioni. Sostituire n con un numero. </p></li>
     <li><p>Delay= [n]: specifica il numero di millisecondi di attesa prima di avviare l'iterazione successiva. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[porta]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Questa API è un wrapper per tutte le API del servizio informazioni di sistema. Internamente, esegue tutte le API di informazioni di sistema e scarica le informazioni in formato zip. </p><p><i><strong>nota</strong>: SystemInfo.info non fornisce il conteggio e la traccia dello stack dei thread attivi. </i></p></td>
  </tr>
 </tbody>
</table>
