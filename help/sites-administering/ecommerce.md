---
title: eCommerce
seo-title: eCommerce
description: AEM eCommerce consente ai professionisti del marketing di offrire esperienze di acquisto personalizzate e personalizzate su siti Web, dispositivi mobili e social network.
seo-description: AEM eCommerce consente ai professionisti del marketing di offrire esperienze di acquisto personalizzate e personalizzate su siti Web, dispositivi mobili e social network.
uuid: 75818c60-1cf1-4a91-94ce-d722563b661c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: e972ee05-f0cb-40ca-9ae2-34395791c709
docset: aem65
translation-type: tm+mt
source-git-commit: 46610888fd61900c52b197e73a8a5850dc9c4c35
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---


# eCommerce{#ecommerce}

* [Concetti ](/help/sites-administering/concepts.md)
* [Amministrazione (generica)](/help/sites-administering/generic.md)

 Adobe fornisce due versioni di Commerce Integration Framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF on-prem</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>Versioni di AEM supportate</p> </td>
   <td><p>AEM on prem o AMS 6.x</p> </td>
   <td>AEM AMS 6.4 e 6.5</td>
  </tr>
  <tr>
   <td><p>Back-end</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>Integrazione monolitica, mappatura pre-build (modello)</li>
     <li>Repository JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Magento</li>
     <li>Java e JavaScript</li>
     <li>Nessun dato di commercio memorizzato nell'archivio JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>AEM pagine sottoposte a rendering sul lato server</p> </td>
   <td>Applicazione a pagina mista (rendering ibrido)</td>
  </tr>
  <tr>
   <td><p>Catalogo prodotti</p> </td>
   <td>
    <ul>
     <li>Importazione prodotti, editor, memorizzazione nella cache in AEM</li>
     <li>Cataloghi regolari con pagine AEM o proxy</li>
    </ul> </td>
   <td>
    <ul>
     <li>Nessuna importazione di prodotti</li>
     <li>Modelli generici</li>
     <li>Dati su richiesta tramite connettore</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Scalabilità</p> </td>
   <td>
    <ul>
     <li>Può supportare fino a pochi milioni di prodotti (dipende dal caso d'uso)</li>
     <li>Memorizzazione in cache del dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Nessuna limitazione del volume</li>
     <li>Memorizzazione nella cache del dispatcher o CDN</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modello dati standardizzato</td>
   <td>No</td>
   <td>Sì, schema Magento GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilità</td>
   <td><p>Sì. COMMERCE CLOUD SAP (estensione aggiornata per supportare AEM 6.4 e Hybris 5 (impostazione predefinita) e mantenere la compatibilità con Hybris 4</p> <p>Commerce Cloud Salesforce (connettore open-source per supportare AEM 6.4)</p> </td>
   <td>Sì tramite open source tramite GitHub. Magento Commerce (Supporta l'Magento 2.3.2 (predefinito) e compatibile con Magento 2.3.1).</td>
  </tr>
  <tr>
   <td>Quando utilizzare</td>
   <td>Casi di utilizzo limitati: Ad esempio, in situazioni in cui potrebbe essere necessario importare cataloghi statici di piccole dimensioni</td>
   <td>Soluzione preferita nella maggior parte dei casi di utilizzo</td>
  </tr>
 </tbody>
</table>

eCommerce, insieme a Product Information Management (PIM), gestisce le attività di un sito web incentrato sulla vendita di prodotti tramite un negozio online:

* Creazione, durata e obsolescenza di un prodotto
* Gestione dei prezzi
* Gestione delle transazioni
* Gestione di interi cataloghi
* Record di archiviazione live e centralizzati
* Interfacce Web

AEM eCommerce consente ai professionisti del marketing di offrire esperienze di acquisto personalizzate e personalizzate su siti Web, dispositivi mobili e social network. L’ambiente di authoring AEM consente di personalizzare pagine e componenti in base al contesto del visitatore e alle strategie di merchandising; ad esempio:

* Pagine prodotto
* Componenti per carrello acquisti
* Componenti di estrazione

L&#39;implementazione consente l&#39;accesso in tempo reale alle informazioni sui prodotti. Può essere utilizzato per applicare:

* Integrità delle informazioni sui prodotti
* Prezzi
* Scorte
* Variazioni nello stato di un carrello

>[!NOTE]
>
>Per utilizzare il framework di integrazione con i provider di eCommerce esterni, è innanzitutto necessario installare i pacchetti richiesti. Per ulteriori informazioni, vedere [Distribuzione di eCommerce](/help/sites-deploying/ecommerce.md).
>
>Per informazioni sull&#39;estensione delle funzionalità di eCommerce, vedere [Sviluppo di eCommerce](/help/sites-developing/ecommerce.md).

## Funzioni principali {#main-features}

AEM eCommerce fornisce:

* Una serie di **componenti AEM out-of-the-box** per illustrare i risultati che è possibile ottenere per il progetto:

   * Visualizzazione del prodotto
   * Carrello
   * Check-out
   * Prodotti visualizzati di recente
   * Voucher
   * e altri

   ![](assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >Il framework di integrazione fornito da AEM consente inoltre di creare componenti AEM aggiuntivi per le funzionalità di eCommerce, indipendentemente dal motore specifico utilizzato.

* **Cerca** - utilizzando:

   * ricerca AEM
   * la ricerca del sistema eCommerce
   * una ricerca di terze parti (ad esempio, Search&amp;Promote)
   * o una loro combinazione.

   ![](assets/chlimage_1-131.png)

* Utilizza la capacità AEM di **presentare i contenuti su più canali**, indipendentemente dalla finestra del browser completa o dal dispositivo mobile. In questo modo, i contenuti vengono distribuiti nel formato richiesto dai visitatori.

   ![](assets/chlimage_1-132.png)

* La capacità di **sviluppare la propria implementazione di integrazione in base al [AEM eCommerce framework](#the-framework)**.

   Le due implementazioni attualmente disponibili sono entrambe basate sulla stessa base, oltre all&#39;API generale (il framework). L&#39;implementazione di una nuova integrazione richiede solo l&#39;implementazione delle funzioni necessarie per l&#39;integrazione. I componenti front-end possono essere utilizzati da qualsiasi nuova implementazione utilizzando interfacce (in modo che siano indipendenti dall&#39;implementazione).

* La possibilità di sviluppare **e-commerce basato sull&#39;esperienza in base ai dati e alle attività dell&#39;acquirente**. Questo consente di realizzare molti scenari:

   * Un esempio potrebbe consistere nel fornire riduzioni dei costi di spedizione quando l&#39;ordine totale supera un importo specifico.
   * Un altro potrebbe consentire di fornire offerte stagionali che utilizzano i dati del profilo (ad esempio la posizione). Questi possono quindi essere evidenziati, sempre in base ad altri fattori, se necessario.

   Nell’esempio di seguito, un teaser viene visualizzato in quanto il contenuto del carrello è inferiore a $75:

   ![](assets/chlimage_1-133.png)

   Questo può essere modificato quando il contenuto del carrello supera i $75:

   ![](assets/chlimage_1-134.png)

* Altre caratteristiche, tra cui:

   * Contenuto del carrello acquisti conservato tra le sessioni
   * Cronologia ordine completo
   * Aggiornamento del catalogo espresso

## Framework {#the-framework}

La sezione [Concetti](/help/sites-administering/concepts.md) descrive il framework in modo più dettagliato, ma quanto segue fornisce una visualizzazione ad alto livello del framework:

### Cosa? {#what}

* Il framework di integrazione fornisce l&#39;API, una serie di componenti per illustrare le funzionalità e diverse estensioni per fornire esempi di metodi di connessione.
* Il quadro fornisce la struttura di base necessaria per l&#39;implementazione di un progetto.
* Il framework è estensibile.
* Il framework non fornisce un sito pronto all&#39;uso e pronto all&#39;uso. Per adattare il framework alle proprie specifiche, è sempre necessario un certo lavoro di sviluppo.

### Perché? {#why}

* Fornire i meccanismi di base necessari per realizzare rapidamente un sito eCommerce personalizzato.
* Tp offre la flessibilità necessaria per sviluppare un sito eCommerce reale.
* Illustra le best practice.