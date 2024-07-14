---
title: Utilizzo dell'AEM con SAP Commerce Cloud
description: Scopri come utilizzare Adobe Experience Manager con SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 2%

---

# COMMERCE CLOUD SAP{#sap-commerce-cloud}

Dopo l’installazione è possibile configurare l’istanza:

1. [Configura la ricerca di Geometrixx Outdoors con facet](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configura la versione del catalogo](#configure-the-catalog-version).
1. [Configura la struttura di importazione](#configure-the-import-structure).
1. [Configurare gli attributi del prodotto da caricare](#configure-the-product-attributes-to-load).
1. [Importazione dei dati di prodotto](#importing-the-product-data).
1. [Configura Importazione catalogo](#configure-the-catalog-importer).
1. Utilizza l&#39;importazione [ per importare il catalogo](#catalog-import) in una posizione specifica in AEM.

## Configurare la ricerca di Geometrixx Outdoors con facet {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Questo non è necessario per hybris 5.3.0.1 e versioni successive.

1. Nel browser, accedi alla **console di gestione Hybris** all&#39;indirizzo:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Dalla barra laterale, seleziona **Sistema**, quindi **Ricerca facet**, quindi **Configurazione ricerca facet**.
1. **Apri editor** per la **Configurazione Solr di esempio per clothescatalog**.

1. In **Versioni catalogo** utilizzare **Aggiungi versione catalogo** per aggiungere `outdoors-Staged` e `outdoors-Online` all&#39;elenco.
1. **Salva** la configurazione.
1. Apri **Tipi di elementi SOLR** per aggiungere **Ordini SOLR** a `ClothesVariantProduct`:

   * rilevanza (&quot;Rilevanza&quot;, punteggio)
   * name-asc (&quot;Name (ascending)&quot;, name)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Price (ascending)&quot;, priceValue)
   * price-desc (&quot;Prezzo (decrescente)&quot;, priceValue)

   >[!NOTE]
   >
   >Utilizzare il menu di scelta rapida, in genere facendo clic con il pulsante destro del mouse, per selezionare `Create Solr sort`.
   >
   >In Hybris 5.0.0 aprire la scheda `Indexed Types`, fare doppio clic su `ClothesVariantProduct`, quindi sulla scheda `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. Nella scheda **Tipi indicizzati**, impostare **Tipo composto** su:

   `Product - Product`

1. Nella scheda **Tipi indicizzati**, regola le **query indicizzatore** per `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. Nella scheda **Tipi indicizzati**, regola le **query indicizzatore** per `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. Nella scheda **Tipi indicizzati**, regola il facet `category`. Fare doppio clic sull&#39;ultima voce nell&#39;elenco delle categorie per aprire la scheda **Proprietà indicizzata**:

   >[!NOTE]
   >
   >Per hybris 5.2 assicurati che l&#39;attributo `Facet` nella tabella Proprietà sia selezionato in base alla schermata seguente:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Apri la scheda **Impostazioni facet** e regola i valori dei campi:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Salva** le modifiche.
1. Di nuovo da **Tipi di elementi SOLR**, regola il facet `price` in base alle schermate seguenti. Come per `category`, fare doppio clic su `price` per aprire la scheda **Proprietà indicizzata**:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Apri la scheda **Impostazioni facet** e regola i valori dei campi:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Salva** le modifiche.
1. Aprire **Sistema**, **Ricerca facet**, quindi **Procedura guidata operazione indicizzatore**. Avvia un processo cronico:

   * **Operazione indicizzatore**: `full`
   * **Configurazione Solr**: `Sample Solr Config for Clothes`

## Configurare la versione del catalogo {#configure-the-catalog-version}

La **versione del catalogo** ( `hybris.catalog.version`) importata può essere configurata per il servizio OSGi:

Configurazione Hybris **Day CQ Commerce**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Versione catalogo** è impostata su `Online` o `Staged` (impostazione predefinita).

>[!NOTE]
>
>Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; per informazioni dettagliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

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

Tale struttura viene creata dal servizio OSGi `DefaultImportHandler` che implementa l&#39;interfaccia `ImportHandler`. Un gestore di importazione viene chiamato dall’effettivo importatore per creare prodotti, varianti di prodotto, categorie, risorse e così via.

>[!NOTE]
>
>Puoi [personalizzare questo processo implementando un tuo gestore di importazione](#configure-the-import-structure).

La struttura da generare durante l’importazione può essere configurata per:

&quot;**Gestione importazione predefinita Day CQ Commerce Hybris**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; per informazioni dettagliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

## Configurare gli attributi del prodotto da caricare {#configure-the-product-attributes-to-load}

Il parser di risposta può essere configurato per definire le proprietà e gli attributi da caricare per i prodotti (varianti):

1. Configura il bundle OSGi:

   **Day CQ Commerce Hybris Default Response Parser**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Qui puoi definire varie opzioni e attributi necessari per il caricamento e la mappatura.

   >[!NOTE]
   >
   >Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; per informazioni dettagliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

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
>L&#39;implementazione hybris (ovvero `geometrixx-outdoors/en_US`) memorizza solo gli ID prodotto e altre informazioni di base in `/etc/commerce`.
>
>Ogni volta che vengono richieste informazioni su un prodotto, viene fatto riferimento al server ibrido.

### Importazione completa {#full-import}

1. Se necessario, elimina tutti i dati di prodotto esistenti utilizzando CRXDE Lite.

   1. Passare alla sottostruttura contenente i dati del prodotto:

      `/etc/commerce/products`

      Ad esempio:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Eliminare il nodo che contiene i dati del prodotto, ad esempio `outdoors`.
   1. **Salva tutto** per mantenere la modifica.

1. Aprire l’importatore di ibridi in AEM:

   `/etc/importers/hybris.html`

   Ad esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configura i parametri richiesti, ad esempio:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Fai clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completato, puoi verificare i dati importati in:

   ```
       /etc/commerce/products/outdoors
   ```

   Puoi aprirlo in CRXDE Lite; ad esempio:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importazione incrementale {#incremental-import}

1. Controllare le informazioni detenute nell’AEM per i prodotti in questione, nel sottoalbero appropriato alla voce:

   `/etc/commerce/products`

   Puoi aprirlo in CRXDE Lite; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni contenute sui prodotti rilevanti.

1. Aprire l’importatore di ibridi in AEM:

   `/etc/importers/hybris.html`

   Ad esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Selezionare la casella di controllo **Importazione incrementale**.
1. Fai clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```


### Aggiornamento rapido {#express-update}

Il processo di importazione può richiedere molto tempo, pertanto come estensione della sincronizzazione di prodotto puoi selezionare aree specifiche del catalogo per un aggiornamento rapido che viene attivato manualmente. Questo utilizza il feed di esportazione insieme alla configurazione degli attributi standard.

1. Controllare le informazioni detenute nell’AEM per i prodotti in questione, nel sottoalbero appropriato alla voce:

   `/etc/commerce/products`

   Puoi aprirlo in CRXDE Lite; ad esempio:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, aggiornare le informazioni contenute sui prodotti rilevanti.

1. In modalità ibrida, aggiungi uno o più prodotti alla coda Express; ad esempio:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Aprire l’importatore di ibridi in AEM:

   `/etc/importers/hybris.html`

   Ad esempio:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Selezionare la casella di controllo **Aggiornamento rapido**.
1. Fai clic su **Importa catalogo** per avviare l&#39;importazione.

   Una volta completati, puoi verificare i dati aggiornati in AEM in:

   ```
       /etc/commerce/products
   ```

## Configurare la funzione di importazione catalogo {#configure-the-catalog-importer}

Il catalogo ibrido può essere importato in AEM, utilizzando l’importazione batch per i cataloghi ibridi, le categorie e i prodotti.

I parametri utilizzati dall’importazione possono essere configurati per:

**Importazione catalogo ibrido Commerce Day CQ**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; per informazioni dettagliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

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

* **Percorso principale**
Percorso in cui importare il catalogo.

## Rimozione di un prodotto dal catalogo {#removing-a-product-from-the-catalog}

Per rimuovere uno o più prodotti dal catalogo:

1. [Configurare per il servizio OSGi](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris Catalog Importer**; vedere anche [Configurare Catalog Importer](#configure-the-catalog-importer).

   Attiva le seguenti proprietà:

   * **Abilita rimozione prodotto**
   * **Abilita rimozione risorse prodotto**

   >[!NOTE]
   >
   >Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; per informazioni dettagliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md). Consulta anche la console per un elenco completo dei parametri configurabili e dei relativi valori predefiniti.

1. Inizializza l&#39;importazione eseguendo due aggiornamenti incrementali (vedi [Importazione catalogo](#catalog-import)):

   * La prima esecuzione si traduce in un set di prodotti modificati, indicato nell’elenco dei registri.
   * Per la seconda volta, non è necessario aggiornare alcun prodotto.

   >[!NOTE]
   >
   >La prima importazione consiste nell’inizializzare le informazioni sul prodotto. La seconda importazione verifica che tutto abbia funzionato e che il set di prodotti sia pronto.

1. Controllare la pagina della categoria contenente il prodotto che si desidera rimuovere. I dettagli del prodotto devono essere visibili.

   Ad esempio, la seguente categoria mostra i dettagli del prodotto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Rimuovi il prodotto nella console Hybris. Utilizzare l&#39;opzione **Modifica stato approvazione** per impostare lo stato su `unapproved`. Il prodotto viene rimosso dal feed vivo.

   Ad esempio:

   * Apri la pagina [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Seleziona il catalogo `Outdoors Staged`
   * Cerca `Cajamara`
   * Selezionare il prodotto e modificare lo stato di approvazione in `unapproved`

1. Esegui un altro aggiornamento incrementale (vedi [Importazione catalogo](#catalog-import)). Il registro elenca il prodotto eliminato.
1. [Rollout](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) del catalogo appropriato. La pagina del prodotto e quella del prodotto sono state rimosse dall’AEM.

   Ad esempio:

   * Apri:

     [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Rollout del catalogo `Hybris Base`
   * Apri:

     [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * Il prodotto `Cajamara` è stato rimosso dalla categoria `Bike`

1. Per ripristinare il prodotto:

   1. In modalità ibrida, impostare di nuovo lo stato di approvazione su **approvato**
   1. Per l&#39;AEM:

      1. esegui un aggiornamento incrementale
      1. esegui nuovamente il rollout del catalogo appropriato
      1. aggiorna la pagina categoria appropriata

## Aggiungi caratteristica cronologia ordini a ClientContext {#add-order-history-trait-to-the-client-context}

Per aggiungere la cronologia degli ordini al [contesto client](/help/sites-developing/client-context.md):

1. Aprire la [pagina di progettazione del contesto client](/help/sites-administering/client-context.md):

   * Apri una pagina per la modifica, quindi apri il contesto client utilizzando **Ctrl-Alt-c** (Windows) o **Control-Option-c** (Mac). Utilizza l&#39;icona della matita nell&#39;angolo in alto a sinistra del contesto client per **aprire la pagina di progettazione del ClientContext**.
   * Passa direttamente a [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Aggiungere il componente **Cronologia ordini**](/help/sites-administering/client-context.md#adding-a-property-component) al componente **Auto acquisti** t del contesto client.
1. Puoi confermare che nel contesto del cliente sono visualizzati i dettagli della cronologia degli ordini. Ad esempio:

   1. Apri il [contesto client](/help/sites-administering/client-context.md).
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
   >* Passa a [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  La campagna è costituita da un’esperienza.
   >
   >* Fai clic sul segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* Il segmento viene creato utilizzando la caratteristica **Proprietà cronologia ordini**.
