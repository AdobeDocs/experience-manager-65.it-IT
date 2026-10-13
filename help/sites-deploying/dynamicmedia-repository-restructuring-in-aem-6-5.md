---
title: Ristrutturazione dell’archivio Dynamic Media in Adobe Experience Manager 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in Experience Manager 6.5 per Dynamic Media.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 3%
---
# Ristrutturazione dell’archivio Dynamic Media in Adobe Experience Manager 6.5 {#dynamic-media-repository-restructuring-in-aem}

Come descritto nella pagina [Ristrutturazione dell’archivio padre in Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che eseguono l’aggiornamento ad Experience Manager 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che influiscono su Dynamic Media. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento di Experience Manager 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Prima dell&#39;aggiornamento futuro**

* [Configurazioni di codifica video adattiva personalizzate](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Configurazione cloud Dynamic Media (DMS7)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Configurazione Cloud Service Dynamic Media (DM ibrido)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - Configurazione Cloud Service di YouTube](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Varie](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## Prima dell’aggiornamento futuro {#prior-to-upgrade}

### Configurazioni di codifica video adattivo personalizzate  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Puoi eseguire il seguente script di migrazione per eseguire la migrazione alla nuova posizione:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>In alternativa, puoi modificare la configurazione nell’interfaccia utente di Experience Manager e salvare le modifiche nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazione cloud Dynamic Media (DMS7) {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Il cliente può eseguire uno script di migrazione in questa posizione:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Riavvia il bundle OSGi Dynamic Media.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurazione Cloud Service Dynamic Media (DM ibrido) {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Puoi eseguire lo script di migrazione seguente per allinearlo al modello più recente:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media: configurazione di YouTube Cloud Service  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>1. Annulla la pubblicazione di tutti i video da YouTube<br /> 2. Creare la configurazione di YouTube utilizzando la nuova interfaccia utente touch (da <code>/conf</code>), inclusa la copia di tutti i canali dalla vecchia posizione<br /> 3. Pubblica tutti i video su YouTube.</p> <p>Questo flusso di lavoro genera nuovi URL YouTube. Se non annulli la pubblicazione prima di creare una configurazione YouTube dell’interfaccia utente touch, vengono elencati più URL di YouTube in Proprietà, perché i canali ricreati vengono pubblicati nuovamente, se ne hai la possibilità. Questa funzionalità indica che hai URL inutili elencati in Proprietà.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Varie {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Il cliente può eseguire il seguente script di migrazione.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>In alternativa, puoi modificare la configurazione nell’interfaccia utente di Experience Manager e salvare le modifiche nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Il cliente può eseguire il seguente script di migrazione.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>
