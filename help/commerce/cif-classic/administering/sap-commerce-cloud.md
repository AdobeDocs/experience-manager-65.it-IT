---
title: Utilizzo dell'AEM con SAP Commerce Cloud
description: Scopri come utilizzare Adobe Experience Manager con SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 2%

---

# COMMERCE CLOUD SAP{#sap-commerce-cloud}

Dopo l’installazione è possibile configurare l’istanza:

1. [Configurare la ricerca di Geometrixx Outdoors con facet](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configurare la versione del catalogo](#configure-the-catalog-version).
1. [Configurare la struttura di importazione](#configure-the-import-structure).
1. [Configurare gli attributi del prodotto da caricare](#configure-the-product-attributes-to-load).
1. [Importazione dei dati di prodotto](#importing-the-product-data).
1. [Configurare la funzione di importazione catalogo](#configure-the-catalog-importer).
1. Utilizza il [importazione per importare il catalogo](#catalog-import) in una sede specifica dell’AEM.

## Configurare la ricerca di Geometrixx Outdoors con facet {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Questo non è necessario per hybris 5.3.0.1 e versioni successive.

1. Nel browser, accedi al **console di gestione hybris** a:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Dalla barra laterale, seleziona **Sistema**, quindi **Ricerca facet**, quindi **Configurazione ricerca facet**.
1. **Apri editor** per **Esempio di configurazione Solr per clothescatalog**.

1. Sotto **Versioni del catalogo** utilizzare **Aggiungi versione catalogo** da aggiungere `outdoors-Staged` e `outdoors-Online` all&#39;elenco.
1. **Salva** la configurazione.
1. Apri **Tipi di articoli SOLR** da aggiungere **Ordinamenti SOLR** a `ClothesVariantProduct`:

   * rilevanza (&quot;Rilevanza&quot;, punteggio)
   * name-asc (&quot;Name (ascending)&quot;, name)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Price (ascending)&quot;, priceValue)
   * price-desc (&quot;Prezzo (decrescente)&quot;, priceValue)

   >[!NOTE]
   >
   >Utilizza il menu di scelta rapida (in genere clic con il pulsante destro del mouse) per selezionare `Create Solr sort`.
   >
   >Per Hybris 5.0.0 aprire il `Indexed Types` , fare doppio clic `ClothesVariantProduct`, quindi la scheda `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. In **Tipi indicizzati** , impostare **Tipo composto** a:

   `Product - Product`

1. In **Tipi indicizzati** , regola il **Query indicizzatore** per `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. In **Tipi indicizzati** , regola il **Query indicizzatore** per `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. In **Tipi indicizzati** , regola il `category` sfaccettatura. Fare doppio clic sull&#39;ultima voce dell&#39;elenco delle categorie per aprire **Proprietà indicizzata** scheda:

   >[!NOTE]
   >
   >Per hybris 5.2 assicurarsi che il `Facet` Nella tabella Proprietà l&#39;attributo è selezionato in base alla schermata seguente:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Apri **Impostazioni facet** e regolare i valori dei campi:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Salva** le modifiche.
1. Di nuovo da **Tipi di articoli SOLR**, regola `price` facet in base alle schermate seguenti. Come con `category`, doppio clic `price` per aprire **Proprietà indicizzata** scheda:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Apri **Impostazioni facet** e regolare i valori dei campi:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Salva** le modifiche.
1. Apri **Sistema**, **Ricerca facet**, quindi **Procedura guidata dell&#39;indicizzatore**. Avvia un processo cronico:

   * **Operazione indicizzatore**: `full`
   * **Configurazione Solr**: `Sample Solr Config for Clothes`

## Configurare la versione del catalogo {#configure-the-catalog-version}

Il **Versione catalogo** ( `hybris.catalog.version`) importato può essere configurato per il servizio OSGi:

**Configurazione Day CQ Commerce Hybris**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Versione catalogo** è impostato su `Online` o `Staged` (impostazione predefinita).

>[!NOTE]
>
>Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate. Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

L’output del registro fornisce feedback sulle pagine e sui componenti creati e segnala potenziali errori.

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

Tale struttura viene creata dal servizio OSGi `DefaultImportHandler` che implementa `ImportHandler` di rete. Un gestore di importazione viene chiamato dall’effettivo importatore per creare prodotti, varianti di prodotto, categorie, risorse e così via.

>[!NOTE]
>
>È possibile [personalizza questo processo implementando il tuo handler di importazione](#configure-the-import-structure).

La struttura da generare durante l’importazione può essere configurata per:

&quot;**Gestore importazione predefinito Day CQ Commerce Hybris**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate. Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

## Configurare gli attributi del prodotto da caricare {#configure-the-product-attributes-to-load}

Il parser di risposta può essere configurato per definire le proprietà e gli attributi da caricare per i prodotti (varianti):

1. Configura il bundle OSGi:

   **Parser di risposta predefinito Day CQ Commerce Hybris**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Qui puoi definire varie opzioni e attributi necessari per il caricamento e la mappatura.

   >[!NOTE]
   >
   >Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate. Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

## Importazione dei dati di prodotto {#importing-the-product-data}

Esistono diversi modi per importare i dati del prodotto. I dati del prodotto possono essere importati durante la configurazione iniziale dell’ambiente o dopo aver apportato modifiche ai dati ibridi:

* [Importazione completa](#full-import)
* [Importazione incrementale](#incremental-import)
* [Aggiornamento rapido](#express-update)

Le informazioni effettive sul prodotto importate da hybris sono conservate nell’archivio in:

`/etc/commerce/products`

Le seguenti proprietà indicano il collegamento con l’ibrido:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>L’implementazione ibrida (ovvero `geometrixx-outdoors/en_US`) memorizza solo gli ID prodotto e altre informazioni di base in `/etc/commerce`.
>
>Ogni volta che vengono richieste informazioni su un prodotto, viene fatto riferimento al server ibrido.

### Importazione completa {#full-import}

1. Se necessario, elimina tutti i dati di prodotto esistenti utilizzando CRXDE Liti.

   1. Passare alla sottostruttura contenente i dati del prodotto:

      `/etc/commerce/products`

      Ad esempio:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Elimina il nodo che contiene i dati del prodotto; ad esempio, `outdoors`.
   1. **Salva tutto** per mantenere la modifica.

1. Aprire l’importatore di ibridi in AEM:

   `/etc/importers/hybris.html`

   Ad esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configura i parametri richiesti, ad esempio:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Clic **Importa catalogo** per avviare l&#39;importazione.

   Una volta completato, puoi verificare i dati importati in:

   ```
       /etc/commerce/products/outdoors
   ```

   Puoi aprirlo in CRXDE Liti; ad esempio:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importazione incrementale {#incremental-import}

1. Controllare le informazioni detenute nell’AEM per i prodotti in questione, nel sottoalbero appropriato alla voce:

   `/etc/commerce/products`

   Puoi aprirlo in CRXDE Liti; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni contenute sui prodotti rilevanti.

1. Aprire l’importatore di ibridi in AEM:

   `/etc/importers/hybris.html`

   Ad esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleziona la casella di controllo **Importazione incrementale**.
1. Clic **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```


### Aggiornamento rapido {#express-update}

Il processo di importazione può richiedere molto tempo, pertanto come estensione della sincronizzazione di prodotto puoi selezionare aree specifiche del catalogo per un aggiornamento rapido che viene attivato manualmente. Questo utilizza il feed di esportazione insieme alla configurazione degli attributi standard.

1. Controllare le informazioni detenute nell’AEM per i prodotti in questione, nel sottoalbero appropriato alla voce:

   `/etc/commerce/products`

   Puoi aprirlo in CRXDE Liti; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni contenute sui prodotti rilevanti.

1. In modalità ibrida, aggiungi uno o più prodotti alla coda Express; ad esempio:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Aprire l’importatore di ibridi in AEM:

   `/etc/importers/hybris.html`

   Ad esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleziona la casella di controllo **Aggiornamento rapido**.
1. Clic **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```

## Configurare la funzione di importazione catalogo {#configure-the-catalog-importer}

Il catalogo ibrido può essere importato in AEM, utilizzando l’importazione batch per i cataloghi ibridi, le categorie e i prodotti.

I parametri utilizzati dall’importazione possono essere configurati per:

**Importazione catalogo ibrido Day CQ Commerce**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate. Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

## Importazione catalogo {#catalog-import}

Il pacchetto hybris viene fornito con un’importazione di cataloghi per la configurazione della struttura della pagina iniziale.

È disponibile all&#39;indirizzo:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerce importconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Devono essere fornite le seguenti informazioni:

* **Archivio di base**
Identificatore dell’archivio base configurato in hybris.

* **Catalogo**
Identificatore del catalogo da importare.

* **Percorso directory principale**
Percorso in cui importare il catalogo.

## Rimozione di un prodotto dal catalogo {#removing-a-product-from-the-catalog}

Per rimuovere uno o più prodotti dal catalogo:

1. [Configurare il per il servizio OSGi](/help/sites-deploying/configuring-osgi.md) **Importazione catalogo ibrido Day CQ Commerce**; vedi anche [Configurare la funzione di importazione catalogo](#configure-the-catalog-importer).

   Attiva le seguenti proprietà:

   * **Abilita rimozione prodotto**
   * **Abilita rimozione risorse prodotto**

   >[!NOTE]
   >
   >Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate. Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

1. Inizializza l’importazione eseguendo due aggiornamenti incrementali (consulta [Importazione catalogo](#catalog-import)):

   * La prima esecuzione si traduce in un set di prodotti modificati, indicato nell’elenco dei registri.
   * Per la seconda volta, non è necessario aggiornare alcun prodotto.

   >[!NOTE]
   >
   >La prima importazione consiste nell’inizializzare le informazioni sul prodotto. La seconda importazione verifica che tutto abbia funzionato e che il set di prodotti sia pronto.

1. Controllare la pagina della categoria contenente il prodotto che si desidera rimuovere. I dettagli del prodotto devono essere visibili.

   Ad esempio, la seguente categoria mostra i dettagli del prodotto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Rimuovi il prodotto nella console Hybris. Utilizza l’opzione **Modifica stato approvazione** per impostare lo stato su `unapproved`. Il prodotto viene rimosso dal feed vivo.

   Ad esempio:

   * Apri la pagina [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Seleziona il catalogo `Outdoors Staged`
   * Cerca `Cajamara`
   * Seleziona questo prodotto e modifica lo stato di approvazione in `unapproved`

1. Eseguire un altro aggiornamento incrementale (vedere [Importazione catalogo](#catalog-import)). Il registro elenca il prodotto eliminato.
1. [Rollout](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) il catalogo appropriato. La pagina del prodotto e quella del prodotto sono state rimosse dall’AEM.

   Ad esempio:

   * Apri:

     [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Eseguire il rollout di `Hybris Base` catalogo
   * Apri:

     [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * Il `Cajamara` il prodotto viene rimosso dal `Bike` categoria

1. Per ripristinare il prodotto:

   1. In hybris, imposta di nuovo lo stato di approvazione su **approvato**
   1. Per l&#39;AEM:

      1. esegui un aggiornamento incrementale
      1. esegui nuovamente il rollout del catalogo appropriato
      1. aggiorna la pagina categoria appropriata

## Aggiungi caratteristica cronologia ordini a ClientContext {#add-order-history-trait-to-the-client-context}

Per aggiungere la cronologia degli ordini al [contesto client](/help/sites-developing/client-context.md):

1. Apri [pagina progettazione contesto client](/help/sites-administering/client-context.md), da:

   * Apri una pagina per la modifica, quindi apri il contesto client utilizzando **Ctrl-Alt-C** (Windows) o **control-option-c** (Mac) Utilizza l’icona a forma di matita nell’angolo in alto a sinistra del contesto client per **Apri la pagina di progettazione del ClientContext**.
   * Passa direttamente a [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Aggiungi il **Cronologia ordini** componente](/help/sites-administering/client-context.md#adding-a-property-component) al **Auto** t componente del contesto client.
1. Puoi confermare che nel contesto del cliente sono visualizzati i dettagli della cronologia degli ordini. Ad esempio:

   1. Apri [contesto client](/help/sites-administering/client-context.md).
   1. Aggiungi un articolo al carrello.
   1. Completa il pagamento.
   1. Controlla il contesto del client.
   1. Aggiungi un altro elemento al carrello.
   1. Passare alla pagina di pagamento:

      * Il contesto client mostra un riepilogo della cronologia degli ordini.
      * Viene visualizzato il messaggio &quot;You&#39;re a return customer&quot; (Sei un cliente di ritorno).

   >[!NOTE]
   >
   >Il messaggio viene realizzato da:
   >
   >* Accedi a [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  La campagna è costituita da un’esperienza.
   >
   >* Fai clic sul segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* Il segmento viene creato utilizzando **Proprietà cronologia ordini** caratteristica.
