---
title: Ristrutturazione dell’archivio Dynamic Medie in Adobe Experience Manager 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio nell’Experience Manager 6.5 per Dynamic Medie.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Ristrutturazione dell’archivio Dynamic Medie in Adobe Experience Manager 6.5 {#dynamic-media-repository-restructuring-in-aem}

Come descritto sull’elemento padre [Ristrutturazione dell’archivio in Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md) , i clienti che eseguono l’aggiornamento all’Experience Manager 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che interessano Dynamic Medie. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento di Experience Manager 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Prima dell’aggiornamento futuro**

* [Configurazioni di codifica video adattiva personalizzate](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Configurazione cloud Dynamic Medie (DMS7)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Configurazione Cloud Service Dynamic Medie (DM ibrido)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Medie - Configurazione Cloud Service YouTube](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
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

### Configurazione cloud Dynamic Medie (DMS7) {#dynamic-media-dms-cloud-configuration}

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
   <td><p>Il cliente può eseguire uno script di migrazione nella posizione seguente:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Riavvia il bundle OSGi di Dynamic Medie.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurazione Cloud Service Dynamic Medie (DM ibrido) {#cloudserviceconfiguration}

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

### Dynamic Medie - Configurazione del Cloud Service YouTube  {#youtubecloudserviceconfiguration}

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
   <td><p>1. Annullare la pubblicazione di tutti i video da YouTube<br /> 2. Creare la configurazione di YouTube utilizzando la nuova interfaccia utente touch (da <code>/conf</code>) inclusa la copia di tutti i canali dalla vecchia posizione<br /> 3. Pubblica tutti i video su YouTube.</p> <p>Questo flusso di lavoro genera nuovi URL YouTube. Se non annulli la pubblicazione prima di creare una configurazione YouTube dell’interfaccia utente touch, vengono elencati più URL di YouTube in Proprietà, perché i canali ricreati vengono pubblicati nuovamente, se ne hai la possibilità. Questa funzionalità indica che hai URL inutili elencati in Proprietà.</p> </td>
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
