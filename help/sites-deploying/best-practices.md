---
title: Implementazione delle best practice
description: Scopri come distribuire e gestire Adobe Experience Manager (AEM) nel modo più efficiente ed efficace possibile.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 10%

---

# Implementazione delle best practice{#deploying-best-practices}

Le best practice per l’implementazione descrivono come implementare o mantenere Adobe Experience Manager (AEM) nel modo più efficiente ed efficace possibile. Questo elenco crescente di argomenti comprende varie aree dell&#39;AEM.

Nelle seguenti aree è disponibile la documentazione relativa all’implementazione e alla manutenzione delle best practice e delle raccomandazioni:

* [Oak](#oak)
* [Communities](#communities)
* [Interfaccia](#ui)
* [Prestazioni](#performance)

Per le best practice sull’amministrazione, lo sviluppo o l’authoring, consulta una delle seguenti sezioni:

* [Amministrazione delle best practice](/help/sites-administering/administer-best-practices.md)
* [Sviluppo di best practice](/help/sites-developing/best-practices.md)
* [Best practice di authoring](/help/sites-authoring/best-practices.md)

I documenti specifici sono descritti e collegati nelle tabelle seguenti.

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md) è un archivio di contenuti gerarchici scalabile ed efficiente, alla base dell’AEM.

<table>
 <tbody>
  <tr>
   <td><p>Scalabilità, prestazioni e disaster recovery</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Prestazioni e scalabilità</a></td>
   <td>Un white paper che illustra l'agilità tecnica, le prestazioni elevate e le funzionalità di disaster recovery</td>
  </tr>
  <tr>
   <td>Distribuzioni Oak consigliate</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Distribuzioni consigliate</a></td>
   <td>Descrive gli scenari di distribuzione</td>
  </tr>
  <tr>
   <td>Topologia di Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Best practice per la topologia Mongo</a></td>
   <td>Descrive la topologia mongo - quando utilizzare quale topologia.</td>
  </tr>
  <tr>
   <td>Opzioni archivio dati</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configurazione di nodi e archivi dati</a></td>
   <td>In questo documento vengono illustrate le best practice per l’archiviazione di dati binari e nodi di contenuto. Include informazioni sull’utilizzo dell’archivio dati Amazon S3.</td>
  </tr>
  <tr>
   <td>Cerca in Oak</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Best practice per query e indicizzazione</a><br /> </td>
   <td>Vengono descritte le procedure consigliate per l'indicizzazione del contenuto.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities semplifica la creazione e la gestione delle community on-premise. Le best practice per AEM Communities sono descritte qui:

[Archivio contenuti community](/help/communities/working-with-srp.md) - Descrive la nuova funzione di archiviazione condivisa per i contenuti generati dagli utenti (UGC, User-Generated Content) e le considerazioni per la scelta del sottostante [topologia](/help/communities/topologies.md).

[Distribuzioni consigliate per community](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Descrive le distribuzioni consigliate per le community. |

## Interfaccia {#ui}

Le best practice relative all’interfaccia utente sono descritte qui:

[Interfaccia utente di Recommendations per i clienti](/help/sites-deploying/ui-recommendations.md)

L’AEM dispone attualmente di due interfacce: classica e ottimizzata per il tocco nella stessa versione. Pertanto, i clienti devono prendere una decisione su quale utilizzare durante l’implementazione del progetto. Questo documento ha lo scopo di aiutare a trovare la scelta giusta.

## Prestazioni {#performance}

Le best practice sulle prestazioni sono elencate qui:

<table>
 <tbody>
  <tr>
   <td>Best practice per la garanzia della qualità</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Best practice per la garanzia della qualità</a></td>
   <td>Panoramica standardizzata dei problemi relativi alla definizione di un concetto di test specifico per i test delle prestazioni su <em>pubblicare</em> ambiente. Questo è di interesse soprattutto per gli ingegneri QA, i project manager e gli amministratori di sistema.</td>
  </tr>
  <tr>
   <td>Utilizzo di Dispatcher con una rete CDN</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it#using-dispatcher-with-a-cdn">Utilizzo di Dispatcher con una rete CDN</a></td>
   <td>Una rete CDN (Content Delivery Network), come Akamai Edge Delivery o Amazon Cloud Front, consente di distribuire contenuto da una località vicina all’utente finale.</td>
  </tr>
  <tr>
   <td>Ottimizzazione delle prestazioni</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Ottimizzazione delle prestazioni</a></td>
   <td>Un problema chiave è il tempo impiegato dal sito web per rispondere alle richieste dei visitatori.</td>
  </tr>
  <tr>
   <td>Test delle prestazioni</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Best practice per i test delle prestazioni</a></td>
   <td>Descrive le best practice per l’esecuzione di test delle prestazioni in una distribuzione AEM.<br /> </td>
  </tr>
 </tbody>
</table>
