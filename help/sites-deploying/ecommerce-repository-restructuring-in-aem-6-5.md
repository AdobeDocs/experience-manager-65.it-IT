---
title: Ristrutturazione dell’archivio di e-commerce in AEM 6.5
seo-title: Ristrutturazione dell’archivio di e-commerce in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per E-Commerce.
seo-description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# Ristrutturazione dell’archivio di e-commerce in AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Come descritto nella pagina padre [Ristrutturazione archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che eseguono l&#39;aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche dell&#39;archivio che influiscono sulla soluzione AEM E-Commerce. Alcune modifiche richiedono un lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

## Aggiornamento 6.5 {#with-upgrade}

### Dati relativi a prodotti, ordini, raccolte, classificazioni, metodi di spedizione e metodi di pagamento {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Puoi utilizzare un'attività <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Lazy Migration</a> per migrare i dati di E-Commerce.</p> <p>Esegue i seguenti passaggi:</p>
    <ul>
     <li>regola i riferimenti alla vecchia posizione in modo che punti alla nuova posizione</li>
     <li>sposta il contenuto dalla vecchia posizione alla nuova posizione</li>
     <li>rimuove la vecchia posizione per attivare infine l'utilizzo della nuova posizione nell'intero sistema</li>
    </ul> <p>Le sedi interessate dall'attività sono:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Per i cataloghi più grandi, si consiglia di eseguire l’attività di migrazione Commerce singolarmente passando la seguente proprietà di sistema Java a AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Dopo la migrazione AEM necessario riavviare.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

