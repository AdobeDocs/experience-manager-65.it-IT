---
title: Commerce Cloud SAP
seo-title: SAP Commerce Cloud
description: Scopri come utilizzare AEM con SAP Commerce Cloud.
seo-description: Learn how to use AEM with SAP Commerce Cloud.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: 61691c300322edcdee33b121ca400e4c89256e45
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 2%

---

# Commerce Cloud SAP{#sap-commerce-cloud}

Dopo l’installazione, puoi configurare la tua istanza:

1. [Configurare la ricerca di Geometrixx Outdoors in facet](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configurare la versione del catalogo](#configure-the-catalog-version).
1. [Configurare la struttura di importazione](#configure-the-import-structure).
1. [Configurare gli attributi di prodotto da caricare](#configure-the-product-attributes-to-load).
1. [Importazione dei dati di prodotto](#importing-the-product-data).
1. [Configurare l’importazione di catalogo](#configure-the-catalog-importer).
1. Utilizza la [Importazione per importare il catalogo](#catalog-import) in una posizione specifica in AEM.

## Configurare la ricerca di Geometrixx Outdoors in facet {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Questo non è necessario per hybris 5.3.0.1 e versioni successive.

1. Nel browser, accedi alla **console di gestione ibrida** a:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Dalla barra laterale, seleziona **Sistema**, quindi **Ricerca dei facet**, quindi **Configurazione di ricerca dei facet**.
1. **Open Editor** per **Configurazione del solr campione per Clothescatalog**.

1. Sotto **Versioni del catalogo** use **Aggiungi versione catalogo** per aggiungere `outdoors-Staged` e `outdoors-Online` all&#39;elenco.
1. **Salva la configurazione.**
1. Apri **Tipi di elementi SOLR** per aggiungere **Sorgenti SOLR** a `ClothesVariantProduct`:

   * pertinenza (&quot;pertinenza&quot;, punteggio)
   * name-asc (&quot;Name (ascending)&quot;, name)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Price (ascending)&quot;, priceValue)
   * price-desc (&quot;Price (descending)&quot;, priceValue)

   >[!NOTE]
   >
   >Utilizza il menu di scelta rapida (in genere fai clic con il pulsante destro del mouse) per selezionare `Create Solr sort`.
   >
   >Per Hybris 5.0.0 apri la sezione `Indexed Types` scheda, doppio clic su `ClothesVariantProduct`, quindi la scheda `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. In **Tipi indicizzati** imposta la **Tipo Composto** a:

   `Product - Product`

1. In **Tipi indicizzati** regolare la **Query indicizzatore** per `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. In **Tipi indicizzati** regolare la **Query indicizzatore** per `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. In **Tipi indicizzati** regolare la `category` sfaccettatura. Fai doppio clic sull’ultima voce nell’elenco delle categorie per aprire la **indicizzato, proprietà** scheda:

   >[!NOTE]
   >
   >Per hybris 5.2 assicurati che il `Facet` nella tabella Proprietà viene selezionato in base alla schermata seguente:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Apri **Impostazioni facet** e regola i valori dei campi:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Salva le modifiche.**
1. Di nuovo da **Tipi di elementi SOLR**, regolare `price` facet secondo le seguenti schermate. Come con `category`, fai doppio clic su `price` per aprire **indicizzato, proprietà** scheda:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Apri **Impostazioni facet** e regola i valori dei campi:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Salva le modifiche.**
1. Apri **Sistema**, **Ricerca dei facet**, quindi **Procedura guidata di indicizzazione**. Avvia un cronjob:

   * **Operazione indicizzatore**: `full`
   * **Configurazione Solr**: `Sample Solr Config for Clothes`

## Configurare la versione del catalogo {#configure-the-catalog-version}

La **Versione catalogo** ( `hybris.catalog.version`) importata può essere configurata per il servizio OSGi:

**Configurazione di Day CQ Commerce Hybris**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Versione catalogo** in genere è impostato su `Online` o `Staged` (impostazione predefinita).

>[!NOTE]
>
>Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete. Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

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

Tale struttura è creata dal servizio OSGi `DefaultImportHandler` che implementa `ImportHandler` interfaccia. Un gestore di importazione viene chiamato dall’importazione effettiva per creare prodotti, varianti di prodotto, categorie, risorse, ecc.

>[!NOTE]
>
>È possibile [personalizzare questo processo implementando il proprio gestore di importazione](#configure-the-import-structure).

La struttura da generare durante l’importazione può essere configurata per:

&quot;**Day CQ Commerce Hybris - Gestore di importazione predefinito**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete. Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Configurare gli attributi di prodotto da caricare {#configure-the-product-attributes-to-load}

Il parser di risposta può essere configurato per definire le proprietà e gli attributi da caricare per i prodotti (variante):

1. Configura il bundle OSGi:

   **Parser di risposta predefinito di Day CQ Commerce Hybris**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Qui puoi definire varie opzioni e attributi necessari per il caricamento e la mappatura.

   >[!NOTE]
   >
   >Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete. Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Importazione dei dati di prodotto {#importing-the-product-data}

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
   1. **Salva tutto** per mantenere il cambiamento.

1. Apri l’importazione di hybris in AEM:

   `/etc/importers/hybris.html`

   Esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configura i parametri richiesti; ad esempio:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Fai clic su **Importa catalogo** per avviare l’importazione.

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
1. Fai clic su **Importa catalogo** per avviare l’importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```


### Aggiornamento espresso {#express-update}

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

1. Seleziona la casella di selezione **Aggiornamento espresso**.
1. Fai clic su **Importa catalogo** per avviare l’importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```

## Configurare l’importazione di catalogo {#configure-the-catalog-importer}

Il catalogo ibrido può essere importato in AEM, utilizzando l’importazione batch per cataloghi, categorie e prodotti ibridi.

I parametri utilizzati dall’importazione possono essere configurati per:

**Importazione Day CQ Commerce Hybris Catalog**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete. Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

## Importazione catalogo {#catalog-import}

Il pacchetto hybris viene fornito con un importatore di catalogo per l’impostazione della struttura della pagina iniziale.

È disponibile da:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Devono essere fornite le seguenti informazioni:

* **Store di base**
Identificatore dell&#39;archivio di base configurato in hybris.

* **Catalogo**
Identificatore del catalogo da importare.

* **Percorso radice**
Percorso in cui importare il catalogo.

## Rimozione di un prodotto dal catalogo {#removing-a-product-from-the-catalog}

Per rimuovere uno o più prodotti dal catalogo:

1. [Configurare il per il servizio OSGi](/help/sites-deploying/configuring-osgi.md) **Importazione Day CQ Commerce Hybris Catalog**; vedi anche [Configurare l’importazione di catalogo](#configure-the-catalog-importer).

   Attiva le seguenti proprietà:

   * **Abilita rimozione prodotti**
   * **Abilita rimozione risorse di prodotto**

   >[!NOTE]
   >
   >Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete. Consulta anche la console per un elenco completo dei parametri configurabili e delle relative impostazioni predefinite.

1. Inizializzare l’importazione eseguendo due aggiornamenti incrementali (vedi [Importazione catalogo](#catalog-import)):

   * La prima esecuzione comporta un set di prodotti modificati, indicato nell’elenco dei registri.
   * Per la seconda volta nessun prodotto deve essere aggiornato.

   >[!NOTE]
   >
   >La prima importazione consiste nell’inizializzare le informazioni di prodotto. La seconda importazione verifica che tutto sia stato lavorato e che il set di prodotti è pronto.

1. Seleziona la pagina della categoria contenente il prodotto da rimuovere. I dettagli del prodotto devono essere visibili.

   Ad esempio, la seguente categoria mostra i dettagli del prodotto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Rimuovi il prodotto dalla console hybris. Utilizza l’opzione **Modifica stato approvazione** per impostare lo stato su `unapproved`. Il prodotto verrà rimosso dal feed live.

   Esempio:

   * Apri la pagina [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Selezionare il catalogo `Outdoors Staged`
   * Cerca `Cajamara`
   * Seleziona questo prodotto e modifica lo stato di approvazione in `unapproved`

1. Esegui un altro aggiornamento incrementale (vedi [Importazione catalogo](#catalog-import)). Il registro elencherà il prodotto eliminato.
1. [Rollout](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) il catalogo appropriato. La pagina prodotto e prodotto sarà stata rimossa da AEM.

   Esempio:

   * Apri:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Rollout del `Hybris Base` catalogo
   * Apri:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * La `Cajamara` il prodotto sarà stato rimosso dal `Bike` categoria

1. Per ripristinare il prodotto:

   1. In hybris, imposta nuovamente lo stato di approvazione su **approvato**
   1. In AEM:

      1. eseguire un aggiornamento incrementale
      1. rollout del catalogo appropriato
      1. aggiorna la pagina della categoria appropriata

## Aggiungi la caratteristica della cronologia degli ordini al contesto client {#add-order-history-trait-to-the-client-context}

Per aggiungere la cronologia degli ordini al [contesto client](/help/sites-developing/client-context.md):

1. Apri [pagina di progettazione del contesto client](/help/sites-administering/client-context.md), mediante:

   * Apri una pagina per la modifica, quindi apri ClientContext utilizzando **Ctrl-Alt-C** (finestre) o **control-option-c** (Mac). Utilizza l’icona a forma di matita nell’angolo in alto a sinistra del contesto client per **Apri la pagina di progettazione del ClientContext**.
   * Passa direttamente a [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Aggiungi il **Cronologia ordini** component](/help/sites-administering/client-context.md#adding-a-property-component) al **Auto Shopping** al componente del contesto client.
1. Puoi confermare che il contesto client sta mostrando i dettagli della cronologia degli ordini. Esempio:

   1. Apri [contesto client](/help/sites-administering/client-context.md).
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
   >* Il segmento viene generato utilizzando la variabile **Proprietà cronologia ordini** caratteristica.

