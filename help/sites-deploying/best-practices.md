---
title: Best practice di distribuzione
seo-title: Best practice di distribuzione
description: Implementazione e manutenzione delle best practice.
seo-description: Implementazione e manutenzione delle best practice.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 15%

---


# Implementazione delle best practice{#deploying-best-practices}

Le best practice di distribuzione descrivono come implementare o mantenere AEM nel modo più efficiente ed efficace possibile. Questo elenco di argomenti è in continuo aggiornamento e copre varie aree di AEM.

Nelle aree seguenti è disponibile la documentazione relativa all&#39;implementazione e alla manutenzione delle procedure ottimali e delle raccomandazioni:

* [OAK](#oak)
* [Community](#communities)
* [Interfaccia](#ui)
* [Spettacolo](#performance)

Per le best practice relative all’amministrazione, allo sviluppo o all’authoring, consulta uno dei seguenti argomenti:

* [Best practice di amministrazione](/help/sites-administering/administer-best-practices.md)
* [Best practice di sviluppo](/help/sites-developing/best-practices.md)
* [Best practice di authoring](/help/sites-authoring/best-practices.md)

Nelle tabelle che seguono è riportata una descrizione di ciascun documento con il collegamento relativo.

## OAK {#oak}

[](/help/sites-deploying/platform.md) Oakis, un archivio di contenuti gerarchici scalabile e performante che è alla base di AEM.

<table>
 <tbody>
  <tr>
   <td><p>Scalabilità, prestazioni e disaster recovery</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Prestazioni e scalabilità</a></td>
   <td>Fornisce un white paper sulle funzioni di agilità tecnica, alte prestazioni e ripristino di emergenza audio</td>
  </tr>
  <tr>
   <td>Implementazioni OAK consigliate</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implementazioni consigliate</a></td>
   <td>Descrive gli scenari di distribuzione</td>
  </tr>
  <tr>
   <td>Topologia mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Best practice per la topologia mongo</a></td>
   <td>Descrive la topologia mongo - quando utilizzare quale topologia.</td>
  </tr>
  <tr>
   <td>Opzioni DataStore</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configurazione di nodi e archivi dati</a></td>
   <td>Questo documento descrive le procedure ottimali per la memorizzazione di dati binari e nodi di contenuto. Include informazioni sull'utilizzo  archivio dati Amazon S3.</td>
  </tr>
  <tr>
   <td>Cerca in OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Best practice per query e indicizzazione</a><br /> </td>
   <td>Illustra le procedure ottimali per l'indicizzazione del contenuto.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

 AEM Communities semplifica la creazione e la gestione di community locali. Le best practice per  AEM Communities sono descritte di seguito:

[Archivio](/help/communities/working-with-srp.md)  di contenuti community: descrive la nuova funzione di memorizzazione condivisa per i contenuti generati dall&#39;utente (UGC) e le considerazioni per la scelta della  [topologia](/help/communities/topologies.md) sottostante.

[Implementazioni consigliate per le community](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities)  - Descrive le distribuzioni consigliate per community. |

## Interfaccia {#ui}

Le best practice relative all&#39;interfaccia utente sono descritte qui:

[Interfaccia utente Recommendations per clienti](/help/sites-deploying/ui-recommendations.md)

AEM dispone attualmente di due interfacce: Interfaccia classica e touch nella stessa versione. Pertanto, i clienti devono prendere una decisione su quale utilizzo utilizzare durante l&#39;implementazione del progetto. Questo documento è inteso a facilitare la scelta giusta.

## Spettacolo {#performance}

Le best practice relative alle prestazioni sono elencate di seguito:

<table>
 <tbody>
  <tr>
   <td>Best practice per la garanzia della qualità</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Best practice per la garanzia della qualità</a></td>
   <td>Panoramica standardizzata dei problemi relativi alla definizione di un concetto di test specifico per i test di prestazioni nell'ambiente <em>publish</em>. Ciò è particolarmente interessante per ingegneri di QA, project manager e amministratori di sistema.</td>
  </tr>
  <tr>
   <td>Utilizzo di Dispatcher con una rete CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilizzo di Dispatcher con una rete CDN</a></td>
   <td>Una rete CDN (Content Delivery Network), come Akamai Edge Delivery o Amazon Cloud Front, consente di distribuire contenuto da una posizione vicina all’utente finale.</td>
  </tr>
  <tr>
   <td>Ottimizzazione delle prestazioni</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Ottimizzazione delle prestazioni</a></td>
   <td>Un problema chiave è rappresentato dal tempo impiegato dal sito Web per rispondere alle richieste dei visitatori.</td>
  </tr>
  <tr>
   <td>Test delle prestazioni</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Best practice per il test delle prestazioni</a></td>
   <td>Illustra le procedure ottimali per l'esecuzione di test delle prestazioni in una distribuzione AEM.<br /> </td>
  </tr>
 </tbody>
</table>

