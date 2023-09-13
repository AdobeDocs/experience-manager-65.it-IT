---
title: Ristrutturazione dell’archivio di e-commerce in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per l’e-commerce.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---

# Ristrutturazione dell’archivio di e-commerce in AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Come descritto sull’elemento padre [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) pagina, i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione di e-commerce AEM. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

## Con aggiornamento 6.5 {#with-upgrade}

### Dati su prodotti, ordini, raccolte, classificazioni, metodi di spedizione e metodi di pagamento {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È possibile utilizzare una <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migrazione lenta</a> attività per migrare i dati di E-Commerce.</p> <p>Esegue i seguenti passaggi:</p>
    <ul>
     <li>regola i riferimenti alla posizione precedente per puntare alla nuova posizione</li>
     <li>sposta il contenuto dalla posizione precedente alla nuova posizione</li>
     <li>rimuove la posizione precedente per attivare l'utilizzo della nuova posizione nell'intero sistema</li>
    </ul> <p>Le località coperte dall'attività sono:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Per cataloghi di grandi dimensioni, l’Adobe consiglia di eseguire l’attività di migrazione e-commerce singolarmente, passando la seguente proprietà di sistema Java™ all’AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Dopo la migrazione, riavviare AEM.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
