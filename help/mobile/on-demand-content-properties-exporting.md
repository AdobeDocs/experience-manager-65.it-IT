---
title: Utilizzo delle proprietà di contenuto per esportare il contenuto
seo-title: Using Content Properties to Export Content
description: La pagina seguente mostra Proprietà app e nodi.
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# Utilizzo delle proprietà di contenuto per esportare il contenuto{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le app sono rappresentate come *cq:Pages* in AEM.

Condividono le stesse proprietà comuni presenti in qualsiasi *cq:Page* oltre ad altri mostrati di seguito che rappresentano le proprietà di supporto dell&#39;integrazione.

## Proprietà app {#app-properties}

La tabella seguente mostra **Proprietà e nodi dell’app**.

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
   <td><p>Percorso a un Cloud Service Mobile On-Demand configurato. Utilizzato per AEM Mobile per azioni on-demand mobili (chiamata API)</p> <p>Questa associazione viene configurata tramite la sezione Gestione connessione quando un autore sceglie un Cloud Service Mobile On-Demand a cui associare l’app.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso delle configurazioni di esportazione dell’app. La configurazione di esportazione è una cartella con 2 modelli di configurazione di esportazione ContentSync figlio;</p> <p><i>articolo del dps</i>: Configurazione dell’esportazione ContentSync per esportare il contenuto dell’articolo</p> <p><i>dps-HTMLResource</i>: Configurazione dell'esportazione ContentSync per esportare le risorse condivise dell'app/articolo</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Stringa</td>
   <td><p>Id/URI del progetto Mobile On-Demand a cui è collegata/associata l’app.</p> <p>Questa associazione viene configurata tramite la sezione Gestisci connessione quando un autore sceglie il progetto da un elenco di progetti disponibili per il Cloud Service Mobile On-Demand associato.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>Stringa</td>
   <td>Titolo dell'app.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>Stringa</td>
   <td>Tipo di contenuto.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResource-lastUploaded</td>
   <td>Data</td>
   <td>Data dell’ultimo caricamento di risorse condivise da AEM ad AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResource-lastUploadedBy</td>
   <td>Stringa:userid</td>
   <td>ID dell'utente che ha eseguito l'ultimo caricamento della richiesta di risorse condivise da AEM ad AEM Mobile.</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>Stringa:Percorso</td>
   <td>Percorso della configurazione del dashboard. Il percorso può essere reindirizzato a una configurazione di dashboard personalizzata in base alle esigenze.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Stringa:Percorso</td>
   <td><p>Percorso di un cq:Component che è o si estende <i>mobileapps/core/components/instance.</i></p> <p>Questo fornisce la presenza e il rendering nel Catalogo app.</p> </td>
  </tr>
 </tbody>
</table>

È possibile utilizzare ***Proprietà contenuto*** per creare contenuti. Consulta le seguenti risorse per creare ed esportare articoli e risorse condivise:

* [Proprietà contenuto](/help/mobile/content-properties.md)
* [Creazione della configurazione di esportazione degli articoli](/help/mobile/creating-article-export-configuration.md)
* [Creazione della configurazione di esportazione delle risorse condivise](/help/mobile/creating-shared-resources-export-configuration.md)
