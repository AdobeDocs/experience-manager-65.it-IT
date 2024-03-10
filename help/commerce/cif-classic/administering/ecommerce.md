---
title: Framework di integrazione eCommerce
description: L’eCommerce dell’AEM aiuta gli esperti di marketing a fornire esperienze di acquisto personalizzate e di marchio attraverso punti di contatto web, mobili e sociali.
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---

# eCommerce{#ecommerce}

* [Concetti](/help/commerce/cif-classic/administering/concepts.md)
* [Amministrazione (generica)](/help/commerce/cif-classic/administering/generic.md)

L&#39;Adobe fornisce due versioni della Commerce integration framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF on-premise</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>Versioni di AEM supportate</p> </td>
   <td><p>AEM on-prem o AMS 6.x</p> </td>
   <td>AEM AMS 6.4 e 6.5</td>
  </tr>
  <tr>
   <td><p>Back-end</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>Integrazione monolitica, mappatura pre-build (modello)</li>
     <li>Archivio JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java e JavaScript</li>
     <li>Nessun dato commerce archiviato nell’archivio JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>Pagine sottoposte a rendering lato server dell’AEM</p> </td>
   <td>Applicazione a pagina mista (rendering ibrido)</td>
  </tr>
  <tr>
   <td><p>Catalogo prodotti</p> </td>
   <td>
    <ul>
     <li>Importazione prodotti, editor, caching in AEM</li>
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
     <li>Può supportare fino a pochi milioni di prodotti (a seconda del caso d’uso)</li>
     <li>Memorizzazione in cache in Dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Nessun limite di volume</li>
     <li>Memorizzazione in cache in Dispatcher o CDN</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modello dati standardizzato</td>
   <td>No</td>
   <td>Sì, schema Adobe Commerce GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilità</td>
   <td><p>Sì. COMMERCE CLOUD SAP (estensione aggiornata per supportare AEM 6.4 e Hybris 5 (impostazione predefinita) e mantenere la compatibilità con Hybris 4</p> <p>Commerce Cloud Salesforce (connettore open source per supportare AEM 6.4)</p> </td>
   <td>Sì tramite open source tramite GitHub. Adobe Commerce (supporta 2.3.2 (impostazione predefinita) e compatibile con 2.3.1).</td>
  </tr>
  <tr>
   <td>Quando utilizzare</td>
   <td>Casi d’uso limitati: ad esempio, scenari in cui potrebbe essere necessario importare cataloghi statici di piccole dimensioni</td>
   <td>Soluzione preferita nella maggior parte dei casi d’uso</td>
  </tr>
 </tbody>
</table>

L’eCommerce, insieme al Product Information Management (PIM), gestisce le attività di un sito web incentrato sulla vendita di prodotti tramite un negozio online:

* Creazione, durata e obsolescenza di un prodotto
* Gestione del prezzo
* Gestione delle transazioni
* Gestione di interi cataloghi
* Record di storage live e centralizzati
* Interfacce web

L’eCommerce dell’AEM aiuta gli esperti di marketing a fornire esperienze di acquisto personalizzate e di marchio attraverso punti di contatto web, mobili e sociali. L’ambiente di authoring AEM consente di personalizzare pagine e componenti in base al contesto del visitatore target e alle strategie di merchandising, ad esempio:

* Pagine prodotto
* Componenti del carrello
* Componenti di cassa

L’implementazione consente l’accesso in tempo reale alle informazioni sui prodotti. Può essere utilizzato per applicare:

* Integrità delle informazioni sul prodotto
* Prezzi
* Inventario delle scorte
* Variazioni dello stato di un carrello

>[!NOTE]
>
>Per utilizzare il framework di integrazione con provider eCommerce esterni, devi innanzitutto installare i pacchetti richiesti. Per ulteriori informazioni, consulta [Distribuzione di eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Per informazioni sull’estensione delle funzionalità di eCommerce, consulta [Sviluppo dell’eCommerce](/help/commerce/cif-classic/developing/ecommerce.md).

## Caratteristiche principali {#main-features}

L’eCommerce dell’AEM fornisce:

* Un certo numero di **componenti AEM preconfigurati** per illustrare cosa si può ottenere da un progetto:

   * Display del prodotto
   * Carrello
   * Check-out
   * Prodotti visualizzati di recente
   * Voucher
   * e altri

  ![esempio di componenti geometrixx](/help/sites-administering/assets/chlimage_1-130.png)

  >[!NOTE]
  >
  >Il framework di integrazione fornito dall’AEM consente inoltre di creare componenti AEM aggiuntivi per le funzionalità di e-commerce, indipendentemente dal motore di eCommerce specifico.

* **Ricerca** - utilizzando:

   * la ricerca AEM
   * la ricerca del sistema di e-commerce
   * una ricerca di terze parti
   * o una combinazione degli stessi.

  ![esempio di ricerca](/help/sites-administering/assets/chlimage_1-131.png)

* Utilizza la capacità dell’AEM di **presentare i contenuti su più canali**, che si tratti dell&#39;intera finestra del browser o del dispositivo mobile. In questo modo i contenuti vengono consegnati nel formato richiesto dai visitatori.

  ![esempio di visualizzazione mobile](/help/sites-administering/assets/chlimage_1-132.png)

* La capacità di **sviluppare un’implementazione personalizzata dell’integrazione in base al [Quadro per l’eCommerce dell’AEM](#the-framework)**.

  Le due implementazioni attualmente disponibili sono entrambe basate sulla stessa API generale (il framework). L’implementazione di una nuova integrazione comporta solo l’implementazione delle funzioni necessarie per l’integrazione. I componenti front-end possono essere utilizzati da qualsiasi nuova implementazione in quanto utilizzano le interfacce (in modo che siano indipendenti dall’implementazione).

* La possibilità di sviluppare **commercio basato sull’esperienza e basato sui dati e sull’attività dell’acquirente**. Questo consente di realizzare molti scenari:

   * Un esempio potrebbe essere la riduzione delle spese di spedizione quando l&#39;ordine totale supera un importo specifico.
   * Un altro potrebbe consentirti di fornire offerte stagionali che utilizzano dati di profilo (ad esempio, posizione). Questi possono quindi essere evidenziati, anche in questo caso a seconda di altri fattori, se necessario.

  Nell’esempio seguente viene mostrato un teaser poiché il contenuto del carrello è inferiore a $ 75:

  ![carrello con contesto cliente](/help/sites-administering/assets/chlimage_1-133.png)

  Questo può essere modificato quando il contenuto del carrello supera i $ 75:

  ![carrello con contesto client dopo la modifica](/help/sites-administering/assets/chlimage_1-134.png)

* E altre caratteristiche, tra cui:

   * Contenuto del carrello mantenuto nelle sessioni
   * Cronologia ordine completa
   * Aggiornamento del catalogo rapido

## Il framework {#the-framework}

Il [Concetti](/help/commerce/cif-classic/administering/concepts.md) la sezione descrive il quadro in modo più dettagliato, ma la sezione seguente fornisce una visione ad alto livello e ad alta velocità del quadro:

### Cosa? {#what}

* Il framework di integrazione fornisce l’API, una serie di componenti per illustrare le funzionalità e diverse estensioni per fornire esempi di metodi di connessione.
* Il framework fornisce la struttura di base necessaria per l&#39;implementazione di un progetto.
* Il framework è estensibile.
* Il framework non fornisce un sito pronto all’uso e pronto all’uso. È sempre necessario un certo impegno di sviluppo per adattare il framework alle proprie specifiche.

### Perché? {#why}

* Fornire i meccanismi di base necessari per realizzare rapidamente un sito di e-commerce personalizzato.
* La tecnologia Tp offre la flessibilità necessaria per sviluppare un sito di e-commerce reale.
* Illustrare le best practice.
