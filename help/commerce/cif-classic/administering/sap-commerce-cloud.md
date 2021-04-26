---
title: Commerce Cloud SAP
seo-title: Commerce Cloud SAP
description: Scopri come utilizzare AEM con SAP Commerce Cloud.
seo-description: Scopri come utilizzare AEM con SAP Commerce Cloud.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 2%

---

# Commerce Cloud SAP{#sap-commerce-cloud}

Dopo l’installazione, puoi configurare la tua istanza:

1. [Configura la ricerca di Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors) per Facet.
1. [Configura la versione del catalogo](#configure-the-catalog-version).
1. [Configura la struttura](#configure-the-import-structure) di importazione.
1. [Configura gli attributi del prodotto da caricare](#configure-the-product-attributes-to-load).
1. [Importazione dei dati di prodotto](#importing-the-product-data).
1. [Configura l’importazione del catalogo](#configure-the-catalog-importer).
1. Utilizza l’ [importazione per importare il catalogo](#catalog-import) in una posizione specifica in AEM.

## Configura la ricerca su facet per i Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Questo non è necessario per hybris 5.3.0.1 e versioni successive.

1. Nel browser, accedi alla **console di gestione ibrida** all&#39;indirizzo:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Dalla barra laterale selezionare **Sistema**, quindi **Ricerca facet**, quindi **Configurazione ricerca facet**.
1. **Apri** Editor per la configurazione del  **campione Solr per clothescatalog**.

1. In **Versioni catalogo** utilizza **Aggiungi versione catalogo** per aggiungere `outdoors-Staged` e `outdoors-Online` all’elenco.
1. **Salva la configurazione.**
1. Apri **SOLR Item types** per aggiungere **SOLR Sorts** a `ClothesVariantProduct`:

   * pertinenza (&quot;pertinenza&quot;, punteggio)
   * name-asc (&quot;Name (ascending)&quot;, name)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Price (ascending)&quot;, priceValue)
   * price-desc (&quot;Price (descending)&quot;, priceValue)

   >[!NOTE]
   >
   >Utilizza il menu di scelta rapida (in genere fai clic con il pulsante destro del mouse) per selezionare `Create Solr sort`.
   >
   >Per Hybris 5.0.0 aprire la scheda `Indexed Types`, fare doppio clic su `ClothesVariantProduct`, quindi sulla scheda `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. Nella scheda **Tipi indicizzati** , imposta il valore **Tipo composto** su:

   `Product - Product`

1. Nella scheda **Tipi indicizzati** , regola le **query indicizzatrici** per `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. Nella scheda **Tipi indicizzati** , regola le **query indicizzatrici** per `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. Nella scheda **Tipi indicizzati** regolare il facet `category`. Fai doppio clic sull&#39;ultima voce nell&#39;elenco delle categorie per aprire la scheda **Proprietà indicizzata** :

   >[!NOTE]
   >
   >Per hybris 5.2, accertati che l&#39;attributo `Facet` nella tabella Proprietà sia selezionato in base alla schermata seguente:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Apri la scheda **Impostazioni facet** e regola i valori dei campi:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Salva le modifiche.**
1. Di nuovo da **SOLR Tipi di elementi**, regolare il facet `price` in base alle seguenti schermate. Come con `category`, fai doppio clic su `price` per aprire la scheda **Proprietà indicizzata** :

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Apri la scheda **Impostazioni facet** e regola i valori dei campi:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Salva le modifiche.**
1. Apri **Sistema**, **Ricerca di facet**, quindi **Procedura guidata di funzionamento dell&#39;indicizzatore**. Avvia un cronjob:

   * **Operazione** indicizzatore:  `full`
   * **Configurazione** solare:  `Sample Solr Config for Clothes`

## Configurare la versione del catalogo {#configure-the-catalog-version}

Il **Catalogo versione** ( `hybris.catalog.version`) importato può essere configurato per il servizio OSGi:

**Configurazione**
 di Day CQ Commerce Hybris (  `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**La** versione del catalogo è in genere impostata su  `Online` o  `Staged` (opzione predefinita).

>[!NOTE]
>
>Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) . Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

L’output del registro fornisce un feedback sulle pagine e sui componenti creati e segnala potenziali errori.

## Configura la struttura di importazione {#configure-the-import-structure}

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

Tale struttura viene creata dal servizio OSGi `DefaultImportHandler` che implementa l&#39;interfaccia `ImportHandler`. Un gestore di importazione viene chiamato dall’importazione effettiva per creare prodotti, varianti di prodotto, categorie, risorse, ecc.

>[!NOTE]
>
>Puoi [personalizzare questo processo implementando il tuo handler di importazione](#configure-the-import-structure).

La struttura da generare durante l’importazione può essere configurata per:

&quot;**Day CQ Commerce Hybris Default Import Handler**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) . Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Configurare gli attributi del prodotto da caricare {#configure-the-product-attributes-to-load}

Il parser di risposta può essere configurato per definire le proprietà e gli attributi da caricare per i prodotti (variante):

1. Configura il bundle OSGi:

   **Analisi della risposta predefinita di Day CQ Commerce Hybris**
 (`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Qui puoi definire varie opzioni e attributi necessari per il caricamento e la mappatura.

   >[!NOTE]
   >
   >Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) . Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Importazione dei dati del prodotto {#importing-the-product-data}

Esistono diversi modi per importare i dati del prodotto. I dati del prodotto possono essere importati quando si configura inizialmente l’ambiente o dopo aver apportato modifiche nei dati di hybris:

* [Importazione completa](#full-import)
* [Importazione incrementale](#incremental-import)
* [Aggiornamento espresso](#express-update)

Le informazioni effettive sul prodotto importate da hybris sono conservate nell’archivio in:

`/etc/commerce/products`

Le seguenti proprietà indicano il collegamento con hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>Implementazione dell’ibrido (ad es. `geometrixx-outdoors/en_US`) memorizza solo gli ID prodotto e altre informazioni di base in `/etc/commerce`.
>
>Viene fatto riferimento al server ibrido ogni volta che vengono richieste informazioni su un prodotto.

### Importazione completa {#full-import}

1. Se necessario, elimina tutti i dati di prodotto esistenti utilizzando CRXDE Lite.

   1. Passa alla struttura ad albero secondario contenente i dati del prodotto:

      `/etc/commerce/products`

      Esempio:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Elimina il nodo che contiene i dati del prodotto; ad esempio, `outdoors`.
   1. **Salva** tutto per mantenere la modifica.

1. Apri l’importazione di hybris in AEM:

   `/etc/importers/hybris.html`

   Esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configura i parametri richiesti; ad esempio:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Fai clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati importati in:

   ```
       /etc/commerce/products/outdoors
   ```

   È possibile aprirlo in CRXDE Lite; ad esempio:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importazione incrementale {#incremental-import}

1. Controllare le informazioni contenute in AEM per il prodotto o i prodotti in questione, nella sottostruttura appropriata sotto:

   `/etc/commerce/products`

   È possibile aprirlo in CRXDE Lite; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni detenute sui prodotti rivelatori.

1. Apri l’importazione di hybris in AEM:

   `/etc/importers/hybris.html`

   Esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleziona la casella di selezione **Importazione incrementale**.
1. Fai clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```


### Aggiornamento Express {#express-update}

Il processo di importazione può richiedere molto tempo, in modo che un&#39;estensione alla sincronizzazione prodotto possa selezionare aree specifiche del catalogo per un aggiornamento rapido che viene attivato manualmente. Questo utilizza il feed di esportazione e la configurazione degli attributi standard.

1. Controllare le informazioni contenute in AEM per il prodotto o i prodotti in questione, nella sottostruttura appropriata sotto:

   `/etc/commerce/products`

   È possibile aprirlo in CRXDE Lite; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni detenute sui prodotti rivelatori.

1. In hybris, aggiungere i prodotti alla coda Express; ad esempio:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Apri l’importazione di hybris in AEM:

   `/etc/importers/hybris.html`

   Esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleziona la casella di selezione **Aggiorna express**.
1. Fai clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```

   ` [](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

## Configurare l&#39;importazione di catalogo {#configure-the-catalog-importer}

Il catalogo ibrido può essere importato in AEM, utilizzando l’importazione batch per cataloghi, categorie e prodotti ibridi.

I parametri utilizzati dall’importazione possono essere configurati per:

**Importazione catalogo ibridi di CQ Day CQ**
(  `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) . Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Importazione catalogo {#catalog-import}

Il pacchetto hybris viene fornito con un importatore di catalogo per l’impostazione della struttura della pagina iniziale.

È disponibile da:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Devono essere fornite le seguenti informazioni:

* **Base**
StoreIdentificatore dell&#39;archivio di base configurato in hybris.

* ****
CatalogoIdentificatore del catalogo da importare.

* **Percorso**
principalePercorso in cui importare il catalogo.

## Rimozione di un prodotto dal catalogo {#removing-a-product-from-the-catalog}

Per rimuovere uno o più prodotti dal catalogo:

1. [Configura l&#39;importazione per ](/help/sites-deploying/configuring-osgi.md) **catalogo di Hybris di OSGi ServiceDay CQ Commerce**; consulta anche  [Configurare l’importazione di catalogo](#configure-the-catalog-importer).

   Attiva le seguenti proprietà:

   * **Abilita rimozione prodotti**
   * **Abilita rimozione risorse di prodotto**

   >[!NOTE]
   >
   >Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) . Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

1. Inizializzare l&#39;importazione eseguendo due aggiornamenti incrementali (vedere [Importazione catalogo](#catalog-import)):

   * La prima esecuzione comporta un set di prodotti modificati, indicato nell’elenco dei registri.
   * Per la seconda volta nessun prodotto deve essere aggiornato.

   >[!NOTE]
   >
   >La prima importazione consiste nell’inizializzare le informazioni di prodotto. La seconda importazione verifica che tutto sia stato lavorato e che il set di prodotti è pronto.

1. Seleziona la pagina della categoria contenente il prodotto da rimuovere. I dettagli del prodotto devono essere visibili.

   Ad esempio, la seguente categoria mostra i dettagli del prodotto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Rimuovi il prodotto dalla console hybris. Utilizza l&#39;opzione **Cambia lo stato di approvazione** per impostare lo stato su `unapproved`. Il prodotto verrà rimosso dal feed live.

   Esempio:

   * Apri la pagina [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Seleziona il catalogo `Outdoors Staged`
   * Cerca `Cajamara`
   * Seleziona questo prodotto e modifica lo stato di approvazione in `unapproved`

1. Esegui un altro aggiornamento incrementale (consulta [Importazione catalogo](#catalog-import)). Il registro elencherà il prodotto eliminato.
1. [](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) Rollout del catalogo appropriato. La pagina prodotto e prodotto sarà stata rimossa da AEM.

   Esempio:

   * Apri:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Rollout del catalogo `Hybris Base`
   * Apri:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * Il prodotto `Cajamara` sarà stato rimosso dalla categoria `Bike`

1. Per ripristinare il prodotto:

   1. In hybris, imposta nuovamente lo stato di approvazione su **approvato**
   1. In AEM:

      1. eseguire un aggiornamento incrementale
      1. rollout del catalogo appropriato
      1. aggiorna la pagina della categoria appropriata

## Aggiungi le caratteristiche della cronologia degli ordini al contesto client {#add-order-history-trait-to-the-client-context}

Per aggiungere la cronologia degli ordini al [contesto client](/help/sites-developing/client-context.md):

1. Apri la [pagina di progettazione del contesto client](/help/sites-administering/client-context.md), effettuando una delle seguenti operazioni:

   * Apri una pagina per la modifica, quindi apri il contesto client utilizzando **Ctrl-Alt-c** (windows) o **control-option-c** (Mac). Utilizza l&#39;icona a forma di matita nell&#39;angolo in alto a sinistra del contesto client per **Aprire la pagina di progettazione del ClientContext**.
   * Passa direttamente a [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Aggiungi il componente  **Cronologia** ](/help/sites-administering/client-context.md#adding-a-property-component) ordine al componente  **Carrello** acquisti del contesto client.
1. Puoi confermare che il contesto client sta mostrando i dettagli della cronologia degli ordini. Esempio:

   1. Apri [ClientContext](/help/sites-administering/client-context.md).
   1. Aggiungi un elemento al carrello.
   1. Completa il checkout.
   1. Controlla il contesto client.
   1. Aggiungi un altro elemento al carrello.
   1. Passa alla pagina di pagamento:

      * Il contesto client mostra un riepilogo della cronologia dell&#39;ordine.
      * Viene visualizzato il messaggio &quot;Sei un cliente di ritorno&quot;.

   >[!NOTE]
   >
   >Il messaggio viene realizzato da:
   >
   >* Passa a [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  La campagna è costituita da un’esperienza.
   >
   >* Fai clic sul segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
      >
      >
   * Il segmento viene creato utilizzando la caratteristica **Proprietà cronologia ordine** .

