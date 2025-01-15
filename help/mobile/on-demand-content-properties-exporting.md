---
title: Utilizzo delle proprietà del contenuto per esportare il contenuto
description: La pagina seguente mostra le proprietà e i nodi dell’app.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 3%

---

# Utilizzo delle proprietà del contenuto per esportare il contenuto{#using-content-properties-to-export-content}

{{ue-over-mobile}}

Le app sono rappresentate come *cq:Pages* in AEM.

Condividono le stesse proprietà comuni presenti in qualsiasi *cq:Page*, oltre ad altre mostrate di seguito che rappresentano le proprietà di supporto dell&#39;integrazione.

## Proprietà app {#app-properties}

La tabella seguente mostra **Proprietà app e nodi**.

<table>
 <tbody>
  <tr>
   <td><strong>NomeProprietà</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso di un Cloud Service Mobile On-Demand configurato. Utilizzato per azioni da AEM Mobile a Mobile On-Demand (chiamata API)</p> <p>Questa associazione viene configurata tramite il riquadro Gestisci connessione quando un autore sceglie un Cloud Service Mobile On-Demand a cui associare l’app.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso delle configurazioni di esportazione dell’app. La configurazione di esportazione è una cartella con 2 modelli di configurazione di esportazione secondari ContentSync;</p> <p><i>dps-article</i>: configurazione di esportazione ContentSync per esportare il contenuto dell'articolo</p> <p><i>dps-HTMLResources</i>: configurazione di esportazione di ContentSync per esportare le risorse condivise dell'app/articolo</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Stringa</td>
   <td><p>ID/URI del progetto Mobile On-Demand a cui questa app è collegata/associata.</p> <p>Questa associazione viene configurata tramite il riquadro Gestisci connessione quando un autore sceglie il progetto da un elenco di progetti disponibili per il Cloud Service Mobile On-Demand associato.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>Stringa</td>
   <td>Titolo app.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>Stringa</td>
   <td>Tipo di contenuto.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>Data</td>
   <td>Data dell’ultimo caricamento di risorse condivise dall’AEM ad AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>Stringa:userid</td>
   <td>ID dell’utente che ha eseguito l’ultimo caricamento della richiesta di risorse condivise dall’AEM ad AEM Mobile.</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>Stringa:Percorso</td>
   <td>Percorso di una configurazione del dashboard. Se necessario, il percorso può essere reindirizzato a una configurazione personalizzata del dashboard.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso di un componente cq:Component che è o estende <i>mobileapps/core/components/instance.</i></p> <p>Questo fornisce la presenza e il rendering nel catalogo delle app.</p> </td>
  </tr>
 </tbody>
</table>

È possibile utilizzare ***Proprietà contenuto*** per creare contenuto. Consulta le risorse seguenti per creare ed esportare articoli e risorse condivise:

* [Proprietà contenuto](/help/mobile/content-properties.md)
* [Creazione della configurazione di esportazione dell&#39;articolo](/help/mobile/creating-article-export-configuration.md)
* [Creazione configurazione esportazione risorse condivise](/help/mobile/creating-shared-resources-export-configuration.md)
