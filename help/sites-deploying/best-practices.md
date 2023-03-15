---
title: Best practice di distribuzione
seo-title: Deploying Best Practices
description: Implementazione e manutenzione delle best practice.
seo-description: Deploying and maintaining best practices.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 16%

---

# Best practice di distribuzione{#deploying-best-practices}

Le best practice di distribuzione descrivono come implementare o mantenere AEM nel modo più efficiente ed efficace possibile. Questo elenco di argomenti è in continuo aggiornamento e copre varie aree di AEM.

Nelle seguenti aree è disponibile la documentazione relativa all’implementazione e alla manutenzione delle best practice e dei consigli:

* [OAK](#oak)
* [Communities](#communities)
* [Interfaccia](#ui)
* [Spettacolo](#performance)

Per le best practice relative all’amministrazione, allo sviluppo o all’authoring, consulta uno dei seguenti argomenti:

* [Best practice di amministrazione](/help/sites-administering/administer-best-practices.md)
* [Best practice di sviluppo](/help/sites-developing/best-practices.md)
* [Best practice di authoring](/help/sites-authoring/best-practices.md)

Nelle tabelle che seguono è riportata una descrizione di ciascun documento con il collegamento relativo.

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) è un archivio di contenuti gerarchici scalabile ed efficiente alla base di AEM.

<table>
 <tbody>
  <tr>
   <td><p>Scalabilità, prestazioni e disaster recovery</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Prestazioni e scalabilità</a></td>
   <td>Fornisce un white paper sulle caratteristiche di agilità tecnica, prestazioni elevate e ripristino di emergenza audio</td>
  </tr>
  <tr>
   <td>Implementazioni OAK consigliate</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implementazioni consigliate</a></td>
   <td>Descrive gli scenari di distribuzione</td>
  </tr>
  <tr>
   <td>Topologia mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Best practice per la topologia dei Mongo</a></td>
   <td>Descrive la topologia mongo - quando utilizzare quale topologia.</td>
  </tr>
  <tr>
   <td>Opzioni del datastore</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configurazione di nodi e archivi dati</a></td>
   <td>In questo documento vengono illustrate le best practice relative all’archiviazione dei dati binari e dei nodi di contenuto. Include informazioni sull'utilizzo dell'archivio dati Amazon S3.</td>
  </tr>
  <tr>
   <td>Cerca in OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Tecniche consigliate per query e indicizzazione</a><br /> </td>
   <td>Descrive le best practice per indicizzare il contenuto.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities semplifica la creazione e la gestione di community on-premise. Le best practice per AEM Communities sono descritte qui:

[Archivio dei contenuti della community](/help/communities/working-with-srp.md) - Illustra la nuova funzione di archiviazione condivisa per i contenuti generati dall&#39;utente (UGC) e le considerazioni per la scelta del sottostante [topologia](/help/communities/topologies.md).

[Implementazioni consigliate per le community](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Descrive le distribuzioni consigliate per Communities. |

## Interfaccia {#ui}

Le best practice relative all’interfaccia utente sono descritte qui:

[Interfaccia utente Recommendations per clienti](/help/sites-deploying/ui-recommendations.md)

AEM dispone attualmente di due interfacce: Interfaccia classica e touch nella stessa versione. Pertanto, i clienti devono decidere quale utilizzare durante l’implementazione del progetto. Questo documento ha lo scopo di aiutare a trovare la scelta giusta.

## Spettacolo {#performance}

Le best practice relative alle prestazioni sono elencate qui:

<table>
 <tbody>
  <tr>
   <td>Best practice per la garanzia della qualità</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Best practice per la garanzia della qualità</a></td>
   <td>Panoramica standardizzata dei problemi relativi alla definizione di un concetto di test specifico per i test delle prestazioni <em>pubblicare</em> ambiente. Questo è di particolare interesse per ingegneri QA, project manager e amministratori di sistema.</td>
  </tr>
  <tr>
   <td>Utilizzo di Dispatcher con una rete CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilizzo di Dispatcher con una rete CDN</a></td>
   <td>Una rete CDN (Content Delivery Network), come Akamai Edge Delivery o Amazon Cloud Front, consente di distribuire contenuto da una località vicina all’utente finale.</td>
  </tr>
  <tr>
   <td>Ottimizzazione delle prestazioni</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Ottimizzazione delle prestazioni</a></td>
   <td>Un problema chiave è il tempo impiegato dal sito web per rispondere alle richieste dei visitatori.</td>
  </tr>
  <tr>
   <td>Test delle prestazioni</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Tecniche consigliate per il test delle prestazioni</a></td>
   <td>Descrive le best practice per eseguire test delle prestazioni in una distribuzione AEM.<br /> </td>
  </tr>
 </tbody>
</table>
