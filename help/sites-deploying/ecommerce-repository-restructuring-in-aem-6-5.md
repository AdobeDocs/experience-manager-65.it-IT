---
title: Ristrutturazione del repository di e-commerce in AEM 6.5
seo-title: Ristrutturazione del repository di e-commerce in AEM 6.5
description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per E-Commerce.
seo-description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---


# Ristrutturazione del repository di e-commerce in AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Come descritto nella pagina [Ristrutturazione repository principale di AEM 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che effettuano l&#39;aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche del repository che influiscono sulla soluzione AEM E-Commerce. Alcune modifiche richiedono sforzi di lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere posticipate fino a un aggiornamento futuro.

## Con aggiornamento 6.5 {#with-upgrade}

### Dati prodotti, ordine, raccolte, classificazioni, metodi di spedizione e metodi di pagamento {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

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
   <td><p>Puoi utilizzare un'attività <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migrazione pigra</a> per migrare i dati di E-Commerce.</p> <p>Effettua le seguenti operazioni:</p>
    <ul>
     <li>regola i riferimenti alla vecchia posizione in modo che punti alla nuova posizione</li>
     <li>sposta il contenuto dalla posizione precedente alla nuova posizione</li>
     <li>rimuove la vecchia posizione per attivare infine l'utilizzo della nuova posizione nell'intero sistema</li>
    </ul> <p>Le posizioni interessate dall'attività sono:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/Orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Per i cataloghi più grandi, si consiglia di eseguire l'attività di migrazione commerciale singolarmente passando la seguente proprietà di sistema Java a AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Dopo la migrazione AEM necessario riavviare.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

