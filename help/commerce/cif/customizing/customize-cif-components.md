---
title: Personalizzare i componenti core CIF
description: Scopri come personalizzare i componenti core CIF di Adobe Experience Manager. Il tutorial illustra come estendere in modo sicuro un componente core CIF per soddisfare i requisiti aziendali specifici. Scopri come estendere una query GraphQL per restituire un attributo personalizzato e visualizzare il nuovo attributo in un componente core CIF.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 8933942e-be49-49d3-bf0a-7225257e2803
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 12%

---

# Personalizzare i componenti core CIF di Adobe Experience Manager {#customize-cif-components}

Il [Progetto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) è una base di codice di riferimento per l’utilizzo di [Componenti core CIF](https://github.com/adobe/aem-core-cif-components). In questo tutorial, puoi estendere ulteriormente il [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) per visualizzare un attributo personalizzato da Adobe Commerce. Scoprirai anche come integrare GraphQL tra Adobe Experience Manager (AEM) e Adobe Commerce e gli hook di estensione forniti dai componenti core CIF.

>[!TIP]
>
>Utilizza il [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) all’avvio dell’implementazione di commerce.

## Cosa verrà creato

Il marchio Venia ha recentemente iniziato a produrre alcuni prodotti utilizzando materiali sostenibili e l&#39;azienda desidera mostrare un **Rispettoso dell&#39;ambiente** come parte del Product Teaser. In Adobe Commerce viene creato un nuovo attributo personalizzato per indicare se un prodotto utilizza **Rispettoso dell&#39;ambiente** materiale. Questo attributo personalizzato viene aggiunto come parte della query GraphQL e visualizzato nel Product Teaser per i prodotti specificati.

![Implementazione finale del badge eco-compatibile](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Prerequisiti {#prerequisites}

Per completare questa esercitazione è necessario un ambiente di sviluppo locale. Ciò include un’istanza in esecuzione dell’AEM configurata e connessa a un’istanza Adobe Commerce. Rivedi i requisiti e i passaggi per [sviluppo locale con l&#39;AEM](../develop.md). Per seguire completamente l’esercitazione, è necessario disporre delle autorizzazioni per aggiungere [Attributi di un prodotto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) in Adobe Commerce.

È inoltre necessario GraphQL IDE, ad esempio [GraphiQL](https://github.com/graphql/graphiql) o un’estensione del browser per eseguire gli esempi di codice e i tutorial. Se installi un’estensione del browser, accertati che sia in grado di impostare le intestazioni della richiesta. Su Google Chrome, [Client Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) è un’estensione che può eseguire il processo.

## Clonare il progetto Venia {#clone-venia-project}

Clonerai il [Progetto Venia](https://github.com/adobe/aem-cif-guides-venia) e quindi ignorare gli stili predefiniti.

>[!NOTE]
>
>**Puoi utilizzare un progetto esistente** (in base all’archetipo del progetto AEM con CIF incluso) e salta questa sezione.

1. Esegui il seguente comando Git per clonare il progetto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza Adobe Commerce o aggiungi le configurazioni al progetto appena creato.

1. A questo punto, devi disporre di una versione funzionante di una vetrina connessa a un’istanza di Adobe Commerce. Accedi a `US` > `Home` pagina in: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandendo il menu principale della vetrina, dovresti vedere diverse categorie, a indicare che la connessione ad Adobe Commerce funziona.

   ![Vetrina configurata con il tema Venia](../assets/customize-cif-components/venia-store-configured.png)

## Creare il Product Teaser {#author-product-teaser}

Il componente Product Teaser viene esteso in tutta questa esercitazione. Come primo passo, aggiungi un’istanza del Product Teaser alla home page per comprenderne le funzionalità della linea di base.

1. Passa alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Inserisci un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserire Product Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. Espandi il pannello laterale (se non è già attivato) e imposta il menu a discesa di ricerca risorse su **Prodotti**. Dovrebbe essere visualizzato un elenco dei prodotti disponibili da un’istanza di Adobe Commerce connessa. Seleziona un prodotto e **trascinalo** sul componente **Product Teaser** nella pagina.

   ![Trascinare su Product Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   >Puoi anche configurare il prodotto visualizzato impostando il componente tramite la finestra di dialogo (clic sull’icona a forma di _chiave inglese_).

4. Ora puoi vedere un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Product Teaser - stile predefinito](../assets/customize-cif-components/product-teaser-default-style.png)

## Aggiungere un attributo personalizzato in Adobe Commerce {#add-custom-attribute}

I prodotti e i dati dei prodotti visualizzati nell’AEM sono memorizzati in Adobe Commerce. Aggiungi un nuovo attributo per **Rispettoso dell&#39;ambiente** come parte dell’attributo del prodotto impostato utilizzando l’interfaccia utente di Adobe Commerce.

>[!TIP]
>
>Hai già un **Sì/No** come parte del set di attributi del prodotto? Puoi utilizzarlo e saltare questa sezione.

1. Accedi all’istanza di Adobe Commerce.
1. Accedi a **Catalogo** > **Prodotti**.
1. Aggiorna il filtro di ricerca per trovare **Prodotto configurabile** utilizzato quando aggiunto al componente Teaser nell’esercizio precedente. Apri il prodotto in modalità di modifica.

   ![Cerca prodotto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. Dalla vista prodotto, fai clic su **Aggiungi attributo** > **Crea nuovo attributo**.
1. Compila il **Nuovo attributo** modulo con i seguenti valori (lasciare le impostazioni predefinite per gli altri valori)

   | Set di campi | Etichetta campo | Valore |
   | ----------------------------- | ------------------ | ---------------- |
   | Proprietà attributo | Etichetta attributo | **Rispettoso dell&#39;ambiente** |
   | Proprietà attributo | Tipo di input catalogo | **Sì/No** |
   | Proprietà attributi avanzate | Codice attributo | **eco_friendly** |

   ![Modulo nuovo attributo](../assets/customize-cif-components/attribute-new-form.png)

   Clic **Salva attributo** al termine.

1. Scorri fino alla parte inferiore del prodotto ed espandi il **Attributi** intestazione. Dovresti visualizzare il nuovo **Rispettoso dell&#39;ambiente** campo. Passa a **Sì**.

   ![Passa a yes](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Salva** le modifiche apportate al prodotto.

   >[!TIP]
   >
   >Ulteriori dettagli sulla gestione [Gli attributi del prodotto sono disponibili nella guida utente di Adobe Commerce.](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Accedi a **Sistema** > **Strumenti** > **Gestione cache**. Poiché è stato effettuato un aggiornamento allo schema dati, è necessario invalidare alcuni dei tipi di cache in Adobe Commerce.
1. Seleziona la casella accanto a **Configurazione** e invia il tipo di cache per **Aggiorna**

   ![Aggiorna tipo cache configurazione](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   >Ulteriori dettagli su [La gestione della cache è disponibile nella guida utente di Adobe Commerce](https://docs.magento.com/user-guide/system/cache-management.html).

## Utilizzare un IDE GraphQL per verificare l&#39;attributo {#use-graphql-ide}

Prima di passare al codice AEM, è utile esplorare i [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) utilizzo di un IDE GraphQL. L’integrazione di Adobe Commerce con l’AEM viene eseguita principalmente tramite una serie di query GraphQL. Comprendere e modificare le query di GraphQL è uno dei modi chiave con cui è possibile estendere i Componenti core dell’CIF.

Quindi, utilizza un IDE di GraphQL per verificare che `eco_friendly` L&#39;attributo è stato aggiunto al set di attributi del prodotto. Le schermate di questo tutorial utilizzano [Client Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Apri l’IDE di GraphQL e immetti l’URL `http://<server>/graphql` nella barra URL dell’IDE o dell’estensione.
2. Aggiungi quanto segue [query prodotti](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) dove `YOUR_SKU` è il **SKU** del prodotto utilizzato nell&#39;esercizio precedente:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Esegui la query e dovresti ricevere una risposta simile alla seguente:

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![Risposta GraphQL di esempio](../assets/customize-cif-components/sample-graphql-query.png)

Il valore di **Sì** è un numero intero di **1**. Questa funzione è utile quando scrivi la query GraphQL in Java™.

>[!TIP]
>
>Documentazione più dettagliata su [Adobe Commerce GraphQL è disponibile qui](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Aggiornare il modello Sling per Product Teaser {#updating-sling-model-product-teaser}

Ora estenderai la logica di business del Product Teaser implementando un modello Sling. [Modelli Sling](https://sling.apache.org/documentation/bundles/models.html), sono &quot;POJO&quot; (Plain Old Java™ Objects) basati su annotazioni che implementano la logica di business necessaria per il componente. I modelli Sling vengono utilizzati con gli script HTL come parte del componente. Seguirai le [pattern di delega per modelli Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) in modo da poter estendere parti del modello esistente di Product Teaser.

I modelli Sling sono implementati come Java™ e si trovano in **core** del progetto generato.

Utilizzare [l&#39;IDE di tua scelta](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) per importare il progetto Venia. Le schermate utilizzate provengono da [IDE codice Visual Studio](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?#microsoft-visual-studio-code).

1. Nell’IDE, passa alla sezione **core** modulo a: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE posizione core](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` è un’interfaccia Java™ che estende l’CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) di rete.

   È già stato aggiunto un nuovo metodo denominato `isShowBadge()` per visualizzare un badge se il prodotto è considerato &quot;Nuovo&quot;.

1. Aggiungi il nuovo metodo `isEcoFriendly()` all’interfaccia:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

Questo è un nuovo metodo per incapsulare la logica per indicare se il prodotto ha `eco_friendly` attributo impostato su **Sì** o **No**.

1. Quindi, controlla `MyProductTeaserImpl.java` a `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   Il [pattern di delega per modelli Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) consente `MyProductTeaserImpl` a riferimento `ProductTeaser` tramite il `sling:resourceSuperType` proprietà:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Per tutti i metodi che non vengono sostituiti o modificati, puoi restituire il valore che `ProductTeaser` restituisce. Ad esempio:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Questo riduce al minimo la quantità di codice Java™ che un’implementazione deve scrivere.

1. Uno dei punti di estensione aggiuntivi forniti dai Componenti core CIF dell’AEM è `AbstractProductRetriever` che consente di accedere ad attributi di prodotto specifici. Inspect `initModel()` metodo:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   Il `@PostConstruct` L’annotazione assicura che questo metodo venga chiamato quando il modello Sling viene inizializzato.

   La query GraphQL del prodotto è già stata estesa utilizzando `extendProductQueryWith` per recuperare i dati aggiuntivi `created_at` attributo. Questo attributo viene in seguito utilizzato come parte del `isShowBadge()` metodo.

1. Aggiorna la query GraphQL per includere `eco_friendly` attributo nella query parziale:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   Aggiunta a `extendProductQueryWith` è un metodo efficace per garantire che gli attributi di prodotto aggiuntivi siano disponibili per il resto del modello. Inoltre si riduce la quantità di query eseguite.

   Nel codice riportato sopra, il`addCustomSimpleField` viene utilizzato per recuperare `eco_friendly` attributo. Questo illustra come eseguire una query per gli attributi personalizzati che fanno parte dello schema di Adobe Commerce.

   >[!NOTE]
   >
   >Il `createdAt()` è stato implementato come parte del [Interfaccia prodotto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). La maggior parte degli attributi dello schema comunemente trovati è già stata implementata, quindi utilizza solo gli attributi `addCustomSimpleField` per gli attributi realmente personalizzati.

1. Aggiungi un logger per facilitare il debug del codice Java™:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Quindi, implementa `isEcoFriendly()` metodo:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   Nel metodo precedente, il `productRetriever` viene utilizzato per recuperare il prodotto e il `getAsInteger()` viene utilizzato per ottenere il valore del `eco_friendly` attributo. In base alle query GraphQL eseguite in precedenza, sai che il valore previsto quando `eco_friendly` è impostato su &quot;**Sì**&quot; è un numero intero di **1**.

   Ora che il modello Sling è stato aggiornato, è necessario aggiornare il markup del componente per visualizzare effettivamente un indicatore di **Rispettoso dell&#39;ambiente** basato sul modello Sling.

## Personalizzazione del markup del Product Teaser {#customize-markup-product-teaser}

I componenti AEM vengono spesso estesi per modificare il markup generato dal componente. A tal fine, sovrascrivi lo [script HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it) utilizzato dal componente per eseguire il rendering del relativo markup. HTL (HTML Template Language) è un linguaggio per modelli leggero utilizzato dai componenti AEM per eseguire il rendering dinamico del markup in base al contenuto creato, che consente di riutilizzare i componenti. Il Product Teaser, ad esempio, può essere riutilizzato più volte per visualizzare prodotti diversi.

In questo caso, desideri applicare un banner sopra il teaser per indicare che il prodotto è &quot;eco-compatibile&quot; in base a un attributo personalizzato. Il modello di progettazione per [personalizzare il markup](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) di un componente è in realtà standard per tutti i componenti di AEM, non solo per i componenti core CIF di AEM.

>[!NOTE]
>
>Se personalizzi un componente utilizzando i selettori di prodotti e categorie dell’CIF come questo Product Teaser o il componente pagina dell’CIF, assicurati di includere i `cif.shell.picker` clientlib per le finestre di dialogo del componente. Consulta [Utilizzo del selettore di prodotti e categorie CIF](use-cif-pickers.md) per i dettagli.

1. Nell’IDE, esplora ed espandi la `ui.apps` ed espandere la gerarchia delle cartelle in modo da: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e ispezionare `.content.xml` file.

   ![Product Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   La definizione del componente Product Teaser in questo progetto è riportata sopra. Osserva la proprietà `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Questo è un esempio di creazione di un [componente Proxy](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components). Invece di copiare e incollare tutti gli script HTL di Product Teaser dai componenti core CIF dell’AEM, puoi utilizzare `sling:resourceSuperType` per ereditare tutte le funzionalità.

1. Apri il file `productteaser.html`. Questa è una copia di `productteaser.html` file da [Product Teaser CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Il modello Sling per `MyProductTeaser` viene utilizzato e assegnato al `product` variabile.

1. Modifica `productteaser.html` per effettuare una chiamata al `isEcoFriendly` metodo applicato nell&#39;esercizio precedente:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   Quando si chiama un metodo Sling Model in HTL, `get` e `is` parte del metodo viene eliminata e la prima lettera viene convertita in minuscolo. Quindi `isShowBadge()` diventa `.showBadge` e `isEcoFriendly` diventa `.ecoFriendly`. In base al valore booleano restituito da `.isEcoFriendly()` determina se `<span>Eco Friendly</span>` viene visualizzato.

   Ulteriori informazioni su `data-sly-test` e altro [Le istruzioni del blocco HTL sono disponibili qui](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. Salva le modifiche e distribuisci gli aggiornamenti a AEM utilizzando le tue competenze Maven, da un terminale della riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Apri una nuova finestra del browser e passa a AEM e al **Console OSGi** > **Stato** > **Modelli Sling**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Cerca `MyProductTeaserImpl` e dovresti vedere una riga simile alla seguente:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Questo indica che il modello Sling è stato distribuito correttamente e mappato al componente corretto.

1. Aggiorna a **Home page Venia** a [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) in cui è stato aggiunto il Product Teaser.

   ![Messaggio eco-compatibile visualizzato](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Se il prodotto ha `eco_friendly` attributo impostato su **Sì**, sulla pagina dovrebbe essere visualizzato il testo &quot;Rispettoso dell&#39;ambiente&quot;. Prova a passare a prodotti diversi per vedere come cambia il comportamento.

1. Quindi, apri l&#39;AEM `error.log` per visualizzare le istruzioni di registro aggiunte. Il `error.log` è in `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Cerca nei registri AEM per visualizzare le istruzioni di registro aggiunte nel modello Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   >Inoltre, potresti vedere alcune tracce dello stack se il prodotto utilizzato nel teaser non ha la proprietà `eco_friendly` come parte del relativo set di attributi.

## Aggiungi stili per il badge eco-compatibile {#add-styles}

A questo punto, la logica per la visualizzazione del **Rispettoso dell&#39;ambiente** Il badge funziona, tuttavia il testo normale potrebbe utilizzare alcuni stili. Quindi aggiungi un’icona e degli stili al `ui.frontend` per completare l&#39;implementazione.

1. Scarica il file [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) file. Viene utilizzato come **Rispettoso dell&#39;ambiente** distintivo.
1. Torna all’IDE e passa a `ui.frontend` cartella.
1. Aggiungi il `eco_friendly.svg` file in `ui.frontend/src/main/resources/images` cartella:

   ![Eco-Friendly SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Apri il file `productteaser.scss` a `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Aggiungi le seguenti regole Sass all’interno del `.productteaser` classe:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   >Estrai [Stile dei componenti core dell’CIF](./style-cif-component.md) per ulteriori dettagli sui flussi di lavoro front-end.

1. Salva le modifiche e distribuisci gli aggiornamenti a AEM utilizzando le tue competenze Maven, da un terminale della riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Aggiorna a **Home page Venia** a [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) in cui è stato aggiunto il Product Teaser.

   ![Implementazione finale del badge eco-compatibile](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Complimenti {#congratulations}

Hai personalizzato il tuo primo componente AEM CIF. Scarica il file [file di soluzione completati qui](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Sfida bonus {#bonus-challenge}

Rivedi la funzionalità di **Nuovo** badge già implementato nel Product Teaser. Prova ad aggiungere una casella di controllo aggiuntiva che consenta agli autori di controllare quando **Rispettoso dell&#39;ambiente** deve essere visualizzato il badge. Aggiorna la finestra di dialogo del componente in `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuova sfida per l’implementazione del badge](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Risorse aggiuntive {#additional-resources}

- [AEM Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)
- [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalizzazione dei componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalizzazione dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=it)
- [Guida introduttiva di AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)
- [Utilizzo del selettore di prodotti e categorie CIF](use-cif-pickers.md)
