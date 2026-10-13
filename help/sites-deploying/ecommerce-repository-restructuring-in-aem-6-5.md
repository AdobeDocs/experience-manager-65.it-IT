---
title: Ristrutturazione dell’archivio e-commerce in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per E-Commerce.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
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
source-wordcount: '215'
ht-degree: 8%
---
# Ristrutturazione dell’archivio e-commerce in AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Come descritto nella pagina [Ristrutturazione dell&#39;archivio padre in AEM 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che eseguono l&#39;aggiornamento ad AEM 6.5 devono utilizzare questa pagina per valutare l&#39;impegno di lavoro associato alle modifiche dell&#39;archivio che influiscono sulla soluzione AEM E-Commerce. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

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
   <td><p>È possibile utilizzare un'attività <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Lazy Migration</a> per eseguire la migrazione dei dati di E-Commerce.</p> <p>Esegue i seguenti passaggi:</p>
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
    </ul> <p>Per i cataloghi di grandi dimensioni, Adobe consiglia di eseguire l’attività di migrazione e-commerce singolarmente, passando la seguente proprietà di sistema Java™ ad AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Dopo la migrazione, riavvia AEM.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
