---
title: COMMERCE CLOUD SAP
seo-title: COMMERCE CLOUD SAP
description: Scopri come utilizzare AEM con SAP Commerce Cloud.
seo-description: Scopri come utilizzare AEM con SAP Commerce Cloud.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 9474519d-14cc-49e0-a81d-9319966fd1f6
pagetitle: Administering hybris
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 2%

---


# COMMERCE CLOUD SAP{#sap-commerce-cloud}

Dopo l’installazione potete configurare l’istanza:

1. [Configurate la ricerca di Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors) in facet.
1. [Configurare la versione](#configure-the-catalog-version) del catalogo.
1. [Configurare la struttura](#configure-the-import-structure) di importazione.
1. [Configurare gli attributi del prodotto da caricare](#configure-the-product-attributes-to-load).
1. [Importazione dei dati](#importing-the-product-data) del prodotto.
1. [Configurare Catalog Importer](#configure-the-catalog-importer).
1. Utilizzate l&#39;utilità di importazione [per importare il catalogo](#catalog-import) in una posizione specifica in AEM.

## Configurare la ricerca su facet per Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Questo non è necessario per hybris 5.3.0.1 e versioni successive.

1. Nel browser, andate alla **console di gestione ibrida** all&#39;indirizzo:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Dalla barra laterale, selezionare **System**, quindi **Facet search**, quindi **Facet Search Config**.
1. **Aprite** Editor per la configurazione di  **esempio Solr per clothescatalog**.

1. In **Versioni catalogo** utilizzare **Aggiungi versione catalogo** per aggiungere `outdoors-Staged` e `outdoors-Online` all&#39;elenco.
1. **Salva la configurazione.**
1. Aprire **SOLR Item types** per aggiungere **SOLR Sorts** a `ClothesVariantProduct`:

   * rilevanza (&quot;Pertinenza&quot;, punteggio)
   * name-asc (&quot;Name (crescente)&quot;, name)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Price (crescente)&quot;, priceValue)
   * price-desc (&quot;Price (descending)&quot;, priceValue)

   >[!NOTE]
   >
   >Utilizzate il menu di scelta rapida (in genere fate clic con il pulsante destro del mouse) per selezionare `Create Solr sort`.
   >
   >Per Hybris 5.0.0 aprire la scheda `Indexed Types`, fare doppio clic su `ClothesVariantProduct`, quindi sulla scheda `SOLR Sort`.

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. Nella scheda **Tipi indicizzati** impostare il tipo composto **Type** su:

   `Product - Product`

1. Nella scheda **Tipi indicizzati** regolare le query indicizzatore **a3/> per `full`:**

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. Nella scheda **Tipi indicizzati** regolare le query indicizzatore **a3/> per `incremental`:**

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. Nella scheda **Tipi indicizzati** regolare il facet `category`. Fare doppio clic sull&#39;ultima voce nell&#39;elenco delle categorie per aprire la scheda **Proprietà indicizzata**:

   >[!NOTE]
   >
   >Per hybris 5.2, accertatevi che l&#39;attributo `Facet` nella tabella Properties (Proprietà) sia selezionato in base alla schermata seguente:

   ![chlimage_1-37](assets/chlimage_1-37a.png) ![chlimage_1-38](assets/chlimage_1-38a.png)

1. Aprite la scheda **Impostazioni facet** e regolate i valori dei campi:

   ![chlimage_1-39](assets/chlimage_1-39a.png)

1. **Salva le modifiche.**
1. Di nuovo da **SOLR Item types**, regolare il facet `price` in base alle seguenti schermate. Come con `category`, fare doppio clic su `price` per aprire la scheda **Proprietà indicizzata**:

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. Aprite la scheda **Impostazioni facet** e regolate i valori dei campi:

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. **Salva le modifiche.**
1. Aprire **System**, **Facet search**, quindi **Indicizzatore operation Wizard**. Avvia un cronjob:

   * **Operazione** indicizzatore:  `full`
   * **Configurazione** Solr:  `Sample Solr Config for Clothes`

## Configurare la versione del catalogo {#configure-the-catalog-version}

La **versione del catalogo** ( `hybris.catalog.version`) importata può essere configurata per il servizio OSGi:

**Configurazione**
 dell&#39;ibrido di CQ Commerce Day(  `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**La** versione del catalogo è in genere impostata su  `Online` o  `Staged` (impostazione predefinita).

>[!NOTE]
>
>Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consultare anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

L’output del registro fornisce un feedback sulle pagine e sui componenti creati e segnala potenziali errori.

## Configurare la struttura di importazione {#configure-the-import-structure}

L’elenco seguente mostra una struttura di esempio (di risorse, pagine e componenti) creata per impostazione predefinita:

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

Tale struttura viene creata dal servizio OSGi `DefaultImportHandler` che implementa l&#39;interfaccia `ImportHandler`. L&#39;importatore effettivo chiama un gestore di importazioni per creare prodotti, varianti di prodotti, categorie, risorse e così via.

>[!NOTE]
>
>È possibile [personalizzare questo processo implementando il proprio gestore di importazione](#configure-the-import-structure).

La struttura da generare durante l&#39;importazione può essere configurata per:

&quot;**Giorno CQ Commerce Hybris - Gestore importazione predefinito**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consultare anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Configurare gli attributi del prodotto da caricare {#configure-the-product-attributes-to-load}

Il parser di risposte può essere configurato per definire le proprietà e gli attributi da caricare per i prodotti (variante):

1. Configurare il bundle OSGi:

   **Analisi**
 di risposta predefinita per CQ Commerce Day (`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Qui puoi definire le varie opzioni e attributi necessari per il caricamento e la mappatura.

   >[!NOTE]
   >
   >Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consultare anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Importazione di dati prodotto {#importing-the-product-data}

Esistono diversi modi per importare i dati del prodotto. I dati del prodotto possono essere importati al momento della configurazione iniziale dell&#39;ambiente o dopo aver apportato modifiche nei dati hybris:

* [Importazione completa](#full-import)
* [Importazione incrementale](#incremental-import)
* [Express Update](#express-update)

Le informazioni effettive sul prodotto importate da hybris sono memorizzate nella directory archivio in:

`/etc/commerce/products`

Le seguenti proprietà indicano il collegamento con hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>Implementazione dell&#39;hybris (es. `geometrixx-outdoors/en_US`) memorizza solo gli ID prodotto e altre informazioni di base in `/etc/commerce`.
>
>Viene fatto riferimento al server hybris ogni volta che vengono richieste informazioni su un prodotto.

### Importazione completa {#full-import}

1. Se necessario, eliminate tutti i dati di prodotto esistenti utilizzando CRXDE Lite.

   1. Andate alla sottostruttura che contiene i dati del prodotto:

      `/etc/commerce/products`

      Esempio:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Eliminare il nodo che contiene i dati del prodotto; ad esempio, `outdoors`.
   1. **Salva** tutto per mantenere la modifica.

1. Aprite hybris importer in AEM:

   `/etc/importers/hybris.html`

   Esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configurare i parametri richiesti; ad esempio:

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Fare clic su **Importa catalogo** per avviare l&#39;importazione.

   Al termine, è possibile verificare i dati importati in:

   ```
       /etc/commerce/products/outdoors
   ```

   È possibile aprirlo in CRXDE Lite; ad esempio:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importazione incrementale {#incremental-import}

1. Controllare le informazioni detenute in AEM per i prodotti interessati, nella sottostruttura appropriata sotto:

   `/etc/commerce/products`

   È possibile aprirlo in CRXDE Lite; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni detenute sui prodotti rivelatori.

1. Aprite hybris importer in AEM:

   `/etc/importers/hybris.html`

   Esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Selezionare la casella di controllo **Importazione incrementale**.
1. Fare clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM sotto:

   ```
       /etc/commerce/products
   ```


### Express Update {#express-update}

Il processo di importazione può richiedere molto tempo, pertanto un’estensione alla sincronizzazione dei prodotti consente di selezionare aree specifiche del catalogo per un aggiornamento rapido attivato manualmente. Questo utilizza il feed di esportazione insieme alla configurazione degli attributi standard.

1. Controllare le informazioni detenute in AEM per i prodotti interessati, nella sottostruttura appropriata sotto:

   `/etc/commerce/products`

   È possibile aprirlo in CRXDE Lite; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni detenute sui prodotti rivelatori.

1. In hybris, aggiungere i prodotti alla coda espressa; ad esempio:

   ![chlimage_1-43](assets/chlimage_1-43a.png)

1. Aprite hybris importer in AEM:

   `/etc/importers/hybris.html`

   Esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Selezionare la casella di controllo **Express Update**.
1. Fare clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM sotto:

   ```
       /etc/commerce/products
   ```

   ` [](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

## Configurare l&#39;importazione catalogo {#configure-the-catalog-importer}

Il catalogo hybris può essere importato in AEM, utilizzando Importazione batch per cataloghi, categorie e prodotti ibridi.

I parametri utilizzati dall&#39;importatore possono essere configurati per:

**Importazione**
 catalogo Ibris di CQ Commerce Day(  `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consultare anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Importazione catalogo {#catalog-import}

Il pacchetto hybris viene fornito con un importatore di catalogo per impostare la struttura di pagina iniziale.

È disponibile da:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](assets/ecommerceimportconsole.png)

Devono essere fornite le seguenti informazioni:

* **Base**
storeIdentificatore dello store di base configurato in hybris.

* ****
Catalogo: l’identificatore del catalogo da importare.

* **Percorso**
radice: percorso in cui importare il catalogo.

## Rimozione di un prodotto dal catalogo {#removing-a-product-from-the-catalog}

Per rimuovere uno o più prodotti dal catalogo:

1. [Configurare l&#39;opzione per l&#39;importazione di catalogo ](/help/sites-deploying/configuring-osgi.md) **di Hybris per OSGi ServiceDay CQ Commerce**; consultate anche  [Configurare l’importazione](#configure-the-catalog-importer) del catalogo.

   Attivare le seguenti proprietà:

   * **Abilita rimozione prodotto**
   * **Abilita rimozione risorse di prodotto**

   >[!NOTE]
   >
   >Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consultare anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

1. Inizializzare l&#39;importazione eseguendo due aggiornamenti incrementali (vedere [Importazione catalogo](#catalog-import)):

   * Il primo risultato di esecuzione consiste in un set di prodotti modificati, indicato nell&#39;elenco di registro.
   * Per la seconda volta nessun prodotto deve essere aggiornato.

   >[!NOTE]
   >
   >La prima importazione consiste nell&#39;inizializzare le informazioni sul prodotto. La seconda importazione verifica che tutto è stato lavorato e il set di prodotti è pronto.

1. Controllate la pagina della categoria che contiene il prodotto da rimuovere. I dettagli del prodotto devono essere visibili.

   Ad esempio, la seguente categoria mostra i dettagli del prodotto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Rimuovere il prodotto dalla console hybris. Utilizzare l&#39;opzione **Modifica stato approvazione** per impostare lo stato su `unapproved`. Il prodotto verrà rimosso dal feed live.

   Esempio:

   * Aprire la pagina [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Selezionare il catalogo `Outdoors Staged`
   * Cerca `Cajamara`
   * Selezionate questo prodotto e cambiate lo stato di approvazione in `unapproved`

1. Eseguire un altro aggiornamento incrementale (vedere [Importazione catalogo](#catalog-import)). Il registro elenca il prodotto eliminato.
1. [Eseguire il ](/help/sites-administering/generic.md#rolling-out-a-catalog) rollout del catalogo appropriato. La pagina prodotto e prodotto sarà stata rimossa dall&#39;interno AEM.

   Esempio:

   * Apri:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Rollout del catalogo `Hybris Base`
   * Apri:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * Il prodotto `Cajamara` sarà stato rimosso dalla categoria `Bike`

1. Per ripristinare il prodotto:

   1. In hybris, reimpostare lo stato di approvazione su **approvato**
   1. In AEM:

      1. eseguire un aggiornamento incrementale
      1. rollout del catalogo appropriato
      1. aggiorna la pagina della categoria appropriata

## Aggiungi caratteristica cronologia ordine al contesto client {#add-order-history-trait-to-the-client-context}

Per aggiungere la cronologia degli ordini al [contesto client](/help/sites-developing/client-context.md):

1. Aprite la [pagina di progettazione del contesto client](/help/sites-administering/client-context.md), effettuando una delle seguenti operazioni:

   * Aprite una pagina per la modifica, quindi aprite il contesto client utilizzando **Ctrl-Alt-c** (finestre) o **control-option-c** (Mac). Utilizzate l&#39;icona matita nell&#39;angolo superiore sinistro del contesto client per **Aprire la pagina di progettazione del ClientContext**.
   * Passa direttamente a [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Aggiungete il componente  **Cronologia** ](/help/sites-administering/client-context.md#adding-a-property-component) ordine al componente  **** Carrello acquisti del contesto client.
1. È possibile confermare che il contesto cliente mostra i dettagli della cronologia degli ordini. Esempio:

   1. Aprire il [contesto client](/help/sites-administering/client-context.md).
   1. Aggiungi un elemento al carrello.
   1. Completate il checkout.
   1. Controllare il contesto del client.
   1. Aggiungi un altro elemento al carrello.
   1. Passate alla pagina di estrazione:

      * Il contesto client mostra un riepilogo della cronologia dell&#39;ordine.
      * Viene visualizzato il messaggio &quot;Sei un cliente di ritorno&quot;.

   >[!NOTE]
   >
   >Il messaggio è realizzato da:
   >
   >* Passa a [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  La campagna è composta da un&#39;esperienza.
   >
   >* Fare clic sul segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
      >
      >
   * Il segmento viene creato utilizzando la caratteristica **Proprietà cronologia ordine**.

