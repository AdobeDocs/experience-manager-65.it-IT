---
title: eCommerce
description: AEM eCommerce aiuta gli esperti di marketing a fornire esperienze di acquisto personalizzate su diversi punti di contatto web, mobili e social.
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# eCommerce{#ecommerce}

* [Concetti ](/help/commerce/cif-classic/administering/concepts.md)
* [Amministrazione (generico)](/help/commerce/cif-classic/administering/generic.md)

In Adobe sono disponibili due versioni di Commerce Integration Framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF on-prem</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>Versioni di AEM supportate</p> </td>
   <td><p>AEM on-premise o AMS 6.x</p> </td>
   <td>AEM AMS 6.4 e 6.5</td>
  </tr>
  <tr>
   <td><p>Back-end</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>Integrazione monolitica, mappatura pre-compilazione (modello)</li>
     <li>Archivio JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java e Java</li>
     <li>Nessun dato di e-commerce memorizzato nell'archivio JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>AEM pagine di rendering lato server</p> </td>
   <td>Applicazione a pagina mista (rendering ibrido)</td>
  </tr>
  <tr>
   <td><p>Catalogo dei prodotti</p> </td>
   <td>
    <ul>
     <li>Importazione prodotti, editor, memorizzazione in cache in AEM</li>
     <li>Cataloghi regolari con pagine AEM o proxy</li>
    </ul> </td>
   <td>
    <ul>
     <li>Nessuna importazione di prodotti</li>
     <li>Modelli generici</li>
     <li>Dati on-demand tramite connettore</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Scalabilità</p> </td>
   <td>
    <ul>
     <li>Può supportare fino a pochi milioni di prodotti (dipende dal caso d’uso)</li>
     <li>Memorizzazione in cache su Dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Nessuna limitazione del volume</li>
     <li>Memorizzazione in cache su Dispatcher o CDN</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modello dati standardizzato</td>
   <td>No</td>
   <td>Sì, schema GraphQL di Adobe Commerce</td>
  </tr>
  <tr>
   <td>Disponibilità</td>
   <td><p>Sì. Commerce Cloud SAP (estensione aggiornata per supportare AEM 6.4 e Hybris 5 (impostazione predefinita) e mantenere la compatibilità con Hybris 4</p> <p>Commerce Cloud Salesforce (connettore open source per supportare AEM 6.4)</p> </td>
   <td>Sì tramite open source tramite GitHub. Adobe Commerce (Supporta 2.3.2 (predefinito) e compatibile con 2.3.1).</td>
  </tr>
  <tr>
   <td>Quando utilizzare</td>
   <td>Casi d’uso limitati: Ad esempio, in situazioni in cui può essere necessario importare cataloghi piccoli e statici</td>
   <td>Soluzione preferita nella maggior parte dei casi d'uso</td>
  </tr>
 </tbody>
</table>

eCommerce, insieme a Product Information Management (PIM), gestisce le attività di un sito web incentrato sulla vendita di prodotti tramite un negozio online:

* Creazione, durata e obsolescenza di un prodotto
* Gestione dei prezzi
* Gestione delle transazioni
* Gestione di interi cataloghi
* Record di storage live e centralizzati
* Interfacce web

AEM eCommerce aiuta gli esperti di marketing a fornire esperienze di acquisto personalizzate su diversi punti di contatto web, mobili e social. L’ambiente di authoring AEM ti consente di personalizzare pagine e componenti in base al contesto del visitatore e alle strategie di merchandising di destinazione; ad esempio:

* Pagine prodotto
* Componenti del carrello
* Componenti di estrazione

L’implementazione consente l’accesso in tempo reale alle informazioni di prodotto. Può essere utilizzato per applicare:

* Integrità delle informazioni sul prodotto
* Prezzi
* Inventario delle scorte
* Variazioni nello stato di un carrello

>[!NOTE]
>
>Per utilizzare il framework di integrazione con provider di eCommerce esterni, devi prima installare i pacchetti richiesti. Per ulteriori informazioni, consulta [Distribuzione di eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Per informazioni sull’estensione delle funzionalità di eCommerce, consulta [Sviluppo di eCommerce](/help/commerce/cif-classic/developing/ecommerce.md).

## Caratteristiche principali {#main-features}

AEM eCommerce fornisce:

* Un certo numero di **componenti AEM predefiniti** per illustrare i risultati ottenibili per il progetto:

   * Display del prodotto
   * Carrello
   * Check-out
   * Prodotti visualizzati di recente
   * Voucher
   * e altri

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >Il framework di integrazione fornito da AEM consente inoltre di creare componenti AEM aggiuntivi per le funzionalità commerce, indipendentemente dal motore di eCommerce specifico.

* **Ricerca** - utilizzando:

   * ricerca AEM
   * ricerca del sistema eCommerce
   * una ricerca di terze parti (ad esempio, Search&amp;Promote)
   * o una loro combinazione.

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* Utilizza la capacità AEM di **presentare i contenuti su più canali**, sia la finestra del browser completa che il dispositivo mobile. In questo modo i contenuti vengono consegnati nel formato richiesto dai visitatori.

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* La capacità di **Sviluppa la tua implementazione di integrazione basata su [Framework eCommerce AEM](#the-framework)**.

   Le due implementazioni attualmente disponibili sono entrambe basate sullo stesso criterio, oltre all’API generale (il framework). L’implementazione di una nuova integrazione comporta solo l’implementazione delle funzioni necessarie per l’integrazione. I componenti front-end possono essere utilizzati da qualsiasi nuova implementazione durante l’utilizzo delle interfacce (in modo che siano indipendenti dall’implementazione).

* La possibilità di sviluppare **e-commerce basato su esperienze basate su dati e attività dell’acquirente**. Questo consente di realizzare molti scenari:

   * Un esempio potrebbe essere la riduzione dei costi di spedizione quando l&#39;ordine totale supera un importo specifico.
   * Un altro potrebbe consentire di fornire offerte stagionali che utilizzano i dati del profilo (ad esempio la posizione). Questi possono quindi essere evidenziati, sempre a seconda di altri fattori quando necessario.

   Nell’esempio seguente viene mostrato un teaser con un contenuto inferiore a $75:

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   Questo può essere modificato quando il contenuto del carrello supera i $75:

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* E altre caratteristiche, tra cui:

   * Contenuto del carrello conservato nelle sessioni
   * Storico ordini completo
   * Aggiornamento del catalogo Express

## Quadro {#the-framework}

La [Concetti](/help/commerce/cif-classic/administering/concepts.md) la sezione descrive il framework in modo più dettagliato, ma quanto segue fornisce una vista ad alto livello del framework:

### Cosa? {#what}

* Il framework di integrazione fornisce l’API , una serie di componenti per illustrare funzionalità e diverse estensioni per fornire esempi di metodi di connessione.
* Il quadro fornisce la struttura di base necessaria per l’implementazione di un progetto.
* Il framework è estensibile.
* Il framework non fornisce un sito pronto all’uso pronto all’uso. Una certa quantità di lavoro di sviluppo è sempre necessaria per adattare il framework alle tue specifiche.

### Perché? {#why}

* Fornire i meccanismi di base necessari per realizzare rapidamente un sito eCommerce personalizzato.
* Tp offre la flessibilità necessaria per lo sviluppo di un sito e-commerce reale.
* Illustra le best practice.
