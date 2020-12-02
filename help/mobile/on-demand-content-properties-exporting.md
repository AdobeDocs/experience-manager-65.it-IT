---
title: Utilizzo delle proprietà di contenuto per esportare il contenuto
seo-title: Utilizzo delle proprietà di contenuto per esportare il contenuto
description: La pagina seguente mostra Proprietà app e Nodi.
seo-description: La pagina seguente mostra Proprietà app e Nodi.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---


# Utilizzo delle proprietà contenuto per esportare contenuto{#using-content-properties-to-export-content}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le app sono rappresentate come *cq:Pages* in AEM.

Condividono le stesse proprietà comuni presenti in qualsiasi *cq:Page*, oltre ad altre mostrate di seguito che rappresentano le proprietà di supporto dell&#39;integrazione.

## Proprietà app {#app-properties}

La tabella seguente mostra **Proprietà e nodi dell&#39;app**.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso di un Cloud Service Mobile On-Demand configurato. Utilizzato per  azioni AEM Mobile su Mobile On-Demand (chiamata API)</p> <p>Questa associazione è configurata tramite la sezione Gestisci connessione quando un autore sceglie un Cloud Service Mobile On-Demand a cui associare l'app.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso delle configurazioni di esportazione dell'app. La configurazione di esportazione è una cartella con 2 modelli di configurazione di esportazione ContentSync figlio;</p> <p><i>dps-article</i>: Configurazione di esportazione ContentSync per esportare il contenuto dell'articolo</p> <p><i>dps-HTMLResources</i>: Configurazione di esportazione ContentSync per esportare risorse condivise per app/articoli</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Stringa</td>
   <td><p>ID/URI del progetto Mobile On-Demand a cui l'app è collegata/associata.</p> <p>Questa associazione viene configurata tramite la sezione Gestisci connessione quando un autore sceglie il progetto da un elenco di progetti disponibili per il Cloud Service Mobile On-Demand associato.</p> </td>
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
   <td>Data dell'ultimo caricamento di risorse condivise da AEM a  AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>ID dell'utente che ha eseguito l'ultimo caricamento della richiesta di risorse condivise da AEM a  AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-dashboard-config</td>
   <td>Stringa:Percorso</td>
   <td>Percorso della configurazione del dashboard. Il percorso può essere reindirizzato a una configurazione dashbaord personalizzata in base alle esigenze.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso di un componente cq:Component che è o estende <i>mobileapps/core/components/instance.</i></p> <p>Questo fornisce la presenza e il rendering nel Catalogo app.</p> </td>
  </tr>
 </tbody>
</table>

È possibile utilizzare ***Proprietà contenuto*** per creare contenuto. Consultate le seguenti risorse per la creazione ed esportazione di articoli e risorse condivise:

* [Proprietà contenuto](/help/mobile/content-properties.md)
* [Creazione della configurazione di esportazione degli articoli](/help/mobile/creating-article-export-configuration.md)
* [Creazione della configurazione di esportazione delle risorse condivise](/help/mobile/creating-shared-resources-export-configuration.md)
